# Facebook Page Messenger AI Agent (n8n)

An n8n workflow that connects a Facebook Page to an AI agent, so incoming Messenger messages get automatic, context-aware replies.

**Workflow name:** `1. Facebook page Scorp messenger Agent virson_2.5.0`
**Version:** 2.5.0
**Tags:** Facebook Automation, ReadyToUse, _Blueprint

## Overview

The workflow listens for messages sent to your Facebook Page, passes them to an AI agent, and sends the generated reply back to the user through the Messenger Send API.

```
Messenger message -> n8n Webhook -> AI Agent -> Reply via Messenger Send API
```

## Features

- Automatic replies to Facebook Page Messenger conversations
- AI agent handling for natural-language responses
- Ready-to-use blueprint you can duplicate for other pages
- Separate testing workflow (`2. ... Testing System Version_0.0.0`) for safe experiments

## Requirements

- An [n8n](https://n8n.io) instance (self-hosted or cloud) reachable over public HTTPS
- A Facebook Page and a Meta Developer app with the Messenger product enabled
- A Page Access Token with messaging permissions
- An API key for the AI model used by the agent node
- *(Optional)* A database or data table for conversation memory

## Setup

1. **Import the workflow**
   In n8n, go to Workflows -> Import from File and select the exported JSON.

2. **Create credentials**
   - Facebook / Messenger: Page Access Token
   - AI model provider: API key
   - Any storage or memory credentials the workflow uses

3. **Configure the Meta app**
   - Add the Messenger product to your app.
   - Set the webhook callback URL to your n8n webhook URL.
   - Set a verify token and use the same value in the workflow.
   - Subscribe the webhook to `messages` and `messaging_postbacks` for your Page.

4. **Customize the agent**
   Edit the agent's system prompt to define your business, tone and rules.

5. **Test, then activate**
   Send a test message to your Page, check the execution log in n8n, then switch the workflow to **Active**.

## Configuration

| Setting | Where | Notes |
|---|---|---|
| Page Access Token | n8n credentials | Never commit this to Git |
| Verify token | Webhook node + Meta app | Must match on both sides |
| System prompt | AI Agent node | Controls the bot's behavior |
| Webhook URL | Meta app settings | Use the production URL, not the test URL |

## Security

- Do not commit exported workflow JSON containing credentials or tokens.
- Rotate the Page Access Token if it is ever exposed.
- Restrict access to your n8n instance.

## Troubleshooting

- **No replies:** confirm the workflow is active and the webhook is subscribed to the Page.
- **Webhook verification fails:** check that the verify token matches in Meta and n8n.
- **Token errors:** regenerate the Page Access Token and update the n8n credential.
- **Messages not arriving:** make sure the app is in Live mode, or that you are testing with an app role account.

## Project Structure

```
.
├── README.md
└── workflows/
    └── facebook-messenger-agent-v2.5.0.json
```

## License

Add your license here (for example, MIT).
