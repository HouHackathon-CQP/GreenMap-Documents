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
| **Staging** | `https://api-staging.greenmap.vn` | `https://orion-staging.greenmap.vn` |
| **Production** | `https://api.greenmap.vn` | `https://orion.greenmap.vn` |

---

## Authentication

### JWT Token Authentication

GreenMap sử dụng **JWT (JSON Web Tokens)** để xác thực người dùng.

#### Login Endpoint

```http
POST /auth/login
Content-Type: application/x-www-form-urlencoded

username=admin@greenmap.vn
password=your_password
```

**Response:**

```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "bearer",
  "expires_in": 3600
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
  "items": [
    {
      "id": 123,
      "title": "Rác thải tràn lan",
      "description": "Nhiều rác thải chưa được thu gom",
      "category": "waste",
      "status": "pending",
      "latitude": 21.0285,
      "longitude": 105.8542,
      "address": "Hoàn Kiếm, Hà Nội",
      "images": ["https://storage.greenmap.vn/reports/123/img1.jpg"],
      "created_by": {
        "id": 456,
        "full_name": "Nguyễn Văn A",
        "phone": "0901234567"
      },
      "created_at": "2024-12-10T10:30:00Z",
      "updated_at": "2024-12-10T10:30:00Z"
    }
  ],
  "total": 150,
  "skip": 0,
  "limit": 20
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
  "items": [
    {
      "id": 1,
      "name": "Công viên Thống Nhất",
      "address": "Hai Bà Trưng, Hà Nội",
      "area_sqm": 50000,
      "latitude": 21.0167,
      "longitude": 105.8456,
      "description": "Công viên lớn nhất quận Hai Bà Trưng",
      "amenities": ["playground", "jogging_track", "restroom"],
      "opening_hours": "05:00 - 22:00",
      "images": ["https://storage.greenmap.vn/parks/1/img1.jpg"]
    }
  ],
  "total": 45
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
  "items": [
    {
      "id": 1,
      "name": "VinFast Station Hà Đông",
      "address": "Hà Đông, Hà Nội",
      "latitude": 20.9716,
      "longitude": 105.7746,
      "total_ports": 8,
      "available_ports": 5,
      "port_types": ["Type 2", "CCS"],
      "power_kw": 150,
      "pricing": "5000 VND/kWh",
      "status": "operational"
    }
  ]
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
  "city": "Hanoi",
  "aqi": 85,
  "level": "Moderate",
  "color": "#FFFF00",
  "pm25": 35.5,
  "pm10": 65.2,
  "o3": 45.0,
  "no2": 25.3,
  "so2": 15.1,
  "co": 0.8,
  "measured_at": "2024-12-10T14:00:00Z",
  "source": "OpenAQ"
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
  "temperature": 28.5,
  "feels_like": 30.2,
  "humidity": 75,
  "pressure": 1013,
  "wind_speed": 3.5,
  "wind_direction": 180,
  "clouds": 45,
  "weather": "Clouds",
  "description": "scattered clouds",
  "icon": "03d",
  "measured_at": "2024-12-10T14:00:00Z"
}
```

**Forecast:**

```http
GET /weather/hanoi?limit=120
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
    data={"username": "admin@greenmap.vn", "password": "password"}
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
    username: 'admin@greenmap.vn',
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
    setBody("username=admin@greenmap.vn&password=password")
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
    "title": "Hà Nội tăng cường trồng cây xanh",
    "link": "https://hanoimoi.com.vn/...",
    "description": "Thành phố Hà Nội đặt mục tiêu trồng 1 triệu cây xanh...",
    "published": "2024-12-15T08:30:00+07:00",
    "author": "Hà Nội Mới"
  }
]
```

---

## Traffic - Dữ Liệu Giao Thông

### Get Traffic Segments (GeoJSON)

```http
GET /api/v1/traffic/segments
```

**Response:**

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "id": "123",
      "geometry": {
        "type": "LineString",
        "coordinates": [[105.8542, 21.0285], [105.8550, 21.0290]]
      },
      "properties": {
        "id": "123",
        "name": "Đoạn đường 123"
      }
    }
  ]
}
```

### Get Live Traffic Status

```http
GET /api/v1/traffic/live
```

**Response:**

```json
{
  "time_real": 1234,
  "time_query": 1230,
  "status": {
    "123": "green",
    "124": "yellow",
    "125": "red"
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
POST /api/v1/ai/weather-insights?lat=21.0285&lon=105.8542&provider=auto
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
  "id": 45,
  "provider": "gemini",
  "model": "gemini-1.5-flash",
  "lat": 21.0285,
  "lon": 105.8542,
  "analysis": "📊 Phân tích Thời tiết & Chất lượng Không khí Hà Nội\n\n**Thời tiết hiện tại:**\n- Nhiệt độ: 25°C, cảm giác như 23°C\n- Độ ẩm: 65%, Gió: 12 km/h\n\n**Chất lượng không khí:**\n- AQI: 85 (Trung bình) - PM2.5: 28 µg/m³\n\n**Lời khuyên:**\n- ✅ Đi bộ, chạy bộ nhẹ: An toàn\n- ⚠️ Người nhạy cảm nên hạn chế hoạt động ngoài trời kéo dài",
  "context": {
    "weather_current": {...},
    "weather_forecast": {...},
    "aqi": {...}
  },
  "user_id": 1,
  "created_at": "2024-12-15T10:30:00Z"
}
```

### Get AI Insights History

```http
GET /api/v1/ai/weather-insights/history?skip=0&limit=20
Authorization: Bearer <token>
```

**Response:**

```json
[
  {
    "id": 45,
    "provider": "gemini",
    "model": "gemini-1.5-flash",
    "lat": 21.0285,
    "lon": 105.8542,
    "analysis": "...",
    "created_at": "2024-12-15T10:30:00Z"
  }
]
```

---

## Notifications - Quản Lý Thông Báo

### Send Notification to All Devices

```http
POST /api/v1/notifications/send
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
POST /api/v1/notifications/send/topic
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
GET /api/v1/notifications/history?skip=0&limit=20
Authorization: Bearer <admin_token>
```

### Get Registered Device Tokens

```http
GET /api/v1/notifications/tokens
Authorization: Bearer <admin_token>
```

**Response:**

```json
[
  {
    "id": 1,
    "device_token": "fK7x...",
    "user_id": 123,
    "created_at": "2024-12-01T10:00:00Z"
  }
]
```

### Cleanup Old Notifications

```http
DELETE /api/v1/notifications/cleanup?days=30
Authorization: Bearer <admin_token>
```

---

## Filtering & Sorting

**Filter by multiple fields:**
```http
GET /api/v1/reports?status=pending&category=waste&created_after=2024-12-01
```

**Sort results:**
```http
GET /api/v1/reports?sort_by=created_at&order=desc
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

- **API Documentation:** [https://api.greenmap.vn/docs](https://api.greenmap.vn/docs)
- **GitHub Issues:** [https://github.com/HouHackathon-CQP/GreenMap-Backend/issues](https://github.com/HouHackathon-CQP/GreenMap-Backend/issues)
- **Email:** api-support@greenmap.vn
