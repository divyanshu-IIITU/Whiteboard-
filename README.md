# 🎨 Real-Time Collaborative Whiteboard

A real-time collaborative whiteboard application that allows multiple users to draw and collaborate on the same canvas simultaneously.

The application combines **real-time WebSocket communication, interactive canvas rendering, authentication, authorization, and persistent storage** to provide a responsive collaborative drawing experience.

## ✨ Features

- 🔄 **Real-Time Collaboration**
  - Multiple users can work on the same whiteboard simultaneously.
  - Real-time synchronization using Socket.IO/WebSockets.

- 🖊️ **Freehand Drawing**
  - Smooth freehand drawing using `perfect-freehand`.
  - Vector-based drawing using `Rough.js`.

- ⚡ **High-Performance Rendering**
  - Optimized Canvas rendering targeting **60 FPS** for a smooth drawing experience.

- ↩️ **Undo / Redo**
  - State-machine-based Undo/Redo system.
  - Efficient element serialization and client-side state reconciliation.

- 🔐 **Authentication & Authorization**
  - JWT-based authentication.
  - Role-Based Access Control (RBAC) for collaborative rooms.

- 💾 **Persistent Whiteboard State**
  - Whiteboard/vector data is persisted using MongoDB.
  - Users can retain their collaborative workspace state.

## 🏗️ Architecture

The application follows a client-server architecture:

```text
                    ┌─────────────────────┐
                    │       Client        │
                    │   React Frontend    │
                    │                     │
                    │  Canvas Rendering   │
                    │  Drawing Engine     │
                    └──────────┬──────────┘
                               │
                         HTTP / WebSocket
                               │
                               ▼
                    ┌─────────────────────┐
                    │       Server        │
                    │ Node.js / Express   │
                    │                     │
                    │ Socket.IO           │
                    │ Authentication      │
                    │ Authorization       │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │      MongoDB        │
                    │                     │
                    │ Whiteboard State    │
                    │ User / Room Data    │
                    └─────────────────────┘
```

## 🔄 Real-Time Synchronization

The core of the application is the real-time synchronization layer.

When a user performs an action on the canvas:

```text
User Action
     │
     ▼
Canvas State Update
     │
     ▼
Socket.IO Event
     │
     ▼
Server
     │
     ├──────────────► Other Connected Users
     │
     ▼
State Persistence
     │
     ▼
MongoDB
```

This allows changes made by one participant to be propagated to other users in the same collaborative room.

## 🧠 State Management

The application uses a **state-machine-based Undo/Redo architecture**.

Instead of directly mutating the canvas state, drawing operations are represented as state transitions.

```text
             ┌──────────────┐
             │ Current State│
             └──────┬───────┘
                    │
              User Action
                    │
                    ▼
             ┌──────────────┐
             │ New State    │
             └──────┬───────┘
                    │
              Serialization
                    │
                    ▼
             Shared State
```

This approach helps maintain consistency between the local canvas and synchronized collaborative state.

## 🔐 Security

The application implements:

- JWT-based authentication
- Role-Based Access Control (RBAC)
- Protected collaborative rooms
- Server-side authorization
- Persistent user and room state

RBAC ensures that users only perform actions permitted by their role within a collaborative room.

## 🛠️ Tech Stack

### Frontend

- React.js
- Canvas API
- Rough.js
- perfect-freehand
- Tailwind CSS

### Backend

- Node.js
- Express.js
- Socket.IO

### Database

- MongoDB

### Authentication

- JWT
- Role-Based Access Control

### Development

- Git
- GitHub

## 📁 Project Structure

```text
Whiteboard/
│
├── client/
│   ├── components/
│   ├── pages/
│   ├── hooks/
│   ├── utils/
│   └── ...
│
├── server/
│   ├── controllers/
│   ├── routes/
│   ├── middleware/
│   ├── sockets/
│   ├── models/
│   └── ...
│
├── package.json
├── README.md
└── ...
```

> Update the structure above if your repository uses different directory names.

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/divyanshu-IIITU/Whiteboard-.git
cd Whiteboard-
```

### 2. Install Dependencies

```bash
npm install
```

If the frontend and backend are separate applications, install dependencies inside each respective directory.

### 3. Configure Environment Variables

Create the required `.env` file(s) and configure your database, authentication, and server settings.

Example:

```env
PORT=5000
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
```

> Use the exact environment variable names required by the project source code.

### 4. Start the Application

```bash
npm run dev
```

The application should then be available at the configured local development URL.

## 🎯 Engineering Highlights

This project focuses on several practical software engineering challenges:

### Real-Time Systems

Designed real-time communication using WebSockets to synchronize changes between multiple connected clients.

### Performance

Built an optimized canvas rendering pipeline targeting **60 FPS**, reducing unnecessary rendering overhead during drawing operations.

### Distributed State

Handled synchronization between local client state, server-side events, and persistent MongoDB state.

### State Management

Implemented state-machine-based Undo/Redo and efficient element serialization to maintain consistent drawing state.

### Security

Implemented JWT authentication and RBAC to protect collaborative rooms and restrict unauthorized operations.

## 🔮 Future Improvements

Potential improvements include:

- Persistent version history
- Conflict resolution for simultaneous edits
- Cursor/presence indicators
- Board sharing through invite links
- Image/file uploads
- Export boards as PNG/PDF
- Offline editing and synchronization
- Redis-based Socket.IO scaling
- Horizontal server scaling
- Automated testing and CI/CD

## 👨‍💻 Author

**Divyanshu Singh Katiyar**

B.Tech Computer Science & Engineering (Cybersecurity)  
Indian Institute of Information Technology, Una

- GitHub: https://github.com/divyanshu-IIITU
- LinkedIn: https://www.linkedin.com/in/divyanshu-singh-katiyar-149773311/

---

⭐ If you find this project useful, consider giving the repository a star.
