# AGENTS.md

## Project

This is Ezra Mechaber's simple static personal site at
https://ezramechaber.com.

The GitHub repository is `ezramechaber/ezra`. GitHub Pages publishes the
repository root.

## Structure

- `index.html` is the page entry point.
- `style.css` contains all site styling.
- `assets/` contains images, including the square halftone portrait.
- `CNAME` must remain `ezramechaber.com`.
- Keep the site dependency-free unless explicitly asked otherwise.

## Development

Work from the repository root.

Preview locally with:

    python3 -m http.server 8000

Check desktop and mobile layouts after visual changes. Preserve semantic HTML,
keyboard accessibility, useful alt text, and relative asset paths.

## Publishing

Use local Git and SSH for ordinary publishing. Do not force-push unless
explicitly requested.

Before calling a deployment complete:

1. Confirm the GitHub Pages deployment succeeded.
2. Confirm `https://ezramechaber.com` returns the updated page.
3. Confirm `https://www.ezramechaber.com` redirects to the apex domain.
4. Confirm HTTPS remains enforced.

## Cloudflare and DNS

Cloudflare is authoritative for DNS. Namecheap is the registrar.

Prefer the Cloudflare MCP API for DNS work. Read current records before writing,
make the smallest possible change, reread after writing, and verify publicly
with `dig` and `curl`.

The GitHub Pages web records should remain DNS-only. Preserve MX, SPF, DKIM,
Google verification, and GitHub ownership-verification records unless a request
explicitly includes them.

Never store account IDs, API tokens, verification values, credentials, or other
secrets in this repository.

## GitHub

Prefer:

- local Git for file changes, commits, and pushes;
- the GitHub connector for repository, commit, PR, and issue data;
- `gh` for Actions logs or API operations not covered by the connector;
- the browser only for authentication or settings unavailable through APIs.
