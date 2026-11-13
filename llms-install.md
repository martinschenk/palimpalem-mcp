# Installing the Palimpalem MCP server

The server is remote (Streamable HTTP). Nothing to clone, build or run.

```json
{
  "mcpServers": {
    "palimpalem": {
      "type": "streamableHttp",
      "url": "https://palimpalem.com/mcp"
    }
  }
}
```

The first three tools need no account and no API key. The account tools ask for a
palimpalem sign-in (OAuth 2.1 with dynamic client registration); a code sent by
e-mail is enough, also for people without an account.

**Check that it works:** call `comprobar_dominio` with `{"name": "panaderiaferia.es"}`.
The answer says whether the name is free or taken (no prices).

**Build a draft:** call `crear_borrador_web` with
`{"description": "Bakery in Seville, Calle Feria 20, bread and cakes every morning, open Monday to Saturday", "language": "en"}`.
It takes 15 to 60 seconds and returns a link to a draft website, valid for 7 days.

No tool takes payments: `solicitar_dominio`, `solicitar_correo` and `solicitar_plus`
return a link to a page on palimpalem.com where the person sees the price and pays.
