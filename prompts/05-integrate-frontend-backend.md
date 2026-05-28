# Prompt 5: Integrate Frontend with Backend via InsForge SDK

Connect the React frontend to the Python backend. Wire up InsForge Realtime for live progress and InsForge DB for history.

## What to build

### API Integration

- When the user clicks "Run Analysis" on the Dashboard, send a `POST /api/analyze` request to the Python backend with the selected resource group and the user's JWT token in the `Authorization` header.
- The backend should verify the JWT before processing.

### Realtime Progress

- Use the InsForge MCP tool `fetch-docs` with `docType: "real-time"` to read the realtime docs.
- After triggering analysis, subscribe to the `analysis:<id>` realtime channel in React.
- Display each progress message in the `ProgressTracker` component as it arrives (with a step indicator or animated list).

### History + Reports

- The History page should fetch from `GET /api/history` using the user's JWT.
- Clicking a past analysis should open the full Report page with all details.

### Analysis Report Display

- Show a summary card at the top with total resources scanned, issues found, and estimated savings.
- List each issue with: resource name, issue type (over-provisioned / unused / misconfigured), severity (high/medium/low with color badges), explanation, and a fix command in a copyable code block.

### Auth Guard

- Add JWT token to all API requests via an Authorization header.
- On the backend, add a middleware or dependency that validates the InsForge JWT on protected endpoints (`/api/analyze`, `/api/history`, `/api/resource-groups`).

Refer to `Architecture.MD` and `RequestFlow.MD`. This prompt covers the full end-to-end integration — steps ① through ⑦.
