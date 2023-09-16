# ADR03: Adoption of Event Sourcing for Reservation Data Management

## Status

Proposed

## Rationale

Maintaining the consistency and accuracy of reservation data is paramount for the RoadWarrior system. Traditional data storage techniques involve saving the current state of an entity, but this approach can lead to challenges:

1. **Data Evolution**: Understanding how data arrived at its current state can be opaque, making it difficult to audit or troubleshoot issues.
2. **Concurrency**: Handling concurrent operations can be complex, leading to potential data inconsistencies.
3. **Integration Delays**: External integrations, like travel agencies, might not always provide real-time data, leading to potential stale reads or missed updates.

Given these challenges and the system's need for robust and real-time data representation, a different approach to data management is necessary.

## Decision

We've decided to implement "Event Sourcing" for managing reservation data. With Event Sourcing:

- **Store Changes, Not Just State**: Instead of storing the current state of a reservation, every change (event) to the reservation is stored sequentially.

- **Rebuild State**: The current state of a reservation can be reconstructed by replaying its events. This offers an inherent audit trail and a deep understanding of data evolution.

- **Projections for Read Efficiency**: Recognizing that reading data by replaying events can be inefficient, especially in read-heavy systems, we'll generate "projections" of the data. These projections represent optimized, read-ready views of the data, making read operations swift and efficient.

## Consequences

- **Traceability**: Event Sourcing provides an inherent audit trail, making it clear how a reservation arrived at its current state. This traceability is valuable for debugging and auditing.

- **Scalability**: The system can scale writes and reads independently. Projections can be optimized and scaled based on read patterns.

- **Complexity**: Event Sourcing can introduce initial complexity in terms of setup and understanding. Developers need to adapt to a mindset of thinking in terms of events rather than state changes.

- **Data Volume**: Storing every event can lead to large volumes of data over time. Adequate storage solutions and potential event pruning or archiving strategies might be required.

- **Consistency**: The system might exhibit eventual consistency, especially when projections lag behind the latest events. However, this is a trade-off for the benefits gained.

- **Recovery and Redundancy**: In cases of system failures, data can be rebuilt from events, offering a robust mechanism for data recovery.
