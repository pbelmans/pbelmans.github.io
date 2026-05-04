# Working on this site after the Hugo migration

This repository is intended to be a **single in-place Hugo site**. There is no
`hugo-site/` subdirectory.

The goal of this README is simple: if a task used to be obvious in Jekyll, this
file should tell you what to do in Hugo instead.

## Jekyll → Hugo quick mapping

| What I used to do in Jekyll | What I do now in Hugo |
|---|---|
| Run `./run-jekyll.fish` | `hugo server --buildFuture --disableFastRender --disableLiveReload --port 8080` for live preview, or `npm run serve` to serve prettified output |
| Build into `_jekyll_site/` | `npm run build` |
| Put blog posts in `_posts/YYYY-MM-DD-slug.html` | Run `hugo new content posts/YYYY-MM-DD-slug.html`, then edit `content/posts/YYYY-MM-DD-slug.html` |
| Edit `_layouts/default.html` | Edit `layouts/_default/baseof.html` |
| Edit `_layouts/post.html` | Edit `layouts/posts/single.html` |
| Edit `_layouts/page.html` | Edit `layouts/_default/single.html` |
| Edit `_includes/*` | Edit `layouts/partials/*` |
| Edit top-level pages like `about.html` | Edit `content/about.html` (and similar files in `content/`) |
| Edit `_data/*.yaml` | Edit `data/*.yaml` |
| Add root-served files such as CSS, images, `CNAME`, or standalone sub-sites | Put them in `static/` |
| Check URL parity by looking at `_jekyll_site/` | Build `_hugo_site/` and compare against `url-inventory.txt` |
| Smoke-test the local site manually | Run the Playwright crawl + screenshot comparison against `https://pbelmans.ncag.info` |

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

## Day-to-day commands

### Start the local dev server

This is the Hugo equivalent of the old `run-jekyll.fish` workflow:

```bash
hugo server --buildFuture --disableFastRender --disableLiveReload --port 8080
```

If you want to serve the already-generated, Prettier-formatted HTML instead:

```bash
npm run serve
```

### Build the site

```bash
npm run build
```

For deployable output in `public/`:

```bash
npm run build:public
```

### Create a new blog post

```bash
hugo new content posts/$(date +%Y-%m-%d)-my-title.html
```

Important:

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

### Edit templates and reusable snippets

- shared wrapper: `layouts/_default/baseof.html`
- generic page layout: `layouts/_default/single.html`
- post layout: `layouts/posts/single.html`
- partials and inline SVG snippets: `layouts/partials/`

### Edit data files

```text
data/coauthors.yaml
data/papers.yaml
```

These are available in templates through `hugo.Data`.

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

## URL and parity checks

### Compare generated URLs

```bash
npm run build
find _hugo_site -type f | sort | sed 's|_hugo_site||' > hugo-urls.txt
diff url-inventory.txt hugo-urls.txt
```

### Crawl from the homepage and compare to the live site

Start the local server:

```bash
npm run serve
```

Install the test tooling once:

```bash
npm install
npx playwright install chromium
```

Then run:

```bash
npm run test:parity
npm run report:parity
```

That script should:

1. crawl internal URLs starting from `/`;
2. save the discovered paths to `crawl-urls.txt`;
3. compare each crawled path locally and at `https://pbelmans.ncag.info`;
4. save screenshots for both sides;
5. fail on missing pages, JS errors, or large visual differences.

Screenshots and diff images are written to `test-output/parity/`.
The categorized summary and HTML diff pointers are written to
`test-output/parity/report.md`.

### Validate generated HTML

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

## Rules worth repeating

- there is **no** `hugo-site/` directory;
- do **not** switch posts to Markdown;
- preserve URLs unless there is a deliberate documented reason not to;
- run the crawl + screenshot parity test before asking for review.
