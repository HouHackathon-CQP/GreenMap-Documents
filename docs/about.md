# Về GreenMap

## GreenMap Là Gì?

**GreenMap** là một hệ thống quản lý dữ liệu môi trường tích hợp, được phát triển cho **HouHackathon 2024**.

Dự án này gồm 4 repositories độc lập:

1. **GreenMap-Backend** - REST API và xử lý dữ liệu realtime
2. **GreenMap-Frontend** - Ứng dụng web React với bản đồ tương tác
3. **GreenMap-Data** - Jupyter notebooks để phân tích dữ liệu
4. **GreenMap-Documents** - Tài liệu toàn diện (tài liệu này)

## Lịch Sử Phát Triển

### Khởi Nguồn

GreenMap được phát triển trong HouHackathon, khi một nhóm các lập trình viên quyết định giải quyết vấn đề giám sát chất lượng không khí và quản lý dữ liệu môi trường ở Hà Nội.

### Vấn Đề Chúng Tôi Giải Quyết

Trước GreenMap:
- Dữ liệu AQI phân tán trên nhiều nền tảng
- Khó khăn trong việc khám phá các dự án xanh địa phương
- Không có cách tập trung để theo dõi tác động môi trường
- Thiếu công cụ quản lý dữ liệu đô thị
- Hạn chế tính năng báo cáo sự cố môi trường từ cộng đồng

### Giải Pháp của Chúng Tôi

GreenMap cung cấp:
- **Nền tảng Tập Trung**: Một nơi để theo dõi tất cả chỉ số AQI, thời tiết, và dữ liệu đô thị
- **Bản Đồ Tương Tác**: Hiển thị trực quan dữ liệu bằng bản đồ thực tế (Leaflet)
- **Theo Dõi Realtime**: Cập nhật dữ liệu sensor liên tục từ external APIs
- **Quản Lý Báo Cáo**: Hệ thống báo cáo sự cố môi trường từ cộng đồng
- **API REST**: Cho phép tích hợp với các ứng dụng khác
- **Dữ Liệu Mở**: Sử dụng GeoJSON format để khả năng tương tác

## Sứ Mệnh

Trao quyền cho các cá nhân và cộng đồng thực hiện hành động có ý nghĩa cho môi trường bằng cách cung cấp các công cụ dễ tiếp cận, hữu ích và hiệu quả để:
- Giám sát chất lượng không khí
- Quản lý dữ liệu đô thị
- Báo cáo sự cố môi trường
- Tương tác với cộng đồng

## Tầm Nhìn

Chúng tôi mong muốn một thế giới nơi:
- Mỗi người có thể dễ dàng theo dõi chất lượng không khí xung quanh mình
- Các cộng đồng được kết nối thông qua dữ liệu môi trường chung
- Tác động môi trường là minh bạch và có thể đo lường được
- Công nghệ phục vụ như một cầu nối giữa ý định và hành động thực tế
- Dữ liệu mở được sử dụng để cải thiện chất lượng sống

## Giá Trị Cốt Lõi

### 🌍 Bền Vững Trên Hết
Bảo vệ môi trường là trái tim của mọi thứ chúng tôi làm. Chúng tôi đảm bảo rằng nền tảng của chúng tôi thúc đẩy tác động môi trường thực tế.

### 👥 Cộng Đồng Trước Tiên
Xây dựng cộng đồng mạnh mẽ, kết nối những người quan tâm đến môi trường.

### 🔓 Minh Bạch Hoàn Toàn
Dữ liệu mở, code mở source, quy trình mở. Bất cứ ai cũng có thể thấy những gì chúng tôi đang làm.

### ♿ Dễ Tiếp Cận
Công cụ của chúng tôi được thiết kế cho mọi người - không cần kỹ năng kỹ thuật cao.

### 🚀 Đổi Mới Liên Tục
Luôn tìm kiếm những cách mới để cải thiện và mở rộng chức năng.

## Các Repositories

### GreenMap-Backend
**Repository:** github.com/HouHackathon-CQP/GreenMap-Backend

**Chủ Động:**
- Cung cấp REST API endpoints
- Quản lý database (PostgreSQL, MongoDB)
- Xử lý xác thực người dùng (OAuth2, JWT)
- Chạy agents realtime (AQI, Weather)
- Tích hợp với Orion-LD Context Broker
- Nhập dữ liệu từ OpenStreetMap

