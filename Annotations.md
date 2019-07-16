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


# Design Principles

#### High Cohesion
> It makes our overall system highly scalable, flexible, and reliable in demand.

- Single Focus
- Single Responsability (from SOLID)
- Only reason for change is business function or domain
- Each microservice must be encapsulated into one package. 
- Easily rewritable code

#### Autonomous
> Loose coupling between microservices. Should not force other microservice to change.

- Honor contracts and interfaces
- Should be stateless
  + No need to remember previous interactions
- Indenpendently changeable and deployable.
- Backwards compatible
- Cuncurrent development


#### Business Domain Centric
> Service must represents business function or business domain of organization.

- Scope of service
- Bound context from DDD
  + Contain all functionality which is related to a specific part of the business
- Identify boundaries/Seams
  + Basically highlight the areas where related functionality exist
- Shuffle code if required
  + Group related code into a service
  +  Aim for high cohesion
- Responsive to business changes


#### Resilience
> Resiliency is the ability of a system to gracefully handle and recover from failures.

- Embrace failure
  + Another service
  + Specific connection
  + Third-party system
- Degrade functionality
- Default functionality
- Multiples Instances
  + Register a service on startup
  + Deregister on failure
- Types of failures
  + Exceptions/Errors
  + Delays
  + Unavailability
- Network issues
  + Delay
  + Unavailability
Validate input
  + Service to service
  + Client to service


#### Observable
> Way to observe our system's health in terms of status, logs and errors that are currently happening in the system.

- Centralized monitoring
- Centralized logging
- Why
  + Distributed transactions
  + Quick problem solving
  + Quick deployment required feedback
  + Data used for capacity planning
  + Data used for scaling (can se demand within our system)
  + Whats actually used
  + Monitor business data


#### Automation
> CI / CD

- Tools to reduce testing
  + Manual regression testing 
  + Time taken on testing integration
  + Environment setup for testing

- Tools to provide quick feedback
  + Integration feedback on check in
  + Continuous Integration for check change integrate qith the entire system

- Tools to provide quick deployment
  + Pipeline to deplyment
  + Automated deployment
  + Reliable deployment
  + Continuous Deployment (Check status, check change, run tests, build and deploy using preconfigured target)

- Why
  + Distributed System
  + Multiple instances of services
  + Manual integration testing too time consuming
  + Manual deployment time consuming and unreliable


# Microservices Design

#### How implement High Cohesion
  > Single thing done well and single focus

- Identify Single Focus
  + Business function
  + Business domain
- Split into finer grained services
- Avoid "Is kind of the same"

#### How be Autonomous
  > Indenpendently changeable and deployable

- Loosely coupled
  + Communication by network
   + Synchronous
     +  When microservice calls another microservice and wait for reply
   + Assynchronous
     + Publish events handled by a message broker
     + Subscribe to events
  + Tecnology agnostic API
  + Avoid client libraries
  + Contracts between services
    + Fixed and agreed interfaces
    + Shared models
    + Clear input and output
  + Avoid chatty exchanges between services
  + Avoid sharing between services
    + Databases
    + Shared libraries


- Microservice ownership by team
  + Responsability to make autonomous
  + Agreeing contract between teams
  + Responsible for long-term maintenance
  + Collaborative development
    + Communicate contract requirements
    + Communicate data requirements
  + Concurrent development

- Versioning
  + Avoid breaking changes
  + Backwards compatibility
  > You increment the major number if the new version of the microservice is not backwards compatible and you only increment the minor number if the new version of the microservice is actually backwards compatible and you increase the patch number if the only change in the new version of the microservice is the defect fix and the overall microservice is still Backwards compatibility.
  + Integration tests
  + Have a versioning strategy
    + Concurrent versions
     > You could have an old version and the new version running at the same time.
    + Semantic versioning
      + Major.Minor.Patch (e.g 15.1.2)
    + Coexisting endpoints
      + /V2/customer/

#### Business Domain Centric
  > A key thing to remember at the same time is the other design principle of a microservice having high cohesion, a microservice must do one thing and do it well. It must have a single focus and only one reason for it to change. 
  + Business function or business domain
  + Approach
    + Identify business domain in a coarse manner
    + Review sub groups of business functions or areas
    + Review benefits of splitting further
    + Agree a commom language
  + Microservices for data (CRUD) or functions
  + Fix incorrect boundaries
    + Merge or split
  + Explicit interfaces for outside world
  + Splitting using technical boundaries
    + Service to access archive data
    + For performance tuning

#### Resilience
 > When in a microservices architecture, we have so many moving parts, and if one specific microservice failed, we can't have the entire system going down because of one failure.

 - Design for known failures
 - Failure of downstream systems
   + Other services internal or external
 - Degrade functionality on failure detection
 - Default functionality on failure detection
 - Design system to fail fast
 - Use timeouts
   + Use for connected systems
   + Timeout our requests after threshold
   + Service to service
   + Service to other systems
   + Standard timeout length
   + Adjust length ib a case by case basis
 - Network outages and latency
 - Monitor timeouts
 - Log timeouts

#### Observable
  > See system health / Centralized logging and monitoring

- Centralized Monitoring
  + Real-time monitoring
  + Monitor the host
    + CPU, memory, disk usage, etc.
  + Expose metrics within the services
    + Response times
    + Timeouts
    + Exceptions and errors
  + Business data relatered metrics
    + Number of orders
    + Average time from from basket to checkout
  + Collect and aggregate monitoring data
    + Monitoring tools that provide aggregation
    + Monitoring tools that provide drill drown options
  + Monitoring tool that can help visualise trends
  + Monitoring tool that can compare data across servers
  + Monitoring tool that can trigger alerts


- Centralized Logging
  + When to log
    + Startup or shutdown
    + Code path milestones
      + Requests, responses and decisions
    + Timesouts, exceptions and errors
  
+ Structured logging
  + Level
    + Information
    + Error
    + Debug
    + Statistic
  + Date and time
  + Correlation ID
  + Host name
  + Service name and service instance
  + Message

+ Traceable distributed transactions
  + Correlation ID
    + Passed service to service

#### Automation
  > Tools for testing, quick feedback and deployment

 - Continuous Integration Tools
   + Work with source control systems
   + Automatic after check-in (Commit)
   + Unit tests and integrations tests required
   + Ensure quality of check-in (Commit)
     + Code compiles
     + Tests pass
     + Changes integrate
     + Quick feedback
   + Urgency to fix quickly
   + Creation of build
   + Build ready for test team
   + Build ready for deployment

- Continuous Deployment Tools
  + Automate software deployment
    + Configure once
    + Works with CI tools
    + Deployable after check in (Commit)
    + Reliably released at anytime
  
  + Benefits
    + Quick to market
    + Reliable deployment
    + Better customer experience









 


