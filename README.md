# zoomoid.de website repository

This GitLab repository is used to dockerize and deploy the webpage to my virtual server

This is an experiment to test DevOps using GitLab's Runner on a single virtual server. Supervision is done using nginx as an outer reverse proxy to route incoming traffic into docker container build from this application. 

VueJS uses webpack to produce a production build. Every required file is bundled into a nginx:alpine docker image (light-weight, 20MB max. size). After primary build stage, the container is deployed to the production environment (<https://www.zoomo.id/>), or, based on the branch we pushed to, the staging environment (<https://staging.zoomo.id/>).

A testing stage COULD be integrated, IF there was actually anything to test programmatically. Since this is currently only a static front-end, testing is (kinda) overkill for this scale of website. Future plans to implement a back-end REST API to serve resources etc. could benefit from a testing stage for the back-end code. 

(c) 2019 Alexander Bartolomey
