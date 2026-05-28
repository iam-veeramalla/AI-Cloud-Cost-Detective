# Prompt 1: FastAPI Backend + Azure CLI

Create a Python FastAPI backend in a `backend/` folder for the AI Cloud Cost Detective project.

## What to build

- A FastAPI server with a `POST /api/analyze` endpoint that accepts `{ "resource_group": "<name>" }` in the request body.
- A `GET /api/resource-groups` endpoint that returns the list of Azure resource groups available in the logged-in Azure account.
- Use Python's `subprocess` module to run Azure CLI commands:
  - `az group list` to list all resource groups.
  - `az resource list --resource-group <name> -o json` to fetch all resources in the selected group.
- Parse the Azure CLI JSON output and return a clean structured response with resource type, name, location, SKU, and tags.
- Add proper error handling for cases where Azure CLI is not installed, not logged in, or the resource group doesn't exist.
- Include a `requirements.txt` with `fastapi` and `uvicorn`.
- Enable CORS for `http://localhost:5173` (React dev server).

## Project structure

```
backend/
├── main.py
├── azure_scanner.py
├── requirements.txt
```

`main.py` — FastAPI app with routes.
`azure_scanner.py` — Functions that shell out to Azure CLI and return parsed JSON.

Refer to `Architecture.MD` and `RequestFlow.MD` for the overall system design. This prompt covers step ③ of the request flow.