**Stack:** Python 3.10+, FastAPI, SQLAlchemy, PostgreSQL, MongoDB, Orion-LD

### GreenMap-Frontend
**Repository:** github.com/HouHackathon-CQP/GreenMap-Frontend

**Chủ Động:**
- Cung cấp giao diện web
- Hiển thị bản đồ tương tác (Leaflet)
- Quản lý tài khoản người dùng
- Tạo và quản lý báo cáo
- Lọc và tìm kiếm dữ liệu
- Chế độ tối/sáng

**Stack:** React 18+, Vite, Tailwind CSS, Leaflet

### GreenMap-Data
**Repository:** github.com/HouHackathon-CQP/GreenMap-Data

**Chủ Động:**
- Cung cấp Jupyter notebooks
- Phân tích dữ liệu AQI
- Xử lý GeoJSON files
- Tạo dữ liệu mô phỏng
- EDA (Exploratory Data Analysis)
- Dự báo và mô phỏng

**Stack:** Python, Jupyter, Pandas, GeoPandas, Shapely

### GreenMap-Documents
**Repository:** github.com/HouHackathon-CQP/GreenMap-Documents

**Chủ Động:**
- Cung cấp tài liệu toàn diện
- Hướng dẫn cài đặt
- Hướng dẫn người dùng
- Tài liệu API
- Hướng dẫn đóng góp

**Stack:** MkDocs, Material Theme

## Kiến Trúc Tổng Thể

```
┌─────────────────────────────────────────────────────────────┐
│                      Người Dùng                              │
│                (Web Browser - GreenMap-Frontend)             │
└──────────────────────────┬──────────────────────────────────┘
                           │ HTTP Request
                           ↓
┌──────────────────────────────────────────────────────────────┐
│               GreenMap-Backend API                           │
│                (Python/FastAPI)                              │
│  ┌──────────────────────────────────────────────────────┐    │
│  │ - Auth (OAuth2, JWT)                               │    │
│  │ - Locations, Sensors, Reports endpoints            │    │
│  │ - AQI Agent (updates realtime)                      │    │
│  │ - Weather Agent (updates realtime)                  │    │
│  │ - Context Broker Integration (Orion-LD)            │    │
│  │ - OSM Data Import                                   │    │
│  └──────────────────────────────────────────────────────┘    │
└──────┬───────────────────┬──────────────────────────┬────────┘
       │                   │                          │
       ↓                   ↓                          ↓
   PostgreSQL           MongoDB                  Orion-LD
   (Relational)       (Documents)            (Context Broker)
   (Users, Reports)   (Sensor Data)          (NGSI-LD Data)
                                                      ↑
                                                      │
                    ┌─────────────────────────────────┘
                    │
                    ↓
       ┌────────────────────────────┐
       │  GreenMap-Data              │
       │  (Jupyter/Pandas/GeoPandas) │
       │  - Data Analysis            │
       │  - GeoJSON Processing       │
       │  - Simulation Data          │
       │  - EDA Notebooks            │
       └────────────────────────────┘
                    │
                    ↑
       ┌────────────────────────────┐
       │  Data Sources               │
       │  - Sensors                  │
       │  - OpenStreetMap            │
       │  - Weather APIs             │
       │  - CSV/GeoJSON Files        │
       └────────────────────────────┘
```

## Công Nghệ Stack

| Lớp | Công Nghệ |
|-----|-----------|
| **Frontend** | React, TypeScript, Tailwind CSS, Vite, Leaflet |
| **Backend** | Python, FastAPI, SQLAlchemy, Pydantic |
| **Database** | PostgreSQL, MongoDB |
| **Context Broker** | Orion-LD (NGSI-LD) |
| **Data Processing** | Jupyter, Pandas, GeoPandas |
| **DevOps** | Docker, Docker Compose |
| **Documentation** | MkDocs, Material Theme |

## Team & Credits

**Phát triển bởi:** HouHackathon-CQP participants

**Giấy Phép:** MIT License

## Liên Hệ & Liên Kết

- **GitHub:** github.com/HouHackathon-CQP
- **Issues:** Report bugs trên GitHub
- **Discussions:** Thảo luận trên GitHub
- **Documentation:** Xem tài liệu tại đây

---

**Cảm ơn bạn đã quan tâm đến GreenMap! 🌍💚**

Để bắt đầu, xem [Hướng Dẫn Cài Đặt](getting-started/installation.md).
