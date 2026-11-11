# Palimpalem MCP server

Remote MCP server of [Palimpalem](https://palimpalem.com): it builds a free draft website for a small local business (restaurant, hairdresser, shop, clinic, tradesperson, association) and returns a link where the person can view it.

- **Endpoint:** `https://palimpalem.com/mcp` (Streamable HTTP, stateless)
- **Authentication:** none for the first three tools; OAuth 2.1 (PKCE, dynamic client registration) for the account tools. Sign-in by a code sent by e-mail, also without an account. Discovery: `https://palimpalem.com/.well-known/oauth-protected-resource/mcp`
- **Account-only endpoint:** `https://palimpalem.com/mcp/cuenta` (asks for sign-in when connecting; same tools)
- **Profile without purchase tools:** `https://palimpalem.com/mcp/openai` (for ChatGPT: same tools except the three payment-link tools)
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

Domain, DNS, e-mail and Plus (with sign-in):

- `ver_dns` (Show where a domain points: name servers, records of the domain and of www, mail servers; read only)
- `conectar_dominio_existente` (Connect a domain the person already owns: exactly two DNS steps at their provider, then a check. It never writes into DNS zones by itself; for a domain managed by palimpalem the owner gets a confirmation link by e-mail, and the change is made only after that click)
- `solicitar_dominio` (Payment link for a new domain; the domain owner is always the person or their business)
- `solicitar_correo` (Payment link for an e-mail package with the own domain; without a package it lists the packages)
- `solicitar_plus` (Payment link for the Plus service)

No tool takes payments, buys or registers anything: the payment-link tools return a link to a page on palimpalem.com where the person sees the price and pays (Stripe). The `/mcp/openai` profile leaves these three tools out. Access can be removed at any time in the palimpalem control centre (My data → Connected AI assistants).

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
- **ChatGPT (developer mode):** add a remote MCP server with the URL `https://palimpalem.com/mcp/openai`
- **Cursor, VS Code, Gemini, Mistral Le Chat, Perplexity, other clients:** add a remote MCP server with the URL `https://palimpalem.com/mcp`

## Examples

> "Make a website for my bakery in Seville: we bake bread and cakes every morning, Calle Feria 20, open Monday to Saturday."

> "Keep that draft as my website and change the main title to Fresh bread every morning."

> "I already have the domain panaderiaferia.es at another provider. Connect it to my website."

## Support and legal

- Support: martin@palimpalem.com
- Privacy: https://palimpalem.com/en-us/privacy
- Terms: https://palimpalem.com/en-us/terms
- Operator: Martin Schenk S.L., Madrid, Spain
