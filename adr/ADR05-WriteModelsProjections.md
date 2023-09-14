# ADR05: Adoption of Separate Write Models and Projections

## Status
Proposed

## Rationale
In the development phase of the RoadWarrior's Reservation Container, performance emerged as a paramount concern. With the expected large user base and strict latency requirements on both web and mobile platforms, there is a need to ensure optimal system responsiveness. Performing complex calculations during read operations could hinder the desired performance, especially given the requirement for real-time updates.

Traditionally, architectures that integrate both read and write operations within a single model can face performance limitations, especially when read patterns diverge significantly from write patterns or when reads considerably outnumber writes.

## Decision
To tackle the performance challenges, we've decided to:

- **Write Models**: These will solely manage data write operations. After each write action, a corresponding projection (or read-optimized model) will be updated or generated to reflect the current data state.

- **Projections**: Optimized specifically for read operations, these models are derived and updated from the write models. By relying on these projections, we can serve data to users without executing costly calculations on-the-fly. Instead, the system retrieves pre-formatted and optimized data tailored for viewing.

This separation aims to cater to the distinct needs of both write-centric and read-centric operations, ensuring that neither operation impacts the other's performance.

## Consequences
- **Enhanced Scalability**: By differentiating read and write operations, each part of the system can be scaled based on its load independently. For instance, in a read-intensive scenario, the projections can be scaled without influencing the write models.

- **Improved Performance**: Due to the utilization of projections, read operations become more efficient as they bypass real-time extensive calculations.

- **Increased Complexity**: This approach might elevate the system's intricacy. Such complexity could potentially affect maintainability and might necessitate comprehensive documentation and additional training for newcomers.

- **Eventual Consistency**: As projections get updated post write operations, there might be a negligible delay in mirroring the latest data, leading to brief periods of inconsistency.

- **Greater Flexibility**: This model ensures adaptability to evolving read and write patterns. If new read trends emerge, they can be addressed by introducing a new projection without altering the current write model.

