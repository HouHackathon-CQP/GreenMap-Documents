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

---

## Yêu Cầu Tiên Quyết

Đảm bảo máy bạn đã cài đặt các công cụ sau:

- **Docker Desktop** (bắt buộc cho backend)
- **Python 3.10+**
- **Node.js 18+** (cho frontend)
- **Android Studio Hedgehog+** (cho mobile)
- **Git**

---

## 🔧 Backend Setup

### 1. Clone Repository

```bash
git clone https://github.com/HouHackathon-CQP/GreenMap-Backend.git
cd GreenMap-Backend
```

### 2. Tạo Virtual Environment

**Windows:**
```bash
python -m venv .venv
.\.venv\Scripts\activate
```

**macOS/Linux:**
```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Cài Đặt Dependencies

```bash
pip install -r requirements.txt
```

### 4. Cấu Hình Environment

Tạo file `.env` tại thư mục gốc:

```env
# Database & Authentication
DATABASE_URL="postgresql+asyncpg://admin:mysecretpassword@127.0.0.1:5432/greenmap_db"
SECRET_KEY="your_secret_key_here_64_chars"
ALGORITHM="HS256"
ACCESS_TOKEN_EXPIRE_MINUTES=30

# CORS Configuration
CORS_ORIGINS="http://localhost:3000"

# Admin Account
FIRST_SUPERUSER="admin@greenmap.hanoi"
FIRST_SUPERUSER_PASSWORD="123456"

# External APIs
OPENAQ_API_KEY="your_openaq_api_key"
ORION_BROKER_URL="http://localhost:1026"

# NGSI-LD config
NGSI_CONTEXT_URL=https://raw.githubusercontent.com/smart-data-models/dataModel.Environment/master/context.jsonld
NGSI_TYPE_AQI=https://smartdatamodels.org/dataModel.Environment/AirQualityObserved
NGSI_TYPE_WEATHER=https://smartdatamodels.org/dataModel.Environment/WeatherObserved

# Firebase push notification
FIREBASE_CREDENTIALS_FILE="/path/to/firebase-service-account.json"
FIREBASE_DEFAULT_TOPIC="greenmap-daily"

# Daily notification schedule (local server time)
DAILY_PUSH_HOUR=7
DAILY_PUSH_MINUTE=0
DAILY_PUSH_TITLE="Bản đồ Xanh - Cập nhật môi trường mỗi ngày"
DAILY_PUSH_BODY="Mở ứng dụng để xem dự báo thời tiết và chất lượng không khí hôm nay."

# AI APIs (Optional)
GEMINI_API_KEY="your_gemini_api_key"
GROQ_API_KEY="your_groq_api_key"
```

### 5. Khởi Động Docker

```bash
docker-compose up -d
```

⏳ **Chờ 10-15 giây** để các container khởi động hoàn toàn.

### 6. Khởi Tạo Dữ Liệu

Chạy lệnh sau để tự động khởi tạo:

```bash
python setup_project.py
```

Hoặc chạy từng bước (dễ debug hơn):

```bash
# Nối file dữ liệu JSON
python Data/merge_json.py

# Tạo tất cả bảng database
python init_db.py

# Đăng ký thiết bị cảm biến
python seed_sensor.py

# Nạp dữ liệu bản đồ
python import_osm.py 
python sync_to_orion.py

