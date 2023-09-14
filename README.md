# O'Reilly Architectural Katas 2023

## Contents
<!-- TOC -->
* [O'Reilly Architectural Katas 2023](#oreilly-architectural-katas-2023)
  * [Contents](#contents)
  * [Introduction](#introduction)
  * [Business Case](#business-case)
  * [Architectural Characteristics](#architectural-characteristics)
  * [Architecture Decision Records](#architecture-decision-records)
<!-- TOC -->

## Introduction

## Business Case

## Architectural Characteristics

1. Feasibility
   - Budget Constraints: Startups often have limited funds, which means that every technology or solution they decide to adopt should be financially viable. This includes considerations around licensing costs, infrastructure costs, and any other operational expenses. Feasibility ensures that the proposed solution doesn't overshoot the budget.
   - Manpower and Skillset: A startup may have a small engineering team, possibly with a limited set of skills. Thus, the technology stack and solutions chosen should be within the competency of the available team, or at least easy for them to pick up. Choosing a very niche or complex tech stack may not be feasible for a small team.
   - Time-to-Market: One of the biggest advantages startups can have is the speed at which they release their products to capture the market. A feasible architecture would consider the speed of development and deployment, ensuring that the startup can launch in a timely manner.

2. Availability
   - The system must always be accessible to the users; the specification states a maximum of 5 minutes per month of unplanned downtime. This means that the system must be highly available.
   - Unavailability would lead to poor user experience, especially if a traveler is relying on the application for real-time travel updates, which could in turn harm the reputation of the startup.
   - The system interfaces with external systems (airlines, hotels, car rentals). It needs to be reliable in these interactions and should have effective error handling mechanisms to ensure users get accurate data.
   - Travelers are relying on this system for accurate and timely information, so it must be trustworthy.

3. Performance, Responsiveness & Interoperability
   - Travel updates must be available within 5 minutes of an update from the source. This requires a high-performance backend system that can handle the processing and pushing of these updates quickly.
   - The web application has a response time requirement of 800ms and the mobile application has a first-contentful paint time of under 1.4 seconds. Both these metrics necessitate a performant frontend and backend to meet the requirements.
   - The system needs to integrate seamlessly with various existing travel systems and should work internationally. This requires the system to be interoperable, meaning it should be capable of exchanging and making use of information from different systems without any hitches.

4. Scalability
   - The system needs to cater to 2 million active users per week and has a total user base of 15 million. The system needs to be scalable to handle this user base and also potential growth.
   - Being a startup, if the application becomes popular, the user base may increase rapidly. Therefore, the system should be designed to scale horizontally to cater to increased loads.

5. Security
   - Users are entrusting the application with their travel details, which is sensitive information. The system must ensure data protection and confidentiality.
   - The application polls and filters emails, which is a sensitive operation and requires strict security measures to prevent unauthorized access or breaches.
   - Sharing trips on social media or with specific people requires robust security mechanisms to ensure only authorized individuals can view the data.

6. Maintainability & Testability
   - The system integrates with multiple third-party systems (e.g., SABRE, APOLLO). As these systems evolve, the application should be architected in a way that allows for easy updates and integrations.
   - Given the dynamic nature of the travel industry, the startup may need to introduce new features or make changes frequently. A maintainable architecture ensures that these changes can be made with minimal disruption.
   - Given the variety of functionalities and integrations, it's essential that the system can be easily tested to ensure all parts work as expected.
   - Effective testing reduces the risk of bugs or issues in the live environment, which is critical given the real-time nature of the application.
   - Given the diverse set of features and third-party integrations, designing the system with modularity in mind would be beneficial. This allows different parts of the system to be developed, updated, and maintained independently.

7. Usability
   - The application aims to provide the richest user interface possible across all platforms. This puts emphasis on the usability aspect, ensuring that users can easily navigate and use the system without friction.
   - Usability also relates to how easily users can manually update reservations, group items by trips, and share their trips.


## Architecture Decision Records
- [ADR01: Emerging Architecture](adr%2FADR01-EmergingArchitecture.md)
- [ADR02: Use of Adapters for External Integrations](adr%2FADR02-UseAdaptersForExternalIntegrations.md)
- [ADR03: Adoption of Event Sourcing for Reservation Data Management](adr%2FADR03-EventSourcingForReservationDataManagement.md)
- [ADR04: Establishment of Analytical Warehouse Subsystem for Trip Data Analytics](adr%2FADR04-AnalyticalWarehouseSubsystem.md)
- [ADR05: Introduction of Write Models and Projections](adr%2FADR05-WriteModelsProjections.md)
- [ADR06: Analytical Warehouse Storage](adr%2FADR06-AnalyticalWarehouseStorage.md)
