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

# Hướng Dẫn Cài Đặt

Hướng dẫn chi tiết cài đặt từng thành phần của hệ thống GreenMap.

## Cài Đặt Nhanh (Docker)

Cách nhanh nhất để chạy toàn bộ hệ thống:

```bash
# 1. Clone Backend repository
git clone https://github.com/HouHackathon-CQP/GreenMap-Backend.git
cd GreenMap-Backend

# 2. Tạo file .env từ template
cp env.example .env
# Chỉnh sửa .env với các giá trị phù hợp

# 3. Khởi động với Docker Compose
docker-compose up -d

# 4. Kiểm tra trạng thái
docker-compose ps
```

!!! success "Kết quả"
    Sau khi hoàn tất, các service sẽ chạy tại:
    
    - **Backend API**: `http://localhost:8000`
    - **API Docs**: `http://localhost:8000/docs`
    - **Orion-LD**: `http://localhost:1026`

---

## Cài Đặt Chi Tiết

### Backend Service

=== "Windows"

    ```powershell
    # 1. Clone repository
    git clone https://github.com/HouHackathon-CQP/GreenMap-Backend.git
    cd GreenMap-Backend

    # 2. Tạo môi trường ảo
    python -m venv .venv
    .\.venv\Scripts\activate

    # 3. Cài đặt dependencies
    pip install -r requirements.txt

    # 4. Cấu hình môi trường
    cp env.example .env
    # Chỉnh sửa .env

    # 5. Khởi động Docker (DB + Broker)
    docker-compose up -d postgres mongo orion

    # 6. Chạy migrations và init data
    python setup_project.py

    # 7. Khởi động server
    uvicorn app.main:app --reload
    ```

=== "macOS/Linux"

    ```bash
    # 1. Clone repository
    git clone https://github.com/HouHackathon-CQP/GreenMap-Backend.git
    cd GreenMap-Backend

    # 2. Tạo môi trường ảo
    python3 -m venv .venv
    source .venv/bin/activate

    # 3. Cài đặt dependencies
    pip install -r requirements.txt

    # 4. Cấu hình môi trường
    cp env.example .env
    # Chỉnh sửa .env

    # 5. Khởi động Docker (DB + Broker)
    docker-compose up -d postgres mongo orion

    # 6. Chạy migrations và init data
    python setup_project.py

    # 7. Khởi động server
    uvicorn app.main:app --reload
    ```

### Frontend Portal

```bash
# 1. Clone repository
git clone https://github.com/HouHackathon-CQP/GreenMap-Frontend.git
cd GreenMap-Frontend

# 2. Cài đặt dependencies
npm install

# 3. Cấu hình môi trường
# Tạo file .env với nội dung:
# VITE_API_URL=http://localhost:8000
# VITE_MAPTILER_KEY=your_maptiler_key

# 4. Khởi động development server
npm run dev
```

!!! info "MapTiler API Key"
    Để sử dụng bản đồ, bạn cần đăng ký tài khoản miễn phí tại [MapTiler](https://www.maptiler.com/) để lấy API Key.

### Mobile App

1. **Mở Android Studio** và chọn "Open" → Chọn thư mục `GreenMap-Mobile-App`

2. **Tạo file `local.properties`** trong thư mục gốc:
   ```properties
   sdk.dir=/path/to/Android/sdk
   MAPTILER_API_KEY=your_maptiler_key
   API_BASE_URL=http://10.0.2.2:8000/
   ```

3. **Sync Gradle** và chờ download dependencies

4. **Chạy ứng dụng** trên Emulator hoặc thiết bị thật

---

## Cấu Hình Môi Trường (.env)

Tạo file `.env` với các biến sau:

```ini
# Database
DATABASE_URL="postgresql+asyncpg://admin:password@localhost:5432/greenmap_db"

# Security
SECRET_KEY="your-super-secret-key-at-least-32-characters"
ALGORITHM="HS256"
ACCESS_TOKEN_EXPIRE_MINUTES=30

# Admin Account
FIRST_SUPERUSER="admin@greenmap.hanoi"
FIRST_SUPERUSER_PASSWORD="your-admin-password"

# Context Broker
ORION_BROKER_URL="http://localhost:1026"

# External APIs
OPENAQ_API_KEY="your-openaq-key"
```

---

## Xác Minh Cài Đặt

Sau khi cài đặt, kiểm tra các endpoint sau:

| Service | URL | Expected |
|---------|-----|----------|
| Backend Health | `http://localhost:8000/api/system/health` | `{"status": "healthy"}` |
| API Docs | `http://localhost:8000/docs` | Swagger UI |
| Orion Version | `http://localhost:1026/version` | Version info JSON |
| Frontend | `http://localhost:5173` | Login page |
