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

# Bắt Đầu Nhanh

Hướng dẫn này sẽ giúp bạn chạy toàn bộ hệ thống GreenMap trên máy local sử dụng Docker Compose.

## 1. Clone Dự Án

```bash
git clone https://github.com/HouHackathon-CQP/GreenMap-Backend.git
git clone https://github.com/HouHackathon-CQP/GreenMap-Frontend.git
```

## 2. Khởi Chạy Backend & Services

```bash
cd GreenMap-Backend
docker-compose up -d
```

Lệnh này sẽ khởi động:
- FastAPI Backend
- PostgreSQL Database
- Orion-LD Context Broker
- MongoDB

## 3. Khởi Chạy Frontend

```bash
cd ../GreenMap-Frontend
npm install
npm run dev
```

## 4. Truy Cập

- **Admin Portal**: `http://localhost:5173`
- **Backend API Docs**: `http://localhost:8000/docs`
