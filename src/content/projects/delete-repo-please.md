---
title: "Delete Repo Please"
description: A utility to bulk delete your github repos that you abandoned
tags:
  - TypeScript
  - Next.js
  - Tailwind CSS
href: https://delete.denniel.dev
repo: https://github.com/jushoo/delete-repo-please
order: 2
---

Side projects have a way of piling up. Delete Repo Please is a small admin
dashboard for cleaning house: sign in with GitHub, review your repositories in
a table, select the ones you no longer want, and delete them in bulk.

## How it works

Sign in with your GitHub account, and the dashboard lists your repositories
in a sortable, paginated table. Pick the repos you've abandoned, confirm, and
they're deleted through the GitHub API. Deletion requires the `delete_repo`
scope, so the GitHub OAuth flow asks for it up front.

## Under the hood

Built with [Next.js](https://nextjs.org) (App Router, server actions) and
[Octokit](https://github.com/octokit/octokit.js) for the GitHub API, with
auth handled by NextAuth. The UI uses shadcn/ui on Radix primitives,
[TanStack Table](https://tanstack.com/table) for the repo list, and
[Tailwind CSS](https://tailwindcss.com) with dark mode support.
