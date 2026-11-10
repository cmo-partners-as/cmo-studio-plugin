# CMO Studio for Claude Code

Put the app you built with Claude Code online: hosting, a Postgres database, file storage and email from your own domain, in one place. Claude does the work through the CMO Studio MCP server; you approve the deletes. GDPR-ready, free to start, no card.

## Install

In Claude Code:

```text
/plugin marketplace add cmo-partners-as/cmo-studio-plugin
/plugin install cmo-studio@cmo-partners
```

Then run `/mcp`, choose `cmo-studio` and sign in (a free account is made on the way). You pick which projects and rights Claude gets.

Just ask: "put this app online with a database", "send booking confirmations from my domain", "move my Supabase database here".

## What it adds

- The `cmo-studio` MCP server (`https://studio.cmopartners.co/mcp`): projects and deploys from GitHub, logs and rollbacks, environment variables, domains, Postgres databases with a SQL console and imports, file buckets, transactional email, support requests.
- A skill that tells Claude when to use CMO Studio and how: never asking for secrets in the chat, and leaving deletes to you.

Not using Claude Code? Codex, Cursor and other agents connect to the same address: `https://studio.cmopartners.co/mcp`.

## Links

- [CMO Studio](https://studio.cmopartners.co) · [Pricing for AI agents](https://studio.cmopartners.co/pricing.md) · [Status](https://studio.cmopartners.co/status)
- Made by [CMO Partners AS](https://cmopartners.co), Oslo. Questions: office@cmopartners.co
