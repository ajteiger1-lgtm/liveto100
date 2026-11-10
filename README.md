# Live to 100

A personal workout tracker. Open `https://ajteiger1-lgtm.github.io/liveto100/` on iPhone, Share, Add to Home Screen.

## Where your data lives
On your phone, in this site's storage. Updating the files in this repo does not touch it.
Your data is lost only if you: clear Safari website data for this site, delete the home-screen app and its data,
or change the site address (renaming the repo or your GitHub username creates a new, empty storage).
**Export a backup from History every week.**

## Updating the app
Add file, Upload files, drop in the new files, replace the old ones, Commit. Then close and reopen the app.
Do not rename the repo.

## Backup file format
`live-to-100-backup-YYYY-MM-DD.json`:
`{ "app": "live-to-100", "schema": 2, "exported": "...", "sessions": { "<date>_<day>": { ... } } }`

Each session: `id, date, key (mon..sun), name, week, done, durationSec, effort, recov, rating, entries, checks, times`.
`entries[moveId].sets[]` holds `{ w, r, rir, note?, w2?, r2? }`: weight, reps, reps left in the tank, an optional note,
and for per-side moves `w`/`r` are the left side and `w2`/`r2` the right side.
Cardio entries are `{ min, dist, note }`.

## Rules that keep old data readable
- Move ids (`backsquat`, `pullup`, ...) are permanent. A move that leaves the program moves to `LEGACY_EX`, never deleted.
- Format changes bump `SCHEMA` and add an upgrade step in `upgradeSession`. Upgrades never delete.
- Before any upgrade runs, the app keeps an untouched copy of your data (`ss.snapshot.*`).
- Importing a backup merges it: newer copy of a workout wins, nothing is removed.
