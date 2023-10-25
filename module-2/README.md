Task requirements. Please find the file [here](https://git.epam.com/epm-cdp/global-java-foundation-program/java-modules/-/blob/master/modules/44.%20Solution%20Architecture%20Styles%20and%20Patterns/Homework.md)

# Tasks:

## **Task 1:**

Try to identify architecture styles being used in legacy and proposed solutions. List benefits and limitations for each of the identified style.

1. *Legacy application*
    - Monolithic, layered
        - Benefits: 
            - Easy to implement and maintain.
            - All source code is centralized into just one repository.
            - Single source code repository.
        - Drawbacks:
            - Easy to lose control over the application and as result end up with high coupling, low cohesion and a big ball of mud.
            - Might be hard to refactor.
            - Might be hard to introduce new features, depending on the complexity.
            - Slow and complex deployment.


2. *Proposed architecture*
    - Microservices
        - Benefits:
            - Separate concerns of the system.
            - Scale fast.
            - Maintenance is easier.
            - Hypermedia discovery.
            - Deployments can be rolledout with no interruptions and few side effects
            - Can support multiple protocols
            - Can expose multiple interfaces
            - Clear business view through resources exposed
            - Uses well know and well defined protocols
        - Drawbacks:
            - Easy to end up with many dependencies between services
            - Easy to have duplicated functions
            - Stale/old services can be part of the ecosystem

    - Event-driven architecture
        - Benefits:
            - Loose coupling between services/components
            - Fault tolerance
            - Fan Out and decreased technical debt
        - Drawbacks: 
            - High complexity
            - Debugging and troubleshooting
            - Monitoring

It's not explicity described as event-driven architecture, however, the use of Publisher/Subscriber makes be believe that there will be a evolutionary movement towards this style.


## **Task 2:**

Try to figure out what architecture patterns has been applied within solution. List what are the problem given pattern is intended to solve.

**Solution:**

1. *Legacy application*:

    - Load Balancer
        - Benefits: 
            - Helps distribute the traffic among different instances of the service.
            - Scale applications.
            - Can work as a bastion/Gatekeeper.
            - Improves uptime.
            - Allows automatic routing when instances must be shutdown
        - Drawbacks: 
            - Single point of failure when it doesn´t have any recovery strategy, even though it might be a light weight component in the infrastructure.
            - Might increase network latency.
            - Possible geographic limitations.

    - OBS: Used only to route requests when the main application fails. No Information available when it comes to health checks, or metrics to identify if the main application is working properly or is just overloaded. Used as Static Content Hosting as well.

    - Single Database/source of truth
        - Benefits:
            - All data stored in one single place, allowing report queries and such.
            - Clear vision of relationships and dependencies between domain entities.
        - Drawbacks:
            - Scalability can be complex.
            - Tendency to become slow over time, as the database grows in size.
            - Changes are hard due to relationships between objects.
            - Data migration can take a very long time in case of a migration or technology update
            - Costly

Per their requirements to the migration, they could perform rehosting to the desired cloud provider, followed by the use of strangler fig pattern to segregate the application into different microservices or functions, depending on the need, using the potential of cloud.

As an alternative, they could start a refactoring of the current application, using a new load balancer or traffic router on the cloud to partially continue using the current solution along with the new microservices that can be depoyed over time into the new infrastructure.

2. *New Architecture*:

    - Gateway Routing/DNS resolver
        - Benefits:
            - Distribute requests/users to the closest AZ
            - Improves uptime
            - Can work as a bastion/gatekeeper for the internal services
        - Drawbacks
            - Introduce a single point of failure
            - Might increase network latency
    - API Gateway/Load balancer
        - Benefits:
            - Allows shielding internal applications over request spikes
            - Implements Rate limits
            - Takes care of authentication/federated authentication
            - Automatic retries (depending on the provider)
            - Local caching
        - Drawbacks:
            - Single point of failure
            - Might increase network latency
            - Depends on the consumed service to implement health checks
    - Backend for frontend
        - Benefits:
            - Orchestrate/Coreograph other service calls exposing one single resource for a specific frontend
            - Targets specific API client types/technology
            - Uses several other patterns on the integrations
        - Drawbacks:
            - Maintenance can become hard depending on how many integrations per microservice
            - Is an integration layer, that can become obsolote quickly
            - Uses several other patterns on the integrations
    - Database per service
        - Benefits:
            - Data stored is related to one domain entity/context only
            - Smaller databases
            - Database normalization is easier and oriented to the business
            - Scale easily
            - Migration doesn´t affect the whole system
            - Database as a code, database migrations can be executed without affecting other systems
        - Drawbacks:
            - Multiple sources of data
            - One database might depend on data from another microservice/database and can lead to eventual consistency or phantom relationships
    - Messaging Bridge or Publisher/Subscriber
        - Benefits:
            - Async communication speeds up the process
            - Easy to replay messages/states from the broker
            - Multiple listeners to the same event (if using Publisher/Subscriber)
        - Drawbacks:
            - Depending on the broker there is no confirmation of delivery of message
            - Dead letter
            - Might not be able to replay events
    - Event Sourcing
        - Benefits:
            - Messages can be read later if the downstream/consumer system is not available
            - Any message format is accepted
            - Near real-time data reporting
        - Drawbacks:
            - Infrastructure must be extremely efficient
            - Controlling the message format/schema requires additional registry/tool
            - Same event produced by different services must have a common schema
    - Data wharehousing
        - Benefits:
            - data standardization
            - improved busines decision-making
            - efficiency
            - single source of truth.
        - Drawbacks:
            - close to no flexibility.
            - might required ETL to clean up the data before storing it.
            - costly.
            - security.
    - Geodes
        - Benefits:
            - Availability even if a disaster occurs.
            - Proximity to the customer, which makes the service "faster".
            - Can target the location with special/required implementation such as regulations and other.
        - Drawbacks:
            - Costly.
            - Duplicated infrastructure for all zones.
            - Pipelines for deployment and delivery can become complex.
            - Monitoring, Auditing, Security concerns.
    - Static Content Hosting (CDN)
        - Benefits:
            - Fast static content delivery.
            - Close to the customer.
            - Can be targeted.
            - Supports even big amounts of data, such as .iso files and others.
        - Drawbacks:
            - Very high cost.
            - Single point of failure.
            - Relies on a very efficient infrastructure.
    - Federated Identity/SSO
        - Benefits:
            - Transfers the responsibility of managing users to trusted providers.
            - Services don´t need to validate user credentials.
            - Lower exposition of PII.
            - Improves customer experience.
        - Drawbacks:
            - Thirdy Part providers.
            - Claims might not be compatible and requires transformation.
            - Succeptible to Surface Attack such as Man-in-the-middle.
            - Relies on Idnetity provider availability.
    - Rate Limiting
        - Benefits:
            - Help prevents some surface attacks such as brute-force, DDoS.
            - There is better flow of data, as all consumers must be concious of the usage of APIs/Resources.
            - Services are more reliable and scale up and down less frequently due to high demand from a small group of users.
            - Reduces the risk of attacks.
        - Drawbacks:
            - Is usually implemented based on users, location or ip addresses, that can be easily circumvented.
    - Cache-Aside
        - Benefits:
            - Offers fast access to frequently required data.
            - Easy to mantain.
            - Scales fast with distributed caching, over different instances.
            - Can be as big as the vm instance's/machine memory.
        - Drawbacks:
            - Costly.
            - Convinient for data that doesn't change much.
            - It might happen that the data is out of sync.