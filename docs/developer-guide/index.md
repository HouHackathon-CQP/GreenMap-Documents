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

# Tài Liệu Kỹ Thuật

Phần này dành cho các nhà phát triển muốn đóng góp hoặc tùy chỉnh hệ thống GreenMap. Bạn sẽ tìm thấy hướng dẫn chi tiết về kiến trúc, công nghệ và quy trình phát triển.

---

## Tổng Quan Kiến Trúc

GreenMap sử dụng kiến trúc **monorepo** với 4 repositories độc lập, mỗi repository có tech stack riêng biệt nhưng tương tác qua REST API chuẩn.

### Sơ Đồ Tổng Quan

**EXTERNAL DATA SOURCES**

- OpenStreetMap
- OpenAQ API
- Weather API
- SUMO Sim

↓

**GREENMAP BACKEND (FastAPI)**

- REST API Server
- Background Workers
- Database Management
- NGSI-LD Integration

↓

**CLIENT APPLICATIONS**

- Frontend (React)
- Mobile App (Kotlin)
- Context Broker (Orion-LD)

---

## Backend Development

### Tech Stack

#### Core Framework

- **FastAPI** - Modern Python web framework với async support
- **Uvicorn** - ASGI server cho production
- **Pydantic** - Data validation và serialization

#### Database

- **PostgreSQL 15+** - Relational database
- **PostGIS** - Spatial extension cho dữ liệu GIS
- **SQLAlchemy 2.0** - ORM với async support
- **Alembic** - Database migration tool

#### Authentication & Security

- **python-jose** - JWT token generation
- **passlib** - Password hashing với bcrypt
- **python-multipart** - File upload support

#### Background Tasks

- **APScheduler** - Job scheduling cho workers
- **httpx** - Async HTTP client

#### IoT Integration

- **Orion-LD Context Broker** - NGSI-LD standard
- **MongoDB** - Storage cho Orion-LD

### Project Structure

```
GreenMap-Backend/
├── app/
│   ├── __init__.py
│   ├── main.py              # Application entry point
│   ├── api/                 # API routes
│   │   ├── api.py           # Main API router
│   │   ├── deps.py          # Dependencies (auth, db)
│   │   └── routes/          # Feature-based routes
│   │       ├── auth.py
│   │       ├── reports.py
│   │       ├── infrastructure.py
│   │       └── ...
│   ├── core/                # Core configuration
│   │   ├── config.py        # Settings management
│   │   └── security.py      # JWT & password utils
│   ├── crud/                # Database operations
│   │   ├── base.py
│   │   ├── user.py
│   │   └── ...
│   ├── db/                  # Database setup
│   │   ├── base.py
│   │   ├── session.py
│   │   └── init_db.py
│   ├── models/              # SQLAlchemy models
│   │   ├── user.py
│   │   ├── report.py
│   │   └── ...
│   ├── schemas/             # Pydantic schemas
│   │   ├── user.py
│   │   ├── report.py
│   │   └── ...
│   ├── services/            # Business logic
│   │   ├── map_service.py
│   │   ├── ai_service.py
│   │   └── ...
│   └── workers/             # Background workers
│       ├── aqi_worker.py
│       └── weather_worker.py
├── requirements.txt
├── .env.example
└── alembic/                 # Database migrations
```

### Ví Dụ: Tạo API Endpoint Mới

**1. Định nghĩa Model (SQLAlchemy):**

```python
# app/models/park.py
from sqlalchemy import Column, Integer, String, Float
from geoalchemy2 import Geometry
from app.db.base import Base

class Park(Base):
    __tablename__ = "parks"
    
    id = Column(Integer, primary_key=True, index=True)
    name = Column(String, nullable=False)
    address = Column(String)
    area_sqm = Column(Float)  # Diện tích m²
    location = Column(Geometry('POINT', srid=4326))
    description = Column(String)
```

**2. Định nghĩa Schema (Pydantic):**

