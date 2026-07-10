# Reyt Good Events

Parent events website, built as a plain [Jekyll](https://jekyllrb.com/) site
so it deploys straight from GitHub Pages — no build step or CI config needed.

## Structure

```
_config.yml       Site-wide settings: brand copy, organiser details, social
                   links, the events collection config. Edit this for
                   site-wide changes rather than hunting through the HTML.
_events/           One file per event — see "Adding a new event" below.
_layouts/          default.html (page shell) and event.html (event pages).
_includes/         Reusable fragments: nav.html, footer.html, banner.html.
assets/css/        site.css — all styling, using CSS variables for colour/
                   font/spacing tokens at the top of the file.
assets/js/         site.js — mobile nav toggle + announcement dismiss.
assets/images/     people-playing-games.avif, mascot.jpg, game1–4.jpg.
index.html          Home — intro, "why people love us", next event spotlight
events/index.html    All events (upcoming + past)
book-online.html     Booking links for every upcoming event
about.html            About Reyt Good Events
traders.html            Info for traders wanting a stall
contact.html              Phone, email, social links
```

Each page is plain HTML with a small YAML front-matter block (`layout`,
`title`, `description`) — no templating knowledge beyond that is needed to
edit copy.

## Adding a new event

Add one new file to `_events/`, e.g. `_events/spring-fayre-2027.md`. The
filename becomes the event's web address (`/events/spring-fayre-2027/`), so
use lowercase words separated by hyphens, no spaces.

Copy `_events/great-yorkshire-geek-meet.md` as a starting template and
change the front-matter fields: `name`, `status` (`upcoming` or `past`),
`live` (`true`/`false` — set `false` to hide the event everywhere without
deleting it), `summary`, `date`, `date_display`, `time_display`,
venue/address fields, `price_adult` / `price_under12`, `booking_url`,
`image`, and the `activities` / `accessibility` / `highlights` /
`love_reasons` / `sessions` / `getting_there` / `top_tips` lists. No other
files need to change — the new event appears automatically on the homepage
(if it's the soonest upcoming one), the Events page, the Book Online page,
and the nav dropdown, as long as `live` is `true`.

Once an event has happened, set its `status` to `past` and it moves from
the upcoming listings into "Past Events".

- `booking_url` — set this once ticket booking goes live for that event;
  while it's blank, the event's Tickets section shows a "coming soon"
  message instead of a dead link
- `organiser.*` (in `_config.yml`) — organiser name/tagline, phone, email
  and social links, shared across all events
  (this can't be called `host` — Jekyll reserves that key for `jekyll serve --host`)
- `announcement_enabled` / `announcement_message` (in `_config.yml`) — a
  dismissible banner across the top of every page, e.g. for "limited spaces
  remaining"

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

The site is served at the default GitHub Pages URL for this repo (no custom
domain), e.g. `https://<username>.github.io/reytgoodevents/`. `_config.yml`'s
`baseurl` is set to `/reytgoodevents` to match — update it if the repo is
ever renamed.

After that, every push to `main` republishes the site within a minute or two.
