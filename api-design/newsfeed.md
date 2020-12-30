# Design a social media newsfeed

- What part of the newsfeed are we designing?
  - Focus on core functionality: updating posts, creating post, how and when it gets constructed, loading posts

1bn users, 10m status updates/day, 500 average friends/user

- Are we ok with having location-based discrepancies?
  - Posting something in the same region of a friend, that friend can see the post asap
  - Posting something in a different region of a friend, that friend can can see the post a bit later
- Posts have to be persistent
- Availability (no need for High Availability)
- Assuming 10kb per post, 1000 posts => 10 mb / newsfeed

#

### <u>Regional System</u>

<br>

Client calls the API servers, which will then call into main database.

API servers are load balanced, hashed by userid. Round Robin

Main db with posts and users stored.

Shards with newsfeeds for particular users.

Shards are hashed by user id, where load balancer will read by hash.

Ranking algo service fetches a bunch of posts from the db, aggregates, generates newsfeed and sends to the shards on a recurring basis. Feed will also likely get paginated.

Store news feeds in 1000 shards carrying 10 terabytes each in disk.

Pub/sub system used to notify that there is an update in the main db (act as a bridge between the write & read). Needs all of the posts to appear in all of those feeds. 1000 feeds to be notified in real time of a new post. Have shards subscribe to pub/sub topics.

Pub/sub topic will be hashed similar to the shards, and input will be user id. The topics will be mapped into each shard.

API server writes into main db, once that is done, then publish to topics of user's friends, userid hashed. (if there are 500 friends, send 500 topics).

Wiring Updates Into Feed Creation

We now need to have a notification mechanism that lets the feed shards know that a new relevant post was just created and that they should incorporate it into the feeds of impacted users.

We can once again use a Pub/Sub service for this. Each one of the shards will subscribe to its own topic--we'll call these topics the Feed Notification Topics (FNT)--and the original subscribers S1 will be the publishers for the FNT. When S1 gets a new message about a post creation, it searches the main database for all of the users for whom this post is relevant (i.e., it searches for all of the friends of the user who created the post), it filters out users from other regions who will be taken care of asynchronously, and it maps the remaining users to the FNT using the same hashing function that our GetNewsFeed load balancers rely on.

For posts that impact too many people, we can cap the number of FNT topics that get messaged to reduce the amount of internal traffic that gets generated from a single post. For those big users we can rely on the asynchronous feed creation to eventually kick in and let the post appear in feeds of users whom we've skipped when the feeds get refreshed manually.

### Cross Regions

When CreatePost gets called and reaches our Pub/Sub subscribers, they'll send a message to another Pub/Sub topic that some forwarder service in between regions will subscribe to. The forwarder's job will be, as its name implies, to forward messages to other regions so as to replicate all of the CreatePost logic in other regions. Once the forwarder receives the message, it'll essentially mimic what would happen if that same CreatePost were called in another region, which will start the entire feed-update logic in those other regions. We can have some additional logic passed to the forwarder to prevent other regions being replicated to from notifying other regions about the CreatePost call in question, which would lead to an infinite chain of replications; in other words, we can make it such that only the region where the post originated from is in charge of notifying other regions.

Several open-source technologies from big companies like Uber and Confluent are designed in part for this kind of operation.
