# API Reference Overview

Welcome to the GreenMap API documentation! This reference provides comprehensive information about the GreenMap REST API.

## Introduction

The GreenMap API allows developers to integrate GreenMap functionality into their applications, websites, or services. Our API is designed to be RESTful, easy to use, and well-documented.

## API Base URL

```
Production: https://api.greenmap.example.com/v1
Staging: https://staging-api.greenmap.example.com/v1
```

## Authentication

### API Keys

To use the GreenMap API, you need an API key:

1. Sign up for a GreenMap account
2. Navigate to Settings → Developer
3. Generate an API key
4. Include the key in all API requests

### Authentication Methods

#### Bearer Token

Include your API key in the Authorization header:

```http
GET /api/v1/projects
Authorization: Bearer YOUR_API_KEY
```

#### Query Parameter (Not Recommended)

For testing purposes only:

```http
GET /api/v1/projects?api_key=YOUR_API_KEY
```

## Rate Limiting

To ensure fair usage, the API implements rate limiting:

| Account Type | Rate Limit | Burst Limit |
|--------------|------------|-------------|
| Free | 100 requests/hour | 10 requests/minute |
| Organizer | 500 requests/hour | 30 requests/minute |
| Organization | 2,000 requests/hour | 100 requests/minute |
| Enterprise | 10,000 requests/hour | 500 requests/minute |

### Rate Limit Headers

Response headers include rate limit information:

```http
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1640000000
```

### Handling Rate Limits

When you exceed the rate limit, you'll receive:

```json
{
  "error": {
    "code": "rate_limit_exceeded",
    "message": "Rate limit exceeded. Try again in 3600 seconds.",
    "retry_after": 3600
  }
}
```

## Request Format

### Content Type

All requests should use JSON:

```http
Content-Type: application/json
```

### Example Request

```bash
curl -X POST https://api.greenmap.example.com/v1/projects \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Community Tree Planting",
    "description": "Join us for a day of tree planting",
    "category": "tree_planting",
    "location": {
      "lat": 30.2672,
      "lng": -97.7431
    },
    "date": "2024-06-15T10:00:00Z"
  }'
```

## Response Format

### Success Response

Successful responses return a 2xx status code:

```json
{
  "success": true,
  "data": {
    "id": "proj_123456",
    "name": "Community Tree Planting",
    "status": "active",
    "created_at": "2024-01-15T10:00:00Z"
  },
  "meta": {
    "request_id": "req_abc123"
  }
}
```

### Error Response

Error responses return appropriate 4xx or 5xx status codes:

```json
{
  "error": {
    "code": "invalid_request",
    "message": "The 'name' field is required",
    "details": {
      "field": "name",
      "issue": "missing_required_field"
    }
  },
  "meta": {
    "request_id": "req_abc123"
  }
}
```

## Status Codes

| Code | Status | Description |
|------|--------|-------------|
| 200 | OK | Request succeeded |
| 201 | Created | Resource created successfully |
| 204 | No Content | Request succeeded with no response body |
| 400 | Bad Request | Invalid request parameters |
| 401 | Unauthorized | Invalid or missing API key |
| 403 | Forbidden | Insufficient permissions |
| 404 | Not Found | Resource not found |
| 429 | Too Many Requests | Rate limit exceeded |
| 500 | Internal Server Error | Server error |
| 503 | Service Unavailable | Temporary service disruption |

## Pagination

List endpoints support pagination:

### Request Parameters

```http
GET /api/v1/projects?page=1&per_page=20
```

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| page | integer | 1 | Page number |
| per_page | integer | 20 | Items per page (max 100) |

### Response Format

```json
{
  "success": true,
  "data": [...],
  "pagination": {
    "page": 1,
    "per_page": 20,
    "total_pages": 5,
    "total_items": 95,
    "has_next": true,
    "has_prev": false
  }
}
```

## Filtering and Sorting

### Filtering

Filter results using query parameters:

```http
GET /api/v1/projects?category=tree_planting&status=active
```

