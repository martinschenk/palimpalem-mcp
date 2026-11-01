# Palimpalem MCP server

Remote MCP server of [Palimpalem](https://palimpalem.com): it builds a free draft website for a small local business (restaurant, hairdresser, shop, clinic, tradesperson, association) and returns a link where the person can view it.

- **Endpoint:** `https://palimpalem.com/mcp` (Streamable HTTP, stateless)
- **Authentication:** none
- **Languages of the websites:** Spanish, German, English

This repository only describes the server; the server itself runs at palimpalem.com.

## Tool

`crear_borrador_web` (Build a website draft)

| Argument | Type | Description |
|---|---|---|
| `description` | string | What the business does, where it is, what it offers, contact details. At least one full sentence. |
| `current_website` | string | Address of the current website; its texts and photos are reused. |
| `language` | `es` \| `de` \| `en` | Language of the website (default `es`). |

Give `description` or `current_website`. Building takes 15 to 60 seconds. The result is a link to the draft, valid for 7 days. No account is needed to build or view it; on the draft page the person can keep the website and later change it by chatting. The tool does not take payments.

## Connect in your assistant

- **Claude (claude.ai, Desktop):** Settings → Connectors → Add custom connector → URL `https://palimpalem.com/mcp`
- **Claude Code:** `claude mcp add --transport http palimpalem https://palimpalem.com/mcp`
- **ChatGPT (developer mode), Cursor, VS Code, other clients:** add a remote MCP server with the URL `https://palimpalem.com/mcp`

## Example

> "Make a website for my bakery in Seville: we bake bread and cakes every morning, Calle Feria 20, open Monday to Saturday."

## Support and legal

- Support: martin@palimpalem.com
- Privacy: https://palimpalem.com/en-us/privacy
- Terms: https://palimpalem.com/en-us/terms
- Operator: Martin Schenk S.L., Madrid, Spain
