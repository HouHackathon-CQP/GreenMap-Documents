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

# Câu Hỏi Thường Gặp (FAQ)

## Tài Khoản & Đăng Nhập

??? question "Tôi quên mật khẩu, làm sao để lấy lại?"
    Hiện tại hệ thống chưa hỗ trợ tính năng quên mật khẩu tự động. Vui lòng liên hệ quản trị viên để được reset mật khẩu.

??? question "Làm sao để tạo tài khoản Admin mới?"
    Chỉ có Super Admin mới có quyền tạo tài khoản Admin. Vào menu **Người dùng** → **Thêm mới** → Chọn vai trò **Admin**.

??? question "Tôi có thể đăng nhập từ nhiều thiết bị không?"
    Có, bạn có thể đăng nhập từ nhiều thiết bị cùng lúc. Token JWT có thời hạn 30 phút (mặc định).

## Bản Đồ

??? question "Bản đồ không hiển thị, chỉ thấy màu xám?"
    Nguyên nhân có thể là:
    
    1. **Thiếu API Key**: Kiểm tra biến `VITE_MAPTILER_KEY` trong file `.env`
    2. **API Key hết hạn**: Đăng nhập [MapTiler](https://www.maptiler.com/) để kiểm tra
    3. **Lỗi mạng**: Kiểm tra kết nối Internet

??? question "Dữ liệu AQI không cập nhật?"
    Kiểm tra các agent có đang chạy không:
    ```bash
    # Kiểm tra AQI Agent
    python aqi_agent.py
    ```
    Nếu lỗi, kiểm tra API key của OpenAQ trong file `.env`.

??? question "Làm sao để thêm layer mới?"
    Cần chỉnh sửa source code Frontend. Tham khảo tài liệu [Developer Guide](../developer-guide/) để biết cách thêm layer.

## Báo Cáo

??? question "Có giới hạn số lượng báo cáo không?"
    Không có giới hạn. Tuy nhiên, hệ thống có cơ chế rate limiting để tránh spam (tối đa 10 báo cáo/phút/người dùng).

??? question "Hình ảnh báo cáo được lưu ở đâu?"
    Hình ảnh được lưu trữ trên server trong thư mục `/uploads/reports/`. Trong production nên dùng cloud storage (S3, GCS).

??? question "Tôi có thể xuất danh sách báo cáo không?"
    Chức năng export đang được phát triển. Tạm thời có thể sử dụng API endpoint để lấy dữ liệu JSON.

## Kỹ Thuật

??? question "Hệ thống hỗ trợ bao nhiêu người dùng đồng thời?"
    Với cấu hình mặc định (Docker Compose), hệ thống có thể xử lý ~100 concurrent users. Để scale up, cần triển khai với Kubernetes.

??? question "Dữ liệu được backup như thế nào?"
    Cần tự thiết lập backup cho PostgreSQL và MongoDB. Khuyến nghị sử dụng `pg_dump` và `mongodump` với cron job hàng ngày.

??? question "Làm sao để deploy lên production?"
    Tham khảo tài liệu [Developer Guide > Deployment](../developer-guide/) để biết cách triển khai với Docker Swarm hoặc Kubernetes.

## Mobile App

??? question "App có trên iOS không?"
    Hiện tại chỉ có phiên bản Android. iOS đang trong kế hoạch phát triển.

??? question "Làm sao để test app trên thiết bị thật?"
    1. Build APK: `./gradlew assembleDebug`
    2. Cài đặt file `.apk` lên điện thoại
    3. Đảm bảo điện thoại và server cùng mạng WiFi

## Liên Hệ Hỗ Trợ

Nếu không tìm thấy câu trả lời, vui lòng:

- 📧 Email: support@greenmap.hanoi
- 💬 GitHub Issues: [Tạo issue mới](https://github.com/HouHackathon-CQP/GreenMap-Backend/issues)
