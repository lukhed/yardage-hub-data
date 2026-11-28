# Contributing

Thanks for wanting to help. **This repo is generated from the yardage-hub database, so changes
can't be made here:** pull requests are closed automatically, because the next weekly snapshot
would overwrite them.

Instead, fix the data at the source: [loopdiaries.com](https://loopdiaries.com) or
[the API](https://loopdiaries.com/developers#key). Your change is reviewed, credited to you, and
lands in the [live API](https://loopdiaries.com/developers/docs) right away and in this repo with
the next snapshot.

1. Find the course on [loopdiaries.com](https://loopdiaries.com),
   or open `https://loopdiaries.com/courses/c/<id>` with its `id` from `courses.csv`.
2. **Easiest:** add the link to the course's published scorecard (or send photos of the
   card). We read the card and fill in its tees, ratings, slopes, pars, and yardages.
3. Or click **Suggest an edit** to change values directly, **vote** on edits waiting for review,
   or **report a dead link**.
4. **Building an app?** Your app can send edits too, and they go through the same review. See the
   [API documentation](https://loopdiaries.com/developers/docs#submit-edit).

A free Loop Diaries account is needed to send edits, so they can be credited to you.

**What does belong here:**

- A course that's missing entirely
  ([open an issue](https://github.com/lukhed/yardage-hub-data/issues/new?template=missing-course.yml)).
- An app you built on yardage-hub, to be listed in the README
  ([open an issue](https://github.com/lukhed/yardage-hub-data/issues/new?template=app-listing.yml)).
- A problem with the files themselves (a broken CSV, a confusing column): open an issue.
