# skyNote Coach, UX design

Live preview: **https://yaswanthramp.github.io/skynote-coach-preview/**

skyNote Coach turns a recorded meeting into private, measured feedback on how you communicate,
and into a scorecard a sales team can coach against. This is the UX design for it: twelve screens
in one interactive shell, covering FR-1 to FR-16 of the functional requirements.

Designed by Yaswanthram Ponnada. Built in the Radix visual language, Radix Colors 12-step scales
and Radix geometry, tinted with Skypoint amber and set in Inter.

All figures, people and accounts are illustrative sample data.

## The method

See a number, then hear yourself say it. Every metric on every screen is one click from the
seconds of audio that produced it. A metric with no moment behind it is an opinion, and Coach
never shows one.

## Getting around

The sidebar switches screens. Design notes for the screen you are on open from the header, next
to the theme toggle. Metric rows expand to reveal the moments behind them. Light and dark are
both supported.

| Nav | What is on it |
|---|---|
| Conversations | The meeting list, plus three meeting sub screens: the Coach tab, the states before a number exists, and one metric drilled into its ten moments |
| My Coach | Trends, one metric in depth, goals and streaks, and the drills that say how to improve each pillar |
| My Discovery | Prospects from the CRM, the Discovery Coach prompt sheet for the next tour, the logged activity behind it, and counselor notes |
| Clip library | Promoting a moment into shared teaching material |
| Settings | Who can see what, ideal ranges, modules and rollout |
| Design review | This index, and the mobile and e-mail screens |

## The two variants

My Coach is identical for everyone. My Discovery only exists once a CRM is connected. The banner
carries a switch between the two states, so you can see both without a rebuild.

| | No CRM | CRM connected |
|---|---|---|
| My Coach | Trends, one metric, goals and streaks, plus improvement drills | Same, unchanged |
| My Discovery | Not in the nav | Prospects, Discovery Coach, Activities, Notes |
| Conversations | No Prospect column | Prospect column, auto matched on the calendar invite |
| Meeting Coach tab | Communication coaching only | Plus what the conversation was for, coached against the prospect record |

Scorecards and Team Coaching are parked for this round, not deleted.

## Requirements coverage

| | | Screen |
|---|---|---|
| FR-1 | Knowing which speaker is you | Meeting, states |
| FR-2 | The fifteen metrics and their ranges | Meeting Coach tab, Settings |
| FR-3 | The per meeting Coach card | Meeting, Coach tab |
| FR-4 | Moments, playback behind every metric | Meeting, filler rate |
| FR-5 | Trends | My Coach |
| FR-6 | Recommendations | Meeting Coach tab, My Coach |
| FR-7 | Goals and the practice loop | My Coach |
| FR-8 | Weekly coaching digest | Mobile and e-mail |
| FR-9 | Scorecards | Scorecard templates, Meeting Scorecard |
| FR-10 | Manager coaching workflow | Team Coaching |
| FR-11 | Leaderboards and benchmarking | Team Coaching |
| FR-12 | Best practice clip library | Clip library |
| FR-13 | Keyword and topic tracking | Team Coaching |
| FR-14 | In person capture | Mobile and e-mail |
| FR-15 | Administration | Settings |
| FR-16 | Privacy | Settings, plus a callout on every screen showing personal data |

## Design principles

1. **See, then say.** Every number is one click from the audio that produced it.
2. **A value is meaningless without its range.** The range bar carries the ideal band, your value,
   your 30-day baseline and, on team screens, the top-performer band. Status is written in words
   as well as colour, so nothing depends on colour alone.
3. **Private until proven otherwise.** Personal Coach data carries a lock. Team data carries a
   blue callout naming its audience. The two are never mixed on one card, and the disclosure
   appears before the first metric exists.
4. **Three recommendations, three goals.** Fifteen metrics shown flat is a wall. Misses sort to
   the top, advice stops at three, goals stop at three.
5. **Say why, in the user's words.** Every failure state names its cause. Every AI grade carries
   one sentence of justification, the moments behind it, and a human override that wins.
6. **Never a performance rating.** No composite rep score, no ranking without an explicit metric,
   no HR surface. The manager's page states what it cannot show.

## Deliberately out of scope

No real-time in-call nudges, Coach is post-meeting. No role-play or practice simulator. No model
other than Gemini. No performance-management surface.

## Files

- `index.html` — the prototype, self-contained apart from the two stylesheets and Google Fonts
- `dashboard.css`, `tokens.css` — the design system, plus a documented Coach extensions block
- `components-coach.md` — spec for every component added on top of the base system
