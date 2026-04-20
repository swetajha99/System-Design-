# System Design Fundamentals

## What is System Design?

System design is the process of defining the architecture, components, modules, interfaces, and data for a system to satisfy specified requirements. It's about making trade-offs between various constraints like performance, scalability, reliability, and cost.

## Key Concepts

### 1. Scalability
- **Horizontal Scaling**: Adding more machines to your pool of resources
- **Vertical Scaling**: Adding more power (CPU, RAM) to an existing machine

### 2. Availability vs Reliability
- **Availability**: System is up and running
- **Reliability**: System continues to work correctly over time

### 3. Latency vs Throughput
- **Latency**: Time taken to process a single request
- **Throughput**: Number of requests processed per unit time

### 4. Consistency Models
- **Strong Consistency**: All nodes see the same data at the same time
- **Eventual Consistency**: Data will eventually be consistent across all nodes

## Basic Components

### Load Balancer
Distributes incoming traffic across multiple servers to prevent any single server from becoming a bottleneck.

### Database
- **SQL**: Relational databases (MySQL, PostgreSQL)
- **NoSQL**: Non-relational databases (MongoDB, Cassandra, Redis)

### Caching
Stores frequently accessed data to reduce database load and improve response times.

### Message Queue
Enables asynchronous communication between services.

## Design Process

1. **Requirements Gathering**: Understand functional and non-functional requirements
2. **Capacity Estimation**: Calculate expected traffic, storage, and bandwidth needs
3. **High-Level Design**: Define major components and their interactions
4. **Detailed Design**: Specify APIs, data models, and algorithms
5. **Identify Bottlenecks**: Find potential performance issues
6. **Iterate and Refine**: Improve the design based on constraints

## Common Trade-offs

- **Performance vs Cost**: Faster systems usually cost more
- **Consistency vs Availability**: CAP theorem states you can only choose two
- **Security vs Usability**: More security often means less convenience
- **Development Speed vs Optimization**: Quick development vs optimized performance
