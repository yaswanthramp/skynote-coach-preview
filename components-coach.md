# Coach extensions to the Radix-Design System

Components skyNote Coach needs that the base DS does not define. Each one is derived from the
12-step scale roles in `references/components.md`, lives in the `COACH EXTENSIONS` block at the
bottom of `dashboard.css`, and binds every value to a token.

Nothing here introduces a new colour, font, radius or shadow. Two documented literals exist, both
following an existing DS precedent:

| Literal | Where | Precedent |
|---|---|---|
| `#242424` + `rgba(255,255,255,.x)` | `.player`, `.clip-thumb`, `.phone-shell`, `.phone-status`, `.email-head` | `.app-header.is-dark`. Media chrome must stay dark in both themes; a video surface that inverts to white stops reading as video. |
| `320px` / `600px` / `34px` | `.phone`, `.phone-screen`, `.phone-shell` radius | Fixed device geometry, the same way `.table td` fixes one row height. |

---

## `.rangebar` — the signature component

A value drawn against the band it should sit in. This is the one thing Coach could not assemble
from stock parts, and it appears on every metric on every screen.

```html
<span class="rangebar">
  <span class="rb-track"></span>
  <span class="rb-ideal" style="left:0%;width:30%"></span>   <!-- optional -->
  <span class="rb-bench" style="left:0%;width:23%"></span>   <!-- team screens only -->
  <span class="rb-base"  style="left:45%"></span>
  <span class="rb-you is-miss" style="left:57%"></span>
  <span class="rb-cap is-start">0</span>
  <span class="rb-cap is-end">6 / min</span>
</span>
```

| Part | Role | Token |
|---|---|---|
| `.rb-track` | the metric's full scale | `--gray-4` (step 4, UI element background) |
| `.rb-ideal` | the healthy band | `--green-3` fill on an inset `--green-7` hairline |
| `.rb-bench` | top-quartile profile, team screens only | `--blue-2` between `--blue-8` dashes |
| `.rb-base` | your own 30-day baseline | `--gray-9` (step 9, solid) |
| `.rb-you` | this meeting's value | `--green-9` / `--orange-9` / `--red-9` by status, ringed in `--color-panel-solid` |
| `.rb-cap` | scale ends | `--fg-subtle`, `--font-mono`, `--fs-1` |

**Status is never carried by colour alone.** Every row that shows a range bar also shows a
`.badge.is-success` / `.is-warning` / `.is-danger` reading *In range*, *Edge of range* or
*Outside range*. `.rangebar-legend` names all four marks wherever bars first appear on a screen.

Amber is deliberately absent: it stays brand, so a red marker never competes with a brand accent.

## `.metric` — expandable metric row

A native `<details>` so the row is keyboard operable with no JS. `summary` is a three-column grid
(name and definition, range bar, value plus delta plus status badge plus chevron). `.is-flagged`
swaps the inset ring to `--red-7`; `[open]` swaps it to `--accent-8` plus `--shadow-2`. One row
open at a time per `.metric-list`, enforced in script.

## `.moment` — playable evidence row

`32px` play button, monospace timestamp in `--accent-11`, transcript text in `--table-fg`, actions.
`.moment-play` inverts to `--accent-9` with `--accent-contrast` on hover, matching the DS
`.list-item` solid-highlight convention. `mark` inside the text tints with `--accent-3`.

## `.rec` — recommendation card

`--accent-2` fill on an inset `--accent-6` ring. Brand tint rather than a status tint, because a
recommendation is the product's voice, not a state. `.rec-rank` is a solid `--accent-9` chip with
`--accent-contrast` text. `.ev-chip` is the clickable evidence pill: surface fill, inset
`--accent-7` ring, monospace timestamp.

## `.crit` — scorecard criterion

Four-column grid matching a bordered `.card`. `.is-lost` swaps to a `--red-7` ring. The answer
control is the stock `.segmented` (yes/no, or 1 to 5): both are exclusive choices, which is what a
segmented control is for, so no new control was invented.

## `.cmt` / `.thread` — coaching comment

`--gray-2` bubble on an inset `--border-subtle` ring; `.is-coach` switches to the `--accent-2`
brand tint so a manager's note is distinguishable from a rep's reply. The thread rule is
`--accent-6`.

## `.streak` — goal streak cells

`26x28` cells tinted `--success-bg`, `--danger-bg` or `--gray-3`. Contents are Lucide `check`, `x`
and `minus`, never a text glyph.

## `.share-row`, `.player`, `.phone-*`, `.email-*`, `.notes-drawer`

Layout scaffolding for the speaker-share list, the recording surface, the device frames, the
digest preview, and the design-notes drawer. The drawer is review chrome, not product.

---

## Base-DS fixes applied in the same block

- `.table .cell-sub { display:block }` — `rules.md` S14, the stacked title and subtitle
  run-together. Without it, "Dana Whitmore" and "the admin setting is off" render on one line.
- `.segmented-item, .seg-tab, .badge { white-space:nowrap }` — a wrapped label breaks the 28px
  segmented track.
- `.app-content > .view:not([hidden])` — the SPA view must fill the content column so the footer
  pins to the bottom, without out-specifying the DS `.view[hidden] { display:none }` rule.

---

## Part 2: CRM layer components

Added for My Discovery and the improvement drills. Same rule as part 1: every value binds to a
token in `tokens.css`, and nothing here overrides a base component.

### CRM gating, `[data-crm-only]` / `[data-nocrm-only]`

The root element carries `data-crm="on"` or `"off"`. Anything that only exists once a CRM is
connected is marked `data-crm-only`; its unconnected counterpart is `data-nocrm-only`. One
attribute drives the My Discovery nav item, the Prospect column on Conversations and the sales
coaching panel on a meeting, so a screen cannot drift out of sync with the navigation.

The artifact host supplies its own `<html>`, so the JS sets the default attribute on load rather
than relying on it being in the page source.

### `.drill` and `.drill-block`

How to improve, on My Coach. A drill is a named technique (`.dr-name`), the metric it fixes
(`.dr-what`), and a cue (`.dr-cue`) short enough to hold in your head mid sentence. The cue sits
on a panel surface with an inset hairline so it reads as the quotable part. Icon tile uses
`--accent-3` on `--accent-11`, matching `.sc-icon` geometry.

### `.prompt` and `.grounded`

A Discovery Coach prompt: what to say (`.pr-say`), what it is for (`.pr-learn`), the CRM record it
came from (`.grounded`, blue-3 on blue-11, deliberately the team-data blue rather than the brand
amber), and Used / Discard. `.prompt.is-used` fades to 55 percent and strikes the text, so a
counselor working down the sheet can see where they are.

### `.say-aloud` and `.ask-card`

`.say-aloud` is the block the counselor reads out: gray-2, inset hairline, italic, wide measure.
`.ask-card` is the one control on the sheet that writes back to the CRM, so it is the only block
tinted `--accent-2` on an `--accent-6` ring, and it carries the single `.btn-solid`.

### `.feed` and `.feed-item`

The activity feed. Type is carried by icon plus label, never colour alone. Tours tint the icon
tile amber, notes tint it blue, everything else stays gray-3.

### `.stages` and `.stage`

The CRM pipeline. Completed stages are green-3, the current stage is the solid amber pill with
`--accent-contrast` text (the same treatment as the active nav item), and future stages are
gray-3. Numbered because the pipeline genuinely is a sequence.
