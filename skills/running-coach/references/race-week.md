# Race week

This covers the agenda's `race_week` and `race_final` items and any time the athlete asks for a race plan, splits or what to do on race day. Race times themselves follow `references/race-times.md`.

## The items

- **`race_week`** (`data.goal_date`): 7 to 3 days before the goal race. Give the briefing (below), then ask the logistics questions.
- **`race_final`** (`data.goal_date`): 2 days before to race day. Give the splits on the latest forecast and the race-morning notes. If `race_week` was never raised, give the whole briefing here.
- Report each with `agenda_done` once given. A save through `set_goal_race` doesn't close them.
- **Asked any other time,** give the plan as it stands: further out than 14 days its weather is the usual weather for the date (`goal.weather.source` `climatology`), so say it will change.

## The briefing, in this order

1. **The target and its odds.** `analytics.race_plan.target_kind` says where the target came from:
   - `median`: none chosen yet. Ask, with a default: "Your data says a typical day is `p50_s`; your goal of `goal_time` has odds of about 1 in N. Which do you want to race?" (`references/race-times.md` for the odds). Plan for the median meanwhile. A realistic target goes with a better marathon (`pred-pacing-realistic-target-time`).
   - `chosen` or `goal_time`: the time they chose; name it.
   - **Saving their choice:** `set_goal_race` with `race_target` (h:mm:ss) and every other field of the goal race exactly as `get_athlete_profile` shows it, since the call replaces the whole goal. It reaches the plan at the next Sync.
   - **`target_outside_range`:** warn once, with its odds, that going out at that pace risks slowing badly late on (`pred-pacing-hitting-the-wall-share-and-cost`), offer the nearest time inside the range, then plan for what they choose. They have the final say.
2. **The splits.** Quote `analytics.race_plan.segments` as published: `km` for metric, `mi` for imperial (`units`). Never work out a split, pace or clock time of your own.
   - A table: each segment, its split, the clock at its end (the sum of the splits to it), and ▲ or ▼ for a `grade` of `up` or `down`. The last row is the part km or mile to the finish.
   - **Even effort, not even pace:** the splits slow on climbs and quicken on descents so the effort stays even. Say so when any segment climbs. No pacing strategy beats even, self-judged effort, and a fast start costs more than it saves (`pred-pacing-no-imposed-strategy-beats-self-pacing`, `pred-pacing-marathons-mostly-positive-split`).
   - **`hills_not_placed`:** the splits are even because the hills aren't placed. Say so, and offer to place them: the course file (**Finding the course file**, below), or a run of theirs on the course (`course_activity_id`).
   - **`course_length_off`:** the course run differs from the race distance and was stretched to it; say the climbs' places are approximate.
3. **The weather.** `goal.weather` as `references/race-times.md` says. The heat is already in the target and spread evenly over every split.
4. **The taper.** The days left and what they hold, from `plan_outline`.
5. **Fuelling.**
   - For a race expected to last over about 90 minutes: eat more carbohydrate than usual for the day or two before, made concrete as meals and snacks, since runners who think they have loaded often have not (`fuel-carb-load-helps-events-over-90-min`, `fuel-carb-load-marathoners-eat-too-little`). For a shorter race, normal eating is enough.
   - A familiar carbohydrate breakfast a few hours before a long race, practised before long runs (`fuel-prerace-meal-helps-prolonged-exercise`).
   - During the race, carbohydrate by its duration, as they've practised it (`fuel-race-carbohydrate-scales-with-duration`, `fuel-train-the-gut`). Turn it into their own gels only when they name them.
   - Speak in meals and gels, never grams per kg of body mass. Caffeine only if they ask (`references/guidance.md`).
6. **The warm-up** (`race_final`, or asked).
   - A 5K or 10K: easy jogging, then a few short efforts near race effort, finishing about 10 minutes before the start (`taper-warmup-high-intensity-5k-time-trial`, `taper-warmup-priming-hard-needs-9min-recovery`).
   - A half or marathon: little more than easy jogging, nothing that tires or heats them, and warm clothes through a long wait at the start (`taper-warmup-endurance-avoid-fatigue-heat`, `taper-warmup-easy-jog-no-clear-gain-30min-run`). No trial has tested a warm-up for these distances: say it is a sensible default.
   - Stretching, if they like it, kept brief (`taper-warmup-stretching-no-running-economy-effect`).
7. **The logistics questions** (`race_week` only, at most two): the start time, if `get_athlete_profile` has none (save it as `start_time`), and the gels or drinks they've trained with.

End the notes with a `Basis:` line naming the claim ids behind them. Say nothing on fuelling, warm-up or pacing that no claim here backs.

## Finding the course file

With `set_race_course` in the chat, and the goal race's course not yet a file or a run of theirs (`goal.course` is not `course_gpx` or `course_activity`):

1. **Offer once:** "I can look for the official course file so your splits slow on the climbs. Want me to?"
2. **On their yes, look for it** with your own web search, if this app gives you one: the race's own site first (its course map or a download page offering a `.gpx` file), then a route the organiser links on a mapping site whose export opens without a sign-in. Never a stranger's recording of the race, and never a file for another year's course if the course changed.
3. **Show what you found before saving:** the race, the year, where the link is from, and the link itself. Save it with `set_race_course` only on their yes.
4. **Without a search,** or when none turns up, ask the athlete to find the course page and paste the link to its `.gpx` file. A page about the course is not the file. They can also give its total climb and descent (`set_goal_race`).
5. **The reply** gives the file's length beside the race distance. Further off than a course file usually is: say so, and ask whether it's the right course.

The file reaches the splits and the race-time range at the next Sync. A new goal race needs its own.

## A race that isn't the goal race

Asked for splits for a tune-up race, give even splits from its Race-today range in the chat (`references/race-times.md`), and say why they're plain: no course or weather is priced for it, and no plan is kept.
