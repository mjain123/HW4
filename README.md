# HW4 - AUTO DEPLOYMENT AND SWITCH

SUB REPOSITORIES -

Deployment - Main application. Manages requests to blue and green slices of repository HW4-App (Redis-Queues-Proxy)

HW4-App - Replication of repository Redis-Queues-Proxy. 

Code file - infrastructure.js

Execution instructions:

1. Execute two redis instances at port 6379 and port 6380.
2. git clone deployment report and execute npm install
3. Execute node infrastructure.js

TASKS:

Complete git/hook setup for triggering deployment on push.

Performed tasks as mentioned in the [Deployment Workshop]

![image1](/images/bluegreeninfrastructure.JPG

* Create blue/green infrastructure for deployment, including a blue redis instance and green redis instance.

Executed redis server on ports 6379 and 6380.
Updated redis client in blue-www/main.js to connect to 6379 and redis client in green-www/main.js to connect to 6380.

BLUE
`var client = redis.createClient(6379, '127.0.0.1', {});`
GREEN
`var client = redis.createClient(6380, '127.0.0.1', {});`


* Default infrastructure will route traffic to the blue instance.

Default setup in infrastructure.js
1. Primary Target = Blue
2. Secondary Target = Green
3. Flag = 0 (Off)

* Introduce a new route, `/switch`, that will trigger a switch from "blue" to "green" and vice versa.

New route `/switch` accepts get requests and triggers switch between Primary and Secondary Target based on their values.

* Recall, the `/upload` and `/meow` routes.  Extend `/switch` so that if a redis instance currently has values in the picture list, then migrate those instances over to the new instance.

Extended `/switch` to support the above request. When the current slice has values in the picture list and a `/switch` request is received, using lrange command, all the values in the redis instance is retrieved and lpush they are pushed to the new connected instance.

* Introduce a feature flag in the application, "mirroring", which when turned on, will forward information added to the picture list, to the other slice.

To handle "mirroring", a 'flag' has been introduced and set to 0 by default. If the value of flag is set to 1, the requests received are forwarded to primary and secondary target both. Thus, if an image upload (`/upload`) or image retrieve (`meow`) is executed, the request is executed at both the blue and green servers. Hence, at any instance, the data at both the slices will be the same.




[Deployment Workshop]: https://github.com/CSC-DevOps/Deployment
