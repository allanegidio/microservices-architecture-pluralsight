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


# Technology for Microservices


## Communication

#### Synchronous

- Request response communication
  + Client to service
  + Service to service
  + Service to external

- Remote procedure call
  > Can use to request a service from a program located in another computer on a network without having to understand the network's details.
  + Sensitive to change

- HTTP
  + Work across the internet
  + Firewall friendly

- REST
  + CRUD using HTTP verbs
  + Natural decoupling
  + Open communication protocol
  + REST with HATEOS
    > Includes links (endpoints) into response like Delete, Retrieve, Update...

- Syncronous issues
  + Both parties have to be available
  + Performance subject to network quality
  + Clients must know location of service (host/port).

#### Asynchronous

- Event based
  + Mitigates the need of client and service availability
  + Decouples client and service

- Message queueing protocol
  + Message brokers
  + Subscriber and publisher are decoupled
  + Microsoft Message Queuing (MSMQ)
  + RabbitMQ
  + ATOM (HTTP to propagate events)

- Asynchronous challenge
  + Complicated 
  + Reliance on message broker
  + Visibility of the transaction
  + Managing the messaging queue

- Real world systems
  + Would use both synchronous and asynchronous 

## Hosting Plataforms

#### Virtualization

- A virtual machine as a host
- Foundation of cloud platforms
  + Platform as a service (PAAS)
    + Microsoft Azure
    + Amazon web services
    + Your own cloud (for example vSphere)

- Could be more efficient
  + Takes time to setup
  + Takes time to load
  + Take quite a bit of resource

- Unique features
  + Take snapshot 
    > (restore VM back to the time when the snapshot was taken)
  + Clone instances

- Standardised  and mature

#### Container

- Type of virtualization
- Isolate services from each other
- Single service per container
- Different to a virtual machine
  + Use less resource than VM
  + Faster than VM
  + Quicker to create new instances
- Future of hosted apps
- Mainly Lunix based
- Examples
  + Docker
  + Rocker
  + Glassware

#### Self hosting

- Implement your own cloud
  + Virtualization
  + Implement containers

- Use of physical machines
  + Single service on a server
  + Multiple services on a server

- Challenges
  + Long-term maintenance
  + Need for technicians
  + Training
  + Need for space
  + Scaling is not as immediate

#### Registration and Discovery

- Where?
  + Host, port and version
- Service registry database
- Register on startup
- Deregister service on failure
- Cloud platforms make it easy
- Local platform registration options
  + Self registration on startup 
  + Third-party registration
- Local platform discovery options
  > Either connect directly to the service or use some kind of gateway which all client connect and the gateway retrieves the location from service registry
  + Client-side discovery
  + Server-side discovery

## Observable Microservices

#### Monitoring Tech

- Centralised tools
  + Nagios
  + PRTG
  + Load balancers
  + New Relic

- Desired features
  + Metrics across servers
  + Automatic or minimal configuration
  + Client libraries to send metrics
  + Test transactions supports
  + Alerting when something is wrong

- Network monitoring
- Standardise monitoring
  + Central tool
  + Preconfigured virtual machines or containers
- Real-time monitoring

#### Logging Tech

- Portal for centralised logging data
  + Elastic log
  + Log stash
  + Splunk
  + Kibana
  + Graphite

- Client logging libraries
  + Serilog

- Desired features
  + Structured logging
  + Logging across servers
  + Automatic or minimal configuration
  + Correlation / Context ID for transaction

- Standardise logging
  + Central tool
  + Template for client library

## Microservices Performance

#### Scaling

- How
  + Creating multiple instances of serviec
  + Adding resource to existing service
- Automated or on-demand
- PAAS auto scaling options
- Virtualization and containers 
- Physical host servers
- Load balancers
  + API Gateway
- When to scale up
  + Performance issues
  + Monitoring data show that you will have issues
  + Capacity planning

#### Caching

- Caching to reduce
  + Client calls to services
  + Service calls to databases
  + Service to service calls
- API Gateway/Proxy level
  > this way cache implementation is invisible for everything else
- Client side
  > Single page applications that download most the data they need and work with that data until they need to make a call back to the system. 
- Service level
  > You could also implement caching at service level. So when service A called service B, it caches a response from service B. 
- Considerations
  + Simple to setup and manage
  + Data leaks
    > Show wrong data.

#### API Gateway
  > So API gateways are basically the central entry point into our system for client applications.

- Help with performance
  + Load balancing
  + Caching

- Help with
  + Creating central entry point
  + Exposing services to clients
  + One interface to many services
  + Dynamic location of services
  + Routing to specific instance of service
    > Example you redirect all requests of Brazil for instances are located in Brazil
  + Service registry database

- Security
  + API Gateway
  + Dedicated security service
  + Central security vs service level

## Automation Tools

#### Continuous Integration

- Many CI Tools
  + Azure DevOps
  + TeamCity
  + Etc...
