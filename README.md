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


* Create blue/green infrastructure for deployment, including a blue redis instance and green redis instance.
* Default infrastructure will route traffic to the blue instance.
* Introduce a new route, `/switch`, that will trigger a switch from "blue" to "green" and vice versa.
* Recall, the `/upload` and `/meow` routes.  Extend `/switch` so that if a redis instance currently has values in the picture list, then migrate those instances over to the new instance.
* Introduce a feature flag in the application, "mirroring", which when turned on, will forward information added to the picture list, to the other slice.
