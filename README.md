# 🔐 AuthVault — User Registration System

Full-stack user authentication system built with Node.js, Express, MongoDB, and vanilla JS.

## 📁 Project Structure

```
user-auth-system/
├── backend/
│   ├── models/
│   │   └── User.js          ← Mongoose schema + bcrypt hashing
│   ├── routes/
│   │   └── auth.js          ← Register, Login, Profile, Logout endpoints
│   ├── middleware/
│   │   └── auth.js          ← JWT protect middleware
│   ├── .env                 ← Environment variables
│   └── server.js            ← Express app entry point
└── frontend/
    └── index.html           ← Complete SPA (Register + Login + Profile)
```

## ⚙️ Tech Stack

| Layer     | Technology                        |
|-----------|-----------------------------------|
| Backend   | Node.js + Express.js              |
| Database  | MongoDB + Mongoose ODM            |
| Auth      | JWT (jsonwebtoken)                |
| Security  | bcryptjs (password hashing)       |
| Validation| express-validator                 |
| Frontend  | HTML, CSS, Vanilla JS             |

## 🚀 Setup & Run

### Prerequisites
- Node.js installed
- MongoDB running locally (or use MongoDB Atlas)

### Step 1 — Install dependencies
```bash
cd backend
npm install
```

### Step 2 — Configure environment
Edit `backend/.env`:
```
PORT=5000
MONGO_URI=mongodb://127.0.0.1:27017/userAuthDB
JWT_SECRET=your_strong_secret_key_here
JWT_EXPIRES=7d
```

### Step 3 — Start MongoDB (if local)
```bash
# On Linux/Mac:
sudo systemctl start mongod

# On Manjaro (your setup):
sudo systemctl start mongodb
```

### Step 4 — Run the server
```bash
cd backend
node server.js
```

### Step 5 — Open frontend
Open `frontend/index.html` directly in your browser, OR the backend serves it at:
```
http://localhost:5000
```

## 🔌 API Endpoints

| Method | Route                  | Access  | Description              |
|--------|------------------------|---------|--------------------------|
| POST   | /api/auth/register     | Public  | Create new user account  |
| POST   | /api/auth/login        | Public  | Login + get JWT token    |
| GET    | /api/auth/profile      | Private | Fetch logged-in user     |
| PUT    | /api/auth/profile      | Private | Update user profile      |
| POST   | /api/auth/logout       | Private | Invalidate session       |
| GET    | /api/health            | Public  | Server health check      |

## 🔒 Security Features

- Passwords hashed with **bcryptjs** (salt rounds: 12)
- Authentication via **JWT** (stored in localStorage)
- Server-side validation with **express-validator**
- Password field excluded from DB queries by default (`select: false`)
- CORS enabled for frontend-backend communication

## 🧪 Testing with cURL

```bash
# Register
curl -X POST http://localhost:5000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{"name":"Dhruv","email":"dhruv@test.com","password":"secret123"}'

# Login
curl -X POST http://localhost:5000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"dhruv@test.com","password":"secret123"}'

# Profile (replace TOKEN with actual JWT)
curl http://localhost:5000/api/auth/profile \
  -H "Authorization: Bearer TOKEN"
```

## 🌐 Deploy

- **Backend**: Deploy to Railway, Render, or any VPS
- **Database**: Use MongoDB Atlas (free tier)
- **Frontend**: Upload `index.html` to Netlify, Vercel, or any static host
- Update `const API = '...'` in `index.html` to your live backend URL
