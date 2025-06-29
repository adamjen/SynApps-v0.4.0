# SynApps v0.4.0 Memory Bank

## 1. Project Overview
*   **Name:** SynApps v0.4.0
*   **Description:** A web-based visual platform for modular AI agents (Snaplets) with database persistence and improved workflow execution.
*   **Mission:** To enable indie creators to build autonomous AI snaplets like LEGO blocks – each with specialized skills (e.g., Writer, Memory, Artist).
*   **Orchestrator Role:** A lightweight SynApps Orchestrator routes messages between snaplets, sequencing their interactions for collaborative task solving.

## 2. Key Features
*   **One-Click Creation & Simplicity:** Minimal steps to create AI workflows.
*   **Autonomous & Collaborative Snaplets:** Snaplets run autonomously and pass data via the orchestrator.
*   **Real-Time Visual Feedback:** Animated graph of nodes (snaplets) and connections (data flow).
*   **Background Execution & Notifications:** Snaplets run in the background with status notifications.
*   **Openness and Extensibility:** Supports user-editable snaplets via code for customization.

## 3. Architecture
*   **Microkernel Architecture**
    *   **Orchestrator:** Lightweight message routing core, manages workflow execution.
    *   **Applets (Snaplets):** Self-contained AI micro-agents with standard interfaces for specialized tasks.
    *   **Frontend:** React application with a visual workflow editor, built on React Flow and anime.js.
    *   **Database:** SQLite with async SQLAlchemy ORM for persistent storage of workflows and execution state.

## 4. Core Applets (MVP)
*   **WriterApplet:** Generates text using `gpt-4o`.
*   **MemoryApplet:** Stores/retrieves information using a vector store to maintain context.
*   **ArtistApplet:** Creates images from text descriptions using Stable Diffusion.

## 5. Setup & Local Development

### Prerequisites
*   [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/)
*   (Optional for local dev): Node.js 16+, Python 3.9+

### Running with Docker
1.  Clone repository: `git clone https://github.com/nxtg-ai/SynApps-v0.4.0.git`
2.  `cd SynApps-v0.4.0`
3.  Create `.env` file with `OPENAI_API_KEY`, `STABILITY_API_KEY`, `DATABASE_URL=sqlite+aiosqlite:///synapps.db`.
4.  Build and run: `docker-compose -f infra/docker/docker-compose.yml up --build`
5.  Access: [http://localhost:3000](http://localhost:3000)

### Local Development (Backend - Orchestrator)
1.  `cd apps/orchestrator`
2.  Install in dev mode: `pip install -e .`
3.  Create `.env` with `OPENAI_API_KEY`, `STABILITY_API_KEY`, `DATABASE_URL=sqlite+aiosqlite:///synapps.db`, `FRONTEND_URL=http://localhost:3000`.
4.  Run migrations: `alembic upgrade head`
5.  Start server: `uvicorn main:app --reload --port 8000`

### Local Development (Frontend)
1.  `cd apps/web-frontend`
2.  Install dependencies: `npm install`
3.  Create `.env` with `REACT_APP_API_URL=http://localhost:8000`, `REACT_APP_WEBSOCKET_URL=ws://localhost:8000/ws`.
4.  Start server: `npm start`

### Development Scripts
*   `./scripts/start-dev.sh` (kills existing processes on 8000/3000, starts both backend and frontend with hot-reloading).

## 6. Deployment
*   **Frontend:** Vercel
*   **Backend:** Fly.io
*   **CI/CD:** GitHub Actions

## 7. Database
*   **ORM Models:** SQLAlchemy for flows, nodes, edges, workflow runs.
*   **Migrations:** Alembic.
*   **Pattern:** Repository Pattern for data access.
*   **Support:** Full async/await for operations.

## 8. Testing
*   **Backend Tests:** `pytest` in `apps/orchestrator/tests/`
    *   Run: `cd apps/orchestrator && source venv/bin/activate && pytest -v`
*   **Frontend Tests:** Jest and React Testing Library, located alongside components.
    *   Run: `cd apps/web-frontend && npm test`

## 9. Contributing
*   Fork repository, create feature branch, commit changes, push to branch, open Pull Request.
*   See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

## 10. License
*   MIT License (see [LICENSE](LICENSE) file).

## 11. Acknowledgements
*   [React Flow](https://reactflow.dev/)
*   [anime.js](https://animejs.com/)
*   [FastAPI](https://fastapi.tiangolo.com/)
*   [Monaco Editor](https://microsoft.github.io/monaco-editor/)