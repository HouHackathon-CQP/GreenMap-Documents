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

# Hướng Dẫn Sử Dụng

Tài liệu hướng dẫn chi tiết cách sử dụng **GreenMap Web Portal** - giao diện quản trị dành cho quản lý môi trường đô thị.

---

## Tổng Quan Giao Diện

### Đăng Nhập & Xác Thực

Truy cập web portal tại địa chỉ được cấp (ví dụ: `https://greenmap.hanoi.vn`).

**Thông tin đăng nhập:**
- Email: Địa chỉ email tài khoản quản trị viên
- Password: Mật khẩu được cấp bởi admin

Sau khi đăng nhập thành công, token xác thực sẽ được lưu trong browser và tự động gửi kèm mọi request.

### Bố Cục Giao Diện

#### Header (Thanh trên cùng)

- Logo GreenMap
- Thanh tìm kiếm nhanh
- Thông báo realtime
- Avatar & dropdown menu

#### Sidebar (Thanh bên trái)

- Dashboard
- Bản đồ
- Báo cáo từ người dân
- Quản lý hạ tầng xanh
- Dữ liệu môi trường
- Cài đặt hệ thống

#### Main Content (Vùng chính giữa)

- Hiển thị nội dung chính của từng trang
- Responsive theo kích thước màn hình

---

## Dashboard - Trang Tổng Quan

Dashboard hiển thị tổng hợp dữ liệu môi trường theo thời gian thực.

### Chỉ Số Chất Lượng Không Khí (AQI)

**Hiển thị:**

- AQI trung bình toàn thành phố
- Màu sắc theo chuẩn: Xanh (Tốt), Vàng (Trung bình), Đỏ (Kém)
- Biểu đồ xu hướng 7 ngày
- So sánh với tuần trước

**Các chỉ số theo dõi:**

- PM2.5 (µg/m³)
- PM10 (µg/m³)
- O3 (ppb)
- NO2 (ppb)
- SO2 (ppb)
- CO (ppm)

### Thống Kê Báo Cáo

**Số liệu:**

- Tổng báo cáo nhận được hôm nay
- Báo cáo đang chờ xử lý
- Báo cáo đã hoàn thành
- Thời gian xử lý trung bình

**Biểu đồ:**

- Xu hướng báo cáo theo ngày
- Phân loại báo cáo theo danh mục
- Bản đồ nhiệt điểm báo cáo

### Tin Tức Môi Trường

**Nguồn tin:**

- Tự động cập nhật từ Hà Nội Mới (RSS feed)
- Refresh 20 tin mới nhất mỗi lần tải
- Hiển thị tiêu đề, tóm tắt, thời gian đăng

**Tính năng:**

- Click vào tin để đọc toàn văn (mở tab mới)
- Auto-refresh định kỳ để cập nhật tin mới
- Sắp xếp theo thời gian (mới nhất trước)

### Hạ Tầng Xanh

**Thống kê:**

- Số lượng công viên
- Trạm sạc xe điện
- Điểm cho thuê xe đạp
- Điểm du lịch xanh

**Trạng thái:**

- Hoạt động bình thường
- Đang bảo trì
- Tạm ngưng

---

## Bản Đồ Tương Tác

### Lớp Dữ Liệu (Layers)

Bản đồ hỗ trợ nhiều lớp dữ liệu có thể bật/tắt:

**Lớp Môi Trường:**

- Chất lượng không khí (màu gradient theo AQI)
- Nhiệt độ và độ ẩm
- Lượng mưa

**Lớp Giao Thông Thời Gian Thực:**

- Trạng thái giao thông realtime từ mô phỏng SUMO
- Màu sắc phân loại: Xanh (Thông thoáng), Vàng (Bình thường), Đỏ (Ùn tắc)
- Auto-refresh mỗi 5 phút
- Cache dữ liệu để tối ưu hiệu suất

### Lớp Dữ Liệu (Layers)

Bản đồ hỗ trợ nhiều lớp dữ liệu có thể bật/tắt:

**Lớp Môi Trường:**

- Chất lượng không khí (màu gradient theo AQI)
- Nhiệt độ và độ ẩm
- Lượng mưa

**Lớp Hạ Tầng:**

- Công viên & không gian xanh
- Trạm sạc xe điện
- Điểm cho thuê xe đạp
- Điểm tham quan du lịch

**Lớp Báo Cáo:**

- Báo cáo từ người dân (markers)
- Mật độ báo cáo (heatmap)

**Lớp Giao Thông:**

- Dữ liệu từ SUMO simulation
- Mật độ phương tiện
- Tốc độ trung bình

