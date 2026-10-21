# Google Workspace setup pages

A self-contained HTML page that walks a client's Google Workspace admin through connecting their Workspace to a CRM that Big Spoon builds. No build step, no dependencies, no data sent anywhere.

`docs/index.html` is the page, published with GitHub Pages.

**This repo is public, so it holds only the client page.** The developer runbook (`runbook.html`) that pairs with it is internal and is kept out of this repo on purpose.

## How it works

The client page reads three link parameters and rebuilds its steps from them:

```
https://<pages-url>/?domain=acme.com&features=send,calendar,drive&sa=1
```

- `domain`: the client's Workspace domain. Every example on the page uses it.
- `features`: any of `signin`, `send`, `history`, `inbox`, `calendar`, `availability`, `meet`, `drive`, `savedrive`, `contacts`, `sheets`.
- `sa=1`: Drive import uses the service-account option instead of the company account (`crm@`).

The client can also type the domain and tick features themselves. Their ticks and progress stay in their own browser. "Email Big Spoon" opens a pre-filled email to tech@bigspoon.ai; nothing else leaves the page.

The internal runbook reads the same parameters, and its **Copy client link** button builds these links.

## Publishing on GitHub Pages

1. Push this repo to GitHub.
2. Repo **Settings → Pages → Build and deployment**: Source **Deploy from a branch**, branch `main`, folder **`/docs`**. Save.
3. After a minute the page is live at the URL GitHub shows there.
4. Put that URL in `CLIENT_PAGE_URL` near the top of the script in the internal runbook.

A GitHub Pages site is always public. The page holds nothing secret: Big Spoon's customer ID and contact address are meant for clients to see.

## Editing

`docs/index.html` is the source; edit it directly.

- **Steps (client page):** the `STEPS` list in the script controls order, minutes, and when a step appears (`only` / `when`). Each step's body is a `<template id="tpl-<step id>">` above the script. Step cross-references are `<span class="ref" data-ref="<step id>">` and fill in automatically.
- **Features:** the `FEATURES` list in the script. The internal runbook has a matching list (`F`) and a copy of the step order (`CS`); change them together.
- **Big Spoon's customer ID** (`C01lltan0`) and account (`tech@bigspoon.ai`) also appear in the runbook.

The screens on the client page are drawn illustrations, not screenshots of Google's console.
