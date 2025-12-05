# Tài liệu GreenMap

Chào mừng đến với kho tài liệu chính thức cho dự án GreenMap!

## 📚 Giới thiệu

Kho lưu trữ này chứa tài liệu đầy đủ cho GreenMap, một nền tảng sáng tạo được thiết kế để kết nối mọi người với các sáng kiến môi trường và thúc đẩy các hành động bền vững trong cộng đồng trên toàn thế giới.

## 🚀 Bắt đầu nhanh

### Yêu cầu

- Python 3.8 trở lên
- pip

### Cài đặt

1. Sao chép kho lưu trữ này:
   ```bash
   git clone https://github.com/HouHackathon-CQP/GreenMap-Documents.git
   cd GreenMap-Documents
   ```

2. Cài đặt các phụ thuộc:
   ```bash
   pip install -r requirements.txt
   ```

### Xây dựng tài liệu

Xây dựng trang web tĩnh:
```bash
mkdocs build
```

Trang web đã xây dựng sẽ nằm trong thư mục `site/`.

### Máy chủ phát triển

Chạy máy chủ phát triển cục bộ với tính năng tải lại trực tiếp:
```bash
mkdocs serve
```

Sau đó mở trình duyệt của bạn tại `http://localhost:8000`

## 📖 Cấu trúc tài liệu

```
docs/
├── index.md                    # Trang chủ
├── getting-started/
│   ├── introduction.md         # Giới thiệu về GreenMap
│   ├── installation.md         # Hướng dẫn cài đặt
│   └── quick-start.md          # Hướng dẫn bắt đầu nhanh
├── user-guide/
│   ├── overview.md             # Tổng quan hướng dẫn người dùng
│   └── features.md             # Tính năng chi tiết
├── api-reference/
│   ├── overview.md             # Tổng quan API
│   └── endpoints.md            # Tài liệu tham khảo điểm cuối API
├── contributing/
│   ├── guidelines.md           # Hướng dẫn đóng góp
│   └── code-of-conduct.md      # Quy tắc ứng xử
└── about.md                    # Về GreenMap
```

## 🛠️ Công nghệ

- **[MkDocs](https://www.mkdocs.org/)** - Trình tạo trang web tĩnh
- **[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)** - Chủ đề Material Design
- **[PyMdown Extensions](https://facelessuser.github.io/pymdown-extensions/)** - Tiện ích mở rộng Markdown

## 🤝 Đóng góp

Chúng tôi hoan nghênh các đóng góp cho tài liệu! Vui lòng đọc [Hướng dẫn đóng góp](docs/contributing/guidelines.md) của chúng tôi trước khi gửi pull request.

### Cách đóng góp

1. Fork kho lưu trữ này
2. Tạo một nhánh mới (`git checkout -b docs/your-feature`)
3. Thực hiện các thay đổi của bạn
4. Kiểm tra cục bộ với `mkdocs serve`
5. Commit các thay đổi của bạn (`git commit -m 'Add some documentation'`)
6. Push lên nhánh (`git push origin docs/your-feature`)
7. Mở một Pull Request

## 📝 Hướng dẫn tài liệu

Khi đóng góp vào tài liệu:

- Sử dụng ngôn ngữ rõ ràng, súc tích
- Bao gồm các ví dụ mã khi thích hợp
- Thêm ảnh chụp màn hình cho tài liệu liên quan đến giao diện người dùng
- Kiểm tra tất cả các liên kết và đoạn mã
- Tuân theo cấu trúc và phong cách hiện có
- Chạy `mkdocs build --strict` để kiểm tra lỗi

## 📄 Giấy phép

Dự án này được cấp phép theo Giấy phép MIT - xem tệp [LICENSE](LICENSE) để biết chi tiết.

## 🌍 Liên kết

- **Dự án chính**: [GreenMap](https://github.com/HouHackathon-CQP/GreenMap)
- **Trang tài liệu**: [GreenMap Docs](https://houhackathon-cqp.github.io/GreenMap-Documents/)
- **Cộng đồng**: [Discord](https://discord.gg/greenmap)

## 💚 Hỗ trợ

Nếu bạn cần trợ giúp hoặc có câu hỏi:

- Mở một [issue](https://github.com/HouHackathon-CQP/GreenMap-Documents/issues)
- Tham gia [cộng đồng Discord](https://discord.gg/greenmap) của chúng tôi
- Gửi email cho chúng tôi tại support@greenmap.example.com

---

*Làm cho hành động môi trường dễ tiếp cận với mọi người!* 🌍💚