```python
# app/schemas/park.py
from pydantic import BaseModel
from typing import Optional

class ParkBase(BaseModel):
    name: str
    address: Optional[str] = None
    area_sqm: Optional[float] = None
    description: Optional[str] = None

class ParkCreate(ParkBase):
    latitude: float
    longitude: float

class ParkResponse(ParkBase):
    id: int
    latitude: float
    longitude: float
    
    class Config:
        from_attributes = True
```

**3. CRUD Operations:**

```python
# app/crud/park.py
from sqlalchemy.orm import Session
from app.models.park import Park
from app.schemas.park import ParkCreate
from geoalchemy2.elements import WKTElement

def create_park(db: Session, park: ParkCreate) -> Park:
    point = WKTElement(f'POINT({park.longitude} {park.latitude})', srid=4326)
    db_park = Park(
        name=park.name,
        address=park.address,
        area_sqm=park.area_sqm,
        location=point,
        description=park.description
    )
    db.add(db_park)
    db.commit()
    db.refresh(db_park)
    return db_park

def get_parks(db: Session, skip: int = 0, limit: int = 100):
    return db.query(Park).offset(skip).limit(limit).all()
```

**4. API Route:**

```python
# app/api/routes/parks.py
from fastapi import APIRouter, Depends, HTTPException
from sqlalchemy.orm import Session
from app.api import deps
from app.crud import park as crud_park
from app.schemas.park import ParkCreate, ParkResponse

router = APIRouter()

@router.post("/", response_model=ParkResponse, status_code=201)
def create_park(
    park_in: ParkCreate,
    db: Session = Depends(deps.get_db),
    current_user = Depends(deps.get_current_admin_user)
):
    """Tạo công viên mới (Admin only)"""
    return crud_park.create_park(db, park_in)

@router.get("/", response_model=list[ParkResponse])
def list_parks(
    skip: int = 0,
    limit: int = 100,
    db: Session = Depends(deps.get_db)
):
    """Lấy danh sách công viên"""
    return crud_park.get_parks(db, skip, limit)
```

**5. Register Router:**

```python
# app/api/api.py
from fastapi import APIRouter
from app.api.routes import parks

api_router = APIRouter()
api_router.include_router(parks.router, prefix="/parks", tags=["Parks"])
```

### Database Migration

```bash
# Tạo migration mới
alembic revision --autogenerate -m "Add parks table"

# Xem SQL sẽ chạy
alembic upgrade head --sql

# Apply migration
alembic upgrade head

# Rollback
alembic downgrade -1
```

### Testing

```python
# tests/api/test_parks.py
from fastapi.testclient import TestClient
from app.main import app

client = TestClient(app)

def test_create_park(admin_token_headers):
    data = {
        "name": "Công viên Thống Nhất",
        "address": "Hai Bà Trưng, Hà Nội",
        "area_sqm": 50000,
        "latitude": 21.0167,
        "longitude": 105.8456
    }
    response = client.post(
        "/api/v1/parks/",
        json=data,
        headers=admin_token_headers
    )
    assert response.status_code == 201
    assert response.json()["name"] == data["name"]
```

### News RSS Service

**Fetch tin tức từ Hà Nội Mới:**

```python
# app/services/rss.py
import feedparser
from typing import List
from app import schemas

async def fetch_hanoimoi_rss(limit: int = 20) -> List[schemas.NewsItem]:
    """Fetch news from Hà Nội Mới RSS feed"""
    url = "https://hanoimoi.com.vn/rss/tin-moi-cap-nhat.rss"
    
    try:
        feed = feedparser.parse(url)
        items = []
        
        for entry in feed.entries[:limit]:
            items.append(schemas.NewsItem(
                title=entry.title,
                link=entry.link,
                description=entry.get("description", ""),
                published=entry.get("published", ""),
                author=entry.get("author", "Hà Nội Mới")
            ))
        
        return items
    except Exception as e:
        print(f"Error fetching RSS: {e}")
        return []
```

**API Route:**

```python
# app/api/routes/news.py
from fastapi import APIRouter, Query
from app.services import rss
from app import schemas

router = APIRouter(prefix="/news", tags=["news"])

@router.get("/hanoimoi", response_model=list[schemas.NewsItem])
async def get_hanoimoi_news(
    limit: int = Query(20, ge=1, le=50)
):
    """Lấy tin tức mới nhất từ Hà Nội Mới"""
    return await rss.fetch_hanoimoi_rss(limit)
```

