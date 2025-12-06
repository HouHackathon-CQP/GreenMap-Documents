# Hướng Dẫn Cài Đặt Toàn Bộ GreenMap

Hướng dẫn này giúp bạn cài đặt tất cả 4 repositories của dự án GreenMap từ GitHub.

## Yêu Cầu Tiên Quyết

Trước khi bắt đầu, hãy đảm bảo bạn có:

- **Git** - Để clone repositories
- **Python 3.10+** - Cho Backend
- **Node.js 18+** - Cho Frontend
- **Docker & Docker Compose** - Cho các services (PostgreSQL, MongoDB, Orion-LD)
- Trình duyệt web hiện đại (Chrome, Firefox, Safari, Edge)

## Bước 1: Tạo Thư Mục Quản Lý Chung

Tạo folder gốc để quản lý tất cả repositories:

```bash
mkdir d:\GreenMap
cd d:\GreenMap
```

## Bước 2: Clone Tất Cả Repositories

```bash
# Clone Backend
git clone https://github.com/HouHackathon-CQP/GreenMap-Backend.git

# Clone Frontend
git clone https://github.com/HouHackathon-CQP/GreenMap-Frontend.git

# Clone Data
git clone https://github.com/HouHackathon-CQP/GreenMap-Data.git

# Clone Documents
git clone https://github.com/HouHackathon-CQP/GreenMap-Documents.git
```

Sau khi clone, cấu trúc thư mục sẽ là:

```
d:\GreenMap\
├── GreenMap-Backend/
├── GreenMap-Frontend/
├── GreenMap-Data/
└── GreenMap-Documents/
```

---

## GreenMap-Backend

**Repository:** `github.com/HouHackathon-CQP/GreenMap-Backend`

### Cài Đặt

```bash
cd d:\GreenMap\GreenMap-Backend

# Tạo virtual environment
python -m venv .venv

# Kích hoạt venv (Windows)
.\.venv\Scripts\activate

# Cài đặt dependencies
pip install -r requirements.txt

# Cấu hình environment
cp env.example .env

# Chỉnh sửa file .env với thông tin cấu hình của bạn
# - Database credentials
# - API keys
# - External service URLs
```

### Khởi Động Docker Services

```bash
# Các services: PostgreSQL, MongoDB, Orion-LD
docker-compose up -d

# Chờ 10-15 giây để tất cả containers khởi động
docker-compose ps
```

### Khởi Tạo Database

```bash
# Với venv đã kích hoạt
python init_db.py

# (Tùy chọn) Seed dữ liệu
python seed_sensor.py
python import_osm.py
```

### Chạy Backend

```bash
# Terminal 1: Chạy API server
python main.py
# Truy cập: http://localhost:8000
# Docs: http://localhost:8000/docs

# Terminal 2: Chạy AQI Agent (cập nhật dữ liệu realtime)
python aqi_agent.py

# Terminal 3: Chạy Weather Agent (cập nhật dữ liệu thời tiết)
python weather_agent.py
```

---

## GreenMap-Frontend

**Repository:** `github.com/HouHackathon-CQP/GreenMap-Frontend`

### Cài Đặt

```bash
cd d:\GreenMap\GreenMap-Frontend

# Cài đặt dependencies
npm install

# Chạy development server
npm run dev
```

Truy cập: `http://localhost:3000`

### Build Production

```bash
npm run build

# Preview build
npm run preview
```

---

## GreenMap-Data

**Repository:** `github.com/HouHackathon-CQP/GreenMap-Data`

### Cài Đặt

```bash
cd d:\GreenMap\GreenMap-Data

# (Tùy chọn) Cài đặt dependencies cho data processing
pip install jupyter pandas geopandas
```

### Chạy Jupyter Notebooks

```bash
# Khởi động Jupyter
jupyter notebook

# Mở browser tại: http://localhost:8888
```

### Dữ Liệu Có Sẵn

Folder này chứa:
- `bicycle_rental.geojson` - Dữ liệu trạm xe đạp
- `charging_station.geojson` - Dữ liệu trạm sạc
- `park.geojson` - Dữ liệu công viên
- `tourist_attractions.geojson` - Dữ liệu điểm du lịch
- `simulation_data_*.json` - Dữ liệu mô phỏng

