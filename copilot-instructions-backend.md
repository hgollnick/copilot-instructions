# AI Local Companion - Backend Copilot Instructions

## Architecture Overview

This is the backend component of a multi-service AI router system:
- **Backend**: FastAPI server with intelligent LLM routing (`backend/src/`)
- **Ollama**: Local LLM service orchestrated via Docker Compose

The core concept is **context-aware LLM routing** - different models handle different query types (code, simple, complex) based on configurable rules in `agent_config.json`.

## Key Components

### Router Architecture
- `RouterAgent` (`backend/src/agent/basic/router_agent.py`) - Main routing logic with two modes:
  - **Basic router** (preferred): Technology-agnostic, uses simple prompt-based classification for "code", "simple", or "complex"
  - **LangChain router**: Experimental option via `langchain_router_agent.py` (unstable, may be replaced with AutoGen or similar)
- Specialized agents inherit from `OllamaService`: `CodeAgent`, `FastAgent`, `GeneralAgent`
- Switch between routers via `use_langchain_router` config flag (default: false for stability)

### Configuration System
- `agent_config.json` - Runtime model assignments and router selection
- `src/config.py` - Config loading with automatic backup and defaults
- Models are mapped: `router_model` → classification, `code_model` → programming, `simple_model` → quick queries, `complex_model` → nuanced responses

### Service Communication
- All LLM calls go through `OllamaService` (`backend/src/commons/ollama_service.py`)
- Docker services communicate via container names: `http://ollama:11434`, `http://backend:8000`
- Environment variables: `OLLAMA_URL` for backend

## Development Workflows

### Local Development (Development Only)
```bash
# Start full stack with hot reload
docker-compose up --build

# Backend only (with debugpy on port 5678)
cd backend && uvicorn src.main:app --reload

# Run tests
cd backend && python -m unittest discover -s tests
```

### VS Code Task Integration
Use the predefined task "Docker Compose: Build and Up" for consistent development environment setup.

## Project-Specific Patterns

### Import Conventions
- Absolute imports from project root: `from src.config import load_config`