### Traffic Simulation Service

**Real-time traffic từ SUMO simulation:**

```python
# app/api/routes/traffic.py
import time
from fastapi import APIRouter, Depends
from sqlalchemy.ext.asyncio import AsyncSession
from app.db.session import get_db

router = APIRouter(prefix="/traffic", tags=["traffic"])

LOOP_DURATION = 3600  # 1 hour loop
DATA_INTERVAL = 10    # 10 seconds

@router.get("/segments")
async def get_traffic_segments(db: AsyncSession = Depends(get_db)):
    """Lấy GeoJSON của tất cả đoạn đường"""
    query = """
        SELECT id, ST_AsGeoJSON(ST_Simplify(geom, 0.0001), 6) as geometry
        FROM traffic_segments
    """
    result = await db.execute(text(query))
    
    features = []
    for row in result.mappings():
        features.append({
            "type": "Feature",
            "id": str(row.id),
            "geometry": json.loads(row.geometry),
            "properties": {"id": str(row.id), "name": f"Đoạn đường {row.id}"}
        })
    
    return {"type": "FeatureCollection", "features": features}

@router.get("/live")
async def get_live_traffic_status(db: AsyncSession = Depends(get_db)):
    """Lấy trạng thái giao thông realtime (vòng lặp 1h)"""
    raw_second = int(time.time() - START_TIME_REF) % LOOP_DURATION
    query_second = (raw_second // DATA_INTERVAL) * DATA_INTERVAL
    
    query = """
        SELECT segment_id, status_color
        FROM simulation_frames
        WHERE time_second = :sec
    """
    result = await db.execute(text(query), {"sec": query_second})
    
    return {
        "time_real": raw_second,
        "time_query": query_second,
        "status": {str(r.segment_id): r.status_color for r in result}
    }
```

### AI Insights Service

**Phân tích thời tiết + AQI bằng Gemini/Groq:**

```python
# app/services/ai_insights.py
import google.generativeai as genai
from groq import Groq
from app.core.config import settings

async def generate_ai_insight(
    lat: float,
    lon: float,
    provider: str = "auto",
    model_override: str | None = None
) -> dict:
    """
    Phân tích thời tiết 24h/7 ngày + AQI bằng AI
    """
    # 1. Fetch weather data from OpenWeatherMap
    weather_data = await fetch_weather(lat, lon)
    
    # 2. Fetch AQI data from OpenAQ
    aqi_data = await fetch_aqi(lat, lon)
    
    # 3. Generate prompt
    prompt = f"""
    Phân tích thời tiết và chất lượng không khí cho khu vực:
    
    **Thời tiết hiện tại:**
    - Nhiệt độ: {weather_data['current']['temp']}°C
    - Độ ẩm: {weather_data['current']['humidity']}%
    - AQI: {aqi_data['aqi']} ({aqi_data['category']})
    
    Hãy đưa ra lời khuyên cho các hoạt động: đi bộ, chạy bộ, xe đạp.
    """
    
    # 4. Call AI (Gemini or Groq)
    if provider == "gemini":
        genai.configure(api_key=settings.GEMINI_API_KEY)
        model = genai.GenerativeModel(model_override or "gemini-1.5-flash")
        response = model.generate_content(prompt)
        analysis = response.text
    elif provider == "groq":
        client = Groq(api_key=settings.GROQ_API_KEY)
        response = client.chat.completions.create(
            model=model_override or "llama-3.3-70b-versatile",
            messages=[{"role": "user", "content": prompt}]
        )
        analysis = response.choices[0].message.content
    
    return {
        "provider": provider,
        "model": model_override or "default",
        "analysis": analysis,
        "context": {"weather": weather_data, "aqi": aqi_data}
    }
```

**API Route:**

