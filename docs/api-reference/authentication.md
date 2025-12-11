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

# Authentication

GreenMap sử dụng JWT (JSON Web Token) cho xác thực và phân quyền.

## Luồng Xác Thực

```mermaid
sequenceDiagram
    participant Client
    participant API
    participant DB

    Client->>API: POST /login (email, password)
    API->>DB: Verify credentials
    DB-->>API: User data
    API->>API: Generate JWT
    API-->>Client: { access_token, token_type }
    
    Note over Client: Store token
    
    Client->>API: GET /users/me (Authorization: Bearer token)
    API->>API: Verify JWT
    API->>DB: Get user data
    DB-->>API: User data
    API-->>Client: User profile
```

## JWT Token

### Structure

Token JWT bao gồm 3 phần:

```
Header.Payload.Signature
```

**Ví dụ Payload:**
```json
{
  "sub": "1",
  "email": "admin@greenmap.hanoi",
  "role": "admin",
  "exp": 1702224600,
  "iat": 1702222800
}
```

### Token Expiration

- **Access Token**: 30 phút (có thể cấu hình)
- Sau khi hết hạn, cần đăng nhập lại

## Endpoints

### Login

```http
POST /login
Content-Type: application/x-www-form-urlencoded

username=admin@greenmap.hanoi&password=yourpassword
```

**Success Response (200):**
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIs...",
  "token_type": "bearer"
}
```

**Error Response (401):**
```json
{
  "detail": "Incorrect email or password"
}
```

### Protected Endpoints

Thêm header `Authorization` với prefix `Bearer`:

```http
GET /users/me
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...
```

## Roles & Permissions

### Roles

| Role | Mô tả |
|------|-------|
| `admin` | Toàn quyền quản trị hệ thống |
| `citizen` | Người dùng thông thường |

### Permissions Matrix

| Resource | Action | Admin | Citizen |
|----------|--------|-------|---------|
| Users | List | ✅ | ❌ |
| Users | Create | ✅ | ❌ |
| Reports | Create | ✅ | ✅ |
| Reports | List Own | ✅ | ✅ |
| Reports | List All | ✅ | ❌ |
| Reports | Update Status | ✅ | ❌ |
| Locations | List | ✅ | ✅ |
| Locations | Create/Update/Delete | ✅ | ❌ |

## Implementation

### Backend (FastAPI)

```python
from fastapi import Depends, HTTPException
from fastapi.security import OAuth2PasswordBearer

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="/login")

async def get_current_user(token: str = Depends(oauth2_scheme)):
    try:
        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])
        user_id = payload.get("sub")
        if user_id is None:
            raise HTTPException(status_code=401, detail="Invalid token")
    except JWTError:
        raise HTTPException(status_code=401, detail="Invalid token")
    
    user = await get_user(user_id)
    if user is None:
        raise HTTPException(status_code=401, detail="User not found")
    return user

async def require_admin(current_user = Depends(get_current_user)):
    if current_user.role != "admin":
        raise HTTPException(status_code=403, detail="Admin access required")
    return current_user
```

### Frontend (React)

```javascript
// Store token
const login = async (email, password) => {
  const response = await api.post('/login', 
    new URLSearchParams({ username: email, password })
  );
  localStorage.setItem('token', response.data.access_token);
};

// Axios interceptor
api.interceptors.request.use((config) => {
  const token = localStorage.getItem('token');
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});

// Handle 401
api.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      localStorage.removeItem('token');
      window.location.href = '/login';
    }
    return Promise.reject(error);
  }
);
```

### Mobile (Kotlin)

```kotlin
class AuthInterceptor : Interceptor {
    override fun intercept(chain: Interceptor.Chain): Response {
        val token = dataStore.getToken()
        
        val request = if (token != null) {
            chain.request().newBuilder()
                .addHeader("Authorization", "Bearer $token")
                .build()
        } else {
            chain.request()
        }
        
        return chain.proceed(request)
    }
}
```

## Security Best Practices

!!! warning "Lưu ý bảo mật"
    
    - ❌ Không lưu token trong code
    - ❌ Không log token ra console
    - ✅ Sử dụng HTTPS trong production
    - ✅ Rotate SECRET_KEY định kỳ
    - ✅ Implement token refresh (nếu cần)
