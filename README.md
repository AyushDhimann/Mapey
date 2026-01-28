# 🚀 Mapey - AI-Powered Career Roadmap Generator

<div align="center">

![Mapey Logo](https://img.shields.io/badge/Mapey-Career_Roadmap_AI-red?style=for-the-badge)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![FastAPI](https://img.shields.io/badge/FastAPI-Backend-009688?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![Next.js](https://img.shields.io/badge/Next.js-Frontend-black?style=for-the-badge&logo=next.js&logoColor=white)](https://nextjs.org/)

**Generate personalized career roadmaps powered by AI**

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Quick Start](#-quick-start)
- [Real-Time Progress](#-real-time-progress-tracking)
- [API Documentation](#-api-documentation)
- [Testing](#-testing)
- [Troubleshooting](#-troubleshooting)

---

## 🎯 Overview

**Mapey** is an AI-powered career roadmap generator that analyzes your resume, compares it with your target role, and creates a personalized learning path. Using advanced LLM technology (Llama 3.2) and multi-agent workflows with **real-time progress tracking**, Mapey provides:

- 📊 **Skill Gap Analysis** - Understand what you need to learn
- 🎓 **Personalized Curriculum** - Step-by-step learning path
- 🔗 **Curated Resources** - Best courses, projects, and materials
- 📈 **Career Strategy** - Timeline and milestones for success
- ⚡ **Real-Time Progress** - Live updates with visual progress bar

## ✨ Features

### Core Capabilities

- **🤖 AI-Powered Analysis**
  - LangGraph 6-stage multi-agent workflow
  - Llama 3.2 (1B) local LLM via Ollama
  - FAISS vector store with RAG (Retrieval Augmented Generation)
  - Semantic search and web scraping (Tavily)

- **📊 Real-Time Progress Tracking** ⭐ NEW
  - **Live progress bar** (0-100%) with smooth animations
  - **Stage-by-stage status updates** (6 visual indicators)
  - **Server-Sent Events (SSE) streaming** for real-time feedback
  - **Time estimates** (typically 3-5 minutes)
  - **Cyberpunk dark theme** with red/black aesthetic

- **💼 Comprehensive Career Analysis**
  - Role breakdown and industry expectations
  - Skill gap identification
  - Multi-phase learning curriculum
  - Resource curation via web search
  - Interview preparation strategy

- **🎨 Modern UI/UX**
  - Responsive dark theme design
  - Smooth animations and transitions
  - Real-time toast notifications
  - Copy-to-clipboard functionality
  - Mobile, tablet, and desktop support

- **🔐 Security**
  - JWT authentication (HS256)
  - Secure API endpoints
  - Environment-based configuration
  - CORS protection

## 🚀 Quick Start

### Prerequisites

- **Python 3.11+** (Python 3.14 recommended)
- **Docker & Docker Compose** (required)
- **Windows 10/11** or **Linux/macOS**
- **4GB RAM minimum** (8GB recommended)
- **10GB free disk space**
- **NVIDIA GPU** (optional but recommended for faster generation)
  - Install [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html) for GPU support

### Installation (5 minutes)

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/mapey.git
   cd mapey
   ```

2. **Setup the project** (creates venv, installs dependencies, configures env files)
   ```powershell
   # Windows PowerShell
   python -m mapey setup
   ```

3. **Update your ENVs**

4. **Start all services** (runs Docker containers for backend, frontend, and Ollama)
   ```powershell
   python -m mapey start
   ```

   This command will:
   - Start Docker Compose services
   - Pull Ollama models (nomic-embed-text, llama3.2:1b)
   - Initialize the backend
   - 🎮 **Use GPU automatically** if NVIDIA GPU is detected!

5. **Open the app!** 🎉
   ```
   Frontend: http://localhost:3000
   Backend API: http://localhost:8000
   API Docs: http://localhost:8000/docs
   ```

### First Roadmap Generation

1. Go to http://localhost:3000
2. Click **"Enter Text"** button
3. Fill in:
   - **Target Role**: "Python Backend Developer"
   - **Resume**: Paste your skills and experience
   - **Job Description** (optional): Paste a job posting
4. Click **"Generate Roadmap"**
5. Watch the **real-time progress bar!** (takes 3-5 minutes)
6. View your personalized roadmap! 🎊

### File Upload Alternative

You can also **upload a PDF/TXT resume** instead of pasting text:
1. Click **"Upload Resume"** button
2. Select your resume file
3. Fill in target role and job description
4. Click **"Generate Roadmap"**
5. Progress updates shown in results area

## 📊 Real-Time Progress Tracking

### Features

- **Live Progress Bar** - Visual feedback from 0% to 100%
- **Stage Indicators** - 6 circular badges showing workflow progress
- **Status Messages** - Real-time updates on current activity
- **Smooth Animations** - Shimmer effects and smooth transitions
- **Time Estimates** - Shows typical 3-5 minute duration

### How It Works

```
Frontend → SSE Connection → Backend
   ↓
Opens EventSource to /generate-from-text-stream
   ↓
Backend sends real-time updates:
  data: {"progress": 10, "step": "Analyzing..."}
  data: {"progress": 45, "step": "Skill gaps..."}
   ↓
Progress Bar updates with animations
   ↓
Final Result delivered at 100%
```

### 6-Stage Workflow

1. **Topic Analyzer** (10-25%) - Analyzes target role and industry expectations
2. **Skill Gap Agent** (30-45%) - Compares resume with job requirements  
3. **Curriculum Planner** (50-60%) - Designs personalized learning path
4. **RAG Retriever** (60-65%) - Retrieves relevant context from experience
5. **Resource Curator** (70-80%) - Finds best learning resources via web search
6. **Validator** (85-100%) - Generates final comprehensive roadmap

### Visual Design

```
Progress Bar:
┌────────────────────────────────────────────┐
│ ████████████████████░░░░░░░░░░░░░░░░░░░░  │ 45%
└────────────────────────────────────────────┘
   "Analyzing skill gaps..."

Stage Indicators:
 [✓] [✓] [●] [ ] [ ] [ ]
  1   2   3   4   5   6
```

## 📡 API Documentation

### Base URL
```
http://localhost:8000/api/v1
```

### Endpoints

#### 1. Health Check
```http
GET /health
```
**Response:**
```json
{
  "status": "healthy",
  "version": "1.0.0",
  "service": "Mapey Roadmap API"
}
```

#### 2. Generate Roadmap (Streaming with Progress) ⭐ NEW
```http
POST /roadmap/generate-from-text-stream
Content-Type: application/json
Authorization: Bearer <JWT_TOKEN>

{
  "topic": "Python Backend Developer",
  "resume": "Your resume text here...",
  "jd": "Optional job description"
}
```

**Response:** Server-Sent Events (SSE)
```
data: {"progress": 10, "step": "Analyzing target role", "status": "processing"}
data: {"progress": 25, "step": "Topic analysis complete", "status": "processing"}
data: {"progress": 45, "step": "Skill gap analysis complete", "status": "processing"}
...
data: {"progress": 100, "step": "Complete", "status": "complete", "result": {...}}
```

#### 3. Generate Roadmap (Non-streaming)
```http
POST /roadmap/generate-from-text
Content-Type: application/json
Authorization: Bearer <JWT_TOKEN>

{
  "topic": "Full Stack Developer",
  "resume": "Your resume...",
  "jd": "Job description..."
}
```

**Response:**
```json
{
  "roadmap": "Complete roadmap markdown...",
  "skill_gaps": "Skill gap analysis...",
  "curriculum": "Learning curriculum...",
  "resources": "Curated resources...",
  "analysis": "Role analysis...",
  "rag_context": "Retrieved context..."
}
```

#### 4. Vector Store Stats
```http
GET /roadmap/vector-store/stats
Authorization: Bearer <JWT_TOKEN>
```

### Authentication

Generate a JWT token:
```powershell
docker exec mapey-backend-1 python -c "import jwt; import time; print(jwt.encode({'sub': 'test-user', 'exp': int(time.time()) + 3600}, 'change-me', algorithm='HS256'))"
```

Use in requests:
```bash
Authorization: Bearer <your_jwt_token>
```

## 🧪 Testing

### Run Test Script
```powershell
.\test_api.ps1
```

Tests include:
- ✅ Health check
- ✅ JWT token generation
- ✅ Vector store stats
- ✅ Roadmap generation (full workflow)

### Manual API Testing
```powershell
# Generate token
$token = docker exec mapey-backend-1 python -c "import jwt; import time; print(jwt.encode({'sub': 'test-user', 'exp': int(time.time()) + 3600}, 'change-me', algorithm='HS256'))"

# Test streaming endpoint
$headers = @{
    "Content-Type" = "application/json"
    "Authorization" = "Bearer $token"
}

$body = @{
    topic = "Data Scientist"
    resume = "Sample resume text"
    jd = ""
} | ConvertTo-Json

Invoke-RestMethod -Uri "http://localhost:8000/api/v1/roadmap/generate-from-text-stream" -Method Post -Body $body -Headers $headers
```

## 🛠️ Configuration

### Environment Variables

**Backend** (`backend/.env`):
```env
# LLM Settings
OLLAMA_MODEL=llama3.2:1b
OLLAMA_BASE_URL=http://ollama:11434
OLLAMA_TEMPERATURE=0.4
OLLAMA_NUM_CTX=1048

# Embedding Model
EMBED_MODEL_NAME=nomic-embed-text

# Tavily API (Web Search)
TAVILY_API_KEY=your_api_key_here

# Authentication
BACKEND_JWT_SECRET=change-me

# API Settings
DEBUG=true
LOG_LEVEL=INFO
```

**Frontend** (`.env.local`):
```env
NEXT_PUBLIC_API_URL=http://localhost:8000
```

## 📊 Logging

The application uses structured JSON logging for production monitoring:


- **Location**: `backend/logs/`
- **Files**:
  - `app.log` - All application logs
  - `errors.log` - Error-level logs only
- **Format**: JSON (production) or text (development)
- **Levels**: DEBUG, INFO, WARNING, ERROR, CRITICAL

## 🐛 Troubleshooting

### Services won't start
```powershell
# Check Docker is running
docker ps

# Restart with Python command
python -m mapey start

# Or manually rebuild containers
docker-compose down -v
docker-compose up --build -d
```

### Models not found
```powershell
# Pull models again
docker exec mapey-ollama-1 ollama pull nomic-embed-text
docker exec mapey-ollama-1 ollama pull llama3.2:1b
docker-compose restart backend
```

### Frontend not loading
```powershell
# Check logs
docker-compose logs frontend --tail=50

# Restart frontend
docker-compose restart frontend
```

### Backend errors
```powershell
# Check backend logs
docker-compose logs backend --tail=50 --follow

# Check if Ollama is ready
docker exec mapey-ollama-1 ollama list
```

### Progress bar not showing
- Make sure you're using "Enter Text" or "Upload Resume" button
- Streaming works for both text and file input
- Check browser console for errors (F12)
- Verify backend logs show streaming endpoint

### File upload not working
- Supported formats: PDF, TXT
- File must be less than 10MB
- Check browser console for errors
- Verify backend logs for file processing errors

### Slow generation
- Normal processing time: **3-5 minutes**
- Depends on hardware (CPU-based LLM)
- Check resource usage: `docker stats`
- First generation may be slower (model loading)

## 📁 Project Structure

```
mapey/
├── backend/                 # FastAPI backend
│   ├── app/
│   │   ├── api/            # API routes
│   │   │   └── routes/
│   │   │       ├── roadmap.py      # Roadmap endpoints + streaming
│   │   │       └── health.py       # Health check
│   │   ├── core/           # Core utilities
│   │   │   ├── config.py           # Configuration
│   │   │   ├── auth.py             # JWT authentication
│   │   │   └── logging.py          # Logging setup
│   │   ├── models/         # Data models
│   │   │   └── schemas.py          # Pydantic schemas
│   │   ├── services/       # Business logic
│   │   │   ├── agents.py           # LangGraph agents + progress
│   │   │   ├── vector_store.py     # FAISS vector store
│   │   │   ├── ollama_service.py   # Ollama integration
│   │   │   └── file_processor.py   # File handling
│   │   └── main.py         # FastAPI app
│   ├── .env                # Environment variables
│   ├── requirements.txt    # Python dependencies
│   └── Dockerfile          # Backend container
├── frontend/                # Next.js frontend
│   ├── app/                # App router pages
│   │   ├── page.tsx                # Home page
│   │   ├── layout.tsx              # Root layout
│   │   └── globals.css             # Global styles + animations
│   ├── components/         # React components
│   │   ├── RoadmapForm.tsx         # Input form
│   │   ├── RoadmapResults.tsx      # Results display + progress
│   │   ├── ProgressBar.tsx         # Progress bar component
│   │   ├── Header.tsx              # Header component
│   │   └── LoadingSpinner.tsx      # Spinner component
│   ├── lib/                # Utilities
│   │   ├── api.ts                  # API client + streaming
│   │   └── store.ts                # Zustand store + progress
│   ├── types/              # TypeScript types
│   │   └── api.ts                  # API type definitions
│   ├── package.json        # Node dependencies
│   └── Dockerfile          # Frontend container
├── docs/                    # Documentation
│   ├── PROGRESS_BAR_GUIDE.md       # Progress bar docs
│   ├── PROGRESS_BAR_COMPLETE.md    # Complete implementation
│   ├── SETUP_GUIDE.md              # Setup instructions
│   └── PROJECT_STRUCTURE.md        # Architecture docs
├── docker-compose.yml       # Multi-container orchestration
├── README.md               # This file
└── test_api.ps1            # API test script
```

## 🌟 Technologies Used

### Backend
- **FastAPI** - Modern Python web framework
- **LangChain** - LLM application framework
- **LangGraph** - Multi-agent workflow orchestration
- **Ollama** - Local LLM inference (Llama 3.2)
- **FAISS** - Vector similarity search
- **Tavily** - Web search API
- **Pydantic** - Data validation
- **PyJWT** - JWT authentication
- **Uvicorn** - ASGI server

### Frontend
- **Next.js 14** - React framework with App Router
- **TypeScript** - Type-safe JavaScript
- **Tailwind CSS** - Utility-first CSS
- **Zustand** - State management
- **React Hot Toast** - Toast notifications
- **React Markdown** - Markdown rendering
- **Lucide React** - Icon library

### Infrastructure
- **Docker** - Containerization
- **Docker Compose** - Multi-container orchestration
- **Node.js 20** - JavaScript runtime

## 📚 Documentation

- **[Progress Bar Guide](PROGRESS_BAR_COMPLETE.md)** - Complete progress tracking documentation
- **[Setup Guide](docs/SETUP_GUIDE.md)** - Detailed setup instructions
- **[Working Status](WORKING_STATUS.md)** - Current project status
- **[API Docs](http://localhost:8000/docs)** - Interactive API documentation (when running)

## 🔒 Security Considerations

- ⚠️ **Change JWT Secret** in production (`BACKEND_JWT_SECRET`)
- ⚠️ **Set DEBUG=false** in production
- ⚠️ **Configure proper CORS** for your domain
- ⚠️ **Use HTTPS** in production
- ⚠️ **Add rate limiting** for public deployments
- ⚠️ **Secure Tavily API key**

## 📊 Performance

- **Generation Time**: 3-5 minutes (varies by hardware)
- **Memory Usage**: ~2GB RAM (with all services)
- **Disk Usage**: ~3GB (includes models)
- **CPU**: CPU-based LLM (no GPU required)
- **Concurrent Users**: Limited by CPU (single-threaded LLM)

## 🔐 Production Considerations

1. **Environment Variables**: Never commit `.env` files. Use secrets management.
2. **CORS**: Configure `CORS_ORIGINS` for your production domain.
3. **Rate Limiting**: Consider adding rate limiting middleware.
4. **Authentication**: JWT tokens with secure secrets.
5. **Database**: Consider persisting vector store and user data.
6. **Monitoring**: Set up APM tools (e.g., Sentry, DataDog).
7. **Scaling**: Use process managers (Gunicorn, Uvicorn workers) for production.

## 📝 License

This project is licensed under the MIT License - see [LICENSE](LICENSE) file for details.

## 🤝 Contributing

Contributions welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 🙏 Acknowledgments

- **Ollama** - For local LLM infrastructure
- **LangChain** - For LLM application framework
- **Tavily** - For web search capabilities
- **FastAPI** - For the excellent Python web framework
- **Next.js** - For the powerful React framework

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/yourusername/mapey/issues)
- **Documentation**: See `/docs` folder

---

<div align="center">

**Made with ❤️ by the Mapey Team**

⭐ Star us on GitHub if you find this helpful!

</div>

