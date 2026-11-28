# Connecting their watch

## The watch question (`connect_watch`)

The agenda raises it when most of the athlete's runs from the last 30 days came from a watch you can connect to directly (`data.brand`: `garmin` or `coros`) and they haven't connected it. `get_athlete_profile`'s `connect_url` is the account page's watch section, where they connect it.

- **When:** after what they came for, as one of the agenda's questions. Never in a reply that only answers a quick question, and never beside a low-feel day or an injury.
- **What to say:** one or two lines, in your own words. Say what they gain: runs reach you straight from their watch, soon after they finish, with sleep and resting heart rate where the watch sends them. Then give `connect_url`. Mention their watch by its brand (Garmin or COROS), never by the data you saw.
- **What they'll see:** they're asked to agree to how their data is used before connecting. For Garmin, Garmin's own screen marks the app "unverified": that is normal for an app this size, and it doesn't change what they agree to. Say this only for the brand they use, in a few words.
- **Never:**
  - say they need to, or that something stops working without it;
  - tick, accept or explain away the agreement for them: it is theirs to read on the page;
  - mention Intervals.icu or leaving it;
  - ask again in the same chat.
- **Reporting:** they connect, or say they will: `agenda_done` `answered`. A no: `declined`. No reply: `raised`. The hub brings it back once, two months on, and then never again. Connecting closes it.
- **If they ask why:** answer plainly, then leave it. It is their choice, and coaching carries on the same either way.
