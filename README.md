# All Good Things Bakery — client-facing site (`agt_foams`)

This **public** repo is the client-facing static site, served at
**https://tomenglish.github.io/agt_foams/** (GitHub Pages — auto-deploys on every push to `main`).
It hosts two different things:

1. **Recipe review** (public) — a tiny static app for the client to review, edit, and approve
   the handwritten-recipe transcriptions.
2. **Protected deliverables** (encrypted) — the throughput **dashboard** and the Tier 1–3
   **assessments**, which contain **financial information** and are therefore **StatiCrypt-
   encrypted at rest** and unlocked with a passphrase shared with the client **privately**.

> ⚠️ **This repo is PUBLIC and now carries (encrypted) client financials.** Treat it accordingly:
> - **Never commit** the StatiCrypt passphrase, the plaintext deliverable masters (these live in
>   the main project's `client_deliverables/`, not here), or any credential.
> - The encrypted pages are **world-downloadable** — their only protection is the passphrase, so
>   keep it strong and out of the repo. For anything more sensitive than these encrypted pages,
>   use a **private repo or a private delivery channel** instead.

## Pages
| File | Audience | Protection |
|---|---|---|
| `index.html` | client | 🌐 public — the recipe-review app |
| `discovery.html` | client | 🌐 public — owner questionnaire (questions only, no financial figures) |
| `dashboard.html` | client | 🔒 StatiCrypt — throughput analytics (financial) |
| `assessments.html` | client | 🔒 StatiCrypt — Tier 1–3 written assessments (financial) |
| `recipes.json`, `images/` | — | 🌐 public — recipe text + photos used by the app |

## Deploy / refresh
GitHub Pages serves the repo root on every push to `main` (no build step; the `netlify.toml`
here is a leftover from an earlier Netlify setup and is unused). **To publish updated
deliverables:** re-encrypt the current `client_deliverables/{dashboard,assessments}.html`
masters with StatiCrypt using the shared passphrase, copy the encrypted output over the files
here, then commit & push.

## Recipe-review workflow
The client steps through each recipe — fixes the text, hits **✓ Approve** or **✎ Needs changes**,
adds optional notes. Progress auto-saves in their browser. When done: **Finish & send back** →
**Download results (.json)** (or **Copy summary text**) and send it back. Hand that
`recipe-approvals.json` over and the approved versions fold into the database. Add recipes by
dropping a photo in `images/` and an entry in `recipes.json` (`{ "id", "image", "text", "rotation" }`);
the app scales to 15+ automatically.
