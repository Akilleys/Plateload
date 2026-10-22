# Plateload

A single-file gym log that runs on GitHub Pages. No build step, no server, no dependencies beyond Google Fonts.

## What's inside

- **154 built-in exercises** tagged by primary and secondary muscle, equipment, type (strength, bodyweight, plyometric, cardio), movement (push, pull, legs, core, full body, cardio) and compound or isolation.
- **8 starter routines**: Push, Pull, Legs, Upper, Lower, 5×5 Strength, Full Body Circuit, Core & Conditioning.
- **Workout builder**: pick muscle groups and the equipment you have, choose a rep scheme, generate, swap exercises, then start or save as a routine.
- **Session logging** with last-time hints, set ticking, and PR detection when you finish.
- **Streaks**: consecutive active days, and consecutive weeks hitting your weekly goal.
- **Records**: heaviest set, estimated 1RM (Epley), best session volume, most reps, longest holds, tested maxes, weekly volume chart.
- **Running**: log runs, walks and hikes; weekly distance chart; longest run and pace records for 1 mi, 5K, 10K and half.
- **End-of-day calories**: workouts (MET), runs and walks (ACSM equations) and resting burn (Mifflin–St Jeor).

## Data and files

Everything autosaves in the browser (localStorage). The **profile file** (`.json`) holds the profile, your custom and imported exercises, routines, workouts, runs and maxes, so you can back up or move devices. **Routine files** include the exercises they use; importing one adds the routine and any missing exercises to your library.

Profile file shape:

```json
{
  "app": "plateload", "type": "profile", "version": 1,
  "profile": { "name": "", "units": "lb", "distUnit": "mi", "weightKg": 81.6, "heightCm": 178, "age": 30, "sex": "m", "weeklyGoal": 4 },
  "library": [ { "id": "c-...", "name": "Viking Press", "muscle": "Shoulders", "secondary": [], "equipment": "Machine",
                 "pattern": "Push", "category": "Strength", "compound": true, "kind": "w" } ],
  "routines": [ { "id": "r-...", "name": "Push Day", "items": [ { "exId": "b-barbell-bench-press", "sets": 4, "reps": 6 } ] } ],
  "workouts": [], "runs": [], "maxes": []
}
```

Weights are stored in kg and distances in km; the app converts for display. `kind` is `w` (weight × reps), `b` (bodyweight reps), `t` (timed hold in seconds) or `c` (cardio minutes and distance).

To add more built-in exercises, edit the `RAW` list near the top of the script: one line per exercise, `name|muscle|secondary|equipment|pattern|category|compound(1/0)|kind|MET`.
