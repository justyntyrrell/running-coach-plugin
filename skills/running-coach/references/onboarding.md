# Onboarding and the profile

This covers the agenda's `onboarding`, `goal`, `ask_once` and `settings` items, **Get started**, and any change the athlete reports to their profile or goal race.

## When onboarding is due

The `onboarding` item is due while `onboarding.done` is false, and its `data.missing` lists what is still unanswered.

- **When it's the whole reply:** the reply to **Get started**, or to a first message that neither asks for anything nor says they ran (a greeting, say), is onboarding.
- **When they asked for something:** answer that first, in full, then begin onboarding in the same reply. That covers a check-in, a question or a run they reported.
- **Urgent things** (pain, illness, a race within two days) always come first.

## Read-back

Say what the history shows, as measured, from `history_coverage`, `training_summary` and `data_quality`:

- **The weeks covered.**
- **Runs and km a week** over the last `last_12_weeks.weeks` complete weeks. Say how many weeks that is.
- **Running days and long-run day:** the days a week they ran (`last_12_weeks.running_days_per_week`), and their long-run day (`long_run_day`; `flexible` means no one day), each when set.
- **The longest run.**
- **Races found:** `analytics.race_candidates.races_known`, when present, counts races flagged in Intervals or confirmed.
  - Give up to three races from `analytics.race_history.races` dated in the last two years, newest first, each with its date, distance and time.
  - These are the only race times onboarding gives. Never give one from `race_candidates` or `race_prediction`.
- **The data problems that matter.**

**Short histories:**
- If `history_coverage.history_start` is set, the history starts there by design: never ask about an import.
- When fewer than 6 weeks are covered, ask their typical weekly km and longest recent run. Without `history_start`, first ask whether a Garmin import is on its way, and ask those two only if it isn't, or they don't know.
  - The answers go to `weekly_km` and `longest_run_km` when `save_athlete_profile` takes them, and to `background` when it doesn't.
  - Ask neither when the profile already gives them.
  - The plan outline starts from these two numbers until 4 weeks are measured (`plan_outline.basis` `reported`).
- When an import is coming, or they don't know while fewer than 6 weeks are covered and `settling_until` is today or later, say the read-back may change as history lands, and plan conservatively. `settling_until` alone is no reason to hedge.

## Questions

- **What to ask:** two or three at a time, and only what `data.missing` lists, plus the goal when there is none:
  - the goal race (**The goal race**, below), where "no race, general fitness" is an answer;
  - running days and long-run day;
  - injuries and limits, where "none" is an answer;
  - schedule constraints;
  - background: years running and recent best times;
  - how they like to be coached;
  - sex and birth year, when the save takes them and `missing` lists them (below).

  What the profile already has is confirmed in the read-back, not asked.
- **Days the history already shows:** when `missing` lists running days or the long-run day and `last_12_weeks` gives it, don't ask for it.
  - Instead, ask once whether the days and long-run day the read-back gave still fit their week. Ask in the same question for schedule constraints when those are missing, and for any value `last_12_weeks` doesn't give.
  - A yes saves the values shown, and a different answer saves theirs.
- **Background:** when the read-back named races, ask how long they've been running, and whether they've run a faster recent time than those.
- **Races not yet known:** when `races_known` is 0 and `race_candidates` lists runs, ask about the first two or three as `references/race-questions.md` says, after the goal race. Those answers go to `confirm_races`, not the profile.

## Sex and birth year

Both are optional. Never press, never ask why, and never infer either from a name, pronouns, pace or anything else.

- **Sex:** ask it plainly, with one sentence on why. Performance standards and most research report results by sex, so it places their level on the right line, and it weighs studies by who was in them.
  - Offer female, male or prefer not to say, and take the answer as given.
  - If neither fits, or they'd rather not say, save `prefer_not_to_say`. With no answer, save nothing.
- **Birth year:** ask the year, never the date, with one sentence on why. Research findings and standards differ by age, and from 40 their level is judged against age-graded standards.
  - If they give an age instead, read back this year minus it, and save that on their yes.
  - If they'd rather not say, save `prefer_not_to_say`.
  - Ask it only in onboarding, or as an `ask_once` item.

## Saving

- **Once:** read the answers back, and on a yes save them all in one `save_athlete_profile` call with `onboarding_complete: true`. Save once at the end, or once when they stop to finish later. Never save field by field.
- **What counts as an answer:** a value the read-back took from the history is saved only on the athlete's yes to it, never because it was shown. Leave out anything not answered, and use `""` only for an explicit none.
- **Skipping:** if they decline or want to stop, ask once whether to finish later.
  - **To finish later:** read back what they answered, and on a yes save it without `onboarding_complete`.
  - **On a skip:** save what they confirmed with `onboarding_complete: true`. The flag alone is accepted.
  - If an earlier chat stopped part-way, ask only for what `missing` still lists.
- **First week:** propose it from `plan_outline`, as `references/plan.md` says, under rule 6.
- **Rhythm:** they run, the Sync happens by itself, and a check-in comes in a new chat. A new goal, an injury or a change of schedule can be told to you any time.
  - With `save_coach_memory`, add that they can tell you how they feel any time, that you keep short notes between chats, and that they can ask what you remember or ask you to forget something.

## Once onboarding is done

- **Get started** gives the read-back with the saved profile and the rhythm, and asks what has changed. It doesn't interview again.
- **`ask_once`** (`data.field`) asks one profile field added since their onboarding. Ask it once, with its why, after what they came for. Save an answer they give, and if they let it pass, leave it.
- **A profile change:** when they report a change to a profile field, save that field on their yes, sent whole. Rule 6 covers this.

## The goal race

- **No goal yet:** with `race_context.state` `awaiting_goal` or `invalid_goal`, coach general fitness from the evidence, and ask for the goal race, its date, distance and any target time.
  - Don't ask when the profile shows a goal, or shows onboarding done without one. The athlete chose general fitness: ask about a race only if they bring one up, or in the weekly review.
- **The `goal` item** (`data.last_goal_date`): their goal race is behind them, so ask whether there's a next one.
- **Saving it:** use `set_goal_race` once the athlete has given the details, asked or not, and in the same way when they change their goal.
  - Never invent a race or a target, and never guess a course or a place the athlete didn't give.
  - When they know them, also save:
    - the distance (needed for `other`);
    - the race's location;
    - its start time;
    - its climb and descent, or `course_activity_id` (a run of theirs on the course).

  The tool's description gives each input's format.

## The settings question

The `settings` item asks an athlete without Intervals to confirm the threshold heart rate their runs give.

- **The estimate:** `coach_context.settings_estimate.lthr` gives `bpm`, its range `low` to `high`, its `basis` (`race`, `threshold_block` or `steady_runs`), the `runs` it rests on and `as_of`. `saved` is what the profile holds now.
- **Why it's due:** `data.reasons` says. `lthr_unset` means nothing is saved, `lthr_outside` means what's saved falls outside the range, and `pace_off` means the saved threshold pace is more than 3% off the Anchor's.
- **How to ask:** give the estimate with its basis and range in one question, with its why: it keeps their effort labels and their load right. Ask whether it fits what they know.
- **With `pace_off`:** also give the Anchor's threshold pace (`threshold_pace`, with its basis) beside the saved one.
- **Saving:** on their yes, save `lthr_bpm`, or the value they give, with `save_athlete_profile`, and `threshold_pace_s_per_km` when they confirm a pace. If they let it pass, leave it.
