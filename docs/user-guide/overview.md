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

# Tổng Quan Giao Diện

Giao diện Admin Portal được thiết kế theo nguyên tắc **Dashboard-first**, tập trung vào việc hiển thị thông tin quan trọng một cách trực quan.

## Bố Cục Chính

Giao diện được chia thành 3 phần chính:

```
┌─────────────────────────────────────────────────────┐
│                    Header Bar                       │
├──────────┬──────────────────────────────────────────┤
│          │                                          │
│ Sidebar  │              Main Content                │
│ (Menu)   │              (Dashboard/Map/...)         │
│          │                                          │
│          │                                          │
└──────────┴──────────────────────────────────────────┘
```

### 1. Header Bar

- **Logo & Tên ứng dụng**: GreenMap Admin Portal
- **Search Bar**: Tìm kiếm nhanh địa điểm, báo cáo
- **Notifications**: Thông báo về báo cáo mới, cảnh báo AQI
- **User Menu**: Thông tin tài khoản, đăng xuất

### 2. Sidebar Navigation

Menu điều hướng chính với các mục:

| Icon | Mục | Mô tả |
|------|-----|-------|
| 📊 | Dashboard | Tổng quan KPIs |
| 🗺️ | Bản đồ | Giám sát đa lớp |
| 📢 | Báo cáo | Quản lý phản ánh |
| 🌳 | Công viên | Quản lý không gian xanh |
| ⚡ | Trạm sạc | Quản lý trạm sạc EV |
| 🚴 | Xe đạp | Điểm thuê xe đạp |
| 📸 | Du lịch | Điểm tham quan |
| 👥 | Người dùng | Quản lý tài khoản |
| ⚙️ | Cài đặt | Cấu hình hệ thống |

### 3. Main Content Area

Khu vực hiển thị nội dung chính, thay đổi tùy theo menu được chọn.

## Dashboard Tổng Quan

Dashboard là trang mặc định khi đăng nhập, hiển thị các thông tin quan trọng:

### KPI Cards

Các thẻ thống kê nhanh ở đầu trang:

- **Tổng số trạm**: 120+ trạm quan trắc
- **Trạm Online**: Số trạm đang hoạt động
- **Báo cáo chờ xử lý**: Số lượng PENDING
- **AQI Trung bình**: Chỉ số trung bình toàn thành phố

### Biểu Đồ Phân Tích

- **Bar Chart**: Xếp hạng AQI theo quận/huyện
- **Area Chart**: Xu hướng nhiệt độ 24h
- **Mini Map**: Vị trí các trạm quan trắc

### Bảng Báo Cáo Gần Đây

Danh sách 5 báo cáo mới nhất từ người dân.

## Đăng Nhập

1. Truy cập `http://localhost:5173`
2. Nhập **Email** và **Mật khẩu**
3. Nhấn **Đăng nhập**

!!! warning "Tài khoản Admin mặc định"
    - Email: `admin@greenmap.hanoi`
    - Password: Theo cấu hình trong `.env`
