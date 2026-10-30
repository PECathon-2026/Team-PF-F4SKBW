# IncogniRead Backend API Server
> **PS-003: Small Web Reader Backend Service**  
> **Team NullVoid · PF-F4SKBW**

Node.js + TypeScript + Express + MongoDB backend service powering SSRF-safe CORS proxying and anonymous co-subscription discovery for the IncogniRead broadsheet reader.

## Prerequisites

- Node.js 18+
- MongoDB 6+ running locally or MongoDB Atlas URI

## Setup

```bash
# From the backend/ directory
cp .env.example .env
npm install
npm run dev     # Hot-reload dev server on port 3000
```

## Environment Variables

| Variable | Default | Description |
|---|---|---|
| `MONGODB_URI` | `mongodb://localhost:27017/incogniread_db` | MongoDB connection string |
| `PORT` | `3000` | Backend server port |
| `ALLOWED_ORIGINS` | `http://localhost:3001,http://localhost:3002,http://localhost:5173` | CORS-allowed frontend origins |
| `NODE_ENV` | `development` | Environment mode |
| `IP_HASH_SALT` | `incogniread-secure-salt-2026-pecathon` | Salt for anonymous IP hashing in discovery |

## API Endpoints

| Method | Path | Description |
|---|---|---|
| GET | `/health` | Server health status check |
| GET | `/api/fetch?url=...` | SSRF-hardened CORS proxy for RSS/Atom XML streams |
| GET | `/api/discovery?userFeeds=...` | Computes anonymous recommendations based on reader overlap |
| POST | `/api/discovery` | Submits opt-in anonymous subscription batch for co-subscription analysis |
| GET | `/api/feeds` | List all cached feeds |
| POST | `/api/feeds` | Create or upsert a feed |
| DELETE | `/api/feeds/:id` | Remove a feed and cascade delete articles |