```python
# app/api/routes/ai.py
from fastapi import APIRouter, Depends, Query
from app.services.ai_insights import generate_ai_insight
from app import models, schemas
from app.db.session import get_db

router = APIRouter(prefix="/ai", tags=["ai"])

@router.post("/weather-insights", response_model=schemas.AIReportRead)
async def get_ai_weather_insights(
    lat: float = Query(21.0285),
    lon: float = Query(105.8542),
    provider: str = Query("auto"),
    model: str | None = Query(None),
    db: AsyncSession = Depends(get_db),
    current_user: models.User = Depends(get_current_user)
):
    """Phân tích AI cho thời tiết + AQI"""
    ai_result = await generate_ai_insight(lat, lon, provider, model)
    
    # Save to database
    saved = await crud.create_ai_report(
        db=db,
        provider=ai_result["provider"],
        model=ai_result["model"],
        lat=lat,
        lon=lon,
        analysis=ai_result["analysis"],
        context=ai_result["context"],
        user_id=current_user.id
    )
    
    return saved
```

### Firebase Notifications Service

**Push notification đến mobile apps:**

```python
# app/services/firebase_messaging.py
from firebase_admin import messaging, initialize_app, credentials
from app.core.config import settings

# Initialize Firebase
cred = credentials.Certificate(settings.FIREBASE_CREDENTIALS_PATH)
initialize_app(cred)

async def send_notification_to_all(
    title: str,
    body: str,
    data: dict = None,
    dry_run: bool = False
) -> dict:
    """Gửi notification đến tất cả device tokens"""
    from app import crud
    from app.db.session import async_session
    
    async with async_session() as db:
        tokens = await crud.get_all_device_tokens(db)
    
    if not tokens:
        return {"success": 0, "failure": 0}
    
    message = messaging.MulticastMessage(
        notification=messaging.Notification(title=title, body=body),
        data=data or {},
        tokens=[t.device_token for t in tokens]
    )
    
    response = messaging.send_multicast(message, dry_run=dry_run)
    
    return {
        "success_count": response.success_count,
        "failure_count": response.failure_count,
        "responses": response.responses
    }

async def send_topic_notification(
    title: str,
    body: str,
    topic: str = "greenmap_all",
    data: dict = None,
    dry_run: bool = False
) -> dict:
    """Gửi notification đến Firebase topic"""
    message = messaging.Message(
        notification=messaging.Notification(title=title, body=body),
        data=data or {},
        topic=topic
    )
    
    response = messaging.send(message, dry_run=dry_run)
    return {"message_id": response}
```

**API Route:**

```python
# app/api/routes/notifications.py
from fastapi import APIRouter, Depends
from app.services import firebase_messaging
from app import schemas, models
from app.api.deps import get_current_admin

router = APIRouter(prefix="/notifications", tags=["notifications"])

@router.post("/send")
async def send_notification(
    payload: schemas.NotificationSend,
    current_user: models.User = Depends(get_current_admin)
):
    """Gửi notification đến tất cả devices (Admin only)"""
    result = await firebase_messaging.send_notification_to_all(
        title=payload.title,
        body=payload.body,
        data=payload.data,
        dry_run=payload.dry_run
    )
    
    # Save to history
    await crud.create_notification_log(db, payload, result)
    
    return result
```

[Xem thêm chi tiết Backend →](backend/)

---

## Frontend Development

### Tech Stack

#### Core

- **React 18** - UI library với hooks
- **Vite** - Build tool cực nhanh
- **TypeScript** - Type-safe JavaScript

#### State Management

- **TanStack Query** - Server state management
- **Zustand** - Client state management

#### Routing

- **React Router v6** - Client-side routing

#### Styling

- **Tailwind CSS** - Utility-first CSS
- **Headless UI** - Unstyled accessible components

#### Maps

- **MapLibre GL JS** - Interactive maps
- **@maplibre/maplibre-gl-geocoder** - Search

#### HTTP Client

- **Axios** - Promise-based HTTP

#### Form Handling

- **React Hook Form** - Form state management
- **Zod** - Schema validation

### Project Structure

