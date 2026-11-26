<div align="center">

# Vivid MCP

<a href="https://vivid.money/en-de/business/api/" target="_blank">
  <img src="assets/logo.png" alt="Vivid" width="48">
</a>

### Ask your AI assistant about your Vivid Business account

Connect Claude, ChatGPT, Codex or VS Code to Vivid.<br>
Sign in once, then ask about your accounts, cards and transactions. Read-only.

<br>

[![Claude](https://img.shields.io/badge/Claude-8B5CF6?style=for-the-badge&logoColor=white)](#claude)
[![ChatGPT](https://img.shields.io/badge/ChatGPT-10A37F?style=for-the-badge&logo=openai&logoColor=white)](#chatgpt)
[![Codex](https://img.shields.io/badge/Codex-000000?style=for-the-badge&logo=openai&logoColor=white)](#codex)
[![VS Code](https://img.shields.io/badge/VS_Code-007ACC?style=for-the-badge&logoColor=white)](#vs-code)
[![MCP](https://img.shields.io/badge/MCP_Compatible-0969DA?style=for-the-badge)](https://modelcontextprotocol.io)

<br>

[**Connect**](#connect) &nbsp;&middot;&nbsp; [**Tools**](#tools) &nbsp;&middot;&nbsp; [**Security**](#security-and-data) &nbsp;&middot;&nbsp; [**Remove access**](#remove-access)

</div>

---

## What it does

Vivid MCP is a remote [Model Context Protocol](https://modelcontextprotocol.io) server for Vivid Business. After you sign in and give access, your AI assistant can read data of the company you choose:

- accounts with their balances and bank details
- cards with their limits and what has been spent against them
- transactions of the last 90 days

Example questions:

- "What is the balance on my EUR account?"
- "List the card payments from last week."
- "How much is left on the limit of my team's cards?"

Vivid MCP is read-only. The assistant cannot send money, issue or change cards, or edit anything in your account.

> **MCP server URL:** `https://api.prime.vivid.money/mcp`

## Supported clients

| Client | |
|:--|:--|
| Claude (web, Desktop, mobile, Claude Code) | Supported |
| ChatGPT | Supported |
| Codex | Supported |
| VS Code | Supported |

Your client signs in with OAuth. Vivid accepts sign-in only from a fixed list of AI apps, and we test and support the four above.

## Before you connect

- You need a Vivid Business account on a plan that includes API access. API access is included in paid plans; on a free plan, the sign-in page offers an upgrade.
- You need the **Manage API tokens** permission in your company's team settings. Owners have it by default; a custom role can be given it.
- One connection covers one company. For a second company, connect again and pick that company.

## Connect

### Claude

1. Open [claude.ai/settings/connectors](https://claude.ai/settings/connectors).
2. Choose **Add custom connector**.
3. Enter `https://api.prime.vivid.money/mcp` and save.
4. Choose **Connect** and sign in to Vivid in the browser window.
5. Pick your company and give access.

Claude Code:

```
claude mcp add --transport http vivid https://api.prime.vivid.money/mcp
```

Then run `/mcp` in Claude Code, choose **vivid** and sign in.

### ChatGPT

1. In ChatGPT, open **Settings → Apps**. Under **Advanced settings**, turn on **Developer mode** (your ChatGPT plan must allow custom apps).
2. Choose **Create app**.
3. Enter `https://api.prime.vivid.money/mcp` and set authentication to **OAuth**.
4. Save, choose **Connect**, sign in to Vivid and give access.

### Codex

```
codex mcp add vivid --url https://api.prime.vivid.money/mcp
codex mcp login vivid
```

Sign in to Vivid in the browser window, pick your company and give access.

### VS Code

Add the server to `.vscode/mcp.json` in your workspace, or to your user `mcp.json`:

```json
{
  "servers": {
    "vivid": {
      "type": "http",
      "url": "https://api.prime.vivid.money/mcp"
    }
  }
}
```

Start the server from the editor. VS Code opens a browser window to sign in. Pick your company and give access.

## Sign-in and access

1. Your assistant calls the server. Without a sign-in, Vivid answers `401` and the client opens a browser window. There is no API key and no anonymous mode.
2. You sign in to Vivid Business.
3. On the Vivid page you see which AI app asks for access, pick the company and choose the data it can read: accounts, transactions, cards.
4. You give access or deny it.
5. The assistant sees only the tools for the data you chose.

The page shows the date your access ends. Access also ends when it is not used for a while. After that, the assistant asks you to sign in again.

## Tools

| Tool | What it returns | Data group |
|:--|:--|:--|
| `list_accounts` | The company's payment accounts with balances and bank details | accounts |
| `get_account` | One account by its ID | accounts |
| `list_cards` | The company's cards you can see, with limits and spend | cards |
| `get_card` | One card by its ID, with limits and spend | cards |
| `list_transactions` | Transactions of the last 90 days on the accounts you can see, newest first | transactions |
| `get_transaction` | One transaction of the last 90 days by its ID | transactions |

All six tools are read-only. The assistant sees exactly what you see in the Vivid app, and no more. If you did not choose a data group, its tools are not listed.

## Security and data

- **Read-only.** No tool moves money or changes data.
- **No card numbers.** The server never returns the full card number or the CVV.
- **Short-lived tokens.** Access tokens are short-lived, and each refresh issues a new refresh token.
- **No API keys on MCP.** Vivid API keys do not work on `/mcp`. For your own software, use the [Vivid Business API](https://api.prime.vivid.money/sme-integration/docs/).
- **Logged.** Vivid logs every request made through MCP.
- **Your AI provider.** Data your assistant reads is processed by that AI provider under its own terms. Check the provider's privacy settings before you connect a company account.

## Remove access

In the Vivid web app, open **API** from **All services** or your profile menu. Filter by **AI apps**, open the app and choose **Remove access**. The assistant stops working with its next request.

Access also ends by itself if the person who gave it loses the **Manage API tokens** permission or leaves the company, if the company is no longer active, or if its plan no longer includes API access.

## Troubleshooting

- **Sign-in is refused.** Check that your user has the **Manage API tokens** permission and that your plan includes API access.
- **Tools are missing.** You did not choose that data group. Remove access and connect again.
- **Old setup stopped working.** Earlier versions of this server worked without sign-in and helped open an account. They now answer `401`. Connect again with the steps above.

## Open an account

Opening an account from the AI chat is no longer part of Vivid MCP. Open a Vivid Business account at [vivid.money/en-de/business](https://vivid.money/en-de/business/).

## Support

Questions or problems: the [Vivid Business help centre](https://help-business.vivid.money/en/) or [support@vivid.money](mailto:support@vivid.money). Report problems with this repository as GitHub issues.

## More

- Business API and MCP: [vivid.money/en-de/business/api](https://vivid.money/en-de/business/api/)
- Business API docs: [api.prime.vivid.money/sme-integration/docs](https://api.prime.vivid.money/sme-integration/docs/)
- About MCP: [modelcontextprotocol.io](https://modelcontextprotocol.io)

## Contributing and license

See [CONTRIBUTING.md](CONTRIBUTING.md). Licensed under [MIT](LICENSE).
