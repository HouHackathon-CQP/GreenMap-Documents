# Các Câu Hỏi Thường Gặp (FAQ)

## Câu Hỏi Chung

### GreenMap là gì?
GreenMap là hệ thống giám sát chất lượng không khí và quản lý dữ liệu môi trường với bản đồ tương tác.

### GreenMap có miễn phí không?
Có, GreenMap hoàn toàn miễn phí và mã nguồn mở (MIT License).

### Tôi có thể đóng góp vào GreenMap không?
Có! Xem [Contributing Guidelines](../contributing/guidelines.md) để biết cách đóng góp.

### GreenMap bảo vệ dữ liệu cá nhân của tôi như thế nào?
Chúng tôi:
- Mã hóa mật khẩu (bcrypt)
- Sử dụng HTTPS
- Không chia sẻ dữ liệu với bên thứ 3
- Tuân thủ quy định bảo vệ dữ liệu

---

## Tài Khoản & Đăng Nhập

### Quên mật khẩu, làm thế nào?
1. Nhấp "Forgot Password?" ở trang login
2. Nhập email của bạn
3. Kiểm tra hộp thư email
4. Nhấp link đặt lại mật khẩu
5. Nhập mật khẩu mới

### Tôi có thể sử dụng email khác không?
Hiện tại không hỗ trợ thay đổi email sau khi đăng ký. Bạn phải tạo tài khoản mới.

### Tôi có thể sử dụng tên người dùng (username) thay vì email không?
Hiện tại GreenMap chỉ hỗ trợ đăng nhập bằng email.

### Tôi đã bị khóa tài khoản, làm thế nào?
Nếu tài khoản bị khóa (sau 5 lần đăng nhập sai):
- Chờ 15 phút trước khi thử lại
- Hoặc sử dụng "Forgot Password" để đặt lại

---

## Bản Đồ & Dữ Liệu

### Dữ liệu bản đồ được cập nhật bao thường?
- **Sensors (AQI)**: Mỗi 5-10 phút
- **Weather**: Mỗi 30 phút
- **Other Data (Bikes, Parks)**: Mỗi ngày
- **User Reports**: Thời gian thực

### Tại sao một số điểm không hiển thị?
Có thể là:
- Lớp dữ liệu bị tắt (kiểm tra sidebar)
- Không có dữ liệu trong khu vực
- Bộ lọc loại trừ chúng (kiểm tra bộ lọc)

### Tôi có thể tải dữ liệu không?
Có, bạn có thể:
- Export báo cáo của bạn (Settings → Export)
- Sử dụng API (xem [API Documentation](../api-reference/overview.md))

### Làm thế nào để cập nhật dữ liệu?
Tùy vào loại dữ liệu:
- **Sensors**: Cập nhật tự động từ APIs
- **User Reports**: Cập nhật khi bạn gửi báo cáo
- **GeoJSON Data**: Liên hệ team để cập nhật

---

## Báo Cáo

### Tôi có thể xóa báo cáo của tôi không?
Bạn có thể xóa báo cáo nếu:
- Trạng thái là "Pending" (chưa được xác nhận)
- Hoặc "Closed" (đã đóng)

Nếu báo cáo đang được xử lý, bạn không thể xóa.

### Tôi có thể chỉnh sửa báo cáo không?
- **Pending**: Có thể chỉnh sửa toàn bộ
- **In Progress**: Có thể thêm bình luận/ảnh
- **Resolved/Closed**: Chỉ xem được

### Báo cáo của tôi được hiển thị công khai không?
Điều này phụ thuộc vào cài đặt quyền riêng tư của bạn:
- Nếu "Public": Bất cứ ai có thể xem
- Nếu "Anonymous": Không hiển thị tên bạn
- Kiểm tra [Settings](settings.md) để thay đổi

### Báo cáo của tôi bị nhầm lẫn/spam, làm thế nào?
1. Mở báo cáo
2. Nhấp **Report as Inappropriate**
3. Chọn lý do (spam, sai địa điểm, etc.)
4. Gửi

### Tôi có thể báo cáo bình luận không phù hợp không?
Có, nhấp **Report** hoặc **⚠️** ở bình luận, chọn lý do và gửi.

---

## Cài Đặt & Thông Báo

### Tôi không nhận được thông báo, làm thế nào?
Kiểm tra:
1. Thông báo được bật trong Settings → Notifications
2. Bạn cho phép browser/ứng dụng gửi thông báo
3. Email notification đã được enable
4. Email filter (check spam folder)

### Làm thế nào để tắt tất cả thông báo?
Settings → Notifications → Tắt tất cả các toggle

### Tôi có thể thay đổi email không?
Hiện tại không hỗ trợ thay đổi email trong Settings. Liên hệ support để hỗ trợ.

### Làm thế nào để thay đổi ngôn ngữ?
Settings → General → Language → Chọn ngôn ngữ

---

## Vấn Đề & Xử Lý Sự Cố

### Trang không tải, làm thế nào?
1. Làm tươi (F5) hoặc Ctrl+Shift+R
2. Xóa cache (Settings → Clear Cache)
3. Thử browser khác
4. Kiểm tra kết nối internet

### Bản đồ bị lỗi/không hiển thị đúng
1. Làm tươi trang
2. Thử browser khác
3. Kiểm tra cài đặt bản đồ
4. Nếu vẫn lỗi, báo cáo issue trên GitHub

### Không thể upload ảnh
- Ảnh quá lớn (tối đa 5MB/ảnh)
- Định dạng không hỗ trợ (hỗ trợ: JPG, PNG, GIF)
- Kết nối internet quá chậm

### Ứng dụng chạy chậm
1. Tắt một số lớp dữ liệu không cần
2. Giảm zoom level
3. Xóa cache
4. Thử lite mode (nếu có)

### Lỗi CORS hoặc 401 Unauthorized
- Đăng xuất rồi đăng nhập lại
- Token hết hạn, cần làm tươi
- Liên hệ support nếu vẫn không được

---

## API & Developer

### Tôi có thể sử dụng API không?
Có! Xem [API Documentation](../api-reference/overview.md)

### Tôi cần API key, làm thế nào?
1. Settings → Advanced → API Keys
2. Tạo key mới
3. Sử dụng trong requests

### API có rate limit không?
Có:
- Public: 100 requests/hour
- Authenticated: 1000 requests/hour

### Tôi có thể tích hợp dữ liệu GreenMap vào app của tôi không?
Có, bạn có thể:
- Sử dụng REST API
- Sử dụng data export (JSON/CSV)

---

## Liên Hệ & Hỗ Trợ

### Tôi tìm thấy bug, làm thế nào?
1. Tạo issue trên GitHub: github.com/HouHackathon-CQP
2. Mô tả chi tiết:
   - Bạn đang làm gì
   - Lỗi là gì
   - Screenshot/logs

### Tôi có câu hỏi/đề xuất
1. **GitHub Discussions**: Thảo luận trên GitHub
2. **Email**: Gửi email cho team
3. **Issues**: Tạo feature request issue

### Tôi muốn báo cáo lỗi bảo mật
**Không** tạo public issue!
- Email: security@greenmap.example.com
- Mô tả chi tiết lỗi
- Không chia sẻ công khai cho đến khi được fix

---

Không tìm thấy câu trả lời? Hãy:
- Xem [User Guide](overview.md)
- [Contact Support](../contributing/guidelines.md)
- Tạo GitHub Issue

---

**Cảm ơn bạn đã sử dụng GreenMap! 🌍**
