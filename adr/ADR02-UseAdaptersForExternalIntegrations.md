# ADR02: Use of Adapters for External Integrations

## Status
Proposed

## Rationale
The RoadWarrior system is required to integrate with a variety of external sources, including travel agencies, email services, and potentially others in the future. Direct integration with each of these sources might involve tight coupling between our system's core logic and the specific APIs or interfaces of these external systems.

This tight coupling can be problematic for several reasons:

1. **Changing APIs**: External systems might update or change their APIs, requiring us to make changes to our core system.
2. **Diverse Integration Points**: Different external systems can have vastly different APIs, leading to inconsistency in our integration logic.
3. **Testing Difficulties**: Direct integration can make it challenging to mock or stub out these external systems during testing.

Given these challenges, there's a need for a structured and consistent way to integrate with these external systems without compromising the integrity and flexibility of our core system.

## Decision
We've decided to adopt the "Adapter Pattern" for integrating with external systems. Each external system will have a corresponding adapter within our system. These adapters will:

- **Provide a Consistent Interface**: All adapters will conform to a predefined interface within our system. This ensures consistency in how our core system interacts with external integrations, regardless of the external system's specific API.

- **Encapsulate External Logic**: All the logic specific to an external system (like API calls, data transformations, and error handling) will be encapsulated within its corresponding adapter.

- **Facilitate Testing**: By using adapters, we can easily mock or stub out external systems during testing, ensuring that our tests remain fast and reliable.

## Consequences
- **Flexibility**: Adapters allow our core system to remain decoupled from external systems. If an external system changes its API or if we decide to replace one system with another, only the corresponding adapter needs to be modified.

- **Consistency**: All external integrations will follow a consistent pattern, making the system more maintainable and understandable.

- **Overhead**: Introducing adapters can add some overhead in terms of development time initially. However, this cost is offset by the long-term benefits of maintainability and flexibility.

- **Complexity**: While the core system's logic remains clean and decoupled, developers will need to familiarize themselves with the adapter pattern and its implementation within the system.

- **Scalability**: In the future, if we need to integrate with more external systems, we can easily extend our system by adding new adapters without affecting the core system or existing integrations.

