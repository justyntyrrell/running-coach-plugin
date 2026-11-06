# The weekly review

This is the agenda's `weekly_review` item, and any Sunday check-in. It's a check-in (rule 9) that looks back on the complete week and agrees the next one.

## Looking back

- **The weeks:** `weekly_review` is the last complete Monday-to-Sunday week. It ends on the previous Sunday, so a partial current Sunday is never mixed into it. Beside it, give the current week to date, labelled as such.
- **What to review:**
  - actual, required and optional km;
  - 28-day volume;
  - quality completed;
  - the long run;
  - recovery;
  - doubles;
  - explicit decisions;
  - upcoming key sessions.
- **The training log:** with `analytics.training_log`, set the week's sessions, `easy_pct`, long-run share and hard days from its `recent` weekly row, beside the four weeks before. Take the earlier weeks from the month sections when `recent` holds fewer than five.
- **A plan decision:** with `weekly_review.plan_decision`, open by setting the reviewed week beside it: the direction and km decided, and the km done. This is kilometres only, so a change made only to intensity doesn't show.
- **The week plan in memory:** with `memory`, set the current week to date beside `memory.week_plan.this_week`.
- **The coach's own changes:** `weekly_review.coach_changes` lists them, logged from `since`. Say which were followed and how the sessions went. A `pending` `verdict` means no run is linked yet, not a skip.
  - `calendar_changes` lists the calendar's changes since the previous Sync: added, modified and removed.
  - `coach_change` is set on the coach's marked edits and null on the athlete's own.
- **Fitness across weeks:** use `analytics.fitness_timeline` as `references/reading-the-data.md` says.

## Race ranges

With `analytics.race_prediction`, set its ranges beside last week's, as `references/race-times.md` says under **In the weekly review**. A due race question is the agenda's `race_question` item (`references/race-questions.md`).

## Looking ahead

- **The decision:** decide whether the coming week stays the same, goes down or goes up, and explain the evidence.
- **The outline's week:** set `plan_outline.weeks[1]` and `weekly_review.next_week_direction` beside the reviewed week and the athlete's decision (`references/plan.md`).
- **Saving it:** with `save_coach_memory`, once the athlete agrees whether to keep, decrease or increase, save it as `week_plan` for the coming Monday. That save closes this item. Include the direction, the reason, and a km target only if they agreed one.
