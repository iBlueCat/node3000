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

The server will run on `http://localhost:3000` by default

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

## 🌐 Port Configuration

### Default Port (3000)

The application defaults to **port 3000**. You can access it at:
```
http://localhost:3000
```

### Changing the Port

The port can be customized using the `PORT` environment variable. Here are examples for testing different network ports:

#### Local Development - Different Ports

```bash
# Port 8000
PORT=8000 npm start
# Access at: http://localhost:8000

# Port 5000
PORT=5000 npm start
# Access at: http://localhost:5000

# Port 3001
PORT=3001 npm start
# Access at: http://localhost:3001

# Port 8080
PORT=8080 npm start
# Access at: http://localhost:8080

# Port 9000
PORT=9000 npm start
# Access at: http://localhost:9000

# Development mode with custom port
PORT=5000 npm run dev
# Access at: http://localhost:5000 with auto-reload
```

#### Testing Multiple Ports

You can run multiple instances on different ports in separate terminal windows:

```bash
# Terminal 1 - Port 3000
npm start

# Terminal 2 - Port 8000
PORT=8000 npm start

# Terminal 3 - Port 5000
PORT=5000 npm start
```

Then test each instance:
```bash
# Test port 3000
curl http://localhost:3000

# Test port 8000
curl http://localhost:8000

# Test port 5000
curl http://localhost:5000
```

### Using .env File (Optional)

Create a `.env` file in the project root:

```env
PORT=8000
NODE_ENV=development
```

Then run normally:
```bash
npm start
# Server will use port 8000
```

## 🐳 Docker

### Build Image
```bash
docker build -t node3000 .
```

### Run Container with Default Port (3000)
```bash
docker run -p 3000:3000 node3000
# Access at: http://localhost:3000
```

### Run Container with Custom Port

The `-p` flag format is: `-p <host-port>:<container-port>`

```bash
# Port 8000
docker run -p 8000:3000 node3000
# Access at: http://localhost:8000
# (Container runs on 3000, but exposed on 8000)

# Port 5000
docker run -p 5000:3000 node3000
# Access at: http://localhost:5000

# Port 9000
docker run -p 9000:3000 node3000
# Access at: http://localhost:9000
```

### Run Multiple Docker Instances

```bash
# Instance 1 - Port 3000
docker run -p 3000:3000 --name node3000-app1 -d node3000

# Instance 2 - Port 8000
docker run -p 8000:3000 --name node3000-app2 -d node3000

# Instance 3 - Port 5000
docker run -p 5000:3000 --name node3000-app3 -d node3000

# View running containers
docker ps

# Stop a container
docker stop node3000-app1

# Remove a container
docker rm node3000-app1
```

### Run with Environment Variable (Custom Container Port)

If you modify the Dockerfile, you can pass PORT as environment variable:

```bash
docker run -e PORT=8000 -p 8000:8000 node3000
# Container runs on 8000 and exposed on 8000
```

### Using Docker Compose

```bash
# Start services
docker-compose up

# Start in background
docker-compose up -d

# View logs
docker-compose logs -f

# View specific service logs
docker-compose logs -f app

# Stop services
docker-compose down

# Stop and remove volumes
docker-compose down -v
```

## 📝 Environment Variables

- `PORT` - Server port (default: 3000)
- `NODE_ENV` - Environment type (development/production, default: development)

Examples:
```bash
# Set PORT only
PORT=8000 npm start

# Set PORT and NODE_ENV
PORT=8000 NODE_ENV=production npm start

# Using .env file
# Create .env file with:
# PORT=8000
# NODE_ENV=production
npm start
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

### Test Default Port (3000)
```bash
# Home endpoint
curl http://localhost:3000

# Health check
curl http://localhost:3000/api/health

# Application info
curl http://localhost:3000/api/info
```

### Test Custom Port (e.g., 8000)

First, start the server on port 8000:
```bash
PORT=8000 npm start
```

Then in another terminal, test:
```bash
# Home endpoint
curl http://localhost:8000

# Health check
curl http://localhost:8000/api/health

# Application info
curl http://localhost:8000/api/info
```

### Batch Testing Multiple Ports
```bash
# Test all instances
for port in 3000 5000 8000; do
  echo "Testing port $port..."
  curl http://localhost:$port
done
```

### Browser Testing

Open your browser and visit:
- http://localhost:3000
- http://localhost:8000
- http://localhost:5000

## 🔍 Troubleshooting

### Port Already in Use

If you get an error like "Address already in use":

```bash
# Find process using the port (macOS/Linux)
lsof -i :3000

# Find process using the port (Windows)
netstat -ano | findstr :3000

# Kill the process (macOS/Linux)
kill -9 <PID>

# Kill the process (Windows)
taskkill /PID <PID> /F
```

### Check if Server is Running

```bash
# Test if server is listening
curl http://localhost:3000 -v

# Check with netstat
netstat -an | grep 3000
```

## 📄 License

MIT

## 👤 Author

iBlueCat

---

**Status:** ✅ Ready to use
