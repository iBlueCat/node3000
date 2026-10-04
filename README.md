# node3000

Node.js app for testing Docker port configuration with Express.js

## 📋 Requirements

- Node.js 18+
- Docker (optional)

## 🚀 Quick Start

### Local Development

```bash
# Install dependencies
npm install

# Start development server (with auto-reload)
npm run dev

# Or start production server
npm start
```

The server will run on `http://localhost:3000`

### Using Docker

```bash
# Build and run with Docker Compose
docker-compose up -d

# Or build and run manually
docker build -t node3000 .
docker run -p 3000:3000 node3000
```

## 📡 API Endpoints

### Home
```
GET /
```
Returns welcome message and server status

**Response:**
```json
{
  "message": "Welcome to Node3000!",
  "status": "running",
  "port": 3000,
  "timestamp": "2026-10-04T10:00:00.000Z"
}
```

### Health Check
```
GET /api/health
```
Returns server health status

**Response:**
```json
{
  "status": "healthy",
  "uptime": 120.5,
  "environment": "production"
}
```

### Application Info
```
GET /api/info
```
Returns application information

**Response:**
```json
{
  "name": "node3000",
  "version": "1.0.0",
  "description": "Node.js app for testing Docker port configuration",
  "author": "iBlueCat"
}
```

## 🛠️ Development

### Prerequisites
```bash
npm install --save-dev nodemon
```

### Run in Development Mode
```bash
npm run dev
```

This uses Nodemon to automatically restart the server when files change.

## 🐳 Docker

### Build Image
```bash
docker build -t node3000 .
```

### Run Container
```bash
docker run -p 3000:3000 node3000
```

### Using Docker Compose
```bash
# Start services
docker-compose up

# Start in background
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down
```

## 📝 Environment Variables

- `PORT` - Server port (default: 3000)
- `NODE_ENV` - Environment type (development/production)

Example:
```bash
PORT=8000 npm start
```

## 📦 Project Structure

```
.
├── app.js                 # Main Express application
├── package.json          # Project dependencies
├── Dockerfile            # Docker configuration
├── docker-compose.yml    # Docker Compose configuration
├── .gitignore           # Git ignore rules
└── README.md            # This file
```

## 📚 Stack

- **Express.js** - Web framework
- **Node.js** - Runtime
- **Docker** - Containerization
- **Nodemon** - Development auto-reload

## 🧪 Testing

Test the endpoints using curl or your browser:

```bash
# Home endpoint
curl http://localhost:3000

# Health check
curl http://localhost:3000/api/health

# Application info
curl http://localhost:3000/api/info
```

## 📄 License

MIT

## 👤 Author

iBlueCat

---

**Status:** ✅ Ready to use
