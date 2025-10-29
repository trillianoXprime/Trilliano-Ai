# ₮ⱤłⱠⱠł₳₦Ø ₳ł

<div align="center">

**₮ⱤłⱠⱠł₳₦Ø ₲ⱠØ฿₳Ⱡ Ɇ₥₱łⱤɆ — by Mohammed Zafeer Ansari**

*Advanced AI Assistant with Multi-Modal Capabilities*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![React Native](https://img.shields.io/badge/React%20Native-0.72+-green.svg)](https://reactnative.dev/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104+-red.svg)](https://fastapi.tiangolo.com/)
[![Docker](https://img.shields.io/badge/Docker-Ready-blue.svg)](https://www.docker.com/)

[🚀 Demo](#demo) • [📱 Features](#features) • [🏗️ Architecture](#architecture) • [⚡ Quick Start](#quick-start) • [📚 Documentation](#documentation)

</div>

---

## 🌟 Overview

Trilliano AI is a comprehensive, privacy-first AI assistant platform that combines cutting-edge artificial intelligence with professional-grade user experience. Unlike conventional AI chatbots, Trilliano offers true multi-modal integration, local processing capabilities, and unique features like multi-perspective analysis.

### 🎯 Key Differentiators

- **🔒 Privacy-First**: Complete local processing option with no data leaving your device
- **🎭 Multi-Perspective Analysis**: Unique feature providing diverse viewpoints on any topic
- **🎨 Professional Design**: Custom glassmorphic interface with accessibility-first approach
- **🔧 Multi-Provider Support**: Works with OpenAI, Anthropic, Google, and local models
- **📱 Cross-Platform**: Native mobile experience with React Native

## ✨ Features

- **💬 Intelligent Chat**: Multi-provider LLM support with conversation memory
- **🎨 Image Generation**: Photorealistic image creation with style presets
- **🎤 Voice Interface**: Speech-to-text and text-to-speech capabilities
- **🔍 Multi-Perspective Analysis**: Get diverse viewpoints on any topic
- **🛡️ Content Moderation**: Three-stage filtering for safe interactions
- **🌟 Glassmorphic UI**: Beautiful black and emerald green interface
- **🔒 Privacy-First**: Local model support with optional API integration

## 🏗️ Architecture

```
trilliano-ai/
├── backend/           # FastAPI backend application
│   ├── app/          # Main application code
│   ├── models/       # Database models
│   ├── services/     # Business logic
│   └── adapters/     # AI model integrations
├── frontend/         # React Native mobile app
│   └── src/
│       ├── screens/  # App screens
│       ├── components/ # Reusable components
│       ├── services/ # API integration
│       └── theme/    # Design system
├── models/           # Local AI models storage
├── docker/           # Container configurations
└── docs/             # Documentation
```

## 🚀 Quick Start

### Prerequisites

- **Python 3.11+** with pip
- **Node.js 18+** with npm
- **Git** for version control
- **Docker** (optional, for containerized deployment)
- **FFmpeg** (for audio processing)
- **CUDA-compatible GPU** (optional, for local model acceleration)

### Installation

#### 1. Clone and Setup Environment

```bash
# Clone the repository
git clone <repository-url>
cd trilliano-ai

# Copy environment configuration
cp .env.example .env
cp backend/.env.example backend/.env

# Edit .env files with your configuration
# See Configuration section below for details
```

#### 2. Backend Setup

```bash
cd backend

# Create virtual environment (recommended)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Initialize database
python -c "from models.database import init_db; init_db()"

# Start development server
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

#### 3. Frontend Setup

```bash
cd frontend

# Install dependencies
npm install

# Install Expo CLI globally (if not already installed)
npm install -g @expo/cli

# Start development server
npm start

# Or run on a specific platform
npm run ios     # iOS simulator
npm run android # Android emulator
npm run web     # Web browser
```

#### 4. Docker Deployment (Alternative)

```bash
# Development environment
docker-compose up -d

# Production environment
docker-compose -f docker-compose.prod.yml up -d

# View logs
docker-compose logs -f backend
docker-compose logs -f frontend
```

### Verification

After setup, verify the installation:

1. **Backend Health Check**: Visit `http://localhost:8000/health`
2. **API Documentation**: Visit `http://localhost:8000/docs`
3. **Frontend**: Open Expo app and scan QR code or visit `http://localhost:19006`

## 🔧 Configuration

### Environment Variables

Configure the application by editing `.env` and `backend/.env` files:

#### Core Settings
```bash
# Application
APP_NAME="Trilliano AI"
APP_VERSION="1.0.0"
DEBUG=true
LOG_LEVEL="INFO"

# Database
DATABASE_URL="sqlite:///./data/trilliano.db"
DATABASE_POOL_SIZE=10

# Security
SECRET_KEY="your-secret-key-here"
JWT_ALGORITHM="HS256"
JWT_EXPIRE_MINUTES=1440

# CORS
ALLOWED_ORIGINS="http://localhost:19006,exp://192.168.1.100:19000"
```

#### API Keys (Optional)

The application defaults to working with local models. For enhanced capabilities, add API keys:

```bash
# LLM Providers
OPENAI_API_KEY="sk-..."
ANTHROPIC_API_KEY="sk-ant-..."
GOOGLE_API_KEY="AIza..."
HUGGINGFACE_API_TOKEN=" hf_..."

# Image Generation
REPLICATE_API_TOKEN="r8_..."
STABILITY_API_KEY="sk-..."

# Voice Services
ELEVENLABS_API_KEY="..."
AZURE_SPEECH_KEY="..."
AZURE_SPEECH_REGION="eastus"

# Content Moderation
OPENAI_MODERATION_API_KEY="sk-..."
PERSPECTIVE_API_KEY="AIza..."
```

#### Model Configuration
```bash
# Local Model Paths
LOCAL_LLM_MODEL_PATH="models/local/llm"
LOCAL_IMAGE_MODEL_PATH="models/local/stable-diffusion-xl"
LOCAL_WHISPER_MODEL_PATH="models/local/whisper"
LOCAL_TTS_MODEL_PATH="models/local/coqui-tts"

# Model Settings
DEFAULT_LLM_PROVIDER="local"  # local, openai, anthropic, google
DEFAULT_IMAGE_PROVIDER="local"  # local, replicate, stability
DEFAULT_VOICE_PROVIDER="local"  # local, elevenlabs, azure

# Performance
MAX_TOKENS=2048
TEMPERATURE=0.7
IMAGE_GENERATION_TIMEOUT=120
VOICE_PROCESSING_TIMEOUT=30
```

### Local Models Setup

#### Download Models

```bash
# Create models directory
mkdir -p models/local

# Download LLM model (example: Llama 2 7B)
cd models/local
git lfs clone https://huggingface.co/microsoft/DialoGPT-medium llm

# Download Stable Diffusion XL
git lfs clone https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0 stable-diffusion-xl

# Download Whisper model
git lfs clone https://huggingface.co/openai/whisper-base whisper

# Download Coqui TTS model
git lfs clone https://huggingface.co/coqui/XTTS-v2 coqui-tts
```

#### GPU Acceleration (Optional)

For CUDA-enabled GPUs:

```bash
# Install PyTorch with CUDA support
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118

# Verify CUDA installation
python -c "import torch; print(torch.cuda.is_available())"
```

### Frontend Configuration

Edit `frontend/app.json` for app-specific settings:

```json
{
  "expo": {
    "name": "Trilliano AI",
    "slug": "trilliano-ai",
    "version": "1.0.0",
    "orientation": "portrait",
    "icon": "./assets/icon.png",
    "userInterfaceStyle": "dark",
    "splash": {
      "image": "./assets/splash.png",
      "resizeMode": "contain",
      "backgroundColor": "#050505"
    },
    "assetBundlePatterns": ["**/*"],
    "ios": {
      "supportsTablet": true,
      "bundleIdentifier": "com.trillianoai.app"
    },
    "android": {
      "adaptiveIcon": {
        "foregroundImage": "./assets/adaptive-icon.png",
        "backgroundColor": "#050505"
      },
      "package": "com.trillianoai.app"
    },
    "web": {
      "favicon": "./assets/favicon.png"
    }
  }
}

## 📱 Mobile App

The React Native frontend provides:

- **Cross-platform**: iOS and Android support
- **Offline Mode**: Works without internet connection
- **Glassmorphic Design**: Modern UI with blur effects
- **Accessibility**: Screen reader and high contrast support
- **Animations**: Smooth transitions with Framer Motion

## 🛡️ Content Moderation

Three-stage filtering system:

1. **Regex/Keyword**: Immediate blocking of obvious violations
2. **ML Classification**: Context-aware content analysis
3. **Educational Override**: Allow academic content with warnings

## 🔒 Security & Privacy

- **Local-First**: All processing can happen on-device
- **Encrypted Storage**: Sensitive data protection
- **API Key Security**: Environment-based key management
- **Rate Limiting**: Abuse prevention
- **Audit Logging**: Compliance tracking

## 📊 Performance

- **Async Processing**: Non-blocking operations
- **Model Caching**: Reduced loading times
- **Connection Pooling**: Efficient database access
- **Progressive Loading**: Smooth user experience

## 🧪 Testing

```bash
# Backend tests
cd backend
pytest

# Frontend tests
cd frontend
npm test
```

## 🔍 API Documentation

### Chat Endpoint

**POST** `/api/v1/chat`

Generate AI responses with conversation context.

```bash
curl -X POST "http://localhost:8000/api/v1/chat" \
  -H "Content-Type: application/json" \
  -d '{
    "session_id": "user-123",
    "message": "What is artificial intelligence?",
    "options": {
      "model": "gpt-3.5-turbo",
      "temperature": 0.7,
      "max_tokens": 1024
    }
  }'
```

**Response:**
```json
{
  "reply": "Artificial intelligence (AI) refers to...",
  "sources": ["https://example.com/ai-definition"],
  "used_providers": ["openai"],
  "session_id": "user-123",
  "timestamp": "2024-01-01T12:00:00Z"
}
```

### Image Generation Endpoint

**POST** `/api/v1/image`

Generate images from text prompts.

```bash
curl -X POST "http://localhost:8000/api/v1/image" \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "A futuristic cityscape at sunset",
    "style": "photorealistic",
    "width": 1024,
    "height": 1024,
    "nsfw_override": false
  }'
```

**Response:**
```json
{
  "image_url": "/api/v1/images/generated/abc123.png",
  "metadata": {
    "model": "stable-diffusion-xl",
    "seed": 42,
    "steps": 50,
    "guidance_scale": 7.5
  },
  "generation_time": 15.2
}
```

### Voice Endpoints

**POST** `/api/v1/voice/stt` (Speech-to-Text)

```bash
curl -X POST "http://localhost:8000/api/v1/voice/stt" \
  -H "Content-Type: multipart/form-data" \
  -F "audio=@recording.wav"
```

**POST** `/api/v1/voice/tts` (Text-to-Speech)

```bash
curl -X POST "http://localhost:8000/api/v1/voice/tts" \
  -H "Content-Type: application/json" \
  -d '{
    "text": "Hello, this is Trilliano AI speaking.",
    "voice": "default",
    "format": "wav"
  }'
```

### Multi-Perspective Analysis

**POST** `/api/v1/chat/perspectives`

```bash
curl -X POST "http://localhost:8000/api/v1/chat/perspectives" \
  -H "Content-Type: application/json" \
  -d '{
    "question": "Should AI be regulated?",
    "perspectives": 3
  }'