```
GreenMap-Frontend/
├── src/
│   ├── main.jsx             # Entry point
│   ├── App.jsx              # Root component
│   ├── assets/              # Static assets
│   ├── components/          # Reusable components
│   │   ├── common/          # Button, Input, Card...
│   │   ├── layout/          # Header, Sidebar, Footer
│   │   └── maps/            # Map-related components
│   ├── pages/               # Page components
│   │   ├── Dashboard.jsx
│   │   ├── MapView.jsx
│   │   ├── Reports.jsx
│   │   └── ...
│   ├── services/            # API services
│   │   ├── api.js           # Axios instance
│   │   ├── authService.js
│   │   └── reportService.js
│   ├── hooks/               # Custom React hooks
│   │   ├── useAuth.js
│   │   ├── useMap.js
│   │   └── ...
│   ├── utils/               # Helper functions
│   ├── context/             # React Context
│   └── types/               # TypeScript types
├── public/
├── index.html
├── vite.config.js
├── tailwind.config.js
└── package.json
```

### Ví Dụ: Component với MapLibre

```jsx
// src/components/maps/ParkMap.jsx
import { useEffect, useRef, useState } from 'react';
import maplibregl from 'maplibre-gl';
import 'maplibre-gl/dist/maplibre-gl.css';
import { useQuery } from '@tanstack/react-query';
import { getParks } from '@/services/parkService';

export function ParkMap() {
  const mapContainer = useRef(null);
  const map = useRef(null);
  const [lng, setLng] = useState(105.8342);
  const [lat, setLat] = useState(21.0278);
  const [zoom, setZoom] = useState(12);

  const { data: parks } = useQuery({
    queryKey: ['parks'],
    queryFn: getParks
  });

  useEffect(() => {
    if (map.current) return;

    map.current = new maplibregl.Map({
      container: mapContainer.current,
      style: 'https://basemaps.cartocdn.com/gl/positron-gl-style/style.json',
      center: [lng, lat],
      zoom: zoom
    });

    map.current.addControl(new maplibregl.NavigationControl());
  }, []);

  useEffect(() => {
    if (!map.current || !parks) return;

    // Add parks as markers
    parks.forEach(park => {
      new maplibregl.Marker({ color: '#10b981' })
        .setLngLat([park.longitude, park.latitude])
        .setPopup(
          new maplibregl.Popup().setHTML(`
            <h3 class="font-bold">${park.name}</h3>
            <p class="text-sm">${park.address}</p>
            <p class="text-xs text-gray-500">${park.area_sqm} m²</p>
          `)
        )
        .addTo(map.current);
    });
  }, [parks]);

  return (
    <div className="relative w-full h-screen">
      <div ref={mapContainer} className="absolute inset-0" />
    </div>
  );
}
```

### News Service

**Fetch tin tức từ Backend:**

```javascript
// src/services/newsService.js
import { apiFetch } from './apiClient';

export const fetchNews = async () => {
  try {
    const data = await apiFetch('news/hanoimoi?limit=20');
    return Array.isArray(data) ? data : [];
  } catch (error) {
    console.error("Failed to fetch news:", error);
    return [];
  }
};
```

**News Feed Page:**

```jsx
// src/pages/NewsFeed.jsx
import React, { useEffect, useState } from 'react';
import { fetchNews } from '../services/newsService';
import { Newspaper, ExternalLink, Loader2 } from 'lucide-react';

export default function NewsFeed() {
  const [news, setNews] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    const loadNews = async () => {
      setLoading(true);
      const data = await fetchNews();
      setNews(data);
      setLoading(false);
    };
    loadNews();
  }, []);

  if (loading) {
    return (
      <div className="flex items-center justify-center h-64">
        <Loader2 className="animate-spin text-emerald-500" size={32} />
      </div>
    );
  }

  return (
    <div className="space-y-4">
      <h1 className="text-2xl font-bold flex items-center gap-2">
        <Newspaper className="text-emerald-500" />
        Tin Tức Môi Trường
      </h1>
      
      <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
        {news.map((item, index) => (
          <a
            key={index}
            href={item.link}
            target="_blank"
            rel="noopener noreferrer"
            className="p-4 bg-white dark:bg-gray-800 rounded-lg shadow hover:shadow-lg transition-shadow"
          >
            <h3 className="font-semibold text-lg mb-2 line-clamp-2">
              {item.title}
            </h3>
            <p className="text-sm text-gray-600 dark:text-gray-400 line-clamp-3 mb-2">
              {item.description}
            </p>
            <div className="flex items-center justify-between text-xs text-gray-500">
              <span>{new Date(item.published).toLocaleDateString('vi-VN')}</span>
              <ExternalLink size={14} />
            </div>
          </a>
        ))}
      </div>
    </div>
  );
}
```

