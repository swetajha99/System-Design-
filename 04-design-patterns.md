# Common System Design Patterns

## 1. Load Balancer Patterns

### Single Load Balancer
```
Clients -> Load Balancer -> [Server1, Server2, Server3]
```
- Simple to implement
- Single point of failure
- Good for small applications

### Multiple Load Balancers (Active-Passive)
```
Clients -> [LB1 (Active), LB2 (Passive)] -> Servers
```
- High availability
- Automatic failover
- More complex setup

## 2. Database Patterns

### Master-Slave Replication
```
Write Operations -> Master Database
Read Operations -> [Slave1, Slave2, Slave3]
```
- Improves read performance
- Write bottleneck at master
- Eventual consistency for reads

### Database Sharding
```
User Data Shard 1: Users 1-1000
User Data Shard 2: Users 1001-2000
User Data Shard 3: Users 2001-3000
```
- Horizontal scaling
- Complex to manage
- Cross-shard queries are difficult

### Database Partitioning
```
Orders Table:
- Recent Orders (Hot Data)
- Historical Orders (Cold Data)
```
- Improved query performance
- Easier maintenance
- Data lifecycle management

## 3. Caching Patterns

### Cache-Aside (Lazy Loading)
```
Application -> Cache -> Database
```
1. Check cache first
2. If miss, load from database
3. Populate cache
4. Return data

### Write-Through
```
Application -> Cache -> Database
```
- Write to both cache and database
- Cache always up-to-date
- Slower writes

### Write-Behind (Write-Back)
```
Application -> Cache -> (Async) -> Database
```
- Fast writes
- Risk of data loss
- Complex to implement

### Refresh-Ahead
```
Scheduler -> Cache -> Database
```
- Proactively refresh cache
- Reduces cache misses
- Requires predicting access patterns

## 4. Message Queue Patterns

### Point-to-Point
```
Producer -> Queue -> Consumer
```
- One message, one consumer
- Guaranteed delivery
- Load balancing

### Publish-Subscribe
```
Publisher -> Topic -> [Subscriber1, Subscriber2, Subscriber3]
```
- One message, multiple consumers
- Decoupled communication
- Fan-out pattern

### Dead Letter Queue
```
Main Queue -> [Processing Failed] -> Dead Letter Queue
```
- Handle failed messages
- Manual inspection and retry
- Prevent message loss

## 5. API Gateway Patterns

### Single API Gateway
```
Clients -> API Gateway -> [Service1, Service2, Service3]
```
- Centralized management
- Authentication and rate limiting
- Request routing and composition

### Microgateway Pattern
```
Clients -> [Gateway1, Gateway2, Gateway3] -> Services
```
- Distributed gateways
- Better performance
- More complex management

## 6. Service Discovery Patterns

### Client-Side Discovery
```
Client -> Service Registry -> [Service Instance1, Service2]
```
- Client chooses service instance
- Direct communication
- More complex client logic

### Server-Side Discovery
```
Client -> Load Balancer -> Service Registry -> Services
```
- Simpler client
- Load balancer handles routing
- Additional network hop

## 7. Circuit Breaker Pattern

```
Service A -> Circuit Breaker -> Service B
```
### States:
- **Closed**: Normal operation, requests pass through
- **Open**: All requests fail immediately
- **Half-Open**: Limited requests test if service recovered

### Benefits:
- Prevents cascading failures
- Fast failure response
- Automatic recovery detection

## 8. Saga Pattern

```
Order Service -> Payment Service -> Inventory Service
```
### Compensating Transactions:
- If payment fails, cancel order
- If inventory fails, refund payment
- Each step has compensation action

### Use Cases:
- Distributed transactions
- Long-running business processes
- Data consistency across services

## 9. CQRS (Command Query Responsibility Segregation)

```
Commands (Write) -> Write Model -> Write Database
Queries (Read) -> Read Model -> Read Database
```
### Separation:
- Different models for read and write
- Optimized for each operation
- Eventual consistency

### Benefits:
- Scalable reads and writes
- Flexible data models
- Better performance

## 10. Event Sourcing

```
Events -> Event Store -> Current State
```
### Instead of storing current state:
- Store all events that changed state
- Rebuild state from events
- Immutable audit trail

### Benefits:
- Complete audit history
- Time travel debugging
- Event replay capabilities

## When to Use Which Pattern

| Pattern | When to Use | Trade-offs |
|---------|-------------|------------|
| Load Balancer | High traffic, multiple servers | Added complexity |
| Database Sharding | Large datasets, high write load | Complex queries |
| Cache-Aside | Read-heavy workloads | Stale data possible |
| Circuit Breaker | Unstable external services | Added latency |
| Saga Pattern | Distributed transactions | Complex compensation |
| CQRS | Different read/write patterns | Eventual consistency |
