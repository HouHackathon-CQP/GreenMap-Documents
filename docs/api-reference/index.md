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

# API Reference

Tài liệu tham khảo đầy đủ về các API của hệ thống GreenMap. Backend cung cấp REST API cho Frontend và Mobile, cùng với tích hợp NGSI-LD Context Broker.

---

## Base URLs

| Môi trường | REST API | Context Broker |
|------------|----------|----------------|
| **Development** | `http://localhost:8000` | `http://localhost:1026` |
| **Staging** | `https://api-staging.myhou.io.vn` | `https://orion-staging.myhou.io.vn` |
| **Production** | `https://backend.myhou.io.vn` | `https://orion.myhou.io.vn` |

---

## Authentication

### JWT Token Authentication

GreenMap sử dụng **JWT (JSON Web Tokens)** để xác thực người dùng.

#### Login Endpoint

```http
POST /auth/login
Content-Type: application/x-www-form-urlencoded

username=admin@myhou.io.vn
password=your_password
```

**Response:**

```json
{
  "access_token": "string",
  "token_type": "bearer",
  "id": 0,
  "email": "string",
  "full_name": "string",
  "role": "ADMIN"
}
```

#### Sử Dụng Token

Gửi token trong header `Authorization`:

```http
GET /reports
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

#### Register User

```http
POST /auth/register
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "SecurePass123!",
  "full_name": "Nguyễn Văn A",
  "phone": "0901234567"
}
```

#### Refresh Token

```http
POST /auth/refresh
Authorization: Bearer <current_token>
```

---

## REST API Endpoints

### Reports - Quản Lý Báo Cáo

#### List Reports

```http
GET /reports?skip=0&limit=20&status=pending
Authorization: Bearer <token>
```

**Query Parameters:**

- `skip` (int): Offset cho pagination. Default: 0
- `limit` (int): Số lượng items. Default: 20, Max: 100
- `status` (string): Filter theo status: `pending`, `in_progress`, `completed`, `rejected`
- `category` (string): Filter theo category: `waste`, `air_pollution`, `noise`, `other`

**Response:**

```json
{
  "title": "string",
  "description": "string",
  "latitude": 0,
  "longitude": 0,
  "image_url": "string",
  "id": 0,
  "user_id": 0,
  "status": "PENDING",
  "created_at": "string"
}
```

#### Get Report Detail

```http
GET /reports/{report_id}
Authorization: Bearer <token>
```

#### Create Report (Mobile App)

```http
POST /reports
Authorization: Bearer <token>
Content-Type: multipart/form-data

{
  "title": "Tiêu đề báo cáo",
  "description": "Mô tả chi tiết",
  "category": "waste",
  "latitude": 21.0285,
  "longitude": 105.8542,
  "images": [<File1>, <File2>]
}
```

#### Update Report Status (Admin)

```http
PATCH /reports/{report_id}/status
Authorization: Bearer <admin_token>
Content-Type: application/json

{
  "status": "in_progress",
  "note": "Đã tiếp nhận, đang xử lý"
}
```

**Status Flow:**
```
pending → in_progress → completed
        ↘ rejected
```

---

### Infrastructure - Quản Lý Hạ Tầng

#### Parks - Công Viên

**List Parks:**

```http
GET /locations?location_type=PUBLIC_PARK&skip=0&limit=50
```

**Response:**

```json
{
  "name": "string",
  "location_type": "CHARGING_STATION",
  "description": "string",
  "id": 0,
  "data_source": "string",
  "is_active": true,
  "latitude": 0,
  "longitude": 0
}
```

**Create Park (Admin):**

```http
POST /locations
Authorization: Bearer <admin_token>
Content-Type: application/json

