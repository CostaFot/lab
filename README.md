# lab

Web experiments at `lab.costafotiadis.com`, hosted on Railway. Built with
[Astro](https://astro.build) (SSR via the Node adapter) so each experiment is
just a folder — vanilla HTML/JS by default, with the option to drop in any UI
framework per page if one ever needs it.

## Adding an experiment

Create `src/pages/<slug>/index.astro` and export an `experiment` object from
its frontmatter:

```astro
---
import Base from '../../layouts/Base.astro';

export const experiment = {
  title: 'My Thing',
  description: 'One line about it.',
  date: '2026-08-21',
};
---

<Base title={`${experiment.title} — lab`}>
  <!-- anything goes -->
</Base>
```

That's it — the homepage globs `src/pages/*/index.astro` and lists everything
with an `experiment` export, newest first. Pages without the export (or API
routes under `src/pages/api/`) stay unlisted.

Server endpoints, when an experiment needs one: `src/pages/api/<name>.ts` with
a `GET`/`POST` export ([docs](https://docs.astro.build/en/guides/endpoints/)).

## Running locally

```
npm install
npm run dev        # http://localhost:4321
```

## Deploy

Railway builds from `main` per `railway.json`: `npm run build`, then runs the
standalone Node server from `dist/`. If an experiment ever needs its own
long-running process (bot, websocket server, …), add it as a sibling directory
and point a second Railway service at that root — no workspace tooling needed.
