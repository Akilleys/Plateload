# Plateload

A single-file gym log that runs on GitHub Pages. No build step, no server, no dependencies beyond Google Fonts.

## Deploy to GitHub Pages

1. Create a new repository (for example `plateload`).
2. Upload `index.html` (and this README) to the root of the `main` branch.
3. In the repo, go to **Settings → Pages**, set **Source** to "Deploy from a branch", branch `main`, folder `/ (root)`, and save.
4. After a minute the app is live at `https://<your-username>.github.io/plateload/`.

## What's inside

- **154 built-in exercises** tagged by primary and secondary muscle, equipment, type (strength, bodyweight, plyometric, cardio), movement (push, pull, legs, core, full body, cardio) and compound or isolation.
- **8 starter routines**: Push, Pull, Legs, Upper, Lower, 5×5 Strength, Full Body Circuit, Core & Conditioning.
- **Workout builder**: pick muscle groups and the equipment you have, choose a rep scheme, generate, swap exercises, then start or save as a routine.
- **Session logging** with last-time hints, set ticking, and PR detection when you finish.
- **Streaks**: consecutive active days, and consecutive weeks hitting your weekly goal.
- **Records**: heaviest set, estimated 1RM (Epley), best session volume, most reps, longest holds, tested maxes, weekly volume chart.
- **Running**: log runs, walks and hikes; weekly distance chart; longest run and pace records for 1 mi, 5K, 10K and half.
- **End-of-day calories**: workouts (MET), runs and walks (ACSM equations) and resting burn (Mifflin–St Jeor).
- **Weekly planner**: assign routines, runs and rest days to each day, see what's done, copy last week, save weeks as reusable plans. Today's plan shows on the Today tab.
- **Routine editor**: build routines from scratch or edit any routine. Editing someone else's routine makes your own remix that credits them.

## Sharing (open source your workouts)

Anything can be shared from the **Share** tab, the Planner, a routine, or a custom exercise, as:

- a **.json file**,
- a **share link** (`https://you.github.io/plateload/#import=PL2...`) that opens the app and imports straight away,
- a **QR code** of that link (when it fits; a single QR code holds about 2,300 characters),
- a **share code** (`PL2.z.…`, the compressed pack) to paste anywhere.

To import, use **Share → Get workouts**: load a file, scan a QR code with the camera, scan a photo or screenshot of a code, paste a code or link, or load a .json from a GitHub link (github.com `blob` links are converted to raw automatically).

Every shared item carries its **author**, a **license** (CC BY 4.0 by default, changeable on the Share tab) and an **update stamp**. Loading a newer version of the same routine or week updates your copy; older or identical copies are skipped. Imported week plans, routines and exercises stay in your library and go into your profile file.

QR codes and scanning load two small libraries from jsDelivr the first time they're used (`qrcode-generator` and `jsQR`). The rest of the app works offline. Phones with the built-in barcode detector (most Android Chrome) scan without the extra library.

To publish a collection, commit pack .json files to a public GitHub repo. Friends load them by link and can send changes back with pull requests.

## Data and files

Everything autosaves in the browser (localStorage). The **profile file** (`.json`) holds the profile, your custom and imported exercises, routines, week plans, your calendar plans, workouts, runs and maxes, so you can back up or move devices. **Routine files** include the exercises they use; importing one adds the routine and any missing exercises to your library.

Profile file shape:

```json
{
  "app": "plateload", "type": "profile", "version": 2,
  "profile": { "name": "", "units": "lb", "distUnit": "mi", "weightKg": 81.6, "heightCm": 178, "age": 30, "sex": "m", "weeklyGoal": 4,
               "authorId": "u-...", "license": "CC-BY-4.0", "shareUrl": "" },
  "library": [ { "id": "c-...", "name": "Viking Press", "muscle": "Shoulders", "secondary": [], "equipment": "Machine",
                 "pattern": "Push", "category": "Strength", "compound": true, "kind": "w" } ],
  "routines": [ { "id": "r-...", "name": "Push Day", "items": [ { "exId": "b-barbell-bench-press", "sets": 4, "reps": 6 } ],
                  "author": { "id": "u-...", "name": "Maya" }, "updatedAt": 1792000000000 } ],
  "weeks": [ { "id": "w-...", "name": "Maya's PPL week", "days": [ [ { "kind": "routine", "routineId": "r-..." } ], [ { "kind": "run", "type": "Run", "km": 5, "note": "easy" } ], [], [], [], [], [ { "kind": "rest" } ] ],
               "author": { "id": "u-...", "name": "Maya" }, "updatedAt": 1792000000000 } ],
  "plans": { "2026-10-19": { "days": [ ... ] } },
  "workouts": [], "runs": [], "maxes": []
}
```

Shared packs use the same pieces: `{ "app": "plateload", "type": "week" | "routines" | "exercises", "version": 2, "name", "author", "license", "weeks", "routines", "exercises" }`. A week pack includes every routine it uses, and routines include any custom exercises. Built-in exercises are referenced by id (`b-...`). Version 1 files from the first release still import.

Weights are stored in kg and distances in km; the app converts for display. `kind` is `w` (weight × reps), `b` (bodyweight reps), `t` (timed hold in seconds) or `c` (cardio minutes and distance).

To add more built-in exercises, edit the `RAW` list near the top of the script: one line per exercise, `name|muscle|secondary|equipment|pattern|category|compound(1/0)|kind|MET`.
