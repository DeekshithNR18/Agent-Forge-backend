# Autonomous AI Engineering Team — Backend

This repository contains the backend for our Autonomous AI Engineering Team project, developed as part of a hackathon.

The main idea is to build a system where different AI agents work together to handle different stages of software development, from understanding a requirement to testing and preparing an application for deployment.

## What does the backend do?

The backend connects the frontend with the AI agents and manages the overall workflow.

- Receives software requirements from the frontend
- Creates and manages projects
- Coordinates the different agents
- Tracks agent status and project progress
- Stores task details, test results, security results and execution logs
- Returns project information to the frontend through REST APIs

## Technologies Used

- Python
- FastAPI
- Uvicorn
- Pydantic
- REST APIs and JSON

## Project Structure

```text
app/
├── main.py
├── api/
│   └── routes.py
├── agents/
│   ├── base_agent.py
│   ├── planner.py
│   ├── architect.py
│   ├── coder.py
│   ├── tester.py
│   ├── debugger.py
│   ├── security.py
│   ├── deployer.py
│   └── registry.py
└── orchestrator/
    ├── coordinator.py
    └── state.py

requirements.txt
README.md
```

## How It Works

1. The user enters a software requirement through the frontend.
2. The backend receives the requirement and creates a new project with a unique ID.
3. The orchestrator manages the workflow and calls the agents in sequence.
4. The Planner prepares the tasks, and the Architect defines the application structure.
5. The Coder handles implementation, followed by testing and debugging.
6. The Security agent reviews security-related areas.
7. The Deployer prepares the application for deployment.
8. The backend returns the project status and available results to the frontend.

The project uses a shared `ProjectState` to keep track of the requirement, plan, architecture, tasks, agent statuses, test results, security results and logs.

The `registry.py` file provides a central place to register and connect the agents. This makes it easier to integrate the actual AI agents developed by other team members.

## Setup and Installation

Make sure Python is installed on your system.

**1. Clone the repository**

```bash
git clone <your-github-repository-url>
cd <your-repository-folder>
```

**2. Create a virtual environment**

```bash
python -m venv venv
```

**3. Activate the environment**

For Windows PowerShell:

```powershell
.\venv\Scripts\Activate.ps1
```

**4. Install the required packages**

```bash
python -m pip install -r requirements.txt
```

**5. Start the backend**

```bash
python -m uvicorn app.main:app --reload
```

## Access the API

Once the server starts, open these URLs in your browser.

- **Backend:** http://127.0.0.1:8000
- **API documentation:** http://127.0.0.1:8000/docs
- **Health check:** http://127.0.0.1:8000/health

The Swagger page can be used to test the endpoints without connecting the frontend first.

## Main API Endpoints

| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/` | Check the backend response |
| GET | `/health` | Check whether the backend is running |
| POST | `/projects` | Create a project |
| POST | `/projects/{project_id}/plan` | Run the planning stage |
| POST | `/projects/{project_id}/run` | Run the complete workflow |
| GET | `/projects/{project_id}` | Retrieve project information |

## Integration with the Frontend and AI Agents

The frontend communicates with the backend through REST APIs using JSON.

The backend manages the project workflow, while the Agent Registry connects the orchestrator to the agents. The actual AI agent implementations can be integrated through this layer, provided they follow the expected interface or use an adapter.

## Current Status

The backend provides the basic API structure, project state management, agent registry and sequential workflow orchestration.

Some of the initial agents are prototype implementations used to test the workflow. Their current behavior does not represent a fully autonomous AI engineering system yet; actual AI reasoning, code generation, execution and validation depend on integrating the team's AI agents.

Project data is currently stored in memory, so active projects are cleared when the backend restarts.

## Future Improvements

- Integrate the team's actual AI agents
- Add database support for persistent project storage
- Improve error handling and agent recovery
- Support background execution for longer workflows
- Add real-time progress updates to the frontend
- Improve testing, security validation and deployment support

## Team Project

This backend is one part of our Autonomous AI Engineering Team project. It is designed to work with the frontend and AI agents developed by the other team members.
