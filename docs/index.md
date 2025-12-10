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

---
hide:
  - navigation
  - toc
---

<div class="hero">
  <img src="assets/logo.png" alt="GreenMap Logo" class="hero-logo">
  <div class="hero-badge">🌿 GREENMAP ECOSYSTEM</div>
  <h1>Bản Đồ Xanh Hà Nội</h1>
  <p class="tagline">Nền tảng giám sát môi trường đô thị thông minh</p>
  <p class="description">
    Hệ thống hoàn chỉnh gồm <strong>Backend API</strong>, <strong>Web Portal</strong>, <strong>Mobile App</strong> và <strong>Data Pipeline</strong> - Kết nối IoT, báo cáo cộng đồng, AI insights để xây dựng thành phố xanh bền vững.
  </p>
  <div class="hero-actions">
    <a href="getting-started/" class="btn btn-primary">
      <span>Bắt Đầu Ngay</span>
      <span class="btn-arrow">→</span>
    </a>
    <a href="https://github.com/HouHackathon-CQP" class="btn btn-secondary">
      <span>GitHub</span>
    </a>
  </div>
</div>

<div class="stats-section">
  <div class="stat-card">
    <div class="stat-icon">🚀</div>
    <div class="stat-number">4</div>
    <div class="stat-label">Repositories</div>
    <div class="stat-desc">Backend · Frontend · Mobile · Data</div>
  </div>
  <div class="stat-card">
    <div class="stat-icon">🌍</div>
    <div class="stat-number">2</div>
    <div class="stat-label">Platforms</div>
    <div class="stat-desc">Web Portal · Android App</div>
  </div>
  <div class="stat-card">
    <div class="stat-icon">⚡</div>
    <div class="stat-number">24/7</div>
    <div class="stat-label">Real-time</div>
    <div class="stat-desc">AQI · Weather · Traffic</div>
  </div>
  <div class="stat-card">
    <div class="stat-icon">🤖</div>
    <div class="stat-number">AI</div>
    <div class="stat-label">Smart Insights</div>
    <div class="stat-desc">Gemini · Groq · Analysis</div>
  </div>
</div>

## 🏗️ Các Thành Phần Hệ Thống

<p class="section-subtitle">4 repositories độc lập, tối ưu cho từng mục đích riêng</p>

<div class="features">
  <div class="feature feature-highlight">
    <div class="feature-tag">Core Infrastructure</div>
    <h3>🚀 Backend API</h3>
    <p><strong>FastAPI + PostgreSQL + PostGIS</strong> - REST API server với async support, tích hợp NGSI-LD Context Broker.</p>
    <ul class="feature-list">
      <li><strong>FastAPI</strong> async với SQLAlchemy 2.0</li>
      <li><strong>PostGIS</strong> - Dữ liệu địa lý & spatial queries</li>
      <li><strong>JWT Auth</strong> - Role-based access control</li>
      <li><strong>Orion-LD</strong> - FIWARE Context Broker sync</li>
      <li><strong>Background Jobs</strong> - AQI, Weather, Traffic agents</li>
      <li><strong>AI Integration</strong> - Gemini & Groq insights</li>
    </ul>
    <a href="developer-guide/#backend-development" class="feature-link">Xem chi tiết →</a>
  </div>
  
  <div class="feature">
    <h3>💻 Web Portal</h3>
    <p><strong>React 18 + Vite + Tailwind</strong> - Admin dashboard với bản đồ realtime, quản lý báo cáo & hạ tầng.</p>
    <ul class="feature-list">
      <li><strong>React 18</strong> - Modern hooks & Context API</li>
      <li><strong>MapLibre GL</strong> - Interactive 3D maps</li>
      <li><strong>Recharts</strong> - Analytics & visualizations</li>
      <li><strong>Real-time KPIs</strong> - Dashboard metrics</li>
      <li><strong>Push Notifications</strong> - Firebase integration</li>
      <li><strong>News Feed</strong> - RSS từ Hà Nội Mới</li>
    </ul>
    <a href="user-guide/" class="feature-link">Hướng dẫn sử dụng →</a>
  </div>
  
  <div class="feature">
    <h3>📱 Mobile App</h3>
    <p><strong>Kotlin + Jetpack Compose</strong> - Android app cho người dân, gửi báo cáo & nhận cảnh báo môi trường.</p>
    <ul class="feature-list">
      <li><strong>Jetpack Compose</strong> - Modern declarative UI</li>
      <li><strong>Material Design 3</strong> - Beautiful interface</li>
      <li><strong>Mapbox SDK</strong> - Offline-capable maps</li>
      <li><strong>Camera & GPS</strong> - Location-based reports</li>
      <li><strong>FCM Push</strong> - Real-time notifications</li>
    </ul>
    <a href="developer-guide/#mobile-development" class="feature-link">Mobile development →</a>
  </div>
  
  <div class="feature">
    <h3>📊 Data Pipeline</h3>
    <p><strong>Python ETL + Jupyter</strong> - Data collection, processing & simulation cho testing & training.</p>
    <ul class="feature-list">
      <li><strong>OSM Import</strong> - OpenStreetMap data processing</li>
      <li><strong>GeoJSON Tools</strong> - Spatial data transformation</li>
      <li><strong>SUMO Simulation</strong> - Traffic data generation</li>
      <li><strong>Jupyter Analysis</strong> - Data exploration notebooks</li>
    </ul>
    <a href="developer-guide/#data-pipeline" class="feature-link">Data pipeline →</a>
  </div>
</div>

## 💻 Tech Stack

<p class="section-subtitle">Công nghệ hiện đại từ Backend, Frontend đến Mobile và Infrastructure</p>

