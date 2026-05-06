# Working on this site

This is a Hugo site. For migration notes and day-to-day development commands,
see [hugo.md](hugo.md).

## Repository layout

Once the migration is complete, the important locations are:

| Path | Purpose |
|---|---|
| `hugo.yaml` | Hugo site configuration |
| `content/posts/` | Blog posts |
| `content/` | Standalone pages |
| `layouts/_default/` | Shared page templates |
| `layouts/posts/` | Post-specific templates |
| `layouts/partials/` | Reusable partials, including migrated SVG includes |
| `data/` | YAML data files |
| `static/` | Files served from the site root |
| `archetypes/posts.html` | Template for new HTML blog posts |
| `test/crawl-and-compare.mjs` | Crawl + screenshot parity test |

## Validate generated HTML

```bash
npm run validate:html
```

## Deployment

Deployment should use a root-level Hugo workflow in `.github/workflows/`. The
published directory is `./public`, not a nested `hugo-site/public`.

There is also a Forgejo workflow in `.forgejo/workflows/codeberg-pages.yml` for
deploying to Codeberg Pages at
`https://<owner>.codeberg.page/<repository>/`.

That workflow targets the newer `codeberg.page`/git-pages flow. If you later
want a custom domain on Codeberg Pages, you will need the legacy `.domains` +
`pages` branch workflow instead.