{
  "name": "Công viên Mới",
  "address": "Địa chỉ",
  "area_sqm": 10000,
  "latitude": 21.0285,
  "longitude": 105.8542,
  "description": "Mô tả",
  "amenities": ["playground"],
  "opening_hours": "06:00 - 21:00"
}
```

#### Charging Stations - Trạm Sạc

```http
GET /locations?location_type=CHARGING_STATION
```

**Response:**

```json
{
  "name": "string",
  "location_type": "CHARGING_STATION",
  "description": "string",
  "id": 0,
  "data_source": "string",
  "is_active": true,
  "latitude": 0,
  "longitude": 0
}
```

#### Bicycle Rentals - Cho Thuê Xe Đạp

```http
GET /locations?location_type=BICYCLE_RENTAL
```

---

### Environmental Data - Dữ Liệu Môi Trường

#### Air Quality Index (AQI)

```http
GET /aqi/hanoi?limit=100
```

**Response:**

```json
{
      "@context": "https://uri.etsi.org/ngsi-ld/v1/ngsi-ld-core-context-v1.8.jsonld",
      "id": "urn:ngsi-ld:AirQualityObserved:Hanoi:AnKhánh:7772012",
      "type": "https://smartdatamodels.org/dataModel.Environment/AirQualityObserved",
      "location": {
        "type": "GeoProperty",
        "value": {
          "type": "Point",
          "coordinates": [
            105.7181,
            21.0024
          ]
        }
      }
}
```

**Historical Data:**

```http
GET /aqi/hanoi?limit=168
```

#### Weather Data

```http
GET /weather/hanoi?limit=1
```

**Response:**
```json
{
      "@context": "https://uri.etsi.org/ngsi-ld/v1/ngsi-ld-core-context-v1.8.jsonld",
      "id": "urn:ngsi-ld:WeatherObserved:Hanoi:BaDinh",
      "type": "https://smartdatamodels.org/dataModel.Environment/WeatherObserved",
      "https://smartdatamodels.org/address": {
        "addressLocality": "Hanoi",
        "addressRegion": "Ba Đình",
        "addressCountry": "VN"
      },
      "location": {
        "type": "Point",
        "coordinates": [
          105.8372,
          21.0341
        ]
      },
      "https://smartdatamodels.org/dataModel.Environment/temperature": 21.1,
      "https://smartdatamodels.org/dataModel.Environment/relativeHumidity": 0.85,
      "https://smartdatamodels.org/dataModel.Environment/weatherType": "Âm u",
      "https://smartdatamodels.org/dataModel.Environment/windSpeed": 3.7,
      "https://smartdatamodels.org/dateObserved": "2025-12-11T10:15"
    }
```

**Forecast:**

```http
GET /weather/hanoi?limit=120
```

**Response:**
```json
"data": {
    "current": {
      "temp": 21.1,
      "humidity": 85,
      "wind_speed": 3.7,
      "desc": "Âm u",
      "time": "2025-12-11T10:15"
    },
    "hourly_24h": [
      {
        "time": "2025-12-11T11:00",
        "temp": 21.6,
        "rain_prob": 5,
        "desc": "Âm u"
      },
      {
        "time": "2025-12-11T12:00",
        "temp": 22.1,
        "rain_prob": 5,
        "desc": "Âm u"
      },
      {
        "time": "2025-12-11T13:00",
        "temp": 22.4,
        "rain_prob": 3,
        "desc": "Âm u"
      },
      {
        "time": "2025-12-11T14:00",
        "temp": 22.1,
        "rain_prob": 3,
        "desc": "Âm u"
      }
    ]
}
```

---

## NGSI-LD Context Broker

GreenMap tích hợp **Orion-LD Context Broker** để quản lý dữ liệu IoT theo chuẩn **FIWARE NGSI-LD**.

### Get Entities

```http
GET http://localhost:1026/ngsi-ld/v1/entities
Accept: application/ld+json
```

### Create Entity

```http
POST http://localhost:1026/ngsi-ld/v1/entities
Content-Type: application/ld+json

