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

<!--docs/api-reference/overview.md-->
# Tài Liệu API - Tổng Quan

Chào mừng đến tài liệu API của **GreenMap-Backend**! 

## GreenMap-Backend API Là Gì?

**GreenMap-Backend** cung cấp REST API để:
- Lấy dữ liệu sensors (AQI, thời tiết)
- Quản lý người dùng (đăng ký, đăng nhập)
- Tạo và quản lý báo cáo sự cố
- Tương tác với Context Broker (Orion-LD)
- Quản lý các địa điểm (locations)

## URL Cơ Sở API

```
Phát triển cục bộ: http://localhost:8000
Phần tài liệu: http://localhost:8000/docs (Swagger UI)
```

## Xác Thực

API sử dụng **OAuth2 và JWT tokens**:

### 1. Đăng Nhập (Lấy Token)

```bash
POST /api/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "password123"
}
```

Response:
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIs...",
  "token_type": "bearer",
  "user": {
    "id": "123",
    "email": "user@example.com",
    "role": "user"
  }
}
```

### 2. Sử Dụng Token

Bao gồm token trong header:

```http
GET /api/locations
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...
```

## Giới Hạn Tỷ Lệ

- **Public endpoints:** 100 requests/hour
- **Authenticated endpoints:** 1000 requests/hour
- **Reset:** Mỗi giờ UTC

## Mã Trạng Thái HTTP

| Mã | Ý Nghĩa |
|----|---------|
| 200 | OK - Thành công |
| 201 | Created - Tạo mới thành công |
| 400 | Bad Request - Yêu cầu không hợp lệ |
| 401 | Unauthorized - Cần xác thực |
| 403 | Forbidden - Không có quyền |
| 404 | Not Found - Không tìm thấy |
| 500 | Internal Server Error - Lỗi server |

## Cấu Trúc Phản Hồi

### Thành Công

```json
{
  "success": true,
  "data": {...},
  "message": "Operation successful"
}
```

### Lỗi

```json
{
  "success": false,
  "error": "Error message",
  "code": "ERROR_CODE",
  "details": {...}
}
```

## Các Endpoints Chính

### Tài Khoản & Xác Thực

- `POST /api/auth/register` - Đăng ký người dùng mới
- `POST /api/auth/login` - Đăng nhập
- `POST /api/auth/logout` - Đăng xuất
- `GET /api/auth/me` - Lấy thông tin người dùng hiện tại
- `PUT /api/auth/profile` - Cập nhật profile

### Locations (Địa điểm)

- `GET /api/locations` - Lấy danh sách địa điểm
- `GET /api/locations/{id}` - Lấy chi tiết địa điểm
- `POST /api/locations` - Tạo địa điểm mới
- `PUT /api/locations/{id}` - Cập nhật địa điểm
- `DELETE /api/locations/{id}` - Xóa địa điểm

### Sensors (Cảm Biến)

- `GET /api/sensors` - Lấy tất cả sensors
- `GET /api/sensors/{id}` - Chi tiết sensor
- `GET /api/sensors/{id}/aqi` - Dữ liệu AQI hiện tại
- `GET /api/sensors/{id}/history` - Lịch sử AQI

### Reports (Báo Cáo)

- `GET /api/reports` - Danh sách báo cáo
- `POST /api/reports` - Tạo báo cáo mới
- `GET /api/reports/{id}` - Chi tiết báo cáo
- `PUT /api/reports/{id}` - Cập nhật báo cáo
- `DELETE /api/reports/{id}` - Xóa báo cáo

### Weather (Thời Tiết)

- `GET /api/weather` - Dữ liệu thời tiết hiện tại
- `GET /api/weather/forecast` - Dự báo thời tiết

### Context Broker (Orion-LD)

- `GET /api/context/entities` - Lấy các entities
- `GET /api/context/entities/{id}` - Chi tiết entity
- `POST /api/context/entities` - Tạo entity mới

## Ví Dụ Sử Dụng

### Lấy Danh Sách Sensors

```bash
curl -X GET "http://localhost:8000/api/sensors" \
  -H "Authorization: Bearer YOUR_TOKEN"
```

Response:
```json
{
  "success": true,
  "data": [
    {
      "id": "sensor_001",
      "name": "Sensor District 1",
      "location": {
        "lat": 10.7769,
        "lng": 106.6296
      },
      "aqi": 45,
      "lastUpdate": "2024-01-15T10:30:00Z"
    }
  ]
}
```

### Tạo Báo Cáo

```bash
curl -X POST "http://localhost:8000/api/reports" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Air Pollution Alert",
    "description": "High pollution detected",
    "location": {
      "lat": 10.7769,
      "lng": 106.6296
    },
    "category": "pollution",
    "severity": "high"
  }'
```

## Công Cụ Thử Nghiệm

### Swagger UI

Khi Backend chạy, truy cập:

```
http://localhost:8000/docs
```

Giao diện Swagger cho phép bạn:
- Xem tất cả endpoints
- Kiểm tra yêu cầu/phản hồi
- Thử trực tiếp các API calls

### API Testing Tools

- **Postman** - GUI client
- **curl** - Command line
- **Thunder Client** - VS Code extension
- **REST Client** - VS Code extension

## Pagination

Các endpoints danh sách hỗ trợ pagination:

```bash
GET /api/sensors?page=1&limit=10&sort=name&order=asc
```

Query Parameters:
- `page` - Trang hiện tại (mặc định: 1)
- `limit` - Số mục mỗi trang (mặc định: 20)
- `sort` - Trường để sort
- `order` - asc hoặc desc

## Caching

API sử dụng HTTP caching headers:

```
Cache-Control: max-age=300
```

Bạn nên respect các headers này trong client.

## Webhooks (Tùy Chọn)

Hiện tại không hỗ trợ webhooks, nhưng có thể thêm vào tương lai.

## Lỗi Thường Gặp

### 401 Unauthorized
- Token hết hạn → Đăng nhập lại
- Token không hợp lệ → Kiểm tra syntax
- Thiếu header Authorization → Thêm header

### 403 Forbidden
- Không có quyền truy cập → Kiểm tra role

### 404 Not Found
- Endpoint không tồn tại → Kiểm tra URL
- Resource không tồn tại → Kiểm tra ID

### 429 Too Many Requests
- Vượt giới hạn tỷ lệ → Chờ trước khi request lại

## Các Tài Liệu Tiếp Theo

- [Endpoints API Endpoints](endpoints.md) - Chi tiết mỗi endpoint
- [Backend Repository](../../../GreenMap-Backend/README.md) - GitHub repo
- [Contributing](../contributing/guidelines.md) - Đóng góp code

## Liên Hệ & Hỗ Trợ

- **GitHub Issues:** Report bugs tại GitHub repos
- **Discussions:** Thảo luận trên GitHub
- **Documentation:** Xem đầy đủ docs tại đây

---

**Sẵn sàng bắt đầu với API? Hãy kiểm tra [Endpoints](endpoints.md)! 🚀**
