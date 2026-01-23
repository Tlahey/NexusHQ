# 🗺️ Project Roadmap: NexusHQ

**Goal:** Build a spatial 3D interface to orchestrate autonomous AI agents using a visual BPMN editor, RPG-style character configuration, and real-world GitHub integration.

---

## 🏁 Phase 1: Infrastructure & Foundation
**Objective:** Set up the monorepo and ensure the "Hello World" communication works between the 3D scene and the Local AI.

- [ ] **1.1. Project Initialization**
    - [ ] Create Monorepo structure (`/frontend`, `/backend`).
    - [ ] Initialize Git repository & `.gitignore`.
    - [ ] Set up `docker-compose.yml` (optional) for services (Redis, etc.).

- [ ] **1.2. Backend Setup (FastAPI + LangGraph)**
    - [ ] Install dependencies (`fastapi`, `uvicorn`, `langchain`, `langgraph`, `crewai`).
    - [ ] Create `test_ollama.py` to verify connection to local models (Llama 3).
    - [ ] Create the `./workspace` directory for agents to write files.

- [ ] **1.3. Frontend Setup (React + Vite)**
    - [ ] Initialize React project.
    - [ ] Install core libs: `reactflow` (BPMN), `@react-three/fiber` (3D), `zustand` (State).
    - [ ] Setup TailwindCSS for the UI overlay.

- [ ] **1.4. The First Handshake**
    - [ ] Create a WebSocket endpoint in FastAPI (`/ws`).
    - [ ] Connect React to the WebSocket.
    - [ ] **Milestone:** Send a "Ping" from React, receive "Pong" from Python.

---

## 🧠 Phase 2: The Graph Engine (Backend)
**Objective:** Replace linear scripts with a dynamic Graph Compiler using LangGraph.

- [ ] **2.1. The JSON Protocol**
    - [ ] Define the JSON Schema: `nodes` (agents), `edges` (links), and `config`.
    - [ ] Create `graph_compiler.py`: A parser that reads JSON and builds a `StateGraph` object dynamically.

- [ ] **2.2. Dynamic Agent Factory**
    - [ ] Create a factory function to spawn Agents based on config (Role, System Prompt).
    - [ ] **The "Ralph" Logic:** Implement a conditional edge in LangGraph that checks output quality. If rejected, loop back to the previous node.

- [ ] **2.3. Tool Implementation (Skills)**
    - [ ] **FileSystem:** `FileRead`, `FileWrite`.
    - [ ] **Design:** `HtmlMockupGenerator` (Returns raw HTML/Tailwind string).
    - [ ] **Code:** `PythonRepl` (Safe execution).

---

## 🎮 Phase 3: The Builder Interface (Frontend 2D)
**Objective:** Build the "Character Creator" and the Node Editor. This is the core UX.

- [ ] **3.1. The Canvas (React Flow)**
    - [ ] Implement the drag-and-drop workspace.
    - [ ] Create custom Node components: `AgentNode`, `StartNode`, `EndNode`.

- [ ] **3.2. The "Inspector" Panel (RPG Style)**
    - [ ] Build a sliding side-panel (Drawer) triggered on Node click.
    - [ ] **Tab 1: Identity & Skin:** Carousel to select 3D models (Robot, Suit, Hoodie).
    - [ ] **Tab 2: Brain:** Markdown editor for the System Prompt (Backstory).
    - [ ] **Tab 3: Skills:** Visual grid to toggle tools (Git, Python, Search) and the "Ralph Protocol" switch.

- [ ] **3.3. Graph Serialization**
    - [ ] Implement `Export to JSON` function to send the blueprint to the Backend.

---

## 🎨 Phase 4: The 3D Simulation (Frontend 3D)
**Objective:** Build the "Office" where the graph comes to life.

- [ ] **4.1. The Environment**
    - [ ] Create `Room.jsx` (Floor, Walls, Lighting).
    - [ ] Implement Camera controls (Orbit + Focus on active agent).

- [ ] **4.2. 3D Avatars**
    - [ ] Import low-poly models (KayKit or similar).
    - [ ] Create `AgentAvatar.jsx` that accepts a `skin_id` prop.

- [ ] **4.3. Real-Time Animations**
    - [ ] Listen to WebSocket events (`NODE_ACTIVE`, `ERROR`, `SUCCESS`).
    - [ ] Trigger animations:
        - 💤 **Idle:** Standing.
        - ⌨️ **Working:** Typing at desk.
        - 🚨 **Ralph Reject:** Red strobe light / Alarm animation.

---

## 🖌️ Phase 5: The Designer Loop & Artifacts
**Objective:** Enable the "Design First" workflow with visual feedback.

- [ ] **5.1. The Designer Persona**
    - [ ] Configure the default "Designer" prompt (Focus on TailwindCSS/HTML).
    - [ ] Implement the `PO <-> Designer` loop in the backend (Textual analysis of HTML).

- [ ] **5.2. Artifact Viewer (UI)**
    - [ ] Create a "TV Screen" or "Preview Modal" in the 3D scene.
    - [ ] When the Designer generates HTML, render it safely in an `<iframe>`.
    - [ ] Add a "Human Approve/Reject" button to gate the workflow.

---

## 🐙 Phase 6: Real World Impact (GitHub)
**Objective:** Move from simulation to real repository contribution.

- [ ] **6.1. Auth Manager**
    - [ ] UI: Settings panel to input `GITHUB_TOKEN`.
    - [ ] Backend: Secure storage (Env var or encrypted).

- [ ] **6.2. The GitHub Skillset (PyGithub)**
    - [ ] `IssueTool`: Create GitHub Issues from PO specs.
    - [ ] `PullRequestTool`: Create branches, commit code, open PRs.
    - [ ] `ReviewTool`: Post comments on PR diffs (QA Agent).

- [ ] **6.3. The End-to-End Flow**
    - [ ] Test a full run: Idea -> Design Mockup -> Code -> PR Created.

---

## ✨ Phase 7: Polish & Persistence
**Objective:** Make it production-ready.

- [ ] **7.1. Save/Load System**
    - [ ] Save graph layouts to `localStorage` or local `.json` files.
    - [ ] "Team Presets": Load a standard "SaaS Startup Team" config.

- [ ] **7.2. Logs & Console**
    - [ ] Build a "Matrix-style" scrolling terminal in the HUD to see raw LLM thoughts.

- [ ] **7.3. Documentation**
    - [ ] Write a "Getting Started" guide.
    - [ ] Record a demo video.
