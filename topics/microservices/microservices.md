# Microservices

* small , harmonic and autonomous subsystems 
* break problems to sub problems and each problem is designed in an optimal way
* Each service is specialized in solving one problem really well . auth service , search , payments , order ,delivery

## Why ?

* code base grows over time and so lots of team have to work on same code
* deployment becomes major problem
* conflicts
* Scaling becomes easy and predictable : each service can be scaled independently
* For example : Search might run on 10 instances , Auth on 5 and payments on 7 
* Autonomous and isolation : you own your own tech stack , networking protocols 
* Every service can decide their own tech stack 
* Upgrades are simpler : If a service decides to move to some new tech stack they can move and expose the same endpoints so other services can consume
* Fault tolerance : If one service is down , all features or complete product is not down . For example : If search service is down , only search will not work 

## How to fence microservices 

* It needs to be small , but how small ?
* Good start to break is to do faeture wise 
* Teams can look into specific set of features 


## How to model ?

* When you are designing a new service / microservice / features , what all things you can consider
* Fresh codebase , new techstack and clean CI/CD setup : You start fresh and do not repeat past mistakes 
* Fencing a microservice is really important
* What happens if I don't fence it will or do not create  microservice ?
* If you have a big boundary : lot of components/features ,few microservices ,  multiple teams working on same
* Too many microservices : more services to talk to each other , inter dependency is more 
* Loose coupling , High cohesion 
* Change in one service it should not require change in other
* Related functionalities part of same microservices
* A service needs to know as little as possible about other service 
* public apis : yes , auth  : yes , db : no , rate limit : yes , communication protocol/contracts : yes

