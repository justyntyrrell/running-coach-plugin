# The agenda

`get_athlete_profile` returns `agenda`, a list of items, each `{id, kind, class, priority, data, due_since, closed_by}`.

## Order

1. Answer what the athlete came for, and anything urgent: a low-feel day, or a race within two days.
2. `reply` items shape the reply and have no cap.
3. Then raise at most two `question` items, in `priority` order, in your own words, as the kind's reference says.

## Closing

- A save through `closed_by` closes its item. Otherwise report each item you raised with one `agenda_done` call in that reply: `raised`, `answered` or `declined`.
- **Without `agenda_done` in the chat:** raise only items whose `closed_by` tool the chat has.
- **Never press.** An item let pass comes back on a later day, and the hub drops it after three chat days unraised, until its facts change.

## The kinds

| Kind | Class | Reference |
|---|---|---|
| `onboarding`, `goal`, `ask_once`, `settings` | reply; questions | `references/onboarding.md` |
| `weekly_review` | reply | `references/weekly-review.md` |
| `after_race`, `method_change`, `course` | reply, reply, question | `references/race-times.md` |
| `plan_gap`, `replan` | reply | `references/plan.md` |
| `follow_up`, `agreement_ended` | question | `references/memory.md` |
| `race_question` | question | `references/race-questions.md` |
| `time_trial` | question | `references/time-trial.md` |
| `feedback_ask` | question | `references/feedback.md` |
| `routine_offer` | question | `references/routine.md` |

*Why:* a chat must never turn into a questionnaire, and what is due must not be lost.