# Xử lý dữ liệu giao thông
python process_simulation.py
```

### 7. Chạy Backend

Mở **4 terminal riêng biệt**:

**Terminal 1: API Backend**
```bash
python main.py
```
- Server URL: http://127.0.0.1:8000
- API Docs: http://127.0.0.1:8000/docs

**Terminal 2: AQI Agent** (Cập nhật dữ liệu realtime)
```bash
python aqi_agent.py
```

**Terminal 3: Weather Agent** (Cập nhật dữ liệu realtime)
```bash
python weather_agent.py
```

**Terminal 4: Daily Notification Job** (Firebase push)
```bash
python notification_job.py
```

!!! success "Backend đã sẵn sàng"
    Truy cập http://localhost:8000/docs để xem API documentation

---

## 🎨 Frontend Setup

### 1. Clone Repository

```bash
git clone https://github.com/HouHackathon-CQP/GreenMap-Frontend.git
cd GreenMap-Frontend
```

### 2. Cài Đặt Dependencies

```bash
npm install
```

### 3. Cấu Hình Environment

Tạo file `.env` tại thư mục gốc:

```env
VITE_API_BASE_URL=http://localhost:8000
```

### 4. Khởi Chạy

```bash
npm run dev
```

Truy cập: **http://localhost:5173** 🎉

**Tài khoản admin mặc định:**
- Email: `admin@greenmap.hanoi`
- Password: `123456`

---

## 📱 Mobile App Setup

### 1. Clone Repository

```bash
git clone https://github.com/HouHackathon-CQP/GreenMap-Mobile-App.git
```

### 2. Mở Bằng Android Studio

Chọn **File → Open** → Chọn thư mục `GreenMap-Mobile-App`

### 3. Cấu Hình local.properties

Tạo file `local.properties` trong thư mục gốc:

```properties
sdk.dir=C:\\Users\\YourName\\AppData\\Local\\Android\\sdk
MAPTILER_API_KEY=your_maptiler_key_here
API_BASE_URL=http://10.0.2.2:8000/
```

!!! tip "Emulator IP"
    Sử dụng `10.0.2.2` để truy cập localhost từ Android Emulator

### 4. Sync & Build

1. Chọn **File → Sync Project with Gradle Files**
2. Chờ Gradle download dependencies
3. Chọn **Run → Run 'app'**

---

## 📊 Data Processing Setup

### 1. Clone Repository

```bash
git clone https://github.com/HouHackathon-CQP/GreenMap-Data.git
cd GreenMap-Data
```

### 2. Tạo Virtual Environment

```bash
python -m venv .venv
.\.venv\Scripts\activate  # Windows
# source .venv/bin/activate  # macOS/Linux
```

### 3. Cài Đặt Dependencies

```bash
pip install jupyter geopandas pandas shapely matplotlib
```

### 4. Khởi Động Jupyter

```bash
jupyter notebook
```

Mở file: `data_collection.ipynb`

---

## ✅ Xác Minh Cài Đặt

Sau khi cài đặt, kiểm tra các endpoint sau:

| Service | URL | Expected Response |
|---------|-----|-------------------|
| **Backend API** | http://localhost:8000 | `{"message": "GreenMap API"}` |
| **API Docs** | http://localhost:8000/docs | Swagger UI |
| **Orion-LD** | http://localhost:1026/version | Version info JSON |
| **Frontend** | http://localhost:5173 | Login page |
| **PostgreSQL** | localhost:5432 | Connected via psql |
| **MongoDB** | localhost:27017 | Connected via mongo shell |

### Test API Endpoints

```bash
# Backend health check
curl http://localhost:8000/

# Get AQI data
curl http://localhost:8000/aqi/hanoi?limit=10

# Get weather data
curl http://localhost:8000/weather/hanoi?limit=10

# Get locations
curl http://localhost:8000/locations?location_type=PUBLIC_PARK&limit=10

# Get news
curl http://localhost:8000/news/hanoimoi?limit=20

# Get traffic segments
curl http://localhost:8000/traffic/segments

# Orion-LD entities
curl http://localhost:1026/ngsi-ld/v1/entities?limit=10
```

---

## 🐳 Docker Services

Các container được khởi động bởi `docker-compose up -d`:

| Service | Port | Description |
|---------|------|-------------|
| **PostgreSQL** | 5432 | Database chính |
| **MongoDB** | 27017 | Context Broker database |
| **Orion-LD** | 1026 | FIWARE Context Broker |

### Quản lý Docker

```bash
# Xem logs
docker-compose logs -f

# Xem trạng thái
docker-compose ps

# Dừng services
docker-compose down

# Xóa volumes (reset data)
docker-compose down -v

# Rebuild images
docker-compose build --no-cache
docker-compose up -d
```
