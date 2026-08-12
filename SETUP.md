# Setup Guide

## Prerequisites

| Software | Version | Purpose |
|----------|---------|---------|
| Node.js | 18+ | JavaScript runtime |
| npm | 9+ | Package manager |
| MongoDB | 6+ | Database (or MongoDB Atlas) |
| Git | Latest | Version control |

## Environment Variables

### Server (.env)

Create `task-flow-proto-server-side/.env`:

```env
PORT=5000
MONGO_URI=mongodb://localhost:27017/task-flow-proto
NODE_ENV=development
JWT_SECRET=your-secret-key-here
JWT_EXPIRES_IN=30d
```

| Variable | Default | Description |
|----------|---------|-------------|
| PORT | `5000` | Server port |
| MONGO_URI | `mongodb://localhost:27017/task-flow-proto` | MongoDB connection string |
| NODE_ENV | `development` | Environment mode |
| JWT_SECRET | `super-secret-trello-clone-key` | JWT signing secret |
| JWT_EXPIRES_IN | `30d` | Token expiry duration |

---

## Backend Setup

### 1. Clone and Install

```bash
# Clone the repository
git clone <repo-url>
cd task-flow-proto

# Navigate to server
cd task-flow-proto-server-side

# Install dependencies
npm install
```

### 2. Configure Environment

```bash
# Copy example env (if available)
cp .env.example .env

# Edit .env with your MongoDB URI
```

### 3. Start Development Server

```bash
# Development mode with hot reload
npm run dev

# Output: Server running in development mode on port 5000
```

### 4. Build for Production

```bash
# TypeScript compilation
npm run build

# Start production server
npm start
```

### Available Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start dev server with hot reload (tsx watch) |
| `npm run build` | Compile TypeScript to JavaScript |
| `npm start` | Run compiled JavaScript from dist/ |

---

## Frontend Setup

### 1. Navigate to Client

```bash
cd task-flow-proto-client-side
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Start Development Server

```bash
npm start

# Output: Local: http://localhost:4200/
```

### 4. Build for Production

```bash
npm run build

# Output: dist/task-flow-proto-client-side/
```

### Available Scripts

| Command | Description |
|---------|-------------|
| `npm start` | Start dev server (ng serve) |
| `npm run build` | Production build |
| `npm run watch` | Build with file watching |
| `npm test` | Run unit tests (Vitest) |

---

## Database Setup

### Local MongoDB

1. Install MongoDB Community Edition
2. Start the service
3. Connection string: `mongodb://localhost:27017/task-flow-proto`

### MongoDB Atlas (Cloud)

1. Create account at [mongodb.com](https://mongodb.com)
2. Create a free cluster
3. Get connection string from "Connect" button
4. Update `MONGO_URI` in `.env`

**Connection string format:**
```
mongodb+srv://<username>:<password>@cluster0.xxxxx.mongodb.net/task-flow-proto?retryWrites=true&w=majority
```

---

## API Testing

### Health Check

```bash
curl http://localhost:5000/
# {"message":"TaskFlowProto TypeScript API is running..."}
```

### Signup

```bash
curl -X POST http://localhost:5000/api/users \
  -H "Content-Type: application/json" \
  -d '{"userName":"testuser","email":"test@example.com","password":"password123"}'
```

### Login

```bash
curl -X POST http://localhost:5000/api/users/login \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","password":"password123"}'
```

### Protected Route

```bash
curl http://localhost:5000/api/projects \
  -H "Authorization: Bearer <your-token-here>"
```

---

## Project Structure Reference

### Server

```
task-flow-proto-server-side/
├── .env                    # Environment variables (DO NOT COMMIT)
├── package.json
├── tsconfig.json
├── dist/                   # Compiled output
└── src/
    ├── server.ts           # Entry point
    ├── app.ts              # Express app
    ├── config/             # Configuration
    ├── models/             # Mongoose schemas
    ├── interface/          # TypeScript interfaces
    ├── enums/              # Enum definitions
    ├── middlewares/         # Express middleware
    ├── controllers/        # Request handlers
    ├── services/           # Business logic
    ├── routes/             # Route definitions
    └── utilities/          # Helper functions
```

### Client

```
task-flow-proto-client-side/
├── package.json
├── angular.json
├── tsconfig.json
├── public/                 # Static assets
└── src/
    ├── index.html
    ├── main.ts             # Bootstrap
    ├── styles.css          # Global styles
    └── app/
        ├── app.ts          # Root component
        ├── app.html        # Root template
        ├── app.config.ts   # App config
        └── app.routes.ts   # Routes
```

---

## Troubleshooting

### Port Already in Use

```bash
# Find process using port 5000
netstat -ano | findstr :5000

# Kill the process
taskkill /PID <process-id> /F
```

### MongoDB Connection Failed

1. Ensure MongoDB is running
2. Check connection string in `.env`
3. For Atlas: check IP whitelist and credentials

### TypeScript Compilation Errors

```bash
# Clean build
rm -rf dist/
npm run build
```

### Angular Build Errors

```bash
# Clear node_modules and reinstall
rm -rf node_modules/
npm install
```
