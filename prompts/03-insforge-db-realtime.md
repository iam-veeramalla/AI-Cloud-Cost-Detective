# Prompt 3: InsForge DB + Realtime Progress Tracking

Build on top of the existing FastAPI backend. Add analysis history storage in InsForge DB and live progress updates via InsForge Realtime.

## What to build

### Database (InsForge DB)

- Use the InsForge MCP tool `fetch-docs` with `docType: "db-sdk"` to read the database docs. Follow those docs exactly.
- Use the InsForge MCP tool `run-raw-sql` to create an `analyses` table with columns: `id`, `user_id`, `resource_group`, `resources_scanned` (int), `issues_found` (int), `estimated_savings`, `analysis_result` (jsonb), `status`, `created_at`.
- After AI analysis completes, store the full result in this table.
- Add a `GET /api/history` endpoint that returns past analyses for the user.

### Realtime Progress (InsForge Realtime)

- Use the InsForge MCP tool `fetch-docs` with `docType: "real-time"` to read the realtime docs. Follow those docs exactly.
- During the `POST /api/analyze` flow, push progress updates at each stage:
  - `"Fetching resource groups..."`
  - `"Scanning resources in <rg>..."`
  - `"Analyzing costs with AI..."`
  - `"Storing results..."`
  - `"Analysis complete"`
- Use a channel name like `analysis:<analysis_id>` so the frontend can subscribe per analysis.

## Project structure update

```
backend/
├── main.py          (updated - add history endpoint, progress pushes)
├── azure_scanner.py (no change)
├── ai_analyzer.py   (no change)
├── db.py            (new - InsForge DB operations)
├── requirements.txt (updated if needed)
```

Refer to `Architecture.MD` and `RequestFlow.MD`. This prompt covers steps ④ and ⑥ of the request flow.
