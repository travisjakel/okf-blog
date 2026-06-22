# okf-ingest blog

📖 **Read it live → <https://travisjakel.github.io/okf-blog/>**

*(This repo is just the blog's source. Send readers to the live site above — not here.)*

A minimal [Quarto](https://quarto.org) blog that hosts the okf-ingest write-ups and
provides the **full-content RSS feed** required by R-bloggers and Planet Python.

## Build & publish

```bash
quarto preview                     # local preview at http://localhost:port
quarto publish gh-pages            # one-time manual publish, or just push (CI does it)
```

Pushing to `main` triggers `.github/workflows/publish.yml`, which renders and deploys
to the `gh-pages` branch. Enable Pages → "Deploy from branch: gh-pages" in repo settings.

## Feed (the important part)

The home page (`index.qmd`) declares `feed: { type: full }`, so `index.xml` carries the
**full post body** — R-bloggers requires full content, not summaries. After the site is
live, validate the feed at <https://validator.w3.org/feed/> then submit:

- **R-bloggers** — submit the feed URL at <https://www.r-bloggers.com/add-your-blog/>.
  (The footer links back to r-bloggers.com, which they require.)
- **Planet Python** — submit the feed via the Planet Python listing process.

If you later mix many non-R posts, create an R-only listing page and submit *its* feed
(`<page>.xml`) to R-bloggers instead of the site-wide one.

## ⚠️ Before publishing the posts

The posts' install lines only work once the packages are live:

- R: install the R-universe GitHub App so `install.packages("okf", repos = "https://travisjakel.r-universe.dev")` resolves.
- Python: `cd ../okf-ingest/py && python -m twine upload dist/*` so `pip install okf-ingest` resolves.
