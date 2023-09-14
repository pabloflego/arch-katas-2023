# ADR01: Emerging Architecture 

## Status

Accepted

## Rationale

In the startup world, one of the main goals for architecture is to allow for fast evolution, ease of development, 
while still give level of confidence and meet required architectural characteristics.

It is also important, that the implementation will allow for further evolution of architecture that will fit future scale and scope.

## Decision

The decision is not to set on any specific architectural style, but start with a mix of modular monolith and microservices, and let the system needs drive the architecture.
At the beginning, modular monolith will be the one handling core of the domain, and microservices are intended for supporting functionalities like agency adapters.
To keep systems internally organised a layered architecture is recommended to separate domain logic, 
from communication channels and data storage - thus allowing for more flexibility in adapting to any issues that may arise.

## Consequences

- **Ease of Development**: The core domain will reside in monolith, allowing for easier adjustment of subdomain boundaries on early stages, while self-evident systems can take more fitting styles.

- **Increased Testability**: Having single system owning most of the domain logic will allow for easier testability.

- **Natural evolution**: Not setting any concrete styles allows for adapting any forms of architecture to any parts of the system that as they fit.
 
- **Lack of direction**: Lack of concrete decision may lead to uncontrolled degradation of architecture. Careful planning is needed acknowledging drives from system needs.  

- **Simplicity**: Not having complex distributed system, will be beneficial and easier to grasp for less experienced or small teams common to early stages of startups.
