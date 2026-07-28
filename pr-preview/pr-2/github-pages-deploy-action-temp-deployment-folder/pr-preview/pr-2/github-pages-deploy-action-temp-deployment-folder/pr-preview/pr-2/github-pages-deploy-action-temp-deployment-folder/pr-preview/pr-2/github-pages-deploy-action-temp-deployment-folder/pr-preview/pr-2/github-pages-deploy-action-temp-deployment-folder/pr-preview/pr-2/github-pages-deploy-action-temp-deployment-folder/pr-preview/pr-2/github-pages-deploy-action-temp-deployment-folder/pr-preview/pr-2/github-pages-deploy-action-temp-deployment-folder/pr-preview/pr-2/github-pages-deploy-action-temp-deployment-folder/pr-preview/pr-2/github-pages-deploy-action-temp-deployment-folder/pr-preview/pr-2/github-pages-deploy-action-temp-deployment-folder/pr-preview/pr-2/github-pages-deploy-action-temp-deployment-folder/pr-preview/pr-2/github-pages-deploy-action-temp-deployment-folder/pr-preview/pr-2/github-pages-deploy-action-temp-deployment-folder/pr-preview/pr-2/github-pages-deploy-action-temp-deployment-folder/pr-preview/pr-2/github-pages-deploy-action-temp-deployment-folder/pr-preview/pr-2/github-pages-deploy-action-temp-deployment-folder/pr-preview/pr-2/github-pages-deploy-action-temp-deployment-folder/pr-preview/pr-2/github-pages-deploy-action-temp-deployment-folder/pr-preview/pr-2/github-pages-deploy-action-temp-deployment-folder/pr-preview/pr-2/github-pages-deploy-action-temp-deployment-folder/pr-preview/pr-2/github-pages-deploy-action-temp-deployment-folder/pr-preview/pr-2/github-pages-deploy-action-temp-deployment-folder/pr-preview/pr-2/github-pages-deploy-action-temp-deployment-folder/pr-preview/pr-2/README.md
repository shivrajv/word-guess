# Word Guess

A browser-based word game served entirely from a single `index.html`. No build
step, no server — GitHub hosts it.

## Live site

`main` is the live product, served by GitHub Pages:

> https://shivrajv.github.io/word-guess/

Anything merged to `main` deploys there automatically.

## How hosting is structured

Everything published lives on the **`gh-pages` branch**, which GitHub Pages
serves:

| URL | What it is | Comes from |
| --- | --- | --- |
| `/` | The live game | `main` (via `deploy.yml`) |
| `/pr-preview/pr-<N>/` | A live preview of PR #N | that PR (via `pr-preview.yml`) |

This lets us keep a stable live version on `main` while iterating on concepts
in pull requests — each PR gets its own URL you can open and refresh to see
exactly what it looks like *before* merging.

## Workflows

- **`.github/workflows/deploy.yml`** — on push to `main`, publishes the game to
  the root of `gh-pages`. Uses `keep_files: true` so it never deletes open PR
  previews.
- **`.github/workflows/pr-preview.yml`** — on every PR open/update, publishes
  that PR to `/pr-preview/pr-<N>/` and comments the link on the PR. On close or
  merge, the preview is removed automatically.

## Working on the game

1. Branch off `main`.
2. Edit `index.html` (and add assets as needed).
3. Open a pull request. Within a minute or two, the preview bot comments a live
   URL on the PR — open it, refresh as you push more commits.
4. When it looks right, merge to `main`. The live site updates automatically.

## One-time setup

GitHub Pages must be pointed at the `gh-pages` branch once it exists:

**Settings → Pages → Build and deployment → Source: "Deploy from a branch" →
Branch: `gh-pages` / `(root)` → Save.**