{
  "id": "urn:ngsi-ld:AirQualityObserved:HanoiStation01",
  "type": "AirQualityObserved",
  "location": {
    "type": "GeoProperty",
    "value": {
      "type": "Point",
      "coordinates": [105.8542, 21.0285]
    }
  },
  "aqi": {
    "type": "Property",
    "value": 85
  },
  "pm25": {
    "type": "Property",
    "value": 35.5,
    "unitCode": "GP"
  },
  "@context": [
    "https://uri.etsi.org/ngsi-ld/v1/ngsi-ld-core-context.jsonld"
  ]
}
```

[Xem chi tiết NGSI-LD →](ngsi-ld/)

---

## Error Handling

### HTTP Status Codes

| Code | Meaning | Description |
|------|---------|-------------|
| **200** | OK | Request thành công |
| **201** | Created | Resource được tạo thành công |
| **400** | Bad Request | Request không hợp lệ (validation error) |
| **401** | Unauthorized | Chưa đăng nhập hoặc token hết hạn |
| **403** | Forbidden | Không có quyền truy cập resource |
| **404** | Not Found | Resource không tồn tại |
| **422** | Unprocessable Entity | Dữ liệu không hợp lệ (chi tiết hơn 400) |
| **500** | Internal Server Error | Lỗi server |

### Error Response Format

```json
{
  "detail": "Error message here",
  "status_code": 400
}
```

| Status Code | Ý nghĩa |
|-------------|---------|
  "detail": "Validation error message"
}
```

**Validation Error (422):**

```json
{
  "detail": [
    {
      "loc": ["body", "email"],
      "msg": "field required",
      "type": "value_error.missing"
    }
  ]
}
```

---

## Rate Limiting

API có rate limiting để bảo vệ server:

- **Anonymous requests:** 100 requests/hour
- **Authenticated users:** 1000 requests/hour
- **Admin users:** 5000 requests/hour

Headers trả về:

```http
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 995
X-RateLimit-Reset: 1639151400
```

---

## Swagger UI

Khi chạy backend server, truy cập tài liệu tương tác tại:

- **Swagger UI:** `http://localhost:8000/docs`
- **ReDoc:** `http://localhost:8000/redoc`
- **OpenAPI JSON:** `http://localhost:8000/openapi.json`

Swagger UI cho phép:
- Test API trực tiếp từ browser
- Xem schema của request/response
- Tự động generate client code

---

## Code Examples

### Python (httpx)

```python
import httpx

BASE_URL = "http://localhost:8000"

# Login
response = httpx.post(
    f"{BASE_URL}/auth/login",
    data={"username": "admin@myhou.io.vn", "password": "password"}
)
token = response.json()["access_token"]

# Get reports
headers = {"Authorization": f"Bearer {token}"}
reports = httpx.get(
    f"{BASE_URL}/reports",
    headers=headers,
    params={"status": "pending", "limit": 10}
).json()

print(reports)
```

### JavaScript (fetch)

```javascript
const BASE_URL = 'http://localhost:8000';

// Login
const loginResponse = await fetch(`${BASE_URL}/auth/login`, {
  method: 'POST',
  headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
  body: new URLSearchParams({
    username: 'admin@myhou.io.vn',
    password: 'password'
  })
});

const { access_token } = await loginResponse.json();

// Get reports
const reportsResponse = await fetch(
  `${BASE_URL}/reports?status=pending&limit=10`,
  {
    headers: { 'Authorization': `Bearer ${access_token}` }
  }
);

const reports = await reportsResponse.json();
console.log(reports);
```

### Kotlin (Ktor)

```kotlin
import io.ktor.client.*
import io.ktor.client.request.*
import io.ktor.client.statement.*
import io.ktor.http.*

val client = HttpClient()
val baseUrl = "http://localhost:8000"

// Login
val loginResponse: HttpResponse = client.post("$baseUrl/auth/login") {
    contentType(ContentType.Application.FormUrlEncoded)
    setBody("username=admin@myhou.io.vn&password=password")
}

val token = loginResponse.body<LoginResponse>().accessToken

// Get reports
val reports: ReportsResponse = client.get("$baseUrl/reports") {
    header("Authorization", "Bearer $token")
    parameter("status", "pending")
    parameter("limit", 10)
}.body()

println(reports)
```

