# ADR06: Analytical Warehouse Storage

## Status
Proposed

## Rationale

The RoadWarrior system, requires a scalable, and efficient database solution for its Analytical Warehouse. 
This decision is based on:

1. **Scalability**: To manage high volumes of analytical data and handle spikes in workloads.
2. **Complex Query Support**: To provide insights, aggregations, and multi-dimensional analyses.
3. **Cost**: Balancing the budget constraints with the feature set required.

## Decision

For sake of simplicity, the initial storage for analytical warehouse can be of same type as the primary data storage. 
This should keep the tech stack under control on the early stages of the startup.
With time, it will require migration to more dedicate solution like Amazon Redshift, a fully managed data warehouse service in the cloud.

## Consequences

### Initial
- **Operational Overhead**: Columnar storage, like Postgres, can handle big amounts of data before it will need to be replaced with dedicated solution, this free resources that may be used elsewhere.

- **Cost**: Starting with simple, well known data storage engine will decrease the need for specialized expertise and infrastructure.

- **Learning Curve**: Low learning curve as it is same engine as primary database.
- 
- **Vendor Lock-in**: Not applicable, as traditional columnar storages can be hosted anywhere.

### Target (e.g. Amazon Redshift)

- **Operational Overhead**: Being a managed service, much of the operational overhead like backups, patching, and scaling is handled by AWS.

- **Cost**: While Redshift might not be the cheapest, its price-performance ratio is competitive. Cost can be managed by scaling clusters according to demand and leveraging reserved instances.

- **Learning Curve**: For teams unfamiliar with Redshift, there might be an initial learning curve. However, its SQL-based interface ensures that anyone with SQL knowledge can get started quickly.

- **Vendor Lock-in**: Choosing a managed service from AWS might lead to some level of vendor lock-in. However, the benefits provided by the managed service outweigh the cons in this context.

