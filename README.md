# Voting Application - DevOps Challenge

![Architecture Diagram](./architecture.excalidraw.png)

# Voting Application - DevOps Challenge

## Project Overview
Distributed voting application with multiple microservices:

- **Vote Service (`/vote`)**: Python Flask app for voting.
- **Result Service (`/result`)**: Node.js app for real-time results.
- **Worker Service (`/worker`)**: .NET worker processing votes from Redis.
- **Redis**: Message broker for queuing votes.
- **PostgreSQL**: Stores final vote counts.
- **Seed Service (`/seed-data`)**: Populates test votes.

---

## Application Architecture

### Data Flow
1. Users vote via Vote Service.
2. Votes are sent to Redis queue.
3. Worker processes votes into PostgreSQL.
4. Result Service displays live results via WebSocket.

### Network
- **Frontend Tier**: Vote + Result (user-facing).
- **Backend Tier**: Worker + Redis + PostgreSQL (internal only).

---

## Phase 1 – Local Setup (Docker Compose)

**Goal:** Run locally.

1. Build & start all services:
```bash
docker compose up --build
