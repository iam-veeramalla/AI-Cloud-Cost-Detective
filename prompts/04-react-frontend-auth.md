# Prompt 4: React Frontend + InsForge Auth

Create the React frontend in a `frontend/` folder with authentication using InsForge Auth.

## What to build

### Setup

- Use Vite + React + TypeScript.
- Use Tailwind CSS for styling. Make the UI clean, modern, and dark-themed.

### Auth (InsForge)

- Use the InsForge MCP tool `fetch-docs` with `docType: "auth-sdk"` to read the auth docs. Follow those docs exactly.
- Create Login and Signup pages using InsForge Auth (email/password).
- Protect all other pages behind authentication. Redirect to login if not authenticated.

### Pages

1. **Login / Signup** — Clean auth forms with email and password.
2. **Dashboard** — Shows a dropdown to select an Azure Resource Group (fetched from `GET /api/resource-groups`), a "Run Analysis" button, and a progress section that shows live status updates.
3. **Analysis Report** — Displays the AI analysis result: summary, list of issues with severity badges, estimated savings, and fix commands in copyable code blocks.
4. **History** — Lists past analyses from `GET /api/history` with resource group name, date, issues found, and estimated savings. Clicking one opens the full report.

### Project structure

```
frontend/
├── src/
│   ├── App.tsx
│   ├── main.tsx
│   ├── pages/
│   │   ├── Login.tsx
│   │   ├── Signup.tsx
│   │   ├── Dashboard.tsx
│   │   ├── Report.tsx
│   │   └── History.tsx
│   ├── components/
│   │   ├── ProgressTracker.tsx
│   │   └── Navbar.tsx
│   └── lib/
│       └── insforge.ts
├── package.json
├── tailwind.config.js
├── index.html
```

Refer to `Architecture.MD` and `RequestFlow.MD`. This prompt covers step ① of the request flow and the UI layer.
