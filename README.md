# GitHub Tree Browser

A single-file, client-only explorer for browsing any **public GitHub repository** as a collapsible tree on **GitHub Pages**. Previews images inline, shows small text files, and gives one-click **raw**, **CDN**, and **GitHub** links.

🔗 **Live:** [michalaferber.github.io/github-tree-browser](https://michalaferber.github.io/github-tree-browser/)

> **No server required.** Uses the public GitHub Contents API; works unauthenticated, or with an optional Personal Access Token kept entirely in your browser.

## Features

- 🗂️ Collapsible directory tree (lazy-loads subfolders, remembers expanded state)
- 🔎 Live filter for the current folder (Esc clears)
- 🖼️ Inline image preview (PNG, JPG, GIF, WEBP, AVIF, SVG) + lightbox with keyboard nav
- 📄 Text preview for small files (≤ ~1 MB; md/txt/json/yml/csv/js/ts/css/html/xml/sh/py)
- 🧭 Breadcrumb navigation
- 🔗 Deep linking to a specific file or folder (`?path=...`)
  - **Safe fallback** when embedded/sandboxed: uses `#path=...` if the environment disallows `history.replaceState`
- 📋 One-click copy of **raw URL**, **jsDelivr CDN URL**, or raw bytes (image/text)
- 🌗 Light / Dark / System theme toggle (persisted)
- 🔑 Optional GitHub PAT (browser-only) to lift the rate limit from 60 → 5000 req/hr
- ⚙️ Switch owner / repo / branch from the header controls
- 📣 Open Graph + Twitter card meta tags for nicer link previews

## Default example

The hosted version opens with `MichalAFerber/resources` (the branding assets / wallpapers repo) loaded by default, so you have something concrete to click around in. Edit the **Owner / Repo / Branch** fields and click **Load** to point it anywhere.

## Use it as a hosted tool for your own repo

Easiest: just use the live URL with query parameters:

```
https://michalaferber.github.io/github-tree-browser/?owner=<USER>&repo=<REPO>&branch=<BRANCH>
```

## Self-host on your own GitHub Pages

1. Copy `index.html` (and optionally `favicon.ico`) to the root of any repo
2. Enable Pages on `main` / `/ (root)` in repo Settings → Pages
3. Open `https://<your-username>.github.io/<your-repo>/`

The defaults can be changed by editing the three `<input>` values near the top of `<body>`:

```html
<label>Owner <input id="owner" value="MichalAFerber" /></label>
<label>Repo <input id="repo" value="resources" /></label>
<label>Branch <input id="branch" value="main" /></label>
```

## Configuration

Header fields are editable at runtime:

- **Owner** — GitHub user/org
- **Repo** — repository name
- **Branch** — default `main`
- **Token** (optional GitHub PAT, browser-only)

## Authentication (optional)

Without a token: ~60 GitHub API requests/hour from your IP. Plenty for casual browsing.

With a fine-grained PAT (no scopes needed for public repos, just `public_repo` if you want to browse your own private repos): 5000 req/hr. The token is kept only in `localStorage` of your browser and never sent anywhere except `api.github.com` over HTTPS.

## Tech

- Vanilla HTML/CSS/JS, no build step, single file
- GitHub Contents API + raw.githubusercontent.com
- jsDelivr CDN for the "copy CDN URL" shortcut

## License

MIT — see [LICENSE](LICENSE).
