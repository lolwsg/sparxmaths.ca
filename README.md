# The Cartridge Index

A static, searchable index of ~865 games — browser/HTML5 titles plus emulated
N64, GBA, NDS, NES, SNES, Genesis, Jaguar, Lynx, and Atari 2600 games — built
as a single-page site you can host for free on GitHub Pages.

## What's in this repo

- `index.html` — the whole site (search bar, platform filter chips, and a
  grid of "cartridge" cards for every title).
- `data.js` — the full game list as structured data (name + filename +
  platform) that `index.html` reads to build the page.
- `games/` — **empty on purpose.** This index only lists filenames; it
  doesn't include the actual game files. See below.

## Important: this is an index, not the games themselves

Each card links to `games/<filename>.html` (e.g. `games/clsupermario64.html`).
For those links to actually load anything, you need to put the matching
`.html` game files into a `games/` folder at the root of this repo, using
the exact filenames shown on each card. Without that, the site will look and
search correctly, but clicking a cartridge will 404.

If you don't have the original files, `data.js` is still useful on its own
as a clean, structured list of titles you can point at whatever hosting
you do have for the actual game files — just change the `href` build logic
near the bottom of `index.html` (search for `'games/' + g.file`).

## Deploying to GitHub Pages

1. Create a new GitHub repository and push these files to it (including
   your `games/` folder once it's populated).
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to `Deploy from a branch`,
   pick your default branch (e.g. `main`) and the `/ (root)` folder.
4. Save. GitHub will give you a URL like
   `https://<your-username>.github.io/<repo-name>/` within a minute or two.

## Editing the game list

`data.js` is plain JSON assigned to a `GAME_DATA` constant:

```js
const GAME_DATA = {
  "web": [ { "name": "...", "file": "....html" }, ... ],
  "consoles": [
    { "id": "N64", "label": "Nintendo 64", "games": [ ... ] },
    ...
  ]
};
```

Add, remove, or rename entries directly in this file — the page re-renders
from it on load, so no other changes are needed. If you add a brand-new
platform, it will automatically show up as its own filter chip and section.

## Local preview

No build step — just open `index.html` in a browser, or serve the folder
with anything static, e.g.:

```bash
python3 -m http.server 8000
```

then visit `http://localhost:8000`.
