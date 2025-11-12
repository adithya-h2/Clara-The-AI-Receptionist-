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
