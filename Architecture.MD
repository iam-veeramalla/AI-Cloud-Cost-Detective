## AI Cloud Cost Detective - Architecture

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
