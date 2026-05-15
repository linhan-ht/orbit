# Orbit — Project Plan

> An AI agent that understands your work, calls your APIs, and delivers what you need.

## 1. Problem Statement

Enterprise employees spend hours every week:
- Searching for documents across wikis, Jira, Confluence, Slack
- Pulling manual reports from dashboards that are hard to use
- Asking colleagues "who owns this?" or "where's the process for X?"
- Filling out spreadsheets with data they had to manually gather

**Orbit** solves this by letting employees talk to their company's systems naturally — and getting back formatted, useful outputs (reports, dashboards, files) in seconds.

## 2. Core Principles

1. **Employee-owned** — Orbit knows who you are, what team you're on, and what you have access to
2. **Natural language first** — You describe what you need, not which API to call
3. **Zero learning curve** — If you can chat, you can use Orbit
4. **Output adapts to need** — Data → Dashboard. List → Table. File → Download.

## 3. Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     Employee                                │
│           (WeChat / Zoom / Web / any channel)               │
└─────────────────────┬───────────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────────┐
│                   OpenClaw Gateway                          │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐  │
│  │   Channel   │  │   Memory   │  │   Skill Framework   │  │
│  │  Router     │  │   System   │  │                     │  │
│  └─────────────┘  └─────────────┘  └─────────────────────┘  │
└─────────────────────┬───────────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────────┐
│                    Orbit Skills                             │
│                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │
│  │  Auth Skill  │  │  API Router  │  │  Output Renderer │  │
│  │  (Okta OAuth)│  │  (intent →  │  │  (JSON → HTML /  │  │
│  │              │  │   API call) │  │   CSV / Excel)   │  │
│  └──────────────┘  └──────────────┘  └──────────────────┘  │
└─────────────────────┬───────────────────────────────────────┘
                      │
         ┌────────────┴────────────┐
         │                         │
  ┌──────▼──────┐          ┌──────▼──────┐
  │  Okta       │          │  Company    │
  │  Identity   │          │  Backend    │
  │  Provider   │          │  APIs       │
  └─────────────┘          └─────────────┘
```

### 3.1 Skills

| Skill | Responsibility |
|-------|---------------|
| **Okta Auth** | PKCE OAuth flow, token storage, refresh, user identity resolution |
| **API Router** | Parse user intent → determine which API(s) to call → execute with user's token |
| **Output Renderer** | Take API JSON response → determine best format → generate HTML Dashboard / CSV / Excel |

### 3.2 Data Flow

1. Employee sends message (e.g. "Show me open VOU tickets about search")
2. OpenClaw routes to Orbit agent with user context
3. API Router skill interprets intent → calls Jira API with user's Okta token
4. Jira returns JSON → Output Renderer decides format (table + chart)
5. Formatted output sent back to employee in the same channel

## 4. Development Phases

### Phase 0 — Foundation (Week 1)
**Goal:** End-to-end demo with one real API

- [ ] Set up OpenClaw skill structure
- [ ] Implement Okta OAuth helper skill (PKCE flow, token management)
- [ ] Implement API Router skill with Jira as the first target
- [ ] Basic JSON → HTML table rendering
- [ ] Run full flow: WeChat → Orbit → Jira → HTML response

**Deliverable:** "Show me open VOU tickets" returns a formatted table in WeChat.

---

### Phase 1 — Output Variety (Week 2–3)
**Goal:** Multiple output formats based on data type

- [ ] CSV / Excel export (for list/table data)
- [ ] HTML Dashboard generation (for metrics/time-series)
- [ ] Intelligent format selection (small list → table, time-series → chart, large data → CSV)
- [ ] Handle paginated APIs correctly

**Deliverable:** Employee can ask for data in different formats and get the right output.

---

### Phase 2 — Multi-API Router (Week 4–5)
**Goal:** Support multiple backend APIs beyond Jira

- [ ] Generic API config format (define an API once, agent learns to call it)
- [ ] Confluence / Wiki integration (for process documentation)
- [ ] AWS/EKS cost API (for infrastructure queries)
- [ ] Monitoring/alerting API (for on-call questions)

**Deliverable:** Adding a new API to Orbit takes hours, not days.

---

### Phase 3 — RAG for Knowledge (Week 6–7)
**Goal:** Enable natural questions over company knowledge base

- [ ] Connect to company RAG / vector database
- [ ] Agentic RAG pattern: retrieve docs → validate relevance → answer or escalate
- [ ] Handle cross-document queries (e.g. "what's the full deployment process?")
- [ ] Fallback to "I couldn't find enough info" vs hallucinating

**Deliverable:** "What's our policy on X?" returns accurate, sourced answers.

---

### Phase 4 — Polish & Enterprise (Week 8+)
**Goal:** Production-ready for company-wide rollout

- [ ] Admin panel: which APIs / data each team can access
- [ ] Audit logging (who asked what, which data was returned)
- [ ] Rate limiting and cost controls
- [ ] Multiple Okta org support (acquisitions, different regions)
- [ ] Mobile-optimized output rendering

## 5. Tech Stack

| Layer | Technology |
|-------|------------|
| Agent Runtime | OpenClaw |
| Auth | Okta OAuth 2.0 (PKCE) |
| API Calls | Company REST APIs |
| Output: Charts | Chart.js / D3.js |
| Output: Tables | HTML + CSS (no heavy deps) |
| Output: Files | SheetJS (Excel), plain CSV |
| Skill Framework | OpenClaw Skills (Node.js) |

## 6. Out of Scope (for now)

- Code generation / coding assistant
- Email / calendar integration (nice to have later)
- Multi-tenant SaaS deployment (self-hosted focus first)
- Non-REST APIs (GraphQL, gRPC)

## 7. Metrics for Success

| Metric | Target |
|--------|--------|
| Time to get an answer vs before | < 2 min vs 30+ min |
| % of employee questions answerable by Orbit | > 60% within Phase 2 |
| Support tickets about "where do I find X?" | 30% reduction after 3 months |

## 8. Team

- **Primary maintainer:** Lin Han (@linhan-ht)
- **Contributing:** Open to colleagues who want to help test and build skills

---

*Last updated: 2026-05-15*