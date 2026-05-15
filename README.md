# Empyr

> An AI agent that knows your work, calls your APIs, and delivers what you need.

## What is Empyr?

Empyr is an enterprise AI agent built on OpenClaw, designed for internal employee use. Instead of a generic chatbot, it's tailored to your company's systems, APIs, and workflows — enabling anyone to get answers, pull reports, and query data through natural language.

## Core Features

### 🔐 Enterprise Auth
- **Okta OAuth** integration — employees authenticate once, agent acts on their behalf
- Token management handled securely via OpenClaw credential system
- No additional login required after initial Okta connection

### 📡 API Integration Layer
- Agent understands user intent and routes requests to the right backend API
- Works with any REST API (Jira, internal services, databases)
- Returns structured data in JSON

### 📊 Output Generation
- **HTML Dashboard** — interactive charts and KPIs
- **CSV / Excel** — downloadable reports
- Output format determined by data type and user context

### 💬 Multi-Channel Access
- Works via WeChat, Zoom, Web, or any OpenClaw-supported channel
- Remembers conversation context across sessions
- Shares outputs natively in the channel where you ask

## Architecture

```
Employee (any channel)
       ↓
  OpenClaw Agent (Empyr brain)
       ↓
  Okta Token Manager (credential helper)
       ↓
  Company Backend APIs
       ↓
  Response Formatter → Dashboard / CSV / Excel
```

## Quick Start

> Coming soon

## Use Cases

- **"How many VOU tickets mention slow search?"** → Jira query → Dashboard
- **"Show me this month's infrastructure costs by team"** → AWS/EKS API → Interactive CSV
- **"What's our deployment process for production?"** → Knowledge base → Formatted answer
- **"Any active alerts firing right now?"** → Monitoring API → Instant status

## Tech Stack

- **OpenClaw** — agent runtime and multi-channel gateway
- **Okta** — enterprise identity provider
- **Custom skill plugins** — Okta auth helper, API router, dashboard renderer

## Status

🟡 Early development — foundation being built