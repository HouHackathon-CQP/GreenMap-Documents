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

# Backend Service

<div class="badge badge-primary">FastAPI</div>
<div class="badge badge-primary">PostgreSQL</div>
<div class="badge badge-primary">Orion-LD</div>
<div class="badge badge-secondary">Python 3.10+</div>

## Kiến Trúc

Backend được thiết kế theo mô hình **Clean Architecture** với các layer rõ ràng:

```
app/
├── api/            # Presentation Layer (Routes, Controllers)
│   ├── routes/     # API Endpoints
│   └── deps.py     # Dependencies (Auth, DB Session)
├── core/           # Configuration & Security
│   ├── config.py   # Settings management
│   └── security.py # JWT, Password hashing
├── crud/           # Data Access Layer
│   ├── user.py     # User CRUD operations
│   ├── report.py   # Report CRUD operations
│   └── location.py # Location CRUD operations
├── db/             # Database Setup
│   ├── base.py     # SQLAlchemy Base
│   └── session.py  # Database session
├── models/         # SQLAlchemy ORM Models
│   ├── user.py
│   └── report.py
├── schemas/        # Pydantic Schemas (Validation)
│   ├── user.py
│   └── report.py
├── services/       # Business Logic Layer
└── workers/        # Background Tasks
```

## API Endpoints Chính

### Authentication

```http
POST /login/access-token
Content-Type: application/x-www-form-urlencoded

username=admin@greenmap.hanoi&password=yourpassword
```

**Response:**
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "bearer"
}
```

### Users

| Method | Endpoint | Mô tả |
|--------|----------|-------|
| `GET` | `/users/me` | Lấy thông tin user hiện tại |
| `POST` | `/users/` | Tạo user mới |
| `GET` | `/users/` | Lấy danh sách users (Admin) |

### Reports

| Method | Endpoint | Mô tả |
|--------|----------|-------|
| `POST` | `/reports/` | Tạo báo cáo mới |
| `GET` | `/reports/` | Lấy danh sách báo cáo |
| `PUT` | `/reports/{id}` | Cập nhật trạng thái |

### Context Broker (Proxy)

| Method | Endpoint | Mô tả |
|--------|----------|-------|
| `GET` | `/ngsi-ld/v1/entities` | Truy vấn entities |
| `GET` | `/ngsi-ld/v1/entities/{id}` | Lấy entity theo ID |

## Data Agents

### AQI Agent (`aqi_agent.py`)

Thu thập dữ liệu chất lượng không khí từ OpenAQ:

```python
# Cấu hình
OPENAQ_API_KEY = os.getenv("OPENAQ_API_KEY")
UPDATE_INTERVAL = 900  # 15 phút

# Entity Type
NGSI_TYPE = "AirQualityObserved"
```

**Chạy agent:**
```bash
python aqi_agent.py
```

### Weather Agent (`weather_agent.py`)

Thu thập dữ liệu thời tiết từ OpenWeather:

```python
# Entity Type
NGSI_TYPE = "WeatherObserved"

# Dữ liệu thu thập
# - temperature
# - humidity
# - windSpeed
# - precipitation
```

## Database Schema

### Users Table

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    hashed_password VARCHAR(255) NOT NULL,
    full_name VARCHAR(255),
    role VARCHAR(50) DEFAULT 'citizen',
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT NOW()
);
```

### Reports Table

```sql
CREATE TABLE reports (
    id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    description TEXT,
    image_url VARCHAR(500),
    latitude FLOAT NOT NULL,
    longitude FLOAT NOT NULL,
    status VARCHAR(50) DEFAULT 'PENDING',
    user_id INTEGER REFERENCES users(id),
    created_at TIMESTAMP DEFAULT NOW()
);
```

## Testing

```bash
# Chạy tất cả tests
pytest

# Chạy với coverage
pytest --cov=app

# Chạy test cụ thể
pytest tests/test_users.py -v
```
