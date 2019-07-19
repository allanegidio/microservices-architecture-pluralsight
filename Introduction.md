# What is a service?

- A service is a piece of software, which basically provides functionality to other pieces of software within your system.
- The other pieces of software could be anything from a website to a mobile app, or a desktop app, or even another service which uses another service in order to carry out a particular type of functionality.
- The communication between these software components and the service normally happen over a network using some kind of communication protocol. 
- It Allows us to scale up our software when demand increases using load balancer.
- Can have multiple instances of the service, so when the demand increases, we just increase the number of instances of the service running across servers.



# Microservice Introduction

- Evolution of SOA. SOA done well.
- Provides service which are more efficiently scalable, more flexible and high performance.
- Hasas a focus on a service
- Microservice Architecture uses lightweight communication mechanism between clients and services and service to service.
- Communication have be quick because the transaction will be distributed which is completed by multiple services.
- Need to be technology agnostic.
- Service needs to use an open communication protocol so that it does not dictate the technology that the client application needs to use.
- Each microservice has its own data storage.
- Indenpendently changeable and deployable.
- Easy to respond change quickly
- If one part of the system breaks, it won't break the entire system.