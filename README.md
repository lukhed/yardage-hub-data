# yardage-hub data

Open golf course data for the United States: **16,000+ courses** with their location, contact
details, holes and pars, and, for a growing number, tees, course ratings, slopes, and hole-by-hole
yardages. Free to use under the [Open Database License](#license).

This repo is a weekly snapshot of the [yardage-hub](https://lukeheide.com/sports/yardage-hub)
database, as plain CSV files you can open in a spreadsheet or load into anything.

> **See something wrong or missing? Fix it on the site, not here.**
> This repo is generated, so pull requests here are closed automatically. Corrections go through
> [lukeheide.com/sports/yardage-hub](https://lukeheide.com/sports/yardage-hub), where they're
> reviewed, credited to you, and land in the live API right away and in this repo with the next
> snapshot. The fastest way to help is to [add a course's scorecard link](#the-easiest-way-to-help-add-a-scorecard-link).

## How complete is the data

Most open golf data is a list of names and locations. This is how far yardage-hub has gotten
toward everything a scoring app needs, counted every week:

Of **16,235 golf courses** (snapshot 2026-10-26; driving ranges, disc, and mini golf not counted), this is how many have each kind of data:

| | Courses | Share |
|---|---:|---:|
| A published scorecard is linked | 147 | 1% |
| The scorecard link was set or checked working in the last year | 147 | 1% |
| Every hole has its par | 5,716 | 35% |
| Every hole has its handicap (stroke index) | 2,385 | 15% |
| At least one set of tees | 229 | 1% |
| A course rating and slope | 96 | 1% |
| Hole-by-hole yardages for a set of tees | 194 | 1% |
| Pars, handicaps, ratings, and yardages: everything a scoring app needs | 87 | 1% |

**By state and region:** [COVERAGE.md](COVERAGE.md) has every state, and each state's folder has its regions, e.g. [Michigan](data/US/MI/). Low numbers are where your [help](#help-fix-the-data) goes furthest.

## Download

- **Everything in one file:** the zip on the [latest release](https://github.com/lukhed/yardage-hub-data/releases/latest). It has
  every region, plus `provenance.csv` (where each value came from).
- **One state:** browse [`data/`](data/) and download that state's folder, e.g.
  [`data/US/MI/`](data/US/MI/).
- **Every snapshot:** this repo's history. Each weekly commit is a dated snapshot, and each one
  has a release.

## Help fix the data

Every course has a page on the site. Find it by searching
[lukeheide.com/sports/yardage-hub](https://lukeheide.com/sports/yardage-hub), or go straight to
it with the course's `id` from `courses.csv`:

```
https://lukeheide.com/sports/yardage-hub?course=<id>
```

### The easiest way to help: add a scorecard link

Most courses publish their scorecard on their website as a page, an image, or a PDF. On the
course's page, click **Add the scorecard link** and paste it. That's all.

A link is the most useful thing you can give: once it's reviewed, we read the card and fill in
every tee, rating, slope, par, handicap, and yardage from it, and the card is cited as the source
of each value. It takes a minute and fills in a whole course.

### Other ways to help

- **Suggest an edit.** On the course's page, click **Suggest an edit** to correct a par, add a
  tee, fix a phone number or website, or mark a course closed. Cite where the numbers come from
  if you can.
- **Vote on pending edits.** Edits waiting for review show on the course's page. A 👍 or 👎 (with
  a reason) helps reviewers decide, and the most-backed edits are reviewed first.
- **Report dead links.** If a course's website or scorecard link is broken, say so on its page.
- **A course that isn't listed at all?** [Open an issue here](https://github.com/lukhed/yardage-hub-data/issues/new?template=missing-course.yml)
  with its name, city, and website.

You'll need a free account on lukeheide.com to send edits, so they can be credited to you. Every
change is reviewed before it goes live, and every value keeps a record of where it came from.

**Building an app?** Your app can send edits too, through the
[yardage-hub API](https://lukeheide.com/sports/yardage-hub/docs). They go through the same review.

## What's in the files

Each state has five CSV files and a README with its coverage by region: `data/<country>/<state>/` (courses with no state are in
`_unknown/`). They join on `course_id`, and tees on `course_id` + `tee_key`.

### `courses.csv`: one row per course

| Column | |
|---|---|
| `id` | yardage-hub's id for the course. Stable: use it to join, and to link to the course's page |
| `osm_id` | The OpenStreetMap way or relation it came from, e.g. `way/16650363`, if any |
| `name`, `club_name` | |
| `kind` | `course`, `par3`, `practice` (ranges), `disc`, `mini`, or `facility` (below) |
| `facility_id` | For a course at a facility with several courses, the facility's `id` |
| `type` | `public`, `private`, `semi_private`, `resort`, `municipal`, `military` |
| `status` | `active` or `closed` |
| `holes_count`, `par` | `par` is the sum of the holes' pars, when every hole has one |
| `architect`, `year_built` | |
| `phone`, `website`, `scorecard_url` | `scorecard_url` is the course's published scorecard |
| `address`, `city`, `state`, `postcode`, `country`, `lat`, `lon` | |
| `updated_at` | When the course last changed (UTC) |

### `holes.csv`

`course_id`, `number`, `par`, `handicap` (the stroke index, 1 = hardest), `women_par` (only where
the women's par differs), `women_handicap` (when the card has a women's handicap row).

### `tees.csv`: one row per set of tees

`course_id`, `tee_key` (stable per course, e.g. `blue`), `name`, `color`, `total_yardage` (as
published).

### `tee_ratings.csv`

`course_id`, `tee_key`, `gender` (`M`/`F`, or empty when the source doesn't say), `par`,
`rating`, `slope`. A set of tees rated for men and women has two rows.

### `tee_holes.csv`

`course_id`, `tee_key`, `hole_number`, `yards`.

### `manifest.json`, `coverage.json`, and the coverage pages

`manifest.json` has the snapshot date, row counts, and the courses per state. `coverage.json` has
how complete the data is nationally, by state, and by region (the numbers behind
[COVERAGE.md](COVERAGE.md) and each state folder's README). Every course in `courses.csv` belongs
to one region; the [API](https://lukeheide.com/sports/yardage-hub/docs) gives each course's region.

### Things to know

- **A course is something you play a round on.** Where a site has several (a 27-hole facility's
  pairs of nines, or named courses like West and North), each is its own course with its own
  ratings, and a row of kind `facility` groups them. If you want a list of places to play golf,
  skip `facility` rows; if you want a list of clubs, use them.
- **Coverage varies** ([how much](COVERAGE.md)). Every course has a location; most have holes and
  pars from OpenStreetMap; tees, ratings, and yardages come from published scorecards and
  contributors and are still being filled in. An empty cell means we don't know yet, which is where your
  [help](#help-fix-the-data) comes in.
- **`kind` is inferred** from OpenStreetMap tags, names, and mapped holes, so a few are wrong.
  Those can be fixed with an edit too.
- Yardages are in yards. Blank means unknown, never zero.

## License

The data is available under the [Open Database License (ODbL) 1.0](https://opendatacommons.org/licenses/odbl/1-0/)
(see [LICENSE](LICENSE)). It contains information from
[OpenStreetMap](https://www.openstreetmap.org/copyright), © OpenStreetMap contributors.

In short: you can use, share, and build on it, commercially too, as long as you:

- **Attribute** it: "Course data from yardage-hub (lukeheide.com/sports/yardage-hub), including
  OpenStreetMap data (© OpenStreetMap contributors), under the ODbL."
- **Share alike:** if you publish a database built from this one, release it under the ODbL too.
- **Keep it open:** don't apply technical restrictions that stop others using it.

Forks are welcome under these terms. If you correct something in your copy, please send the fix
[through the site](#help-fix-the-data) as well, so everyone gets it.

## How this repo is made

The yardage-hub repo exports the database every week (`python -m pipeline export`) and commits
the result here, with a release holding the zip. Only reviewed, live data is exported, never
pending edits or any account details. For live data between snapshots, use the
[API](https://lukeheide.com/sports/yardage-hub/docs).