### Sorting

Sort results using the `sort` parameter:

```http
GET /api/v1/projects?sort=created_at:desc
```

Multiple sort fields:

```http
GET /api/v1/projects?sort=status:asc,created_at:desc
```

## Webhooks

Subscribe to real-time events:

### Available Events

- `project.created` - New project created
- `project.updated` - Project details updated
- `project.deleted` - Project deleted
- `participant.joined` - User joined a project
- `participant.left` - User left a project

### Webhook Configuration

Configure webhooks in your developer settings:

```json
{
  "url": "https://your-app.com/webhooks/greenmap",
  "events": ["project.created", "participant.joined"],
  "secret": "whsec_your_secret_key"
}
```

### Webhook Payload

```json
{
  "event": "project.created",
  "timestamp": "2024-01-15T10:00:00Z",
  "data": {
    "project": {
      "id": "proj_123456",
      "name": "Community Tree Planting"
    }
  }
}
```

## SDKs and Libraries

Official SDKs are available for popular languages:

### JavaScript/Node.js

```bash
npm install @greenmap/sdk
```

```javascript
const GreenMap = require('@greenmap/sdk');
const client = new GreenMap('YOUR_API_KEY');

const projects = await client.projects.list();
```

### Python

```bash
pip install greenmap-sdk
```

```python
from greenmap import GreenMap

client = GreenMap(api_key='YOUR_API_KEY')
projects = client.projects.list()
```

### Ruby

```bash
gem install greenmap
```

```ruby
require 'greenmap'

client = GreenMap::Client.new(api_key: 'YOUR_API_KEY')
projects = client.projects.list
```

## API Versioning

The API uses URL versioning:

```
/v1/projects  # Current stable version
/v2/projects  # Next version (beta)
```

We maintain backward compatibility for at least 12 months after a new version is released.

## Testing

### Sandbox Environment

Test your integration safely:

```
Sandbox: https://sandbox-api.greenmap.example.com/v1
```

Sandbox features:
- Test API keys
- Sample data
- No rate limiting
- Data resets daily

### Postman Collection

Download our Postman collection:

[Download Collection](https://api.greenmap.example.com/postman/collection.json)

## Best Practices

### Error Handling

Always handle errors gracefully:

```javascript
try {
  const project = await client.projects.get(projectId);
} catch (error) {
  if (error.code === 'not_found') {
    console.log('Project not found');
  } else if (error.code === 'rate_limit_exceeded') {
    // Wait and retry
    await sleep(error.retry_after * 1000);
  } else {
    throw error;
  }
}
```

### Caching

Implement caching to reduce API calls:

```javascript
// Cache for 5 minutes
const cache = new Map();
const CACHE_TTL = 5 * 60 * 1000;

async function getCachedProject(id) {
  const cached = cache.get(id);
  if (cached && Date.now() - cached.time < CACHE_TTL) {
    return cached.data;
  }
  
  const project = await client.projects.get(id);
  cache.set(id, { data: project, time: Date.now() });
  return project;
}
```

### Batch Requests

Minimize API calls by batching:

```javascript
// Instead of multiple requests
const project1 = await client.projects.get('proj_1');
const project2 = await client.projects.get('proj_2');

// Use batch endpoint
const projects = await client.projects.getBatch(['proj_1', 'proj_2']);
```

## Support

Need help with the API?

- 📖 [Full API Documentation](endpoints.md)
- 💬 [Developer Forum](https://forum.greenmap.example.com)
- 📧 Email: api@greenmap.example.com
- 🐛 [Report Issues](https://github.com/HouHackathon-CQP/GreenMap/issues)

## Changelog

Stay updated with API changes:

- [API Changelog](https://api.greenmap.example.com/changelog)
- [Breaking Changes](https://api.greenmap.example.com/breaking-changes)
- [Deprecation Schedule](https://api.greenmap.example.com/deprecations)

---

*Ready to build with GreenMap? Check out the [Endpoints](endpoints.md) documentation!*
