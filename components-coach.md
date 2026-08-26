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
