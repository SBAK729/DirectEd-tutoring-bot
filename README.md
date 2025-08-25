# DirectEd E-Learning Platform AI Assistant

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104+-green.svg)](https://fastapi.tiangolo.com)
[![LangChain](https://img.shields.io/badge/LangChain-Latest-orange.svg)](https://langchain.com)
[![Docker](https://img.shields.io/badge/Docker-Ready-blue.svg)](https://docker.com)

A comprehensive AI-powered virtual assistant system for DirectEd's e-learning platform, built using LangChain orchestration with LangServe FastAPI backend. This intelligent system provides tutoring conversations, quiz generation, content analysis, and flashcard creation for both students and instructors through a unified interface.

## 🎯 Project Overview

This project implements an advanced educational AI assistant that combines conversational AI, retrieval-augmented generation (RAG), and fine-tuned language models to create a seamless learning experience. The system serves both students seeking personalized tutoring and instructors creating educational content.

### Key Features

- **🧠 Intelligent Tutoring**: Adaptive conversational AI for personalized student support
- **📝 Content Generation**: Automated quiz and flashcard creation aligned with curriculum
- **🔍 Smart Retrieval**: RAG-powered content search from DirectEd's curriculum database
- **📊 Learning Analytics**: Progress tracking and engagement analysis
- **🎓 Dual User Support**: Unified interface serving both students and instructors

## 🏗️ System Architecture

The system is built on four core LangChain components:

1. **EducationalRetriever**: Identifies relevant DirectEd curriculum content and learning materials
2. **AdaptiveConversationChain**: Produces personalized explanations using structured prompts and context
3. **ContentGenerator**: Creates practice questions, flashcards, and assessments based on curriculum materials
4. **LearningAnalyzer**: Monitors user engagement and adapts response approaches

## 🚀 Technology Stack

- **Backend Framework**: FastAPI with LangServe
- **AI Orchestration**: LangGraph
- **Language Models**: Groq
- **Vector Database**: ChromaDB
- **Fine-tuning**: LoRA (Low-Rank Adaptation)
- **Monitoring**: LangSmith
- **Containerization**: Docker & Docker Compose
- **API Documentation**: Swagger UI (FastAPI auto-generated), Postman

## 📋 Requirements

### System Requirements
- Python 3.8+
- Docker & Docker Compose
- 8GB+ RAM (for local vector database and model inference)
- Internet connection for LLM API calls

### API Keys Required
- OpenAI API Key OR Google Gemini API Key OR Groq API Key
- LangSmith API Key (for monitoring)

## 🛠️ Installation & Setup

### 1. Clone the Repository
```bash
git clone https://github.com/SBAK729/DirectEd-tutoring-bot
cd DirectEd-tutoring-bot

```

### 2. Create Virtual Environment
```bash
python -m venv venv
source venv/bin/activate 
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Environment Configuration
Create a `.env` file in the root directory:

```env
# LLM Configuration (choose one)
OPENAI_API_KEY=your_openai_api_key_here
GEMINI_API_KEY=your_gemini_api_key_here
GROQ_API_KEY=your_groq_api_key_here

# LangSmith Monitoring
LANGCHAIN_TRACING=true
LANGCHAIN_API_KEY=your_langsmith_api_key_here
LANGCHAIN_PROJECT=directed-ai-assistant

# Database
CHROMA_DB_PATH=./data/chroma

# API Configuration
API_HOST=0.0.0.0
API_PORT=8000
CORS_ORIGINS=["http://localhost:3000", "https://your-frontend-domain.com"]


### 5. Initialize Vector Database

# Create embeddings and populate ChromaDB
python scripts/build_knowledge_base.py
```

### 6. Run the Application

#### Development Mode
```bash
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

#### Production Mode with Docker
```bash
# Build and run with Docker Compose
docker-compose up --build -d

# View logs
docker-compose logs -f
```

### 7. Verify Installation
Visit `http://localhost:8000/docs` to access the interactive API documentation (Swagger UI).


### Core Endpoints

#### Chat Interface
```http
POST /api/assistant/chat
Content-Type: application/json

{
  "user_id": "string",
  "user_type": "string",
  "request_type": "string",
  "subject": "string",
  "auto_detect_topic": false,
  "difficulty_level": "intermediate",
  "query": "string"
}
```

#### Content Generation Response
```http
POST /api/assistant/content/generate
Content-Type: application/json

{
  "conversation_response": "string",
  "logs": [
    {
      "additionalProp1": {}
    }
  ]
}
```
## 🐳 Docker Deployment

### Local Development
```bash
# Start all services
docker-compose up -d

# View service status
docker-compose ps

# Stop services
docker-compose down
```

### Production Deployment

#### Build Production Image
```bash
docker build -t directed-ai-assistant:latest .
```

#### Deploy to Cloud (Render/Railway)
1. Connect your GitHub repository to your cloud platform
2. Set environment variables in the platform dashboard
3. Deploy using the provided `Dockerfile`


## 📊 Monitoring & Logging

### LangSmith Integration

Monitor your AI assistant's performance:
1. Visit [LangSmith Dashboard](https://smith.langchain.com)
2. View traces for each conversation
3. Analyze component performance
4. Debug prompt effectiveness

### Application Logs

Logs are structured and include:
- Component execution traces
- User interaction patterns
- Performance metrics
- Error tracking
- Security events


### Interface Design Guidelines

- **Sidebar Placement**: AI assistant chat interface integrates as expandable sidebar
- **Quick Actions**: One-click buttons for common educational tasks
- **Unified Input**: Single input field handles both conversation and quick actions


### API Performance

- **Rate Limiting**: Prevents API abuse
- **Connection Pooling**: Efficient database connections
- **Async Processing**: Non-blocking request handling
- **Response Compression**: Reduces bandwidth usage

## 🔐 Security

### Data Security

- **Input Validation**: Sanitize all user inputs
- **CORS Configuration**: Controlled cross-origin access
- **Rate Limiting**: DDoS protection

## 🛠️ Troubleshooting

### Common Issues

1. **ChromaDB Connection Issues**
   ```bash
   # Reset ChromaDB
   rm -rf ./data/chroma
   python scripts/build_knowledge_base.py
   ```

2. **API Rate Limits**
   - Check your API key limits
   - Implement exponential backoff
   - Consider upgrading API tier


3. **LangSmith Tracing Issues**
   - Verify `LANGCHAIN_API_KEY` is set
   - Check network connectivity to LangSmith

### Debug Mode

Enable debug logging:
```env
LOG_LEVEL=DEBUG
LANGCHAIN_VERBOSE=true
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Submit a pull request

---

## 📊 Project Status

- ✅ Core LangChain components implemented
- ✅ FastAPI backend with LangServe
- ✅ Docker containerization
- ✅ Basic authentication
- 🔄 LoRA fine-tuning implementation
- 🔄 Advanced monitoring setup
- ⏳ Production deployment
- ⏳ Frontend integration testing

**Last Updated**: August 25, 2025
**Version**: 1.0.0
**Build Status**: [![Build Status](https://img.shields.io/badge/build-passing-brightgreen.svg)](#)