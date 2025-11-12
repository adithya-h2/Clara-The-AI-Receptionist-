# CLARA - Unified Communication Platform

<div align="center">

![CLARA](https://img.shields.io/badge/CLARA-Platform-blue?style=for-the-badge)
![TypeScript](https://img.shields.io/badge/TypeScript-5.6-blue?logo=typescript)
![React](https://img.shields.io/badge/React-19.2-blue?logo=react)
![Node.js](https://img.shields.io/badge/Node.js-18+-green?logo=node.js)

**A comprehensive real-time communication platform with WebRTC video calling, AI-powered chat, and staff management capabilities.**

[Features](#-features) • [Quick Start](#-quick-start) • [Documentation](#-documentation) • [API Reference](#-api-reference)

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Architecture](#-architecture)
- [Prerequisites](#-prerequisites)
- [Quick Start](#-quick-start)
- [Development](#-development)
- [Production Deployment](#-production-deployment)
- [API Reference](#-api-reference)
- [Configuration](#-configuration)
- [Testing](#-testing)
- [Docker Deployment](#-docker-deployment)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)
- [License](#-license)

## 🎯 Overview

CLARA is a unified monorepo platform that provides real-time video communication between clients and staff members. Built with modern web technologies, it offers a seamless experience for video calling, AI-powered chat assistance, staff availability management, and comprehensive notification systems.

### Key Capabilities

- **Real-time WebRTC Video Calls**: High-quality peer-to-peer video communication with reliable signaling
- **AI Chat Assistant**: Google Gemini-powered conversational AI for enhanced user interactions
- **Staff Management**: Availability tracking, skills-based routing, and team coordination
- **Notification System**: Real-time notifications with sync and persistence
- **Meeting & Task Management**: Schedule meetings, manage timetables, and track tasks
- **Team Directory**: Group chat and team collaboration features

## ✨ Features

### Core Features

- 🎥 **WebRTC Video Calls**
  - Real-time peer-to-peer video communication
  - CAS-protected call lifecycles to prevent race conditions
  - Reliable SDP/ICE signaling over Socket.IO
  - TURN server support for NAT traversal
  - Automatic call timeout handling

- 🔐 **Authentication & Security**
  - JWT-based authentication with refresh tokens
  - Staff login and auto-login demo mode
  - CORS protection and rate limiting
  - Payload validation with Zod

- 👥 **Staff Availability System**
  - Real-time staff presence tracking
  - Skills-based call routing
  - Availability status management
  - Multi-organization support

- 🔔 **Notification System**
  - Real-time notifications via Socket.IO
  - Unread tracking and marking
  - Cross-platform synchronization
  - Notification persistence

- 🤖 **AI Chat Assistant**
  - Google Gemini integration
  - Enhanced conversational capabilities
  - Context-aware responses

- 📅 **Management Tools**
  - Meeting scheduling and management
  - Personal timetable with persistence
  - Task tracking and management
  - Team directory with group chat

### Technical Features

- **Feature-flagged Architecture**: Safe deployment with `ENABLE_UNIFIED_MODE` flag
- **PostgreSQL Integration**: Persistent state with in-memory fallback
- **Monorepo Structure**: Shared packages for types and utilities
- **TypeScript**: Full type safety across the codebase
- **Development Tools**: Encoding validation, health checks, and status monitoring

## 🏗️ Architecture

CLARA follows a monorepo architecture with the following structure:



### Technology Stack

**Frontend:**
- React 19.2 with TypeScript
- Vite for build tooling
- Socket.IO Client for real-time communication
- Zustand for state management
- Framer Motion for animations

**Backend:**
- Node.js with Express
- Socket.IO for WebSocket communication
- PostgreSQL for data persistence
- JWT for authentication
- Zod for schema validation

## 📦 Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** 18 or higher
- **npm** or **pnpm** package manager
- **PostgreSQL** (optional, falls back to in-memory storage)
- **Git** for version control

## 🚀 Quick Start

### 1. Clone the Repository

git clone <repository-url>
cd clara-monorepo### 2. Install Dependencies

npm install### 3. Configure Environment

cp env.example .envEdit `.env` with your configuration:
v
NODE_ENV=development
SERVER_PORT=8080
JWT_SECRET=your-secret-key-here
ENABLE_UNIFIED_MODE=true
DATABASE_URL=postgres://user:pass@localhost:5432/clara
GEMINI_API_KEY=your-gemini-api-key### 4. Start Development Servers

npm run devThis starts all services:
- **Client App**: http://localhost:5173
- **Staff App**: http://localhost:5174
- **Server**: http://localhost:8080

## 💻 Development

### Available Scripts

# Start all services in development mode
npm run dev

# Start individual services
npm run dev:server      # Server only
npm run dev:client      # Client only
npm run dev:staff       # Staff only

# Build for production
npm run build

# Run tests
npm test

# Lint code
npm run lint

# Format code
npm run format

# Check encoding issues
npm run check:encoding
npm run fix:encoding### Development Workflow

1. **Server Development**: The server runs on port 8080 and provides:
   - REST API endpoints at `/api/*`
   - WebSocket connections at `/socket`
   - Health check at `/healthz`

2. **Client Development**: The client app runs on port 5173 with hot module replacement

3. **Staff Development**: The staff app runs on port 5174 with hot module replacement

### Windows-Specific Scripts

For Windows users, helper scripts are available:

# PowerShell
.\scripts\start-dev.ps1

# Command Prompt
scripts\start-dev.batThese scripts automatically handle port conflicts and start all services.

## 🚢 Production Deployment

### 1. Build All Applications
sh
npm run build### 2. Configure Production Environment

Set `ENABLE_UNIFIED_MODE=true` in your `.env` file:

ENABLE_UNIFIED_MODE=true
NODE_ENV=production### 3. Start Production Server

npm startThe server will serve:
- `/` → Client application
- `/staff` → Staff application
- `/api/*` → REST API endpoints
- `/socket` → WebSocket connections

### Docker Deployment

cd infra
docker-compose up -dSee `infra/docker-compose.yml` for configuration details.

## 📡 API Reference

### Authentication

- `POST /api/auth/login` - Authenticate and receive JWT tokens
- `POST /api/auth/refresh-token` - Refresh access token
- `POST /api/auth/logout` - Logout and invalidate tokens

### Call Management

- `POST /api/v1/calls` - Initiate a new video call
- `POST /api/v1/calls/:callId/accept` - Accept an incoming call
- `POST /api/v1/calls/:callId/decline` - Decline an incoming call
- `POST /api/calls/sdp` - Send WebRTC SDP offer/answer
- `POST /api/calls/ice` - Send WebRTC ICE candidate

### Staff Management

- `GET /api/v1/staff/available` - Get available staff members
- `POST /api/v1/staff/availability` - Set staff availability status
- `GET /api/v1/staff/:staffId` - Get staff member details

### Notifications

- `GET /api/notifications` - Get all notifications
- `GET /api/notifications/unread` - Get unread notifications
- `POST /api/notifications/:id/read` - Mark notification as read
- `POST /api/notifications/read-all` - Mark all notifications as read

### Health Check

- `GET /healthz` - Server health status

### Socket.IO Events

**Client → Server:**
- `call.initiate` - Initiate a call
- `call.accept` - Accept a call
- `call.decline` - Decline a call
- `webrtc.sdp` - Send SDP offer/answer
- `webrtc.ice` - Send ICE candidate

**Server → Client:**
- `call.initiated` - Call initiated notification
- `call.accepted` - Call accepted notification
- `call.declined` - Call declined notification
- `call.missed` - Call missed notification
- `call.ended` - Call ended notification
- `webrtc.sdp` - Receive SDP offer/answer
- `webrtc.ice` - Receive ICE candidate

## ⚙️ Configuration

### Environment Variables

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| `NODE_ENV` | Environment mode | `development` | No |
| `SERVER_PORT` | Server port | `8080` | No |
| `JWT_SECRET` | JWT signing secret | - | Yes |
| `ENABLE_UNIFIED_MODE` | Enable unified server mode | `false` | No |
| `DATABASE_URL` | PostgreSQL connection string | - | No |
| `GEMINI_API_KEY` | Google Gemini API key | - | No |
| `CORS_ORIGINS` | Allowed CORS origins | - | No |
| `RING_TIMEOUT_MS` | Call ring timeout (ms) | `45000` | No |
| `TURN_SERVER_URL` | TURN server URL | - | No |
| `TURN_USERNAME` | TURN server username | - | No |
| `TURN_CREDENTIAL` | TURN server password | - | No |

See `env.example` for the complete list of configuration options.

## 🧪 Testing

The project includes a comprehensive test suite located in `testsprite_tests/`:

# Run all tests
npm test

# Run specific test file
cd testsprite_tests
python TC001_health_check_endpoint_should_return_server_status_ok.py### Test Coverage

The test suite covers:
- ✅ Health check endpoints
- ✅ Authentication and JWT tokens
- ✅ Call initiation, acceptance, and decline
- ✅ Staff availability management
- ✅ Notification system
- ✅ WebRTC signaling (SDP/ICE exchange)
- ✅ Socket.IO event handling
- ✅ Timetable management
- ✅ Complete call workflows

## 🐳 Docker Deployment

### Using Docker Compose

cd infra
docker-compose up -d### Manual Docker Build

cd apps/server
docker build -t clara-server .
docker run -p 8080:8080 --env-file .env clara-server## 🔧 Troubleshooting

### Port Already in Use

If port 8080 is already in use:

**Windows PowerShell:**
Get-NetTCPConnection -LocalPort 8080
Stop-Process -Id <PID> -Force**Windows CMD:**md
netstat -ano | findstr ":8080"
taskkill /PID <PID> /F**Linux/Mac:**
lsof -ti:8080 | xargs kill -9### Connection Errors

1. Verify server is running: Check for "Server listening on :8080" in logs
2. Test health endpoint: `curl http://localhost:8080/healthz`
3. Check CORS configuration in environment variables
4. Verify Socket.IO path matches client configuration

### Encoding Issues

# Check for encoding issues
npm run check:encoding

# Fix encoding issues automatically
npm run fix:encoding### Database Connection

If PostgreSQL is not available, the server will automatically fall back to in-memory storage. For production, ensure `DATABASE_URL` is properly configured.

## 📚 Documentation

Additional documentation is available:

- [Development Start Guide](DEV_START_GUIDE.md) - Detailed development setup
- [Integration Guide](INTEGRATION_GUIDE.md) - Production WebRTC integration
- [Production WebRTC Implementation](PRODUCTION_WEBRTC_IMPLEMENTATION.md) - WebRTC architecture details
- [Security and Encoding Fix](SECURITY_AND_ENCODING_FIX.md) - Security considerations

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines

- Follow TypeScript best practices
- Write tests for new features
- Update documentation as needed
- Ensure all tests pass before submitting PR

## 📄 License

This project is private and proprietary. All rights reserved.

---

<div align="center">

**Built with ❤️ by the CLARA Team**

[Report Bug](https://github.com/your-repo/issues) • [Request Feature](https://github.com/your-repo/issues) • [Documentation](#-documentation)

</div>
