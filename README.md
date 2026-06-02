# All Good Things Bakery — Recipe Review (temporary)

A tiny **static** app for the client to review, edit, and approve the handwritten‑recipe
transcriptions. No backend, no logins, **no credentials** — just these files. Safe to host
publicly for a short window.

## Deploy to Netlify
- **Easiest (drag & drop):** Netlify → *Add new site → Deploy manually* → drag this whole folder in.
- **From a Git repo:** push these files to your private repo, *Import from Git* in Netlify,
  **Publish directory = repo root** (this folder), no build command. `netlify.toml` already sets it.

## How approvals come back to you
The client steps through each recipe — fixes the text, hits **✓ Approve** or **✎ Needs changes**,
adds optional notes. Progress auto‑saves in their browser. When done they click
**Finish & send back** → **Download results (.json)** (or **Copy summary text**) and send it to you.
Hand me that `recipe-approvals.json` and I'll fold the approved versions into the database.

## Add more recipes
Drop the photo into `images/` and add an entry to `recipes.json`
(`{ "id", "image", "text", "rotation" }`). The app picks it up automatically — scales to 15+.

## Contents
- `index.html` — the app (self‑contained, vanilla JS)
- `recipes.json` — recipe text + image references
- `images/` — the handwritten‑note photos

No secrets, no API keys, nothing from the main project.
