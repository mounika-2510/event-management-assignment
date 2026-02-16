#  Event Management Application

A full-stack MERN (MongoDB, Express.js, React.js, Node.js) application for discovering, browsing, and managing event registrations. Users can explore various events, register for events, manage their registrations through a personal dashboard, and more.

## 🌐 Live Demo

- **Frontend:** [https://event-management-inky-theta.vercel.app/](https://event-management-inky-theta.vercel.app/)
- **Backend API:** [https://event-management-backend-q916.onrender.com/](https://event-management-backend-q916.onrender.com/)

## ✨ Features

### User Features

- 🔐 **User Authentication** - Secure registration and login with JWT tokens
- 🎯 **Event Discovery** - Browse all available events with rich details
- 🔍 **Advanced Search & Filters** - Search by name, filter by category and location
- 📝 **Event Details** - View comprehensive information about each event
- ✅ **Event Registration** - Register for events with real-time seat availability
- ❌ **Cancel Registration** - Cancel event registrations anytime
- 📊 **Personal Dashboard** - Track upcoming and past event registrations
- 🔒 **Protected Routes** - Secure access to user-specific features
- 📱 **Responsive Design** - Works seamlessly on desktop, tablet, and mobile

### Technical Features

- 🚀 **Real-time Updates** - Automatic seat count management
- 🎨 **Modern UI/UX** - Clean and intuitive interface
- 🔄 **Auto-deploy** - Continuous deployment from GitHub
- 🌍 **Cloud Hosted** - Backend on Render, Frontend on Vercel
- 💾 **MongoDB Atlas** - Cloud-based database
- 🛡️ **Secure** - Password hashing, JWT authentication, CORS protection

## 🛠️ Tech Stack

### Frontend

- **React.js** - UI library for building user interfaces
- **React Router DOM** - Client-side routing
- **Axios** - HTTP requests
- **Context API** - Global state management
- **CSS3** - Custom styling with responsive design

### Backend

- **Node.js** - JavaScript runtime environment
- **Express.js** - Web application framework
- **MongoDB** - NoSQL database
- **Mongoose** - ODM for MongoDB
- **JWT** - JSON Web Tokens for authentication
- **bcryptjs** - Password hashing

### Deployment

- **Frontend:** Vercel
- **Backend:** Render
- **Database:** MongoDB Atlas

## 📋 Prerequisites

Before running this project locally, make sure you have:

- Node.js (v14 or higher)
- npm or yarn
- MongoDB Atlas account
- Git

## 🚀 Local Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/mounika-2510/event-management-assignment
cd event-management-assignment
```

### 2. Backend Setup

```bash
# Navigate to backend folder
cd backend

# Install dependencies
npm install

# Create .env file
touch .env
```

**Add these to `.env` file:**

```env
PORT=5000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_secret_key
```

**Seed the database with sample events:**

```bash
node seedEvents.js
```

**Start backend server:**

```bash
npm run dev
```

Backend will run on `http://localhost:5000`

### 3. Frontend Setup

Open a new terminal window:

```bash
# Navigate to frontend folder
cd frontend

# Install dependencies
npm install

# Start frontend application
npm start
```

Frontend will run on `http://localhost:3000`

## 📁 Project Structure

```
event-management-assignment/
│
├── backend/
│   ├── config/
│   │   └── db.js                 # Database connection
│   ├── middleware/
│   │   └── authMiddleware.js     # JWT authentication
│   ├── models/
│   │   ├── User.js               # User schema
│   │   ├── Event.js              # Event schema
│   │   └── Registration.js       # Registration schema
│   ├── routes/
│   │   ├── authRoutes.js         # Auth endpoints
│   │   ├── eventRoutes.js        # Event CRUD endpoints
│   │   └── registrationRoutes.js # Registration endpoints
│   ├── .env                      # Environment variables
│   ├── .gitignore
│   ├── package.json
│   ├── seedEvents.js             # Database seeding
│   ├── server.js                 # Entry point
│   └── vercel.json               # Vercel config
│
└── frontend/
    ├── public/
    │   └── index.html
    ├── src/
    │   ├── components/
    │   │   ├── EventCard.js      # Event card component
    │   │   ├── Navbar.js         # Navigation bar
    │   │   └── ProtectedRoute.js # Route protection
    │   ├── context/
    │   │   └── AuthContext.js    # Auth state management
    │   ├── pages/
    │   │   ├── Dashboard.js      # User dashboard
    │   │   ├── EventDetails.js   # Event details page
    │   │   ├── Events.js         # Events listing
    │   │   ├── Login.js          # Login page
    │   │   └── Register.js       # Registration page
    │   ├── App.css               # Global styles
    │   ├── App.js                # Main component
    │   ├── config.js             # API configuration
    │   └── index.js              # Entry point
    ├── .gitignore
    ├── package.json
    └── vercel.json               # Vercel config
```

## 🔌 API Endpoints

### Authentication Routes (Public)

| Method | Endpoint           | Description       |
| ------ | ------------------ | ----------------- |
| POST   | `/api/auth/signup` | Register new user |
| POST   | `/api/auth/login`  | Login user        |

**Request Body (Signup):**

```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "password123"
}
```

**Response:**

```json
{
  "message": "User created successfully",
  "token": "jwt_token_here",
  "user": {
    "id": "user_id",
    "name": "John Doe",
    "email": "john@example.com"
  }
}
```

### Event Routes (Public)

| Method | Endpoint                          | Description        |
| ------ | --------------------------------- | ------------------ |
| GET    | `/api/events`                     | Get all events     |
| GET    | `/api/events?search=keyword`      | Search events      |
| GET    | `/api/events?category=Technology` | Filter by category |
| GET    | `/api/events?location=Bangalore`  | Filter by location |
| GET    | `/api/events/:id`                 | Get single event   |
| POST   | `/api/events`                     | Create new event   |
| PUT    | `/api/events/:id`                 | Update event       |
| DELETE | `/api/events/:id`                 | Delete event       |

### Registration Routes (Protected - Requires JWT Token)

| Method | Endpoint                       | Description         |
| ------ | ------------------------------ | ------------------- |
| POST   | `/api/registrations/:eventId`  | Register for event  |
| DELETE | `/api/registrations/:eventId`  | Cancel registration |
| GET    | `/api/registrations/my-events` | Get user's events   |

**Headers Required:**

```
Authorization: Bearer <jwt_token>
```

## 📊 Database Schema

### User Model

```javascript
{
  name: String,
  email: String (unique, lowercase),
  password: String (hashed),
  createdAt: Date,
  updatedAt: Date
}
```

### Event Model

```javascript
{
  name: String,
  organizer: String,
  location: String,
  date: Date,
  description: String,
  capacity: Number,
  availableSeats: Number,
  category: String,
  createdAt: Date,
  updatedAt: Date
}
```

### Registration Model

```javascript
{
  userId: ObjectId (ref: User),
  eventId: ObjectId (ref: Event),
  registeredAt: Date,
  createdAt: Date,
  updatedAt: Date
}
```

## 🎯 Event Categories

- Technology
- Music
- Sports
- Business
- Arts
- Entertainment
- Health

## 📍 Available Locations

- Bangalore
- Mumbai
- Delhi
- Hyderabad
- Pune
- Chennai
- Goa

## 🌐 Deployment Guide

### Backend Deployment (Render)

1. Push code to GitHub
2. Go to [render.com](https://render.com)
3. Create new Web Service
4. Connect GitHub repository
5. Configure:
   - **Root Directory:** `backend`
   - **Build Command:** `npm install`
   - **Start Command:** `node server.js`
6. Add environment variables:
   - `MONGO_URI`
   - `JWT_SECRET`
   - `NODE_ENV=production`
7. Deploy

### Frontend Deployment (Vercel)

1. Push code to GitHub
2. Go to [vercel.com](https://vercel.com)
3. Import repository
4. Configure:
   - **Root Directory:** `frontend`
   - **Framework:** Create React App
   - **Build Command:** `npm run build`
   - **Output Directory:** `build`
5. Add environment variable:
   - `REACT_APP_API_URL=https://your-backend-url.onrender.com/api`
6. Deploy

## ⚙️ Environment Variables

### Backend (.env)

```env
PORT=5000
MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/event_management
JWT_SECRET=your_secret_key_here
NODE_ENV=production
```

### Frontend (Vercel Dashboard)

```env
REACT_APP_API_URL=https://your-backend-url.onrender.com/api
```

## 🐛 Common Issues & Solutions

### Issue: "Cannot connect to MongoDB"

**Solution:**

- Check MongoDB Atlas connection string
- Ensure IP whitelist includes `0.0.0.0/0`
- Verify database name in connection string

### Issue: "CORS Error"

**Solution:**

- Update backend CORS to include frontend URL
- Verify frontend URL in `server.js`

### Issue: "Token expired"

**Solution:**

- Login again to get new token
- Check JWT_SECRET matches in both environments

### Issue: "Event registration failed"

**Solution:**

- Check if event is full (availableSeats = 0)
- Verify user is not already registered
- Check authentication token is valid

## 📸 Screenshots

### Home Page

![Home Page](https://res.cloudinary.com/drecb9hgv/image/upload/v1771231569/Screenshot_2026-02-16_141455_tnzptz.png)

### Event Details

![Event Details](https://res.cloudinary.com/drecb9hgv/image/upload/v1771231803/Screenshot_2026-02-16_141945_v3j4ol.png)

### Dashboard

![Dashboard](https://res.cloudinary.com/drecb9hgv/image/upload/v1771231565/Screenshot_2026-02-16_141432_at4epf.png)

## 👨‍💻 Author

**Mounika Vemula**

- GitHub: [@mounika-2510](https://github.com/mounika-2510)
- Email: vemulamounika540@gmail.com

## 📄 License

This project is created for educational purposes as part of a job assignment.

## 🙏 Acknowledgments

- MongoDB Atlas for database hosting
- Render for backend hosting
- Vercel for frontend hosting
- React.js team for the amazing library
- Express.js team for the web framework
- Bellcorp Studio for the opportunity

---

**Built with ❤️ using MERN Stack**

