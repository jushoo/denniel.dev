# denniel.dev

Personal site of Denniel Joshua — projects, work, and contact.

Built with [Astro](https://astro.build) and [Tailwind CSS](https://tailwindcss.com).
Project details live in `src/content/projects/` as Markdown files with
frontmatter (title, description, tags, href, repo, order) and are rendered
from the content collection.

## Development

```sh
pnpm install
pnpm dev
```

| Command                | Action                                           |
| :--------------------- | :----------------------------------------------- |
| `pnpm install`         | Installs dependencies                            |
| `pnpm dev`             | Starts local dev server at `localhost:4321`      |
| `pnpm build`           | Build your production site to `./dist/`          |
| `pnpm preview`         | Preview your build locally, before deploying     |
| `pnpm astro ...`       | Run CLI commands like `astro check`              |

Requires Node.js >= 22.12.0.

## Adding a project

Create a new Markdown file in `src/content/projects/`:

```md
---
title: "Project Name"
description: One-line description.
tags:
  - TypeScript
href: https://example.com
repo: https://github.com/user/repo
order: 3
---

Project writeup goes here.
```

## Analytics (Umami)

Umami is wired up via `src/components/Umami.astro` and activated through
environment variables — no tracking snippet is committed to the repo.

1. Copy the example file and fill in your website ID:

   ```sh
   cp .env.example .env
   ```

   ```dotenv
   PUBLIC_UMAMI_WEBSITE_ID=your-website-id
   ```

2. Optional overrides:
   - `PUBLIC_UMAMI_SRC` — custom/self-hosted script URL (defaults to
     `https://cloud.umami.is/script.js`).
   - `PUBLIC_UMAMI_DOMAINS` — comma-separated domains to track.

`.env` is gitignored. The site is built in **GitHub Actions** (see
`.github/workflows/deploy.yml`) and the finished `dist/` is uploaded to
Cloudflare Pages — Cloudflare does not run a build. Because Astro inlines
`PUBLIC_*` values at build time, the website ID must be available to the
GitHub Actions build.

Add it as a **repository variable** (not the Cloudflare dashboard):

> GitHub repo → **Settings → Secrets and variables → Actions → Variables →
> New repository variable**
>
> Name: `PUBLIC_UMAMI_WEBSITE_ID` · Value: your website ID

The workflow already passes `vars.PUBLIC_UMAMI_WEBSITE_ID` into the
`pnpm build` step. When it is unset, no script is rendered.

## Learn more

Check the [Astro documentation](https://docs.astro.build).