---

## Pagination

Tất cả list endpoints đều hỗ trợ pagination:

**Request:**
```http
GET /reports?skip=20&limit=10
```

**Response:**
```json
{
  "items": [...],
  "total": 150,
  "skip": 20,
  "limit": 10
}
```

**Calculation:**
- Page 1: `skip=0, limit=20`
- Page 2: `skip=20, limit=20`
- Page 3: `skip=40, limit=20`
- Total pages: `ceil(total / limit)`

---

## News - Tin Tức Môi Trường

### Get News from Hà Nội Mới

```http
GET /news/hanoimoi?limit=20
```

**Query Parameters:**

- `limit` (int): Số lượng tin tức trả về. Default: 20, Max: 50

**Response:**

```json
[
  {
    "title": "string",
    "link": "string",
    "description": "string",
    "published_at": "2025-12-11T03:26:54.934Z",
    "image_url": "string",
    "source": "vnexpress"
  }
]
```

---

## Traffic - Dữ Liệu Giao Thông

### Get Traffic Segments (GeoJSON)

```http
GET /traffic/segments
```

**Response:**

```json
{
      "type": "Feature",
      "id": "28958235#7_0",
      "geometry": {
        "type": "LineString",
        "coordinates": [
          [
            105.825079,
            20.999466
          ],
          [
            105.825288,
            20.999379
          ]
        ]
      },
      "properties": {
        "id": "28958235#7_0",
        "name": "Đoạn đường 28958235#7_0"
      }
    }
```

### Get Live Traffic Status

```http
GET /traffic/live
```

**Response:**

```json
{
    "time_real": 1564,
  "time_query": 1560,
  "status": {
    "596710689#0_1": "red",
    "600083145#2_0": "red",
    "705794897_0": "red",
    "848915392#0_0": "orange",
    "35972592#3_0": "red",
    "397649390#3_3": "red",
    "397649390#3_1": "red",
    "596710689#1_1": "red",
    "-1266085189#0_0": "red",
    "725772905#3_0": "red",
    "1331204980#1_0": "red",
    "709673461#1_0": "red",
    "35972592#2_1": "red",
    "708658353#1_2": "red",
    "35978173_0": "red",
    "711367567_1": "red",
    "875229039_0": "red",
    "848915392#0_1": "orange",
    "711367569#1_1": "red",
    "1014224394_0": "red",
    "397649390#2_1": "red",
    "1204912791#2_0": "green",
    "848915394#6_0": "red"
    }
}
```

**Status Colors:**

- `green`: Thông thoáng (0-30 xe)
- `yellow`: Bình thường (30-60 xe)
- `red`: Ùn tắc (>60 xe)

---

## AI Insights - Phân Tích Thông Minh

### Generate AI Weather Insights

```http
POST /ai/weather-insights?lat=21.0285&lon=105.8542&provider=auto
Authorization: Bearer <token>
Content-Type: application/json
```

**Query Parameters:**

- `lat` (float): Vĩ độ. Default: 21.0285 (Hà Nội)
- `lon` (float): Kinh độ. Default: 105.8542 (Hà Nội)
- `provider` (string): AI provider - `gemini`, `groq`, hoặc `auto`
- `model` (string, optional): Ghi đè model mặc định (ví dụ: `gemini-1.5-pro`)

**Response:**

```json
{
  "lat": 0,
  "lon": 0,
  "provider": "string",
  "model": "string",
  "analysis": "string",
  "context": {
    "additionalProp1": {}
  },
  "id": 0,
  "user_id": 0,
  "created_at": "2025-12-11T03:30:27.213Z"
}
```

### Get AI Insights History

