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

# Về GreenMap

GreenMap là hệ sinh thái quản lý dữ liệu môi trường đô thị thông minh, được phát triển cho cuộc thi **HouHackathon 2024**. Chúng tôi giải quyết vấn đề dữ liệu môi trường phân tán bằng một nền tầng tập trung duy nhất.

---

## Tầm Nhìn & Sứ Mệnh

<div class="mission-vision">

### Tầm Nhìn

Trở thành nền tảng giám sát môi trường đô thị hàng đầu tại Việt Nam, giúp các thành phố xây dựng hệ sinh thái xanh, bền vững thông qua dữ liệu minh bạch và công nghệ tiên tiến.

### Sứ Mệnh

**Trao quyền cho cộng đồng** thực hiện hành động vì môi trường thông qua:

- **Minh bạch dữ liệu** - Mọi người đều có quyền tiếp cận thông tin môi trường realtime
- **Công nghệ mở** - Open source, APIs công khai, chuẩn FIWARE NGSI-LD
- **Tham gia cộng đồng** - Người dân có thể báo cáo vấn đề môi trường qua Mobile App
- **Ra quyết định dựa trên dữ liệu** - Cung cấp insights cho quản lý đô thị

</div>

---

## Vấn Đề Chúng Tôi Giải Quyết

### Hiện Trạng

<div class="problem-list">

**Dữ liệu môi trường phân tán:**
- Thông tin AQI từ nhiều nguồn khác nhau
- Không có nền tảng tập trung
- Người dân khó tiếp cận dữ liệu chính xác

**Thiếu sự tham gia của cộng đồng:**
- Không có kênh báo cáo vấn đề môi trường hiệu quả
- Phản ánh của người dân không được xử lý kịp thời
- Thiếu minh bạch trong quy trình giải quyết

**Quản lý hạ tầng xanh không hiệu quả:**
- Dữ liệu công viên, trạm sạc, xe đạp không được số hóa
- Khó theo dõi trạng thái và bảo trì
- Không tận dụng được dữ liệu để tối ưu

</div>

### Giải Pháp GreenMap

<div class="solution-grid">

**Nền tảng tập trung**
Tích hợp dữ liệu từ OpenAQ, OpenWeatherMap, OpenStreetMap và SUMO simulation vào một hệ thống duy nhất.

**Mobile App cho người dân**
Ứng dụng Android cho phép báo cáo vấn đề môi trường với hình ảnh, vị trí GPS và theo dõi tiến độ xử lý.

**Web Portal cho quản trị viên**
Giao diện quản lý với bản đồ tương tác, dashboard realtime và công cụ xử lý báo cáo.

**APIs mở & chuẩn NGSI-LD**
REST APIs công khai và tích hợp Orion-LD Context Broker theo chuẩn FIWARE, cho phép mở rộng và tích hợp dễ dàng.

</div>

---

## Công Nghệ & Kiến Trúc

### Tech Stack

<div class="tech-overview">

**Backend:**
- FastAPI (Python) - REST API server
- PostgreSQL + PostGIS - Spatial database
- Orion-LD Context Broker - NGSI-LD standard
- APScheduler - Background workers

**Frontend:**
- React 19 + Vite 7.2 - Modern UI
- MapLibre GL JS - Interactive maps
- Tailwind CSS - Styling
- TanStack Query - Data fetching

**Mobile:**
- Kotlin + Jetpack Compose - Android native
- MVI Architecture - Unidirectional data flow
- Ktor Client - HTTP requests
- Coil - Image loading

**Data:**
- OpenStreetMap Overpass API
- OpenAQ API - Air quality
- OpenWeatherMap API
- SUMO Traffic Simulation

**Infrastructure:**
- Docker & Docker Compose
- GitHub Actions - CI/CD
- Nginx - Reverse proxy

</div>

---

## Team

GreenMap được phát triển bởi đội ngũ **Chúng Quản Phú** tại HouHackathon 2024.

<div class="team-about">

