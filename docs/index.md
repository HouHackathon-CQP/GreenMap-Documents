# GreenMap - Bản Đồ Xanh Hà Nội

Chào mừng đến với tài liệu chính thức của **GreenMap** - Nền tảng giám sát chất lượng không khí và quản lý dữ liệu đô thị thông minh tại Hà Nội.

## GreenMap là gì?

GreenMap là một dự án open-source được phát triển với mục đích:

- **Giám sát chất lượng không khí**: Theo dõi chỉ số AQI (Air Quality Index) theo thời gian thực
- **Phân tích dữ liệu thời tiết**: Cập nhật thông tin thời tiết chính xác
- **Quản lý dữ liệu đô thị**: Tích hợp Linked Open Data (LOD) và IoT sensor
- **Giao diện bản đồ tương tác**: Hiển thị dữ liệu trên bản đồ thực tế

## Các Tính Năng Chính

- 📍 **Bản đồ Tương Tác**: Visualize các điểm AQI, thời tiết, và dữ liệu đô thị trên bản đồ
- 📊 **Theo Dõi Realtime**: Cập nhật dữ liệu sensor theo thời gian thực
- 🔗 **NGSI-LD Compliant**: Tuân thủ tiêu chuẩn Linked Data cho IoT
- 👥 **Quản Lý Báo Cáo**: Hệ thống báo cáo sự cố môi trường
- 🔐 **Xác Thực Người Dùng**: JWT-based authentication và authorization
- 📱 **Responsive Design**: Hỗ trợ desktop, tablet, mobile

## Kiến Trúc Hệ Thống

```
┌─────────────────────────────────────────────────────────────┐
│                    GreenMap Frontend (React)                │
│                  Vite + Tailwind + MapLibre                 │
└──────────────────────────┬──────────────────────────────────┘
                           │
                    ┌──────┴──────┐
                    │             │
        ┌───────────▼──┐  ┌───────▼────────────┐
        │  FastAPI     │  │  Orion-LD Context  │
        │  Backend     │  │  Broker            │
        │  PostgreSQL  │  │  MongoDB           │
        └──────────────┘  └────────────────────┘
        
        Agents: AQI, Weather Realtime Update
```

## Liên Kết Nhanh

<div class="grid cards" markdown>

-   :material-rocket:{ .lg .middle } __Bắt Đầu Nhanh__

    ---

    Thiết lập và chạy dự án trong vài phút

    [:octicons-arrow-right-24: Quick Start](getting-started/quick-start.md)

-   :material-book-open-page-variant:{ .lg .middle } __Hướng Dẫn Người Dùng__

    ---

    Tìm hiểu tất cả các tính năng

    [:octicons-arrow-right-24: Hướng Dẫn](user-guide/overview.md)

-   :material-api:{ .lg .middle } __Tài Liệu API__

    ---

    Chi tiết API cho developers

    [:octicons-arrow-right-24: API Reference](api-reference/overview.md)

-   :material-heart:{ .lg .middle } __Đóng Góp__

    ---

    Giúp chúng tôi phát triển GreenMap

    [:octicons-arrow-right-24: Contributing](contributing/guidelines.md)

</div>

## Công Nghệ Sử Dụng

### Backend
- **FastAPI**: Framework hiệu năng cao
- **PostgreSQL + GIS**: Hỗ trợ dữ liệu địa lý
- **MongoDB**: Lưu trữ dữ liệu NGSI-LD
- **Orion-LD**: Context Broker
- **SQLAlchemy**: ORM

### Frontend
- **React 19**: UI Framework
- **Vite**: Build tool hiệu quả
- **MapLibre GL JS**: Thư viện bản đồ
- **Tailwind CSS**: Styling
- **Recharts**: Biểu đồ dữ liệu

## Hỗ Trợ & Câu Hỏi

Nếu bạn cần giúp đỡ:

- 📖 [Hướng Dẫn Người Dùng](user-guide/overview.md)
- 🔌 [Tài Liệu API](api-reference/overview.md)
- 🤝 [Hướng Dẫn Đóng Góp](contributing/guidelines.md)
- 📞 Liên hệ: [GitHub Issues](https://github.com/HouHackathon-CQP/GreenMap)

## Về Dự Án

GreenMap được phát triển bởi đội **HouHackathon-CQP** trong HouHackathon. Xem thêm tại [Về GreenMap](about.md)

---

**Let's make our cities greener! 🌍🌱**
