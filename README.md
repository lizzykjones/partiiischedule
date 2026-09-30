# partiiischedule.io

**Live site: https://lizzykjones.github.io/partiiischedule/**

A Hyperschedule-style timetable planner for Cambridge Mathematical Tripos Part III (2026–27).

It's a static site with no build step and no backend: `index.html` holds all the HTML, CSS, JavaScript and course data. Fonts load from Google Fonts. Each visitor's schedules are saved in their own browser (localStorage).

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole app |
| `favicon.svg` | Browser tab icon |

## Run locally

```
cd partiiischedule
python3 -m http.server 8000
```

Then open http://localhost:8000. You can also open `index.html` directly in a browser.

## Deploy

The site is served by GitHub Pages from the root of `main`, so pushing to `main` redeploys it in about a minute.

To use a custom domain later (e.g. `partiiischedule.io`), add it under Settings → Pages → Custom domain, and point your DNS at GitHub Pages as described in [GitHub's docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site).

## Updating the course list

The course data is the `RAW` array near the top of the `<script>` in `index.html`. Each row looks like this:

```
[term, title, lecturers, days, startHour, room, area, extras?]
["M","Cosmology","Prof. E. Pajer","MWF",9,"MR3","Astrophysics & Cosmology"]
```

- `term`: `M` (Michaelmas), `L` (Lent) or `E` (Easter)
- `days`: any of `M Tu W Th F S`, written together (e.g. `TuThS`)
- `extras` (optional):
  - `dur`: length in hours (default 1)
  - `count`: exact number of lectures
  - `first`: first lecture date, `YYYY-MM-DD`
  - `notes`: a list of text notes
  - `ex`: a list of cancelled dates
  - `add`: a list of extra sessions, each `[date, hour, dur, room]`

Lecture-term dates for the calendar export are in `TERMS`. When the Faculty publishes the next year's list, update `RAW`, `TERMS` and the "last updated" line in the header.

Course IDs are made from the term and title, so saved schedules and share codes carry across updates as long as titles don't change.
