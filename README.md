# n8n Automation Workflows

A collection of automation workflows I've built with [n8n](https://n8n.io), an open-source workflow automation tool. Each workflow connects apps and services to automate repetitive tasks — no manual work required.

## What's here

| Workflow | What it does | Apps used |
|----------|-------------|-----------|
| [Gmail AI Triage](workflows/gmail-ai-triage.json) | AI agent that classifies, labels, and sorts incoming email automatically — with safe-by-default rules and error handling | Gmail, OpenAI |
| [Stripe → Google Sheets](workflows/stripe-to-sheets.json) | Logs every new Stripe payment into a spreadsheet automatically | Stripe, Google Sheets |
| _(more coming as I build them)_ | | |

## How to use these workflows

1. Download the `.json` file for the workflow you want.
2. In n8n, go to **Workflows → Import from File**.
3. Select the downloaded file.
4. Add your own credentials for each connected app.
5. Activate the workflow.

> **Note:** No credentials or API keys are included in any workflow file here. You'll add your own after importing.

## About me

I build automations that save businesses time by connecting their tools and removing manual data entry. Available for freelance and remote automation work.

- **Email:** tatul.ghazaryan.ai@gmail.com
- **LinkedIn:** https://www.linkedin.com/in/ai-tatul/

## Skills

- n8n workflow design (triggers, data transformation, error handling)
- AI agents and LLM integration (OpenAI, structured output parsing)
- API integrations (REST, webhooks, OAuth)
- Connecting CRMs, spreadsheets, payment systems, and messaging apps