---

## GreenMap-Documents

**Repository:** `github.com/HouHackathon-CQP/GreenMap-Documents`

### Cài Đặt

```bash
cd d:\GreenMap\GreenMap-Documents

# Tạo virtual environment riêng
python -m venv .venv

# Kích hoạt venv
.\.venv\Scripts\activate

# Cài đặt dependencies
pip install -r requirements.txt
```

### Xây Dựng & Xem Tài Liệu

```bash
# Build tài liệu
mkdocs build

# Chạy doc server (truy cập tại http://localhost:8000/GreenMap-Documents/)
mkdocs serve
```

---

## Các Port Sử Dụng

| Ứng Dụng | URL | Port |
|---------|-----|------|
| **Frontend** | http://localhost:3000 | 3000 |
| **Backend API** | http://localhost:8000 | 8000 |
| **Backend Docs** | http://localhost:8000/docs | 8000 |
| **PostgreSQL** | localhost | 5432 |
| **MongoDB** | localhost | 27017 |
| **Orion-LD** | http://localhost:1026 | 1026 |
| **Documentation** | http://localhost:8000 | 8000 |
| **Jupyter** | http://localhost:8888 | 8888 |

## Cài Đặt Nhanh (Một Lần)

Nếu muốn cài đặt tất cả cùng lúc:

```bash
# 1. Backend
cd d:\GreenMap\GreenMap-Backend
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
cp env.example .env
docker-compose up -d
python init_db.py

# 2. Frontend (mở terminal mới)
cd d:\GreenMap\GreenMap-Frontend
npm install
npm run dev

# 3. Documentation (mở terminal mới)
cd d:\GreenMap\GreenMap-Documents
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
mkdocs serve
```

## Xử Lý Sự Cố

### Backend không khởi động

```bash
# Kiểm tra Docker containers
docker-compose ps

# Xem logs
docker-compose logs

# Restart containers
docker-compose restart
```

### Frontend có lỗi

```bash
# Xóa node_modules và cài lại
rm -r node_modules package-lock.json
npm install
npm run dev
```

### Database connection error

```bash
# Kiểm tra PostgreSQL chạy chưa
docker-compose logs postgres

# Kiểm tra credentials trong .env file
```

### Ports đã bị chiếm dụng

```bash
# Kiểm tra process đang chạy trên port
# Windows: netstat -ano | findstr :3000
# Linux/Mac: lsof -i :3000

# Kill process hoặc thay đổi port trong config
```

## Tiếp Theo

- Xem [Hướng Dẫn Bắt Đầu Nhanh](quick-start.md)
- Đọc [Hướng Dẫn Người Dùng](../user-guide/overview.md)
- Tìm hiểu [Tài Liệu API](../api-reference/overview.md)
- Đóng góp theo [Hướng Dẫn Đóng Góp](../contributing/guidelines.md)

---

**Selamat datang ke GreenMap! 🚀🌍**

### Phương Pháp 2: Cài Đặt Thủ Công

Để kiểm soát quá trình cài đặt hơn:

#### Bước 1: Clone Repository

```bash
git clone https://github.com/HouHackathon-CQP/GreenMap.git
cd GreenMap
```

#### Bước 2: Cài Đặt Dependencies Backend

```bash
cd GreenMap-Backend
python -m venv .venv

# Windows
.\.venv\Scripts\activate

# macOS/Linux
source .venv/bin/activate

pip install -r requirements.txt
```

#### Bước 3: Cài Đặt Dependencies Frontend

```bash
cd ../GreenMap-Frontend
npm install
```

#### Bước 4: Cấu Hình Biến Môi Trường

Tạo file `.env` trong thư mục GreenMap-Backend:

```bash
cp env.example .env
```

Chỉnh sửa file `.env` với cấu hình của bạn:

