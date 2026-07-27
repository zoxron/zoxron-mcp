# Zoxron MCP

**Your AI agent deploys, migrates & upgrades self-hosted Odoo ERP — on a server you own.**

[![MCP Registry](https://img.shields.io/badge/MCP%20Registry-com.zoxron%2Fmcp-2FBF71)](https://registry.modelcontextprotocol.io/v0.1/servers?search=com.zoxron)
[![Price](https://img.shields.io/badge/price-free-2FBF71)](https://zoxron.com/connect)
[![Transport](https://img.shields.io/badge/transport-streamable--http%20%2B%20OAuth-444)](https://zoxron.com/connect/guide)

Zoxron MCP is a **hosted [Model Context Protocol](https://modelcontextprotocol.io) server** that lets an AI coding agent — **Claude** (Desktop / claude.ai / Claude Code) or **Codex** — provision and operate real Odoo installations for you: install, configure, migrate server‑to‑server, upgrade across major versions, run staging, backups and monitoring. **You keep the server, the data and the keys.**

It is the tool we use for our own Odoo work every day. It is **free** — and it stays free (see [Why it's free](#why-its-free)).

> This repository is **connection documentation** for the hosted service. Zoxron MCP is a proprietary, hosted service — it is **not** open‑source, and no server source is published here. Free to use ≠ open source.

---

## Who it's for

You'll get value if you:

- use an MCP‑capable AI agent (Claude, Codex, or any MCP client), **and**
- run — or want to run — **self‑hosted Odoo** on a VPS/server you control.

You do **not** need to be a sysadmin. The agent explains every step in plain language and never changes anything without your confirmation.

---

## How to connect

There are two ways in. Pick one.

### A. One‑click connector (recommended — Claude Desktop / claude.ai)

Uses OAuth. One sign‑in, no token to copy or store.

1. First, create a free account at **<https://zoxron.com/connect>** and sign in.
2. In Claude Desktop or claude.ai → **Settings → Connectors → Add custom connector**.
3. Enter the URL:
   ```
   https://zoxron.com/mcp
   ```
4. Complete the sign‑in when prompted. The Zoxron tools become available in your next chat.

### B. Token / CLI (Claude Code, Codex, or when you want several separate keys)

Get a personal, scoped access token from **<https://zoxron.com/connect>** (valid 30 days), then wire it into your client.

**Claude Code:**
```bash
claude mcp add --transport http zoxron https://zoxron.com/mcp \
  --header "Authorization: Bearer YOUR_TOKEN"
```

**Any client via `mcp-remote` (e.g. Claude Desktop config) — OAuth, no token:**
```json
{
  "mcpServers": {
    "zoxron": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://zoxron.com/mcp"]
    }
  }
}
```

Full, up‑to‑date steps for every client are in the **[Guide](https://zoxron.com/connect/guide)**.

---

## What you can ask it to do

Once connected, just talk to your agent. For example:

- *"Deploy Odoo 18 Community on this VPS and point my domain at it."*
- *"Install Odoo 19 Enterprise (I have the .deb) with CRM, Sales and Accounting."*
- *"Migrate this running Odoo to a new, bigger server and cut the domain over."*
- *"Upgrade my Odoo to 19 and carry my custom / OCA modules across."*
- *"Stand up a staging copy of production so I can test a change safely."*
- *"Set up nightly backups with a restore test, and alert me if anything breaks."*
- *"How is my server doing?"*

The agent works through the [full tool set](https://zoxron.com/connect/capabilities) — provisioning, TLS/DNS, multi‑instance hosting, cloud provisioning, code deploy (staging → prod), migration, upgrades, backups and monitoring.

---

## Built to be safe

- **Preview‑first.** Every changing step is shown to you as a dry‑run and needs your explicit confirmation before it runs. Nothing is touched until you say so.
- **You own everything.** It runs on *your* server, under *your* cloud account. You hold the keys; there's no lock‑in.
- **Careful upgrades/migrations.** Backup‑first, one major version at a time, record counts checked against a baseline, and the original database kept as an immediate rollback.
- **Fenced destructive actions.** Anything destructive is restricted to fresh / throwaway targets.

New to it? The easiest way in is to learn it on a **throwaway server or a test database first** — dry‑run everything.

---

## Why it's free

This is the tool we use for our own Odoo work every day; we made it available and we keep it free for good. It does a lot, so learn it on a test target first. After a workflow, please send the short **anonymous** feedback — that is literally how it gets better, and it is why it stays free.

Free to use — not open source. The service is hosted and proprietary.

---

## Links

- **Start / create an account:** <https://zoxron.com/connect>
- **Guide (step‑by‑step, all clients):** <https://zoxron.com/connect/guide>
- **Capabilities:** <https://zoxron.com/connect/capabilities>
- **Product page:** <https://zoxron.com/zoxron-mcp/>
- **MCP registry entry:** [`com.zoxron/mcp`](https://registry.modelcontextprotocol.io/v0.1/servers?search=com.zoxron)

The website and portal are available in **English, Polish and German**.

---

## About

Built by **Zoxron LLC** (Wyoming, USA) — Odoo implementation, automation and ERP→AI data migration.

*Odoo is a trademark of Odoo S.A. Zoxron LLC is an independent provider, not affiliated with, endorsed by, or sponsored by Odoo S.A. Product names and brands are the property of their respective owners.*
