# Contributing

Thanks for wanting to help. **This repo is generated from the yardage-hub database, so changes
can't be made here:** pull requests are closed automatically, because the next weekly snapshot
would overwrite them.

Instead, fix the data at the source, where your change is reviewed, credited to you, and reaches
everyone using the data or the API:

1. Find the course on [lukeheide.com/sports/yardage-hub](https://lukeheide.com/sports/yardage-hub),
   or open `https://lukeheide.com/sports/yardage-hub?course=<id>` with its `id` from `courses.csv`.
2. **Easiest:** click **Add the scorecard link** and paste the link to the course's published
   scorecard. We read the card and fill in its tees, ratings, slopes, pars, and yardages.
3. Or click **Suggest an edit** to change values directly, **vote** on edits waiting for review,
   or **report a dead link**.

A free lukeheide.com account is needed to send edits. Apps can send them through the
[API](https://lukeheide.com/sports/yardage-hub/docs).

**What does belong here:** a course that's missing entirely
([open an issue](https://github.com/lukhed/yardage-hub-data/issues/new?template=missing-course.yml)), or a problem with the files
themselves (a broken CSV, a confusing column). Open an issue for those.
