# Reading the data

How to read `coach_context.json`'s `analytics`, and the files beside it. A section read's `about` gives each field's meaning. This file holds what a meaning can't: how far each one can be trusted, and what it must never be used for.

## The analytics

**What they are:** when `availability` is `available`, use these as descriptive evidence:
- the latest activity's features;
- the grade-adjusted baseline comparison;
- the workout comparison;
- the athlete-state components;
- planned-workout coverage.

They are never a diagnosis, a composite readiness score or a prescription. When analytics are unavailable, give the `reason` and read no other analytics file in their place. `analytics.limitations` lists what they can't show.

- **Decoupling:** `decoupling_pct` is never aerobic decoupling. Nothing shows the run was aerobic, and heat isn't separated out.
- **Critical speed:** `critical_speed` is what the last 90 days' efforts *demonstrated*. It is a floor unless one of them was a race or a test. Never prescribe threshold work faster than it, and never make it a race time.
- **Baseline comparison:** `baseline_comparison` is the athlete's own, never a population norm, and hills are already in it.
  - Judge a `residual_median` against the same metric in the other recent runs in `run_detail.json`, not against a fixed cutoff.
  - Heart rate above expectation fits fatigue, illness, dehydration, sun or detraining, and below it fits fitness. The data can't tell these apart, so weigh it with recovery signals and the check-in.
  - Form at matched effort (cadence, ground contact time, vertical ratio, step length): report a deviation that persists across runs, or appears late in one. Never report one run's value alone, and never treat form as an injury signal or a target.
- **Weather:** `analytics.weather.latest` is modelled air at the run's start area, not what the athlete felt. Sun, shade and shelter aren't in it.
  - `provisional` values may still change.
  - `start_cell_only` means the route left the start area.
  - **With the athlete's heat curve applied** (`heat_cost_bpm` above 0), heart rate's `expected_median` already includes heat. Never adjust it again.
  - **With no curve applied,** heat and humidity still raise heart rate at a given pace. Weigh them before reading a high residual as lost fitness.
  - Pace and decoupling are never adjusted for heat, and heat still slows pace at a given effort.
- **Heat:** `analytics.heat` is the athlete's own heart-rate cost of weather. Quote it as theirs only when `verdict` is `supported`.
  - `applied.model` says whether the baselines already take it off (`personal`) or not (`none`).
  - It is heart rate at a given pace, never a race time. What race-day weather adds to the goal is in `analytics.race_prediction`.
- **Effort:** `analytics.effort.latest` shows how the latest run's efforts held up. Use `execution` for rep counts against the plan.
  - One session is one observation. Compare it with earlier sessions of the same kind before calling durability better or worse.
- **Run detail:** for a session deep-dive, read `run_detail.json`, and only when `analytics.run_detail` lists the activity.
  - Judge effort on hills by `grade_adjusted_pace_sec_per_km`, not raw pace. Grades beyond 8% are weakly evidenced.
  - Air temperature and dew point there are the modelled weather, not the device's `temperature_c`.
  - A column absent from a run is unavailable, never zero, and `unavailable_fields` says why.
  - Source detail blocks are not verified laps.
- **Fitness timeline:** for the weekly review, or when asked how fitness compares with the past. Never use it for readiness or a race time.
  - Compare it indicator by indicator, naming which moved which way. Never merge the indicators into one score, and never rank a period best overall.
  - Its paces are demonstrated, so a block without races or hard efforts reads slower than it may be. Critical pace (90 days) and efficiency (28 days) lag.
  - Confirm a candidate peak against the athlete's races before calling it one.
  - Null is unavailable. The weekly rows are in `fitness_timeline.json`, which you read only when this section is present.
- **Race history:** `analytics.race_history` is for taper and race-readiness questions.
  - It describes and never prescribes: compare race by race and name the races. Races under 28 days apart share a `cluster` and count once.
  - Never rank races by 10 km equivalents, and never promise a race time from it.
- **Race candidates:** `analytics.race_candidates` are runs that look like races, but that nobody has confirmed. They are not races.
  - Never count, compare or quote one as a race, and never give a race time from one. Only the athlete's answer makes one a race.
  - A confirmed race counts from the next Sync, not in this chat: say so.
  - How to ask about them is in `references/race-questions.md`.

## The training log

When `analytics.training_log` is present, read `training_log.json` by section.

- **Start with `about`.** Its `generated_at` must equal `analytics.generated_at`. If it doesn't, the log is stale: skip it. `about` also explains every column and code.
- **Labels:**
  - Its anchors, and a run's own `T`, are the threshold pace and heart rate runs are labelled against, never a target.
  - A run's `label` is measured, never read from its name.
  - A low-confidence label (`conf`) is a question for the athlete, not a fact.
  - Across a day in `anchors.jumps`, compare paces, not labels.
- **The rules' inputs:** `coaching_guidance` reads its intensity inputs from the newest completed weeks' rows, which `analytics.training_log.completed_weeks` carries as the file has them.
- **The flags in `recent_days`:** the `quality` flag (steady and progression included), and the `hard` and `easy` flags, are these labels. A run not labelled yet is flagged from its plan, an RPE or its name (`quality_basis` says which), so prefer the log's label.
  - `long_run` is measured against the log's long threshold, so the two agree on long runs. The context times a run by Intervals' moving time, though, and the log by its samples.
  - `athlete_state.days_since_hard_session` and `days_since_long_run` count from these labels.
- **Adding runs up:** read the log for individual runs and weeks, never to add them up (`references/metric-queries.md`).

## Matching runs to plans

- **Matching:** compare matched event and activity ids.
  - Group split recordings linked to one event before judging whether it was completed.
  - Keep doubles separate. A `DUPLICATE_SUSPECT` pair may be one run recorded twice, and it counts twice: ask before calling it a double.
- **Reps:**
  - Never count recoveries, warm-ups or cool-downs as work reps.
  - `execution.blocks` groups laps into efforts, since auto-laps split one rep into several laps.
  - `completed_reps` counts work blocks that match the planned reps within 15%.
  - `work_blocks` counts the work in an unplanned session.
- **Targets and heart rate:**
  - A planned target is not an observed result.
  - Never diagnose controlled heart rate from a sensor-artifact flag or missing heart rate. Check the sensor data before reading it.
  - Missing median heart rate or drift can't be replaced by a lap-average heart rate.
- **Older runs:** for runs older than the calendar's window, the log's `plan` and `verdict` are the comparison. A plan with no matched run doesn't prove it was skipped.
- **Benchmarks:** a benchmark comparison needs a comparable protocol, route, sensor and conditions.

## The athlete's reported background

- **Where it is:** `athlete_model.observed_facts` with `source: "setup intake"` is what the athlete reported, not measured. That covers:
  - running days and long-run day;
  - injuries and limits;
  - schedule constraints;
  - background and best times;
  - coaching preferences;
  - sex and year of birth.
- **Against the history:** prefer the Intervals history once it covers the same period, and name any disagreement between the two.
- **Recency:** `get_athlete_profile`'s `profile` and `goal` are current. `race_context` and these facts are as of the last Sync, which during a first Sync can be a day away.
- **The calendar:** Intervals is authoritative for it. The Sync never writes to it.
