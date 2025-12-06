# Hướng Dẫn Bắt Đầu Nhanh

Hướng dẫn này giúp bạn khởi chạy toàn bộ GreenMap system trong 10-15 phút.

## Điều Kiện Tiên Quyết

Đảm bảo bạn đã:
- Clone tất cả 4 repositories từ [Hướng Dẫn Cài Đặt](installation.md)
- Cài đặt các dependencies cần thiết
- Khởi động Docker services cho Backend

## Bước 1: Khởi Động Backend Services

```bash
cd d:\GreenMap\GreenMap-Backend

# Kích hoạt venv (nếu chưa)
.\.venv\Scripts\activate

# Khởi động Docker containers
docker-compose up -d

# Kiểm tra containers đã chạy
docker-compose ps
```

Chờ 10-15 giây để PostgreSQL, MongoDB, và Orion-LD khởi động.

## Bước 2: Khởi Tạo Database (Lần Đầu)

```bash
# Với venv đã kích hoạt
python init_db.py

# Xem output để xác nhận
```

## Bước 3: Khởi Động Backend API

Mở **Terminal 1** và chạy:

```bash
cd d:\GreenMap\GreenMap-Backend
.\.venv\Scripts\activate
python main.py
```

Chờ cho đến khi thấy:
```
Uvicorn running on http://127.0.0.1:8000
```

### Kiểm Tra Backend

Mở browser và truy cập: **http://localhost:8000/docs**

Bạn sẽ thấy Swagger API documentation.

## Bước 4: Khởi Động Agents (Tùy Chọn)

Mở **Terminal 2** và chạy AQI Agent:

```bash
cd d:\GreenMap\GreenMap-Backend
.\.venv\Scripts\activate
python aqi_agent.py
```

Mở **Terminal 3** và chạy Weather Agent:

```bash
cd d:\GreenMap\GreenMap-Backend
.\.venv\Scripts\activate
python weather_agent.py
```

Các agents này cập nhật dữ liệu AQI và thời tiết realtime từ external APIs.

## Bước 5: Khởi Động Frontend

Mở **Terminal 4** và chạy:

```bash
cd d:\GreenMap\GreenMap-Frontend
npm run dev
```

Chờ cho đến khi thấy:
```
Local:   http://localhost:3000/
```

### Kiểm Tra Frontend

Mở browser và truy cập: **http://localhost:3000**

Bạn sẽ thấy GreenMap web application.

## Bước 6: Khám Phá Application

### Đăng Ký / Đăng Nhập

1. Nhấp **Sign Up** (hoặc **Login** nếu đã có account)
2. Điền thông tin:
   - Email
   - Password
   - Confirm Password
3. Nhấp **Create Account**

### Khám Phá Bản Đồ

1. Sau khi đăng nhập, bạn sẽ thấy bản đồ tương tác
2. Các điểm dữ liệu hiển thị:
   - 🟢 Sensors (chất lượng không khí)
   - 🚲 Bicycle Rental Stations
   - 🔌 Charging Stations
   - 🌳 Parks
   - 🏛️ Tourist Attractions

### Xem Chi Tiết

1. Nhấp vào bất kỳ điểm nào trên bản đồ
2. Xem thông tin chi tiết:
   - Tên vị trí
   - Tọa độ
   - AQI value (nếu có)
   - Thời tiết cục bộ
   - Dữ liệu lịch sử

### Lọc Dữ Liệu

Sử dụng sidebar bên trái để lọc theo:
- Loại dữ liệu (sensors, bikes, charging, etc.)
- Khoảng AQI
- Thời gian

## Bước 7: Xem Tài Liệu (Tùy Chọn)

Mở **Terminal 5** để xem documentation:

```bash
cd d:\GreenMap\GreenMap-Documents
.\.venv\Scripts\activate
mkdocs serve
```

Truy cập: **http://localhost:8000/GreenMap-Documents/**

## Tóm Tắt Các Port

| Ứng Dụng | URL | Terminal |
|---------|-----|----------|
| **Backend API** | http://localhost:8000 | Terminal 1 |
| **AQI Agent** | (Background) | Terminal 2 |
| **Weather Agent** | (Background) | Terminal 3 |
| **Frontend** | http://localhost:3000 | Terminal 4 |
| **Documentation** | http://localhost:8000/GreenMap-Documents/ | Terminal 5 |

## Xử Lý Sự Cố Nhanh

### Frontend không load

```bash
# Xóa cache và cài lại
cd d:\GreenMap\GreenMap-Frontend
rm -r node_modules
npm install
npm run dev
```

### Database connection error

```bash
# Kiểm tra Docker containers
docker-compose ps

# Xem logs
docker-compose logs postgres

# Restart if needed
docker-compose restart
```

### Port đã bị chiếm dụng

Thay đổi port trong config files hoặc:
```bash
# Tìm process đang sử dụng port
netstat -ano | findstr :3000

# Kill process (Windows)
taskkill /PID <PID> /F
```

## Các Bước Tiếp Theo

1. **Đọc User Guide** - [Hướng Dẫn Người Dùng](../user-guide/overview.md)
2. **Tìm Hiểu API** - [API Reference](../api-reference/overview.md)
3. **Contribute Code** - [Contributing Guidelines](../contributing/guidelines.md)
4. **Tìm Kiếm Issues** - [GitHub Issues](https://github.com/HouHackathon-CQP)

## Cần Giúp?

- Kiểm tra [FAQ](../user-guide/faq.md) (nếu có)
- Xem logs của các terminals
- Mở issue trên GitHub repositories

---

**🎉 Chúc mừng! Bạn đã thiết lập GreenMap thành công!**