```http
GET /ai/weather-insights/history?skip=0&limit=20
Authorization: Bearer <token>
```

**Response:**

```json
[
  {
    "lat": 0,
    "lon": 0,
    "provider": "string",
    "model": "string",
    "analysis": "string",
    "context": {
      "additionalProp1": {}
    },
    "id": 0,
    "user_id": 0,
    "created_at": "2025-12-11T03:30:27.150Z"
  }
]
```

---

## Notifications - Quản Lý Thông Báo

### Send Notification to All Devices

```http
POST /notifications/send
Authorization: Bearer <admin_token>
Content-Type: application/json

{
  "title": "Cảnh báo AQI cao",
  "body": "AQI Hà Nội đạt 152 - Kém. Hạn chế ra ngoài.",
  "data": {
    "aqi": 152,
    "location": "Hanoi"
  },
  "dry_run": false
}
```

**Response:**

```json
{
  "id": 123,
  "title": "Cảnh báo AQI cao",
  "body": "AQI Hà Nội đạt 152...",
  "data": {...},
  "success_count": 45,
  "failure_count": 2,
  "created_at": "2024-12-15T10:30:00Z"
}
```

### Send Notification to Topic

```http
POST /notifications/send/topic
Authorization: Bearer <admin_token>
Content-Type: application/json

{
  "title": "Tin tức môi trường",
  "body": "Hà Nội trồng thêm 10,000 cây xanh",
  "topic": "greenmap_all",
  "data": {},
  "dry_run": false
}
```

### Get Notification History

```http
GET /notifications/history?skip=0&limit=20
Authorization: Bearer <admin_token>
```

### Get Registered Device Tokens

```http
GET /notifications/tokens
Authorization: Bearer <admin_token>
```

**Response:**

```json
{
  "id": 0,
  "token": "string",
  "platform": "string",
  "is_active": true,
  "user_id": 0,
  "last_sent_at": "2025-12-11T03:27:29.955Z",
  "created_at": "2025-12-11T03:27:29.955Z"
}
```

### Cleanup Old Notifications

```http
DELETE /notifications/history/cleanup?days=90
Authorization: Bearer <admin_token>
```

---

## Filtering & Sorting

**Filter by multiple fields:**
```http
GET /reports?status=pending&limit=&skip=
```

---

## Webhooks (Coming Soon)

GreenMap sẽ hỗ trợ webhooks để notify external services khi có sự kiện:

- New report created
- Report status changed
- AQI exceeds threshold
- New park added

---

## API Versioning

API hiện tại: **v1**

Các breaking changes sẽ được release ở version mới (v2, v3...) và maintain song song với version cũ trong 6 tháng.

---

## Support

- **API Documentation:** [https://backend.myhou.io.vn/docs](https://backend.myhou.io.vn/docs)
- **GitHub Issues:** [https://github.com/HouHackathon-CQP/GreenMap-Backend/issues](https://github.com/HouHackathon-CQP/GreenMap-Backend/issues)
- **Email:** api-support@myhou.io.vn

---

## Users - Quản lý người dùng

### List Users

```http
GET /users
Authorization: Bearer <token>
```

**Response:**
```json
[
  {
    "email": "user@example.com",
    "full_name": "string",
    "id": 0,
    "is_active": true,
    "role": "ADMIN"
  }
]
```

---

### AI Directions

```http
POST /ai/directions
Authorization: Bearer <token>
Content-Type: application/json
```

**Response:**
```json
{
  "start": {
    "name": "string",
    "lat": 0,
    "lon": 0
  },
  "destination": {
    "name": "string",
    "lat": 0,
    "lon": 0
  },
  "via_pois": [
    {
      "name": "string",
      "lat": 0,
      "lon": 0,
      "type": "string"
    }
  ],
  "route": {
    "distance": 0,
    "duration": 0,
    "geometry": {
      "type": "string",
      "coordinates": [
        [
          0
        ]
      ]
    }
  },
  "summary": "string"
}
```
