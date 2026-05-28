## AI Cloud Cost Detective - Request Flow

```
①  User ─·─·─► React ─·─·─► InsForge Auth ─·─·─► JWT

②  User selects Resource Group ─·─·─► Python Backend

③  Python ─·─·─► Azure CLI ─·─·─► Fetches all resources in RG

④  Python ─·─·─► InsForge Realtime ─·─·─► React (live progress)

⑤  Python ─·─·─► InsForge AI (OpenRouter) ─·─·─► Cost analysis

⑥  Python ─·─·─► InsForge DB ─·─·─► Stores analysis history

⑦  React ◄·─·─·─ Final report with suggestions & fixes
```
