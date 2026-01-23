# 🏢 NexusHQ

> **Stop chatting with AI. Start managing a workforce.**
> A 3D spatial interface to orchestrate, visualize, and manage autonomous AI agents running locally.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Stack](https://img.shields.io/badge/stack-React_Three_Fiber_|_FastAPI_|_Ollama-black)
![Status](https://img.shields.io/badge/status-Concept_Initialization-orange)

## 💡 The Vision: Modular Agentic BPMN

**NexusHQ** is not just a fixed team; it is a **dynamic workflow builder**.
We bring the **BPMN (Business Process Model and Notation)** concept to AI orchestration.

- **Draw your Strategy:** Use the integrated Node Editor to design your workflow visually.
- **Modular Blocks:** Drag & drop blocks like "LLM Agent", "Human Validation", "Python Tool", or "API Call".
- **Infinite Combinations:**
    - *Scenario A:* User (You) -> Developer Agent -> User (Validation).
    - *Scenario B:* PO -> Dev -> QA -> Dev (Loop) -> Manager.
    - *Scenario C:* Research Agent -> Summarizer Agent -> Email Tool.
- **3D Visualization:** Once the graph is designed, switch to "3D View" to watch the agents execute the graph physically in the building.
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
