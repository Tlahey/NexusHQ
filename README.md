# 🏢 NexusHQ

> **Stop chatting with AI. Start managing a workforce.**
> A 3D spatial interface to orchestrate, visualize, and manage autonomous AI agents running locally.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Stack](https://img.shields.io/badge/stack-React_Three_Fiber_|_FastAPI_|_Ollama-black)
![Status](https://img.shields.io/badge/status-Concept_Initialization-orange)

## 💡 The Vision

**NexusHQ** reimagines how we interact with LLMs. Instead of a linear chat window, we introduce a **spatial management system** modeled as a virtual headquarters.

- **The Building:** A global view of all your ongoing projects. Each "Room" represents a specific repository or task force.
- **The Workforce:** Agents are represented as 3D avatars. You can see them working, thinking, or waiting for feedback.
- **The Workflow:** A gamified experience where you assign "Skills" to agents (e.g., *Python Expert*, *SEO Wizard*) and watch them execute complex pipelines autonomously.

**Target:** 100% Local, 100% Open Source, Privacy-First.

## 🏗️ Architecture

The project follows a decoupled architecture to ensure smooth 3D rendering independent of heavy AI processing.

```mermaid
graph TD
    %% Nodes
    User([User / Manager])
    UI[Frontend: React + R3F]
    Store[State: Zustand]
    API[Backend: FastAPI]
    Crew[Orchestrator: CrewAI]
    Ollama[AI Engine: Ollama]
    FS[FileSystem: Workspace]

    %% Flow
    User -->|Interacts via 3D| UI
    
    subgraph "The View"
        UI <-->|Sync State| Store
    end

    UI <-->|WebSockets| API
    
    subgraph "The Brain"
        API -->|Delegates Task| Crew
        Crew -->|Read/Write Code| FS
    end
    
    Crew <-->|Inference| Ollama
