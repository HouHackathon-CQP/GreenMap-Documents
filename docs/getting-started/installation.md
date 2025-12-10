# 📚 Hướng Dẫn Cài Đặt Toàn Bộ GreenMap

Chào mừng bạn đến với hướng dẫn cài đặt chi tiết GreenMap! Tài liệu này được viết cho **người mới bắt đầu hoàn toàn** - ngay cả khi bạn chưa bao giờ lập trình trước đây, bạn cũng có thể theo dõi từng bước.

!!! info "Thời gian cài đặt dự kiến"
    - **Cài đặt nhanh**: 30-45 phút (chỉ Backend + Frontend)
    - **Cài đặt đầy đủ**: 1-2 giờ (tất cả 4 repositories)
    - **Lần đầu tiên**: Thêm 15-30 phút để cài đặt công cụ cần thiết

---

## 🔧 Yêu Cầu Tiên Quyết

Trước khi bắt đầu, bạn cần cài đặt các công cụ sau. Đừng lo lắng - chúng tôi sẽ hướng dẫn bạn chi tiết!

### 1. Git - Công Cụ Quản Lý Mã Nguồn

**Git là gì?** Git giúp bạn tải mã nguồn từ GitHub về máy tính.

=== "Windows"
    
    **Tải về:**
    
    1. Truy cập [git-scm.com/download/win](https://git-scm.com/download/win)
    2. Tải file cài đặt (tự động tải xuống)
    3. Chạy file `.exe` và nhấn "Next" cho tất cả các bước
    4. Chọn "Git from the command line and also from 3rd-party software"
    
    **Kiểm tra cài đặt:**
    ```powershell
    git --version
    # Kết quả: git version 2.43.0 (hoặc mới hơn)
    ```

=== "macOS"
    
    **Tải về:**
    
    1. Mở **Terminal** (Cmd + Space, gõ "Terminal")
    2. Chạy lệnh:
    ```bash
    xcode-select --install
    ```
    3. Hoặc tải từ [git-scm.com/download/mac](https://git-scm.com/download/mac)
    
    **Kiểm tra cài đặt:**
    ```bash
    git --version
    # Kết quả: git version 2.43.0
    ```

=== "Linux"
    
    **Ubuntu/Debian:**
    ```bash
    sudo apt update
    sudo apt install git -y
    ```
    
    **Fedora:**
    ```bash
    sudo dnf install git -y
    ```
    
    **Kiểm tra cài đặt:**
    ```bash
    git --version
    # Kết quả: git version 2.43.0
    ```

---

### 2. Python 3.10+ - Ngôn Ngữ Lập Trình Backend

**Python là gì?** Python là ngôn ngữ lập trình chạy Backend (máy chủ) của GreenMap.

=== "Windows"
    
    **Tải về:**
    
    1. Truy cập [python.org/downloads](https://www.python.org/downloads/)
    2. Tải **Python 3.11** hoặc **3.12** (khuyến nghị)
    3. **QUAN TRỌNG**: Tích chọn "Add Python to PATH" khi cài đặt!
    4. Nhấn "Install Now"
    
    **Kiểm tra cài đặt:**
    ```powershell
    python --version
    # Kết quả: Python 3.11.7 (hoặc 3.10+)
    
    pip --version
    # Kết quả: pip 23.3.1 from ...
    ```

=== "macOS"
    
    **Tải về:**
    
    **Cách 1: Homebrew (khuyến nghị)**
    ```bash
    # Cài Homebrew trước (nếu chưa có)
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    
    # Cài Python
    brew install python@3.11
    ```
    
    **Cách 2: Tải trực tiếp**
    1. Truy cập [python.org/downloads/macos](https://www.python.org/downloads/macos/)
    2. Tải **Python 3.11** macOS installer
    3. Chạy file `.pkg` và làm theo hướng dẫn
    
    **Kiểm tra cài đặt:**
    ```bash
    python3 --version
    # Kết quả: Python 3.11.7
    ```

=== "Linux"
    
    **Ubuntu/Debian:**
    ```bash
    sudo apt update
    sudo apt install python3.11 python3.11-venv python3-pip -y
    ```
    
    **Fedora:**
    ```bash
    sudo dnf install python3.11 python3-pip -y
    ```
    
    **Kiểm tra cài đặt:**
    ```bash
    python3 --version
    # Kết quả: Python 3.11.7
    ```

---

### 3. Node.js 18+ - Môi Trường Chạy Frontend

**Node.js là gì?** Node.js chạy ứng dụng Frontend (giao diện người dùng) của GreenMap.

=== "Windows"
    
    **Tải về:**
    
    1. Truy cập [nodejs.org](https://nodejs.org/)
    2. Tải phiên bản **LTS** (Long Term Support) - khuyến nghị 20.x
    3. Chạy file `.msi` và làm theo hướng dẫn
    4. Chọn "Automatically install necessary tools" nếu được hỏi
    
    **Kiểm tra cài đặt:**
    ```powershell
    node --version
    # Kết quả: v20.11.0
    
    npm --version
    # Kết quả: 10.2.4
    ```

=== "macOS"
    
    **Tải về:**
    
    **Cách 1: Homebrew (khuyến nghị)**
    ```bash
    brew install node@20
    ```
    
    **Cách 2: Tải trực tiếp**
    1. Truy cập [nodejs.org](https://nodejs.org/)
    2. Tải phiên bản **LTS** cho macOS
    3. Chạy file `.pkg` và làm theo hướng dẫn
    
    **Kiểm tra cài đặt:**
    ```bash
    node --version
    npm --version
    ```

=== "Linux"
    
    **Ubuntu/Debian (dùng NodeSource):**
    ```bash
    # Thêm repository Node.js 20.x
    curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
    
    # Cài đặt Node.js
    sudo apt install nodejs -y
    ```
    
    **Fedora:**
    ```bash
    sudo dnf install nodejs -y
    ```
    
    **Kiểm tra cài đặt:**
    ```bash
    node --version
    npm --version
    ```

---

### 4. Docker & Docker Compose - Container Services

**Docker là gì?** Docker chạy các dịch vụ cơ sở dữ liệu (PostgreSQL, MongoDB) trong "container" - giống như máy ảo nhẹ.

=== "Windows"
    
    **Tải về:**
    
    1. Truy cập [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop/)
    2. Tải **Docker Desktop for Windows**
    3. Cài đặt và **khởi động lại máy tính**
    4. Mở Docker Desktop - đợi nó khởi động hoàn toàn
    
    **Kiểm tra cài đặt:**
    ```powershell
    docker --version
    # Kết quả: Docker version 24.0.7
    
    docker-compose --version
    # Kết quả: Docker Compose version v2.23.3
    ```

=== "macOS"
    
    **Tải về:**
    
    1. Truy cập [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop/)
    2. Tải **Docker Desktop for Mac** (Intel hoặc Apple Silicon)
    3. Kéo thả Docker.app vào thư mục Applications
    4. Mở Docker Desktop từ Applications
    
    **Kiểm tra cài đặt:**
    ```bash
    docker --version
    docker-compose --version
    ```

=== "Linux"
    
    **Ubuntu/Debian:**
    ```bash
    # Cài Docker Engine
    sudo apt update
    sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt update
    sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
    
    # Thêm user vào docker group
    sudo usermod -aG docker $USER
    newgrp docker
    ```
    
    **Kiểm tra cài đặt:**
    ```bash
    docker --version
    docker compose version
    ```

!!! success "✅ Checkpoint 1: Công cụ cần thiết"
    Bạn đã cài đặt thành công:
    
    - ✅ Git
    - ✅ Python 3.10+
    - ✅ Node.js 18+
    - ✅ Docker & Docker Compose
    
    Nếu tất cả các lệnh `--version` đều hoạt động, bạn đã sẵn sàng tiếp tục!

!!! success "✅ Checkpoint 1: Công cụ cần thiết"
    Bạn đã cài đặt thành công:
    
    - ✅ Git
    - ✅ Python 3.10+
    - ✅ Node.js 18+
    - ✅ Docker & Docker Compose
    
    Nếu tất cả các lệnh `--version` đều hoạt động, bạn đã sẵn sàng tiếp tục!

---

## 📁 Bước 1: Tạo Thư Mục Quản Lý Chung

**Tại sao cần bước này?** Chúng ta sẽ tạo một thư mục để chứa tất cả 4 repositories của GreenMap, giúp dễ quản lý.

=== "Windows"
    
    ```powershell
    # Tạo thư mục GreenMap trên ổ D:
    mkdir D:\GreenMap
    
    # Di chuyển vào thư mục
    cd D:\GreenMap
    ```

=== "macOS/Linux"
    
    ```bash
    # Tạo thư mục GreenMap trong home directory
    mkdir ~/GreenMap
    
    # Di chuyển vào thư mục
    cd ~/GreenMap
    ```

!!! tip "Mẹo"
    Bạn có thể tạo thư mục ở bất kỳ đâu bạn muốn. Chỉ cần nhớ đường dẫn để dễ tìm lại!

---

## 📥 Bước 2: Clone Tất Cả Repositories

**Clone là gì?** "Clone" nghĩa là tải toàn bộ mã nguồn từ GitHub về máy tính của bạn.

### Clone 4 Repositories Chính

=== "Windows"
    
    ```powershell
    # Đảm bảo bạn đang ở trong D:\GreenMap
    cd D:\GreenMap
    
    # 1. Clone Backend
    git clone https://github.com/HouHackathon-CQP/GreenMap-Backend.git
    
    # 2. Clone Frontend
    git clone https://github.com/HouHackathon-CQP/GreenMap-Frontend.git
    
    # 3. Clone Data
    git clone https://github.com/HouHackathon-CQP/GreenMap-Data.git
    
    # 4. Clone Documents
    git clone https://github.com/HouHackathon-CQP/GreenMap-Documents.git
    ```

=== "macOS/Linux"
    
    ```bash
    # Đảm bảo bạn đang ở trong ~/GreenMap
    cd ~/GreenMap
    
    # Clone tất cả repositories
    git clone https://github.com/HouHackathon-CQP/GreenMap-Backend.git
    git clone https://github.com/HouHackathon-CQP/GreenMap-Frontend.git
    git clone https://github.com/HouHackathon-CQP/GreenMap-Data.git
    git clone https://github.com/HouHackathon-CQP/GreenMap-Documents.git
    ```

**Cấu trúc thư mục sau khi clone:**

```
GreenMap/
├── GreenMap-Backend/      # Máy chủ FastAPI
├── GreenMap-Frontend/     # Giao diện React
├── GreenMap-Data/         # Dữ liệu GeoJSON
└── GreenMap-Documents/    # Tài liệu MkDocs
```

!!! success "✅ Checkpoint 2: Clone repositories"
    Kiểm tra xem bạn có 4 thư mục bằng lệnh:
    
    **Windows:** `dir`
    
    **macOS/Linux:** `ls -l`
    
    Bạn sẽ thấy 4 thư mục: `GreenMap-Backend`, `GreenMap-Frontend`, `GreenMap-Data`, `GreenMap-Documents`

---

## 🔐 Bước 3: Lấy API Keys

GreenMap sử dụng **Google Gemini AI** và **Groq AI** để phân tích thời tiết và chất lượng không khí. Bạn cần đăng ký API key miễn phí.

### 3.1. Lấy Google Gemini API Key

1. Truy cập [aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey)
2. Đăng nhập bằng tài khoản Google
3. Nhấn **"Create API Key"**
4. Sao chép API key (bắt đầu bằng `AIza...`)

!!! warning "Lưu ý bảo mật"
    **Không bao giờ** chia sẻ API key công khai! Giữ nó như mật khẩu.

### 3.2. Lấy Groq API Key (Tùy chọn - dùng khi Gemini lỗi)

1. Truy cập [console.groq.com](https://console.groq.com/)
2. Tạo tài khoản miễn phí
3. Vào **API Keys** → **Create API Key**
4. Sao chép API key (bắt đầu bằng `gsk_...`)

!!! info "Groq là gì?"
    Groq là dịch vụ AI dự phòng. Nếu Gemini API không hoạt động, GreenMap tự động chuyển sang dùng Groq.

---

## 🖥️ Bước 4: Cài Đặt Backend

Backend là phần máy chủ của GreenMap, xử lý dữ liệu và API.

### 4.1. Cài Đặt Python Dependencies

=== "Windows"
    
    ```powershell
    # Di chuyển vào thư mục Backend
    cd D:\GreenMap\GreenMap-Backend
    
    # Tạo virtual environment (môi trường Python riêng)
    python -m venv .venv
    
    # Kích hoạt virtual environment
    .\.venv\Scripts\activate
    
    # Bạn sẽ thấy (.venv) xuất hiện ở đầu dòng lệnh
    
    # Cài đặt các thư viện Python
    pip install -r requirements.txt
    ```

=== "macOS/Linux"
    
    ```bash
    # Di chuyển vào thư mục Backend
    cd ~/GreenMap/GreenMap-Backend
    
    # Tạo virtual environment
    python3 -m venv .venv
    
    # Kích hoạt virtual environment
    source .venv/bin/activate
    
    # Cài đặt các thư viện Python
    pip install -r requirements.txt
    ```

!!! question "Virtual Environment là gì?"
    Virtual environment giống như "hộp cát" riêng cho dự án này. Các thư viện Python được cài trong `.venv` không ảnh hưởng đến hệ thống.

**Quá trình cài đặt sẽ mất 3-5 phút** - đừng tắt terminal!

### 4.2. Cấu Hình File `.env`

File `.env` chứa các thông tin cấu hình như mật khẩu database, API keys.

=== "Windows"
    
    ```powershell
    # Sao chép file mẫu
    copy env.example .env
    
    # Mở file .env bằng Notepad
    notepad .env
    ```

=== "macOS/Linux"
    
    ```bash
    # Sao chép file mẫu
    cp env.example .env
    
    # Mở file .env bằng nano (hoặc vim, code, gedit...)
    nano .env
    ```

**Chỉnh sửa file `.env`:**

```env
# === Database Configuration ===
DATABASE_URL="postgresql+asyncpg://admin:mysecretpassword@127.0.0.1:5432/greenmap_db"
# ☝️ Đừng thay đổi dòng này - Docker sẽ tự động tạo

# === Security ===
SECRET_KEY="your-secret-key-here-make-it-very-long-and-random-64-characters"
# ☝️ Thay bằng chuỗi ngẫu nhiên dài 64 ký tự (dùng generator online)
ALGORITHM="HS256"
ACCESS_TOKEN_EXPIRE_MINUTES=30

# === CORS (Frontend URL) ===
CORS_ORIGINS="http://localhost:3000,http://127.0.0.1:3000"
# ☝️ URL của Frontend - giữ nguyên

# === Admin Account ===
FIRST_SUPERUSER="admin@greenmap.hanoi"
FIRST_SUPERUSER_PASSWORD="123456"
# ☝️ Tài khoản admin đầu tiên - ĐỔI MẬT KHẨU sau khi cài xong!

# === External Services ===
ORION_BROKER_URL="http://localhost:1026"
# ☝️ URL của Orion-LD context broker - giữ nguyên

# === AI API Keys ===
GEMINI_API_KEY="AIza..."  # ← DÁN API KEY GEMINI Ở ĐÂY
GROQ_API_KEY="gsk_..."    # ← DÁN API KEY GROQ Ở ĐÂY (tùy chọn)

# === MongoDB ===
MONGO_URI="mongodb://admin:mysecretpassword@localhost:27017"
MONGO_DB_NAME="greenmap_orion"
# ☝️ Giữ nguyên - Docker tự động tạo
```

!!! danger "Quan trọng"
    - **Bắt buộc**: Thay `GEMINI_API_KEY` bằng API key bạn vừa lấy
    - **Khuyến nghị**: Đổi `SECRET_KEY` bằng chuỗi ngẫu nhiên 64 ký tự
    - **Bắt buộc**: Đổi `FIRST_SUPERUSER_PASSWORD` sau khi cài xong!

**Lưu file `.env`:**

- **Notepad/nano**: Ctrl + S (Windows) / Ctrl + X, Y, Enter (Linux/macOS)

### 4.3. Khởi Động Docker Services

Docker sẽ chạy 3 services quan trọng: PostgreSQL, MongoDB, Orion-LD.

=== "Windows"
    
    ```powershell
    # Đảm bảo Docker Desktop đang chạy!
    # Mở Docker Desktop trước khi chạy lệnh này
    
    # Khởi động tất cả containers
    docker-compose up -d
    
    # -d nghĩa là "detached" - chạy ngầm
    ```

=== "macOS/Linux"
    
    ```bash
    # Đảm bảo Docker Desktop đang chạy!
    
    # Khởi động containers
    docker compose up -d
    ```

**Đợi 15-30 giây** để containers khởi động hoàn toàn.

**Kiểm tra containers:**

```bash
docker-compose ps
# hoặc
docker compose ps
```

**Kết quả mong đợi:**

```
NAME                  STATUS      PORTS
greenmap-postgres     Up          0.0.0.0:5432->5432/tcp
greenmap-mongo        Up          0.0.0.0:27017->27017/tcp
greenmap-orion        Up          0.0.0.0:1026->1026/tcp
```

!!! tip "Mẹo"
    Nếu thấy `Exited` thay vì `Up`, chạy `docker-compose logs <tên-container>` để xem lỗi.

### 4.4. Khởi Tạo Database

Bây giờ ta cần tạo bảng trong PostgreSQL và import dữ liệu mẫu.

=== "Windows"
    
    ```powershell
    # Đảm bảo virtual environment đã kích hoạt (thấy .venv ở đầu dòng)
    
    # Tạo các bảng trong database
    python init_db.py
    
    # Import dữ liệu OpenStreetMap (parks, charging stations...)
    python import_osm.py
    
    # (Tùy chọn) Tạo dữ liệu sensor mẫu
    python seed_sensor.py
    ```

=== "macOS/Linux"
    
    ```bash
    # Đảm bảo virtual environment đã kích hoạt
    
    # Khởi tạo database
    python init_db.py
    
    # Import dữ liệu OSM
    python import_osm.py
    
    # (Tùy chọn) Seed sensors
    python seed_sensor.py
    ```

**Mỗi script sẽ mất 30 giây - 2 phút.** Bạn sẽ thấy log hiển thị:

```
✅ Created tables successfully
✅ Imported 127 parks
✅ Imported 45 charging stations
✅ Created admin user: admin@greenmap.hanoi
```

!!! success "✅ Checkpoint 3: Backend setup"
    Kiểm tra:
    
    - ✅ File `.env` đã có GEMINI_API_KEY
    - ✅ Docker containers đang chạy (`docker-compose ps`)
    - ✅ Database đã được khởi tạo (`init_db.py` chạy thành công)
    - ✅ Dữ liệu OSM đã được import (`import_osm.py` hoàn tất)

---

## 🚀 Bước 5: Chạy Backend Server

Bây giờ ta sẽ chạy 3 process của Backend:

## 🚀 Bước 5: Chạy Backend Server

Bây giờ ta sẽ chạy 3 process của Backend:

1. **FastAPI Server** - API chính
2. **AQI Agent** - Cập nhật chất lượng không khí
3. **Weather Agent** - Cập nhật thời tiết

!!! warning "Lưu ý"
    Mỗi process cần **1 terminal riêng**. Không đóng các terminal khi process đang chạy!

### Terminal 1: FastAPI Server

=== "Windows"
    
    ```powershell
    # Đảm bảo bạn ở trong D:\GreenMap\GreenMap-Backend
    cd D:\GreenMap\GreenMap-Backend
    
    # Kích hoạt venv
    .\.venv\Scripts\activate
    
    # Chạy server
    python main.py
    ```

=== "macOS/Linux"
    
    ```bash
    cd ~/GreenMap/GreenMap-Backend
    source .venv/bin/activate
    python main.py
    ```

**Kết quả mong đợi:**

```
INFO:     Uvicorn running on http://0.0.0.0:8000
INFO:     Application startup complete.
```

**Kiểm tra API:**

Mở trình duyệt và truy cập:

- **API Docs (Swagger)**: [http://localhost:8000/docs](http://localhost:8000/docs)
- **API Health**: [http://localhost:8000/api/health](http://localhost:8000/api/health)

Bạn sẽ thấy trang Swagger UI với danh sách 27+ endpoints!

### Terminal 2: AQI Agent (Mở terminal mới!)

=== "Windows"
    
    ```powershell
    # MỞ TERMINAL MỚI (PowerShell mới)
    cd D:\GreenMap\GreenMap-Backend
    .\.venv\Scripts\activate
    
    # Chạy AQI Agent
    python aqi_agent.py
    ```

=== "macOS/Linux"
    
    ```bash
    # MỞ TERMINAL MỚI
    cd ~/GreenMap/GreenMap-Backend
    source .venv/bin/activate
    
    # Chạy AQI Agent
    python aqi_agent.py
    ```

**Kết quả:**

```
🌍 AQI Agent started - updating every 5 minutes
✅ Fetched AQI data for Hanoi: AQI=95
🤖 AI Analysis: Chất lượng không khí ở mức TB...
```

### Terminal 3: Weather Agent (Mở terminal mới!)

=== "Windows"
    
    ```powershell
    # MỞ TERMINAL THỨ 3
    cd D:\GreenMap\GreenMap-Backend
    .\.venv\Scripts\activate
    
    # Chạy Weather Agent
    python weather_agent.py
    ```

=== "macOS/Linux"
    
    ```bash
    # MỞ TERMINAL THỨ 3
    cd ~/GreenMap/GreenMap-Backend
    source .venv/bin/activate
    
    # Chạy Weather Agent
    python weather_agent.py
    ```

**Kết quả:**

```
🌤️ Weather Agent started
✅ Fetched weather: 28°C, Cloudy
🤖 AI Insights: Thời tiết hôm nay thích hợp...
```

!!! success "✅ Checkpoint 4: Backend đang chạy"
    Bạn sẽ có 3 terminals:
    
    - ✅ Terminal 1: `python main.py` - API server
    - ✅ Terminal 2: `python aqi_agent.py` - AQI updates
    - ✅ Terminal 3: `python weather_agent.py` - Weather updates
    
    Tất cả đều hiển thị log liên tục. **KHÔNG tắt các terminal này!**

---

## 🎨 Bước 6: Cài Đặt Frontend

Frontend là giao diện web React mà người dùng sẽ thấy.

### 6.1. Cài Đặt Node.js Dependencies

**Mở terminal mới (thứ 4):**

=== "Windows"
    
    ```powershell
    # Di chuyển vào thư mục Frontend
    cd D:\GreenMap\GreenMap-Frontend
    
    # Cài đặt tất cả thư viện JavaScript
    npm install
    ```

=== "macOS/Linux"
    
    ```bash
    cd ~/GreenMap/GreenMap-Frontend
    npm install
    ```

**Quá trình này sẽ mất 2-5 phút** tùy vào tốc độ internet. Bạn sẽ thấy:

```
added 1247 packages in 3m
```

### 6.2. Chạy Development Server

=== "Windows"
    
    ```powershell
    # Chạy Vite dev server
    npm run dev
    ```

=== "macOS/Linux"
    
    ```bash
    npm run dev
    ```

**Kết quả mong đợi:**

```
  VITE v7.2.0  ready in 1234 ms

  ➜  Local:   http://localhost:3000/
  ➜  Network: http://192.168.1.100:3000/
  ➜  press h + enter to show help
```

**Mở trình duyệt:**

Truy cập [http://localhost:3000](http://localhost:3000) - bạn sẽ thấy trang chủ GreenMap!

!!! tip "Hot Reload"
    Vite hỗ trợ "hot reload" - khi bạn sửa code trong `src/`, trình duyệt tự động cập nhật ngay lập tức!

### 6.3. Đăng Nhập Tài Khoản Admin

Trên trang web:

1. Nhấn nút **"Đăng Nhập"** ở góc trên phải
2. Nhập thông tin:
    - **Email**: `admin@greenmap.hanoi`
    - **Mật khẩu**: `123456` (hoặc mật khẩu bạn đặt trong `.env`)
3. Nhấn **"Đăng Nhập"**

!!! success "Thành công!"
    Bạn sẽ thấy tên "Admin" hiển thị ở góc trên phải. Bây giờ bạn có thể:
    
    - Xem bản đồ tương tác
    - Xem dữ liệu AQI và thời tiết realtime
    - Tạo báo cáo môi trường
    - Quản lý người dùng (tính năng admin)

!!! success "✅ Checkpoint 5: Frontend đang chạy"
    - ✅ Frontend chạy tại http://localhost:3000
    - ✅ Bạn đã đăng nhập thành công
    - ✅ Bản đồ hiển thị Hà Nội với các layers

---

## 📊 Bước 7: Cài Đặt Data Repository (Tùy chọn)

Repository này chứa Jupyter notebooks để xử lý dữ liệu GeoJSON.

**Chỉ cần cài nếu bạn muốn:**

- Xử lý dữ liệu GeoJSON mới
- Chạy analysis notebooks
- Tạo simulation data

### 7.1. Cài Đặt

=== "Windows"
    
    ```powershell
    cd D:\GreenMap\GreenMap-Data
    
    # Tạo venv riêng cho Data
    python -m venv .venv
    .\.venv\Scripts\activate
    
    # Cài Jupyter và pandas
    pip install jupyter pandas geopandas matplotlib
    ```

=== "macOS/Linux"
    
    ```bash
    cd ~/GreenMap/GreenMap-Data
    python3 -m venv .venv
    source .venv/bin/activate
    
    # Cài dependencies
    pip install jupyter pandas geopandas matplotlib
    ```

### 7.2. Chạy Jupyter Notebook

```bash
# Với venv đã kích hoạt
jupyter notebook
```

Trình duyệt sẽ tự động mở [http://localhost:8888](http://localhost:8888) với Jupyter interface.

**Mở notebook:**

1. Click vào `data_collection.ipynb`
2. Chạy từng cell bằng Shift + Enter
3. Xem kết quả phân tích dữ liệu

---

## 📖 Bước 8: Cài Đặt Documentation (Tùy chọn)

Repository này chứa tài liệu MkDocs mà bạn đang đọc!

### 8.1. Cài Đặt

=== "Windows"
    
    ```powershell
    cd D:\GreenMap\GreenMap-Documents
    
    # Tạo venv riêng
    python -m venv .venv
    .\.venv\Scripts\activate
    
    # Cài MkDocs
    pip install -r requirements.txt
    ```

=== "macOS/Linux"
    
    ```bash
    cd ~/GreenMap/GreenMap-Documents
    python3 -m venv .venv
    source .venv/bin/activate
    
    # Cài dependencies
    pip install -r requirements.txt
    ```

### 8.2. Xem Docs Locally

```bash
# Chạy MkDocs dev server
mkdocs serve
```

Truy cập [http://localhost:8000](http://localhost:8000) để xem tài liệu!

!!! info "Chỉnh sửa docs"
    Mọi file `.md` trong `docs/` đều có thể chỉnh sửa. MkDocs tự động reload khi bạn lưu file.

---

## 📋 Tổng Quan Các Port Đang Sử Dụng

| Service | URL | Port | Mô Tả |
|---------|-----|------|-------|
| **Frontend** | http://localhost:3000 | 3000 | Giao diện React web |
| **Backend API** | http://localhost:8000 | 8000 | FastAPI server |
| **API Docs** | http://localhost:8000/docs | 8000 | Swagger UI |
| **PostgreSQL** | localhost:5432 | 5432 | Database chính |
| **MongoDB** | localhost:27017 | 27017 | Context data |
| **Orion-LD** | http://localhost:1026 | 1026 | FIWARE broker |
| **Jupyter** | http://localhost:8888 | 8888 | Notebooks (tùy chọn) |
| **MkDocs** | http://localhost:8000 | 8000 | Documentation (tùy chọn) |

!!! warning "Port conflicts"
    Nếu port đã bị chiếm, xem phần [Xử Lý Sự Cố](#xu-ly-su-co) bên dưới!

---

## ✅ Hoàn Tất! Kiểm Tra Hệ Thống

Bây giờ hệ thống GreenMap của bạn đã chạy hoàn toàn! Hãy kiểm tra:

### Checklist Cuối Cùng

- [ ] **Backend API**: http://localhost:8000/docs hiển thị Swagger UI
- [ ] **Frontend**: http://localhost:3000 hiển thị bản đồ Hà Nội
- [ ] **Đăng nhập**: Bạn có thể đăng nhập với `admin@greenmap.hanoi`
- [ ] **Docker**: Chạy `docker-compose ps` - thấy 3 containers "Up"
- [ ] **AQI Data**: Trong Frontend, click "Layers" → "Air Quality" - thấy dữ liệu
- [ ] **Weather**: Trang chủ hiển thị nhiệt độ và thời tiết hiện tại

### Test Workflow

**1. Xem bản đồ:**

- Mở http://localhost:3000
- Click vào các layer: Parks, Charging Stations, Tourist Attractions
- Zoom in/out, di chuyển bản đồ

**2. Tạo báo cáo:**

- Đăng nhập → "Tạo Báo Cáo"
- Click vào bản đồ để chọn vị trí
- Nhập mô tả, chọn loại (ô nhiễm, cây xanh, giao thông...)
- Submit → Báo cáo xuất hiện trên bản đồ!

**3. Xem AI Insights:**

- Trang chủ → Scroll xuống phần "AI Analysis"
- Đọc phân tích thời tiết và AQI do Gemini AI tạo
- Các insight được cập nhật mỗi 5 phút

!!! success "🎉 Chúc mừng!"
    Bạn đã cài đặt thành công toàn bộ hệ thống GreenMap! 
    
    Bây giờ bạn có thể:
    
    - ✅ Xem bản đồ tương tác với 500+ POIs
    - ✅ Theo dõi AQI và thời tiết realtime
    - ✅ Tạo báo cáo môi trường
    - ✅ Xem AI insights về chất lượng không khí
    - ✅ Quản lý người dùng (admin)

---

## 🆘 Xử Lý Sự Cố

### Lỗi 1: Port đã bị chiếm dụng

**Triệu chứng:**

```
Error: listen EADDRINUSE: address already in use :::3000
```

**Giải pháp:**

=== "Windows"
    
    ```powershell
    # Tìm process đang dùng port 3000
    netstat -ano | findstr :3000
    
    # Kết quả: TCP  0.0.0.0:3000  0.0.0.0:0  LISTENING  12345
    # 12345 là PID
    
    # Kill process
    taskkill /PID 12345 /F
    ```

=== "macOS/Linux"
    
    ```bash
    # Tìm process
    lsof -i :3000
    
    # Kill process
    kill -9 <PID>
    ```

**Hoặc thay đổi port:**

- **Frontend**: Sửa `vite.config.js` → `port: 3001`
- **Backend**: Sửa `main.py` → `uvicorn.run(port=8001)`

---

### Lỗi 2: Docker containers không khởi động

**Triệu chứng:**

```
docker-compose ps
# Thấy "Exited" thay vì "Up"
```

**Giải pháp:**

```bash
# Xem logs của container lỗi
docker-compose logs postgres
docker-compose logs mongo
docker-compose logs orion

# Restart containers
docker-compose restart

# Hoặc xóa và tạo lại
docker-compose down
docker-compose up -d
```

**Lỗi phổ biến:**

- **Port 5432 đã dùng**: PostgreSQL cài sẵn đang chạy
    ```bash
    # Windows: Tắt PostgreSQL service
    net stop postgresql-x64-15
    
    # macOS: 
    brew services stop postgresql
    ```

- **Thiếu quyền**: Chạy Docker Desktop với quyền Administrator

---

### Lỗi 3: Python dependencies lỗi

**Triệu chứng:**

```
ERROR: Could not find a version that satisfies the requirement fastapi==0.104.1
```

**Giải pháp:**

```bash
# Upgrade pip trước
pip install --upgrade pip

# Cài lại requirements
pip install -r requirements.txt

# Nếu vẫn lỗi, cài từng package quan trọng:
pip install fastapi uvicorn sqlalchemy asyncpg
```

---

### Lỗi 4: Frontend không kết nối được Backend

**Triệu chứng:**

Frontend hiển thị lỗi: `Network Error` hoặc `Failed to fetch`

**Giải pháp:**

1. **Kiểm tra Backend đang chạy:**
    ```bash
    curl http://localhost:8000/api/health
    # Phải trả về: {"status": "healthy"}
    ```

2. **Kiểm tra CORS trong .env:**
    ```env
    CORS_ORIGINS="http://localhost:3000,http://127.0.0.1:3000"
    ```

3. **Kiểm tra apiService.js:**
    File `src/apiService.js` phải có:
    ```javascript
    const API_BASE_URL = 'http://localhost:8000';
    ```

4. **Restart cả Backend và Frontend:**
    - Ctrl + C trong terminal Backend → chạy lại `python main.py`
    - Ctrl + C trong terminal Frontend → chạy lại `npm run dev`

---

### Lỗi 5: Database connection error

**Triệu chứng:**

```
sqlalchemy.exc.OperationalError: could not connect to server
```

**Giải pháp:**

1. **Kiểm tra PostgreSQL container:**
    ```bash
    docker-compose ps postgres
    # Phải thấy "Up"
    
    # Xem logs
    docker-compose logs postgres
    ```

2. **Kiểm tra DATABASE_URL trong .env:**
    ```env
    DATABASE_URL="postgresql+asyncpg://admin:mysecretpassword@127.0.0.1:5432/greenmap_db"
    ```
    
    - Username: `admin`
    - Password: `mysecretpassword`
    - Host: `127.0.0.1` (KHÔNG phải `localhost` trên một số hệ thống)
    - Port: `5432`
    - Database: `greenmap_db`

3. **Test kết nối thủ công:**
    ```bash
    # Cài psql client (nếu chưa có)
    # Windows: Cài PostgreSQL từ postgresql.org
    # macOS: brew install postgresql
    # Linux: sudo apt install postgresql-client
    
    # Kết nối
    psql -h 127.0.0.1 -U admin -d greenmap_db
    # Nhập password: mysecretpassword
    ```

---

### Lỗi 6: GEMINI_API_KEY không hoạt động

**Triệu chứng:**

AQI Agent hoặc Weather Agent hiển thị lỗi:

```
❌ Gemini API Error: 403 API key not valid
```

**Giải pháp:**

1. **Kiểm tra API key:**
    - Truy cập [aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey)
    - Tạo API key mới
    - Sao chép lại vào file `.env`

2. **Đảm bảo không có khoảng trắng:**
    ```env
    # ❌ SAI - có khoảng trắng
    GEMINI_API_KEY = "AIza..."
    
    # ✅ ĐÚNG - không có khoảng trắng
    GEMINI_API_KEY="AIza..."
    ```

3. **Restart Backend:**
    Sau khi sửa `.env`, **phải restart** Backend:
    ```bash
    # Ctrl + C trong terminal chạy main.py
    # Chạy lại:
    python main.py
    ```

4. **Dùng Groq thay thế:**
    Nếu Gemini không hoạt động, hệ thống tự động chuyển sang Groq. Đảm bảo `GROQ_API_KEY` cũng được điền.

---

### Lỗi 7: Node.js `npm install` lỗi

**Triệu chứng:**

```
npm ERR! code ERESOLVE
npm ERR! ERESOLVE could not resolve
```

**Giải pháp:**

```bash
# Xóa cache npm
npm cache clean --force

# Xóa node_modules và package-lock.json
rm -rf node_modules package-lock.json

# Cài lại với --legacy-peer-deps
npm install --legacy-peer-deps

# Hoặc dùng --force
npm install --force
```

---

### Lỗi 8: Virtual Environment không kích hoạt

**Triệu chứng:**

Không thấy `(.venv)` ở đầu dòng lệnh

**Giải pháp:**

=== "Windows PowerShell"
    
    ```powershell
    # Nếu gặp lỗi "cannot be loaded because running scripts is disabled"
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
    
    # Kích hoạt lại
    .\.venv\Scripts\activate
    ```

=== "Windows CMD"
    
    ```cmd
    .\.venv\Scripts\activate.bat
    ```

=== "macOS/Linux"
    
    ```bash
    source .venv/bin/activate
    ```

---

### Lỗi 9: `init_db.py` báo lỗi "Table already exists"

**Triệu chứng:**

```
sqlalchemy.exc.ProgrammingError: (psycopg2.errors.DuplicateTable) relation "users" already exists
```

**Giải pháp:**

Bạn đã chạy `init_db.py` trước đó. Có 2 lựa chọn:

**Option 1: Bỏ qua (khuyến nghị nếu chỉ test):**

```bash
# Không cần chạy lại init_db.py
# Database đã sẵn sàng
```

**Option 2: Xóa database và tạo lại:**

```bash
# Dừng Backend
# Ctrl + C trong terminal chạy main.py

# Xóa containers và volumes
docker-compose down -v

# Tạo lại containers
docker-compose up -d

# Đợi 15 giây

# Chạy lại init
python init_db.py
python import_osm.py
```

---

### Lỗi 10: Frontend hiển thị trắng xóa

**Triệu chứng:**

Trang http://localhost:3000 chỉ hiển thị màu trắng, không có gì

**Giải pháp:**

1. **Mở Console (F12):**
    - Nhấn F12 trong trình duyệt
    - Chuyển sang tab "Console"
    - Xem lỗi gì được hiển thị

2. **Lỗi thường gặp:**
    
    **"Failed to fetch":** Backend không chạy → Chạy lại `python main.py`
    
    **"Unexpected token":** Lỗi syntax trong code → Kiểm tra file bạn vừa sửa
    
    **"Module not found":** Thiếu dependency → Chạy lại `npm install`

3. **Hard refresh:**
    - Windows/Linux: Ctrl + Shift + R
    - macOS: Cmd + Shift + R

4. **Xóa cache trình duyệt:**
    - F12 → Application → Clear storage → Clear site data

---

## 🔗 Tài Nguyên Hữu Ích

### Documentation

- [Hướng Dẫn Bắt Đầu Nhanh](quick-start.md) - Dùng GreenMap trong 5 phút
- [API Reference](../api-reference/endpoints.md) - Tất cả 27+ endpoints
- [User Guide](../user-guide/features.md) - Hướng dẫn tính năng
- [FAQ](../user-guide/faq.md) - Câu hỏi thường gặp

### External Resources

- [FastAPI Docs](https://fastapi.tiangolo.com/) - Framework Backend
- [React Docs](https://react.dev/) - Framework Frontend
- [MapLibre GL JS](https://maplibre.org/) - Thư viện bản đồ
- [Docker Docs](https://docs.docker.com/) - Containerization

### Community

- **GitHub**: [HouHackathon-CQP/GreenMap](https://github.com/HouHackathon-CQP/GreenMap)
- **Issues**: [Report bugs](https://github.com/HouHackathon-CQP/GreenMap/issues)
- **Discussions**: [Ask questions](https://github.com/HouHackathon-CQP/GreenMap/discussions)

---

## 🎯 Các Bước Tiếp Theo

Bây giờ bạn đã cài đặt xong, hãy:

1. **Đọc [Quick Start Guide](quick-start.md)** - Học cách sử dụng GreenMap trong 5 phút
2. **Xem [User Guide](../user-guide/features.md)** - Khám phá tất cả tính năng
3. **Thử [API](../api-reference/endpoints.md)** - Tích hợp GreenMap vào ứng dụng của bạn
4. **Đóng góp** - Đọc [Contributing Guidelines](../contributing/guidelines.md) để tham gia phát triển

!!! tip "Thay đổi mật khẩu admin"
    **Quan trọng**: Sau khi cài xong, hãy đổi mật khẩu admin:
    
    1. Đăng nhập http://localhost:3000
    2. Click avatar → "Settings"
    3. Tab "Security" → "Change Password"
    4. Đổi từ `123456` sang mật khẩu mạnh

---

**Chúc bạn thành công với GreenMap! 🌍💚**

*Nếu gặp vấn đề không có trong tài liệu, vui lòng [tạo Issue](https://github.com/HouHackathon-CQP/GreenMap/issues) trên GitHub.*
