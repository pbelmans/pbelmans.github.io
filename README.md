# Working on this site

This is a Hugo site.

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

## Adding new content

### Create a new blog post

```bash
hugo new content posts/$(date +%Y-%m-%d)-my-title.html
```

Then edit the generated file in `content/posts/`.

- blog posts stay **HTML**, not Markdown;
- keep the `.html` extension;
- only enable `mathjax: true` when the post actually uses LaTeX.

### Add or edit a standalone page

Create or edit a file in `content/`, for example:

```text
content/about.html
content/teaching.html
content/writing.html
```

Use `url:` in front matter whenever you need to preserve an exact public path.

### Add static files

Anything that should be served unchanged at the public site root belongs in
`static/`, for example:

```text
static/assets/
static/css/
static/favicon.png
static/CNAME
static/atlas/
static/courses/
static/notes/
static/projects/
```

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

