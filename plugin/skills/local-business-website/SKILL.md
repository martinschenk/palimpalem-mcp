---
name: local-business-website
description: Use when someone wants a website for a small local business (restaurant, shop, hairdresser, clinic, tradesperson, association), wants to rebuild an old business website, or wants to change, translate, publish or host such a website with its own domain and e-mail.
---

# A website for a local business

Palimpalem builds the website, keeps it online and lets the owner change it by chatting.

1. **New website:** call `crear_borrador_web` with a `description` of the business (what,
   where, offer, contact) or the address of its `current_website`, and the `language`
   (es, de, en). It takes 15 to 60 seconds and returns a link to a draft, valid for 7 days.
   Give the person that link. No account is needed to look at it.
2. **Keep and change it:** with palimpalem sign-in (a code by e-mail is enough),
   `reclamar_borrador` saves the draft as the person's website. Then `ver_mi_web` shows
   pages and element ids, `editar_web` changes texts, pages or photos from a request in
   plain words, `idiomas_web` adds languages, `versiones_web` brings back an earlier state.
   Every change can be undone.
3. **Publish:** `publicar_web` only after the person has said yes (`confirm=true`).
4. **Domain and e-mail:** `comprobar_dominio` checks a name, `conectar_dominio_existente`
   connects a domain the person already owns (two DNS steps at their provider).
   `solicitar_dominio`, `solicitar_correo` and `solicitar_plus` return a payment link on
   palimpalem.com; the person sees the price and pays there. No tool charges anything.

The domain is always registered to the person or their business, never to palimpalem.
