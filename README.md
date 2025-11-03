# 🏠 Tro-Hub - Hệ thống tìm phòng trọ và bạn cùng phòng

Ứng dụng web giúp kết nối người tìm phòng trọ với chủ nhà và tìm kiếm bạn cùng phòng phù hợp. Hệ thống bao gồm Backend (FastAPI + MongoDB) và Frontend (React + TanStack Query).

## 📁 Cấu trúc dự án

```
tro-hub/
├── tro-hub-be/          # Backend API (FastAPI + MongoDB)
└── tro-hub-fe/          # Frontend Web App (React + Vite)
```

## 🚀 Tính năng chính

### 🔐 Xác thực & Hồ sơ người dùng
- Đăng ký/Đăng nhập tài khoản
- Quản lý hồ sơ cá nhân với thông tin chi tiết
- Tùy chỉnh sở thích và yêu cầu tìm bạn cùng phòng

### 🏘️ Quản lý tin đăng phòng trọ
- Tạo, chỉnh sửa, xóa tin đăng phòng trọ
- Tìm kiếm phòng trọ theo vị trí (GeoSpatial), giá, diện tích
- Xem chi tiết phòng trọ với hình ảnh và mô tả đầy đủ
- Hiển thị trên bản đồ tương tác (Leaflet)

### 🤝 Tìm kiếm và ghép đôi (Matching)
- Thuật toán ghép đôi thông minh dựa trên sở thích
- Đề xuất bạn cùng phòng phù hợp
- Quản lý danh sách yêu thích

### 💬 Nhắn tin trực tuyến
- Chat real-time qua WebSocket
- Lịch sử tin nhắn lưu trữ trong database
- Giao diện chat thân thiện

### ⭐ Đánh giá & Báo cáo
- Đánh giá người dùng và phòng trọ
- Hệ thống báo cáo vi phạm

## 🛠️ Công nghệ sử dụng

### Backend
- **Framework**: FastAPI
- **Database**: MongoDB (Motor async driver)
- **Authentication**: bcrypt
- **WebSocket**: FastAPI WebSocket
- **Validation**: Pydantic v2
- **Deployment**: Docker + Docker Compose

### Frontend
- **Framework**: React 18 + TypeScript
- **Build Tool**: Vite
- **State Management**: TanStack Query (React Query)
- **Routing**: React Router v6
- **Form Management**: React Hook Form + Zod
- **Styling**: Tailwind CSS
- **Maps**: Leaflet + React Leaflet
- **HTTP Client**: Axios

## 📦 Yêu cầu hệ thống

- **Node.js**: >= 18.x
- **Python**: >= 3.10
- **Docker & Docker Compose**: (khuyến nghị cho backend)
- **MongoDB**: >= 5.0 (nếu chạy local không dùng Docker)

## 🚀 Hướng dẫn cài đặt

### 1️⃣ Clone Repository

```bash
git clone https://github.com/VietDSK6/tro-hub.git
cd tro-hub
```

### 2️⃣ Cài đặt Backend

#### Sử dụng Docker (Khuyến nghị)

```bash
cd tro-hub-be
cp .env.example .env
docker compose up --build
```

- API Server: http://localhost:8000
- API Documentation: http://localhost:8000/docs
- Mongo Express: http://localhost:8081 (admin/admin)

#### Chạy local không Docker

```bash
cd tro-hub-be
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env
# Chỉnh sửa .env với MongoDB connection string
uvicorn app.main:app --reload
```

📖 [Xem chi tiết Backend README](./tro-hub-be/README.md)

### 3️⃣ Cài đặt Frontend

```bash
cd tro-hub-fe
npm install
cp .env.example .env
# Chỉnh sửa VITE_API_BASE nếu cần (mặc định: http://localhost:8000)
npm run dev
```

- Web App: http://localhost:5173

📖 [Xem chi tiết Frontend README](./tro-hub-fe/README.md)

## 📚 API Documentation

Sau khi chạy backend, truy cập Swagger UI để xem tài liệu API tương tác:

- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

### API Endpoints chính

#### Authentication
- `POST /auth/register` - Đăng ký tài khoản mới
- `POST /auth/login` - Đăng nhập

#### Listings (Tin đăng phòng trọ)
- `GET /listings` - Lấy danh sách phòng trọ (hỗ trợ tìm kiếm geo-spatial)
- `POST /listings` - Tạo tin đăng mới
- `GET /listings/{id}` - Chi tiết tin đăng
- `PUT /listings/{id}` - Cập nhật tin đăng
- `DELETE /listings/{id}` - Xóa tin đăng

