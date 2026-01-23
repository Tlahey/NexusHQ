# 🗺️ Project Roadmap: NexusHQ

This document outlines the step-by-step development plan for **NexusHQ**.
**Goal:** Build a spatial 3D interface to orchestrate autonomous AI agents using a visual BPMN editor and RPG-style character configuration.

---

## 🏁 Phase 1: Infrastructure & "Hello World"
**Objective:** Set up the monorepo environment and ensure the local stack communicates correctly.

- [ ] **1.1. Project Initialization**
    - Create Monorepo structure (`/frontend`, `/backend`).
    - Initialize Git repository with `.gitignore`.
    - Set up `docker-compose.yml` (optional) for orchestrating services.

- [ ] **1.2. Backend Setup (FastAPI + Ollama)**
    - Install Python dependencies (`fastapi`, `uvicorn`, `langchain`, `langgraph`, `crewai`).
    - **Task:** Create a script `test_ollama.py` to verify connection to local Ollama (Llama 3).
    - Create the `./workspace` directory for agents to write files.

- [ ] **1.3. Frontend Setup (React + Vite)**
    - Initialize React project.
    - Install core libraries: `reactflow` (BPMN), `@react-three/fiber` (3D), `zustand` (State).
    - Setup TailwindCSS for the UI overlay.

- [ ] **1.4. The First Handshake**
    - Create a WebSocket endpoint in FastAPI (`/ws`).
    - Connect React to the WebSocket.
    - **Goal:** Send a "Ping" from the React client and receive a "Pong" from the Python server.

---

## 🧠 Phase 2: The Graph Engine (Backend)
**Objective:** Move from hardcoded scripts to a dynamic graph execution engine (LangGraph).

- [ ] **2.1. The JSON Protocol**
    - Define the JSON Schema for a workflow: `nodes` (agents), `edges` (links), and `config`.
    - Create a parser in Python that reads this JSON and constructs a `LangGraph` object.

- [ ] **2.2. Dynamic Agent Factory**
    - Create a function that instantiates `CrewAI` agents on the fly based on incoming parameters (Role, Goal, Model).
    - **The "Ralph" Logic:** Implement a middleware that checks if `use_ralph_protocol` is true. If yes, wrap the agent's output in a validation loop.

- [ ] **2.3. Tool Implementation**
    - **Core Tools:** `FileRead`, `FileWrite`.
    - **Advanced Tools:** `WebSearch` (DuckDuckGo), `PythonRepl` (for code execution).

---

## 🎮 Phase 3: The Builder Interface (RPG Style)
**Objective:** Build the "Character Creator" and the Node Editor. This is the core UX.

- [ ] **3.1. The Canvas (React Flow)**
    - Implement the drag-and-drop workspace.
    - Create custom Node components:
        - `AgentNode`: Represents an AI worker.
        - `StartNode` / `EndNode`.

- [ ] **3.2. The "Inspector" Panel (Drawer)**
    - Build a sliding side-panel that opens when a Node is clicked.
    - Implement Tabs: **Identity**, **Brain**, **Skills**.

- [ ] **3.3. Tab 1: Identity & Visuals (Skins)**
    - **Skin Selector:** A carousel to choose the agent's 3D look (e.g., *Cyberpunk Dev*, *Corporate Suit*, *Robot*).
    - **Name & Role:** Input fields for "Persona Name" and "Job Title".

- [ ] **3.4. Tab 2: Brain (Markdown Context)**
    - Integrate a text editor (Monaco or simple textarea).
    - Allow users to write the "Backstory" or specific instructions in Markdown (e.g., *"You are a Senior React Dev, you hate jQuery"*).

- [ ] **3.5. Tab 3: The Skill Tree**
    - **UI:** Create a visual grid of icons (Hexagonal or Tree).
    - **Logic:** Clicking an icon adds the tool to the agent's config.
    - **The Ralph Switch:** A special toggle button: *"Enable Ralph Code Validation"*. When active, this agent's work will be double-checked.

---

## 🎨 Phase 4: The 3D Simulation (Visualization)
**Objective:** Build the "Office" where the graph comes to life.

- [ ] **4.1. The Environment**
    - Create a `Room.jsx` component using R3F.
    - Add environmental lighting and a floor grid.

- [ ] **4.2. 3D Avatars & Skins**
    - Import low-poly models corresponding to the skins chosen in Phase 3.
    - Create an `AgentAvatar.jsx` component that accepts a `skinId` prop.

- [ ] **4.3. State Visuals**
    - Add animations/indicators for agent states:
        - 💤 **Idle:** Standing still.
        - 💡 **Thinking:** Pulsing halo / "..." bubble.
        - ⌨️ **Working:** Typing animation.
        - 🚨 **Error/Ralph Reject:** Red alert symbol.

---

## 🔗 Phase 5: Integration (The Wiring)
**Objective:** Connect the 2D Builder to the 3D Simulation via the Backend.

- [ ] **5.1. The "Build" Button**
    - Action: User clicks "Run Simulation" in the 2D Editor.
    - Result: The JSON graph is sent to the Backend, and the view switches to the 3D Room.

- [ ] **5.2. Real-Time Event Mapping**
    - **Backend:** Emit WebSocket events during LangGraph execution (`NODE_ENTER`, `TOOL_USE`, `NODE_EXIT`).
    - **Frontend:** Listen to events and trigger 3D animations (e.g., Agent A throws a "packet" to Agent B).

- [ ] **5.3. The Console (HUD)**
    - Create a terminal overlay to show the raw logs ("Thinking...", "File saved to /workspace").

---

## ✨ Phase 6: Polish & Persistence
**Objective:** Make it usable for real projects.

- [ ] **6.1. Save/Load System**
    - Save the BPMN graph layout to `localStorage` or a local JSON file.
    - Allow loading previous "Team Configurations".

- [ ] **6.2. Custom Assets**
    - Allow users to add their own `.glb` models for avatars.

- [ ] **6.3. Documentation**
    - Write a "Getting Started" guide to creating your first Autonomous Squad.
