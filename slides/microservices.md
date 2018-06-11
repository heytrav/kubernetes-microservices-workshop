### Microservices


#### Typical Monolithic Systems
* Typically one or a few large binaries to deploy
* Simple command to run
* Tightly coupled code



#### Disadvantages of Monolith
* Long release cycles 
   + Lots of changes spread across application
   + Potential for errors
* Usually single large DB
   + Tight coupling with data model
   + Simple schema change can break app
* Scaling difficult
* Rollback of an entire version



#### Microservices
* Services are isolated in scope and functionality
   + Lowers impact of change (good or bad)
* Services can be coupled to separate storage backends
   + Reduce impact of schema changes on entire app
+ Can be scaled independently 
+ Smaller memory/CPU fingerprint means faster deployment


#### Disadvantages of Microservices
* Complexity
   + How to define service boundaries?
   + Service explosion
* Need to define service interface
* Can become complicated to version individual services
* Managing 10s or 100s of services tricky
* Inter service networking


#### Microservices and Containers
Note: containers mitigate some of the above issues
* Containers as _unit_ equivalent of microservice
* Deployable artefact
* Can be versioned
* Layered filesystem
   + Deploying changes equivalent of deploying _change only_


#### Managing Microservice Containers
Note: Containers solve part of the problem 
* Still quite a lot of work maintaining large applications
* Monitoring health of many services difficult
* Maintain homeostasis 
   + constant number of _healthy_ services
   + scale in proportion to demand



#### Orchestration to the rescue
* Monitors health of services
   + Cull unhealthy services
   + Periodically spawn new services
* React to change in demand (autoscaling)
* Manage networking between services
