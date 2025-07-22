# 🐛 FastAPI Debug Requirements & Setup Guide

A comprehensive guide for setting up debugging in FastAPI projects with VS Code.
This guide provides everything you need to debug FastAPI applications effectively.

## 📦 Debug Dependencies

```bash
# Core debugging requirements
debugpy>=1.8.0              # Python debugger for VS Code
uvicorn[standard]>=0.24.0   # ASGI server with full features

# Testing and debugging
pytest>=7.4.0               # Testing framework
pytest-asyncio>=0.21.0      # Async test support
httpx>=0.25.0                # HTTP client for testing FastAPI
pytest-cov>=4.1.0           # Coverage reporting

# Development tools
black>=23.0.0                # Code formatter
isort>=5.12.0                # Import sorter
flake8>=6.0.0                # Linting
mypy>=1.5.0                  # Type checking
pre-commit>=3.4.0            # Git hooks

# Optional but recommended
rich>=13.0.0                 # Better console output
ipython>=8.0.0               # Enhanced Python shell
watchdog>=3.0.0              # File watching for auto-reload
```

## 🔧 VS Code Debug Configuration

Create `.vscode/launch.json`:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Debug FastAPI App",
            "type": "debugpy",
            "request": "launch",
            "program": "${workspaceFolder}/main.py",
            "console": "integratedTerminal",
            "env": {
                "DEBUG": "true",
                "LOG_LEVEL": "DEBUG",
                "PYTHONPATH": "${workspaceFolder}"
            },