# Zoxron MCP

**Your AI agent deploys, migrates and upgrades self-hosted Odoo ERP, on a server you own.**

[![MCP Registry](https://img.shields.io/badge/MCP%20Registry-com.zoxron%2Fmcp-2FBF71)](https://registry.modelcontextprotocol.io/v0.1/servers?search=com.zoxron)
[![Price](https://img.shields.io/badge/price-free-2FBF71)](https://zoxron.com/connect)
[![Transport](https://img.shields.io/badge/transport-streamable--http%20%2B%20OAuth-444)](https://zoxron.com/connect/guide)

Zoxron MCP is a **hosted [Model Context Protocol](https://modelcontextprotocol.io) server** that lets an AI coding agent, **Claude** (Desktop / claude.ai / Claude Code) or **Codex**, provision and operate real Odoo installations for you: install, configure, migrate server to server, upgrade across major versions, run staging, backups and monitoring. **You keep the server, the data and the keys.**

It is the tool we use for our own Odoo work every day. It is **free**, and it stays free (see [Why it's free](#why-its-free)).

---

## What this repository is, and what it is not

This repository is the **connection documentation** for a hosted service, plus the `server.json` manifest that the MCP registries resolve. There is no server source here, and there will not be. Zoxron MCP is proprietary. Free to use is not the same as open source, and we would rather say so on the first screen than have you discover it three clicks in.

Three honest reasons the source is not published:

- **It would not run for you.** This is a hosted endpoint speaking streamable HTTP behind OAuth, not a package you install. Cloning it would give you a client for infrastructure you do not have.
- **The code is not where the value is.** What makes it work is the accumulated operational knowledge: which dependencies each Odoo version actually needs, what breaks between majors, which fields moved, the order that turns a migration into a boring afternoon. That is years of doing the work, and it is the product.
- **The free tier is paid for by the paid tier.** Provisioning and discovery are free and stay free. Publishing the server would end the thing that funds that promise.

What you can do without an account: read this page, read the [product page](https://zoxron.com/zoxron-mcp/), and see the registry entry. Everything operational needs a free account, for the reason in the next section.

---

## Who it's for

You'll get value if you:

- use an MCP-capable AI agent (Claude, Codex, or any MCP client), **and**
- run, or want to run, **self-hosted Odoo** on a VPS or server you control.

You do **not** need to be a sysadmin. The agent explains every step in plain language and never changes anything without your confirmation.

---

## How to connect

Create a **free account** at **<https://zoxron.com/connect>** first. That account is what issues your credentials and unlocks the documentation, so it comes before either method below.

### A. One-click connector (recommended: Claude Desktop, claude.ai)

Uses OAuth. One sign-in, no token to copy or store.

1. Sign in at **<https://zoxron.com/connect>**.
2. In Claude Desktop or claude.ai, go to **Settings, Connectors, Add custom connector**.
3. Enter the URL:
   ```
   https://zoxron.com/mcp
   ```
4. Complete the sign-in when prompted. The Zoxron tools become available in your next chat.

### B. Token / CLI (Claude Code, Codex, or when you want several separate keys)

Get a personal, scoped access token from **<https://zoxron.com/connect>** (valid 30 days), then wire it into your client.

**Claude Code:**
```bash
claude mcp add --transport http zoxron https://zoxron.com/mcp \
  --header "Authorization: Bearer YOUR_TOKEN"
```

**Any client via `mcp-remote` (e.g. Claude Desktop config), OAuth, no token:**
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

Per-client steps, kept current, are in the **[Guide](https://zoxron.com/connect/guide)** (sign-in required).

---

## What the account unlocks

The account is free and takes an email. Signing in gives you the tools **and** the two documents that matter, both of which live behind it:

**[Guide](https://zoxron.com/connect/guide)** walks the real workflows end to end, in order, with the decisions called out where you actually have to make them:

- which client to use, and the exact setup for each
- provisioning a new Odoo, step by step, from empty VPS to working login
- letting the agent create the server itself, at a cloud provider, on your account
- running several independent Odoo instances on one machine
- staging: a safe copy of production to test against
- migrating an existing Odoo to a new server, including the domain cutover
- upgrading Odoo across major versions, and Community to Enterprise
- monitoring and alerts, DNS and TLS, and what day-2 looks like after go-live
- where your passwords live, how SSH keys are handled, and the safety model
- troubleshooting and FAQ

**[Capabilities](https://zoxron.com/connect/capabilities)** is the full reference for what the agent can actually reach.

Both are in **English, Polish and German**.

---

## What you can ask it to do

Once connected, just talk to your agent:

- *"Deploy Odoo 18 Community on this VPS and point my domain at it."*
- *"Install Odoo 19 Enterprise (I have the .deb) with CRM, Sales and Accounting."*
- *"Migrate this running Odoo to a new, bigger server and cut the domain over."*
- *"Upgrade my Odoo to 19 and carry my custom and OCA modules across."*
- *"I need approvals on purchase orders. Is there an OCA module for that?"*
- *"Stand up a staging copy of production so I can test a change safely."*
- *"Put Odoo 16 and Odoo 19 on the same box, I need both during the transition."*
- *"Does `sale.order.line` still have `product_uom` in 19, or did it move?"*
- *"Deploy my custom module to staging, and promote it once I've checked it."*
- *"Set up nightly backups with a restore test, and alert me if anything breaks."*
- *"How is my server doing?"*

Four of those are worth calling out, because they are the ones people do not expect from a provisioning tool:

- **Find a module by describing the problem, not the name.** The Odoo Community Association publishes thousands of free modules, and their names rarely match what you would search for. Describe the behaviour you want; you get candidates, their licence, and whether they exist for your version, before anything is installed.
- **Write custom code against the real Odoo, not a guess.** The agent can check a field, a model, or what changed between two majors, against the actual version you run. This is what stops an afternoon of debugging a field that was renamed two releases ago.
- **Ship that code properly.** Deploy to staging, look at it, promote to production, roll back if it is wrong.
- **Run two different Odoo majors on one machine.** Odoo installs natively from its official `.deb` by default, as a plain system service. Containers are the other option you can pick, and they are what makes 16 and 19 coexist on one box, which native cannot do because those versions want different Python versions. Useful for exactly as long as a transition lasts.

---

## Built to be safe

- **Preview first.** Every changing step is shown to you as a dry run and needs your explicit confirmation before it runs. Nothing is touched until you say so.
- **You own everything.** It runs on *your* server, under *your* cloud account. You hold the keys. There is no lock-in, and your data stays in open formats you can take elsewhere.
- **Careful upgrades and migrations.** Backup first, one major version at a time, record counts checked against a baseline, and the original database kept as an immediate rollback.
- **Fenced destructive actions.** Anything destructive is restricted to fresh or throwaway targets.

New to it? The easiest way in is to learn it on a **throwaway server or a test database first**, and dry-run everything.

---

## Why it's free

This is the tool we use for our own Odoo work every day. We made it available and we keep it free for good. It does a lot, so learn it on a test target first. After a workflow, please send the short **anonymous** feedback. That is literally how it gets better, and it is why it stays free.

Free to use, not open source. The service is hosted and proprietary.

---

## Links

| | |
|---|---|
| **Start, create an account** | <https://zoxron.com/connect> |
| **Guide**, step by step, all clients | <https://zoxron.com/connect/guide> (sign-in) |
| **Capabilities**, full reference | <https://zoxron.com/connect/capabilities> (sign-in) |
| **Product page** | <https://zoxron.com/zoxron-mcp/> |
| **MCP registry entry** | [`com.zoxron/mcp`](https://registry.modelcontextprotocol.io/v0.1/servers?search=com.zoxron) |

The website and portal are available in **English, Polish and German**.

---

## About

Built by **Zoxron LLC** (Wyoming, USA): Odoo implementation, automation, and ERP to AI data migration.

*Odoo is a trademark of Odoo S.A. Zoxron LLC is an independent provider, not affiliated with, endorsed by, or sponsored by Odoo S.A. Product names and brands are the property of their respective owners.*