#### Profiles (Hồ sơ)
- `GET /profiles/{user_id}` - Xem hồ sơ người dùng
- `PUT /profiles/{user_id}` - Cập nhật hồ sơ

#### Matching (Ghép đôi)
- `GET /matching` - Lấy danh sách đề xuất bạn cùng phòng

#### Chat (Nhắn tin)
- `GET /chat/history/{peer_id}` - Lịch sử chat
- `WebSocket /ws/chat/{peer_id}` - Real-time chat

#### Favorites (Yêu thích)
- `POST /favorites` - Thêm vào yêu thích
- `GET /favorites` - Danh sách yêu thích
- `DELETE /favorites/{listing_id}` - Xóa khỏi yêu thích

#### Reviews (Đánh giá)
- `POST /reviews` - Tạo đánh giá
- `GET /reviews` - Danh sách đánh giá

## 🎨 Giao diện người dùng

### Các trang chính

- **`/`** - Trang chủ: Danh sách phòng trọ với bộ lọc
- **`/auth`** - Đăng nhập / Đăng ký
- **`/listings/:id`** - Chi tiết phòng trọ
- **`/listings/new`** - Tạo tin đăng mới (có guard)
- **`/profile`** - Hồ sơ cá nhân (có guard)
- **`/favorites`** - Danh sách yêu thích (có guard)
- **`/matching`** - Tìm bạn cùng phòng (có guard)
- **`/messages/:peerId`** - Chat với người dùng (có guard)

**Guard**: Các trang có guard yêu cầu đăng nhập, nếu chưa đăng nhập sẽ redirect về `/auth`

## 🔧 Scripts hữu ích

### Backend
```bash
# Chạy development server
uvicorn app.main:app --reload

# Chạy với Docker
docker compose up -d

# Xem logs
docker compose logs -f api

# Dừng services
docker compose down
```

### Frontend
```bash
# Development server
npm run dev

# Build production
npm run build

# Preview production build
npm run preview
```

## 🧪 Testing

### Ví dụ test API với curl

**Đăng ký tài khoản:**
```bash
curl -X POST http://localhost:8000/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "email": "demo@example.com",
    "password": "secret123",
    "name": "Demo User"
  }'
```

**Tạo tin đăng phòng trọ:**
```bash
curl -X POST http://localhost:8000/listings \
  -H "Content-Type: application/json" \
  -H "x-user-id: YOUR_USER_ID" \
  -d '{
    "title": "Phòng trọ Quận 3 có điều hòa",
    "desc": "Gần trường, an ninh tốt",
    "price": 3500000,
    "area": 18,
    "amenities": ["ac","parking","water_heater"],
    "rules": {"pet": false, "cook": true},
    "images": ["https://example.com/1.jpg"],
    "location": {"type":"Point","coordinates":[106.682,10.78]}
  }'
```

**Tìm kiếm phòng trọ trong bán kính 3km:**
```bash
curl "http://localhost:8000/listings?lng=106.68&lat=10.78&radius_km=3&min_price=2500000&max_price=5000000"
```

## 🌍 Environment Variables

### Backend (.env)
```env
MONGO_URI=mongodb://localhost:27017
DB_NAME=roommate_db
```

### Frontend (.env)
```env
VITE_API_BASE=http://localhost:8000
```

## 📝 Database Schema

### Collections chính

- **users** - Thông tin tài khoản người dùng
- **profiles** - Hồ sơ chi tiết và sở thích
- **listings** - Tin đăng phòng trọ (có GeoJSON index)
- **messages** - Lịch sử tin nhắn
- **favorites** - Danh sách yêu thích
- **reviews** - Đánh giá
- **reports** - Báo cáo vi phạm

## 🤝 Đóng góp

Mọi đóng góp đều được chào đón! Vui lòng:

1. Fork repository
2. Tạo branch mới (`git checkout -b feature/AmazingFeature`)
3. Commit thay đổi (`git commit -m 'Add some AmazingFeature'`)
4. Push lên branch (`git push origin feature/AmazingFeature`)
5. Mở Pull Request

## 📄 License

Dự án này được phát triển cho mục đích học tập và nghiên cứu.

## 👥 Team

- **Repository**: [github.com/VietDSK6/tro-hub](https://github.com/VietDSK6/tro-hub)
- **Owner**: VietDSK6

## 📞 Liên hệ & Hỗ trợ

Nếu bạn gặp vấn đề hoặc có câu hỏi, vui lòng:
- Tạo Issue trên GitHub
- Kiểm tra Documentation tại `/docs` endpoint
- Xem README chi tiết của từng module

---

**Chúc bạn code vui vẻ! 🎉**
