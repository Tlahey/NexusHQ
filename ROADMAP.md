# 🗺️ Project Roadmap: NexusHQ

This document outlines the step-by-step development plan for NexusHQ.
**Goal:** Build a spatial 3D interface to manage autonomous AI agents running locally via Ollama.

---

## 🏁 Phase 1: Infrastructure & "Hello World"
**Objective:** Set up the environment and ensure the 3D engine talks to the Local AI.

- [ ] **1.1. Project Initialization**
    - Create Monorepo structure (`/frontend`, `/backend`).
    - Initialize Git repository.
    - Set up `docker-compose.yml` (optional) for orchestrating services.

- [ ] **1.2. Backend Setup (FastAPI + Ollama)**
    - Install Python dependencies (`fastapi`, `uvicorn`, `langchain`, `crewai`).
    - Create a basic `/health` endpoint.
    - **Task:** Create a script `test_ollama.py` to verify connection to local Ollama (Llama 3).

- [ ] **1.3. Frontend Setup (React + Vite)**
    - Initialize React project with Vite.
    - Install 3D dependencies (`@react-three/fiber`, `@react-three/drei`, `three`).
    - Install UI dependencies (`tailwindcss`, `zustand`, `framer-motion`).

- [ ] **1.4. The First Handshake**
    - Create a WebSocket endpoint in FastAPI (`/ws`).
    - Connect React to the WebSocket.
    - **Goal:** Send a "Ping" from React, receive a "Pong" from Python, and display it in a 3D Text element.

---

## 🧠 Phase 2: The Brain (Agent Logic)
**Objective:** Define the agents and the "Ralph" workflow logic using CrewAI.

- [ ] **2.1. Agent Definitions (`/agents`)**
    - Define **Product Owner (PO):** Role = "Spec Definer", Goal = "Break down tasks".
    - Define **Developer:** Role = "Senior Python Dev", Goal = "Write clean code".
    - Define **QA (Ralph):** Role = "Code Reviewer", Goal = "Find bugs and security flaws".

- [ ] **2.2. Tool Creation (`/tools`)**
    - Implement `FileReadTool`: Allow agents to read local files.
    - Implement `FileWriteTool`: Allow agents to write code to a specific `./workspace` folder.

- [ ] **2.3. The Orchestration Logic**
    - Setup `Crew` class with the 3 agents.
    - Implement the **Conditional Logic**:
        - *If QA approves:* Return "SUCCESS".
        - *If QA rejects:* Loop back to Developer with the error message.

---

## 🎨 Phase 3: The Body (3D Visualization)
**Objective:** Build the "Office" and the Avatars in React Three Fiber.

- [ ] **3.1. The Environment (The Room)**
    - Create a `Room.jsx` component (Floor, Walls, Desk).
    - Add Lighting (AmbientLight + SpotLight for dramatic effect).
    - Implement `OrbitControls` to allow the user to rotate around the room.

- [ ] **3.2. The Avatars**
    - Import low-poly 3D models (using `.glb` format).
    - Create an `AgentAvatar.jsx` component.
    - **State Visuals:** Add a visual indicator above the head (Floating Text or Colored Halo).
        - 🟢 Idle
        - 🟡 Thinking (Pulsing effect)
        - 🔴 Error
        - 🔵 Typing

- [ ] **3.3. State Management (Zustand)**
    - Create `useAgentStore.js`.
    - Structure the store:
      ```javascript
      agents: {
        po: { status: 'IDLE', currentTask: '' },
        dev: { status: 'IDLE', currentTask: '' },
        qa: { status: 'IDLE', currentTask: '' }
      }
      ```

---

## 🔗 Phase 4: Integration (The Wiring)
**Objective:** Make the 3D scene react to the Backend events in real-time.

- [ ] **4.1. WebSocket Event Standardization**
    - Define JSON payloads for events:
      - `AGENT_START_TASK`: { agent: "PO", task: "..." }
      - `AGENT_THINKING`: { agent: "PO" }
      - `AGENT_OUTPUT`: { agent: "PO", content: "..." }
      - `WORKFLOW_COMPLETE`: { result: "..." }

- [ ] **4.2. Animation Triggers**
    - When Backend sends `DEV_TYPING`, trigger the specific animation on the Dev Avatar.
    - When QA sends `REJECTED`, draw a visible red line (laser) between QA and Dev.

- [ ] **4.3. The Console (HUD)**
    - Build a "Terminal" overlay component using HTML/CSS.
    - Display the raw logs coming from CrewAI in this terminal (Matrix style).

---

## 🧩 Phase 5: The Modular "Persona" System (BPMN)
**Objective:** Move from hardcoded agents to a dynamic workflow builder where users define Roles (Designer, Architect) and Flows.

- [ ] **5.1. The Node Editor (React Flow)**
    - Install `reactflow` library.
    - Create a `BlueprintEditor.jsx` view.
    - Create a custom `AgentNode` component with inputs for:
        - **Role:** (e.g., "UI Designer")
        - **Goal:** (e.g., "Create a color palette")
        - **Tools:** (Checkbox list: Search, FileWrite, ImageGen)

- [ ] **5.2. Dynamic Backend Instantiation**
    - Refactor `main.py` to accept a JSON payload describing the graph.
    - **Logic:** Instead of loading `class PO`, the backend iterates through the JSON nodes and spawns generic `Agent()` instances with the user's parameters.

- [ ] **5.3. Specialized Skills (The Toolbelt)**
    - **Image Gen Tool:** Integrate a connector (DALL-E or Local Stable Diffusion) for the "Designer" persona.
    - **Style Guide Tool:** A custom prompt tool that forces output in CSS/JSON format.

- [ ] **5.4. Graph Execution (LangGraph)**
    - Implement the logic to execute the graph edges:
        - *Sequential:* Node A -> Node B.
        - *Conditional:* Node A -> (If Error) -> Node A.

---

## 🕹️ Phase 6: User Interaction & Skills
**Objective:** Allow the user to control the simulation.

- [ ] **5.1. Input System**
    - Create a specialized Input Field in the UI to send the "Mission" to the PO.
    - Implement "Human-in-the-loop": Pause the backend after the PO's plan and wait for the user to click "Approve" in the UI.

- [ ] **5.2. Skill Assignment UI**
    - Create a drag-and-drop interface (HTML overlay).
    - **Logic:** Dragging a "Python Skill" icon onto the Dev Avatar updates the Agent's system prompt in the backend.

- [ ] **5.3. Multi-Project Support (The Building)**
    - Create a main menu to select different "Rooms" (Projects).
    - Save the state of each room (History of chats/code) in a local JSON file.

---

## ✨ Phase 7: Polish & Optimization
**Objective:** Make it look good and run smooth.

- [ ] **6.1. Performance Tuning**
    - Optimize 3D assets (compression).
    - Ensure WebSocket doesn't flood the frontend.

- [ ] **6.2. Visual Juice**
    - Add Bloom effects (Post-processing) for neon lights.
    - Add Sound Effects (Typing sounds, "Success" chime).

- [ ] **6.3. Documentation**
    - Write a tutorial on how to add new Agents.
    - Create a video demo.
