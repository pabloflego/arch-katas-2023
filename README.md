# O'Reilly Architectural Katas 2023

> Team: BingBongDingDong
> 
> Members:
>    - Luiz Tanure
>    - Marko Novaković
>    - Michał Wachowski
>    - Pablo Flego

## Contents

<!-- TOC -->
- [O'Reilly Architectural Katas 2023](#oreilly-architectural-katas-2023)
  - [Contents](#contents)
  - [Introduction](#introduction)
  - [Business Case](#business-case)
  - [Architectural Characteristics](#architectural-characteristics)
  - [Architecture Decision Records](#architecture-decision-records)
  <!-- TOC -->

## Introduction _(TODO: Proof Read)_

**RoadWarrior** is an ambitious endeavor to provide travelers with a next-generation online trip management dashboard. Its goal is to deliver a unified platform where travelers can view and manage their reservations, spanning across multiple services like flights, hotels, and car rentals. The system's essence lies in its real-time updates, seamless integrations with prominent travel systems, and a rich user interface to offer the best experience across both web and mobile platforms. Furthermore, with the power of analytics, RoadWarrior aims to understand travel trends and preferences, providing valuable insights for travelers and stakeholders alike.

## Business Case  _(TODO: Proof Read)_

### **Objective**:

To develop a state-of-the-art trip management dashboard that not only offers utility to travelers but also leads in terms of performance, availability, and integration capabilities.

### **Key Reasons**:

1. **Market Gap**: There's an increasing need for a singular platform where travelers can consolidate their trip details and receive real-time updates. The clutter of multiple platforms and the lack of instantaneous updates leave a gap in the market that RoadWarrior aims to fill.
2. **Competitive Advantage**: By ensuring updates within 5 minutes and targeting high response times for both web and mobile interfaces, RoadWarrior seeks to outperform the competition, making it the preferred choice for travelers.
3. **Integration with Existing Systems**: The seamless integration with established travel systems like SABRE and APOLLO opens up a broad user base for RoadWarrior, ensuring rapid market penetration.
4. **Data-Driven Insights**: With an emphasis on analytics, RoadWarrior doesn't just stop at providing utility. By gathering and analyzing user trip data, the system can offer insights into travel trends, preferences, and much more. This can be a significant tool for travelers planning future trips and for businesses to understand market dynamics.
5. **Analytical Warehouse Evolution**: Initially, RoadWarrior will use simple columnar storage to manage analytical data, benefiting from cost savings and reducing operational overhead. This choice also ensures a smooth learning curve, as the storage engine is similar to the primary database. As the startup matures and data demands grow, a migration to a dedicated solution, such as Amazon Redshift, will offer greater scalability, efficiency, and complex query support.
6. **Monetization and Growth**: The data collected can be monetized in various ways, from providing businesses with travel trends to offering users premium insights or advanced features. Furthermore, the analytical warehouse's establishment ensures that as the user base grows, the system scales efficiently, promising sustainability and further growth.
7. **Robust Architecture Decisions**: With decisions like employing a Analytics Warehouse, using event sourcing, and segregating write and read operations, the system is being designed with scalability, performance, and reliability in mind.

### **Expected Outcomes**:

1. **High User Adoption**: Given the system's features and real-time capabilities, a rapid increase in user base is anticipated.
2. **Stakeholder Value**: By gathering analytical data, RoadWarrior can provide invaluable insights to stakeholders in the travel industry, leading to potential partnerships and collaborations.
3. **Revenue Streams**: Monetizing insights, premium features, and potential partnerships can result in diverse revenue streams for RoadWarrior.

### **Conclusion**:

The RoadWarrior system, with its emphasis on user experience, performance, and data analytics, is positioned not just as a utility tool but as a game-changer in the travel industry. With the right execution, it holds the promise of reshaping how travelers manage and plan their trips.


## Architectural Characteristics

1. **Feasibility**

   - Budget Constraints: Startups often have limited funds, which means that every technology or solution they decide to adopt should be financially viable. This includes considerations around licensing costs, infrastructure costs, and any other operational expenses. Feasibility ensures that the proposed solution doesn't overshoot the budget.
   - Manpower and Skillset: A startup may have a small engineering team, possibly with a limited set of skills. Thus, the technology stack and solutions chosen should be within the competency of the available team, or at least easy for them to pick up. Choosing a very niche or complex tech stack may not be feasible for a small team.
   - Time-to-Market: One of the biggest advantages startups can have is the speed at which they release their products to capture the market. A feasible architecture would consider the speed of development and deployment, ensuring that the startup can launch in a timely manner.

2. **Availability**

   - The system must always be accessible to the users; the specification states a maximum of 5 minutes per month of unplanned downtime. This means that the system must be highly available.
   - Unavailability would lead to poor user experience, especially if a traveler is relying on the application for real-time travel updates, which could in turn harm the reputation of the startup.
   - The system interfaces with external systems (airlines, hotels, car rentals). It needs to be reliable in these interactions and should have effective error handling mechanisms to ensure users get accurate data.
   - Travelers are relying on this system for accurate and timely information, so it must be trustworthy.

3. **Performance, Responsiveness & Interoperability**

   - Travel updates must be available within 5 minutes of an update from the source. This requires a high-performance backend system that can handle the processing and pushing of these updates quickly.
   - The web application has a response time requirement of 800ms and the mobile application has a first-contentful paint time of under 1.4 seconds. Both these metrics necessitate a performant frontend and backend to meet the requirements.
   - The system needs to integrate seamlessly with various existing travel systems and should work internationally. This requires the system to be interoperable, meaning it should be capable of exchanging and making use of information from different systems without any hitches.

4. **Scalability**

   - The system needs to cater to 2 million active users per week and has a total user base of 15 million. The system needs to be scalable to handle this user base and also potential growth.
   - Being a startup, if the application becomes popular, the user base may increase rapidly. Therefore, the system should be designed to scale horizontally to cater to increased loads.

5. **Security**

   - Users are entrusting the application with their travel details, which is sensitive information. The system must ensure data protection and confidentiality.
   - The application polls and filters emails, which is a sensitive operation and requires strict security measures to prevent unauthorized access or breaches.
   - Sharing trips on social media or with specific people requires robust security mechanisms to ensure only authorized individuals can view the data.

6. **Maintainability & Testability**

   - The system integrates with multiple third-party systems (e.g., SABRE, APOLLO). As these systems evolve, the application should be architected in a way that allows for easy updates and integrations.
   - Given the dynamic nature of the travel industry, the startup may need to introduce new features or make changes frequently. A maintainable architecture ensures that these changes can be made with minimal disruption.
   - Given the variety of functionalities and integrations, it's essential that the system can be easily tested to ensure all parts work as expected.
   - Effective testing reduces the risk of bugs or issues in the live environment, which is critical given the real-time nature of the application.
   - Given the diverse set of features and third-party integrations, designing the system with modularity in mind would be beneficial. This allows different parts of the system to be developed, updated, and maintained independently.

7. **Usability**
   - The application aims to provide the richest user interface possible across all platforms. This puts emphasis on the usability aspect, ensuring that users can easily navigate and use the system without friction.
   - Usability also relates to how easily users can manually update reservations, group items by trips, and share their trips.


## Narrative

### Identifying the underlying architectural needs via Event Storming

We decided to discover the problem space, interactions, dependencies and flows in a Event Storming session.
The assumption is that defining the users can perform while interacting with the system, 
and the work the system needs to execute to achieve expected results will allow us to identify subdomains and 
interactions between them. This will allow us to define scopes & boundaries to decide which areas will drive 
architectural decisions.

![eventstorming.jpeg](eventstorming%2Feventstorming.jpeg)

We identified domains:

- **Reservation** - which is responsible for managing reservations and grouping them into trips. Reservations will be constantly updated from Adapters, therefore an Event Sourced representation will be beneficial as it is more natural to the actual usage.

- **Adapters** - intended for integration with travel agencies and abstract the specifics of each and report updates to the Reservation domain as normalized update events.

- **Analytical Warehouse** - a separate component that will be collecting data from Reservations, and updates, shared content for analytical purposes so it is separated and can evolve independently from the rest of architecture as it is driven by a separate set of requirements.

- **Notifications** - a relatively simple component acting as integration gateway with chosen third party provider, its implementation and size heavily depends on which will be chosen.

### Modeling the architecture [ADR01][ADR01]

We invision an architecture that will provide strong basis for the product to begin with, and be able to evolve in any direction with the changes to the product. No concrete architectural style is enforces, instead a mix between them is picked.

Part of the systems, containing the core functionality is defined as a modular monolith, to ease the discovery and modeling process.
While the supporting functionality, external integration points are as microservices to enforce separation from domain and allow for easier independent scaling, error handling without affecting the main platform. 

We started with modeling the architecture by skipping the first level of the C4 models - context and focus on the containers and components.

#### Containers

![C4L2_container.png](c4%2FC4L2_container.png)

The key container is the Reservation, that owns the domain of managing reservations and trips, which is the core domain. It is also one of the two user facing containers - thus, it also needs to contain the web server.
The actual tooling for web server can be picked independently of the rest of the architecture as in our opinion the greatest driver is the familiarity of the platform.
The other one user facing is the Analytical Warehouse, which is receiving tracking and other analytical data from the client applications.

#### Components

##### Access Control Layer
![C4L3_component_acl.png](c4%2FC4L3_component_acl.png)

The Access Control Layer (ACL) diagram represents the component that manages access to the system for users that want to interact with it.
There is second ACL, that is intended only for controlling and tracking access to shared content.

The idea is to have clear and strong separation between data that is dedicated to the customers and freely accessible by people that were shared with.

##### Adapters [ADR02][ADR02]

![C4L3_component_adapter.png](c4%2FC4L3_component_adapter.png)

Diagram visualises three versions of adapters that will update reservations by tracking different sources of information.
The main goal of the adapters is to serve as an abstraction layer between external sources that differ in quality, availability etc. and provide updates to the reservations.

The *E-Mail Gateway Adapter* is intended to receive e-mails from the customers, where they can forward relevant updates without integrating directly.

The *E-Mail Scanning Adapter* is scanning configure e-mail account for messages according to defined filters, and converts them into updates.

The *Api Travel Agency Adapter* is designed for polling information from Travel Agencies APIs.

##### Reservations [ADR03][ADR03] [ADR05][ADR05]
![C4L3_component_reservation.png](c4%2FC4L3_component_reservation.png)

This is the core system. It starts as a modular monolith as this will provide ease of evolution and extensibility needed on the early stages needed in startups. At the same time it will allow for future extraction of subdomains if they become large enough to be independent services.

The Reservation and Trips component is the one containing all the business logic around managing reservations and grouping them ino trips.

The reservations aggregate is event sourced, that all updates from adapters are additive, and this will allow for presenting changes to customers and will allow for clear separation between write and read model.

Trips serve as grouping container for reservations, therefore tracking changes in same way as for reservations will not bring significant value - Trips follow traditional columnar persistence.

Both, reservations and trips are projected into read model (Projections), that is responsible for accessing ongoing reservations and trips, but also serves as archive.
Archiving is based on copying latest projection as a form of snapshot of reservation and trip into a separate storage (initially a separate table, but can evolve into cold storage later) and removing the event source representation from write model.

Projection are also used for annual reporting by the Report Generator that is a periodic task running in the background.

If customer decides to share trip with the world, a copy of it is made into shared content storage (also a separate table, but can evolve into more specialized storage), wich is the only place accessible by anonymous users.

On every update of the reservation a notification trigger is sent to the Notification component, that will converse it into a notification message fitting specific communication channel.

##### Analytical warehouse [ADR04][ADR04] [ADR06][ADR06]
![C4L3_component_warehouse.png](c4%2FC4L3_component_warehouse.png)

It is purely passive system that receives data from the core domain - reservations, or from the client applications. Processes them before storing them in the columnar storage.
The processing is limited to ensuring anonymity of the users (PII compliance), while still keeping them relevant for analytical usage.

### Rich client thingie [ADR07] [ADR07]

<TODO>

### Evaluation, Risk assessment

The presented architecture is intended as a _starting point_ for something bigger. The main drivers were simplicity, fast development and ability to go to market quickly under limited budget.

This lead to compromises, where the architecture is relatively simple, easy to set up and understand by small engineering team, while still able to deliver on expected characteristics.

The design is not intended to cover all possible case that may arise, but to give strong basis for evolution and adaptation to future product directions and popularity rise.

The main risk is that, if the evolution is not disciplined, it may go in the direction where all systems are interconnected, boundaries are broken and domains are blurry.
In such case it will consume additional resources, require extra effort in development - thus slowing down.

Also, the engineering team needs to keep an eye, on the moment when system needs to evolve - e.g. the core domain of reservations and trips is split into separate more dedicated services - or they will end up in situation where system is barely able to handle the expected traffic.

## Architecture Decision Records

- [ADR01: Emerging Architecture][ADR01]
- [ADR02: Use of Adapters for External Integrations][ADR02]
- [ADR03: Adoption of Event Sourcing for Reservation Data Management][ADR03]
- [ADR04: Establishment of Analytical Warehouse Subsystem for Trip Data Analytics][ADR04]
- [ADR05: Introduction of Write Models and Projections][ADR05]
- [ADR06: Analytical Warehouse Storage][ADR06]
- [ADR07: React Native as framework for apps][ADR07]

[ADR01]:adr%2FADR01-EmergingArchitecture.md
[ADR02]:adr%2FADR02-UseAdaptersForExternalIntegrations.md
[ADR03]:adr%2FADR03-EventSourcingForReservationDataManagement.md
[ADR04]:adr%2FADR04-AnalyticalWarehouseSubsystem.md
[ADR05]:adr%2FADR05-WriteModelsProjections.md
[ADR06]:adr%2FADR06-AnalyticalWarehouseStorage.md
[ADR07]:adr%2FADR07-ReactNativeFrameworkForApps.md
