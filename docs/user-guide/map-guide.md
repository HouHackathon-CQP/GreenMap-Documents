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

# Bản Đồ Tương Tác

Bản đồ là thành phần cốt lõi của GreenMap, cho phép trực quan hóa dữ liệu môi trường trên không gian địa lý.

## Giao Diện Bản Đồ

```
┌─────────────────────────────────────────────────────┐
│  Layer Controls  │        Map View        │ Legend │
│  ┌───────────┐   │                        │        │
│  │ 💨 AQI    │   │    [Interactive Map]   │ 🟢 Tốt │
│  │ 🌧️ Rain   │   │                        │ 🟡 TB  │
│  │ 🚗 Traffic│   │         📍 📍          │ 🟠 Kém │
│  │ 🌳 Parks  │   │       📍    📍         │ 🔴 Xấu │
│  │ ⚡ Charge │   │    📍        📍        │        │
│  │ 🚴 Bikes  │   │                        │        │
│  │ 📸 Tourist│   │                        │        │
│  └───────────┘   │                        │        │
├──────────────────┴────────────────────────┴────────┤
│                   Location Details Panel           │
└────────────────────────────────────────────────────┘
```

## Các Lớp Dữ Liệu (Layers)

### 💨 AQI Layer (Chất lượng không khí)

Hiển thị các trạm quan trắc với màu sắc theo thang đo QCVN:

| Màu | Mức độ | AQI | Ý nghĩa |
|-----|--------|-----|---------|
| 🟢 | Tốt | 0-50 | An toàn cho mọi người |
| 🟡 | Trung bình | 51-100 | Chấp nhận được |
| 🟠 | Kém | 101-150 | Nhạy cảm với nhóm yếu |
| 🔴 | Xấu | 151-200 | Ảnh hưởng sức khỏe |
| 🟣 | Rất xấu | 201-300 | Cảnh báo sức khỏe |
| 🟤 | Nguy hại | >300 | Khẩn cấp |

**Cách sử dụng:**
1. Click vào marker để xem chi tiết AQI
2. Popup hiển thị: Tên trạm, AQI, PM2.5, PM10, thời gian cập nhật

### 🌧️ Weather Layer (Thời tiết)

Hiển thị thông tin thời tiết tại các vị trí:

- Nhiệt độ hiện tại (°C)
- Độ ẩm (%)
- Tốc độ gió (m/s)
- Lượng mưa (mm)

### 🚗 Traffic Layer (Giao thông)

Mật độ giao thông theo thời gian thực:

- 🟢 **Xanh**: Thông thoáng
- 🟠 **Cam**: Đông đúc
- 🔴 **Đỏ**: Tắc nghẽn

### 🌳 Parks Layer (Công viên)

Vị trí các công viên và không gian xanh:

- Tên công viên
- Diện tích
- Địa chỉ

### ⚡ Charging Stations (Trạm sạc)

Trạm sạc xe điện:

- Nhà cung cấp (VinFast, E-Station...)
- Số cổng sạc
- Trạng thái hoạt động

### 🚴 Bicycle Rental (Thuê xe đạp)

Điểm thuê xe đạp công cộng:

- Tên trạm
- Số xe khả dụng
- Địa chỉ

### 📸 Tourist Attractions (Du lịch)

Điểm tham quan:

- Tên địa điểm
- Loại hình (Đền, chùa, di tích...)
- Mô tả ngắn

## Điều Khiển Bản Đồ

### Zoom & Pan

- **Scroll** để zoom in/out
- **Drag** để di chuyển bản đồ
- **Double-click** để zoom vào điểm

### Công Cụ

| Nút | Chức năng |
|-----|-----------|
| 🔍+ | Zoom in |
| 🔍- | Zoom out |
| 📍 | Định vị vị trí hiện tại |
| 🧭 | Reset về góc nhìn mặc định |
| 🎚️ | Bộ lọc bán kính (1km - 10km) |

## Tips

!!! tip "Mẹo sử dụng"
    - Bật/tắt các layer bằng cách click vào tên layer trong panel bên trái
    - Sử dụng bộ lọc bán kính để tìm tiện ích gần vị trí cụ thể
    - Click và giữ để xem thông tin chi tiết của nhiều marker cùng lúc
