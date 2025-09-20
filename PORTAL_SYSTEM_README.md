# Multi-Portal Timetable System

## 🎯 Overview

Complete multi-portal system with **Admin**, **Faculty**, and **Student** portals with role-based authentication and access control.

## 🚀 Features

### 🔐 Authentication System
- **JWT Token-based Authentication**
- **Role-based Access Control** (Admin, Faculty, Student)
- **Secure Password Hashing**
- **Session Management**

### 👨‍💼 Admin Portal
- **Full System Control**
- **User Management** (Create/View all users)
- **Timetable Generation** (Regular & NEP 2020)
- **System Dashboard** with statistics
- **Faculty & Student Management**

### 👨‍🏫 Faculty Portal
- **Personal Timetable View**
- **All Timetables Access** (can view any class timetable)
- **Profile Management**
- **Teaching Schedule Overview**

### 👨‍🎓 Student Portal
- **Class Timetable View** (own batch only)
- **Batch Information**
- **Profile Management**
- **Academic Details**

## 🛠️ Quick Setup

### 1. Install Dependencies
```bash
pip install python-jose[cryptography] passlib[bcrypt]
```

### 2. Run Database Migration
```bash
python -m backend.migrate_auth
```

### 3. Create Sample Users
```bash
python -m backend.create_sample_users
```

### 4. Start the Server
```bash
uvicorn backend.main:app --reload --host 0.0.0.0 --port 8000
```

## 🔑 Default Login Credentials

| Role | Username | Password | Access |
|------|----------|----------|---------|
| **Admin** | admin | admin123 | Full system control |
| **Faculty** | faculty1 | faculty123 | View all timetables |
| **Student** | student1 | student123 | View own timetable |

## 📊 API Endpoints

### Authentication
- `POST /auth/login` - Login with username/password
- `POST /auth/register` - Register new user (Admin only)
- `GET /auth/me` - Get current user info

### Admin Portal
- `GET /admin/dashboard` - System overview
- `GET /admin/users` - All users
- `GET /admin/faculty` - All faculty
- `GET /admin/students` - All students
- `POST /admin/generate-timetable/{batch_id}` - Generate timetable
- `GET /admin/timetables` - All timetables

### Faculty Portal
- `GET /faculty/profile` - Faculty profile
- `GET /faculty/my-timetable` - Personal timetable
- `GET /faculty/all-timetables` - All timetables
- `GET /faculty/timetable/{id}` - Specific timetable

### Student Portal
- `GET /student/profile` - Student profile
- `GET /student/my-timetable` - Class timetable
- `GET /student/batch-info` - Batch information

## 🔒 Security Features

- **JWT Token Authentication**
- **Password Hashing** with salt
- **Role-based Access Control**
- **Session Management**
- **Protected Endpoints**

## 🎯 Usage Examples

### Login
```bash
curl -X POST "http://localhost:8000/auth/login" \
  -H "Content-Type: application/json" \
  -d '{"username": "admin", "password": "admin123"}'
```

### Access Protected Endpoint
```bash
curl -X GET "http://localhost:8000/admin/dashboard" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN"
```

## 🎉 Ready to Use!

Your multi-portal timetable system is now ready with:
- ✅ **Admin Portal** - Full system control
- ✅ **Faculty Portal** - View all timetables
- ✅ **Student Portal** - View own timetable
- ✅ **Authentication** - Secure login system
- ✅ **NEP 2020 Support** - Enhanced scheduling
- ✅ **Role-based Access** - Proper permissions

**Access the API docs at: http://localhost:8000/docs**
