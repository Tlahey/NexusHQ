# 🏗️ Technical Architecture & Stack

This document details the technology choices, software architecture, and data flows for **NexusHQ**.

## 🔭 Overview

The project relies on a **decoupled client-server architecture** designed for local performance and an immersive user experience.

* **Frontend:** A Single Page Application (SPA) acting as a real-time 3D rendering engine.
* **Backend:** An asynchronous API that maintains agent state and manages execution loops.
* **AI Engine:** Pure local inference via Ollama.

```mermaid
graph TD
    subgraph "Local Machine (User PC)"
        Browser[Web Browser]
        Server[Python Server]
        Ollama[Ollama Service]
    end

    Browser -- "WebSocket (Events)" --> Server
    Browser -- "HTTP (Init/Config)" --> Server
    
    Server -- "LLM Prompts" --> Ollama
    Ollama -- "Inference Tokens" --> Server
    
    subgraph "Frontend Tech"
        React[React 18]
        R3F[React Three Fiber]
        Zustand[Zustand Store]
    end
    
    subgraph "Backend Tech"
        FastAPI[FastAPI]
        CrewAI[CrewAI]
        LangChain[LangChain]
    end

🎨 1. Frontend (The Visualizer)
The frontend is not just a dashboard; it is an interactive 3D environment (similar to a management video game).
| Component | Technology | Why this choice? |
|---|---|---|
| Framework | React 18 (Vite) | Rich ecosystem, fast HMR via Vite. |
| 3D Engine | React Three Fiber (R3F) | Declarative abstraction of Three.js. Allows managing 3D elements as React components. |
| 3D Helpers | Drei | Collection of utilities (Cameras, 3D Text, Environments). |
| State Manager | Zustand | Lighter than Redux. Handles "transient" state (high frequency) needed for 3D animations without unnecessary re-renders. |
| UI Overlay | TailwindCSS + Radix UI | For the 2D interface (HUD) overlaid on the 3D scene (buttons, consoles, logs). |
| Animation | React Spring | To interpolate agent movements smoothly (physics-based). |
Frontend Structure
src/
├── canvas/          # Everything living inside the 3D <Canvas>
│   ├── World.jsx    # The Building (Room container)
│   ├── Agent.jsx    # The 3D Avatar (Mesh + Animations)
│   └── Effects.jsx  # Post-processing (Bloom, lights)
├── hud/             # The 2D Overlay Interface
│   ├── Terminal.jsx # Log console
│   └── SkillTree.jsx# Skill Drag & Drop system
└── stores/          # Global State (Zustand)
    └── useGameStore.js

🧠 2. Backend (The Orchestrator)
The backend is the brain. It must be capable of handling multiple agents in parallel without blocking the user interface.
| Component | Technology | Why this choice? |
|---|---|---|
| Language | Python 3.10+ | The industrial standard for AI and Agentic workflows. |
| API Server | FastAPI | Native Async support (async/await) essential for WebSockets and LLM wait times. |
| Agent Framework | CrewAI | Natively handles roles, hierarchical delegation, and sequential processes. |
| LLM Connector | LangChain | Standardized interface to communicate with Ollama. |
| Communication | WebSockets | To push agent states (Thinking, Typing, Error) to the frontend in real-time. |
Backend Structure
app/
├── agents/          # Persona definitions
│   ├── po.py        # Product Owner logic
│   ├── dev.py       # Developer logic
│   └── qa.py        # QA logic
├── tools/           # Agent "Hands"
│   ├── file_io.py   # Read/Write files
│   └── search.py    # Web Search (optional)
├── api/
│   └── socket.py    # WebSocket Event Handler
└── main.py          # FastAPI Entry Point

🤖 3. Artificial Intelligence (Local)
The project follows a Local-First philosophy. No data leaves the machine, ensuring privacy and zero cost.
 * Inference Engine: Ollama (must run in the background on port 11434).
 * Recommended Models:
   * Llama-3-8B: Excellent intelligence/speed ratio for the PO and QA.
   * Mistral: Very fast for simple tasks.
   * CodeLlama or DeepSeek-Coder: Specialized for the "Developer" agent.
🔄 4. Data Flow (The Loop)
Here is how a user action traverses the stack:
 * Input: User types a request in the React HUD ("Create a Python backup script").
 * Transmission: React sends a JSON payload via WebSocket to the Backend.
 * Orchestration:
   * FastAPI receives the message and instantiates a Crew.
   * The PO agent analyzes the request.
   * Event: Backend sends status: "PO_THINKING" -> 3D PO Avatar lights up.
 * Execution:
   * PO delegates to Dev.
   * Dev generates code via Ollama.
   * Event: Backend sends status: "DEV_TYPING" -> Dev Avatar plays typing animation.
 * Validation:
   * The QA agent reads the generated file.
   * If OK: status: "SUCCESS" -> Confetti in 3D scene.
   * If KO: status: "REJECTED" -> Red laser from QA to Dev -> Loop restarts.
📦 Deployment & Environment
Currently, the project is designed to run on localhost.
 * Docker (Optional): A docker-compose.yml is provided to launch the Backend and Frontend together.
 * GPU Note: For Ollama to access the GPU from Docker, specific configuration (NVIDIA Container Toolkit) is required. It is often simpler to run Ollama on the host machine.
