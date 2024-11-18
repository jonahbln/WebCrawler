Web Crawler - README
- High-Level Approach:
This is a web crawler intended to visit all of the pages in https://fakebook.khoury.northeastern.edu/ in search of 5 secret flags. It uses HTTP 1.1 requests to communicate with the server, which has been implemented from scratch without the use of any prefab HTTP libraries.

Breakdown of the Program Flow -
1. Initialization:
An SSL-wrapped connection is made to the given server, and port (or default if none provided). 

2. Log in:
The login page is requesting using a GET, and CSRF tokens are extracted from the response. Then using the given username and password, an HTTP POST request is formulated and sent to the server to log in.

3. Crawl:
Session ID is scraped from the response, and a list of crawlable sites are extracted. Then, recursively, each site on the list is crwalled, and additional crawlable sites are accumulated. Errors are handled gracefuly as necessary. Each site is searched for the secret flags, until all 5 flags have been found and printed out.

4. Closure:
Once all 5 flags are recieved, the program exits gracefully and the socket is closed.

- Challenges Faced:
1. HTTP can be a little finicky when it comes to making requests in the exact right format. If you hve any tiny mistake in your request, it will not be successful, and debugging the issues has been tricky and time consuming. 

2. The CSRF token was easy enough to find, but we didnt realize there were two different tokens, and that they were both significant and had to be used. This took some time to figure out.

3. Getting the crawl loop logic to work out such that every single site is searched without loops or skipping any was a little tough.

Testing Approach -
- The router was thoroughly tested incrementally at each step along the way:
- first check if connection is successfully initialized
- then check if we can login properly
- then try crawling just one site
- then ramp it up to recursive crawling
- then test it all together, terminating only once all flags are found