### Tương Tác Với Bản Đồ

**Di chuyển:**
- Kéo thả chuột để pan
- Scroll hoặc +/- để zoom
- Double-click để zoom nhanh

**Xem Thông Tin:**
- Click vào marker/polygon để xem popup
- Hover để xem tooltip nhanh

**Tìm Kiếm:**
- Tìm theo địa chỉ
- Tìm theo tên địa điểm
- Tìm theo tọa độ

---

## Quản Lý Báo Cáo

### Danh Sách Báo Cáo

Hiển thị tất cả báo cáo từ người dân qua Mobile App.

**Thông tin mỗi báo cáo:**
- Tiêu đề & mô tả
- Danh mục (Rác thải, Ô nhiễm không khí, Tiếng ồn, Khác)
- Vị trí (địa chỉ + tọa độ)
- Hình ảnh đính kèm
- Thời gian báo cáo
- Trạng thái (Mới, Đang xử lý, Hoàn thành, Từ chối)
- Người báo cáo

**Bộ lọc:**
```
- Trạng thái: Tất cả | Mới | Đang xử lý | Hoàn thành
- Danh mục: Tất cả | Rác thải | Ô nhiễm | Tiếng ồn | Khác
- Thời gian: Hôm nay | 7 ngày | 30 ngày | Tùy chọn
- Khu vực: Theo quận/huyện
```

### Xử Lý Báo Cáo

**Quy trình:**

1. **Xem chi tiết** - Click vào báo cáo để mở modal chi tiết
2. **Đánh giá** - Xác nhận tính hợp lệ của báo cáo
3. **Chuyển trạng thái:**
   - "Đang xử lý" - Đã tiếp nhận và đang giải quyết
   - "Hoàn thành" - Đã xử lý xong
   - "Từ chối" - Báo cáo không hợp lệ (ghi rõ lý do)
4. **Thêm ghi chú** - Cập nhật tiến độ xử lý
5. **Lưu & thông báo** - Người báo cáo sẽ nhận notification

---

## Quản Lý Hạ Tầng Xanh

### Công Viên & Không Gian Xanh

**Danh sách:**
- Hiển thị tất cả công viên trên hệ thống
- Tìm kiếm theo tên hoặc địa chỉ
- Sắp xếp theo diện tích, ngày tạo

**Thêm mới công viên:**

```
Tên công viên: [Nhập tên]
Địa chỉ: [Nhập địa chỉ hoặc chọn trên bản đồ]
Diện tích (m²): [Nhập số]
Mô tả: [Thông tin chi tiết]
Tiện ích: ☑ Sân chơi trẻ em ☑ Đường chạy bộ ☑ WC công cộng
Giờ mở cửa: [Nhập]
Hình ảnh: [Upload]
```

**Chỉnh sửa/Xóa:**
- Click nút "Sửa" để cập nhật thông tin
- Click "Xóa" (cần xác nhận) để xóa khỏi hệ thống

### Trạm Sạc Xe Điện

**Thông tin hiển thị:**
- Tên trạm
- Địa chỉ
- Số cổng sạc
- Loại cổng (Type 2, CCS, CHAdeMO)
- Công suất (kW)
- Trạng thái hoạt động
- Giá cước

**Quản lý:**
- Thêm/sửa/xóa trạm sạc
- Cập nhật trạng thái từng cổng sạc
- Theo dõi lịch sử sử dụng

### Điểm Cho Thuê Xe Đạp

**Thông tin:**
- Tên điểm
- Địa chỉ
- Số lượng xe khả dụng
- Số lượng chỗ đỗ
- Giá thuê (giờ/ngày)
- Nhà cung cấp

**Theo dõi:**
- Số lượt thuê trong ngày
- Xe đạp cần bảo trì
- Điểm có mật độ sử dụng cao

---

## Dữ Liệu Môi Trường

### Xem Dữ Liệu Lịch Sử

**Chất lượng không khí:**
- Biểu đồ xu hướng theo thời gian
- So sánh giữa các khu vực
- Export dữ liệu CSV/JSON

**Thời tiết:**
- Nhiệt độ, độ ẩm, lượng mưa
- Tốc độ gió
- Tia UV

### API Integration

Xem dữ liệu nguồn từ:
- OpenAQ (Chất lượng không khí)
- OpenWeatherMap (Thời tiết)
- SUMO (Giao thông)

---

## Quản Lý Push Notifications

### Gửi Thông Báo Đến Mobile App

**Tab "Gửi Thông Báo":**

Quản trị viên có thể gửi push notification đến tất cả ứng dụng mobile đã đăng ký.

