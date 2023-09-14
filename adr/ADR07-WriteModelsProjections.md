# ADRXX: Introduction of Write Models and Projections 

## Status

proposed

## Rationale

During the system design phase for the RoadWarrior's Reservation Container, performance surfaced as a critical concern. The application is expected to serve a large user base, with strict response times specified for both web and mobile platforms. Furthermore, the application's need to consistently provide real-time updates and respond to user actions necessitates a system that avoids on-the-fly complex calculations, especially during read operations.

Traditional architectures that combine both read and write operations into a single model can often encounter performance bottlenecks. These bottlenecks are particularly evident in systems where the read patterns are vastly different from the write patterns or where the read frequency far exceeds the write frequency.

## Decision

To address the performance concerns, the system will adopt a CQRS (Command Query Responsibility Segregation) architectural pattern. This involves separating the write operations (commands) from the read operations (queries).

- Write Models: These will handle all data write operations. After every write operation, a projection will be generated or updated, representing the current state of the data.

- Projections (Read Models): These are optimized for read operations. They are created and updated by the write models. Instead of running costly calculations every time a user wants to view data, the system will query these projections, which are already in a format optimized for reading and displaying to the user.

This separation ensures that the system can be optimized for both write-heavy operations and read-heavy operations without one affecting the performance of the other.

## Consequences

- Easier Scalability: By segregating read and write operations, we can independently scale the parts of the system that are under the most load.

- Performance: Read operations will be faster since the system will fetch pre-computed results from the projections instead of performing calculations during the read process.

- Complexity: Introducing CQRS can increase the overall complexity of the system. This could impact the maintainability and could require more documentation and training for new team members.

- Consistency: Since projections are updated after write operations, there might be a slight delay in reflecting the most recent data. This can introduce eventual consistency concerns where the data might not be immediately consistent across the system but will become consistent after a short period.

- Flexibility: The system can easily adapt to changing read and write patterns. If a new read pattern emerges that wasn't initially considered, a new projection can be introduced without affecting the existing write model.