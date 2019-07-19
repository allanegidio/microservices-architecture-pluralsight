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