<div class="tech-grid">
  <div class="tech-card">
    <h4>🐍 Backend</h4>
    <p><strong>FastAPI</strong> · PostgreSQL · PostGIS · SQLAlchemy · Redis · JWT Auth</p>
  </div>
  <div class="tech-card">
    <h4>⚛️ Frontend</h4>
    <p><strong>React 18</strong> · Vite · Tailwind CSS · MapLibre GL · Recharts</p>
  </div>
  <div class="tech-card">
    <h4>🤖 Mobile</h4>
    <p><strong>Kotlin</strong> · Jetpack Compose · Mapbox SDK · Material 3 · Hilt</p>
  </div>
  <div class="tech-card">
    <h4>🔌 IoT</h4>
    <p><strong>FIWARE Orion-LD</strong> · NGSI-LD · MongoDB · Context Broker</p>
  </div>
  <div class="tech-card">
    <h4>📊 Data</h4>
    <p><strong>Python</strong> · Pandas · GeoPandas · Jupyter · SUMO Simulation</p>
  </div>
  <div class="tech-card">
    <h4>🐳 DevOps</h4>
    <p><strong>Docker</strong> · Docker Compose · GitHub Actions · CI/CD</p>
  </div>
</div>

## 🌐 Nguồn Dữ Liệu

<div class="data-sources">
  <div class="data-source">
    <div class="data-icon">🗺️</div>
    <h4>OpenStreetMap</h4>
    <p>Bản đồ nền, POIs, hạ tầng xanh</p>
    <span class="data-update">Cộng đồng</span>
  </div>
  <div class="data-source">
    <div class="data-icon">☁️</div>
    <h4>OpenWeatherMap</h4>
    <p>Thời tiết hiện tại & dự báo 7 ngày</p>
    <span class="data-update">Mỗi 5 phút</span>
  </div>
  <div class="data-source">
    <div class="data-icon">🌬️</div>
    <h4>OpenAQ</h4>
    <p>Chất lượng không khí realtime</p>
    <span class="data-update">Mỗi 5-15 phút</span>
  </div>
  <div class="data-source">
    <div class="data-icon">🚗</div>
    <h4>SUMO Simulation</h4>
    <p>Mô phỏng giao thông thời gian thực</p>
    <span class="data-update">Loop 1 giờ</span>
  </div>
  <div class="data-source">
    <div class="data-icon">🤖</div>
    <h4>AI Analysis</h4>
    <p>Gemini & Groq cho weather insights</p>
    <span class="data-update">On-demand</span>
  </div>
  <div class="data-source">
    <div class="data-icon">📰</div>
    <h4>Hà Nội Mới RSS</h4>
    <p>Tin tức môi trường</p>
    <span class="data-update">Real-time</span>
  </div>
</div>

## 📚 Tài Liệu

<div class="doc-grid">
  <a href="getting-started/" class="doc-card">
    <div class="doc-icon">🚀</div>
    <h4>Bắt Đầu</h4>
    <p>Cài đặt & thiết lập hệ thống</p>
  </a>
  <a href="user-guide/" class="doc-card">
    <div class="doc-icon">📝</div>
    <h4>Hướng Dẫn</h4>
    <p>Sử dụng Web Portal & Mobile</p>
  </a>
  <a href="developer-guide/" class="doc-card">
    <div class="doc-icon">🛠️</div>
    <h4>Kỹ Thuật</h4>
    <p>Architecture & Code examples</p>
  </a>
  <a href="api-reference/" class="doc-card">
    <div class="doc-icon">📡</div>
    <h4>API Reference</h4>
    <p>REST API & NGSI-LD endpoints</p>
  </a>
</div>

## 🌟 Tính Năng Nổi Bật

<div class="features-highlight">
  <div class="feature-item">
    <span class="feature-badge">✨ NEW</span>
    <h4>AI Weather Insights</h4>
    <p>Phân tích thời tiết + AQI bằng Gemini/Groq, tự động sinh lời khuyên hoạt động ngoài trời</p>
  </div>
  <div class="feature-item">
    <span class="feature-badge">✨ NEW</span>
    <h4>Real-time Traffic Map</h4>
    <p>Hiển thị giao thông thời gian thực từ SUMO simulation, màu sắc theo mức độ ùn tắc</p>
  </div>
  <div class="feature-item">
    <span class="feature-badge">✨ NEW</span>
    <h4>Push Notifications</h4>
    <p>Gửi thông báo đến mobile app qua Firebase, hỗ trợ topic & device tokens</p>
  </div>
  <div class="feature-item">
    <span class="feature-badge">✨ NEW</span>
    <h4>News Feed</h4>
    <p>Tin tức môi trường từ Hà Nội Mới, tự động cập nhật qua RSS feed</p>
  </div>
</div>

<div class="cta-section">
  <h2>🚀 Sẵn Sàng Bắt Đầu?</h2>
  <p>Khám phá hệ thống GreenMap và đóng góp cho thành phố xanh bền vững</p>
  <div class="cta-buttons">
    <a href="getting-started/" class="cta-btn cta-primary">
      <span>Bắt Đầu Ngay</span>
      <span class="btn-arrow">→</span>
    </a>
    <a href="https://github.com/HouHackathon-CQP" class="cta-btn cta-secondary">
      <span>GitHub Organization</span>
    </a>
  </div>
</div>

---

<div class="footer-info">
  <p><strong>License:</strong> Apache 2.0 · <strong>Team:</strong> HouHackathon-CQP · <strong>Year:</strong> 2025</p>
  <p>Built with ❤️ for Hà Nội Smart City</p>
</div>
