# The Great Yorkshire Geek Meet

Event website, built as a plain [Jekyll](https://jekyllrb.com/) site so it
deploys straight from GitHub Pages — no build step or CI config needed.

## Structure

```
_config.yml       Site-wide settings: event date/venue/price, host details,
                   social links, booking URL. Edit this for most content
                   changes rather than hunting through the HTML.
_layouts/          Page shell (default.html) shared by every page.
_includes/         Reusable fragments: nav.html, footer.html, banner.html.
assets/css/        site.css — all styling, using CSS variables for colour/
                   font/spacing tokens at the top of the file.
assets/js/         site.js — mobile nav toggle + announcement dismiss.
assets/images/     banner.jpeg, mascot.jpg.
index.html          Home
whats-on.html        Activities on the day
tickets.html          Pricing + booking CTA
location.html          Venue, map, accessibility
contact.html            Social links
```

Each page is plain HTML with a small YAML front-matter block (`layout`,
`title`, `description`) — no templating knowledge beyond that is needed to
edit copy.

## Updating event details each year

Almost everything that changes year-to-year lives in `_config.yml`:

- `event.*` — date, time, venue, address, ticket prices
- `booking_url` — set this once ticket booking goes live; while it's blank,
  the Tickets page shows a "coming soon" message instead of a dead link
- `organiser.*` — organiser name/tagline and social links
  (this can't be called `host` — Jekyll reserves that key for `jekyll serve --host`)
- `announcement_enabled` / `announcement_message` — a dismissible banner
  across the top of every page, e.g. for "limited spaces remaining"

## Local preview

Requires Ruby + Bundler.

```sh
gem install bundler jekyll
bundle exec jekyll serve
```

Then open http://localhost:4000.

## Deployment

This repo deploys with a plain `git push` — no GitHub Actions workflow is
needed. GitHub Pages builds Jekyll sites automatically.

One-time setup on GitHub:

1. Push this repo to GitHub.
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**,
   then select the `main` branch and `/ (root)` folder.
4. Under **Custom domain**, enter `reytgoodevents.co.uk` (the `CNAME` file in
   this repo already sets this, so GitHub should pick it up automatically).
   You'll need to point your domain's DNS at GitHub Pages — see
   [GitHub's custom domain docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)
   for the required `A`/`ALIAS`/`CNAME` records.
5. Once DNS has propagated, tick **Enforce HTTPS**.

After that, every push to `main` republishes the site within a minute or two.
