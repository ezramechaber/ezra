# ezramechaber.com

A small, dependency-free personal site.

## Preview

From this directory:

```sh
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

## Structure

- `index.html` — content and metadata
- `style.css` — the complete visual system
- `assets/ezra-halftone.png` — square halftone portrait
- `favicon.svg` — browser icon

The site can be hosted by any static file host. There is no build step.

## Hosting

GitHub Pages serves the site from the repository root. The `CNAME` file binds
the Pages site to `ezramechaber.com`.
