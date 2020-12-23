## Client - Server Model

- What happens when you open up google.com?
  - A `client` is a machine that speaks to a server
  - A `server` is a machine that receives data from a client, and responds data to the client
  - When you type `www.google.com` on the browser, the browser makes a `DNS query`, to find out what the IP address is
    - An `IP address` is an unique identifier for a machine
    - For example, in Google Cloud Platform, I reserved an IP address for my server that hosts my HTML/JavaScript
    - try `dig` command (`nslookup` for windows)
  - Once the `DNS query` is called, the client will know to make an `HTTP request` to the server
  - Once the server receives the request, it will know to respond to the IP address to send its response to
  - Based on convention invented long ago, the client will know to make an HTTP request to the server on port `80`, for HTTPS requests port `443`
  - Once the server receives the HTTP request, it will then respond with HTML/JavaScript to the browser/client and the browser will then render the HTML/JavaScript
