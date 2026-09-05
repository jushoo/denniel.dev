---
title: "Johnnie's Poker"
description: A minimalist planning poker tool for agile teams.
tags:
  - TypeScript
  - SolidJS
  - WebSockets
  - Docker
href: https://poker.denniel.dev
repo: https://github.com/jushoo/johnnies-poker
order: 1
---

Planning poker helps an agile team estimate work. Each member votes on story
points. The votes stay hidden until all members vote. This keeps the estimates
honest and fast.

Johnnie's Poker does one thing: planning poker. No login, no setup, no
distractions. Open the site, share the room link, and start the vote.

## How it works

Create a room, share the link, and everyone joins with just a name. Votes stay
hidden until every member has picked a card, then all votes reveal at once.
Results come with the average, median, mode, and an agreement percentage, so
the team can spot outliers and converge quickly.

## Features

- **Real-time voting** — rooms sync instantly over WebSockets.
- **Fibonacci scale** — standard story point values, plus `?` and the `☕`
  "need a break" card.
- **Reveal & stats** — average, median, mode, and agreement percentage on
  reveal.
- **Spectator mode** — observe the session without voting.
- **Responsive** — works on desktop and mobile.

## Under the hood

Built with [SolidStart](https://start.solidjs.com/) on the
[Nitro](https://nitro.unjs.io/) server engine (via Vinxi), using
[crossws](https://crossws.unjs.io/) for WebSockets and
[Vanilla Extract](https://vanilla-extract.style/) for zero-runtime CSS-in-JS.
State lives in the room, not a database — rooms exist only while the session
is live. Deployed as a Docker container on a VPS.