### Traffic Service

**Fetch traffic data với caching:**

```javascript
// src/services/trafficService.js
import { apiFetch } from './apiClient';

const TRAFFIC_MAP_CACHE_KEY = 'greenmap_traffic_map_cache';
const TRAFFIC_MAP_TTL = 5 * 60 * 1000; // 5 minutes

export const fetchTrafficMap = async (forceRefresh = false) => {
  const now = Date.now();
  const cached = localStorage.getItem(TRAFFIC_MAP_CACHE_KEY);
  
  if (!forceRefresh && cached) {
    try {
      const parsed = JSON.parse(cached);
      if (now - parsed.timestamp < TRAFFIC_MAP_TTL) {
        return parsed.data;
      }
    } catch {
      localStorage.removeItem(TRAFFIC_MAP_CACHE_KEY);
    }
  }

  const geojsonData = await apiFetch('traffic/segments');
  localStorage.setItem(TRAFFIC_MAP_CACHE_KEY, JSON.stringify({ 
    data: geojsonData, 
    timestamp: now 
  }));
  
  return geojsonData;
};

export const fetchTrafficStatus = async () => {
  return await apiFetch('traffic/live');
};
```

**Traffic Layer Integration:**

```jsx
// Integration vào AirQualityMap.jsx
import { fetchTrafficMap, fetchTrafficStatus } from '../services/trafficService';

// Add traffic layer to map
useEffect(() => {
  if (!map || !showTraffic) return;

  const loadTraffic = async () => {
    const segments = await fetchTrafficMap();
    
    if (!map.getSource('traffic-segments')) {
      map.addSource('traffic-segments', {
        type: 'geojson',
        data: segments
      });

      map.addLayer({
        id: 'traffic-lines',
        type: 'line',
        source: 'traffic-segments',
        paint: {
          'line-color': ['case',
            ['==', ['get', 'status'], 'green'], '#10b981',
            ['==', ['get', 'status'], 'yellow'], '#f59e0b',
            ['==', ['get', 'status'], 'red'], '#ef4444',
            '#6b7280'
          ],
          'line-width': 4
        }
      });
    }

    // Update every 10s
    const interval = setInterval(async () => {
      const status = await fetchTrafficStatus();
      segments.features.forEach(f => {
        f.properties.status = status.status[f.properties.id] || 'gray';
      });
      map.getSource('traffic-segments').setData(segments);
    }, 10000);

    return () => clearInterval(interval);
  };

  loadTraffic();
}, [map, showTraffic]);
```

### Notification Service

```javascript
// src/services/notificationService.js
import { apiFetch } from './apiClient';

export const sendNotification = async (payload) => {
  return apiFetch('notifications/send', {
    method: 'POST',
    body: JSON.stringify(payload)
  });
};

export const sendTopicNotification = async (payload) => {
  return apiFetch('notifications/send/topic', {
    method: 'POST',
    body: JSON.stringify(payload)
  });
};

export const getNotificationHistory = async (skip = 0, limit = 20) => {
  return apiFetch(`notifications/history?skip=${skip}&limit=${limit}`);
};

export const getAIWeatherInsights = async (params) => {
  const query = new URLSearchParams(params).toString();
  return apiFetch(`ai/weather-insights?${query}`, { method: 'POST' });
};
```

**Notification Page với AI Integration:**

