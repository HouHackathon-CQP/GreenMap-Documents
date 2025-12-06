# Giới Thiệu GreenMap

## GreenMap Là Gì?

**GreenMap** là một hệ thống thông minh để cảnh báo chất lượng không khí và môi trường dựa trên vị trí, được phát triển cho HouHackathon 2024.

GreenMap gồm 4 repository độc lập nhưng kết nối với nhau:

1. **GreenMap-Backend** - REST API và xử lý dữ liệu
2. **GreenMap-Frontend** - Ứng dụng web React
3. **GreenMap-Data** - Jupyter notebooks và xử lý dữ liệu
4. **GreenMap-Documents** - Tài liệu và hướng dẫn

## Cách GreenMap Hoạt Động

```
┌─────────────────────────────────────────────────────────┐
│                   GreenMap System                       │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌──────────────────────────────────────────────────┐  │
│  │         GreenMap-Frontend (React)                │  │
│  │  - Bản đồ tương tác                             │  │
│  │  - Thông tin chất lượng không khí               │  │
│  │  - Thống kê và dự báo                           │  │
│  └────────────────┬─────────────────────────────────┘  │
│                   │ (HTTP Requests)                    │
│  ┌────────────────▼─────────────────────────────────┐  │
│  │      GreenMap-Backend (Python/FastAPI)           │  │
│  │  - REST API endpoints                           │  │
│  │  - Xử lý dữ liệu realtime                       │  │
│  │  - AQI & Weather agents                         │  │
│  │  - OAuth2 authentication                        │  │
│  └────────────────┬─────────────────────────────────┘  │
│                   │                                    │
│  ┌────────────────┴─────────────────────────────────┐  │
│  │  GreenMap-Data (Jupyter/Pandas/GeoPandas)       │  │
│  │  - Xử lý GeoJSON data                           │  │
│  │  - Phân tích dữ liệu không khí                  │  │
│  │  - Mô phỏng và dự báo                           │  │
│  └────────────────┬─────────────────────────────────┘  │
│                   │ (PostgreSQL, MongoDB, Orion-LD)    │
│  ┌────────────────▼─────────────────────────────────┐  │
│  │         Databases & Services                     │  │
│  │  - PostgreSQL (relational data)                 │  │
│  │  - MongoDB (document store)                     │  │
│  │  - Orion-LD (NGSI-LD API context broker)        │  │
│  └─────────────────────────────────────────────────┘  │
│                                                         │
│  ┌─────────────────────────────────────────────────┐  │
│  │      GreenMap-Documents (MkDocs)                │  │
│  │  - Tài liệu này                                │  │
│  │  - Hướng dẫn installation & usage               │  │
│  │  - API reference                               │  │
│  └─────────────────────────────────────────────────┘  │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

## Tính Năng Chính

### 📊 Giám Sát Chất Lượng Không Khí
- Cập nhật dữ liệu AQI realtime từ các sensors
- Dữ liệu thời tiết tích hợp
- Cảnh báo tự động khi AQI vượt ngưỡng

### 🗺️ Bản Đồ Tương Tác
- Hiển thị vị trí sensors trên bản đồ
- Thông tin chi tiết từng điểm (tooltip)
- Tìm kiếm vị trí gần đó
- Chế độ tối/sáng

### 📍 Các Loại Dữ Liệu
- **Trạm xe đạp** - Vị trí bicycle rental
- **Trạm sạc** - Charging stations cho phương tiện điện
- **Công viên** - Green areas và indoor space
- **Điểm du lịch** - Tourist attractions
- **Sensors** - Cảm biến chất lượng không khí

### 👥 Quản Lý Người Dùng
- Đăng ký / Đăng nhập
- Quản lý profile
- Theo dõi lịch sử báo cáo
- Các báo cáo từ cộng đồng

### 🔐 Bảo Mật
- OAuth2 authentication
- JWT tokens
- Role-based access control

## Các Thành Phần Chính

### 1. GreenMap-Backend
Xử lý tất cả logic business:
- API REST endpoints
- Database queries
- Data aggregation
- Realtime agents (AQI, Weather)
- OpenStreetMap integration

**Stack:** Python, FastAPI, PostgreSQL, MongoDB, Orion-LD

**Repository:** github.com/HouHackathon-CQP/GreenMap-Backend

### 2. GreenMap-Frontend
Giao diện người dùng web:
- Bản đồ tương tác (Leaflet)
- Dashboard thống kê
- Quản lý hồ sơ người dùng
- Báo cáo realtime

**Stack:** React, Tailwind CSS, Vite, Leaflet

**Repository:** github.com/HouHackathon-CQP/GreenMap-Frontend

### 3. GreenMap-Data
Xử lý và phân tích dữ liệu:
- Jupyter notebooks để EDA
- GeoJSON data processing
- Dữ liệu mô phỏng
- Phân tích không khí chuyên sâu

**Stack:** Python, Jupyter, Pandas, GeoPandas

**Repository:** github.com/HouHackathon-CQP/GreenMap-Data

### 4. GreenMap-Documents
Tài liệu hoàn chỉnh:
- Installation guide
- User guide
- API reference
- Contributing guidelines

**Stack:** MkDocs, Material Theme

**Repository:** github.com/HouHackathon-CQP/GreenMap-Documents

## Kiến Trúc Dữ Liệu

### Data Flow
```
Sensors & OpenStreetMap
        ↓
   GreenMap-Backend
        ↓
  PostgreSQL / MongoDB / Orion-LD
        ↓
   GreenMap-Frontend
        ↓
    Users
```

### GeoJSON Format
Dữ liệu địa lý sử dụng GeoJSON standard:
```json
{
  "type": "Feature",
  "geometry": {
    "type": "Point",
    "coordinates": [106.6296, 10.7769]
  },
  "properties": {
    "name": "Sensor A",
    "aqi": 45,
    "location": "District 1"
  }
}
```

## Công Nghệ Sử Dụng

| Phần | Công Nghệ |
|-----|-----------|
| **Backend** | Python 3.10+, FastAPI, SQLAlchemy |
| **Frontend** | React 18+, Tailwind CSS, Leaflet |
| **Database** | PostgreSQL, MongoDB, Orion-LD |
| **Data** | Jupyter, Pandas, GeoPandas, Shapely |
| **DevOps** | Docker, Docker Compose |
| **Docs** | MkDocs, Material Theme |

## Bắt Đầu

### Cài Đặt Nhanh (5 phút)
Xem [Hướng Dẫn Cài Đặt](installation.md) để thiết lập tất cả components.

### Chạy Lần Đầu
Xem [Hướng Dẫn Bắt Đầu Nhanh](quick-start.md) để run toàn bộ hệ thống.

### Tài Liệu Thêm
- [Hướng Dẫn Người Dùng](../user-guide/overview.md) - Cách sử dụng GreenMap
- [Tài Liệu API](../api-reference/overview.md) - API endpoints
- [Đóng Góp](../contributing/guidelines.md) - Cách contribute

## Liên Hệ & Hỗ Trợ

- **Docs:** Xem tài liệu tại đây
- **Issues:** Báo cáo bugs trên GitHub
- **Discussions:** Thảo luận trên GitHub
- **Email:** [Your Email]

## Giấy Phép

GreenMap được phân phối dưới giấy phép MIT.

---

**Sẵn sàng bắt đầu? 🚀**
Hãy truy cập [Hướng Dẫn Cài Đặt](installation.md) ngay!
