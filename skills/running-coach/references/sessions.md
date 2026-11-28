# Choosing the sessions

This applies when `references/plan.md` composes a week with hard sessions in it, and the connector's `get_runs` takes a `label`, or `app_tools.missing_args` in the profile names `get_runs`' `label` (the athlete's app holds an older list). In that second case, open each label's runs by date: its `last` date in `session_record.families`, and the dates of its earlier runs from `training_log.json`. Say once that the app needs its tool list refreshed, as `app_tools` says. Otherwise, compose as `references/plan.md` says and leave this reference out.

The outline says how many hard sessions a week holds and the stage's rules say which domains it covers. This reference says which session each hard day gets and how it moves on from the last one, from what the athlete's own runs showed. You judge the runs; `check_week` holds the week to its bounds.

- **The record:** `plan_outline.session_record` holds counts and dates, no sessions:
  - `stage`, and `since`, the Monday it began
  - `families`: for each training-log label run in the last 26 weeks, its `last` date, `days_since` and `stage_count`
  - `covers`: each label the stage's `rule` covers, `done` once it ran this stage, else `not_yet`
  - `double_threshold_days` (`count`, `last`)
  - `threshold_28d` (`runs`, and their `verdicts`)

  With `session_record` null, there are no labelled sessions yet: build from the shapes in `plan_outline.sessions.kinds` and say there are no past sessions to build on.
- **Opening the runs:** before you choose a hard day's session, open the last runs of each label you might use with `get_runs` and `label` (`threshold`, `intervals`, `steady`, `long`, `race`…): 3 to 5 is usually enough, with `since` set to the stage's `since` for this stage alone. Every row has its `work` (e.g. `5x1.6k @3:25 (T+1%) r1:00 jog`), its plan verdict, the athlete's effort and feel marks and note, and, on a quality run, its `facts`:
  - `reps`: each rep's pace in s/km and heart rate
  - `fade_pct`: the last third of the reps against the first third, + when they slowed
  - `vs_last`: heart rate in bpm and pace in % (- faster) against the last session of that label in the same band, and its `date`
  - `next_easy`: the next day's easy run against the 28-day easy median, heart rate and grade-adjusted pace, and its feel
  - `pm_vs_am`: on a double day's evening run, its heart rate and pace against the morning's

  A missing fact was not measured: say so, and judge from the rest.
- **The one to build on:** a label holds several formats (5x1 km, 8x2 min and 3x8 min can all be `threshold`). A session moves on from the last run of its own format: the same rep length, give or take a minute, and the same kind of recovery. Read the label's latest run too, when it is another format: if it faded or its heart rate drifted, repeat this format rather than move it on. Name both in the session's line when they differ.
- **S sessions:** the log has no `sub_threshold` label. A past S session is labelled `steady` or `threshold`, by its pace: build on the last of either whose `work` pace sat inside or near `plan_outline.paces.bands.S`. With none, say it is the first S session.
- **Reading a session:** read each run as a whole, with its heat, hills, sleep and note:
  - **held:** reps even, heart rate steady or lower than `vs_last`, felt fine. Move it on one step.
  - **faded, or heart rate drifted up** with nothing around it to explain it: repeat it as it was.
  - **cut short or missed:** step back to the last session that held.

  These readings are yours, not the pipeline's: it publishes what a run showed and never a verdict on it.
- **Moving a session on:** one change at a time, in this order: longer work at the same pace (more reps, or longer ones), then shorter recoveries, then a faster pace inside the band. A session that held is never repeated unchanged, and a session that didn't is never moved on. There are no fixed step sizes: keep a step small enough that the session still looks like the one the athlete ran.
- **Choosing each hard day's kind:** take the hard sessions the outline's week holds and give each a kind from `plan_outline.sessions.kinds`:
  - A label `not_yet` in `covers` is covered before the stage's last week: `check_week` warns on that week if it still isn't.
  - The stage's rules say the rest: threshold and intervals while building, goal pace in sharpen, sessions kept short and sharp in the taper.
  - Inside that, give the session the athlete ran most and ran well (`stage_count`, the `families` with recent `last` dates), in a format they know.
  - A domain the athlete avoids (no `last`, or a `days_since` far longer than the others) comes in its easiest version, with one line saying why: "intervals: none since May, and this stage's rule covers them; 5x3 min to start".
- **Structure:** write any structure inside its kind. The bounds per kind are in `references/plan-defaults.md` (`<kind>_structure`: rep, recovery and total work minutes), and `check_week` warns past them. These are examples, not a list to choose from:
  - **threshold** (T): 5x6 min r1 min, 3x10 min r2 min, 2x15 min r3 min, 20 to 30 min continuous
  - **sub_threshold** (S): 10x3 min r1 min, 6x5 min r1 min, 4x8 min r1 min
  - **intervals** (I): 5x3 min r2 min, 4x4 min r2 to 3 min, 6x2 min r2 min
  - **repetition** (R): 8x200 m r200 m jog, 6x400 m r400 m jog
  - **marathon_pace** (M): 3x5 km r1 km, or 10 to 16 km of M in the long run
  - **race_specific:** goal pace in blocks, from `analytics.goal_pace` (`references/paces.md`)
- **Quoting the facts:** each hard session you propose says in one line which run it builds on and what that run showed: "Thursday 6x6 min T: your 5x6 min on 11-12 held (fade 0.4%, heart rate 3 below the 10-28 session), so one more rep". Quote the facts from the row: fade, heart rate against `vs_last`, never just "controlled". With no run of that format yet, say it is the first.
- **Never a cause:** say what the runs showed, never why a result came. Never say an athlete responds best to a kind of session, and never call anyone a responder or a non-responder: one runner's log can show what each session did, not what made them fitter.
- **Double threshold:** asked for double threshold, or for a week that holds it, a double day is two hard sessions on one date, both `threshold` or `sub_threshold`, the morning with `part` `am` and the evening `pm`. It counts as one hard day, and the week's km hold both runs.
  - **Readiness:** read `session_record.double_threshold_days` and `threshold_28d` first. With past double days, build on the last one (`get_runs` with `label` `threshold` and `double`). With neither a double day nor a threshold run in the last 28 days, `check_week` returns `double_threshold_readiness`, a hard bound: push back as **Past a bound** in `references/plan.md` says, and offer single threshold sessions first. Its soft warnings (`double_threshold_week_km`, `_run_days`, `_days`, `_first`) each name their basis: show them in one line each.
  - **The two sessions:** the morning in S, the evening in T and no faster than T's fast edge; both well under their total-work bounds. Write "At least 6 h after the morning run." in the evening workout's text: the calendar holds no start time, so nothing checks the gap.
  - **Afterwards:** read the evening run's `pm_vs_am`. Heart rate higher in the evening at a matched pace means the morning ran too fast: next time, the morning slower in S. Watch the next two days' easy runs (`next_easy`) before the next hard day.
