# API Endpoints

Complete reference for all GreenMap API endpoints.

## Projects

### List Projects

Retrieve a list of projects with optional filtering.

```http
GET /api/v1/projects
```

#### Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| page | integer | Page number (default: 1) |
| per_page | integer | Items per page (default: 20, max: 100) |
| category | string | Filter by category |
| status | string | Filter by status (active, completed, cancelled) |
| location | string | Filter by location (lat,lng,radius) |
| date_from | string | Start date (ISO 8601) |
| date_to | string | End date (ISO 8601) |
| search | string | Search query |

#### Example Request

```bash
curl -X GET "https://api.greenmap.example.com/v1/projects?category=tree_planting&status=active" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

#### Example Response

```json
{
  "success": true,
  "data": [
    {
      "id": "proj_123456",
      "name": "Community Tree Planting",
      "description": "Join us for a day of tree planting",
      "category": "tree_planting",
      "status": "active",
      "location": {
        "lat": 30.2672,
        "lng": -97.7431,
        "address": "Austin, TX"
      },
      "date": "2024-06-15T10:00:00Z",
      "participants": {
        "current": 15,
        "max": 50
      },
      "organizer": {
        "id": "user_789",
        "name": "John Doe",
        "avatar": "https://cdn.greenmap.example.com/avatars/user_789.jpg"
      },
      "created_at": "2024-01-15T10:00:00Z",
      "updated_at": "2024-01-20T14:30:00Z"
    }
  ],
  "pagination": {
    "page": 1,
    "per_page": 20,
    "total_pages": 3,
    "total_items": 45
  }
}
```

### Get Project

Retrieve a specific project by ID.

```http
GET /api/v1/projects/{project_id}
```

#### Path Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| project_id | string | The project ID |

#### Example Request

```bash
curl -X GET "https://api.greenmap.example.com/v1/projects/proj_123456" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

#### Example Response

```json
{
  "success": true,
  "data": {
    "id": "proj_123456",
    "name": "Community Tree Planting",
    "description": "Join us for a day of tree planting in the local park.",
    "category": "tree_planting",
    "status": "active",
    "location": {
      "lat": 30.2672,
      "lng": -97.7431,
      "address": "Zilker Park, Austin, TX 78746"
    },
    "date": "2024-06-15T10:00:00Z",
    "duration": 240,
    "participants": {
      "current": 15,
      "max": 50,
      "waiting_list": 3
    },
    "organizer": {
      "id": "user_789",
      "name": "John Doe",
      "email": "john@example.com",
      "avatar": "https://cdn.greenmap.example.com/avatars/user_789.jpg"
    },
    "images": [
      "https://cdn.greenmap.example.com/projects/proj_123456/img1.jpg",
      "https://cdn.greenmap.example.com/projects/proj_123456/img2.jpg"
    ],
    "tags": ["trees", "community", "outdoor"],
    "requirements": ["Bring gloves", "Wear comfortable shoes"],
    "impact": {
      "trees_planted": 0,
      "co2_offset": 0
    },
    "created_at": "2024-01-15T10:00:00Z",
    "updated_at": "2024-01-20T14:30:00Z"
  }
}
```

### Create Project

Create a new environmental project.

```http
POST /api/v1/projects
```

#### Request Body

```json
{
  "name": "Community Tree Planting",
  "description": "Join us for a day of tree planting",
  "category": "tree_planting",
  "location": {
    "lat": 30.2672,
    "lng": -97.7431,
    "address": "Zilker Park, Austin, TX"
  },
  "date": "2024-06-15T10:00:00Z",
  "duration": 240,
  "max_participants": 50,
  "tags": ["trees", "community"],
  "requirements": ["Bring gloves"],
  "images": ["https://example.com/image1.jpg"]
}
```

#### Example Response

```json
{
  "success": true,
  "data": {
    "id": "proj_123456",
    "name": "Community Tree Planting",
    "status": "active",
    "created_at": "2024-01-15T10:00:00Z"
  }
}
```

### Update Project

Update an existing project.

```http
PUT /api/v1/projects/{project_id}
```

#### Request Body

```json
{
  "name": "Updated Project Name",
  "description": "Updated description",
  "max_participants": 60
}
```

### Delete Project

Delete a project (organizer only).

```http
DELETE /api/v1/projects/{project_id}
```

#### Example Response

```json
{
  "success": true,
  "message": "Project deleted successfully"
}
```

## Participants

### Join Project

Add the authenticated user as a participant.

```http
POST /api/v1/projects/{project_id}/participants
```

#### Example Response

```json
{
  "success": true,
  "data": {
    "participant_id": "part_123",
    "user_id": "user_456",
    "project_id": "proj_123456",
    "status": "confirmed",
    "joined_at": "2024-01-20T10:00:00Z"
  }
}
```

### Leave Project

Remove the authenticated user from a project.

```http
DELETE /api/v1/projects/{project_id}/participants/me
```

### List Participants

Get all participants for a project.

