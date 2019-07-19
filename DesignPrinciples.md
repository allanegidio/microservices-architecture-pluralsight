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