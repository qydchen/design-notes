Design Reddit API

User

- userId: string

SubReddit

- subredditId: string

What kind of ui screen will consume this api? /r/wallstreetbets, all posts associated with wsb? each post has many comments, comments have many comments

Will we support upvote + downvote?

WIll we support moderators?

Are we supporting the CRUD operations of posts?

Entities:

User

- userId: string
- username: string
- password_digest: string (hashified password digest)
- last_logged_in: timestamp
- created_at: timestamp

SubReddit

- subredditId: string
- subreddit_name: string
- subreddit_creator: User

Posts

- postId: string
- subredditId: string
- creatorId: string (aka userId)
- commentIds: string[]
- content: string
- vote_count: integer
- created_at: timestamp

Comment

- commentId: string
- content: string
- created_at: timestamp
- vote_count: integer
- commentIds: string[]

Is there any other functionality of a subreddit that we should design? (missed this clarifying question)

Award

- awardId: string;
- userId: string;
- special_currency_amount: int;
- entities_awarded: string[] {ids of posts and comments}

caveat: ensure all ids of posts and comments are inclusively unique

api.reddit.com/v1

GET /user/:id
GET /user/:id/posts
GET /user/:id/posts/:id
GET /user/:id/subreddit/:id/posts/:id

GET /posts
GET /posts/:id
POST /posts/:subredditId
UPDATE /posts/:id
DELETE /posts/:id

GET /comments
GET /comments/:id
POST /comments/
UPDATE /comments/:id
DELETE /comments/:id

POST /vote
{
"on": "comment" {comment, post}
"entity_id": 1234 (the entity id of what we are upvoting)
"user_id": 4321 (ensure user can only vote on an entity once)
"vote": 1 (+1, -1)
}
