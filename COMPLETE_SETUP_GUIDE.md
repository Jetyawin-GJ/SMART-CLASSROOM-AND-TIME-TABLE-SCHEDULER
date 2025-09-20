# 🚀 Complete Multi-Portal Timetable System Setup Guide

## 📋 Prerequisites
- Python 3.8+
- Node.js 16+
- Git

## 🛠️ Backend Setup

### 1. Install Python Dependencies
```bash
cd backend
pip install fastapi uvicorn sqlalchemy python-jose[cryptography] passlib[bcrypt] python-dotenv
```

### 2. Run Database Migrations
```bash
# Run NEP 2020 migration
python -m backend.migrate_nep

# Run authentication migration
python -m backend.migrate_auth
```

### 3. Create Sample Users
```bash
python -m backend.create_sample_users
```

### 4. Start Backend Server
```bash
uvicorn backend.main:app --reload --host 0.0.0.0 --port 8000
```

**Backend will be running at: http://localhost:8000**

## 🎨 Frontend Setup

### 1. Install Node.js Dependencies
```bash
cd frontend
npm install
```

### 2. Start Frontend Development Server
```bash
npm run dev
```

**Frontend will be running at: http://localhost:5173**

## 🔑 Login Credentials

| Role | Username | Password | Access Level |
|------|----------|----------|--------------|
| **Admin** | admin | admin123 | Full system control |
| **Faculty** | faculty1 | faculty123 | View all timetables |
| **Student** | student1 | student123 | View own timetable |

## 🎯 How to Run Both Together

### Option 1: Manual (Recommended for Development)
Open **2 terminal windows**:

**Terminal 1 (Backend):**
```bash
cd backend
uvicorn backend.main:app --reload --host 0.0.0.0 --port 8000
```

**Terminal 2 (Frontend):**
```bash
cd frontend
npm run dev
```

### Option 2: Using Docker (If Available)
```bash
# From project root
docker-compose up --build
```

## 🌐 Access Points

- **Frontend Portal**: http://localhost:5173
- **Backend API**: http://localhost:8000
- **API Documentation**: http://localhost:8000/docs
- **Admin Portal**: http://localhost:5173 (login as admin)
- **Faculty Portal**: http://localhost:5173 (login as faculty1)
- **Student Portal**: http://localhost:5173 (login as student1)

## 🎉 Features Available

### 👨‍💼 Admin Portal
- ✅ System dashboard with statistics
- ✅ User management (view all users)
- ✅ Timetable generation (regular & NEP 2020)
- ✅ Faculty and student management
- ✅ Full system control

### 👨‍🏫 Faculty Portal
- ✅ Personal teaching schedule
- ✅ View all class timetables
- ✅ Profile management
- ✅ Teaching overview

### 👨‍🎓 Student Portal
- ✅ Class timetable view (own batch only)
- ✅ Batch information
- ✅ Profile management
- ✅ Academic details

## 🔧 Quick Test Commands

### Test Backend API
```bash
# Test login
curl -X POST "http://localhost:8000/auth/login" \
  -H "Content-Type: application/json" \
  -d '{"username": "admin", "password": "admin123"}'

# Test admin dashboard (replace TOKEN with actual token)
curl -X GET "http://localhost:8000/admin/dashboard" \
  -H "Authorization: Bearer TOKEN"
```

### Test Frontend
1. Open http://localhost:5173
2. Login with any of the demo credentials
3. Explore the portal based on your role

## 🐛 Troubleshooting

### Backend Issues
- **Port 8000 in use**: Change port in uvicorn command
- **Database errors**: Run migrations again
- **Import errors**: Check Python dependencies

### Frontend Issues
- **Port 5173 in use**: Frontend will auto-assign new port
- **API connection errors**: Ensure backend is running on port 8000
- **Build errors**: Run `npm install` again

### Common Solutions
```bash
# Reset database
rm backend/dev.db
python -m backend.migrate_nep
python -m backend.migrate_auth
python -m backend.create_sample_users

# Clear frontend cache
cd frontend
rm -rf node_modules package-lock.json
npm install
```

## 🎯 Success Indicators

✅ **Backend Running**: See "Uvicorn running on http://0.0.0.0:8000"  
✅ **Frontend Running**: See "Local: http://localhost:5173"  
✅ **Login Working**: Can login with demo credentials  
✅ **Portals Working**: Can access role-specific features  

## 🚀 You're Ready!

Your complete multi-portal timetable system is now running with:
- ✅ **Authentication System** - Secure login/logout
- ✅ **Role-based Access** - Admin, Faculty, Student portals
- ✅ **NEP 2020 Compliance** - Enhanced scheduling
- ✅ **Real-time Timetables** - Live data from backend
- ✅ **Responsive UI** - Works on all devices

**Start exploring at: http://localhost:5173** 🎉