```

**Response:**
```json
{
  "perspectives": [
    {
      "viewpoint": "Pro-regulation",
      "reasoning": "AI regulation ensures safety...",
      "confidence": 0.85,
      "sources": ["policy-paper-1.pdf"]
    },
    {
      "viewpoint": "Anti-regulation",
      "reasoning": "Excessive regulation stifles innovation...",
      "confidence": 0.78,
      "sources": ["tech-report-2.pdf"]
    },
    {
      "viewpoint": "Balanced approach",
      "reasoning": "Smart regulation with industry collaboration...",
      "confidence": 0.92,
      "sources": ["academic-study-3.pdf"]
    }
  ]
}
```

## 🛠️ Troubleshooting

### Common Issues

#### Backend Issues

**Issue: "ModuleNotFoundError: No module named 'app'"**
```bash
# Solution: Ensure you're in the backend directory and the virtual environment is activated
cd backend
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

**Issue: "Database connection failed"**
```bash
# Solution: Initialize the database
python -c "from models.database import init_db; init_db()"

# Or reset the database
rm data/trilliano.db
python -c "from models.database import init_db; init_db()"
```

**Issue: "CUDA out of memory"**
```bash
# Solution: Reduce model size or use CPU
export CUDA_VISIBLE_DEVICES=""  # Force CPU usage
# Or edit .env file:
# LOCAL_LLM_MODEL_PATH=" models/local/smaller-model"
```

