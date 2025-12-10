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

# Tính Năng Chi Tiết

GreenMap cung cấp một bộ tính năng toàn diện phục vụ việc giám sát và quản lý môi trường đô thị.

## 1. Giám Sát Chất Lượng Không Khí (AQI)

<div class="badge badge-primary">Real-time</div>
<div class="badge badge-success">NGSI-LD</div>

- **Theo dõi liên tục** chỉ số AQI từ các trạm quan trắc
- **Mã màu chuẩn hóa** theo QCVN 05:2013/BTNMT:
  - 🟢 Tốt (0-50)
  - 🟡 Trung bình (51-100)  
  - 🟠 Kém (101-150)
  - 🔴 Xấu (151-200)
  - 🟣 Rất xấu (201-300)
  - 🟤 Nguy hại (>300)
- **Cảnh báo tự động** khi vượt ngưỡng an toàn
- **Lịch sử và xu hướng** qua biểu đồ phân tích

## 2. Thông Tin Thời Tiết

<div class="badge badge-primary">OpenWeather</div>

- Nhiệt độ, độ ẩm, tốc độ gió hiện tại
- Dự báo thời tiết 24 giờ tới
- Biểu đồ kết hợp nhiệt độ và xác suất mưa
- Cảnh báo thời tiết cực đoan

## 3. Bản Đồ Đa Lớp (Multi-layer Map)

<div class="badge badge-primary">MapLibre GL</div>
<div class="badge badge-secondary">3D View</div>

Hệ thống bản đồ hỗ trợ chồng lớp nhiều loại dữ liệu:

| Lớp | Mô tả | Icon |
|-----|-------|------|
| AQI | Chất lượng không khí | 💨 |
| Weather | Thời tiết & lượng mưa | 🌧️ |
| Traffic | Mật độ giao thông | 🚗 |
| Parks | Công viên công cộng | 🌳 |
| Charging | Trạm sạc xe điện | ⚡ |
| Bicycle | Điểm thuê xe đạp | 🚴 |
| Tourism | Điểm tham quan | 📸 |

## 4. Quản Lý Báo Cáo Cộng Đồng

<div class="badge badge-primary">Crowdsourcing</div>

Hệ thống tiếp nhận và xử lý phản ánh từ người dân:

1. **Người dân** chụp ảnh và gửi báo cáo qua Mobile App
2. **Hệ thống** tự động gắn tọa độ GPS và timestamp
3. **Quản trị viên** duyệt và phân loại báo cáo
4. **Đơn vị xử lý** nhận thông tin và phản hồi

**Trạng thái báo cáo:**

- `PENDING` - Chờ xử lý
- `APPROVED` - Đã duyệt
- `REJECTED` - Từ chối

## 5. Quản Lý Hạ Tầng Xanh

CRUD đầy đủ cho các loại hạ tầng:

- **Công viên** - Quản lý không gian xanh công cộng
- **Trạm sạc xe điện** - VinFast và các nhà cung cấp khác
- **Điểm thuê xe đạp** - Dịch vụ xe đạp công cộng
- **Điểm du lịch** - Di tích lịch sử, địa điểm tham quan

## 6. Dashboard Analytics

<div class="badge badge-primary">Data Visualization</div>

- **KPI Cards**: Tổng hợp các chỉ số quan trọng
- **Bar Charts**: So sánh AQI giữa các quận/huyện
- **Area Charts**: Xu hướng nhiệt độ và lượng mưa
- **Geo Heatmap**: Bản đồ nhiệt ô nhiễm

## 7. Xác Thực & Phân Quyền

<div class="badge badge-success">JWT</div>
<div class="badge badge-secondary">OAuth2</div>

- Đăng ký/Đăng nhập bảo mật
- Phân quyền theo vai trò:
  - `ADMIN` - Toàn quyền quản trị
  - `CITIZEN` - Người dùng thông thường
- Token-based authentication (JWT)
