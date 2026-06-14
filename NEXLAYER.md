# Nexlayer — AutoGPT

<!-- nexlayer:meta version=1 analyzed=2026-06-14T22:00:51Z repo=https://github.com/armondhonore/AutoGPT branch=master -->

> **For AI agents (Claude Code, Cursor, Gemini CLI, Copilot):**
> This file is the **project context** for this Nexlayer deployment — tech stack, env vars, secrets, live URL.
> For full platform detail (nexlayer.yaml schema, Dockerfile rules, CI/CD, task recipes) read **`nexlayer.skills`** in this repo.
>
> **Critical rules (full detail in `nexlayer.skills`):**
> - Inter-pod refs: `${podName:port}` only — never `localhost` or bare hostnames
> - Docker Hub images: prefix with `mirror.gcr.io/library/` — bare tags fail on the cluster
> - Secrets: set in the Nexlayer dashboard — never commit to `nexlayer.yaml` or Dockerfile
>
> **This file:** `agent-managed` sections update automatically. `user-editable` sections (Local Development Setup, Nexlayer Deployment Plan, Build Notes) are yours — preserved across re-analysis.

## Project Summary
<!-- nexlayer:section agent-managed=project_summary -->
AutoGPT is an autonomous AI agent platform designed to create, deploy, and manage agents that automate complex workflows through continuous execution.
<!-- nexlayer:end -->

## Technology Stack
<!-- nexlayer:section agent-managed=tech_stack -->
| Name | Kind | Version | Detected From |
|------|------|---------|---------------|
| Node.js | language | 22 | .nvmrc |
| Python | language | 3.10+ | classic/ |
| Docker | infra | latest | .dockerignore |
<!-- nexlayer:end -->

## Repository Structure
<!-- nexlayer:section agent-managed=structure_map -->
- autogpt_platform/ — Core platform logic and orchestration
- classic/ — Original AutoGPT implementation
- .agents/ — Agent configuration and definitions
- docs/ — Project documentation
<!-- nexlayer:end -->

## External Services Required
<!-- nexlayer:section agent-managed=external_deps -->
Services that must be configured separately (not deployed by Nexlayer):

- OpenAI API
- Anthropic API
<!-- nexlayer:end -->

## Local Development Setup
<!-- nexlayer:section user-editable=local_setup -->
### Prerequisites

- Node.js 22
- Python 3.10+
- Docker Desktop / WSL2

### Environment variables

Copy `.env.example` to `.env.local` and fill in:

```
OPENAI_API_KEY=your_key
PORT=3000
```

### Steps

1. `npm install` — Install frontend/platform dependencies
2. `pip install -r requirements.txt` — Install AI agent backend dependencies
3. `npm run dev` — Start the AutoGPT platform locally

<!-- nexlayer:end -->

## Nexlayer Setup
<!-- nexlayer:section agent-managed=nexlayer_setup -->
### nexlayer.yaml

```yaml
application:
  name: deep-tide-autogpt
  pods:
    - name: app
      image: "# filled by pipeline"
      path: /
      servicePorts:
        - 3000
      vars: {}
```

<!-- nexlayer:end -->

## Nexlayer Deployment Plan
<!-- nexlayer:section user-editable=deployment_plan -->
### Pod Topology

| Pod | Image | Port | Role |
|-----|-------|------|------|
| autogpt-web | mirror.gcr.io/library/node:22-alpine | 3000 | web |
| autogpt-backend | mirror.gcr.io/library/python:3.11-slim | 8000 | worker |
| autogpt-db | mirror.gcr.io/library/postgres:16-alpine | 5432 | database |

### Inter-pod environment variables

- `autogpt-web` pod: `BACKEND_URL=${autogpt-backend:8000}`
- `autogpt-backend` pod: `DATABASE_URL=${autogpt-db:5432}`

### Deployment notes

- Adheres to one-service-per-pod rule: separating the Node.js frontend, Python backend, and Postgres DB.
- Inter-pod communication established via ${podName:port} syntax.
- Images mapped to mirror.gcr.io to satisfy Nexlayer cluster requirements.

<!-- nexlayer:end -->

## Build Notes
<!-- nexlayer:section user-editable=build_notes -->
<!-- Add notes for future builds here — preserved across re-analysis -->
<!-- nexlayer:end -->

## Nexlayer Configuration
<!-- nexlayer:section agent-managed=nexlayer_config -->
**Last deployed:** 2026-06-14T22:19:10Z  
**Live URL:** https://awesome-moose-deep-tide-autogpt.cloud.nexlayer.ai  
**Runtime:** node · **Port:** 3000  
**Deploy branch:** master  

```yaml
application:
  name: deep-tide-autogpt
  pods:
    - name: app
      image: "# filled by pipeline"
      path: /
      servicePorts:
        - 3000
      vars: {}
```
<!-- nexlayer:end -->

## Build History
<!-- nexlayer:section agent-managed=build_history -->
| Date | Status | Notes |
|------|--------|-------|
| 2026-06-14T22:00:51Z | analyzed | initial repo analysis |
| 2026-06-14T22:19:10Z | success | deployed https://awesome-moose-deep-tide-autogpt.cloud.nexlayer.ai |
<!-- nexlayer:end -->
