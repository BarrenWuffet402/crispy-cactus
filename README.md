# crispy-cactus

Sandbox monorepo. Each top-level directory is a self-contained project with its
own Netlify site.

## Layout

```
crispy-cactus/
├── requirement-builder/       # project — own Netlify site
│   ├── index.html
│   └── netlify.toml
└── tronrud-sveiseverksted/    # project — own Netlify site
    ├── index.html
    └── netlify.toml
```

## Adding a project

1. `mkdir <project-name>` at the repo root.
2. Add a `netlify.toml` with `command = ""` and `publish = "."` (copy an existing one).
3. In Netlify: **Add new site → Import from Git → crispy-cactus**, then set
   **Base directory** to `<project-name>`. Netlify will only rebuild that site
   when files under that directory change.

## Branches

| Branch | Purpose | Deploy |
| --- | --- | --- |
| `qa-develop` | Where new work lands. Agents commit here directly. | Auto-deploys to a branch URL. |
| `main` | Reviewed and approved only. | Production. |

`main` accepts changes **only** via pull request from `qa-develop`, merged by a
human. Nothing reaches production without review.

## Conventions

- Projects are independent — no cross-imports between top-level directories.
- Secrets live in Netlify environment variables, never in the repo.
- Keep each project deployable on its own; if two need shared code, extract it
  deliberately rather than reaching across directories.
