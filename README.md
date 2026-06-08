# Create_Resume

A full-stack résumé / CV builder — build a résumé section by section with a live
preview, customise the layout/colours/fonts, download a vector PDF, and (with an
account) save multiple résumés to the cloud and reload them later. Fully responsive,
with a light/dark theme.

**Live:** <https://resume.axlothecook.com> — self-hosted on a Raspberry Pi, exposed
via Cloudflare Tunnel.

The project is split across three repositories. Pick the one you want to view:

| Repository | What it is |
| --- | --- |
| [**Front end**](https://github.com/axlothecook/Create_Resume) | React 19 + Vite single-page app. The résumé-builder UI + live preview + PDF export. |
| [**Back end**](https://github.com/axlothecook/Create_Resume-backend) | Node.js + Express 5 + MongoDB REST API. Accounts (session auth) + saved résumés. |
| [**Deploy**](https://github.com/axlothecook/create-resume-deploy) | Docker Compose orchestration + Cloudflare Tunnel for the Raspberry Pi deploy. Includes `ARCHITECTURE.md` + `DEPLOY.md`. |

## How it fits together

```
Browser ─▶ Cloudflare Tunnel ─┬─▶ Front end (nginx, static SPA)
                              │
                              └─▶ Back end (Express API) ─▶ MongoDB
```

- The **front end** is a static SPA served by nginx; the browser calls the API
  directly (the API URL is baked in at build time).
- The **back end** owns all data — accounts and saved résumés — with session-cookie
  auth. Résumés are stored as JSON in MongoDB (no object storage needed).
- The **deploy** repo ties everything together with Docker Compose and runs the whole
  stack (plus MongoDB and `cloudflared`) on a Raspberry Pi. CI builds the images and
  auto-deploys on every push to `main`.

## Tech stack at a glance

- **Front end:** React 19, Vite, @react-pdf/renderer (vector PDF), @dnd-kit (drag-to-
  reorder), self-hosted Poppins, plain CSS (mobile-first, light/dark theme).
- **Back end:** Node.js, Express 5, MongoDB / Mongoose, passport-local + sessions.
- **Infra:** Docker / Docker Compose, nginx, GitHub Actions (GHCR), Cloudflare Tunnel,
  Tailscale (CI → Pi), Raspberry Pi.

## Features

- Section-by-section editor (personal details, experience, education, projects,
  skills & languages) with drag-to-reorder and per-item show/hide.
- Live A4 preview that mirrors the downloadable PDF; customise layout, accent colour,
  and font.
- One-click **vector PDF** download.
- Accounts: sign up / log in, save up to 5 résumés, reload them as live A4 cards,
  or browse as a guest (build + download, no save).
- Fully responsive — a full-screen overlay menu + scale-to-fit preview on mobile.
