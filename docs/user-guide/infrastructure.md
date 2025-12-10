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

# Quản Lý Hạ Tầng

Hệ thống hỗ trợ quản lý CRUD đầy đủ cho 4 loại hạ tầng xanh.

## Các Loại Hạ Tầng

| Loại | Đường dẫn | Mô tả |
|------|-----------|-------|
| 🌳 Công viên | `/parks` | Công viên, vườn hoa, không gian xanh |
| ⚡ Trạm sạc | `/charging` | Trạm sạc xe điện |
| 🚴 Xe đạp | `/bikes` | Điểm thuê xe đạp công cộng |
| 📸 Du lịch | `/tourist` | Điểm tham quan |

## Giao Diện Chung

Tất cả các trang quản lý hạ tầng có cấu trúc tương tự:

```
┌─────────────────────────────────────────────────────┐
│ Tiêu đề                         [+ Thêm mới]       │
├─────────────────────────────────────────────────────┤
│ [Tìm kiếm...                    ] [Lọc ▼]          │
├─────────────────────────────────────────────────────┤
│ ┌─────────────────────────────────────────────────┐ │
│ │ ID │ Tên          │ Vị trí    │ Hành động      │ │
│ ├────┼──────────────┼───────────┼────────────────┤ │
│ │ 1  │ Công viên A  │ Hoàn Kiếm │ [Sửa] [Xóa]    │ │
│ │ 2  │ Công viên B  │ Ba Đình   │ [Sửa] [Xóa]    │ │
│ │ ...│ ...          │ ...       │ ...            │ │
│ └─────────────────────────────────────────────────┘ │
├─────────────────────────────────────────────────────┤
│              [< 1 2 3 4 5 >]                        │
└─────────────────────────────────────────────────────┘
```

## Thao Tác CRUD

### Thêm Mới (Create)

1. Click nút **[+ Thêm mới]**
2. Điền thông tin trong form:
   - **Tên**: Tên địa điểm (bắt buộc)
   - **Mô tả**: Thông tin chi tiết
   - **Tọa độ**: Lat/Long (hoặc chọn trên bản đồ)
   - **Thông tin bổ sung**: Tùy loại hạ tầng
3. Click **[Lưu]**

### Xem Chi Tiết (Read)

Click vào tên địa điểm hoặc icon 👁️ để xem chi tiết.

### Chỉnh Sửa (Update)

1. Click nút **[Sửa]** hoặc icon ✏️
2. Chỉnh sửa thông tin trong form
3. Click **[Lưu thay đổi]**

### Xóa (Delete)

1. Click nút **[Xóa]** hoặc icon 🗑️
2. Xác nhận trong dialog: "Bạn có chắc muốn xóa?"
3. Click **[Xác nhận]**

!!! warning "Lưu ý"
    Thao tác xóa không thể hoàn tác. Dữ liệu sẽ bị xóa vĩnh viễn.

## Chi Tiết Từng Loại

### 🌳 Quản Lý Công Viên

Các trường thông tin:

| Trường | Kiểu | Mô tả |
|--------|------|-------|
| name | String | Tên công viên |
| description | Text | Mô tả chi tiết |
| address | String | Địa chỉ |
| area | Number | Diện tích (m²) |
| coordinates | [lat, lng] | Tọa độ |

### ⚡ Quản Lý Trạm Sạc

Các trường thông tin:

| Trường | Kiểu | Mô tả |
|--------|------|-------|
| name | String | Tên trạm |
| operator | String | Nhà vận hành (VinFast, E-Station...) |
| capacity | Number | Số cổng sạc |
| connector_types | Array | Loại cổng (Type 2, CCS2...) |
| status | Enum | Trạng thái (active/inactive) |
| coordinates | [lat, lng] | Tọa độ |

### 🚴 Quản Lý Điểm Thuê Xe Đạp

Các trường thông tin:

| Trường | Kiểu | Mô tả |
|--------|------|-------|
| name | String | Tên điểm |
| operator | String | Nhà vận hành |
| capacity | Number | Số xe tối đa |
| available | Number | Số xe khả dụng |
| coordinates | [lat, lng] | Tọa độ |

### 📸 Quản Lý Điểm Du Lịch

Các trường thông tin:

| Trường | Kiểu | Mô tả |
|--------|------|-------|
| name | String | Tên địa điểm |
| type | Enum | Loại hình (Đền, Chùa, Di tích...) |
| description | Text | Mô tả |
| opening_hours | String | Giờ mở cửa |
| coordinates | [lat, lng] | Tọa độ |
