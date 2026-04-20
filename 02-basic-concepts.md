# Basic System Design Concepts

## 1. Client-Server Architecture

### Client
- Frontend application that makes requests to the server
- Can be web browser, mobile app, or desktop application

### Server
- Backend that processes requests and returns responses
- Handles business logic, data processing, and storage

## 2. API Design

### RESTful APIs
- **GET**: Retrieve data
- **POST**: Create new data
- **PUT**: Update existing data
- **DELETE**: Remove data

### Key Principles
- Statelessness: Each request contains all needed information
- Resource-based: URLs represent resources
- HTTP methods: Use appropriate HTTP verbs

## 3. Database Design

### Relational Databases (SQL)
```
Users Table:
- id (Primary Key)
- username
- email
- created_at

Posts Table:
- id (Primary Key)
- user_id (Foreign Key)
- title
- content
- created_at
```

### NoSQL Databases
- **Document**: MongoDB (JSON-like documents)
- **Key-Value**: Redis (simple key-value pairs)
- **Column-family**: Cassandra (wide-column storage)

## 4. Caching Strategies

### Cache-Aside Pattern
1. Check cache first
2. If miss, query database
3. Store result in cache
4. Return to client

### Write-Through Cache
- Write to both cache and database simultaneously
- Ensures cache is always consistent

## 5. Load Balancing Algorithms

### Round Robin
Distributes requests evenly across all servers

### Least Connections
Sends requests to server with fewest active connections

### IP Hash
Uses client IP to determine which server handles the request

## 6. Microservices vs Monolith

### Monolithic Architecture
- Single application with all functionality
- Easier to develop initially
- Harder to scale individual components

### Microservices Architecture
- Multiple small, independent services
- Each service handles specific business function
- Better scalability and fault isolation

## 7. Network Protocols

### HTTP/HTTPS
- Web communication protocol
- HTTPS adds encryption layer

### TCP vs UDP
- **TCP**: Reliable, ordered delivery
- **UDP**: Fast, no guarantee of delivery

### WebSocket
- Real-time, bidirectional communication
- Useful for chat apps, live updates

## 8. Security Basics

### Authentication vs Authorization
- **Authentication**: Who are you?
- **Authorization**: What can you do?

### Common Security Measures
- HTTPS encryption
- Input validation
- Rate limiting
- Authentication tokens (JWT)
