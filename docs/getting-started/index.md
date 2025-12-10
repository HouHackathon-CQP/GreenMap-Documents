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

# Bắt Đầu với GreenMap

Chào mừng bạn đến với tài liệu hướng dẫn của GreenMap! Phần này sẽ giúp bạn hiểu rõ về dự án và bắt đầu sử dụng hoặc phát triển hệ thống.

---

## Tổng Quan Nhanh

GreenMap là hệ sinh thái quản lý dữ liệu môi trường đô thị thông minh, bao gồm **4 repositories** độc lập:

<div class="doc-grid">
  <div class="doc-card">
    <h3>Backend</h3>
    <p>REST API server với FastAPI, PostgreSQL và PostGIS. Tích hợp NGSI-LD Context Broker để xử lý dữ liệu IoT theo chuẩn FIWARE.</p>
    <a href="../developer-guide/backend/" class="doc-link">Xem chi tiết →</a>
  </div>
  
  <div class="doc-card">
    <h3>Frontend</h3>
    <p>Web portal quản trị với React, Vite và MapLibre GL JS. Giao diện tương tác cho quản trị viên giám sát và quản lý hệ thống.</p>
    <a href="../developer-guide/frontend/" class="doc-link">Xem chi tiết →</a>
  </div>
  
  <div class="doc-card">
    <h3>Mobile</h3>
    <p>Ứng dụng Android native với Kotlin và Jetpack Compose. Cho phép người dân báo cáo vấn đề môi trường và xem thông tin AQI.</p>
    <a href="../developer-guide/mobile/" class="doc-link">Xem chi tiết →</a>
  </div>
  
  <div class="doc-card">
    <h3>Data Pipeline</h3>
    <p>ETL pipeline thu thập dữ liệu từ OpenStreetMap, OpenAQ, Weather API và SUMO traffic simulation.</p>
    <a href="../developer-guide/data/" class="doc-link">Xem chi tiết →</a>
  </div>
</div>

---

## Yêu Cầu Hệ Thống

Trước khi cài đặt, hãy đảm bảo máy tính của bạn đáp ứng các yêu cầu sau:

### Phần Cứng Tối Thiểu

| Thành phần | Yêu cầu tối thiểu | Khuyến nghị |
|------------|-------------------|-------------|
| **CPU** | 2 cores | 4+ cores |
| **RAM** | 4 GB | 8+ GB |
| **Ổ cứng** | 10 GB trống | 20+ GB SSD |
| **Mạng** | 10 Mbps | 50+ Mbps |

### Phần Mềm Bắt Buộc

#### Backend Development

- Python 3.11+
- PostgreSQL 15+ with PostGIS extension
- Docker & Docker Compose
- Git

#### Frontend Development

- Node.js 18+ & npm/yarn
- Modern browser (Chrome, Firefox, Edge)

#### Mobile Development

- Android Studio Hedgehog+
- JDK 17+
- Android SDK 34+

---

## Hướng Dẫn Cài Đặt

### Bước 1: Clone Repositories

```bash
# Clone tất cả repositories
git clone https://github.com/HouHackathon-CQP/GreenMap-Backend.git
git clone https://github.com/HouHackathon-CQP/GreenMap-Frontend.git
git clone https://github.com/HouHackathon-CQP/GreenMap-Mobile-App.git
git clone https://github.com/HouHackathon-CQP/GreenMap-Data.git
```

### Bước 2: Cài Đặt Backend

```bash
cd GreenMap-Backend

# Tạo virtual environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Setup database
cp env.example .env
# Chỉnh sửa .env với thông tin database của bạn

# Initialize database
python init_db.py

# Chạy server
uvicorn app.main:app --reload
```

Server sẽ chạy tại `http://localhost:8000`

### Bước 3: Cài Đặt Frontend

```bash
cd GreenMap-Frontend

# Install dependencies
npm install

# Setup environment
cp .env.example .env.local
# Chỉnh sửa .env.local với API URL

# Chạy development server
npm run dev
```

Web portal sẽ chạy tại `http://localhost:5173`

### Bước 4: Cài Đặt Mobile (Optional)

```bash
cd GreenMap-Mobile-App

# Mở project trong Android Studio
# Sync Gradle dependencies
# Chạy app trên emulator hoặc device
```

---

## Kiến Trúc Hệ Thống

### Luồng Dữ Liệu

**Data Sources → Backend API → Clients**

**Nguồn dữ liệu:**

- OpenStreetMap
- OpenAQ
- Weather API
- SUMO Traffic

**Backend xử lý:**

- FastAPI Server
- PostgreSQL Database
- Orion-LD Context Broker
- Background Workers

**Ứng dụng người dùng:**

- Web Portal
- Mobile App

### Công Nghệ Sử Dụng

#### Backend

- FastAPI (Python web framework)
- PostgreSQL + PostGIS (Spatial database)
- SQLAlchemy (ORM)
- Alembic (Database migrations)
- Orion-LD Context Broker (NGSI-LD standard)

#### Frontend

- React 18 (UI library)
- Vite (Build tool)
- MapLibre GL JS (Interactive maps)
- TanStack Query (Data fetching)
- Tailwind CSS (Styling)

#### Mobile

- Kotlin (Programming language)
- Jetpack Compose (UI toolkit)
- Ktor (HTTP client)
- Coil (Image loading)
- MVI Architecture

#### Data Pipeline

- Python scripts
- OpenStreetMap Overpass API
- OpenAQ API integration
- SUMO traffic simulation

---

## Các Bước Tiếp Theo

1. **[Tìm hiểu chi tiết về Kiến trúc](architecture/)** - Hiểu rõ cách các thành phần tương tác với nhau

2. **[Khám phá Tính năng](features/)** - Xem các chức năng chính của hệ thống

3. **[Đọc Tài liệu API](../api-reference/)** - Tham khảo các REST API endpoints

4. **[Hướng dẫn Sử dụng](../user-guide/)** - Học cách sử dụng web portal

5. **[Đóng góp vào dự án](../contributing/)** - Tham gia phát triển GreenMap

---

## Cần Giúp Đỡ?

Nếu gặp vấn đề trong quá trình cài đặt:

- Xem [FAQ](../user-guide/faq/) cho các câu hỏi thường gặp
- Tạo issue trên [GitHub](https://github.com/HouHackathon-CQP)
- Liên hệ team qua email: support@greenmap.vn
