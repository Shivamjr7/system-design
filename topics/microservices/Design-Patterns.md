## Shared database pattern

## Database per service pattern

## API Gateway

## Service registry and discovery

## Service Mesh

## Backend for frontend pattern

## Distributed transactions 

## Distributed consensus


## Leader election algorithm

## LCR algorithm for leader election 

* Every node needs to know about the next node in clockwise direction
* Every node is assigned a UID 
* Each node forwards its UID to next node
* The node compares the UID of the prev to its UID , if it is smaller it ignores and forwards its UID
* If it is equal , it forwards the UID 
* Once a node sees back its UID , it declares itself as the leader and sends a message to stop the election
* Complexity : O(n2)


# Rate Limiting and Throttling

* Throttling : technique that ensures the data/request sent to the target system is sent at a rate which is acceptable to the target system
* Rate limiter is a component which kicks in which ensures the data sent to the target system is at acceptable rate 
* Throttler could slow down the requests if there are too many or can reject or ignore

## Why do we need throttling?
* Preventing abuse of endpoints/systems
* Only allow traffic that can be handled
* Control consumption cost : in case of large no of requests coming it would increase cpu usage , memory
* Also in the above case if you are running EC2 instances or cloud , it would lead to spin up of more instances increasing cost
* To prevent cascading effects

## Use case 

* prevent DDOS attack : if there are flood of requests coming from some IP , location , rate limiter can configure rules to drop those 
* Gracefully handle surge of users : users are legitimate but infra is not scaled 
* Multi tiered limits : CI/CD used internally by users : internal rate limiter
* You are not overusing a third party system
* To protect unprotected systems


# Strangler Pattern

* To separate Monoliths to Microservices
* First you will need to make monoliths to modular monoliths(payments , authentication , orders ...)
* Then separate each module to a separate microservice 
* After separating we can use different microservice patterns like API gateway , BFF , Service discovery and service mesh


# Anti corruption layer


# Exponential backoff 

* When a service is failing and clients keep on sending requests
* Server may not get enough time to recover 
* So in case of failures services can retry assuming request is idempotent
* When we do retry to avoid load on the server , we make the retry in exponential gaps
* First try at T sec , second at T+2 , third at T+8 
* We can also add a random jitter so all the clients do not retry at the same time 
