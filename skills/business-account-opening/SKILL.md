---
name: business-account-opening
description: >
  Open a Vivid Business account via the vivid-mcp remote MCP server.
  Collects legal entity data from the user (or extracts it from uploaded
  documents locally), then calls the build_onboarding_link tool to generate
  a pre-filled onboarding URL. No local install or credentials required.
version: 0.1.0

metadata:
  openclaw:
    emoji: "🏦"
    homepage: "https://github.com/vivid-money/vivid-mcp"
    requires:
      env: []
      bins: []
      config: []
---

# Business Account Opening

Open a Vivid Business account using the `vivid-mcp` remote MCP server.

## Integration

- **Server:** `https://api.prime.vivid.money/mcp` (remote, streamable HTTP)
- **Tool:** `build_onboarding_link` — accepts legal entity data, returns an onboarding URL
- **Auth:** none required — the endpoint is publicly accessible
- **Install:** nothing to install — the MCP server is hosted by Vivid; the client connects via the `.mcp.json` config in this repository

## Trigger

User wants to open a business account or start business onboarding.

## Flow

1. Ask for **legal entity type** (GmbH, UG, freelancer, etc.) if not provided.
2. Ask for **country** if not provided. Default: Germany.
3. Call MCP to get required fields and accepted document types.
4. If the user uploads a document, extract the fields **locally in the client** — the document itself is never sent to the MCP server. Summarize what was extracted; do not echo raw document contents.
5. Show the user a summary of all collected data and **ask for explicit confirmation** before proceeding.
6. Call `build_onboarding_link` with the confirmed data. The server returns an onboarding URL.
7. Present the URL to the user.

## Data handling

- **Documents stay local.** Uploaded files are parsed by the AI client. Only structured fields (company name, address, etc.) are sent to the MCP server.
- **No PII stored by the skill.** The skill does not persist any data. The MCP server creates an onboarding session;
- **No credentials in chat.** Never ask for or accept passwords, API keys, or bank account numbers.

## Rules

- Always confirm collected data with the user before calling `build_onboarding_link`.
- Never call the tool autonomously — require explicit user approval.
- Treat uploaded documents as sensitive — summarize only, don't echo contents.
- On error: ask for missing fields or suggest a different document.
