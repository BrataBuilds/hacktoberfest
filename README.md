# Pixly - Your AI Gaming Assistant 🎮

Pixly is a sophisticated desktop gaming assistant that combines AI-powered chat functionality with automated screenshot capture to provide contextual gaming advice and support.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Python](https://img.shields.io/badge/python-3.11+-green.svg)
![Platform](https://img.shields.io/badge/platform-Windows-blue.svg)

## 🚀 Quick Start

### Table of Contents
- [Quick Start](#-quick-start)
- [Features](#-features)
- [Architecture Overview](#-architecture-overview)
- [Technology Stack](#-technology-stack)
- [Project Structure](#-project-structure)
- [Security & Privacy](#-security--privacy)
- [Contributing](#-contributing)
- [Troubleshooting](#-troubleshooting)

### Prerequisites
- Windows 10/11 (overlay + screenshot capture)
- Python 3.11+ (auto-installed by setup on Windows if missing)
- [`uv`](https://docs.astral.sh/uv/) (auto-installed by setup if missing)
- Google Gemini API key

### One‑click Setup (Windows)

1) Clone the repo
```bash
git clone <repository-url>
cd hacktoberfest
```

2) Run the setup script
- Double‑click `setup.bat` in File Explorer, or
```bat
setup.bat
```

What it does:
- Ensures Python, pip, and `uv` are installed
- Creates `.venv` and installs dependencies (`uv sync`)
- Creates `vector_db/` and `.env` (if missing)
- Starts the backend (`run.py`) in a new window, then launches the overlay (`overlay.py`)

3) Use Pixly
- Press `Ctrl+Alt+M` to toggle the overlay
- Start chatting with your AI gaming assistant!

### Manual Setup (alternative)

1) Create `.venv` and install dependencies with `uv`
```bash
uv venv .venv
.\.venv\Scripts\activate
uv sync
```

2) Create `.env` and add your API key
```ini
GOOGLE_API_KEY=your_api_key_here
```

3) Run the apps in two terminals
```bash
uv run run.py      # Terminal 1: backend
uv run overlay.py  # Terminal 2: overlay
```

## 🎯 Features

### 🤖 **Intelligent Gaming Assistant**
- AI-powered chatbot specialized in gaming knowledge
- Contextual advice based on what games you're currently playing
- Screenshot analysis for visual game elements
- Encyclopedic knowledge of video games, board games, and tabletop RPGs

### 📸 **Automated Screenshot Capture**
- Background monitoring of your gaming sessions
- Privacy-focused with local AES encryption
- Smart filtering by application type
- Configurable capture intervals
- Secure SQLite database storage

### 🖥️ **Modern Desktop Interface**
- Always-on-top overlay for quick access
- Global hotkey (`Ctrl+Alt+M`) for instant toggling
- Intuitive settings management
- Built-in screenshot viewer with gallery
- Dark theme with modern UI elements

## 🏗️ Architecture Overview

### Frontend Layer (`overlay.py`)
- **Technology**: CustomTkinter (modern Python GUI framework)
- **Design**: Floating overlay window with draggable interface
- **Components**:
  - Chat interface for AI conversations
  - Settings panel for configuration
  - Screenshot viewer and gallery
  - Semi-transparent, always-on-top design

### Backend Layer
The backend is structured with modular components:

#### API Server (`backend/backend.py`)
- **Framework**: FastAPI with automatic documentation
- **Port**: 127.0.0.1:8000
- **Endpoints**:
  - `/chat` - AI conversation interface
  - `/screenshots/*` - Screenshot management APIs
  - `/taskA`, `/taskB` - Extensible task endpoints

#### AI Chatbot (`backend/chatbot.py`)
- **Model**: Google Gemini 2.5 Flash Lite
- **Specialization**: Gaming expert personality
- **Features**: Context-aware responses using screenshot data

#### Screenshot System (`backend/screenshot.py`)
- **Encryption**: Fernet (AES 128) for secure storage
- **Database**: SQLite with optimized indexing
- **Monitoring**: Real-time window and application tracking

### Data Layer
- **Primary Database**: `screenshots.db` (encrypted SQLite)
- **Configuration**: JSON-based settings
- **Security**: Separate encryption key management

## 🛠️ Technology Stack

### Core Dependencies
```toml
customtkinter = ">=5.2.2"     # Modern GUI framework
fastapi = ">=0.117.1"         # Async web framework  
google-generativeai = ">=0.8.3"  # AI integration
uvicorn = ">=0.37.0"          # ASGI server
cryptography = ">=41.0.0"    # Encryption
pillow = ">=10.0.0"           # Image processing
psutil = ">=5.9.0"            # System monitoring
pywin32 = ">=306"             # Windows integration
keyboard = ">=0.13.5"         # Global hotkeys
requests = ">=2.32.5"         # HTTP client
```

### Development Tools
- **Package Manager**: [uv](https://github.com/astral-sh/uv) (fast Python package manager)
- **Configuration**: `pyproject.toml` (modern Python packaging)
- **Environment**: `.env` for sensitive configuration

## 📁 Project Structure

```
hacktoberfest/
├── backend/
│   ├── __init__.py          # FastAPI app initialization
│   ├── backend.py           # API endpoints and routing
│   ├── chatbot.py           # Gemini AI integration & prompt handling
│   └── screenshot.py        # Encrypted screenshot capture system
├── overlay.py               # Main GUI application with CustomTkinter
├── run.py                   # Backend server launcher
├── PROMPTS.txt              # AI system instructions and personality
├── pyproject.toml           # Project dependencies and metadata
├── screenshots.db           # Encrypted screenshot database (auto-created)
├── screenshot_key.key       # Encryption key (auto-generated)
└── README.md                # This file
```

## 🔒 Security & Privacy

- **Local Processing**: All data remains on your machine
- **Encryption**: Screenshots encrypted with AES before database storage
- **Key Management**: Separate encryption key file for data security
- **Minimal Network**: Only API calls to Google Gemini for AI responses
- **No Telemetry**: No data collection or tracking

## 🤝 Contributing

We welcome contributions! Here's how you can help:

### Development Setup

1. **Fork the repository** and clone your fork
2. **Install dependencies**: `uv sync`
3. **Create a feature branch**: `git checkout -b feature/your-feature-name`
4. **Set up your environment**: Copy `.env.example` to `.env` and add your API keys

### Code Style & Standards

- **Python**: Follow PEP 8 style guidelines
- **Imports**: Use absolute imports where possible
- **Documentation**: Add docstrings to new functions and classes
- **Type Hints**: Use type hints for function parameters and returns

### Areas for Contribution

- **🎮 Gaming Knowledge**: Expand the AI's gaming expertise
- **🔧 New Features**: Add new screenshot analysis capabilities
- **🎨 UI/UX**: Improve the interface design and user experience
- **🔒 Security**: Enhance encryption and privacy features
- **📱 Cross-platform**: Add support for macOS and Linux
- **🧪 Testing**: Add unit tests and integration tests
- **📚 Documentation**: Improve code documentation and guides

### Pull Request Process

1. **Test your changes** thoroughly
2. **Update documentation** if needed
3. **Submit a pull request** with a clear description
4. **Respond to feedback** during the review process

## 🐛 Troubleshooting

### Common Issues

**Backend won't start:**
- Check if port 8000 is available
- Verify your Google API key in `.env`
- Ensure all dependencies are installed with `uv sync`

**Frontend overlay not appearing:**
- Try the hotkey `Ctrl+Alt+M`
- Check if the backend is running first
- Verify Windows permissions for screen capture

**Screenshots not capturing:**
- Ensure the application has necessary Windows permissions
- Check the screenshot settings in the UI
- Verify the encryption key was generated correctly

### Windows setup script shows `... was unexpected at this time.`
- Close the terminal window and open a fresh Command Prompt, then run `setup.bat` again
- Ensure your PATH does not contain malformed entries; if the issue persists, open an issue with the full output

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Google Gemini** for AI capabilities
- **CustomTkinter** for modern GUI components
- **FastAPI** for robust backend framework
- **Hacktoberfest** community for open source collaboration

## 📧 Support

If you encounter any issues or have questions:

1. **Check the troubleshooting section** above
2. **Search existing issues** in the repository
3. **Create a new issue** with detailed information
4. **Join our community discussions** for help and tips

---

**Happy Gaming with Pixly! 🎮✨**