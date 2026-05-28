# Prompt 2: InsForge AI (OpenRouter) Integration

Build on top of the existing FastAPI backend. Add AI-powered cost analysis using InsForge's model gateway (OpenRouter).

## What to build

- Use the InsForge MCP tool `fetch-docs` with `docType: "ai-integration-sdk"` to read the InsForge AI integration docs. Follow those docs exactly for setup and API usage.
- Create an `ai_analyzer.py` module in `backend/` that:
  - Takes the list of Azure resources (from `azure_scanner.py`) as input.
  - Builds a prompt asking the AI to analyze the resources for: over-provisioning, unused/idle resources, misconfigurations, wrong pricing tiers, and cost optimization opportunities.
  - Sends the prompt to InsForge AI (OpenRouter) and returns the structured analysis.
- The AI response should include: a summary, list of issues found (with severity), estimated savings, and actionable fix commands (Azure CLI commands the user can run).
- Update the `POST /api/analyze` endpoint to call `azure_scanner` first, then pass the results to `ai_analyzer`, and return the final analysis.
- Store InsForge credentials (URL, API key) in environment variables. Add a `.env.example` file.

## Project structure update

```
backend/
├── main.py          (updated)
├── azure_scanner.py (no change)
├── ai_analyzer.py   (new)
├── requirements.txt (updated - add httpx, python-dotenv)
├── .env.example     (new)
```

Refer to `Architecture.MD` and `RequestFlow.MD`. This prompt covers step ⑤ of the request flow.
