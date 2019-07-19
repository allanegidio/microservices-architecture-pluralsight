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