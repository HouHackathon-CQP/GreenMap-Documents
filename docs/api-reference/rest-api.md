<!-- /*Copyright 2025 HouHackathon-CQP

 Licensed under the Apache License, Version 2.0 (the "License");
 you may not use this file except in compliance with the License.
 You may obtain a copy of the License at

     http://www.apache.org/licenses/LICENSE-2.0

 Unless required by applicable law or agreed to in writing, software
 distributed under the License is distributed on an "AS IS" BASIS,
 WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 See the License for the specific language governing permissions and
 limitations under the License. */ -->

# REST API

## Authentication

### Login

Đăng nhập và lấy access token.

```http
POST /api/v1/login/access-token
Content-Type: application/x-www-form-urlencoded
```

**Request Body:**
```
username=admin@greenmap.hanoi&password=yourpassword
```

**Response:**
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "bearer"
}
```

---

## Users

### Get Current User

```http
GET /api/v1/users/me
Authorization: Bearer <token>
```

**Response:**
```json
{
  "id": 1,
  "email": "admin@greenmap.hanoi",
  "full_name": "Admin User",
  "role": "admin",
  "is_active": true
}
```

### Create User

```http
POST /api/v1/users/
Authorization: Bearer <admin_token>
Content-Type: application/json
```

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "securepassword",
  "full_name": "New User",
  "role": "citizen"
}
```

### List Users (Admin only)

```http
GET /api/v1/users/?skip=0&limit=20
Authorization: Bearer <admin_token>
```

---

## Reports

### Create Report

```http
POST /api/v1/reports/
Authorization: Bearer <token>
Content-Type: multipart/form-data
```

**Request Body:**
```
title: Rác thải chưa thu gom
description: Bãi rác lớn tại góc đường...
latitude: 21.0285
longitude: 105.8542
image: [file]
```

**Response:**
```json
{
  "id": 123,
  "title": "Rác thải chưa thu gom",
  "description": "Bãi rác lớn tại góc đường...",
  "latitude": 21.0285,
  "longitude": 105.8542,
  "image_url": "/uploads/reports/abc123.jpg",
  "status": "PENDING",
  "created_at": "2025-12-10T14:30:00Z"
}
```

### List Reports

```http
GET /api/v1/reports/?status=PENDING&skip=0&limit=20
Authorization: Bearer <token>
```

**Query Parameters:**

| Param | Type | Description |
|-------|------|-------------|
| status | string | Filter by status (PENDING, APPROVED, REJECTED) |
| skip | int | Pagination offset |
| limit | int | Number of items per page |

### Update Report Status

```http
PUT /api/v1/reports/{id}
Authorization: Bearer <admin_token>
Content-Type: application/json
```

**Request Body:**
```json
{
  "status": "APPROVED"
}
```

---

## Locations

### List Locations

```http
GET /api/v1/locations/?type=park
Authorization: Bearer <token>
```

**Query Parameters:**

| Param | Type | Description |
|-------|------|-------------|
| type | string | Filter by type (park, charging, bicycle, tourist) |
| lat | float | Center latitude for geo query |
| lng | float | Center longitude for geo query |
| radius | float | Radius in km |

### Create Location

```http
POST /api/v1/locations/
Authorization: Bearer <admin_token>
Content-Type: application/json
```

**Request Body:**
```json
{
  "name": "Công viên Thống Nhất",
  "type": "park",
  "latitude": 21.0117,
  "longitude": 105.8442,
  "description": "Công viên lớn nhất Hà Nội",
  "metadata": {
    "area": 50000,
    "facilities": ["playground", "lake", "jogging_track"]
  }
}
```

### Update Location

```http
PUT /api/v1/locations/{id}
Authorization: Bearer <admin_token>
```

### Delete Location

```http
DELETE /api/v1/locations/{id}
Authorization: Bearer <admin_token>
```

---

## System

### Health Check

```http
GET /api/system/health
```

**Response:**
```json
{
  "status": "healthy",
  "database": "connected",
  "broker": "connected",
  "version": "1.0.0"
}
```
