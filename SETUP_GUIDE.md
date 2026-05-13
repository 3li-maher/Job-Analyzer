# 🚀 Job Analyzer Pro - Complete Setup Guide

**Version**: 1.0 Production-Ready  
**Status**: ✅ Ready to Deploy  
**Cost**: $0/month (100% Free)  
**Last Updated**: May 13, 2026

---

## 📋 Quick Navigation

- [Project Structure](#project-structure)
- [System Requirements](#system-requirements)
- [Installation & Setup](#installation--setup)
- [Running Locally](#running-locally)
- [Deployment](#deployment)
- [API Documentation](#api-documentation)
- [Configuration](#configuration)
- [Troubleshooting](#troubleshooting)

---

## 📁 Project Structure

```
job-analyzer/
├── 📄 index.html                    # Landing page website
├── 📄 JOB_ANALYZER_BLUEPRINT.md    # Complete technical documentation
├── 📄 SETUP_GUIDE.md               # This file
├── 📄 DEPLOYMENT_GUIDE.md          # Deployment instructions
│
├── backend/                         # Python FastAPI Backend
│   ├── app/
│   │   ├── api/v1/
│   │   │   ├── jobs.py             # Job analysis endpoints
│   │   │   ├── search.py           # Search & filter endpoints
│   │   │   ├── auth.py             # Authentication endpoints
│   │   │   ├── bookmarks.py        # Bookmark management
│   │   │   ├── history.py          # User history
│   │   │   └── health.py           # Health check endpoint
│   │   ├── services/
│   │   │   ├── scraper_service.py  # Web scraping (Playwright)
│   │   │   ├── ai_service.py       # Ollama LLM integration
│   │   │   ├── risk_detection_service.py  # Scam detection
│   │   │   ├── auth_service.py     # JWT authentication
│   │   │   └── cache_service.py    # Redis caching
│   │   ├── database/
│   │   │   ├── models.py           # SQLAlchemy ORM models
│   │   │   ├── db.py               # Database configuration
│   │   │   └── crud.py             # Database operations
│   │   ├── models/
│   │   │   └── schemas.py          # Pydantic request/response schemas
│   │   ├── config.py               # Configuration management
│   │   ├── dependencies.py         # Dependency injection
│   │   ├── main.py                 # FastAPI app initialization
│   │   └── utils/                  # Utility functions
│   │
│   ├── requirements.txt            # Python dependencies
│   ├── .env.example                # Environment variables template
│   ├── Dockerfile                  # Docker configuration
│   ├── docker-compose.yml          # Docker Compose setup
│   └── migrations/                 # Database migrations (Alembic)
│
├── frontend/                        # React Native Mobile App
│   ├── src/
│   │   ├── screens/
│   │   │   ├── URLInputScreen.tsx  # Main URL input screen
│   │   │   ├── JobCardScreen.tsx   # Detailed job view
│   │   │   ├── SearchScreen.tsx    # Job search interface
│   │   │   └── SavedJobsScreen.tsx # Bookmarks
│   │   ├── components/
│   │   │   ├── JobCard.tsx         # Reusable job card
│   │   │   ├── RiskBadge.tsx       # Risk score display
│   │   │   └── LoadingSpinner.tsx  # Loading state
│   │   ├── services/
│   │   │   └── api.ts              # API client
│   │   ├── hooks/
│   │   │   └── useJobAnalysis.ts   # Custom hooks
│   │   ├── store/
│   │   │   └── redux/              # Redux state management
│   │   └── App.tsx                 # Root component
│   │
│   ├── package.json                # NPM dependencies
│   ├── app.json                    # Expo configuration
│   └── tsconfig.json               # TypeScript configuration
│
├── docs/                           # Documentation
│   ├── API_REFERENCE.md            # API endpoints documentation
│   ├── DATABASE_SCHEMA.md          # Database tables & relationships
│   ├── DEPLOYMENT_GUIDE.md         # How to deploy
│   ├── ARCHITECTURE.md             # System architecture
│   └── CONTRIBUTING.md             # Contributing guidelines
│
└── .github/                        # GitHub configuration
    ├── workflows/
    │   ├── test.yml                # CI/CD testing
    │   └── deploy.yml              # Auto-deployment
    └── ISSUE_TEMPLATE/             # Issue templates
```

---

## 🖥️ System Requirements

### For Development

**Minimum:**
- 4GB RAM
- 20GB Disk Space
- Python 3.11+
- Node.js 18+
- Docker & Docker Compose

**Recommended:**
- 8GB RAM
- SSD with 50GB space
- Modern terminal (iTerm2, Windows Terminal, etc.)

### For Production Deployment

**Server Specs (Railway/Render Free Tier):**
- 0.5 CPU
- 512MB RAM
- 5GB Database storage

**Scaling to 10k+ users:**
- 1-2 CPUs
- 2-4GB RAM
- 20GB Database storage
- Redis cache (1GB)

---

## 🚀 Installation & Setup

### Step 1: Clone & Prepare Project

```bash
# Create project directory
mkdir job-analyzer && cd job-analyzer

# If you have the ZIP file, extract it
unzip job-analyzer.zip
cd job-analyzer

# Initialize git
git init
git add .
git commit -m "Initial commit: Production-ready job analyzer"
```

### Step 2: Setup Python Backend

```bash
cd backend

# Create virtual environment
python3.11 -m venv venv

# Activate virtual environment
# On macOS/Linux:
source venv/bin/activate
# On Windows:
venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Create .env file
cp .env.example .env

# Edit .env with your configuration
nano .env
```

### Step 3: Setup Database

```bash
# Start PostgreSQL (using Docker is easiest)
docker run --name job-analyzer-db \
  -e POSTGRES_PASSWORD=password \
  -e POSTGRES_DB=jobanalyzer \
  -p 5432:5432 \
  -d postgres:15-alpine

# Initialize database tables
python -m alembic upgrade head
```

### Step 4: Setup Redis Cache

```bash
# Start Redis
docker run --name job-analyzer-redis \
  -p 6379:6379 \
  -d redis:7-alpine
```

### Step 5: Setup Ollama (Local LLM)

```bash
# Download and install Ollama
# Visit: https://ollama.ai

# Start Ollama server
ollama serve

# In a new terminal, download the model
ollama pull mistral

# Or use a smaller model
ollama pull neural-chat  # ~4GB
```

### Step 6: Setup Frontend (React Native)

```bash
cd ../frontend

# Install dependencies
npm install

# Or using yarn
yarn install

# Setup Expo CLI
npm install -g expo-cli

# Test the app (opens in browser)
npx expo start
```

---

## 🔧 Running Locally

### Option 1: Using Docker Compose (Recommended)

```bash
cd backend

# Build and start all services
docker-compose up -d

# Check logs
docker-compose logs -f api

# Stop services
docker-compose down
```

### Option 2: Manual Setup

#### Terminal 1: Start Backend API

```bash
cd backend
source venv/bin/activate
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

#### Terminal 2: Start Frontend

```bash
cd frontend
npm start
# Or
npx expo start
```

#### Terminal 3: Monitor Logs

```bash
# Watch backend logs
tail -f backend/logs/app.log
```

### Access the Application

- **Landing Page**: http://localhost:3000
- **API Docs**: http://localhost:8000/docs
- **API Redoc**: http://localhost:8000/redoc
- **Mobile App**: Expo app on your phone or http://localhost:19000

---

## 📊 Testing the System

### Test Job Analysis Endpoint

```bash
curl -X POST http://localhost:8000/v1/jobs/analyze \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -d '{
    "url": "https://linkedin.com/jobs/123456",
    "force_refresh": false
  }'
```

### Expected Response

```json
{
  "status": "success",
  "job_id": "550e8400-e29b-41d4-a716-446655440000",
  "analysis": {
    "job_info": {
      "title": "Senior Backend Engineer",
      "employment_type": "full-time",
      "required_experience_years": 5
    },
    "company_info": {
      "name": "Tech Corp",
      "industry": "Software Development"
    },
    "risk_analysis": {
      "risk_score": 5,
      "risk_level": "low"
    }
  }
}
```

### Test Search Endpoint

```bash
curl -X GET "http://localhost:8000/v1/search?query=python&location=Egypt&page=1" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN"
```

---

## 🌐 Environment Configuration

### .env File Template

```bash
# Database
DATABASE_URL=postgresql://user:password@localhost:5432/jobanalyzer
DATABASE_POOL_SIZE=10

# Redis
REDIS_URL=redis://localhost:6379/0

# Ollama LLM
OLLAMA_HOST=http://localhost:11434
OLLAMA_MODEL=mistral

# JWT Authentication
JWT_SECRET_KEY=your-super-secret-key-min-32-chars
JWT_ALGORITHM=HS256
JWT_EXPIRE_MINUTES=60

# API Configuration
API_ENVIRONMENT=development
CORS_ORIGINS=http://localhost:3000,http://localhost:19000

# Email (for future notifications)
SMTP_SERVER=smtp.gmail.com
SMTP_PORT=587
SMTP_USERNAME=your-email@gmail.com
SMTP_PASSWORD=your-app-password

# Scraping Configuration
SCRAPER_TIMEOUT=15
SCRAPER_RETRY_ATTEMPTS=3

# Feature Flags
ENABLE_NOTIFICATIONS=false
ENABLE_CV_MATCHING=false
```

---

## 🚀 Deployment

### Deploy to Railway

1. **Create Railway Account**
   - Visit https://railway.app
   - Sign up with GitHub

2. **Connect Repository**
   ```bash
   # Push to GitHub
   git push origin main

   # Go to Railway dashboard → New Project → GitHub
   # Select your repository
   ```

3. **Configure Services**
   - API: Python service from `backend/` folder
   - Database: PostgreSQL plugin
   - Redis: Redis plugin
   - Ollama: Custom Docker service

4. **Set Environment Variables**
   - Add all variables from `.env`
   - Railroad will provide DATABASE_URL, REDIS_URL

5. **Deploy**
   - Push to main branch
   - Railway auto-deploys

### Deploy to Render

1. **Create Render Account**
   - Visit https://render.com
   - Sign up

2. **Create New Service**
   - Select Web Service
   - Connect GitHub repo
   - Build command: `pip install -r requirements.txt`
   - Start command: `uvicorn app.main:app --host 0.0.0.0`

3. **Add Database**
   - PostgreSQL instance
   - Set connection string in environment

4. **Deploy**
   - Render auto-deploys on push

### Self-Hosted Deployment

```bash
# On your VPS (Ubuntu 22.04):

# 1. Install dependencies
sudo apt-get update
sudo apt-get install -y docker.io docker-compose nginx postgresql

# 2. Clone repository
git clone https://github.com/your-username/job-analyzer.git
cd job-analyzer

# 3. Setup environment
cp backend/.env.example backend/.env
nano backend/.env

# 4. Start services
docker-compose -f backend/docker-compose.yml up -d

# 5. Configure Nginx reverse proxy
sudo nano /etc/nginx/sites-available/jobanalyzer.com
# (Copy nginx config below)

# 6. Enable site
sudo ln -s /etc/nginx/sites-available/jobanalyzer.com /etc/nginx/sites-enabled/
sudo systemctl restart nginx

# 7. Setup SSL with Let's Encrypt
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d jobanalyzer.com
```

### Nginx Configuration

```nginx
upstream api {
    server 127.0.0.1:8000;
}

server {
    listen 80;
    server_name jobanalyzer.com www.jobanalyzer.com;

    location / {
        proxy_pass http://api;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    location /static {
        alias /var/www/jobanalyzer/static;
    }
}
```

---

## 📚 API Documentation

### Authentication

All requests (except `/auth/login`, `/auth/register`) require JWT token:

```bash
# Get token
curl -X POST http://localhost:8000/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "user@example.com",
    "password": "password123"
  }'

# Response
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "bearer",
  "user": { "id": "...", "email": "user@example.com" }
}

# Use token in requests
curl -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..." \
  http://localhost:8000/v1/jobs/analyze
```

### Main Endpoints

#### 1. Analyze Job Post
```
POST /v1/jobs/analyze
Authorization: Bearer {token}

Request:
{
  "url": "https://linkedin.com/jobs/123456",
  "force_refresh": false
}

Response:
{
  "job_id": "uuid",
  "analysis": { ... },
  "risk_score": 5,
  "confidence": 0.95
}
```

#### 2. Search Jobs
```
GET /v1/search?
  query=python&
  location=Egypt&
  salary_min=3000&
  salary_max=10000&
  page=1&limit=20
Authorization: Bearer {token}

Response:
{
  "total_results": 247,
  "jobs": [ ... ]
}
```

#### 3. Save Job
```
POST /v1/jobs/{job_id}/bookmark
Authorization: Bearer {token}

Response:
{ "bookmarked": true, "job_id": "..." }
```

#### 4. Get User History
```
GET /v1/history?limit=50&offset=0
Authorization: Bearer {token}

Response:
{
  "total": 50,
  "jobs": [ ... ]
}
```

---

## 🛠️ Development Workflow

### Adding a New Feature

1. **Create Feature Branch**
   ```bash
   git checkout -b feature/cv-matching
   ```

2. **Backend Development**
   - Add new endpoint in `backend/app/api/v1/`
   - Add service logic in `backend/app/services/`
   - Add database models if needed
   - Write tests in `backend/tests/`

3. **Frontend Development**
   - Add new screen in `frontend/src/screens/`
   - Add components in `frontend/src/components/`
   - Update navigation

4. **Testing**
   ```bash
   # Backend tests
   cd backend
   pytest tests/ -v

   # Frontend tests
   cd frontend
   npm test
   ```

5. **Push & Create PR**
   ```bash
   git push origin feature/cv-matching
   # Create PR on GitHub
   ```

### Database Migrations

```bash
# Create new migration
alembic revision --autogenerate -m "Add new_column to jobs"

# Apply migration
alembic upgrade head

# Rollback if needed
alembic downgrade -1
```

---

## 🐛 Troubleshooting

### Issue: Connection refused to PostgreSQL

**Solution:**
```bash
# Check if PostgreSQL is running
docker ps | grep postgres

# If not running, start it
docker-compose up -d postgres

# Check connection string in .env
# Should be: postgresql://user:password@localhost:5432/jobanalyzer
```

### Issue: Ollama not responding

**Solution:**
```bash
# Ensure Ollama service is running
ollama serve

# In another terminal, test connection
curl http://localhost:11434/api/tags

# If no response, reinstall Ollama
# Visit https://ollama.ai
```

### Issue: Redis connection error

**Solution:**
```bash
# Check Redis is running
docker ps | grep redis

# Restart Redis
docker-compose up -d redis

# Test connection
redis-cli ping
```

### Issue: Frontend won't load

**Solution:**
```bash
# Clear cache and reinstall
cd frontend
rm -rf node_modules package-lock.json
npm install

# If using Expo
npx expo start --clear
```

### Issue: JWT token expired

**Solution:**
```bash
# Token expiry is set in .env (default 60 min)
# To extend, update JWT_EXPIRE_MINUTES=120

# Or get a new token by logging in again
curl -X POST http://localhost:8000/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email": "user@example.com", "password": "password"}'
```

---

## 📊 Performance Tuning

### Database Optimization

```sql
-- Add indexes for faster queries
CREATE INDEX CONCURRENTLY idx_jobs_user_date 
    ON job_posts(user_id, created_at DESC);

CREATE INDEX CONCURRENTLY idx_jobs_risk_score 
    ON job_posts(risk_score);

-- Check query performance
EXPLAIN ANALYZE SELECT * FROM job_posts WHERE user_id = 'uuid';
```

### Cache Configuration

```python
# In backend/app/services/cache_service.py

# Increase cache TTL for frequently accessed data
CACHE_TTL = {
    'search_results': 300,  # 5 minutes
    'job_analysis': 3600,   # 1 hour
    'user_profile': 86400   # 24 hours
}
```

### API Rate Limiting

```python
# Configure in backend/app/main.py

from slowapi import Limiter

limiter = Limiter(key_func=get_remote_address)

# Set limits per endpoint
@app.post("/v1/jobs/analyze")
@limiter.limit("100/hour")  # 100 requests per hour
async def analyze_job(...):
    pass
```

---

## 📈 Monitoring & Logging

### View Logs

```bash
# Docker container logs
docker-compose logs -f api

# Application logs
tail -f /var/log/job-analyzer/app.log

# Database queries
tail -f /var/log/job-analyzer/db.log
```

### Health Check

```bash
# Check API health
curl http://localhost:8000/health

# Response
{
  "status": "healthy",
  "database": "connected",
  "redis": "connected",
  "ollama": "connected"
}
```

### Monitor Performance

```bash
# CPU and Memory usage
docker stats

# Database connections
psql -U user -d jobanalyzer -c "SELECT datname, count(*) FROM pg_stat_activity GROUP BY datname;"
```

---

## 🔐 Security Checklist

- [ ] Change JWT_SECRET_KEY to a strong random value
- [ ] Set CORS_ORIGINS to your domain only
- [ ] Enable HTTPS/SSL in production
- [ ] Rotate database passwords regularly
- [ ] Enable database encryption
- [ ] Setup firewall rules
- [ ] Enable audit logging
- [ ] Regular security audits
- [ ] Keep dependencies updated

---

## 🤝 Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/amazing`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing`)
5. Create Pull Request

See [CONTRIBUTING.md](./docs/CONTRIBUTING.md) for detailed guidelines.

---

## 📄 License

This project is open source under the MIT License. See [LICENSE](./LICENSE) for details.

---

## 🆘 Support

- **Documentation**: [Full Documentation](./JOB_ANALYZER_BLUEPRINT.md)
- **Issues**: GitHub Issues
- **Discussions**: GitHub Discussions
- **Email**: support@jobanalyzer.com

---

## 🎉 What's Next?

1. **Try it locally** - Follow the setup guide above
2. **Deploy to production** - Choose Railway, Render, or self-hosted
3. **Customize for your needs** - Fork and modify
4. **Share feedback** - Create issues or discussions
5. **Contribute** - Submit PRs for improvements

---

**Created with ❤️ for job seekers everywhere**  
**100% Open Source | 100% Free | 100% Powerful**

```

---

## Quick Start Command Reference

```bash
# Development setup (one-liner)
cd backend && python3.11 -m venv venv && source venv/bin/activate && \
pip install -r requirements.txt && cp .env.example .env && \
docker-compose up -d

# Test the system
curl -X GET http://localhost:8000/health

# Deploy to Railway
git push origin main

# View logs
docker-compose logs -f api

# Stop everything
docker-compose down
```

---

For more details, see the complete **JOB_ANALYZER_BLUEPRINT.md** document.
