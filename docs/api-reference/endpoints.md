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

<!--docs/api-reference/endpoints.md-->
# Các Điểm Cuối API (Endpoints)

**Lưu Ý:** GreenMap-Backend hiện đang trong giai đoạn phát triển. Danh sách endpoints dưới đây là dự kiến và có thể thay đổi.

Để xem danh sách đầy đủ các endpoints hiện có, vui lòng truy cập **Swagger UI** khi Backend đang chạy:

```
http://localhost:8000/docs
```

## Endpoints Hiện Có

### 🔐 Xác Thực (Authentication)

- `POST /auth/register` - Đăng ký người dùng mới
- `POST /auth/login` - Đăng nhập (trả về access token)
- `GET /auth/me` - Lấy thông tin người dùng hiện tại

### 👥 Người Dùng (Users)

- `GET /users` - Lấy danh sách người dùng (Admin)
- `GET /users/me` - Lấy thông tin user hiện tại
- `PUT /users/{user_id}` - Cập nhật thông tin user
- `DELETE /users/{user_id}` - Xóa user (Admin)

### 📍 Địa Điểm (Locations)

- `GET /locations` - Lấy danh sách địa điểm (hỗ trợ filter theo `location_type`)
- `GET /locations/{id}` - Lấy chi tiết địa điểm
- `POST /locations` - Tạo địa điểm mới (Admin)
- `PUT /locations/{id}` - Cập nhật địa điểm (Admin)
- `DELETE /locations/{id}` - Xóa địa điểm (Admin)

**Location Types:**
- `CHARGING_STATION` - Trạm sạc xe điện
- `PUBLIC_PARK` - Công viên công cộng
- `BICYCLE_RENTAL` - Điểm thuê xe đạp
- `TOURIST_ATTRACTION` - Điểm tham quan du lịch

### 🌫️ Chất Lượng Không Khí (AQI)

- `GET /aqi/hanoi?limit=100` - Lấy dữ liệu AQI từ Orion-LD Context Broker

### 🌤️ Thời Tiết (Weather)

- `GET /weather/hanoi?limit=100` - Lấy dữ liệu thời tiết từ Orion-LD

### 🚗 Giao Thông (Traffic)

- `GET /traffic/segments` - Lấy dữ liệu các đoạn đường (GeoJSON)
- `GET /traffic/live` - Lấy dữ liệu giao thông real-time

### 📢 Báo Cáo (Reports)

- `GET /reports` - Danh sách báo cáo (hỗ trợ filter theo `status`)
- `GET /reports/{id}` - Chi tiết báo cáo
- `POST /reports` - Tạo báo cáo mới
- `PUT /reports/{id}` - Cập nhật trạng thái báo cáo (Admin)
- `DELETE /reports/{id}` - Xóa báo cáo

**Report Status:**
- `PENDING` - Chờ xử lý
- `APPROVED` - Đã duyệt
- `REJECTED` - Đã từ chối

### 📰 Tin Tức (News)

- `GET /news/hanoimoi?limit=20` - Lấy tin tức môi trường từ báo Hà Nội Mới (RSS)

### 🔔 Thông Báo (Notifications)

- `POST /notifications/register` - Đăng ký device token (Mobile)
- `DELETE /notifications/register/{token}` - Hủy đăng ký token
- `GET /notifications/tokens` - Danh sách device tokens (Admin)
- `POST /notifications/send` - Gửi push notification (Admin)
- `POST /notifications/send/topic` - Gửi theo topic (Admin)
- `GET /notifications/history` - Xem lịch sử notifications (Admin)
- `GET /notifications/history/{id}` - Chi tiết lịch sử
- `DELETE /notifications/cleanup` - Dọn dẹp lịch sử cũ (Admin)

### 🤖 AI Insights

- `POST /ai/weather-insights?lat=21.0285&lon=105.8542` - Phân tích thời tiết & AQI bằng AI
- `POST /ai/weather-insights?provider=gemini` - Chọn AI provider (gemini/groq/auto)
- `GET /ai/weather-insights/history?limit=10` - Xem lịch sử phân tích AI

### 📤 Uploads

- `POST /upload/image` - Upload ảnh (multipart/form-data)

### ⚙️ System

- `GET /` - Health check
- `GET /health` - System health status

## Cách Xem Tài Liệu Chi Tiết

1. **Khởi động Backend**:
   ```bash
   cd d:\GreenMap\GreenMap-Backend
   .\.venv\Scripts\activate
   python main.py
   ```

2. **Truy cập Swagger UI**:
   - Mở browser: `http://localhost:8000/docs`
   - Giao diện Swagger sẽ hiển thị tất cả endpoints
   - Bạn có thể test trực tiếp từ đây

3. **Hoặc xem ReDoc**:
   - `http://localhost:8000/redoc`

## Xác Thực

Hầu hết các endpoints cần token JWT. Lấy token bằng cách:

```bash
POST /api/auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "password123"
}
```

Sau đó sử dụng token trong header:

```bash
Authorization: Bearer YOUR_TOKEN
```

## Lỗi Thường Gặp

| Mã | Ý Nghĩa |
|----|---------|
| 200 | OK - Thành công |
| 201 | Created - Tạo mới thành công |
| 400 | Bad Request - Yêu cầu không hợp lệ |
| 401 | Unauthorized - Cần xác thực |
| 403 | Forbidden - Không có quyền |
| 404 | Not Found - Không tìm thấy |
| 500 | Internal Server Error - Lỗi server |

## Bạn Cần Giúp?

- Xem [API Overview](overview.md) để hiểu rõ hơn
- Truy cập [Backend Repository](https://github.com/HouHackathon-CQP/GreenMap-Backend) để code
- Tạo issue trên GitHub nếu tìm thấy bug

---

**Lưu Ý:** Vì GreenMap-Backend đang phát triển, danh sách endpoints có thể thay đổi. Luôn kiểm tra Swagger UI để có danh sách mới nhất.
