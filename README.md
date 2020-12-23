# Facebook Product Architecture

## Behavioral Interview

- Have you learned from mistakes and grown as a result?
- Do you generally assume positive intent?
- Do you have passion of enthusiasm for some area of technology?
- Overall will you add to your positive workplace environment and culture for example...
- Do you resolve conflicts in ways that match the company's culture?
- Are you excited about the company mission and/or specific teams?

## Architecture & Design

- Design is about strategy, coding is about tactics
- More diagrams, less code

#

## Build a tool/product to shorten URL - Bitly example

<br>
2 functions; How do we make short URLs, URL resolution (serving URLs)

Focus on user interactions

Make sure this scales, FB type scale, clear path for users, what APIs
do we need, error cases

<br>

### Functional Requirements

- Fast, reliable, scale
- Set short urls
- Servicing the redirections for these URLs

### User requirements

- Arbitrary text (url) -> expect output
- Give us a url -> expect redirection
- Security (ddos), deceitful urls

Webservers

- Creating URLs
  - User provide URLs, output a short urls,
- Servicing URLs
  - Give short URLs, redirect to appropriate website, or error landing page

Load Balancer

Service 1 URL Creation

Service 2 URL Serving

Store URLs (Distributed, sharded)

### Method

- Hashing (caches redundant urls)
  - main thing to think about - collisions
  - napkin math: A-z 52 letters, assume 20 characters => 52^20 unique identifiers
  - collisions can be resolved internally
- youtube.com -> youtu.be
  - can also hash namespaces
- Specify their own URLs

### Scale

- Assumption: DAU -> 1 billion consuming URLs
- Assumption: 10 million new URLs/day
- Writing QPS 10m/86400
- Reading QPS 10k/s <- cache
- Storage 50% repeats, 5 million new/day, 1.5G, 100KB, 150TB

### Database Schema

- `Long URL, Short URL`
- `Varchar, varchar(20)`
- `expiration_date, timestamp`
- `Request_ID bigint`
- `Counter int` (for telemetry nice to have)
- `Namespaces enum`

makeNewURL (longURL string, request ID bigint)

respondWithURL (shortURL string, errorMessage)

#

## FAQ

Is it required to actually draw diagrams?
leverage the current medium, get acclimated to your communication medium (drawing arrows etc.)

Is it expected to solve the problem completely?
no, but have a holistic picture that we need to care about
