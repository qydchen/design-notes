## Hashing

Hashing and modding by servers is not reliable as if one server goes down it throws the logic out

Consistent hashing + Rendevous Hashing fixes that problem

### Consistent Hashing

A type of hashing that minimizes the number of keys that need to be remapped when a hash table gets resized. It's often used by load balancers to distribute traffic to servers; it minimizes the number of requests that get forwarded to different servers when new servers are added or when existing servers are brought down

### Rendevous Hashing (highest random weight)

Allows for minimal-redistribution of mappings when a server goes down. Calculate scores for your servers

Below, suppose `s5` is a server and it breaks down, the rendevous method ensures that the usernames `u0` and `u5` will be instead mapped to the next highest ranking server, which would be `s4`

```js
const serverSet1 = ['s0', 's1', 's2', 's3', 's4', 's5'];
const serverSet2 = ['s0', 's1', 's2', 's3', 's4'];
const usernames = [
  'u0',
  'u1',
  'u2',
  'u3',
  'u4',
  'u5',
  'u6',
  'u7',
  'u8',
  'u9',
  'u10',
];

function pickServerRendevous(username, server) {
  let maxServer = null;
  let maxScore = null;
  for (const server of servers) {
    const score = utils.computeScore(username, server);
    if (maxScore === null || score > maxScore) {
      maxScore = score;
      maxServer = server;
    }
  }
  return maxServer;
}

for (const username of usernames) {
  const server1 = pickServerRendezvous(username, serverSet1);
  const server2 = pickServerRendezvous(username, serverSet2);
  const serversAreEqual = server1 === server2;
  console.log(
    `${username}: ${server1} => ${server2} | equal: ${serversAreEqual}`
  );
}
```
