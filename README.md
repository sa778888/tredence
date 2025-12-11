
# Workflow Engine

A minimal workflow/graph execution engine built with FastAPI. Nodes are Python callables that read and modify a shared state dictionary. The system supports branching, looping, conditional edges, and a simple tool registry.

## Features

- Node-based workflow execution
- Shared mutable state passed through nodes
- Conditional transitions between nodes
- Looping via node-returned next steps
- Simple tool registry for reusable helper functions
- FastAPI endpoints to create and run graphs
- Sample Code Review Mini-Agent workflow

## Installation

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000
```

## API Endpoints

### POST /graph/create
Create a workflow graph.

### POST /graph/run
Run a graph with a given initial state.

### GET /graph/state/{run_id}
Retrieve the state and log of a run.

## Sample Workflow: Code Review Mini-Agent

1. Extract functions  
2. Check complexity  
3. Detect issues  
4. Suggest improvements  
5. Loop until quality score meets threshold

## Example Run

```bash
curl -X POST http://127.0.0.1:8000/graph/run \
  -H "Content-Type: application/json" \
  -d '{
    "graph_id": "code_review_sample",
    "initial_state": {
      "code": "def a(): pass\n# TODO improve",
      "threshold": 85
    }
  }'
```

## Future Improvements

- Persistent storage of graphs and execution runs
- WebSocket log streaming
- Safe condition parsing (remove eval)
- Improved validation of graph definitions
