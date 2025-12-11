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

<!--docs/contributing/guidelines.md-->
# Hướng Dẫn Đóng Góp

Cảm ơn bạn quan tâm đến việc đóng góp cho GreenMap! Dự án này gồm 4 repositories độc lập, mỗi repository có hướng dẫn đóng góp riêng.

## Các Repository GreenMap

Trước khi bắt đầu, xác định bạn muốn đóng góp cho repository nào:

### 1. GreenMap-Backend
**Repository:** github.com/HouHackathon-CQP/GreenMap-Backend

Stack: Python, FastAPI, PostgreSQL, MongoDB, Orion-LD

**Các Cách Đóng Góp:**
- Thêm API endpoints mới
- Cải thiện business logic
- Xử lý bugs
- Tối ưu hóa database queries
- Cập nhật agents (AQI, Weather)

### 2. GreenMap-Frontend
**Repository:** github.com/HouHackathon-CQP/GreenMap-Frontend

Stack: React, Tailwind CSS, Vite, Leaflet

**Các Cách Đóng Góp:**
- Cải thiện UI/UX
- Thêm features mới
- Sửa bugs
- Tối ưu hóa performance
- Cập nhật stylesheets

### 3. GreenMap-Data
**Repository:** github.com/HouHackathon-CQP/GreenMap-Data

Stack: Python, Jupyter, Pandas, GeoPandas

**Các Cách Đóng Góp:**
- Thêm notebooks phân tích
- Xử lý dữ liệu GeoJSON
- Cải thiện data simulation
- Thêm visualizations
- Dokumentasi data

### 4. GreenMap-Documents
**Repository:** github.com/HouHackathon-CQP/GreenMap-Documents

Stack: MkDocs, Material Theme

**Các Cách Đóng Góp:**
- Cập nhật documentation
- Sửa typos
- Thêm ví dụ mới
- Cải thiện clarity
- Dịch sang ngôn ngữ khác

## Quy Trình Đóng Góp Chung

### Bước 1: Fork Repository

1. Truy cập repository GitHub bạn muốn đóng góp
2. Nhấp **Fork** ở góc phải
3. Clone fork của bạn:

```bash
git clone https://github.com/YOUR_USERNAME/GreenMap-REPO.git
cd GreenMap-REPO
```

### Bước 2: Tạo Feature Branch

```bash
# Update từ upstream
git fetch upstream

# Tạo branch mới
git checkout -b feature/your-feature-name upstream/main
```

Quy ước tên branch:
- `feature/add-new-endpoint` - Tính năng mới
- `fix/bug-description` - Sửa bug
- `docs/update-readme` - Cập nhật docs
- `style/format-code` - Cải thiện style

### Bước 3: Làm Việc Cục Bộ

**Backend:**
```bash
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
# Make changes...
python main.py  # Test
```

**Frontend:**
```bash
npm install
npm run dev
# Make changes...
npm run build  # Test build
```

**Data:**
```bash
pip install jupyter pandas geopandas
jupyter notebook
# Make changes to notebooks...
```

**Documents:**
```bash
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
mkdocs serve
# Make changes to .md files...
```

### Bước 4: Commit Changes

```bash
# Stage changes
git add .

# Commit với message rõ ràng
git commit -m "feature: add new endpoint for sensor data"
```

Quy ước commit messages:
- `feature:` - Tính năng mới
- `fix:` - Sửa bug
- `docs:` - Cập nhật docs
- `test:` - Thêm tests
- `refactor:` - Cải thiện code
- `style:` - Định dạng code

### Bước 5: Push & Create Pull Request

```bash
git push origin feature/your-feature-name
```

Sau đó:
1. Truy cập GitHub fork của bạn
2. Nhấp **Compare & Pull Request**
3. Điền mô tả chi tiết
4. Nhấp **Create Pull Request**

## Tiêu Chuẩn Mã

### Python (Backend & Data)

```python
# Follow PEP 8
# Use type hints
def get_sensors(limit: int = 10) -> List[Sensor]:
    """Get list of sensors with limit."""
    return sensors[:limit]

# Use docstrings
class SensorRepository:
    """Repository for sensor data access."""
    
    def find_by_id(self, sensor_id: str) -> Optional[Sensor]:
        """Find sensor by ID."""
        pass
```

### JavaScript/React (Frontend)

```javascript
// Use ES6+ syntax
const getSensors = async (limit = 10) => {
  const response = await fetch(`/api/sensors?limit=${limit}`);
  return response.json();
};

// Use proper component structure
export const SensorCard = ({ sensor }) => {
  return (
    <div className="sensor-card">
      {sensor.name}
    </div>
  );
};

// Use JSDoc comments
/**
 * Fetch sensors from API
 * @param {number} limit - Number of sensors to fetch
 * @returns {Promise<Array>} List of sensors
 */
```

### Markdown (Documentation)

```markdown
# Heading 1
## Heading 2

- Use bullet points
- For lists

1. Use numbered
2. For sequences

**Bold** for emphasis
*Italic* for code references

`inline code` for variables
```

## Kiểm Tra Trước Khi Commit

### Backend
```bash
# Run tests
pytest

# Check code style
flake8 .

# Type checking
mypy .
```

### Frontend
```bash
# Run tests
npm test

# Check linting
npm run lint

# Build check
npm run build
```

## Báo Cáo Vấn Đề (Issues)

Nếu tìm thấy bug hoặc có đề xuất:

1. Kiểm tra [GitHub Issues](https://github.com/HouHackathon-CQP) đã có issue chưa
2. Nếu không có, tạo issue mới
3. Cung cấp:
   - **Title:** Tiêu đề rõ ràng
   - **Description:** Mô tả chi tiết vấn đề
   - **Steps to Reproduce:** Cách tái tạo (nếu là bug)
   - **Expected/Actual:** Kết quả mong muốn/thực tế

## Quy Tắc Ứng Xử

Tất cả đóng góp viên phải:
- Tôn trọng những người khác
- Không quấy rối hoặc phân biệt đối xử
- Thảo luận một cách xây dựng
- Chấp nhận phản hồi tích cực

Xem [Code of Conduct](code-of-conduct.md) để chi tiết.

## Liên Hệ

- **Maintainers:** Xem README của mỗi repository
- **GitHub Discussions:** Thảo luận ý tưởng
- **Issues:** Báo cáo vấn đề
- **Pull Requests:** Gửi đóng góp

## Điều Khoản Giấy Phép

Bằng cách đóng góp, bạn đồng ý rằng đóng góp của bạn sẽ được cấp phép dưới giấy phép Apache 2.0.

---

**Cảm ơn bạn đã đóng góp cho GreenMap! 🙏**

Để biết thêm chi tiết, kiểm tra README trong từng repository:
- [GreenMap-Backend README](../../../GreenMap-Backend/README.md)
- [GreenMap-Frontend README](../../../GreenMap-Frontend/README.md)
- [GreenMap-Data README](../../../GreenMap-Data/README.md)
