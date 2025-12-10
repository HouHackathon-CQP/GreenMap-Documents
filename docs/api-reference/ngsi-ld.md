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

# NGSI-LD API

GreenMap sử dụng Orion-LD Context Broker để quản lý dữ liệu ngữ cảnh theo tiêu chuẩn NGSI-LD.

## Overview

NGSI-LD là tiêu chuẩn của ETSI cho dữ liệu ngữ cảnh (context data), được thiết kế cho các ứng dụng IoT và Smart City.

## Base URL

```
http://localhost:1026/ngsi-ld/v1
```

## Required Headers

```http
Accept: application/ld+json
Content-Type: application/ld+json
Link: <https://raw.githubusercontent.com/smart-data-models/dataModel.Environment/master/context.jsonld>; rel="http://www.w3.org/ns/ldp#context"; type="application/ld+json"
```

---

## Entities

### Query Entities

```http
GET /ngsi-ld/v1/entities
```

**Query Parameters:**

| Param | Type | Description |
|-------|------|-------------|
| type | string | Filter by entity type |
| q | string | Query expression |
| georel | string | Geo-relationship (near, within, etc.) |
| geometry | string | Geometry type (Point, Polygon) |
| coordinates | string | Coordinates array |
| geoproperty | string | Property to use for geo query |

**Example - Get all AQI stations:**
```http
GET /ngsi-ld/v1/entities?type=AirQualityObserved
```

**Example - Geo query (within 5km):**
```http
GET /ngsi-ld/v1/entities?type=AirQualityObserved&georel=near;maxDistance==5000&geometry=Point&coordinates=[105.8542,21.0285]
```

### Get Entity by ID

```http
GET /ngsi-ld/v1/entities/{entityId}
```

**Example:**
```http
GET /ngsi-ld/v1/entities/urn:ngsi-ld:AirQualityObserved:HN-001
```

**Response:**
```json
{
  "@context": "https://uri.etsi.org/ngsi-ld/v1/ngsi-ld-core-context.jsonld",
  "id": "urn:ngsi-ld:AirQualityObserved:HN-001",
  "type": "AirQualityObserved",
  "location": {
    "type": "GeoProperty",
    "value": {
      "type": "Point",
      "coordinates": [105.8542, 21.0285]
    }
  },
  "airQualityIndex": {
    "type": "Property",
    "value": 85
  },
  "dateObserved": {
    "type": "Property",
    "value": "2025-12-10T14:30:00Z"
  }
}
```

### Create Entity

```http
POST /ngsi-ld/v1/entities
Content-Type: application/ld+json
```

**Request Body:**
```json
{
  "@context": [
    "https://raw.githubusercontent.com/smart-data-models/dataModel.Environment/master/context.jsonld"
  ],
  "id": "urn:ngsi-ld:AirQualityObserved:HN-002",
  "type": "AirQualityObserved",
  "location": {
    "type": "GeoProperty",
    "value": {
      "type": "Point",
      "coordinates": [105.85, 21.03]
    }
  },
  "airQualityIndex": {
    "type": "Property",
    "value": 75
  }
}
```

### Update Entity

```http
PATCH /ngsi-ld/v1/entities/{entityId}/attrs
Content-Type: application/ld+json
```

**Request Body:**
```json
{
  "airQualityIndex": {
    "type": "Property",
    "value": 90
  }
}
```

### Delete Entity

```http
DELETE /ngsi-ld/v1/entities/{entityId}
```

---

## Entity Types

### AirQualityObserved

Dữ liệu chất lượng không khí.

| Property | Type | Description |
|----------|------|-------------|
| location | GeoProperty | Vị trí trạm |
| airQualityIndex | Property | Chỉ số AQI |
| PM2.5 | Property | Nồng độ PM2.5 (µg/m³) |
| PM10 | Property | Nồng độ PM10 (µg/m³) |
| dateObserved | Property | Thời gian đo |

### WeatherObserved

Dữ liệu thời tiết.

| Property | Type | Description |
|----------|------|-------------|
| location | GeoProperty | Vị trí trạm |
| temperature | Property | Nhiệt độ (°C) |
| humidity | Property | Độ ẩm (%) |
| windSpeed | Property | Tốc độ gió (m/s) |
| precipitation | Property | Lượng mưa (mm) |
| dateObserved | Property | Thời gian đo |

### TrafficFlow

Dữ liệu giao thông.

| Property | Type | Description |
|----------|------|-------------|
| location | GeoProperty | Vị trí đoạn đường |
| density | Property | Mật độ (0-1) |
| averageSpeed | Property | Tốc độ trung bình (km/h) |
| congestionLevel | Property | Mức độ tắc nghẽn |
| dateObserved | Property | Thời gian đo |

---

## Subscriptions

Đăng ký nhận thông báo khi dữ liệu thay đổi.

### Create Subscription

```http
POST /ngsi-ld/v1/subscriptions
Content-Type: application/ld+json
```

**Request Body:**
```json
{
  "@context": "https://uri.etsi.org/ngsi-ld/v1/ngsi-ld-core-context.jsonld",
  "type": "Subscription",
  "entities": [
    {
      "type": "AirQualityObserved"
    }
  ],
  "watchedAttributes": ["airQualityIndex"],
  "notification": {
    "endpoint": {
      "uri": "http://your-callback-url/notify",
      "accept": "application/json"
    }
  }
}
```
