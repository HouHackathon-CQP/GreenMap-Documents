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

<!--docs/user-guide/features.md-->
# Các Tính Năng GreenMap-Frontend

GreenMap-Frontend cung cấp một bộ tính năng toàn diện để giám sát chất lượng không khí và quản lý dữ liệu môi trường.

## Bản Đồ Tương Tác

### Tính Năng Chính

- **Zoom & Pan**: Phóng to, thu nhỏ, và di chuyển trên bản đồ
- **Multiple Layers**: Các lớp dữ liệu khác nhau (Sensors, Bikes, Charging, Parks, Attractions)
- **Click for Details**: Nhấp vào điểm bất kỳ để xem thông tin chi tiết
- **Real-time Updates**: Dữ liệu cập nhật theo thời gian thực

### Các Loại Điểm Dữ Liệu

| Biểu Tượng | Loại | Thông Tin |
|-----------|------|----------|
| 🟢 | Sensor | AQI, Thời tiết, Tọa độ |
| 🚲 | Bicycle Rental | Tên trạm, Vị trí |
| 🔌 | Charging Station | Loại sạc, Nhà cung cấp |
| 🌳 | Park | Tên công viên, Mô tả |
| 🏛️ | Tourist Attraction | Tên địa điểm, Thông tin |

## Chỉ Số AQI & Thời Tiết

### Chỉ Số AQI

| Giá Trị | Mức | Màu |
|--------|-----|-----|
| 0-50 | Tốt | Xanh |
| 51-100 | Trung Bình | Vàng |
| 101-150 | Xấu | Cam |
| 151-200 | Rất Xấu | Đỏ |
| 201+ | Nguy Hiểm | Tím |

### Dữ Liệu Thời Tiết

- Nhiệt độ hiện tại
- Độ ẩm
- Tốc độ gió
- Điều kiện thời tiết
- Dự báo

## Báo Cáo Sự Cố

### Tạo Báo Cáo

1. Nhấp biểu tượng báo cáo trên bản đồ
2. Chọn vị trí (hoặc tự động từ vị trí hiện tại)
3. Điền thông tin:
   - **Title**: Tiêu đề báo cáo
   - **Description**: Mô tả chi tiết
   - **Category**: Loại vấn đề (pollution, waste, etc.)
   - **Severity**: Mức độ (low, medium, high)
   - **Images**: Tải lên hình ảnh

4. Nhấp **Submit Report**

### Quản Lý Báo Cáo

Xem các báo cáo của bạn:
- Trạng thái (pending, reviewed, resolved)
- Phản hồi từ cộng đồng
- Dữ liệu cập nhật

## Lọc & Tìm Kiếm

### Lọc Dữ Liệu

Sử dụng sidebar để lọc:
- **By Type**: Sensor, Bike, Charging, Park, etc.
- **By AQI Range**: 0-50, 51-100, etc.
- **By Date**: Hôm nay, tuần này, tháng này
- **By Location**: Radius tìm kiếm

### Tìm Kiếm

Sử dụng search bar:
- Tìm kiếm theo tên vị trí
- Tìm kiếm theo địa chỉ
- Tìm kiếm theo ID sensor

## Chế Độ Tối/Sáng

Nhấp biểu tượng mặt trăng/mặt trời ở góc trên bên phải để:
- **Light Mode**: Giao diện sáng, dễ dàng trong ngày
- **Dark Mode**: Giao diện tối, bảo vệ mắt vào đêm

---

Để biết thêm, xem [Map Guide](map-guide.md) hoặc [User Guide Overview](overview.md).
