# Trail Making Test

A web-based implementation of the Trail Making Test (TMT), a neuropsychological instrument for assessing cognitive processing speed, visual scanning, and cognitive flexibility. The test is built with [PsychoJS](https://github.com/psychopy/psychojs) and is designed to be launched from a survey platform such as Qualtrics.

---

## Task Description

The Trail Making Test consists of two parts that are presented sequentially.

### Part A

Participants are shown 18 numbered targets (1–18) placed randomly on the screen. The goal is to click the targets **in ascending numerical order** as quickly as possible (1 → 2 → 3 → … → 18). A line is drawn connecting each target as it is visited. Part A measures **processing speed and visual scanning**.

### Part B

Participants are shown 18 targets: 9 numbers (1–9) and 9 letters (A–I) placed randomly on the screen. The goal is to alternate between numbers and letters in ascending order as quickly as possible (1 → A → 2 → B → 3 → C → … → 9 → I). Part B measures **cognitive flexibility and executive function** in addition to processing speed.

---

## Trials

The experiment runs **5 trials** in total:

| Trial | Part | Sequence |
|-------|------|----------|
| 1 | A – Trial 1 | Numbers only: 1 → 2 → … → 18 |
| 2 | A – Trial 2 | Numbers only: 1 → 2 → … → 18 |
| 3 | B – Trial 1 | Alternating: 1 → A → 2 → B → … → 9 → I |
| 4 | B – Trial 2 | Alternating: 1 → A → 2 → B → … → 9 → I |
| 5 | B – Trial 3 | Alternating: 1 → A → 2 → B → … → 9 → I |

After each trial the participant's completion time is shown on screen before the next trial begins.

---

## URL Parameters

Session metadata can be supplied via URL query parameters. Any parameter **not** provided through the URL will be requested from the participant via a dialog box at startup.

| Parameter | Description | Example values |
|-----------|-------------|----------------|
| `participant` | Unique participant / subject identifier | `P001`, `sub-42` |
| `group` | Group assignment for the participant | `Control`, `EDS_Treatment` |
| `session` | Session number | `1`, `2` |
| `time_of_day` | Time-of-day code | `0` (morning), `1` (afternoon) |

### Example URL

```
https://example.com/html/index.html?participant=P001&group=Control&session=1&time_of_day=0
```

Passing all four parameters skips the startup dialog entirely so the task begins immediately — useful when launched automatically from Qualtrics or another survey platform.

---

## Results Variables

At the end of each trial the following variables are saved to the experiment data file (CSV):

| Variable | Type | Description |
|----------|------|-------------|
| `trial` | integer | Trial number: `1`=A1, `2`=A2, `3`=B1, `4`=B2, `5`=B3 |
| `session` | string | Session number passed via URL or dialog |
| `time_of_day` | string | Time-of-day code passed via URL or dialog |
| `cumulativetime` | float (s) | Time elapsed since the experiment started (global clock) |
| `result` | float (s) | **Completion time** for this trial (primary performance metric); rounded to 2 decimal places |
| `inter_time` | array of floats (s) | Time at which each individual target was reached, in order |
| `stimulusX` | array of floats | X-coordinates of all 18 target positions (in PsychoJS height units) |
| `stimulusY` | array of floats | Y-coordinates of all 18 target positions (in PsychoJS height units) |
| `stimulusSymbol` | array of strings | Labels displayed on each target (numbers and/or letters), in position order |
| `steps` | array | Step-by-step record of which target was clicked at each stage of the trial |
| `trialMouse.x` | array of floats | Full X-coordinate history of mouse/cursor movements during the trial |
| `trialMouse.y` | array of floats | Full Y-coordinate history of mouse/cursor movements during the trial |
| `trialMouse.leftButton` | array of integers | Left mouse button state at each sample (`0` = up, `1` = down) |
| `trialMouse.midButton` | array of integers | Middle mouse button state at each sample |
| `trialMouse.rightButton` | array of integers | Right mouse button state at each sample |
| `trialMouse.time` | array of floats (s) | Timestamp of each mouse sample, relative to trial onset |

The primary outcome measure is **`result`** (total trial completion time in seconds). The `inter_time` array can be used to compute per-target latencies, and the full mouse trajectory (`trialMouse.*`) supports detailed movement analysis.

---

## Credits & Attribution

This implementation is based on a Trail Making Test project found on [Pavlovia GitLab](https://gitlab.pavlovia.org/). It is unclear who originally created that version first. If this repository is derived from your work, please feel free to contact me so I can add proper credits to you.

The edits to the experiment code and all documentation in this repository were made by [menzynski-biskup](https://github.com/menzynski-biskup).
