# Hướng Dẫn Người Dùng - Tổng Quan

Chào mừng đến hướng dẫn người dùng GreenMap! Hướng dẫn này giúp bạn sử dụng GreenMap web application hiệu quả.

## GreenMap-Frontend Là Gì?

**GreenMap-Frontend** là ứng dụng web React cho phép người dùng:
- Xem chất lượng không khí trên bản đồ tương tác
- Tìm kiếm và khám phá các địa điểm
- Báo cáo vấn đề môi trường
- Quản lý hồ sơ cá nhân
- Tương tác với cộng đồng

## Các Tính Năng Chính

### 🗺️ Bản Đồ Tương Tác
- Hiển thị realtime các sensors, trạm xe đạp, trạm sạc, công viên, điểm du lịch
- Phóng to/thu nhỏ để khám phá từng khu vực
- Nhấp vào các điểm để xem thông tin chi tiết
- Lọc dữ liệu theo loại

### 📊 Dữ Liệu AQI Realtime
- Chỉ số AQI từ các sensors
- Dữ liệu thời tiết cục bộ (nhiệt độ, độ ẩm, gió)
- Cảnh báo tự động khi AQI xấu
- Dữ liệu lịch sử và xu hướng

### 👤 Quản Lý Tài Khoản
- Đăng ký / Đăng nhập
- Cập nhật profile
- Quản lý mật khẩu
- Theo dõi lịch sử báo cáo

### 🔔 Báo Cáo Sự Cố
- Tạo báo cáo về vấn đề môi trường
- Kèm theo vị trí và hình ảnh
- Theo dõi trạng thái báo cáo
- Nhận phản hồi từ cộng đồng

### 🌙 Chế Độ Tối/Sáng
- Tùy chỉnh giao diện theo sở thích
- Bảo vệ mắt trong điều kiện ánh sáng khác nhau

## Các Loại Dữ Liệu Trên Bản Đồ

### 🟢 Sensors (Chất Lượng Không Khí)
- Hiển thị AQI realtime
- Cập nhật từ các external APIs
- Cung cấp thông tin thời tiết

### 🚲 Trạm Xe Đạp (Bicycle Rental)
- Vị trí các trạm cho thuê xe đạp
- Từ GreenMap-Data GeoJSON files

### 🔌 Trạm Sạc (Charging Stations)
- Vị trí trạm sạc xe điện
- Để hỗ trợ giao thông xanh

### 🌳 Công Viên (Parks)
- Vị trí các công viên và không gian xanh
- Từ OpenStreetMap data

### 🏛️ Điểm Du Lịch (Tourist Attractions)
- Các địa điểm du lịch nổi tiếng
- Thông tin du lịch bổ sung

## Công Nghệ Sử Dụng

| Thành Phần | Công Nghệ |
|-----------|-----------|
| **Framework** | React 18+ |
| **Styling** | Tailwind CSS |
| **Build Tool** | Vite |
| **Bản Đồ** | Leaflet |
| **State Management** | React Hooks |
| **API Client** | Fetch API |
| **Runtime** | Node.js 18+ |

## Kiến Trúc

```
┌─────────────────────────────────────────┐
│   GreenMap-Frontend (React)             │
├─────────────────────────────────────────┤
│                                         │
│  ┌─────────────────────────────────┐   │
│  │  src/                           │   │
│  │  ├── pages/                     │   │
│  │  │   ├── Login                  │   │
│  │  │   ├── Home (Map)             │   │
│  │  │   ├── Reports                │   │
│  │  │   └── Profile                │   │
│  │  ├── components/                │   │
│  │  │   ├── MapComponent           │   │
│  │  │   ├── Sidebar                │   │
│  │  │   ├── InfoPanel              │   │
│  │  │   └── Navigation             │   │
│  │  ├── services/                  │   │
│  │  │   └── apiService.js          │   │
│  │  ├── utils/                     │   │
│  │  └── App.jsx                    │   │
│  └─────────────────────────────────┘   │
│            ↓ (HTTP)                     │
│  ┌─────────────────────────────────┐   │
│  │  GreenMap-Backend API           │   │
│  │  (http://localhost:8000)        │   │
│  └─────────────────────────────────┘   │
│                                         │
└─────────────────────────────────────────┘
```

## Điều Kiện Trước Khi Bắt Đầu

Đảm bảo:
- Backend API đang chạy tại `http://localhost:8000`
- Frontend đang chạy tại `http://localhost:3000`
- Bạn có kết nối internet để tải bản đồ
- Browser hỗ trợ JavaScript

## Cấu Trúc Hướng Dẫn

Hướng dẫn người dùng gồm các phần:

1. **[Features](features.md)** - Chi tiết về các tính năng
2. **[Map Usage](map-guide.md)** - Cách sử dụng bản đồ
3. **[Accounts](accounts.md)** - Quản lý tài khoản
4. **[Reports](reports.md)** - Tạo và quản lý báo cáo
5. **[Settings](settings.md)** - Tùy chỉnh ứng dụng

## Bước Tiếp Theo

- Xem [Các Tính Năng](features.md) để chi tiết hơn
- Đọc [Hướng Dẫn Bản Đồ](map-guide.md) để sử dụng bản đồ
- Khám phá [API Documentation](../api-reference/overview.md) nếu bạn là developer

---

**Sẵn sàng khám phá GreenMap? Hãy bắt đầu! 🚀**
