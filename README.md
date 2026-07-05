# Atelier — Drawing Practice Timer

A timer for drawing exercises: instructions and matching prompts are built
right into each session plan. Runs entirely in the browser, no data
collection, no login. Add new exercise plans yourself as JSON — no coding
required.

Live demo once set up: `https://YOUR-GITHUB-NAME.github.io/atelier-timer/`

## 1. Create the GitHub repo

1. Go to [github.com/new](https://github.com/new) and create a new
   repository, e.g. named `atelier-timer`. Keep it **Public** — free GitHub
   Pages hosting requires a public repo (unless you're on a paid plan).
2. **Don't** let GitHub initialize a README/`.gitignore` — the files here
   replace that.

## 2. Upload the files

Easiest option, no command line needed:

1. In the empty repo, click **"uploading an existing file"**.
2. Drag in all files from this folder: `index.html`, `manifest.json`,
   `sw.js`, `icon-192.png`, `icon-512.png`.
3. Enter a commit message (e.g. "Initial commit") and click **Commit changes**.

Alternative using Git:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR-GITHUB-NAME/atelier-timer.git
git push -u origin main
```

## 3. Enable GitHub Pages

1. In the repo, go to **Settings → Pages**.
2. Under **Build and deployment → Source**, choose `Deploy from a branch`.
3. Branch: `main`, folder: `/ (root)` — click **Save**.
4. After about a minute, the app is live at
   `https://YOUR-GITHUB-NAME.github.io/atelier-timer/`.

## 4. Install it on your phone

1. Open the GitHub Pages URL in your phone's browser.
2. **iOS (Safari):** tap the Share icon → "Add to Home Screen".
   **Android (Chrome):** tap the menu (⋮) → "Install app" / "Add to Home screen".
3. The app then opens full-screen like a native app, and works offline
   (thanks to `sw.js`) once it has loaded at least once.

## Adding new sessions

There are two ways to add a session — both end up in the same place: the
**"+ New session"** button in the app.

### Option A — generate one with an AI

1. In the app, tap **🤖** to open the built-in template.
2. Copy it, paste it into an AI chat, and add your current training goal at
   the bottom (e.g. "loose gesture lines and Bridgman block-in").
3. The AI replies with a JSON object. Copy that JSON.
4. In the app, tap **+ New session**, paste the JSON into the text box, tap
   **Save**.

### Option B — write the JSON yourself

Each session is one JSON object with this shape:

```json
{
  "id": "unique-id-kebab-case",
  "titel": "Session title",
  "beschreibung": "One sentence: what skill this trains",
  "fokus": ["gesture", "perspective"],
  "schwierigkeit": "einsteiger | fortgeschritten | erfahren",
  "phasen": [
    {
      "name": "Phase name, e.g. Warm-up",
      "typ": "warmup | hauptblock | cooldown",
      "wiederholungen": 5,
      "dauer_sek_pro_wiederholung": 30,
      "anweisung": "Concrete instruction, max. 2 sentences.",
      "checkfrage": "A self-check question to ask while drawing.",
      "prompts": ["reference search term 1", "reference search term 2"]
    }
  ],
  "hinweise": "Optional: one overall rule for the whole session."
}
```

Notes:
- `phasen` needs at least one entry; 2–4 phases is typical
  (warmup → hauptblock → optional cooldown).
- `prompts` are short reference/search terms, not full sentences. If there
  are fewer prompts than repetitions, they repeat in a cycle.
- `id` must be unique. Reusing an existing session's `id` and saving will
  overwrite that session — this is also how editing works (tap the pencil
  icon on a session card, which pre-fills its current JSON for editing).
- Field names stay in German (`titel`, `beschreibung`, `phasen`, etc.) since
  that's the app's internal schema — only the displayed text needs to be in
  whatever language you want.

Everything you add is stored locally on your device (`localStorage` when
self-hosted) — nothing is sent to a server.

## Pushing updates

Just re-commit and push changes to `index.html`, `manifest.json`, etc. (or
edit directly in the repo on GitHub and commit) — GitHub Pages redeploys
automatically.

## Custom domain (optional)

Under **Settings → Pages → Custom domain** you can set up your own domain.
Not necessary for personal use.

## Files in this repo

| File | Purpose |
|---|---|
| `index.html` | The full app (timer, library, import) |
| `manifest.json` | PWA metadata (name, icon, full-screen launch) |
| `sw.js` | Service worker for offline caching |
| `icon-192.png`, `icon-512.png` | App icons for the home screen |
