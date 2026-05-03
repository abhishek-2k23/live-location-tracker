# Live Location Tracker

A real-time collaborative location tracking application that enables users to share and monitor live geolocation data in real-time using WebSocket technology.

**[🚀 Live Demo](https://live-location-qwdk.onrender.com/)**

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [Project Structure](#project-structure)
- [API Endpoints](#api-endpoints)
- [WebSocket Events](#websocket-events)
- [Contributing](#contributing)

---

## 📖 Overview

Live Location Tracker is a full-stack web application that allows multiple users to authenticate, share their real-time location, and view the locations of other connected users on an interactive map. The application leverages WebSocket technology for instant location synchronization, providing a seamless collaborative experience.

### Use Cases
- Track delivery personnel in real-time
- Monitor team member locations during field operations
- Collaborative location sharing among friends or family
- Real-time situational awareness applications

---

## ✨ Features

- **Real-Time Location Updates**: Instant geolocation sharing across all connected users using WebSockets
- **User Authentication**: Secure JWT-based authentication system
- **Interactive Map**: Interactive map interface using Leaflet for location visualization
- **Online Status Tracking**: Real-time user online/offline status updates
- **Multi-User Support**: Support for multiple concurrent users with individual location tracking
- **Responsive Design**: Mobile-friendly and responsive user interface
- **Secure Communication**: CORS-enabled and JWT-protected WebSocket connections

---

## 🛠️ Tech Stack

### Frontend
- **React 18.3** - UI library for building interactive components
- **Vite 5.4** - Next-generation frontend build tool for fast development
- **Leaflet 1.9** - Open-source library for interactive maps
- **React-Leaflet 4.2** - React components for Leaflet maps
- **Socket.IO Client 4.7** - Real-time bidirectional communication library

### Backend
- **Node.js** - JavaScript runtime environment
- **Express.js 4.19** - Minimal and flexible web framework
- **Socket.IO 4.7** - Real-time communication framework
- **JWT (jsonwebtoken 9.0)** - Secure token-based authentication
- **CORS 2.8** - Cross-Origin Resource Sharing middleware
- **Dotenv** - Environment variable management

---

## 📦 Prerequisites

Before you begin, ensure you have the following installed on your system:

- **Node.js** (v16 or higher)
- **npm** (v7 or higher) or **pnpm**
- **Git** (for cloning the repository)

To verify your installations, run:
```bash
node --version
npm --version
git --version
```

---

## 🚀 Installation

### Step 1: Clone the Repository

```bash
git clone https://github.com/abhishek-2k23/live-location-tracker
cd live-location-tracker
```

### Step 2: Install Backend Dependencies

```bash
npm install
```

### Step 3: Install Frontend Dependencies

```bash
cd frontend
npm install
cd ..
```

---

## ⚙️ Configuration

### Step 1: Create Environment File

Create a `.env` file in the root directory of the project:

```bash
touch .env
```

### Step 2: Configure Environment Variables

Add the following variables to your `.env` file:

```env
# Server Configuration
PORT=3001

# JWT Configuration
JWT_SECRET=your-super-secret-key-here
JWT_EXPIRY=12h

# CORS Configuration
CORS_ORIGIN=*
```

**Important**: For production, use a strong, unique `JWT_SECRET` and restrict `CORS_ORIGIN` to specific domains.

---

## ▶️ Running the Application

### Development Mode

#### Terminal 1 - Start the Backend Server
```bash
npm start
```
The server will run on `http://localhost:3001` (or the port specified in `.env`)

#### Terminal 2 - Start the Frontend Development Server
```bash
cd frontend
npm run dev
```
The frontend will typically run on `http://localhost:5173`

### Production Build

#### Build the Frontend
```bash
npm run build
```

#### Start the Server
```bash
npm start
```

The application will serve the built frontend from the backend server at `http://localhost:3001`

---

## 📁 Project Structure

```
live-location-tracker/
├── src/
│   ├── server.js              # Express server configuration and routes
│   └── socket.js              # WebSocket event handlers and real-time logic
├── frontend/
│   ├── src/
│   │   ├── App.jsx            # Main React application component
│   │   └── components/        # React components
│   ├── index.html             # HTML entry point
│   ├── package.json           # Frontend dependencies
│   └── vite.config.js         # Vite configuration
├── .env                       # Environment variables (create this file)
├── .gitignore                 # Git ignore rules
├── package.json               # Backend dependencies
└── readme.md                  # This file
```

---

## 🔌 API Endpoints

### Authentication

#### POST `/api/login`
Authenticates a user and returns a JWT token.

**Request Body:**
```json
{
  "username": "john_doe"
}
```

**Response (200 OK):**
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "userId": "usr_am9objpk",
  "username": "john_doe"
}
```

**Error Response (400 Bad Request):**
```json
{
  "error": "Username required"
}
```

---

## 📡 WebSocket Events

The application uses Socket.IO for real-time communication. All events require a valid JWT token.

### Client → Server Events

#### `location_update`
Emitted when a user's location changes.

**Data:**
```javascript
{
  latitude: 40.7128,
  longitude: -74.0060,
  accuracy: 10,
  timestamp: 1234567890
}
```

### Server → Client Events

#### `location_update`
Broadcasted to all connected clients when any user's location changes or when a user connects/disconnects.

**Data:**
```javascript
{
  userId: "usr_am9objpk",
  username: "john_doe",
  location: {
    latitude: 40.7128,
    longitude: -74.0060,
    accuracy: 10
  },
  timestamp: 1234567890,
  status: "online" // or "offline"
}
```

---

## 🔒 Authentication Flow

1. User enters username on login page
2. Frontend sends POST request to `/api/login`
3. Backend generates JWT token with user credentials
4. Frontend stores token in localStorage
5. Token is attached to WebSocket connection handshake
6. Backend verifies token middleware before processing WebSocket events
7. Authenticated users receive real-time location updates

---

## 🌐 Deployment

### Deploying to Render

1. Push your code to GitHub
2. Connect your GitHub repository to [Render](https://render.com)
3. Create a new Web Service
4. Configure environment variables in Render dashboard
5. Set build command: `npm run build`
6. Set start command: `npm start`
7. Deploy!

---

## 📝 Usage

1. Open the application in your browser
2. Enter a username and click "Login"
3. Allow location access when prompted
4. Your location will be shared in real-time on the map
5. See other connected users' locations update in real-time
6. Users appear/disappear as they connect/disconnect

---

## 🐛 Troubleshooting

### Issue: "Token missing" error
- Ensure you're using a valid JWT token
- Clear browser localStorage and re-login
- Check that JWT_SECRET in .env is consistent

### Issue: Location not updating
- Check browser console for JavaScript errors
- Ensure location permissions are granted
- Verify WebSocket connection status in browser DevTools

### Issue: CORS errors
- Check CORS_ORIGIN setting in .env
- For local development, ensure both frontend and backend are running
- Review browser console for specific CORS error details

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

## 👨‍💻 Author

Created by Abhishek (Cohort 26)

**Live Demo**: [https://live-location-qwdk.onrender.com/](https://live-location-qwdk.onrender.com/)

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to:

1. Fork the repository
2. Create a new branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📧 Support

For support, please open an issue on the GitHub repository or contact the project maintainer.

---

**Last Updated**: May 2026
