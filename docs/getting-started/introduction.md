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

# Giới Thiệu GreenMap

## GreenMap là gì?

**GreenMap** (Bản Đồ Xanh Hà Nội) là một hệ sinh thái phần mềm mã nguồn mở được phát triển nhằm giám sát và quản lý môi trường đô thị thông minh. Dự án được xây dựng với mục tiêu tạo ra một nền tảng tích hợp, nơi dữ liệu từ nhiều nguồn khác nhau được kết nối và trực quan hóa để hỗ trợ việc ra quyết định.

## Tại sao cần GreenMap?

Hà Nội đang đối mặt với nhiều thách thức về môi trường đô thị:

- :material-air-purifier: **Ô nhiễm không khí** - Chỉ số AQI thường xuyên ở mức không tốt cho sức khỏe
- :material-car-multiple: **Tắc nghẽn giao thông** - Ảnh hưởng đến chất lượng cuộc sống
- :material-tree: **Thiếu không gian xanh** - Cần tối ưu hóa việc sử dụng các tiện ích công cộng
- :material-database-off: **Dữ liệu phân tán** - Khó khăn trong việc tổng hợp và phân tích

GreenMap giải quyết các vấn đề này bằng cách:

1. **Tập trung dữ liệu**: Thu thập và chuẩn hóa dữ liệu từ nhiều nguồn khác nhau
2. **Trực quan hóa**: Hiển thị dữ liệu trên bản đồ tương tác dễ hiểu
3. **Cảnh báo sớm**: Thông báo khi có vấn đề về môi trường
4. **Tham gia cộng đồng**: Cho phép người dân đóng góp thông tin

## Đối tượng sử dụng

<div class="feature-grid">
  <div class="feature-card">
    <span class="icon">🏛️</span>
    <h3>Cơ Quan Quản Lý</h3>
    <p>Sử dụng Admin Portal để giám sát toàn diện và ra quyết định dựa trên dữ liệu.</p>
  </div>
  <div class="feature-card">
    <span class="icon">👥</span>
    <h3>Người Dân</h3>
    <p>Sử dụng Mobile App để theo dõi môi trường xung quanh và gửi phản ánh.</p>
  </div>
  <div class="feature-card">
    <span class="icon">👨‍💻</span>
    <h3>Nhà Phát Triển</h3>
    <p>Tích hợp dữ liệu qua API chuẩn NGSI-LD để xây dựng ứng dụng mới.</p>
  </div>
</div>

## Các thành phần chính

| Thành phần | Mô tả | Công nghệ |
|------------|-------|-----------|
| **Backend API** | Core service xử lý nghiệp vụ và xác thực | FastAPI, PostgreSQL |
| **Context Broker** | Quản lý dữ liệu ngữ cảnh IoT chuẩn NGSI-LD | Orion-LD, MongoDB |
| **Admin Portal** | Giao diện web cho quản trị viên | React, Vite, MapLibre |
| **Mobile App** | Ứng dụng di động cho người dân | Kotlin, Jetpack Compose |
| **Data Pipeline** | Thu thập và xử lý dữ liệu từ nhiều nguồn | Python, GeoJSON |
