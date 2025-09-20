# 🎯 Quizling - Modern Quiz Platform
A comprehensive quiz platform built with React, TypeScript, Node.js, and MongoDB. Features role-based access control, multiple correct answers, real-time analytics, and a modern responsive design.

## ✨ Features

### 🎓 **For Students**
- Take interactive quizzes with multiple correct answer support
- View detailed results with question-by-question breakdown
- Track performance history and progress
- Responsive design for mobile and desktop

### 👨‍🏫 **For Professors**
- Create and manage question sets
- View student results and performance analytics
- Question-level statistics and insights
- Score distribution analysis

### 🔧 **For Administrators**
- Complete user management with CRUD operations
- Role assignment and permission management
- System-wide analytics and statistics
- User search and filtering capabilities

### 🎨 **Modern UI/UX**
- Mobile-first responsive design
- Toast notifications for user feedback
- Loading states with skeleton screens
- Intuitive navigation with hamburger menu

## 🚀 Quick Start

### Prerequisites

- **Node.js** (v18 or higher)
- **MongoDB** (v4.4 or higher)
- **npm** or **yarn**

### Local Startup

Start backend and frontend locally:

```bash
# Option A: One command (simple)
./start.sh

# Option B: One command with preflight checks (MongoDB, .env)
./start-simple.sh

# Option C: Manual start
# Backend
cd backend
npm install
npm run dev

# Frontend
cd ../frontend
npm install
npm run dev
```

Notes:
- The `start-simple.sh` script checks MongoDB, creates `backend/.env` from `env.example` if missing, and starts both servers.
- The `start.sh` script simply starts both servers without checks.
- The frontend runs on `http://localhost:5173`. Use `npm run dev:flexible` to allow any available port if 5173 is occupied.

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/quizling.git
cd quizling
```

### 2. Backend Setup

```bash
cd backend

# Install dependencies
npm install

# Create environment file
cp env.example .env
```

#### Environment Configuration

Create a `.env` file in the `backend` directory:

```env
# Database Configuration
MONGODB_URI=mongodb://localhost:27017/quizling
DB_NAME=quizling

# JWT Configuration
JWT_SECRET=your-super-secret-jwt-key-here-make-it-long-and-random
JWT_EXPIRES_IN=7d

# Server Configuration
PORT=5001
NODE_ENV=development

# CORS Configuration
CORS_ORIGIN=http://localhost:5173
```

#### Start MongoDB

Make sure MongoDB is running on your system:

```bash
# macOS (with Homebrew)
brew services start mongodb-community

# Ubuntu/Debian
sudo systemctl start mongod

# Windows
net start MongoDB
```

#### Start Backend Server

```bash
npm run dev
```

The backend will be available at `http://localhost:5001`

### 3. Frontend Setup

```bash
cd ../frontend

# Install dependencies
npm install

# Start development server
npm run dev
```

The frontend will be available at `http://localhost:5173`

### 4. Seed Database (Optional)

```bash
cd backend
npm run seed
```

This creates sample users:
- **Admin**: admin@quizling.com / admin123
- **Professor**: professor@quizling.com / prof123
- **Student**: student@quizling.com / student123

## 📁 Project Structure

```
quizling/
├── backend/                 # Node.js + Express API
│   ├── config/              # Database configuration
│   ├── controllers/         # Route controllers
│   ├── middleware/          # Authentication & RBAC
│   ├── models/              # MongoDB models
│   ├── routes/              # API routes
│   ├── seed/                # Database seeding
│   ├── validators/          # Input validation schemas
│   └── server.js            # Entry point
├── frontend/                # React + TypeScript app
│   ├── public/              # Static assets
│   └── src/
│       ├── api/             # API client
│       ├── components/      # Reusable components
│       ├── context/         # React contexts
│       ├── pages/           # Page components
│       ├── routes/          # Route guards
│       ├── types/           # TypeScript types
│       └── App.tsx          # Main app component
├── start.sh                 # Start both backend and frontend
├── start-simple.sh          # Simplified starter with checks
└── quiz.md                  # Project design overview
```

## 🔧 API Endpoints

### Authentication
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `GET /api/auth/me` - Get current user

### Profile Management
- `PUT /api/me/profile` - Update user profile
- `PUT /api/me/password` - Change password

### User Management (Admin Only)
- `GET /api/users` - List all users
- `POST /api/users` - Create new user
- `PUT /api/users/:id` - Update user
- `PUT /api/users/:id/role` - Update user role
- `DELETE /api/users/:id` - Delete user

### Question Sets
- `GET /api/question-sets` - List question sets
- `POST /api/question-sets` - Create question set
- `PUT /api/question-sets/:id` - Update question set
- `DELETE /api/question-sets/:id` - Delete question set
- `GET /api/question-sets/my/results` - Professor analytics
- `GET /api/question-sets/:id/analytics` - Detailed analytics

### Quiz Attempts
- `POST /api/attempts` - Submit quiz attempt
- `GET /api/attempts` - Get attempt history
- `GET /api/attempts/:id` - Get attempt details

## 🛠️ Development

### Backend Development

```bash
cd backend

# Development with auto-reload
npm run dev
```

### Frontend Development

```bash
cd frontend

# Development server (default port 5173)
npm run dev

# Development server (any free port)
npm run dev:flexible

# Build for production
npm run build

# Preview production build
npm run preview
```

## 🚀 Deployment

### Backend Deployment

1. **Environment Variables**: Set production environment variables
2. **Database**: Use MongoDB Atlas or hosted MongoDB
3. **Platform**: Deploy to Render, Heroku, or similar

### Frontend Deployment

1. **Build**: Run `npm run build`
2. **Platform**: Deploy to Vercel, Netlify, or similar
3. **Environment**: The frontend auto-detects the current hostname and targets backend port `5001` by default. Set up your reverse proxy or environment so the backend is reachable from the deployed domain.

Development CORS is permissive for `localhost` in the backend. For production, set `CORS_ORIGIN` to your frontend domain.

## 🔒 Security Features

- **JWT Authentication** with secure token handling
- **Password Hashing** using bcrypt
- **Input Validation** with Joi schemas
- **CORS Protection** for cross-origin requests
- **Helmet** for security headers
- **Role-Based Access Control** (RBAC)

## 🎨 Tech Stack

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **MongoDB** - Database
- **Mongoose** - ODM
- **JWT** - Authentication
- **Joi** - Input validation
- **bcrypt** - Password hashing

### Frontend
- **React 19** - UI library
- **TypeScript** - Type safety
- **Vite 7** - Build tool
- **MUI 7** - Component library
- **React Router 7** - Navigation
- **React Hook Form** - Form handling
- **Axios** - HTTP client

## 📊 Current Status

- **Overall Progress**: 95%
- **Backend**: 95% complete
- **Frontend**: 90% complete
- **Core Features**: 100% complete
- **User Management**: 100% complete
- **UI/UX**: 95% complete

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built with modern web technologies
- Inspired by educational technology needs
- Designed for scalability and maintainability

---

**Made with ❤️ for educators and students worldwide**