**Các trường thông tin:**

- **Tiêu đề**: Tiêu đề ngắn gọn (ví dụ: "Cảnh báo AQI cao")
- **Nội dung**: Thông báo chi tiết (ví dụ: "AQI Hà Nội đạt 152 - Kém, nên hạn chế ra ngoài")
- **Dữ liệu bổ sung**: JSON object chứa thông tin thêm (tùy chọn)
- **Chế độ thử nghiệm (Dry Run)**: Kiểm tra notification mà không gửi thực tế

**Hai loại gửi:**

1. **Gửi theo Device Token**: Gửi đến tất cả thiết bị đã đăng ký trong database
2. **Gửi theo Topic**: Gửi đến tất cả thiết bị subscribe topic Firebase (ví dụ: topic `greenmap_all`)

### AI Weather Insights

**Tính năng phân tích thời tiết tự động bằng AI:**

- Click nút **"Tạo Nội dung bằng AI"** để phân tích thời tiết + AQI tự động
- Chọn vị trí: Hà Nội (hoặc Hồ Chí Minh trong tương lai)
- Chọn AI Provider: Gemini, Groq, hoặc Auto (thử lần lượt)
- Chỉ định model tùy chỉnh (tùy chọn)

**AI sẽ phân tích:**

- Dự báo thời tiết 24h & 7 ngày
- Chất lượng không khí (AQI) hiện tại
- Lời khuyên hoạt động ngoài trời (đi bộ, chạy bộ, xe đạp)
- Cảnh báo sức khỏe dựa trên AQI & thời tiết

**Kết quả:**

- Nội dung AI được tự động điền vào form notification
- Xem lịch sử các báo cáo AI đã tạo trong tab "Lịch Sử"
- Có thể chỉnh sửa trước khi gửi

### Lịch Sử Notifications

**Tab "Lịch Sử":**

- Xem tất cả notification đã gửi (thành công/thất bại)
- Thông tin: Tiêu đề, nội dung, thời gian gửi, số thiết bị nhận
- Chi tiết response từ Firebase (success_count, failure_count)
- Xóa lịch sử cũ để dọn dẹp database

### Danh Sách Device Tokens

**Tab "Device Tokens":**

- Xem tất cả thiết bị mobile đã đăng ký nhận notification
- Thông tin: Device token, user_id, thời gian đăng ký, trạng thái
- Xóa token không còn active

---

## Cài Đặt & Quản Lý

### Quản Lý Tài Khoản

**Thông tin cá nhân:**
- Cập nhật email, số điện thoại
- Đổi mật khẩu
- Cài đặt ngôn ngữ (Tiếng Việt/English)

**Phân quyền (Admin only):**
- Xem danh sách users
- Thêm/xóa quản trị viên
- Phân quyền: Admin | Moderator | Viewer

### Cài Đặt Hệ Thống

**Thông báo:**
- Bật/tắt email notification
- Bật/tắt push notification
- Cài đặt ngưỡng cảnh báo AQI

**Hiển thị:**
- Chủ đề giao diện (Light/Dark)
- Ngôn ngữ mặc định
- Múi giờ

---

## Các Tính Năng Nâng Cao

### Export Dữ Liệu

Xuất dữ liệu theo định dạng:
- CSV (Excel-compatible)
- JSON (API format)
- GeoJSON (Spatial data)
- PDF Report (Báo cáo tổng hợp)

### Cảnh Báo Tự Động

Hệ thống tự động gửi cảnh báo khi:
- AQI vượt ngưỡng nguy hiểm (> 150)
- Có báo cáo mới cần xử lý gấp
- Hệ thống phát hiện anomaly

### Tích Hợp AI

**Gemini AI Assistant:**
- Phân tích xu hướng ô nhiễm
- Đề xuất giải pháp giảm AQI
- Tóm tắt báo cáo từ người dân

---

## Câu Hỏi Thường Gặp

**Q: Làm sao để reset mật khẩu?**  
A: Click "Quên mật khẩu" tại trang đăng nhập, nhập email để nhận link reset.

**Q: Dữ liệu AQI cập nhật bao lâu một lần?**  
A: Background workers fetch dữ liệu mỗi 15 phút từ OpenAQ API.

**Q: Có thể xem dữ liệu offline không?**  
A: Không. Web portal yêu cầu kết nối internet để truy cập database realtime.

**Q: Làm sao để export báo cáo định kỳ?**  
A: Vào Settings > Scheduled Reports > Tạo lịch export tự động (daily/weekly/monthly).

[Xem thêm câu hỏi →](faq/)