```http
GET /api/v1/projects/{project_id}/participants
```

#### Example Response

```json
{
  "success": true,
  "data": [
    {
      "id": "part_123",
      "user": {
        "id": "user_456",
        "name": "Jane Smith",
        "avatar": "https://cdn.greenmap.example.com/avatars/user_456.jpg"
      },
      "status": "confirmed",
      "joined_at": "2024-01-20T10:00:00Z"
    }
  ]
}
```

## Users

### Get Current User

Get the authenticated user's profile.

```http
GET /api/v1/users/me
```

#### Example Response

```json
{
  "success": true,
  "data": {
    "id": "user_123",
    "username": "johndoe",
    "email": "john@example.com",
    "name": "John Doe",
    "avatar": "https://cdn.greenmap.example.com/avatars/user_123.jpg",
    "bio": "Environmental enthusiast",
    "location": "Austin, TX",
    "stats": {
      "projects_joined": 25,
      "projects_created": 5,
      "hours_contributed": 120,
      "trees_planted": 50,
      "co2_offset": 250
    },
    "badges": ["first_step", "tree_hugger"],
    "created_at": "2023-06-01T10:00:00Z"
  }
}
```

### Update User Profile

Update the authenticated user's profile.

```http
PUT /api/v1/users/me
```

#### Request Body

```json
{
  "name": "John Doe",
  "bio": "Updated bio",
  "location": "Austin, TX",
  "interests": ["tree_planting", "cleanup"]
}
```

### Get User by ID

Get a specific user's public profile.

```http
GET /api/v1/users/{user_id}
```

## Categories

### List Categories

Get all available project categories.

```http
GET /api/v1/categories
```

#### Example Response

```json
{
  "success": true,
  "data": [
    {
      "id": "tree_planting",
      "name": "Tree Planting",
      "icon": "🌳",
      "description": "Reforestation and tree planting initiatives"
    },
    {
      "id": "cleanup",
      "name": "Cleanup",
      "icon": "🗑️",
      "description": "Litter and waste removal events"
    }
  ]
}
```

## Search

### Search Projects

Search for projects using full-text search.

```http
GET /api/v1/search/projects
```

#### Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| q | string | Search query (required) |
| location | string | Location filter (lat,lng,radius) |
| category | string | Category filter |
| date_from | string | Start date filter |
| date_to | string | End date filter |

#### Example Request

```bash
curl -X GET "https://api.greenmap.example.com/v1/search/projects?q=tree+planting&location=30.2672,-97.7431,50" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## Comments

### Get Comments

Get comments for a project.

```http
GET /api/v1/projects/{project_id}/comments
```

### Create Comment

Add a comment to a project.

```http
POST /api/v1/projects/{project_id}/comments
```

#### Request Body

```json
{
  "text": "Looking forward to this event!"
}
```

### Delete Comment

Delete a comment (author or organizer only).

```http
DELETE /api/v1/projects/{project_id}/comments/{comment_id}
```

## Statistics

### Get Project Stats

Get statistics for a specific project.

```http
GET /api/v1/projects/{project_id}/stats
```

#### Example Response

```json
{
  "success": true,
  "data": {
    "project_id": "proj_123456",
    "participants": {
      "total": 45,
      "confirmed": 40,
      "waitlist": 5
    },
    "impact": {
      "trees_planted": 120,
      "hours_contributed": 180,
      "co2_offset": 600
    },
    "engagement": {
      "views": 1250,
      "comments": 23,
      "shares": 15
    }
  }
}
```

### Get User Stats

Get statistics for a user.

```http
GET /api/v1/users/{user_id}/stats
```

## Notifications

### Get Notifications

Get notifications for the authenticated user.

```http
GET /api/v1/notifications
```

#### Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| unread_only | boolean | Show only unread notifications |
| type | string | Filter by notification type |

### Mark as Read

Mark a notification as read.

```http
PUT /api/v1/notifications/{notification_id}/read
```

### Mark All as Read

Mark all notifications as read.

```http
PUT /api/v1/notifications/read-all
```

## Error Codes

Common error codes you may encounter:

| Code | HTTP Status | Description |
|------|-------------|-------------|
| invalid_request | 400 | Malformed request |
| unauthorized | 401 | Invalid or missing API key |
| forbidden | 403 | Insufficient permissions |
| not_found | 404 | Resource not found |
| validation_error | 422 | Invalid data provided |
| rate_limit_exceeded | 429 | Too many requests |
| server_error | 500 | Internal server error |

## Webhook Events

Available webhook events:

| Event | Description |
|-------|-------------|
| project.created | New project created |
| project.updated | Project details updated |
| project.deleted | Project deleted |
| project.completed | Project marked as completed |
| participant.joined | User joined a project |
| participant.left | User left a project |
| comment.created | New comment posted |
| user.updated | User profile updated |

---

*Need more examples? Check out our [GitHub repository](https://github.com/HouHackathon-CQP/GreenMap) for sample code!*