**Issue: "API key not found"**
```bash
# Solution: Check environment variables
python -c "import os; print(os.getenv('OPENAI_API_KEY'))"

# Ensure .env file is in the correct location and properly formatted
```

#### Frontend Issues

**Issue: "Metro bundler failed to start"**
```bash
# Solution: Clear cache and restart
cd frontend
npm start -- --clear-cache

# Or reset node_modules
rm -rf node_modules package-lock.json
npm install
```

**Issue: "Expo app won't connect"**
```bash
# Solution: Check network connectivity
# Ensure backend is running on the correct port
curl http://localhost:8000/health

# Update CORS settings in backend/.env
# ALLOWED_ORIGINS="http://localhost:19006,exp://YOUR_IP:19000"
```

**Issue: "Audio recording not working"**
```bash
# Solution: Check permissions
# iOS: Add microphone usage description in app.json
# Android: Ensure RECORD_AUDIO permission is granted
```

#### Docker Issues

**Issue: "Container fails to start"**
```bash
# Solution: Check logs
docker-compose logs backend
docker-compose logs frontend

# Rebuild containers
docker-compose down
docker-compose build --no-cache
docker-compose up -d
```

**Issue: "Port already in use"**
```bash
# Solution: Stop conflicting services
sudo lsof -i:8000  # Find process using port 8000
sudo kill -9 <PID>

# Or change ports in docker-compose.yml
```

