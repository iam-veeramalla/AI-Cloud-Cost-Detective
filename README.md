# AI Cloud Cost Detective

An AI-powered tool that investigates Azure cloud costs automatically. It scans resources in an Azure Resource Group, detects cost issues like over-provisioning and misconfigurations, and provides actionable suggestions with fixes.

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React |
| Backend | Python (FastAPI) |
| Auth | InsForge Auth |
| Cloud Data | Azure CLI |
| Cloud | Azure |
| AI Analysis | InsForge AI (OpenRouter) |
| Database | InsForge DB (PostgreSQL) |
| Live Updates | WebSocket |

## Architecture

```
                              ┌──────────────┐
                              │     USER     │
                              └──────┬───────┘
                                     │
                                     ▼
                           ┌───────────────────┐
                           │  REACT FRONTEND   │
                           └────────┬──────────┘
                                    :
                                    ▼
                             ┌─────────────┐
                             │  INSFORGE   │
                             │    AUTH     │
                             └──────┬──────┘
                                    :
                                    : JWT
                                    ▼
                           ┌───────────────────┐
                           │  PYTHON BACKEND   │
                           │    (FastAPI)      │
                           └───┬───────┬───┬───┘
                               :       :   :
                ┌──────────────┘       :   └──────────────┐
                :                      :                  :
                ▼                      ▼                  ▼
         ┌─────────────┐     ┌──────────────┐    ┌──────────────┐
         │  AZURE CLI  │     │  INSFORGE    │    │  INSFORGE    │
         │             │     │  REALTIME    │    │     AI       │
         │ az resource │     │ (WebSocket)  │    │ (OpenRouter) │
         │ list --rg   │     └──────┬───────┘    └──────┬───────┘
         └──────┬──────┘            :                   :
                :                   : Progress          : Analysis
                ▼                   ▼                   :
         ┌─────────────┐   ┌───────────────┐            :
         │   AZURE     │   │    REACT      │            :
         │ (Resource   │   │  (Live UI     │            :
         │   Group)    │   │   Updates)    │            :
         └─────────────┘   └───────────────┘            :
                                                        ▼
                                                 ┌─────────────┐
                                                 │  INSFORGE   │
                                                 │     DB      │
                                                 │ (PostgreSQL)│
                                                 └──────┬──────┘
                                                        :
                                                        : Stored results
                                                        ▼
                                                 ┌───────────────┐
                                                 │    REACT      │
                                                 │ (Final Report │
                                                 │  + Suggestions│
                                                 │  + Fixes)     │
                                                 └───────────────┘
```

## Request Flow

```
①  User ─·─·─► React ─·─·─► InsForge Auth ─·─·─► JWT

②  User selects Resource Group ─·─·─► Python Backend

③  Python ─·─·─► Azure CLI ─·─·─► Fetches all resources in RG

④  Python ─·─·─► InsForge Realtime ─·─·─► React (live progress)

⑤  Python ─·─·─► InsForge AI (OpenRouter) ─·─·─► Cost analysis

⑥  Python ─·─·─► InsForge DB ─·─·─► Stores analysis history

⑦  React ◄·─·─·─ Final report with suggestions & fixes
```

## What It Detects

- **Over-provisioned resources** — VMs, App Services, or databases sized larger than needed
- **Unused resources** — Orphaned disks, unattached public IPs, idle load balancers
- **Misconfigurations** — Wrong pricing tiers, missing auto-shutdown, no reserved instances
- **Storage & logging costs** — Excessive log retention, no lifecycle policies on blob storage

## How It Works

1. User logs in via InsForge Auth
2. Selects an Azure Resource Group to analyze
3. Python backend fetches all resources using Azure CLI
4. Live progress is streamed to the UI via InsForge Realtime
5. Resource data is sent to InsForge AI (OpenRouter) for cost analysis
6. Analysis results are stored in InsForge DB
7. Final report with cost breakdown, suggestions, and fix commands is displayed
