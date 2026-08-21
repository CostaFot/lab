# lab

Web experiments site at lab.costafotiadis.com. Small self-contained toys for fun;
the serious content lives on costafotiadis.com.

## Stack

- Astro 5 in server mode with the Node adapter (`@astrojs/node`, standalone).
- three.js is available for 3D experiments.
- Deployed on Railway. **Every push to `main` deploys to production** — commit
  freely, but only push when the change is verified working, and mention that a
  push will deploy.

## Adding an experiment

Create `src/pages/<slug>/index.astro` and export an `experiment` object from its
frontmatter:

```ts
export const experiment = {
  title: 'Name',
  description: 'One line, shown on the homepage.',
  date: 'YYYY-MM-DD',
};
```

The homepage (`src/pages/index.astro`) auto-discovers these via `import.meta.glob`
— there is no registry to update. Pages without an `experiment` export are not
listed. Use the `Base` layout and its CSS variables (`--bg`, `--fg`, `--muted`,
`--accent`, `--card`, `--border`) so pages match the site in light and dark mode.
See `src/pages/bounce/index.astro` for the pattern.

## Commands

- `npm run dev` — dev server on port 4321 (also launchable via `.claude/launch.json`, config name "lab").
- `npm run build` then `npm start` — production build and serve.
- No tests or linting; verify experiments by running them in the browser.
