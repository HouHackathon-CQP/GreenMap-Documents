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

# Chính Sách Bảo Mật

## Giới Thiệu

Chúng tôi coi trọng việc bảo mật thông tin của người dùng và hệ thống. Tài liệu này mô tả các biện pháp bảo mật được áp dụng và cách báo cáo lỗ hổng bảo mật.

## Báo Cáo Lỗ Hổng Bảo Mật

Nếu bạn phát hiện lỗ hổng bảo mật, vui lòng:

1. **KHÔNG** công khai lỗ hổng trên GitHub Issues
2. Gửi email đến: **security@greenmap.hanoi**
3. Mô tả chi tiết:
   - Loại lỗ hổng
   - Các bước để tái tạo
   - Tác động tiềm ẩn
   - Đề xuất cách khắc phục (nếu có)

!!! warning "Responsible Disclosure"
    Chúng tôi cam kết phản hồi trong vòng 48 giờ và làm việc cùng bạn để khắc phục vấn đề trước khi công khai.

## Biện Pháp Bảo Mật

### Authentication & Authorization

- ✅ JWT với thời hạn ngắn (30 phút)
- ✅ Password hashing với bcrypt
- ✅ Rate limiting để chống brute force
- ✅ Role-based access control (RBAC)

### Data Protection

- ✅ HTTPS trong production
- ✅ Input validation với Pydantic
- ✅ SQL injection prevention với SQLAlchemy ORM
- ✅ XSS protection headers

### Infrastructure

- ✅ Docker containerization
- ✅ Non-root container users
- ✅ Network isolation giữa services
- ✅ Secret management qua environment variables

## Supported Versions

| Version | Supported |
|---------|-----------|
| 1.x.x   | ✅         |
| < 1.0   | ❌         |

## Checklist Bảo Mật

Khi triển khai production:

- [ ] Thay đổi `SECRET_KEY` mặc định
- [ ] Disable debug mode
- [ ] Cấu hình HTTPS
- [ ] Giới hạn CORS origins
- [ ] Bật rate limiting
- [ ] Thiết lập backup định kỳ
- [ ] Cấu hình firewall
- [ ] Monitor logs