**Nguyễn Bá Phú** - *Team Lead & Backend Developer*  
Backend architecture & API development, Database design & optimization, NGSI-LD Context Broker integration  
GitHub: [@nguyenbaphu](https://github.com/nguyenbaphu)

**Vũ Tiến Quân** - *Frontend Developer*  
React web portal development, MapLibre GL JS integration, UI/UX design & implementation  
GitHub: [@tienbienquang1422](https://github.com/tienbienquang1422)

**Hoàng Mạnh Cường** - *Mobile Developer & Data Engineer*  
Android app development (Kotlin + Compose), Data pipeline & ETL scripts, SUMO traffic simulation integration  
GitHub: [@manhhcuong1503](https://github.com/manhhcuong1503)

</div>

---

## Tính Năng Nổi Bật

<div class="features-list">

**Giám sát Môi trường Realtime**  
AQI tracking từ OpenAQ, Weather data updates mỗi 30 phút, Dashboard với biểu đồ xu hướng, Cảnh báo khi AQI vượt ngưỡng nguy hiểm

**Bản Đồ Tương Tác**  
MapLibre GL JS với multiple layers, Hiển thị công viên, trạm sạc, điểm cho thuê xe đạp, Heatmap mật độ báo cáo, Search địa điểm với geocoder

**Báo Cáo Từ Cộng Đồng**  
Mobile app cho người dân, Upload hình ảnh + GPS location, Theo dõi trạng thái xử lý, Push notifications khi có cập nhật

**NGSI-LD Standard**  
Tích hợp Orion-LD Context Broker, Tuân thủ chuẩn FIWARE, IoT-ready architecture, Scalable & extensible

**AI-Powered Insights**  
Gemini AI phân tích xu hướng ô nhiễm, Đề xuất giải pháp giảm AQI, Tóm tắt báo cáo tự động, Dự đoán chất lượng không khí

**Open Source & APIs**  
Public REST APIs, Comprehensive documentation, Docker deployment, GitHub repositories

</div>

---

## Roadmap

### Đã Hoàn Thành (v1.0)

- Backend API với FastAPI + PostgreSQL + PostGIS
- Web Portal với React + MapLibre
- Mobile App Android với Kotlin + Compose
- Data Pipeline từ OpenAQ, Weather, OSM
- NGSI-LD Context Broker integration
- Background workers cho AQI & Weather
- JWT authentication & authorization
- CRUD operations cho Parks, Charging Stations, Bicycle Rentals
- Report management system
- Interactive maps với multiple layers

### Kế Hoạch Tương Lai

**v1.1 (Q1 2025)**
- iOS App (Swift + SwiftUI)
- Push notifications cho mobile
- Export reports to PDF
- Admin dashboard analytics

**v1.2 (Q2 2025)**
- Machine Learning models cho AQI prediction
- Real IoT sensors integration
- Webhooks API
- Multi-language support (English, Vietnamese)

**v2.0 (Q3 2025)**
- Microservices architecture
- Kubernetes deployment
- Real-time collaboration features
- GraphQL API
- Advanced analytics & reporting

---

## Open Source

GreenMap là dự án **open source**, được phát triển công khai trên GitHub:

**Repositories:**
- [GreenMap-Backend](https://github.com/HouHackathon-CQP/GreenMap-Backend) - FastAPI backend
- [GreenMap-Frontend](https://github.com/HouHackathon-CQP/GreenMap-Frontend) - React web portal
- [GreenMap-Mobile-App](https://github.com/HouHackathon-CQP/GreenMap-Mobile-App) - Android app
- [GreenMap-Data](https://github.com/HouHackathon-CQP/GreenMap-Data) - Data pipeline

**License:** MIT License

**Contributing:** Chúng tôi hoan nghênh mọi đóng góp! Xem [Contributing Guidelines](contributing/) để biết thêm chi tiết.

---

## Liên Hệ

**Email:** contact@greenmap.vn  
**GitHub Organization:** [@HouHackathon-CQP](https://github.com/HouHackathon-CQP)  
**Documentation:** https://docs.greenmap.vn  

**HouHackathon 2024** - Team: Chúng Quản Phú

---

## Acknowledgments

Cảm ơn các công nghệ và dịch vụ mã nguồn mở:

- OpenAQ for air quality data
- OpenWeatherMap for weather data
- OpenStreetMap for geographic data
- FIWARE Foundation for NGSI-LD standard
- MapLibre for mapping library
- FastAPI, React, Kotlin communities