```env
# Database Configuration
DATABASE_URL="postgresql+asyncpg://admin:mysecretpassword@127.0.0.1:5432/greenmap_db"
SECRET_KEY="your_secret_key_here_64_chars"
ALGORITHM="HS256"
ACCESS_TOKEN_EXPIRE_MINUTES=30

# CORS
CORS_ORIGINS="http://localhost:3000"

# Admin
FIRST_SUPERUSER="admin@greenmap.hanoi"
FIRST_SUPERUSER_PASSWORD="123456"

# External APIs
ORION_BROKER_URL="http://localhost:1026"
```

#### Bước 5: Khởi Tạo Cơ Sở Dữ Liệu

```bash
cd GreenMap-Backend
python init_db.py
```

#### Bước 6: Khởi Động Ứng Dụng

```bash
# Terminal 1: API Backend
cd GreenMap-Backend
python main.py

# Terminal 2: AQI Agent
python aqi_agent.py

# Terminal 3: Weather Agent
python weather_agent.py

# Terminal 4: Frontend (trong thư mục GreenMap-Frontend)
npm run dev
```

## Cài Đặt với Docker

Để triển khai được containerize:

```bash
# Clone repository
git clone https://github.com/HouHackathon-CQP/GreenMap.git
cd GreenMap

# Xây dựng và chạy với Docker Compose
docker-compose up --build -d
```

## Xác Minh Cài Đặt

Sau khi cài đặt, xác minh rằng GreenMap đang chạy:

1. Mở trình duyệt và điều hướng đến `http://localhost:3000`
2. Bạn sẽ thấy trang chủ GreenMap
3. Cố gắng đăng nhập bằng tài khoản admin để đảm bảo backend hoạt động

```
Tài khoản mặc định:
Email: admin@greenmap.hanoi
Mật khẩu: 123456
```

## Xử Lý Sự Cố

### Các Vấn Đề Thường Gặp

#### Cổng Đã Được Sử Dụng

Nếu cổng 3000 hoặc 8000 đã được sử dụng:

```bash
# Tìm và kết thúc process
# Windows
netstat -ano | findstr :3000
taskkill /PID <PID> /F

# Linux/macOS
lsof -i :3000
kill -9 <PID>
```

#### Lỗi Kết Nối Cơ Sở Dữ Liệu

Đảm bảo cơ sở dữ liệu đang chạy và chuỗi kết nối chính xác:

```bash
# Kiểm tra trạng thái PostgreSQL
systemctl status postgresql

# Hoặc với Docker
docker ps | grep postgres
```

#### Thiếu Dependencies

Nếu gặp lỗi dependency:

```bash
# Xóa cache npm và cài đặt lại
npm cache clean --force
rm -rf node_modules
npm install

# Python
pip install --upgrade pip
pip install -r requirements.txt
```

## Yêu Cầu Hệ Thống

### Yêu Cầu Tối Thiểu

- **CPU**: Bộ xử lý lõi kép
- **RAM**: 4 GB
- **Lưu Trữ**: 10 GB không gian trống
- **OS**: Windows 10, macOS 10.14+, hoặc Linux

### Yêu Cầu Được Khuyến Nghị

- **CPU**: Bộ xử lý lõi tứ
- **RAM**: 8 GB trở lên
- **Lưu Trữ**: 20 GB không gian trống
- **OS**: Phiên bản mới nhất của Windows, macOS, hoặc Linux

## Bước Tiếp Theo

Bây giờ bạn đã cài đặt GreenMap:

- Theo dõi [Hướng Dẫn Bắt Đầu Nhanh](quick-start.md) để học cơ bản
- Khám phá [Hướng Dẫn Người Dùng](../user-guide/overview.md) để biết thêm tính năng
- Kiểm tra [Tài Liệu API](../api-reference/overview.md) nếu bạn là nhà phát triển

## Lấy Trợ Giúp

Nếu gặp sự cố trong quá trình cài đặt:

- Kiểm tra [Câu Hỏi Thường Gặp](../user-guide/features.md)
- Truy cập trang [Issues](https://github.com/HouHackathon-CQP/GreenMap/issues) của GitHub
- Tham gia máy chủ Discord cộng đồng của chúng tôi

---

*Sẵn sàng tạo ra sự khác biệt? Hãy bắt đầu nào!*