```jsx
// src/pages/Notification.jsx (simplified)
import { useState } from 'react';
import { sendNotification, getAIWeatherInsights } from '../services';

export default function Notification() {
  const [formData, setFormData] = useState({
    title: '',
    body: '',
    dry_run: false
  });
  
  const [loading, setLoading] = useState(false);

  const generateAIContent = async () => {
    const result = await getAIWeatherInsights({
      lat: 21.0285,
      lon: 105.8542,
      provider: 'auto'
    });
    
    setFormData({
      ...formData,
      title: 'Phân tích Thời tiết & AQI',
      body: result.analysis
    });
  };

  const handleSend = async () => {
    setLoading(true);
    try {
      await sendNotification(formData);
      alert('Sent successfully!');
    } finally {
      setLoading(false);
    }
  };

  return (
    <div className="space-y-4">
      <input
        value={formData.title}
        onChange={(e) => setFormData({...formData, title: e.target.value})}
        placeholder="Title"
      />
      <textarea
        value={formData.body}
        onChange={(e) => setFormData({...formData, body: e.target.value})}
        placeholder="Body"
      />
      <button onClick={generateAIContent}>Generate AI Content</button>
      <button onClick={handleSend} disabled={loading}>Send</button>
    </div>
  );
}
```

### State Management với Zustand

```javascript
// src/stores/authStore.js
import { create } from 'zustand';
import { persist } from 'zustand/middleware';

export const useAuthStore = create(
  persist(
    (set, get) => ({
      user: null,
      token: null,
      
      setAuth: (user, token) => set({ user, token }),
      
      logout: () => set({ user: null, token: null }),
      
      isAuthenticated: () => !!get().token,
      
      isAdmin: () => get().user?.role === 'admin'
    }),
    {
      name: 'auth-storage'
    }
  )
);
```

[Xem thêm chi tiết Frontend →](frontend/)

---

## Mobile Development

### Tech Stack

#### Language & Framework

- **Kotlin** - Modern JVM language
- **Jetpack Compose** - Declarative UI toolkit
- **Coroutines & Flow** - Async programming

#### Architecture

- **MVI (Model-View-Intent)** - Unidirectional data flow
- **Clean Architecture** - Separation of concerns

#### Networking

- **Ktor Client** - HTTP client
- **Kotlinx Serialization** - JSON parsing

#### Database

- **Room** - SQLite wrapper
- **DataStore** - Key-value storage

#### Maps

- **Mapbox Maps SDK** - Interactive maps
- **Google Location Services** - GPS

#### Image Loading

- **Coil** - Image loading library

#### Dependency Injection

- **Koin** - Lightweight DI

### Project Structure

```
GreenMap-Mobile-App/
└── app/src/main/java/vn/greenmap/
    ├── MainActivity.kt
    ├── GreenMapApplication.kt
    ├── di/                  # Dependency injection
    │   ├── NetworkModule.kt
    │   └── RepositoryModule.kt
    ├── data/                # Data layer
    │   ├── local/           # Room database
    │   ├── remote/          # API services
    │   └── repository/      # Repository implementations
    ├── domain/              # Domain layer
    │   ├── model/           # Domain models
    │   ├── repository/      # Repository interfaces
    │   └── usecase/         # Business logic
    ├── presentation/        # Presentation layer
    │   ├── navigation/
    │   ├── screens/
    │   │   ├── home/
    │   │   ├── map/
    │   │   ├── report/
    │   │   └── profile/
    │   ├── components/      # Reusable Composables
    │   └── theme/           # Material 3 theme
    └── util/                # Utilities
```

### Ví Dụ: Screen với Compose

