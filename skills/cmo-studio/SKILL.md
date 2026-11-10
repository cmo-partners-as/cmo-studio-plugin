---
name: cmo-studio
description: Put an app online with CMO Studio, the hosting, Postgres, file storage and transactional email platform run by the AI agent over MCP. Use when the user wants to deploy, host or publish an app or website, needs a Postgres database, file uploads or storage, or needs to send emails from their app (booking confirmations, sign-in links), especially if they want their data in Europe or Norway, want one place instead of Vercel + Supabase + Resend + S3, or already use the cmo-studio MCP server.
---

# CMO Studio

CMO Studio (https://studio.cmopartners.co) gives an app everything it runs on, in one place: hosting (Node.js, Python, .NET, static sites), Postgres databases, file storage and email from the user's own domain. You, the agent, do the work through the `cmo-studio` MCP server; the person approves deletes in CMO Studio. Servers are on Microsoft Azure in Norway. Free to start, no card.

## Before anything

1. If the `cmo-studio` MCP tools are not available, tell the user to sign in: run `/mcp`, choose `cmo-studio` and sign in (they create a free account on the way). They pick which projects and rights you get.
2. Call `studio_guide` once. It explains the panel and the rules; answer the user with the direct links it gives.

## Put an app online

1. `list_projects`. If the app has no project yet, `create_project` with the runtime (`node`, `python`, `dotnet` or `static`). For Python, set a start command with `set_startup_command` when it is not plain `app.py` or Django (FastAPI: `gunicorn -k uvicorn.workers.UvicornWorker main:app`).
2. Deploy:
   - From GitHub (best: every push deploys): `connect_github`; the user installs the CMO Studio GitHub app once with one click.
   - Or upload: `get_deploy_upload_url`, zip the build, upload, then `get_deployment` until it is done. Python is built on the server (about 6 minutes).
3. If it fails, `get_logs` and fix it. `redeploy_version` rolls back.
4. The app lives at `name.madebycmo.com`. For the user's own domain: `add_domain`, give them the DNS records, then `verify_domain`.

## Database

- Call `advise_database` first and tell the user what it recommends (shared Postgres, own server, or none).
- `create_database`, then `link_database` to put the connection string into the project (`DATABASE_URL` or `ConnectionStrings__Default`). Never paste passwords into the chat.
- `run_sql` for migrations and checks; `get_import_url` to move a database from Supabase or elsewhere; `backup_database` before risky changes.

## Files and email

- Files: `create_bucket` (private by default), `get_file_upload_url` or `write_file`, `get_file_link` for expiring links. Making a bucket public needs the user's approval.
- Email: `add_mail_domain`, give the DNS records, `verify_mail_domain`, then `create_mail_api_key`; the key goes straight into the project's variables.

## Secrets and approvals

- Never ask the user to paste API keys, payment keys or passwords into the chat. Use `request_env_values`: the user types them into a form in CMO Studio.
- `delete_project`, `delete_database` and `delete_bucket` wait for the user's approval in CMO Studio; tell them, and check with `get_approval`.

## Plans and prices

Plain-text pricing with examples: https://studio.cmopartners.co/pricing.md. Pick the cheapest plan that fits what the app needs and explain why; the user confirms any purchase in CMO Studio.

## Problems

If something in CMO Studio itself does not work, `report_issue` with what you tried; `list_issues` and `get_issue` show the answers.