### Performance Optimization

#### Slow Model Loading
```bash
# Use smaller models for development
export LOCAL_LLM_MODEL_PATH=" models/local/distilbert-base"

# Enable model caching
export MODEL_CACHE_ENABLED=true
export MODEL_CACHE_SIZE=2048  # MB
```

#### High Memory Usage
```bash
# Limit concurrent requests
export MAX_CONCURRENT_REQUESTS=2

# Reduce model precision
export MODEL_PRECISION="fp16"  # or "int8"
```

#### Network Timeouts
```bash
# Increase timeout values in .env
export API_TIMEOUT=120
export MODEL_TIMEOUT=300
```

### FAQ

**Q: Can I use the app without internet?**
A: Yes, with local models installed, the app works completely offline.

**Q: How do I add custom models?**
A: Place Hugging Face compatible models in `models/local/` and update the model path in `.env`.

**Q: Is my data stored or shared?**
A: All data is stored locally by default. API providers may log requests if you use their services.

**Q: How do I update the app?**
A: Pull the latest code, rebuild containers, and restart services:
```bash
git pull origin main
docker-compose down
docker-compose build --no-cache
docker-compose up -d
```

**Q: Can I customize the UI theme?**
A: Yes, edit `frontend/src/theme/` files to customize colours, fonts, and animations.

## 📚 Documentation

- [API Documentation](docs/API.md)
- [Deployment Guide](docs/DEPLOYMENT.md)
- [Configuration Guide](docs/CONFIGURATION.md)
- [Model Integration](docs/MODELS.md)
- [Contributing Guidelines](docs/CONTRIBUTING.md)
- [Privacy Policy](docs/PRIVACY.md)
- [Terms of Service](docs/TERMS.md)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Attribution

Built with love using:

- [FastAPI](https://fastapi.tiangolo.com/) - Modern Python web framework
- [React Native](https://reactnative.dev/) - Cross-platform mobile development
- [Hugging Face](https://huggingface.co/) - AI model ecosystem
- [Stable Diffusion](https://stability.ai/) - Image generation
- [Whisper](https://openai.com/research/whisper) - Speech recognition
- [Expo](https://expo.dev/) - React Native development platform

## 🤝 Contributing

Contributions are welcome! Please read our [Contributing Guidelines](docs/contributing.md) for details on our code of conduct and the process for submitting pull requests.

## 📞 Support

For support, email [trillianoprime@gmail.com](mailto:trillianoprime@gmail.com) or join our [Discord community](https://discord.gg/trillianoxprime).

---

**₮ⱤłⱠⱠł₳₦Ø ₳ł** - Empowering conversations with artificial intelligence.
