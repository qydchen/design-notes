# Design a social media newsfeed

- What part of the newsfeed are we designing?
  - Focus on core functionality: updating posts, creating post, how and when it gets constructed, loading posts

1bn users, 10m status updates/day, 500 average friends/user

- Are we ok with having location-based discrepancies?

  - Posting something in the same region of a friend, that friend can see the post asap
  - Posting something in a different region of a friend, that friend can can see the post a bit later

- Posts have to be persistent
- Availability (no need for High Availability)