```kotlin
// presentation/screens/report/CreateReportScreen.kt
@Composable
fun CreateReportScreen(
    viewModel: ReportViewModel = koinViewModel(),
    onNavigateBack: () -> Unit
) {
    val state by viewModel.state.collectAsState()
    
    Scaffold(
        topBar = {
            TopAppBar(
                title = { Text("Báo Cáo Vấn Đề") },
                navigationIcon = {
                    IconButton(onClick = onNavigateBack) {
                        Icon(Icons.Default.ArrowBack, "Back")
                    }
                }
            )
        }
    ) { padding ->
        Column(
            modifier = Modifier
                .fillMaxSize()
                .padding(padding)
                .padding(16.dp)
        ) {
            OutlinedTextField(
                value = state.title,
                onValueChange = { viewModel.onTitleChange(it) },
                label = { Text("Tiêu đề") },
                modifier = Modifier.fillMaxWidth()
            )
            
            Spacer(modifier = Modifier.height(16.dp))
            
            OutlinedTextField(
                value = state.description,
                onValueChange = { viewModel.onDescriptionChange(it) },
                label = { Text("Mô tả chi tiết") },
                modifier = Modifier
                    .fillMaxWidth()
                    .height(120.dp),
                maxLines = 5
            )
            
            Spacer(modifier = Modifier.height(16.dp))
            
            // Category selection
            CategorySelector(
                selected = state.category,
                onSelect = { viewModel.onCategoryChange(it) }
            )
            
            Spacer(modifier = Modifier.height(16.dp))
            
            // Image picker
            ImagePickerButton(
                images = state.images,
                onImagesSelected = { viewModel.onImagesSelected(it) }
            )
            
            Spacer(modifier = Modifier.weight(1f))
            
            Button(
                onClick = { viewModel.submitReport() },
                modifier = Modifier.fillMaxWidth(),
                enabled = state.isValid && !state.isLoading
            ) {
                if (state.isLoading) {
                    CircularProgressIndicator(
                        modifier = Modifier.size(24.dp),
                        color = MaterialTheme.colorScheme.onPrimary
                    )
                } else {
                    Text("Gửi Báo Cáo")
                }
            }
        }
    }
}
```

[Xem thêm chi tiết Mobile →](mobile/)

---

## Data Pipeline

### Data Sources

#### OpenStreetMap

- Overpass API để query dữ liệu địa lý
- Import công viên, trạm sạc, điểm du lịch
- Định kỳ cập nhật mỗi tuần

#### OpenAQ

- Realtime air quality data
- Fetch mỗi 15 phút
- Lưu vào PostgreSQL + sync Orion-LD

#### Weather API

- OpenWeatherMap
- Current weather + 5-day forecast
- Update mỗi 30 phút

#### SUMO Simulation

- Traffic simulation data
- Vehicle density, speed, emissions
- Export XML → parse → PostgreSQL

### ETL Scripts

```python
# import_osm.py - Import POI từ OpenStreetMap
import overpy
from app.db.session import SessionLocal
from app.models.park import Park
from geoalchemy2.elements import WKTElement

api = overpy.Overpass()

query = """
[out:json];
area[name="Hà Nội"]->.hanoi;
(
  node["leisure"="park"](area.hanoi);
  way["leisure"="park"](area.hanoi);
);
out center;
"""

result = api.query(query)
db = SessionLocal()

for elem in result.nodes + result.ways:
    if hasattr(elem, 'center'):
        lat, lon = elem.center.lat, elem.center.lon
    else:
        lat, lon = elem.lat, elem.lon
    
    park = Park(
        osm_id=elem.id,
        name=elem.tags.get("name", "Unknown"),
        location=WKTElement(f'POINT({lon} {lat})', srid=4326)
    )
    db.add(park)

db.commit()
```

[Xem thêm chi tiết Data Pipeline →](data/)

## Quy Ước Chung

### Git Workflow

Chúng tôi sử dụng **GitHub Flow**:

1. Tạo branch từ `main`: `git checkout -b feature/ten-tinh-nang`
2. Commit thay đổi với message rõ ràng
3. Tạo Pull Request để review
4. Merge sau khi được approve

### Commit Message Convention

```
<type>(<scope>): <description>

[optional body]
[optional footer]
```

**Types:**

- `feat`: Tính năng mới
- `fix`: Sửa lỗi
- `docs`: Cập nhật tài liệu
- `style`: Format code (không ảnh hưởng logic)
- `refactor`: Refactor code
- `test`: Thêm/sửa test
- `chore`: Công việc bảo trì

**Ví dụ:**
```
feat(map): add traffic layer to map view
fix(auth): resolve JWT expiration issue
docs(api): update authentication endpoints
```

### Code Style

| Ngôn ngữ | Style Guide | Linter |
|----------|-------------|--------|
| Python | PEP 8 | flake8, black |
| JavaScript/React | Airbnb | ESLint |
| Kotlin | Kotlin Coding Conventions | ktlint |
