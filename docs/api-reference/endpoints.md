# Các Điểm Cuối API (Endpoints)

**Lưu Ý:** GreenMap-Backend hiện đang trong giai đoạn phát triển. Danh sách endpoints dưới đây là dự kiến và có thể thay đổi.

Để xem danh sách đầy đủ các endpoints hiện có, vui lòng truy cập **Swagger UI** khi Backend đang chạy:

```
http://localhost:8000/docs
```

## Endpoints Hiện Có

### Xác Thực (Authentication)

- `POST /api/auth/register` - Đăng ký người dùng mới
- `POST /api/auth/login` - Đăng nhập
- `POST /api/auth/logout` - Đăng xuất
- `GET /api/auth/me` - Lấy thông tin người dùng hiện tại
- `PUT /api/auth/profile` - Cập nhật profile

### Địa Điểm (Locations)

- `GET /api/locations` - Lấy danh sách địa điểm
- `GET /api/locations/{id}` - Lấy chi tiết địa điểm
- `POST /api/locations` - Tạo địa điểm mới
- `PUT /api/locations/{id}` - Cập nhật địa điểm
- `DELETE /api/locations/{id}` - Xóa địa điểm

### Cảm Biến (Sensors)

- `GET /api/sensors` - Lấy tất cả sensors
- `GET /api/sensors/{id}` - Chi tiết sensor
- `GET /api/sensors/{id}/aqi` - Dữ liệu AQI hiện tại
- `GET /api/sensors/{id}/history` - Lịch sử AQI

### Báo Cáo (Reports)

- `GET /api/reports` - Danh sách báo cáo
- `POST /api/reports` - Tạo báo cáo mới
- `GET /api/reports/{id}` - Chi tiết báo cáo
- `PUT /api/reports/{id}` - Cập nhật báo cáo
- `DELETE /api/reports/{id}` - Xóa báo cáo

### Thời Tiết (Weather)

- `GET /api/weather` - Dữ liệu thời tiết hiện tại
- `GET /api/weather/forecast` - Dự báo thời tiết

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
