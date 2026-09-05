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

## Learn more

Check the [Astro documentation](https://docs.astro.build).
