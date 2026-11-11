# Palimpalem MCP server

Remote MCP server of [Palimpalem](https://palimpalem.com): it builds a free draft website for a small local business (restaurant, hairdresser, shop, clinic, tradesperson, association) and returns a link where the person can view it.

- **Endpoint:** `https://palimpalem.com/mcp` (Streamable HTTP, stateless)
- **Authentication:** none for the first three tools; OAuth 2.1 (PKCE, dynamic client registration) for the account tools. Sign-in by a code sent by e-mail, also without an account. Discovery: `https://palimpalem.com/.well-known/oauth-protected-resource/mcp`
- **Account-only endpoint:** `https://palimpalem.com/mcp/cuenta` (asks for sign-in when connecting; same tools)
- **Languages of the websites:** Spanish, German, English

This repository only describes the server; the server itself runs at palimpalem.com.

## Tools

Without sign-in:

- `crear_borrador_web` (Build a website draft)
- `ver_borrador` (Look up a website draft, read only: name, pages, validity)
- `comprobar_dominio` (Check a domain name, read only: free or taken, no prices)

With palimpalem sign-in (OAuth, scopes `web:read`, `web:write`):

- `reclamar_borrador` (Save a draft as my website: creates a new free website in the account, never overwrites one)
- `listar_mis_webs` (List my websites, read only)
- `ver_mi_web` (Look at my website: status and outline of pages and texts, read only)
- `editar_web` (Change my website from a request in plain words; every change can be undone)
- `publicar_web` (Publish my website; changes nothing without `confirm=true`)

No tool takes payments or buys anything. Access can be removed at any time in the palimpalem control centre (My data → Connected AI assistants).

Details of the first tool:

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

## Examples

> "Make a website for my bakery in Seville: we bake bread and cakes every morning, Calle Feria 20, open Monday to Saturday."

> "Keep that draft as my website and change the main title to Fresh bread every morning."

## Support and legal

- Support: martin@palimpalem.com
- Privacy: https://palimpalem.com/en-us/privacy
- Terms: https://palimpalem.com/en-us/terms
- Operator: Martin Schenk S.L., Madrid, Spain
