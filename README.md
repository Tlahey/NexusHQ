Voici le fichier `README.md` complet et définitif. Il intègre toutes nos discussions : l'architecture BPMN, l'interface 3D, la configuration style RPG, le Designer Agent, et l'intégration GitHub.

Tu peux copier-coller ce bloc directement à la racine de ton projet.

---

```markdown
# 🏢 NexusHQ

> **Stop chatting with AI. Start managing a workforce.**
> A local-first, spatial 3D interface to orchestrate autonomous AI agents using visual BPMN workflows.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Stack](https://img.shields.io/badge/stack-React_Three_Fiber_|_FastAPI_|_LangGraph-black)
![AI](https://img.shields.io/badge/AI-Ollama_Local-orange)

<div align="center">
  <img src="docs/screenshot-mockup.png" alt="NexusHQ Interface" width="100%" />
</div>

## 💡 The Vision

**NexusHQ** reimagines how we build software with LLMs. We move away from linear chat windows to a **Spatial Management System**.

Instead of prompting a black box, you:
1.  **Design** your team's workflow visually (BPMN).
2.  **Configure** your agents like RPG characters (Skins, Stats, Skills).
3.  **Observe** them working in a 3D virtual office.
4.  **Deploy** their work directly to GitHub.

**Target:** 100% Local (Ollama), Privacy-First, Open Source.

## ✨ Key Features

- **🎮 RPG-Style Agent Config:** Customize your workforce. Give the "Designer" a beret and a high creativity temp. Give the "QA" a robot skin and strict validation protocols.
- **🗺️ Visual Workflow Builder:** Use a node-based editor (React Flow) to design complex loops (e.g., `Dev -> QA -> Dev`).
- **🎨 Design-First Approach:** The **Designer Agent** generates live HTML/Tailwind mockups for validation *before* any backend code is written.
- **🛡️ The "Ralph" Protocol:** A strictly enforced QA loop. Code is not finished until the "Ralph" agent (Linter + Logic Check) approves it.
- **🐙 Real-World GitHub Integration:** Agents don't just chat. They open Issues, create Branches, push commits, and review Pull Requests.

## 🏗️ Architecture

NexusHQ uses a decoupled architecture to handle heavy AI logic without freezing the 3D interface.

```mermaid
graph TD
    User([User])
    
    subgraph "Frontend (The View)"
        UI[React Flow: BPMN Builder]
        HUD[RPG Inspector Panel]
        Sim[R3F: 3D Simulation]
    end

    subgraph "Backend (The Brain)"
        API[FastAPI]
        Graph[LangGraph Engine]
        Crew[CrewAI Agents]
    end

    subgraph "External / Local Tools"
        Ollama[Ollama (Llama-3/Mistral)]
        GitHub[GitHub API]
        FS[Local FileSystem]
    end

    User -->|Designs| UI
    UI -->|JSON Config| API
    API -->|Executes| Graph
    Graph -->|Spawns| Crew
    
    Crew <-->|Inference| Ollama
    Crew -->|Commit/PR| GitHub
    Crew -->|Write Code| FS
    
    Graph -->|Real-time Events| Sim

```

## 🔄 The Core Workflow

NexusHQ implements a specific "Software Factory" pipeline by default, though you can modify it.

1. **Ideation:** You chat with the **Product Owner (PO)** to define specs.
2. **Visualization:** The **Designer Agent** reads specs and generates a `mockup.html` (TailwindCSS).
3. **Human Gate:** You review the mockup in the UI.
* *Reject:* Feedback loop back to Designer.
* *Approve:* Triggers the Build phase.


4. **Construction:** The **Developer Agent** writes the React/Python code based on the approved visual.
5. **Validation (Ralph):** The **QA Agent** reviews the code.
6. **Deployment:** The agents open a Pull Request on your GitHub repo.

## 🚀 Getting Started

### Prerequisites

* **Python 3.10+**
* **Node.js 18+**
* **[Ollama](https://ollama.com/)** running locally (`ollama serve`).

### 1. Installation

```bash
# Clone the repository
git clone [https://github.com/yourusername/nexushq.git](https://github.com/yourusername/nexushq.git)
cd nexushq

# --- Backend Setup ---
cd backend
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install -r requirements.txt

# --- Frontend Setup ---
cd ../frontend
npm install

```

### 2. Configuration

Create a `.env` file in `./backend`:

```ini
# API Settings
PORT=8000
DEBUG=true

# AI Provider (Local)
OLLAMA_BASE_URL=http://localhost:11434
MODEL_PO=llama3
MODEL_DESIGNER=llama3
MODEL_DEV=codellama

# GitHub Integration (Optional)
GITHUB_ACCESS_TOKEN=your_token_here
TARGET_REPO=your_username/target_repo

```

### 3. Running NexusHQ

**Terminal 1 (Backend):**

```bash
cd backend
uvicorn main:app --reload

```

**Terminal 2 (Frontend):**

```bash
cd frontend
npm run dev

```

Open `http://localhost:5173` and build your first team!

## 🗺️ Roadmap

* [ ] **Phase 1: Foundation** - Setup R3F scene and basic FastAPI <-> Ollama handshake.
* [ ] **Phase 2: The Graph Engine** - Implement LangGraph for dynamic PO/Designer loops.
* [ ] **Phase 3: RPG Interface** - Build the "Inspector" drawer to configure agent skins and skills.
* [ ] **Phase 4: 3D Simulation** - Connect WebSocket events to Avatar animations (Typing, Thinking).
* [ ] **Phase 5: GitHub Connector** - Implement `PyGithub` tools for real repository management.

## 🤝 Contributing

This is a community-driven experiment in **Agentic UX**.
Feel free to open issues for new "Skins", "Skills", or architectural improvements.

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

```

```