- Desired features
  + Cross platform
    + Windows builders, Java builders and others
  + Source Control integrations
  + Notifications
  + IDE Integrations
- Map a microservice to a CI build
  > Every microservice have be single focus and independently changeable/deployable

  + Code change triggers build of specific service 
  + Feedback just received on that service
  + Builds and tests run quicker
  + Separate code repository for service
  + End product is in one place
  + CI builds to test database changes
  + Both microservice build and database upgrade are ready

- Avoid one CI build for all service

#### Continuous Deployment

- Many CD Tools
  + Aim for cross platform tools

- Desired features
  + Central control panel
  + Simple to add deployment targets
  + Support for scripting
  + Support for build statuses
  + Integration with CI Tool
  + Support for multiple environments
  + Support for PAAS


# Moving Forward With Microservices

## Browfield Microservices
  > When you need migrate existing project to Microservices architecture

#### Approach

 - Existing system
   + Monolithic system
   + Organically grown
   + Seems to large to split
- Lacks microservices design principles
- Identify seams
  + Separation that reflects domains
  + Identify bounded contexts
- Start modularising the bounded contexts
  + Move code incrementally
  + Tidy up a section per release
    + Take your time
    + Existing functionality needs to remain intact
  + Run unit tests and integration tests to validate change
  + Keep reviewing
- Seams are future microservice boundaries

#### Migration

- Code is organised into bounded contexts
  + Code related to a business domain or function is in one place
  + Clear boundaries with clear interfaces between each
- Convert bounded contexts into microservices
  + Start off with one
    + Use to get comfortable
  + Make it switchable
    + Maintain two versions of the code
- How to prioritise what to split?
  + By risk
  + By technology
  + By dependencies
- Incremental approach
- Integrating with the monolithic
  + Monitor both for impact
  + Monitor operations that talk to microservices
  + Review and improve infrastructure
  + Incrementally the monolithic will be converted

#### Database Migration

- Avoid shared database
- Split database using seams
   + Relate tables to code seams
- Supporting the existing application
  + Data layer that connects to a multiple database
- Tables that link across seams
  + API call that can fetch that data for a relationship
- Refactor database into multiple databases
- Data referential integrity
- Static data tables
  + Place that static data within a configuration file and make available to each microservice.
  + Other option is to have a specific microservice for receive requests from other microservice.
- Share Datas
  + Data that read and written to by multiple microservices, move to your own microservice so that the other microservices can interact with it.

#### Transactions

- Transactions ensure data integrity
- Transactions are simple in monolithic applications
- Transactions spanning microservices are complex
  + Complex to observe
  + Complex to problem solve
  + Complex to rollback
- Options for failed trannsactions
  + Try again later
    > We place back onto the queue for possibly another service to pick up
  + Abort entire transaction
  + Use a transaction manager
    + In Two Phase Commit, all the participanting microservices first tell the transaction manager if they are okay to commit their part of transaction. 
    + Disadvantage of transaction manager
      + Reliance on transaction manager
      + Delay in processing
      + Potential bottleneck
      + Complex to implement
- Distributed transaction compatibility
  + Our new microservice needs to tell the monolithic system that their part of the transaction is complete
  + Can be achieved by placing message in the Message queue
  + Completed message for the monolith


+ #### Reporting

- Microservices complicate reporting
  + Data split across microservices
  + No central database
  + Joining data across databases
  + Slower reporting
  + Complicate report development

- Possible solutions
  + Service calls for report data
    > Create a Reporting service that call other microservices to collect the data. But is not good for large volumes of data or real time reporting.
  + Data pumps
    > Send data to a central Reporting database


## Greenfield Microservices
 > Create new system from scratch

- New project
- Evolving requirements
- Business domain
  + Not fully understood
  + Getting domain experts involved
  + System boundaries will evolve
- Teams experience
  + First microservice
  + Experienced with microservices
- Existing system integration
  + Monolithic system
  + Estabilished microservices architecture
- Push for change
  + Changes to apply microservice principles

> However if requirements are evolving not quite clear to see what microservices are required, it's best to start off with a monolithic design. 

- Start off with monolithic design
  + High level design
  + Evolving seams
  + Develop areas into modules
  + Boundaries start to become clearer
  + Refine and refactor design
  + Split further when required
- Modules becomes services
  > Eventually these modules should represent business domains and business functions at a very finite granular level.
+ Shareable code libraries promote to service
+ Review microservice principles at each stage
+ Prioritise by
  + Minimal viable product
  + Customer needs and demand


## Microservices Provisos

- Accepting initial expense
  + Longer development times
  + Cost and training for tools and new skills
- Skilling up for distributed systems
  + Handling distributed transactions
  + Handling reporting
- Additional testing resource
  + Latency and performance testing
  + Testing for resilience
- Improving infrastructure
  + Security
  + Performance
  + Reliance
- Overhead tomange microservices
- Cloud technologies
- Culture change