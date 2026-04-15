# basic-slides

A zero-dependency, single-file markdown slides app. No build step, no framework.

## What it is

Drop `slides.html` into a folder alongside a `slides.md` file, serve it with a local
web server, and you have a full-screen slide deck. Navigate with Space / arrow keys.
Bullets are revealed one at a time.

## Repo structure

```
basic-slides/
  slides.html          ← master template (copy this into each talk folder)
  index.html           ← hub page listing all talks (fetches talks.json)
  talks.json           ← manifest: array of { name, path, description }
  talks/
    welcome/
      slides.html      ← per-talk copy of the template (can be tweaked)
      slides.md        ← the actual slide content
      *.jpg / *.svg    ← images referenced by slides.md
```

To add a new talk: copy `slides.html` into a new folder under `talks/`, create a
`slides.md`, then add an entry to `talks.json`.

## Markdown format (slides.md)

Slides are separated by `---` on its own line.

```markdown
# Slide title
- Bullet one
- Bullet two
- Bullet three

---

# Next slide
- Another bullet
```

### Image variants

**Standalone image** — shown immediately below the heading, before bullets:
```markdown
# Title
![alt text](diagram.png)
- Bullet
```

**Bullet image** — revealed in sequence like a text bullet:
```markdown
# Title
- Text bullet
- ![alt text](chart.png)
- Another text bullet
```

**Image aside** — full-height CSS background on the right (40% width by default).
Uses a frontmatter block between two `---` separators:
```markdown
---
image_aside: photo.jpg
---

# Title
- Bullet one
- Bullet two
```
The aside width defaults to 40%. To change it for a specific deck, edit the
`.aside-bg { width: ... }` rule in that talk's `slides.html` copy.

## Running locally

```sh
cd talks/my-talk
python3 -m http.server
# open http://localhost:8000/slides.html
```

## GitHub Pages

Published at: https://mnsc.github.io/basic-slides/

The hub index is at the root. Each talk is at its folder path, e.g.
`/talks/welcome/slides.html`.

## Development

- Trunk-based: commit and push directly to `main`, no PRs needed
- Master template is `slides.html` at the repo root
- When improving the template, propagate changes to all `talks/*/slides.html` copies
- Font: Roboto (300, 700) loaded from Google Fonts CDN
- Dark theme: background `#0f0f0f`, text `#f0f0f0`

## Navigation

| Key | Action |
|-----|--------|
| Space / → / ↓ | Reveal next bullet; advance to next slide when all bullets shown |
| ← / ↑ | Hide last bullet; go back to previous slide |
