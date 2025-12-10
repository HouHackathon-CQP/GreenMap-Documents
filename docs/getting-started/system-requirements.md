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

# Yêu Cầu Hệ Thống

Để chạy và phát triển GreenMap, bạn cần đảm bảo hệ thống đáp ứng các yêu cầu sau.

## Yêu Cầu Chung

### Phần Cứng Tối Thiểu

| Thành phần | Yêu cầu tối thiểu | Khuyến nghị |
|------------|-------------------|-------------|
| **CPU** | 2 cores | 4+ cores |
| **RAM** | 4 GB | 8+ GB |
| **Disk** | 10 GB trống | 20+ GB SSD |
| **Network** | Kết nối Internet | Băng thông ổn định |

### Phần Mềm

- **Docker Desktop** (bắt buộc cho Backend)
- **Git** để clone repositories
- **Trình duyệt hiện đại** (Chrome, Firefox, Edge)

## Backend Development

=== "Windows"

    - Windows 10/11 64-bit
    - Python 3.10+ ([Download](https://www.python.org/downloads/))
    - Docker Desktop ([Download](https://www.docker.com/products/docker-desktop/))
    - PowerShell 5.1+ (có sẵn)

=== "macOS"

    - macOS 10.15 (Catalina) trở lên
    - Python 3.10+ (`brew install python`)
    - Docker Desktop for Mac
    - Terminal (có sẵn)

=== "Linux"

    - Ubuntu 20.04+ / Debian 10+ / Fedora 34+
    - Python 3.10+ (`sudo apt install python3`)
    - Docker Engine + Docker Compose
    - Terminal (có sẵn)

## Frontend Development

- **Node.js** 18+ LTS ([Download](https://nodejs.org/))
- **npm** 9+ (đi kèm Node.js)
- **Trình soạn thảo**: VS Code (khuyến nghị)

## Mobile Development

- **Android Studio** Hedgehog 2023.1.1+ ([Download](https://developer.android.com/studio))
- **JDK** 17 (đi kèm Android Studio)
- **Android SDK** API Level 24+ (Android 7.0)
- **Thiết bị test**: Android Emulator hoặc thiết bị thật

## Cổng Mạng Sử Dụng

Đảm bảo các cổng sau không bị chiếm dụng:

| Cổng | Service | Mô tả |
|------|---------|-------|
| `8000` | FastAPI | Backend API |
| `5173` | Vite | Frontend Dev Server |
| `5432` | PostgreSQL | Database |
| `1026` | Orion-LD | Context Broker |
| `27017` | MongoDB | Broker Database |

## Kiểm Tra Môi Trường

Chạy các lệnh sau để xác nhận cài đặt:

```bash
# Python
python --version  # Python 3.10+

# Node.js
node --version    # v18+

# Docker
docker --version  # Docker 20+

# Git
git --version     # git 2+
```
