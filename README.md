# Orbit

> Your AI work companion — asks questions, calls APIs, delivers insights.

Orbit is an enterprise AI agent built on OpenClaw, tailored to your company's systems and workflows. Instead of a generic chatbot, it understands *who you are*, *what you do*, and connects to the APIs that matter to your job — returning formatted, useful outputs right where you work.

## What can it do?

- **Ask in plain language** — "Show me open VOU tickets about search performance"
- **Get answers, not links** — Orbit queries Jira, AWS, monitoring, and more — then formats the result for you
- **Output adapts to the data** — Tables, charts, dashboards, downloadable CSV/Excel — Orbit picks the right format
- **Available everywhere** — WeChat, Zoom, Web, or any OpenClaw-supported channel

## How it works

```
You → Natural language question
  ↓
OpenClaw routes to Orbit agent
  ↓
Okta Auth (your token, your permissions)
  ↓
API Router (calls the right backend)
  ↓
Output Renderer (formats result as Dashboard / CSV / Excel)
  ↓
You receive a clear, actionable answer
```

## Status

🟡 **Phase 0** — Foundation building. See [PLANNING.md](./PLANNING.md) for the full roadmap.

## Quick Links

- [Project Plan](./PLANNING.md)
- [GitHub Issues](https://github.com/linhan-ht/orbit/issues) — bug reports, feature requests