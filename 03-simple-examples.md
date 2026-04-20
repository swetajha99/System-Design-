# Simple System Design Examples

## Example 1: URL Shortener

### Requirements
- Create short URLs from long URLs
- Redirect short URLs to original URLs
- Handle high traffic volume

### Design Components
```
Client -> Load Balancer -> Web Servers -> Cache -> Database
```

### API Design
```
POST /api/shorten
Request: {"url": "https://example.com/very/long/url"}
Response: {"short_url": "https://short.ly/abc123"}

GET /abc123
Response: 301 Redirect to original URL
```

### Data Model
```
URLs Table:
- id (Primary Key)
- short_code (Unique)
- original_url
- created_at
- access_count
```

### Algorithm for Short Code Generation
1. Use base62 encoding (0-9, a-z, A-Z)
2. Convert database auto-increment ID to base62
3. Example: ID 1000 -> "g8"

## Example 2: Simple Chat Application

### Requirements
- Real-time messaging
- Multiple chat rooms
- User authentication

### Architecture
```
Client -> WebSocket Server -> Message Queue -> Database
```

### Components
- **WebSocket Server**: Handles real-time connections
- **Message Queue**: Buffers messages for reliability
- **Database**: Stores message history and user data

### API Design
```
WebSocket Events:
- join_room: {"room_id": "room123"}
- send_message: {"room_id": "room123", "message": "Hello!"}
- leave_room: {"room_id": "room123"}

REST API:
POST /api/auth/login
POST /api/rooms/create
GET /api/rooms/{id}/messages
```

### Data Model
```
Users Table:
- id, username, password_hash, created_at

Rooms Table:
- id, name, created_by, created_at

Messages Table:
- id, room_id, user_id, content, timestamp
```

## Example 3: Image Hosting Service

### Requirements
- Upload and store images
- Serve images quickly
- Handle different image sizes

### Architecture
```
Client -> Upload Service -> Object Storage -> CDN
```

### Components
- **Upload Service**: Handles image uploads and processing
- **Object Storage**: Stores original and processed images (S3)
- **CDN**: Distributes images globally for fast access
- **Image Processor**: Creates different sizes (thumbnail, medium, large)

### Processing Pipeline
1. User uploads image
2. Store original in object storage
3. Generate multiple sizes asynchronously
4. Store processed versions
5. Update database with image metadata

### API Design
```
POST /api/upload
Request: multipart/form-data with image file
Response: {"image_id": "img123", "url": "https://cdn.example.com/img123.jpg"}

GET /api/images/{id}/info
Response: {"sizes": ["thumbnail", "medium", "large"], "original_size": "1920x1080"}
```

## Example 4: Todo List Application

### Requirements
- CRUD operations for tasks
- User authentication
- Task categorization

### Simple Architecture
```
Client -> Web Server -> Database
```

### API Design
```
GET /api/tasks
POST /api/tasks
PUT /api/tasks/{id}
DELETE /api/tasks/{id}

POST /api/auth/register
POST /api/auth/login
```

### Data Model
```
Users Table:
- id, email, password_hash, created_at

Tasks Table:
- id, user_id, title, description, status, due_date, created_at

Categories Table:
- id, user_id, name, color
```

## Key Takeaways

1. **Start Simple**: Begin with basic architecture and add complexity as needed
2. **Identify Bottlenecks**: Find potential performance issues early
3. **Use Appropriate Tools**: Choose databases and technologies based on requirements
4. **Plan for Growth**: Design with scalability in mind
5. **Security First**: Always consider authentication and authorization
