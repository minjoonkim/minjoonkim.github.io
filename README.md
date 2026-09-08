# minjoon.kim

Jekyll 4 site, built and deployed by GitHub Actions.

## Design

- **Ground** oat `#F2ECE1`, ink warm charcoal `#2A2E2B`
- **Hairlines** cool chrome `#B7BDBB` — deliberately cooler than the ground
- **Links** olive `#5F7350`; **mark** terracotta `#B96F4C`, used once per page
- **Tints** sage and dusty pink, for tags only
- **Type** Hanken Grotesk for headings, labels, nav and UI; Faustina for
  paragraphs; system mono for code
- **Layout** narrow label rail plus content column, collapsing to one column
  under 46rem

Every colour and size lives in `_sass/_tokens.scss`. Change it there, nowhere else.

## Setup

```
bundle install
bundle exec jekyll serve
```

Then set the repo's Pages source to **GitHub Actions** (Settings → Pages →
Build and deployment → Source). The workflow in `.github/workflows/deploy.yml`
handles the rest on every push to `main`.

## Adding a Korean font

The site expects a subset Pretendard at
`assets/fonts/Pretendard-Regular.subset.woff2`. From the official repo
(`orioncactus/pretendard`, SIL OFL — not the `fonts-archive` mirror):

```
pip install fonttools brotli
pyftsubset Pretendard-Regular.otf \
  --text="김민준" --flavor=woff2 \
  --output-file=assets/fonts/Pretendard-Regular.subset.woff2
```

`unicode-range` in `_tokens.scss` scopes it to Hangul, so Pretendard can never
override Hanken for Latin text. If you start writing Korean posts, swap the
subset for the full dynamic subset and widen that rule.

## Updating content

| What | Where |
|---|---|
| Short dated notes | `_data/updates.yml` — one entry, no post needed |
| Now page | `_data/now.yml` |
| Projects | `_data/projects.yml` |
| Publications | `_data/publications.yml` |
| Roles and education | `_data/bio.yml`, `_data/education.yml` |
| About paragraphs | `index.html` |
| Posts | `_posts/YYYY-MM-DD-slug.md` |

The CV is data, not markup — updating it is editing YAML.

## Body copy

Two dials in `_sass/_tokens.scss`:

```
--prose-size: 1.03rem;
--prose-leading: 1.85;
```

Faustina has a large x-height and a fairly economical set width, so it runs
tighter than it looks. If prose feels cramped, raise the leading before the
size.

## Still to do

- [ ] Subset and commit the Pretendard file
- [ ] Delete `_posts/2026-09-08-example-post.md`
- [ ] Fix the CSCW '21 publication URL in `_data/publications.yml` — the old
      site pointed it at the CHI '20 DOI
- [ ] Replace `hello@minjoon.kim` in `_config.yml` with a real address
- [ ] Add an `og-image.png` and reference it in `_config.yml` for link previews
- [ ] Decide whether to keep the old `/articles/...` URLs alive with
      `jekyll-redirect-from`, or let them go
