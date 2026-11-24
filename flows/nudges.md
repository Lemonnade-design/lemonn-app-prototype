# Flow: Overtrading nudges (playground) (`nudges`)

> One self-contained file for converting this flow to another platform. Read https://lemonnade-design.github.io/lemonn-app-prototype/CONVERT.md first. Design system: Lemonnade V3 @ `ed10506` (components, tokens and rules: https://lemonnade-design.github.io/lemonnade-v3-docs/llms.txt).

Journey-aware P&L limit and TP/SL prompts: silent help on the order pad, and one nudge sheet when the revenge flag and the journey engine agree.

Prototype: https://lemonnade-design.github.io/lemonn-app-prototype/#/nudges · machine-readable: https://lemonnade-design.github.io/lemonn-app-prototype/flows/nudges.json

## Screens

| Id | Screen | Figma | Taps go to | Note |
|---|---|---|---|---|
| `nudges-01` | Order pad · silent help | [8671:18433]() | — | The default — no interruption. The F&O commodity order pad (fno-25) as it is, plus silent help: “Set TPSL” becomes a TP/SL row, pre-filled and on (Target +20% · Stop-loss −10%); “Set a loss limit for today” is the first line of the dock. Buy fires the nudge picked in the settings (Case, Data state), once: the shared cap is 1 per session. |
| `nudges-02` | Nudge · from settings | — | — | The one nudge sheet — the risk meter — filled by the case and data state picked in the settings. Pills on the floating switcher: Meter (4f Soft dial · 4g Blocks), Risk level, Meter layout, Meter fill, Case, State. |
| `nudges-03` | Nudge · generic | — | — | Fires on Positions with the revenge flag when no single behaviour stands out, or the trader is too new to compare (state D). The meter and its own fact under it. Dismiss says just “Not now” (no order in hand). |
| `nudges-04` | Nudge · size-up · A (own loss) | — | — | Size-up after a loss, own history and last loss (A): the meter at high risk, “You are placing a bigger order right after a loss”. |
| `nudges-05` | Nudge · orders today · B | — | — | Orders today, own history (B): the meter, and the fact “3X more orders than usual today” under it. |
| `nudges-06` | Nudge · orders today · C (thin history) | — | — | Too few past sessions for “your usual”: the fact under the meter is today’s raw fact (“14 orders today”), no multiple. |
| `nudges-07` | Nudge · averaging down (TP/SL first) | — | — | Averaging down: the main button is TP/SL; the fact under the meter is the case\ |
| `nudges-08` | Set today’s loss limit | — | — | From the nudge’s “Set a loss limit for today” or the order pad dock. Pre-filled ₹25,000, quick amounts as pill tabs. Set limit → back to the pad with the limit shown. |
| `nudges-09` | TP/SL for this order | — | — | From the nudge’s “Add TP/SL to this order” or the TP/SL row. Target and stop-loss in %, the exit price under each. |
| `nudges-10` | Order pad · limit set | — | — | Silent help once a limit exists: “₹25,000 left of today’s loss limit” with a bar in the dock (tap to change it). |
| `nudges-11` | Order pad · close to the limit | — | — | ₹21,000 of ₹25,000 used: the bar and the line turn warning. Still no interruption. |

## Spec (README.md)


> PLAYGROUND, not a shipped flow. The product team's draft (2026-10-30, `playground/overtrading-nudges/README.md`),
> redesigned in L3 so the idea can be shown and tested. No Figma yet. Every number in the copy is an example; the real
> values are computed per trader.

- **Prototype:** `#/nudges` · single screen: `#/nudges-02` (the nudge, driven by the settings)
- **Status:** 🟨 exploration · last updated 2026-10-30
- **Entry:** the F&O commodity options order pad (`fno-25`, copied into this flow) · **Exit:** back to wherever the order pad came from

### The idea in one line

When an F&O trader starts chasing a loss, the app shows one short sheet at the moment of the order, with one fact
about today and one reason, and offers a loss limit for the day or a TP/SL on this order. He can always skip it.

### Screens

Each screen is the order pad in one state; within a screen, sheets swap over the same page. Screens 03–09 open with
their own case; changing Case or Data state in the settings switches the open sheet to the pick on any screen.

| Id | Screen | What it shows / when |
|---|---|---|
| `nudges-01` | Order pad · silent help | Default. TP/SL on and pre-filled, "Set a loss limit for today" in the dock. Buy fires the nudge from the settings, once. |
| `nudges-02` | Nudge · from settings | The nudge sheet for any case (17) × data state (A / B / C) and the button variant. |
| `nudges-03` | Nudge · generic | Fires on Positions: nothing stands out, or the behaviour can't be scored (state D). No bars. |
| `nudges-04` | Nudge · size-up · A | Bars: the trade he lost vs this order; line = his own last loss (red strip). |
| `nudges-05` | Nudge · orders today · B | Bars: his usual day vs today; line = the group (7 in 10 lost more). |
| `nudges-06` | Nudge · orders today · C | No "usual" yet: headline = today's raw fact, no bars. |
| `nudges-07` | Nudge · averaging down | A TP/SL-first case whose fact isn't a multiple: no bars. |
| `nudges-08` | Set today's loss limit | Amount field + quick amounts. |
| `nudges-09` | TP/SL for this order | Target / stop-loss % with exit prices. |
| `nudges-10` | Order pad · limit set | "₹25,000 left of today's loss limit" + bar. |
| `nudges-11` | Order pad · close to the limit | Bar and line in warning. |

### Navigation

```
nudges-01 ──Buy (1st time)──▶ nudge sheet ──Not now, place order──▶ order placed (toast)
                                 ├──Set a loss limit──▶ nudges-08 ──Set limit──▶ nudges-10
                                 └──Add TP/SL──────────▶ nudges-09 ──Save──────▶ pad, TP/SL on
nudges-01 ──Buy (again)──▶ order placed (cap: 1 nudge per session, 2 per day, shared by every nudge)
           (prototype setting "Show on every Buy", on by default: the nudge fires on every Buy / Sell, to demo it; off = the real cap)
```

### The nudge sheet — the risk meter (one template, every case)

Cut down on 19 Nov to the versions in use: Layouts 1 (bars) and 5 (risk bar, 5a–5g) and meters 4a–4e are removed (in
git history). It opens on a trader who is mid-order and stressed: what this is, a meter that shows how far from his
usual he is, one plain line on what he is doing, then the guardrail or Not now. Everything is centred; 24 between
blocks, the body text 16 under the meter, 32 from the last text to the dock's line (L3's sheet has 24).

| Slot | Content |
|---|---|
| Heading | "You are overtrading" (`heading-24`) over "Your chances of losing money today are high" (`label-14`, secondary) |
| Meter | 4f Soft dial or 4g Blocks (below); in the middle the level word — Safe · Caution · High risk — only (no multiple in any layout since 20 Nov) |
| Body text | Size-up: "You are placing a bigger order right after a loss"; every other case its own fact ("3X more orders than usual today"; state C: the raw fact, "14 orders today"). `description-14`, secondary |
| Dock | `ButtonGroup` vertical: `primary` = the case's guardrail · `secondary` "Not now, place order" (on Positions: "Not now"). Setting "Buttons → Both guardrails": primary · secondary (other guardrail) · ghost Not now |

**Settings** (prototype; also pills on the floating switcher):

| Setting | Values |
|---|---|
| Meter | **4f · Soft dial** (default) · 4g · Blocks · 4h · Speedometer · 0–100 · 4i · Speedometer · Low–High (4h / 4i have their own layout; Meter layout doesn't apply) |
| Risk level | **High risk** (default) · Caution · Safe — where the reading stops, with that level's colours, glow, grains and word |
| Meter layout | **Text first** (default: heading, sub line, meter, body text) · Meter first (meter, "You are overtrading", body text; other cases add "Your chances of losing money today are high" to their fact) · Tag first (a red secondary L3 Tag "Overtrading Detected" with a filled warning icon — 8 padding, 2 icon → text, an L3 gap — then "Your chances of losing money are high" (`heading-18`), the meter, body text) · With multiple (now the same as Text first: the dial's multiple was removed, 20 Nov) |
| Meter fill (Soft dial only) | **One colour** (default: the whole ring turns green → yellow → red as the needle moves; levels 0–45 / 45–65 / 65–100 %, high risk lands at ~75 % for 2X) · Blended (each part keeps the colour it was filled with, melting into the next over a soft band; levels 0–33 / 33–60 / 60–100 %, high risk at ~85 %) · Blended · 3 blocks (20 Nov: the blended ring cut by a 6 gap at each colour change — three blocks, each in its own colour) · 3 blocks · Low–High (20 Nov: the 3-block dial in three equal blocks (0–⅓–⅔–1; low stops at ⅙, medium at ½), drawn at 0.84 about its base centre, with Low and High beside its ends and Medium over the top — Heading/16, content/primary — the risk Tag in the disc where the level word was, fading in as the needle reaches the reading; under the dial the speedometer's heading and fact, whatever the Meter layout) · One colour · Low–High (20 Nov: the one-colour ring with everything of 3 blocks · Low–High — equal thirds, the scale round it, the tag in the disc, the heading and fact under it) |

**4f · Soft dial** (`sheets/SoftDial.tsx`, from the user's reference): a thick ring filled from the left with a radial
gradient (deep inside, light outside), sparse white grains (brightest in a soft wedge behind the needle; the ones on
passed levels fade away), small ticks, a solid black needle standing on the centre disc, glass on the fill (sheen, soft
highlight, fine rim), a faint tint on the rest, a blurred glow behind each level as the needle reaches it and a bloom at
the tip; the lower ends fade into the sheet. Before the needle moves the ring is plain grey. Motion (Web Animations,
one path for needle, fill, grains, colours and word): ease-in-out a little past the reading, back, forward a touch,
settle (≈ 2.7 s); colours blend in oklab; the word swaps Safe → Caution → High risk (out, then in).

**4h / 4i · Speedometer** (`sheets/GaugeMeter.tsx`, Figma LM → F&O Playground 6917:62779, 20 Nov): the Figma
speedometer illustration (`sheets/gaugeArt.ts`, its exported paths and colours — a brand illustration, not tokens): six
colour segments green → red with a thin pastel rim, a black ring with ticks, a dark face and a white needle; its scale
in Heading/12 — 4h 0 · 30 · 50 · 80 · 100, 4i Low · Medium · High — placed as in Figma. Its own layout: a pink wave (the
level's light tint, blurred 11.3) across the top of the sheet, the dial, 16, the risk Tag (md, secondary, loss / warning
/ profit, warning icon), 16, "Your chances of losing money is high" (Heading/20; medium / low for the other levels; Figma said "Your portfolio is at high risk", changed 20 Nov), 8, the fact (Description/14, secondary — Figma had Label/12, changed 20 Nov; size-up:
"You are placing a bigger order right after loss"); 24 from the sheet's top and 24 to the dock's line. Where the needle
stops: high risk 78 (as drawn in Figma), medium 50, low 15. Motion, once on open: the segments light up left → right
(0.26 s each, 70 ms apart) with their labels, then the needle swings up from 0 with the soft dial's run (eased, a little
past the reading, back a touch, settle; 2 s after 0.32 s) and the segment it lands on brightens once. Reduced motion:
the end state. Dark: the illustration as it is; the wave and text follow the theme.

**4g · Blocks** (`sheets/BlockDial.tsx`, from the user's reference): 13 thick rounded blocks with gaps, grey at rest; a
fast eased fill (1.8 s, the same run with overshoot and bounce) lights them in their level's colour with a gradient (no
glass); the block under the fill's head lifts outward and settles back — a wave travelling with the fill; level glows and
a tip bloom as on 4f.

**Mobile:** each dial's drawing area reaches past the ring (16 at the sides — the sheet's edge — and 70 above), pulled
back with negative margins so the dial doesn't move: mobile Safari clips SVG at the svg's box, which cut the blurred
glows off in hard edges. The text is drawn above the glow.

**Floating switcher (prototype only):** on the order pad and over the open nudge, a draggable pill: grip · Meter · Risk
level · Meter layout · Meter fill · Case · State. Each opens its own menu. `components/SheetSwitcher.tsx`, options in
`options.ts`. Not part of the design: don't build it.

**Vibration:** two short pulses (70 · 60 · 70 ms) when the sheet opens, not when it changes; setting "Vibrate when it
opens" (on). In the Lemonn Android app the page calls `window.LemonnApp.vibrate`; in a browser, `navigator.vibrate`
(Android Chrome, right after a tap; iPhone has none). Real app: a native warning haptic.

Data states: A = own history and last time lost · B = own history, no loss · C = thin history (raw fact, no multiple)
· D = can't score → the generic sheet. Cases: `data.ts`; words: `copy.json` `case.<id>.*`.

### Trade protect sheets (nudges-12 … nudges-29)

From Figma "Nudges" (LM → F&O Playground, 6928:31781, 23 Nov) — seven frames, five use cases — and the shortlist
"TP/SL and PnL Protect nudges — shortlisted triggers" (20 Nov) for the rest. ONE sheet (`sheets/TradeProtectSheet.tsx`)
over the order pad, as Figma draws it; a use case only fills its slots (`data.ts` `protectUseCases`, words in
`copy.json` `protect.<id>.*`).

| Slot | What (Figma) |
|---|---|
| Picture | Figma's illustrations — the shield with "High Risk" (80 in 100, its lower half fading into the sheet), the calendar, the warning triangle, the candles (120 crops of Figma's artwork, white cleared so they sit on dark too) — on Figma's pink wave (error light tint, blurred 17.65); or a glyph on discs: **dot** 80 (light 66.67 + solid 48, white glyph 22.67) · **hero** 100 (light 83.33, glyph 56) |
| Tag | Over the heading: "P&L: −₹4,800" or "High Risk" (L3 Tag md, secondary, loss / profit) |
| Heading · line | Heading/20 · Description/14 secondary — or the P&L figure itself ("P&L: −₹4,800", the figure in its colour) |
| Content | RECOMMENDED list (grey head, Label/12 2 apart, rows: 32 tool box + Label/12) · one recommended tool (36 box, Recommended tag sm) · his figures side by side (Label/12 tertiary over Heading/18, 50 rules, white → error tint; the order size with an up arrow) · the stop-loss price (Recommended tag, "Set a stop loss to this order at", Heading/14) |
| Buttons | Primary: the tool — PnL Protect (today's loss limit sheet) or TP/SL for this order · Secondary: "Not now, place order" (places it) or "Not now, I will trade on my own" (closes) |

Spacing as Figma's L3 sheet header: 24 above the picture; picture → words 12 (icon) / 16 (illustration) / 24
(illustration alone); 8 between the words; 16 to the content; 24 to the dock. Figma's Auto TP/SL icon animates as in
Figma (candle grows in, target then stop slide in; 2 s loop; none with reduced motion).

**Versions** (setting *Trade protect · version*, floating V1 / V2 on these screens): Figma's two drawings where it has
two — M10 (calendar + Recommended card · calendar on the wave + P&L tag) and size-up (dot icon · warning illustration) —
otherwise Figma's design and the other kind of picture; for use cases not drawn in Figma, an icon and an illustration.

**Use cases** (screen list sections):
- **Figma designs**: High risk today (Figma 1) · Size-up after a loss (4 / 5) · Trading more aggressively (7)
- **Money moves**: M1 · M2 (₹ added, today so far, exits at) · M11 (lost all the money added)
- **The day's P&L**: M7 (calendar, P&L) · M8 · M17 (high / peak and now) · M9 (Figma 6: High Risk, stop-loss ₹96.45)
- **One trade**: M13 · M14 · M15 (High Risk / P&L tag, the stop-loss price)
- **Across days**: M10 (Figma 2 / 3) · M18 (best day, green) · M19
- **Your positions and tools**: N3 (Protect both) · N12 (Auto TP/SL)

Differences from Figma: "Active P&L Protect" reads "Activate P&L Protect"; "You trades" → "Your trades"; "lemonn" →
"Lemonn"; the order pad behind is the playground's Gold F&O pad (Figma: TATA MOTORS). The shortlist places some triggers
on deposit success, Positions or a fill toast; here every one opens over the order pad (each screen's note says which).

### Data

`data.ts`: `nudgeCases` (id, kind, `where` order | positions, primary guardrail `pnl` | `tpsl`, `ratio`,
`othersLostMore` %, `lastLoss` ₹, `othersVs`), values from the product team's compare file (2026-11-01); the sample
order (`orderContract`, `funds`), pre-filled TP/SL (20% / 10%), loss-limit presets and sample loss. The API must
provide, per nudge: case id, data state, the headline numbers, ratio, own last loss (A), group share.

### Rules & behaviour

- Silent help first: the sheet only appears when the revenge flag and the journey engine agree; capped 1 per session,
  2 per day, shared across all nudges.
- Every sheet is skippable in one tap; it never blocks the order, never asks for a deposit, never gives advice.
- Box 2 describes what happens to people, never "because you…". Never promise a green day. Never use "only 2 in 100
  stop" as copy.

### Differences from the draft

- **One consequence, not two:** the draft shows "Others who did this 67% lost more" and "What it cost them ₹2,500
  more" (or "Loss grew 1.8X"). The sheet keeps one line; the cost stat is dropped. Percentages read as "7 in 10".
- **"Overtrading Detected" is a tag** over the fact, not the headline: the tag says what this is, the fact says why.
- **Behaviour box → bars:** "3X more orders than usual" is drawn as his usual vs today, so the size is seen, not read.
- **Buttons:** one guardrail + Not now by default (one clear choice); the draft's two guardrails are the "Buttons"
  setting. Main button L3 `primary`, not lime (lime is Buy, right under this sheet).
- **"Not now" says what it does:** "Not now, place order"; on Positions just "Not now".
- **Not measured → left out:** cases the draft marks "Not measured" show no group line instead of the words.
- **Positions:** generic, expiry and giving-back fire on Positions in the draft; the prototype shows them over the
  order pad (no Positions page here yet), with the Positions dismiss label.

### L3 gaps

- No illustration for "slow down" / caution moments (the draft wants the Lemonn character).
- BottomSheet has no non-dismissible mode: without `onClose` a backdrop tap does nothing, but the sheet still follows a drag (5d pins it with a flow CSS rule on the dialog). A `dismissible={false}` prop would cover it.
- No static (non-tappable) pill: Layout 1’s Chip header is drawn in the flow (NudgeSheet .chip) in the pill-tab shape with error-light tokens. A Tag with `radius-full` and a larger size would cover it.

### Changelog

- 2026-10-30 · first build on the `playground` branch.
- 2026-10-30 · nudge sheet revamp: one card (big number + proof, 10 people filling in), pulsing icon, primary + secondary dock; tags, bars, explainer and disclaimer removed to cut text.
- 2026-11-01 · nudge sheet redesigned from the product team's 17 use cases for a one-glance read: ✋ + "Overtrading" tag, the fact as the heading, usual-vs-now bars, one consequence line; case values from their compare file; "Sheet title" setting removed.
- 2026-11-01 · settings: "Show on every Buy" toggle (fires the nudge on every Buy / Sell); data state is a dropdown.
- 2026-11-01 · "Layout" setting: 1 · Centred + bars, 2 · Big number, 3 · Compact alert.
- 2026-11-01 · tag reads "Overtrading Detected" (md), in every layout and case; Compact icon centred.
- 2026-11-01 · the Case / Data state settings now change the sheet on every nudge screen, not only 01–02.
- 2026-11-01 · the phone vibrates when the nudge opens (setting "Vibrate when it opens").
- 2026-11-01 · "Show on every Buy" is on by default.
- 2026-11-01 · floating Layout · Case · State switcher over the open nudge (prototype only, draggable).
- 2026-11-01 · the floating switcher shows on the order pad too, before the nudge fires.
- 2026-11-02 · multipliers are written with a capital X (2X, 3X) in every layout, so the sign sits level with the number.
- 2026-11-02 · every sheet in this flow has 24 above its content as well as below (L3 has 16 on top); a difference from L3.
- 2026-11-02 · Layout 1 header: Chip (✋ + label in one light-red pill, no circle; default) or Icon + tag — setting and floating switcher.
- 2026-11-02 · Chip header: 24 above and below it; on open it pops in as ✋ alone, then opens to show "Overtrading Detected" (while the bars grow).
- 2026-11-02 · a nudge with no bars and no consequence (giving back) keeps 24 under the headline, above the dock.
- 2026-11-02 · Size-up after a loss is the default case and heads the case list. Floating switcher: every control is a dropdown pill with its own designed menu (no system picker); the case pill truncates so the bar never runs off the screen.
- 2026-11-04 · Layouts 4 · Risk meter and 5 · Risk bar: where the trader is on a safe → danger scale, his usual vs now, animated once.
- 2026-11-04 · Layouts 4 and 5 trimmed: the meter / bar at the top, one heading, the tag under it; the not-safe line, the consequence and the bar's card removed.
- 2026-11-05 · Layout 5 is the default and has one version (size-up); the switcher hides Case and State on it.
- 2026-11-05 · Layout 5: zones renamed Low / High risk zone; the Usual and You now pills, the green usual dot and the tag removed; one floating tooltip ("High chance of losing money", two lines) centred on the red dot, sliding with it; heading "Overtrading, you just entered the high risk zone".
- 2026-11-05 · Layout 5: the tooltip grows out of the red dot once it settles (no longer rides along), with 12 of room above so its overshoot isn't clipped; the red dot then glows on loop like a live indicator (a soft red ring swells and fades). Reduced motion: all still.
- 2026-11-05 · Layout 5: the tooltip is one line, with its arrow near its right end (on the dot), so it covers the empty part of the bar on the left; it still grows out of the arrow.
- 2026-11-05 · Layout 5: the tooltip emerges from the red dot: a small red blob leaves the dot, rises to the arrow spot and opens into the dark bubble (0.7 s), text last.
- 2026-11-05 · Layout 5b · Everyone vs you, picked in the Case pill: Everyone and You tooltips in turn, Safe zone / trading to plan · Danger zone / chasing losses.
- 2026-11-05 · Layout 5c · Why first: L3 lg header "You're overtrading" · "Your chances of losing money are high", then the Everyone vs You bar without the zone notes.
- 2026-11-05 · Layout 5d · Story: 5c played as a short feature video (heading stamps in centred, the risk line, both rise, the bar builds step by step, buttons last); can't be dismissed; buttons "Place an order with an SL limit" · "Place without limit".
- 2026-11-05 · Layout 5d: tighter: the risk line follows the stamp, the bar grows from its centre as the words are halfway up, and Everyone → You is quicker (≈ 5 s in all).
- 2026-11-05 · Layouts 2 · Big number and 3 · Compact alert archived (out of the Layout setting; code kept in NudgeSheet, a stored value falls back to Layout 5). Phone app mode: two floating one-tap buttons on the order pad screens — 5A–5D (Layout 5 version) and L1 · L4 · L5 (layout) — in place of the app-wide V8 button.
- 2026-11-19 · Layout 5e · Fact first, 5f · One card, 5g · Compact (Case pill on Layout 5): 5a re-laid out after a design review — the fact leads, plain-word markers on a calmer scale, no prediction tooltip or looping glow; 5g has side-by-side buttons. Branch `Anshul_Risk_Meter`.
- 2026-11-19 · Layout 4 · Risk meter is the default, for every case: the fact as the heading, the consequence under it in secondary (no tag), secondary end labels. New **Meter** setting with five styles — 4a Needle, 4b Ticks, 4c Sweep, 4d Knob, 4e Levels — each with a blurred glow behind every level as the reading reaches it (`sheets/Meter.tsx`). Branch `Anshul_Risk_Meter`.
- 2026-11-19 · Meter 4f · Soft dial (from the user's reference) is the default: thick gradient ring with dots, ticks and a dark marker, centre disc with the multiple and the level word; the dial and the word change green → yellow → red as it fills, with the blurred glow per level. The meter replays when the case or state changes.
- 2026-11-19 · 4f Soft dial: softer background blur (wider, about half as strong), fewer and smaller grains that travel with the needle (passed grains fade to 35 %), and a glass needle standing on the centre disc.
- 2026-11-19 · 4f Soft dial: the background glow is back to its earlier strength but in a lighter colour (level colour + 50 % white); the needle is solid black (no glass); the glass effect moved onto the filled part of the ring.
- 2026-11-19 · 4f Soft dial: the blur is no longer cut at the left / top (mask and filter areas reach past the ring); one continuous green → yellow → red blend; the needle eases in and out, overshoots and swings back before it settles; the sub line in the disc is gone; on Layout 4 the fact heading now sits above the meter.
- 2026-11-19 · 4f Soft dial: until the needle starts, the ring is plain grey with no glow or bloom; the tint, colours and blurred glows all start with the needle.
- 2026-11-19 · 4f Soft dial: a grain trail rides just behind the needle (30 grains, densest, biggest and brightest at the needle, twinkling while it runs; it turns with the needle, bounce included); grains left on the green and yellow levels fade away once the needle moves on, the red level keeps a few; the level word swaps out-then-in (no overlap).
- 2026-11-19 · 4f Soft dial: the bigger grain cluster at the needle is gone — back to the earlier even grains, a little brighter (60 %) in a soft wedge that rides behind the needle; the grains on the green and yellow levels still fade away as the needle moves on.
- 2026-11-19 · Layout 4 · Risk meter copy: heading "You are overtrading", sub line "Your chances of losing money today are high"; under the meter, size-up reads "You are placing a bigger 2X order right now after a loss of ₹2,900" (was "Last time you did this, you lost ₹2,900"), other cases show their own fact there.
- 2026-11-19 · Layout 4 · Soft dial: the centre shows only the level word — Safe, Caution or High risk — no "2X". New **Risk level** setting (pill on the floating switcher): the reading stops in the green (Safe), yellow (Caution) or red (High risk) level, with that level's colours, glow, grains and word (Safe stays green; Caution blends green → yellow). The heading "You are overtrading" is heading-24 (was 20), centred with its sub line, no separator; 24 above and below the meter; the fact under it is body text (description-14) in secondary.
- 2026-11-19 · Layout 4 · Soft dial, two new versions (pills on the floating switcher): **Meter layout → Meter first** — the meter on top, then "You are overtrading" (heading-24) and one line under it, "You are placing a bigger 2X order right now and your chances of losing money today are high" (other cases: their fact + "Your chances of losing money today are high"); **Meter fill → Blended** — each part of the ring keeps the colour it was filled with, green → yellow → red, melting into each other over a soft band at each level edge (oklab, smoothstep), drawn as 90 slices under a radial shade; the default stays One colour (the whole ring changes colour).
- 2026-11-19 · Layout 4 meter-first line: "You are placing a bigger **2X** order right now, and your chances of losing money are high, as you have already made a loss of **₹2,900**" — the multiple and the loss in bold (weight 750, primary). The gap from it to the button dock's line stays 24 (the content's bottom space).
- 2026-11-19 · Meter **4g · Blocks** (from the user's reference): the half ring as 13 thick rounded blocks with gaps; up to the reading they light up one by one in their level's colour — green, yellow, red — the rest stay grey; the level word in the middle; follows the Risk level setting and works with both meter layouts (`sheets/BlockDial.tsx`).
- 2026-11-19 · Meter-first line shortened to fit two lines: "A **2X** bigger order right after a **₹2,900** loss raises your chances of losing more today" (bold multiple and loss kept).
- 2026-11-19 · Layout 4, third meter layout **Tag first**: a red secondary L3 Tag "Overtrading Detected" (md), 12 below it the heading "Your chances of losing money today are high" (heading-18), 24 to the meter, 24 to the fact as body text ("You are placing a bigger 2X order right now after a loss of ₹2,900").
- 2026-11-19 · 4g · Blocks in the soft dial's design language: each block has depth (deep inside, light outside) and glass (sheen, soft highlight); grey blocks have a soft gradient; a fast eased sweep (1.8 s, the needle's run with its overshoot and bounce) fills the blocks, resting on the last lit block's edge; a blurred glow per level as the fill reaches it, a bloom riding the tip in the current level's colour, and the word swapping Safe → Caution → High risk on the way.
- 2026-11-19 · Tag first: the tag has a red exclamation (Material "error") in L3 Tag's left icon slot; the heading is "Your chances of losing money are high" (one line).
- 2026-11-19 · Tag first: the tag's icon is a filled triangle exclamation (Material warning-fill) in the tag's red, 2 from "Overtrading Detected", 8 padding left and right (L3 gap: Medium Tag has 2 at the sides and 6 icon → text, no prop to change it). Soft dial level edges moved: green 0–33 %, yellow 33–60 %, red 60–100 %; High risk lands at ~85 % (2X), Caution at 47 %, Safe at 20 %.
- 2026-11-19 · Soft dial: the moved level edges and deeper needle apply to the **Blended** fill only (green 0–33 %, yellow 33–60 %, red 60–100 %; High risk at ~85 %); the **One colour** fill is back to 45 % / 65 % with High risk at ~75 % (2X).
- 2026-11-19 · 4g · Blocks: no glass (gradient only); a wave travels with the fill — the block under the fill's head lifts 7 outward and settles back as it moves on, following the same eased path with its overshoot and back-swing.
- 2026-11-19 · Meter layout **With multiple**: as Text first, with the multiple big in the dial (heading-36, "2X") above the level word — soft dial and blocks — and the fact "You are placing a bigger order right after a loss of ₹2,900" with the loss in red (content/accent-error, weight 650).
- 2026-11-19 · With multiple: the fact reads "You’re placing a bigger order right after a loss of ₹2,900". Soft dial and Blocks: the drawing area now reaches 16 past the ring on each side and 30 above / below (viewBox −16 −24 372 240, the svg pulled back by negative margins so the dial doesn't move) — mobile Safari clips SVG at the svg's box, which cut the blurred glows off in hard edges.
- 2026-11-19 · Size-up body text in every meter layout (Text first, Meter first, Tag first, With multiple): "You are placing a bigger order right after a loss" — no multiple, no amount (the bold 2X / ₹2,900 and the red loss are gone).
- 2026-11-19 · Meter + body text read as one block: the dial's box now ends at the ring's base line (soft dial and blocks, svg bottom margin −40/340) and the body text sits 16 under it (Text first, Tag first, With multiple); 24 from the sub line to the meter and 24 from the body text to the dock's line, as before.
- 2026-11-19 · Tag first: the dial shows the multiple too — "2X" above "High risk", as in With multiple (soft dial and blocks).
- 2026-11-19 · Layout 4: 32 from the last text (the body text, or Meter first's line) to the dock's line (was L3's 24).
- 2026-11-19 · Cut down to the risk meter: Layouts 1 and 5 (5a–5g), meters 4a–4e and their settings removed (Layout, Layout 1 header, Layout 5 versions, the app-mode quick switches); kept 4f Soft dial and 4g Blocks with Risk level, Meter layout and Meter fill. The dials' drawing area now reaches 70 above the dial (was 30), so the blurred glow isn't cut off on mobile; text drawn above the glow.
- 2026-11-20 · The dial's multiple ("2X") is removed from every version (Text first, Meter first, Tag first, With multiple; soft dial and blocks): the disc shows only the level word. With multiple now looks the same as Text first.
- 2026-11-20 · Meters **4h · Speedometer · 0–100** and **4i · Speedometer · Low–High** from Figma (6917:62779), with their own layout and motion (segments light up, the needle swings up and settles). Meter fill **Blended · 3 blocks**: the blended soft dial cut into three blocks where the colour changes, each block in its own colour.
- 2026-11-20 · 4h / 4i speedometer heading: "Your chances of losing money is high" (was "Your portfolio is at high risk"); medium / low for the other levels.
- 2026-11-20 · 4h / 4i speedometer: the fact under the heading in L3 Description/14 (was Label/12).
- 2026-11-20 · Meter fill **3 blocks · Low–High**: the 3-block soft dial with the speedometer's Low · Medium · High scale round it (the dial a little smaller to make room).
- 2026-11-20 · 3 blocks · Low–High: three equal blocks (Medium now over the middle of the yellow), the scale words at 14, and the disc's word reads Low risk → Medium risk → High risk as the needle moves.
- 2026-11-20 · 3 blocks · Low–High: no word in the dial; under it the speedometer's text — the risk Tag (High Risk), 16, "Your chances of losing money is high" (Heading/20), 8, the fact (Description/14) — and 24 to the dock's line; Meter layout doesn't apply (hidden in the switcher).
- 2026-11-20 · 3 blocks · Low–High: the risk Tag moves into the dial's disc (where the level word was) and fades in as the needle reaches the reading; the heading and fact follow the dial; Low · Medium · High at 16.
- 2026-11-20 · 3 blocks · Low–High: 24 from the dial to the heading (was 16).
- 2026-11-20 · Meter fill **One colour · Low–High**: the one-colour soft dial (the whole ring turns green → yellow → red) with the 3 blocks · Low–High design — equal thirds, Low · Medium · High round it, the High Risk tag in the disc fading in as the needle lands, the heading and fact 24 under it.
- 2026-11-20 · Blended · 3 blocks: three equal blocks (green, yellow, red a third each; low stops at ⅙, medium at ½), as in 3 blocks · Low–High.
- 2026-11-23 · Trade protect sheets rebuilt from Figma "Nudges" (6928:31781): its illustrations, wave, tags, Recommended list / card, figures card and stop-loss row; 18 use cases (Figma's 5 + the shortlist), each in two versions; replaces the 22 Nov draft. Branch Anshul_Trade_Protect_Bottom_Sheets.


## Source — this flow

### `src/flows/nudges/assets/protect/arrow-up.svg`

```tsx
<svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="Frame">
<path id="Vector" d="M16.2256 9.47C16.4456 9.80333 16.459 10.14 16.2656 10.48C16.0723 10.82 15.779 10.9933 15.3856 11H13.2056V18C13.2056 18.28 13.109 18.5167 12.9156 18.71C12.729 18.9033 12.4923 19 12.2056 19C11.919 19 11.6823 18.9033 11.4956 18.71C11.309 18.5167 11.2123 18.28 11.2056 18V11H9.02565C8.62565 11 8.32898 10.83 8.13565 10.49C7.94231 10.15 7.95565 9.81333 8.17565 9.48L11.3556 5.33C11.5556 5.01 11.839 4.85 12.2056 4.85C12.5723 4.85 12.8556 5.01 13.0556 5.33L16.2256 9.48V9.47Z" fill="#000"/>
</g>
</svg>
```

### `src/flows/nudges/assets/protect/calendar.png`

```tsx
�PNG

   IHDR  h  h   z�a�   IDATx�]`���ޞ�\�^p�c:��;���$�N��@��.؀�%�IB���{�e[VwQ����foO'Y.�����v޼y�f�����ٽ��h�,Y �@d�M����$OKT���" ���zAd�����A�#�Nr����6ODz�<oQ�#Dh�t38�Q���6o	���p�6D�,�EZ r�[�i�Y ���`��Ao	g1j÷�@$Y`��@�7��U2�@d��h��A7ǳ�9�@d������,N�[ɨ���6Dz�8Q-"D�,��"��I"Fd���6D�۞�H>�@d��?�"�:*&�@d����������#D�,�Y`;���Q1�"Dh�t38�Q#D�<-9���E��,Y`[`ST9�M�Du�,Y � -9h!�#D�,�)Z rЛ�Y��Y`S�@T�����Q�Y �@d�u[ r��Q$Y �@d�����Q��eY jMd��c��Ao�FZ#D�,�-9��m�HAd���6�"�q�i��@DE�,�-9��h�([d���6�"��-�,Y ��w�@䠿��6T�HOd����d��A��2?�@d��?�"�#������"�����^S�#~d�����"�Nr����6ODz�<oQ�#Dش-�Aj9�b�HId���6�"��mi�,Y ���@�7�#%�"|D��g��A���"���"����n����"��"�~v��"�p�J�,��@䠓�����"lj���vF��D�,Y i��A'���zFh>�t�9�QK#D��,9���EՍ,Y��X r�[ֹ�ZY ��d��AoA'3jJd��[�"�e�Ϩ5�"lAhVz:oQS"Dh�t38�Q#D�<-9���E��,Y�X��A7��FM�,Y ���d��AoNg+�kd������nV�;jld�-�[l�"�Şڨa�"l����~��G�,��Z r�[쩍Y �@t�|-9����E5�,Y`�@䠷�5/��e�y������/��>�̟1c�?T�[r9��ޒ�nԶu[ �� �8iҧO==��o�	�]w-t�Q�o��XI䠛�ɏ�Y`CX@��!C�|�=w���믿A���c��A���!�h�:"�\�|����s��9��7^��!#s`��.�.]z�*�Y��t�<����H.���-PR^r��9s��h</t'c6?G<� ����E�k�(_d����ˊJ�=z4�<�`3C�n=Ъe����<߻����)�,Y��Z��������<.od��1�f��?�ڷ{���-�}�Q�����
.�왳��J���*-Z����D�6m��h�GȪ�1k�-�@d��l�����fϙ���Rdff"##��̰M�mУg�����#����o�#�}-�,��,�bŊ>jrQѲ'O����:7���b\��,��{��Z�h��h��G޵f�#Dز-�hѢ�'L� �>�M�ę}7�����߲e4{�]��9��c�(od�fh-[�4g�̜9	:�x"�x;t�{����I?�yF�7�o����yII�q?T����AolG�#l�(//�;{�,��� ������A����:u��'9��􊊊�_{��~�~�z=��#x������Ͽ5{���߽�M'g�7�s�$��fc��e�Ν5{6j����'֢���9����yyy�7vc������o��Ï�o}#G���－A��O>����蔍]���?r����[�fΜ9ӵ�-q��QW[����{�����5�%n�Cii��|�����?�q��@(�7I2�p�B|��W�2�f�3��Ao���,��Z�5k���7o��Ã��.���;�4�U�V������5��=���3s��fp����x���o������Aov�,�pd��t�w����RX򗃪QFF��w ڴ)ب��0f��g�y��6</����p��C�����.hۦ������*����F�TFؒ-�����9��"�Fz���琝��c�=��͇L�(�7ߌ(6lל�D,#ý�g�2ǹ�R]]��t�!8ꨣ�t���!F7�]�٬U>���d��P����eΙ31O�9ϋ!��U���o�}6ʻ�Z�3v�aÞi���ϻ�r�c�f��u�:��޸�����^{n�������U?�@d�����dQ!29����,�����N;�Ʈ����ƨNaa�U/�����{ƽ1��	Ĺ������a��w�C=��v�8u��Z���A��BQzd��)̚5k��i�QQQA���Xb^L?J�~���ېF�{b��3�=;5�5Tm�A�D�9i9���\��i����Gz�9��AC�*n��:m�e3fL����YsVf�{�.7/�p�oߢE�ny��'��˟����
��� �k�1.��q�w�n<1hv�s��#��C���tc�D����h�R������3G�l�
���c؀[qq�I����_ǲ�"��=w1�s7��Л�*�=� ��k�#��ޢ��AoQ�3jLd��k�]w�u��{�l�\�ի�Pв G�[��~��*]�>��o��&�.Y3s�u����m�s�=8���~֦��{s��#"�#~�b#Nd�M�[o��E��z���.��v��{.��r\t��6�u��<5�W^Ƃ��Q�E�9�[c�]v��7ހÎ<옶m[�Gi[""�%�ըM�6���{��g�q�c��rn��ړO9���w�}�*rР'��}3g��C�:h)C03��ܻ�+.��Ru�ѧ������DzS<+Q�"l��z뭯>��m�����֭�=�������������܇����?���n���������n�_,���cћ������Y ��d�>���'0}�T���O�Ut<�P�]v��s>N<���;v�8�1��C䠷�5/���`�/�����1z�H��-e�ug���ؕk�g�q&~u���9����!�@d������<���[�Я�RP3�޽w�9g��~u��7˙���l䠿�񢬑"|���������>�_UU����o������O���\�����a4D���sTJd��k�@]]]'����O����}�n�.��2��n�֭�{��h��ft���F��, }������Y��2b1t��W]y5N<����φ�;n�������E�,�a,�W�~�?��kO�o�;��z�!���SNm���"M#D{d��?�������W_���_���g�����O����9�uY(J�,��Y�ٕ��v۝ծ]�7�]�����A��0;�@d��?�"�c��͸����Sƌ?�w��_����_��=;���g�W^}������>ܟ=k֐����7�n�����1yʔ��y�}�ŗ^��?��#�#�>�8�饗�w�{ϟ1c����F�H�x��@�7�ӲiVJB�d�S��W\q��ig�z�y�m�����;nǽ�ރ��x�x�qםwᦛn¥�^�3�<��s�9���o����_���͛w߆h��cڌ����ʫ�����_r��\t�}o��:��޻��#�`�O�����G�=����]�s�9��s�9{��o����_���̚5`smT���@���V�V�����?�п�{G\u�}�� ^y�|��9b&����S�aƌ��5sfΜ��ӧcҤI3f�>�����̰a�뮻�%�[��O�W_~闗��\��ǟ������u�\sʟ��=�����՗_a�ĉ�=k6-\�%��K�p�B�"o������������N������/����?��c?�;�r{P䠷�s��[VVV���?����W���x�g����cڴ�(-)EnN.��v[���8�#����q�O��A�=���z�B�֭a��U�V���cǍ����<�$n��V
��   IDAT<>p�[�Ə�re��߻���S����w�w��x��������k"���вU+�޹7;�0�◿�I�>	��Չ��	��1�w9��ޥ7:w��Ű��&L�;＃g��Y���ׯߧ����Z��Z`ӬVYYY��=j���_r��t��s7��FzS;#�>�SϜYs���o?p��x����٧�����Z�O�}p�)'�����q��'�������9�r(�8�pvء���ܥ�X�ժ.^��s�����C��O�o������/��	l!�y��/o�����:����m�p N=�T\~�����8��������{��v�������o?�������=�A������>��3:�g��C����-[v�b����?���_�B��7��q}�_����]w�q�wu������6j���?l�ҿ���Aw�m�9Ǎ�0��g���������ڷ�!���;W_}�;�<���Vݺ!�3i�47^8��?-h]�nݻc�]wu�e��~�=��l�a��x�7���7�|���ٳ���6cb����^|��W~�a����t��hӦ-;�0\p����6<���ܝG7�0p��ݙ���c�����u��/?/m
ڠ/r={�@�Ν��6�8�.Y�w�}�{O>��3�M{�t�s^��?~���>����?��2���������|�����c�?����/�?�y���=���x���9˦b>oS�HT�M�_}����SO�����b��I����^{�<�\{-~���gｱ|�JL�:'L�����.BIq	*++Q�|9t�^�tg�K!�C_93��:�OJ�����?�y��ǿ.ܜ"���O�<���������j�k﮻�3N?���j^��G�}��oNL�8_�Ǝ���f���X^�U+�\�����p�B��S���yNr�"?����7PSS�I'aРA��S&�?b��Q��Ϲ'N��s:����+��:b��A�y��_�������|��G1��g���_�޳g��r�S��232�=迆�����_ߍ[����L���9I�9jـ���q�}���QG�+��UW]�#�<5t�_~�%���̟7�V��4�f�Q]S���bv�9\c��Q�Fb��ἵ��>��y0�p@����y&���/������h�a3ܸ�~ǟ_��C��2�,�l��͚���J\y�����G����1��`��%���qN"�PKg[T��gaʔi\��l7�w\3��K����Aw.�I�^�x1�z�)�I��>m���o��7����;��Þyv��?vD�~��#��^<�X���K|0�|��״�\:�Jg�����Yb\n<�;���|n�����t��9��l5���cȐ�۽���L�]�v�9k��������c���t���}�����F,#�\-.)��30r�H�|A|�ǤI� ��u%g�r&�S��'�*n&�̈́	���k��0|�&a�oQ	:���{���{�y�9�u���9�r�-\o>]��Ҳ|ɋ�fqzcC6��ʤ3�'P��gΤ��hw��3{�_ٰ���9���rTW�p��')ȶ��y�ty�8��_�&l����G�=����t?��n<ͥ����-�;K�,q�X�s��P��>��!�^Z��쇉�����:�o��"��9�M�4����,멧������J��ܪU+��g����\���n�1g�\|��'�2y2�23!��^εҕ�����ÿ���0q�Dw�^�[qp���40<�����!g��xf������/�I�ڤب�k�l��g��{��1o�l�jي�;��>��i7��K��Ï>�p��"������p�B3f��R���/�k��\2Zɥ�U�V���Z>r���TW;G��s���`ft�����~p��z7�5l�-����>��}T�f�ڬ>F��J��c�`�_ JV3���\��ߵkW�Ç����w�~�m6��V�"N3�������C���svN�=�8\|���{��Q�s<��9Ϛ9�sܭ��F˸��ɧ��>�,:�vgeeA3k� ���G7�1S��Cc3r9����s�(�D��>��ަ�ܭ��l�Yd�׸�?���^{�ƌF����ɾ���;�{��ǧs���0j�TUU!F���b\ڈc.�.>��3g�\6R�c�΁{1!xI�,;N�$h7����	����p������.��JKK��"���G̙;�5�؏4V��:�P�%�*B�qJ��28���6|x݅[w�q����N�%�\�?ri��^|��~i�з@"�Ns�=���[os�^�����������	r�-|�"���-�
�b�>s���`2Li@x��s(1������9{I�y��`f is �25�K�)�~	�)���2�������&�͚5k����o�&�.Jz x�-�b�]wv5�����ͣ�u���DfFg��1�k�}�!/p3��>����M��0Βe#��ᾳ��B|'Ì�y,�0k�<;�,\��+V�i�k�j���m�����/�j����/�����<��ҭ��?�w_�	�����~����ǿ���?������s������u�ٶ�۝�Ml�6��D��-P^�r�'�7s�L�#ע�V[��˯@�>?��0:��=
S�NA�W`����yo��_���|:ֺ�Z�[������r������r���t����	ȉ{�Q�0y�d���_��6����߿��o���߫W/�q��8����<��9�����`lW&g�YY�XTX.�`�V.���K盠�H�75��r��<h('/�63��_W[�"���PG�K�ϯ�����Zi������ߞt2��=
�ڵ�V\��}�����\v|������O�3|�g}��'��/�=w���9�l;��C�G��nv�6�JFu�8�;w搧�q:����3�Į���,��Z�T1�k�>g)1�(W�Qc����Gg�fr%��c�v��q�W���_�[o������c���_������n�9͘}���Ŭ�,d�2R2r�z��/�K�3IԬ��S����g�zg�c΀gL��u�8���qү~�j�w�{G�=�7^�b���y/�r�s��q�2c˖-p衇���»ﾋ�>��k��������Ǟ{ '7k����y؊�.���gق�y.�|�M-U=�����:Ȇ=��E_~�Ջ��t����˟��	w���c�>��C�;��i�~־}�7��Fzs>{߱��-Z\t�k~m�e˖A�r�޻���;�3�v.>g��+�*�L���S�N��|���G�ھ}G����/����m8��c���}p������c�>���������t�Z�h�N�:�ywD�.]ѣgt���}}�f{P��������f�Y�Y#��m�w4�������]�n�w�~G>\�9:u� N�݃����
e�eȦc����z�|�9Ŵ{��33��+n��.<�Գ8笳��n�9G۳GO��^����ŗ^�%_�l�䖑��6mۢW��؞�m���;wF��ж];'e�>��#L?1Xsq)���s��C��f������]:vئM��Çܟm��Z�Atl.�s�cQ�t�7�x��>�0���GOt-e�G&�9.*��PWS�^��ƽ}PI���a�]���Ͼ�w>vޥ788����X,!�;u섟��(�}�]���!����A�Jp 9�ܕ����ڣe��|�^�<��EC�D��\���}�O�M	����W��>���g�}p�����r�gQ�"9Edgf"3+���=ztQL��Άt(n���s���}+�ff�#�ه�;���<l��ָ��+q���b������K^n.�t�.[uu?��ګ~Ģ�*]u���2|��g�:e�[�������ړ��-����#����Ҭo��Y�y[o��>���]9P��J��VWU�8�]VR�	'�wL���!vܡ7�rz�   IDAT��=mZ�[@�r�tH��i�&G���ν{�����g�	�k܃I9*]���b��mzAA�sTHnz���>J�6�`Ĩ��O�҆."[��Ż��yG��UP��M�0t����4k�'���%�Sk������e��G�\��Z�.L�r��e�/v^�C̋A��O9��v:t�t�QQQ�����E-?/��y�cخ]�»B�����o�����?�U0:l��fq�6l%+�W�����ei>��ñ�6[s��	�k�76JKK�zpUu�54�����бsG�|�-�w�} G"G!�xt$�c��-S�q��y؞O��?�<����C��t.	�g�ë*��bhٲ%Z��wq�F��:����9<-�d��N�w�^{���!G�Y���y�K�.���Pŋ��p�^[�׿�5/�G!??�碎���#�i�z2<σ�p[;����p�a�"���+Vp��� dq�.����lt������t ��Μ1���NYt��-�m�5�*��-PR\z�לMIq>�QG�<:��ŋ�L9^W�L������[ypiD�k���K��q���&�lXG�����s���� .:ͮ�8v޹7�>�l�KN}��N^efgϹn6��5[	Jn)ܘ1�.T<��'�7@�^*�2�͟�oʔ)�/�:rG��޳�k˪U+1s�,+ZFgs�w*g��M�-����'���}ѦMd����naE�\����zK�{��8��#��;����**+a<�;���Ӆ���n�yX�r�yGr��`}�DG�4-�m�Պj�!,���GHץ�Ӽys�͟;1�{m�=���͞�(.\�ffd:������%��h�o��v8��ӹ^��ݪ����ˡ�i�Y��������?�:u���G����`fn��"�eW>a�ʕ���j�yGp�u� �Z�}����Y3��;�5|xڣ{�!]nn��I9���!������(-)�,Ξ�"����۷/���:���.�������&��E=�d��2>��{�'28k�a9���ty�!ME�0�@��>Ȇl���s��9ZZ:�Jt~s�?7rҲƦ	��M�bQ�����,�k��Z�ǌӰj�*ddf`�=�B�.] g��3����Ihݴ�KJJ�\_���l�yG�=}�ً�232�Cg�1��69P� �srf�1��ޭ;�8�h�T��Z�V��kv��si�z��UWWA3V$7>����}ڴi�a�6&E6x�rT��A����sO�?kV+���3/\�ƿ��8�WJ;��D���/~��wމ�3SY��.��l�BF�F���<����uO����sOt�NN[vT���țdì�,�1�b�x����d;�u��_2훠�M�NQ��� U�ܡ�O�:����&}:~����'L1n��Db��&�?~�q�':�?i�p���Yݫӧ�0a�D��lo>��K:���
T����AFf�{M�r�rʹ���x;�k뭹�9�'O�ԩ�0m�t�#I3f̄>�w|������0s�l̘�p����ٳ���;��#T��u\�]9/9A3E�*c^^,3C]m�ϟ����|0w����f���p�3f� ��`Y/�y� >��*���ô�o�nt�o�'O�`"m�p��o����S��]�6}��!��f�2{��a�g�"̝=����W%�rrr�$��m���j����LS[�,\���Z�ނ���l�5Vq-z����Λ-#)�;�0��ys1w�\Hf�E(\�K�.qw4��@��mѥkP��_mM�<��|�Y�#V���-1�-����?��{����Bqq�I\;?s]�rӹ�⢢J�m�X��(Z#���,Ӧ�x�������[o�o����Ͽ���C�=wГ��8h�����}���<`�@�w~���O0m��g�wРA�<����r�W��q
��b�����@�C�Q��t"+V�d��Qz��2�'~�>��hڿ�����1<��x�	��'��?�P�'<� b��`���M8n��UGg⣸�ĭ{s��-uԖ.[�5�UAٞ�[��s��<��O?��UO=�̅C�zC�z��'�r�`�'�}r�Ƈ�9x�P��O!�����<i�����&�4p����0�/þ:n��A�<�����<�y�2��s�}��!O=�i�ɺ_��sî����P^V}w�M�6��˃.,�b�����X�u��Ņlg�t����O��s�a�С<d��x�t��.�=�cѿ�b�6�Y<��3���S���� �Gsk�βU^aa!��x�R^hk��}O�\�Ͽ�������So��׿���7^��k���_}��7^~��^z��^|�5��^~�a���/M=o����?��c����x����W`t�^���2߆��Au˗_����������r�M7g^yŕ����q���G��=��a����}�I<E}r0�"<	�BPx�}(���{�>3��3�mu�/�w� �\3-}�R�Z��g�*.y��Ǳ�3��������x���������x�)<��P#�:ĕ�Ԑ'Y��)4��}����r�\���{��9�����9�1���q!�*//Ӵ�U1:���2x� <���x�߃�����#�`0|�x8�G�c�
��q^D#�?<����b2x�@<)�N�c��']]U�'�����ǣ����G��C�߃@���˯��/-�9�b��ͪ��ø̐�z��Α˾�-K���)��?݋~�������&�9z�?�,�	ՙ����l�#<�����x ��^<��0L�2��Ӆ`�̙���'O��b���r���>/����^r�I}���-7ވ[o�	��r3n��V�~ۭ��Px�m��6�n��V�r�͸��q�o�������>6�}v�u��6n���/���G}0jԨżP\�vG�n��w�[�\ �[��c��2��.��J\{��J��g�r&��� [�j�Ν;����⃩��w놭�n��\G���ȮLo �o������R0�i�Δ=������tƫ�#�R�o��Pj��ol_f�CK�η��Gަ�o�m�[��m8{,��C>�k׺:�v�c�v�ԡ=:v耎�tPHt���:u$�#:w�.�o�N�]�:1�x�;������o߶-��C���ўe�o�B;�ӡ��׎���d	��X�ݾ����'��d��,GoEp����i���� �������n���:�>*0*�����]n>���Mv6Zge��V99h�如�-P@;�j��V-!�uKѭ�Я5�q�.;�m�m
о��mZ�F���F���)h���)צ-���h��ޒ�Nw ��y��%�g�-� �h�s 
[��5eZ��bz������E������t�7����M���鍿�u���|�R��JYm��޷���7���x߫������:���߇ѣG����<��v�egs�1��w���ߎ?�s/q�t�=��?����w�q��L�N΂��&8�z3��L���ߎ{��=q.8�,���ע��!F�[͵K.������:��D"�*.q��3Cg:�_�.:�h⧸��G⢣���}�"�ąG��w4.��I��ܳp�����.�W^���
7]w-n��o�L�&�X��8{��A3�[o���&��fr�swq;�q�v+�v�M7qwn�]ōқ��_�믽�]s5�g�׭	W]�k���\y%�b����2\yťI���R\M�5W]��ګ�r��ޛ���_|�޺s�9gee"���MQ�8��F����F��fe��>{����<���?��?��߾�������Y����W������O�%g��K�9���]~���qՅ��~��w���q�E�r�R���w�~)�.a����W0��K.�՗^����/}1���"\�6]~����q��������,��s�d�g�R����=W������HM   IDAT�N�Q��z�@K:n�������������]��]xa�/���Y#J++���부�n�HbcY@3�q��M�슫o��fܸ�����B���_����G����K/����p0�|�i�홧��3���g���9�����/��\ �g����p�����3�����3N9��{Zr�sv�[�ں8�zW��֡�ި`���w��P[SKWl�Y��?�%�9�����p�G�C'���D������pÅ��K���W]v������W\��/�_z��El���\������.������El�p!Χ�.��b\t�e��K.���.��WP�aY,��+�����ꫮ�ռ#����p͵����o���M�A���[p�ͷ���ov���q5e�b�+��r.3]I��_r�?����GgBF���v�'�����kѵ��ӡE+\v�q��'�c���G��?�H�M��s���ﱸ����+�Ž�݄?p�N�.����o���o�B���E����7&q/T�3��n�7�D�q;�;���yq����q����:�^ˋٵ�\�뮹�7�3q˵����F]�Q�V��J�[y����������=��O<��=��N9�xW� ��۵m��D6�ƍ�~�t��W����Aqq�I������ף�P�����Ͼ�b�)������W�eg-a\x�x��?�	>|�կ��ݺf���倯��0$��	p��gnX�[y%\�-\�ꅅ�����E��h�z$�X�Og\���娮�	ts�\�Y�f��I�\Ke<:�x�J�+V"��
�*:�u�UqxU	d&<d$��k��%K�X�u��k�5��f�\T/��>4��C���R�q�UWY�8�j�+�#�rE �u˗���u���q=���u%Ũe�8�r�|(��x�"�-D�p!ׯUv�8�g�u�>�Q˰�25�_,X�:.@�<֕�&���G�b�<��9U�棘��V��lh1����&J-m�y17��������igT��/_�x�*$�h�Z^�E�ǲ�����ATQf%�+P[V���2�.+A��e�]�����M���|Tϝ���sP=k6j��3g�z�,bysQ3��E̡,�W����Գ5�35�3���f���O,(D|�bƗ�n�]Z���m�q'��������wqw��-q�o�#�>�;u��Ї|��y�����X�h�-i���5X�[?boD�5����׷~���)�R%�?�������~�]{�ˈ���R���l)��i�3A'��9��|�t9��PQ	�W �a\�0淺x�5��V#�3f��&8M�C�����l%�TWU;'�A�YG�x<�ZƫYN������㨋Q�G7��<�l�̜x�Azu�L���C�z2xQ��.�n���Օ�,+��*AǛ(^�D�PİXV_(R���b��V\+)�WZ��=���E�c�ct��#V�ˊ�� Ƈ�ުU�V�F��ĥ��L�fA�H \�7�=�[��b�c��vˎ���O-g�U����ym F�.[z��G��A�.X,��I�Z�Ff��:|�R��=>�1 F(.�((H��2��X/կ!��1�1��1t�^*n@�1��V<�#m LvXQ����{o���x��nXV�S'N��w�����/i٪5����ԓOs����� �zD�Z-��V�(q�Z������z���t̟�N�M��r�x�O���do��!�:�ǃ~ؠ�h�xtpVZ,^+, z�����q���1gЙ��hb|�#x�Z��p�P�?�����i��娤��l�Χ�r
}:Z�PNh�^�Y�!$j`�Zx
Q���_�ڴ����|l[���:�%F'�3��l���!�P��BN4FGī�I����ٳ��}tv1���#�2��b�C:<��#ϣ�Gy/YR���6�n��^�bt܂��4�vͦ3��̠�򠇪q����u1�=5�2x���*�F׉�I�A�,AǗ����r��ц��,ڶ�WLu�C�~������(��\�g=<�/Ƽ��1�����;.OH��\��^ƕF]^
u��/e�&YD����.4�:n�7�}��!��`��i�n�mp�Y��g??zo{��J���۸�޻�UTT쌳�~�jy?v�[�������Y�8K2���G�e\{��uޘ�!��b0dp:�!��� ������㒀�%��AO���*7Cv�y=��!�r�F�dtPr���Ov�CY�t	�8-�,T�f��!�Ʋ��R�[�K��F��sƁ���3�Z��x�=[^>@�e��W��X�QW7�5�k���6z��{�^ȗ�@�9�]l�s�t
�XZC�\��$�}�C�H�:�󩃜��<�ѩzԲ�m�#��rs���<T򢵘�F��/����w��7�92x1�[r�f�r^|��ʠ�m�'�.���~���<X˖ Ͽ�b>I��ً�3�S���=Xg�SiJOCxΝ��7�ߣ|���.?��ʒ���s��ъ�� �z2X��:�>�`��0��8t�]پ&M��
��th���=?;�8t�֍}����)�m�P?^cb��a-��'��/��
�_B��rfq��w���9ڵm�w�Lb:�:����E�5C�C6:19*8�`�h��HP-3� '<ih3���v��I1�O�6��E��::]9͠���l:�̬,'[�Y�8�!�p '�j���rs�QP ���b�����A�cf��<83 ��yP+� �ʁ�q'#9](�!�� }#���2̌�����q3�@��t���d�z�իFd���y����Ѧ��{�b�J̜=��O�\��j��%$�m���ꗃ���<��cڢ.T��abJo�
�������E�lGX#���> �$\>�y�v
ґ��!\�d<��t�g��Ϭf�z����lfbЕ�b��mڢ�O���E>�q)/`�[-��t��������;��$�7�������ccЪ�YQ|cX�����>�������;��K��q�8-[�`�>t22�م� �쒥�+*`\��s0:0�˧S�9�9�E O�&:80N�F��G'ړ3uH_Ǹ	P�O��)	��Zj�=�m�r.�#�j�lL��J�3C=���3�Ѻ%��Q���IA�p4� 9�u�rI�Xk:���`{@'�ӡ<n��~�.��eS���T��̃H�C��,H;��U�#�e�]�L�ٙ�ک#�xa��X?��z��H����X��[�h���Z�c= >�>K�W ����3�υW�
��\�u`^�6SD����z;�0t\��f���,E��\��jO
"OzCQr؜���<��Wo�<��vۢun>�8�(�C�ZN,��E~���g�}ು3f̀~�2#�nv�ՙg�[`��_^��G���3�jw�q8��К��O��= =�Ӄ3h��k�&���cLΉ��H4�mI�@1�B������ܪr����ޙ3g���	�v�~���[q�B�j=(�́�񔩨�8�����v
:+���5�<��`u���2�$M�M�1�'#� �L�*���iU~���jW1����_`:E��c;�����`��XB*+/g�F!�P19|hڡC;���܄���|:g�k�	^�\ވ�n%�dCg;�a-�;;�Ϋ��k=χD���w�a������,/oh�1� P�W��zƝc�A<]p(߁��un|ޅ��$u\�N���Gm۶�n���ݶ��
|��W�裏Y��5�b {@d��m�����cҤI����?�'�|2�w�F����n�p��/)�.l\�5W9c	�㋝�'����#�
p7��8����C�C�M�^�I�A.Z�%\�朖���b:g�wt�V��/봆J�(�z�{S'cVE9��\s�9#2F��ŧs�݀5��DX)*M뜢�H6�K�)>��,I��z0�D`p���~4��� 1�1D���G%>�����[o�\��X^	�����d9P�϶�ɹ�   IDAT1�G�w�j+x��+	�Dޟ2hK�}��˅s�yy�����)�`�y�X��]�u�Ty�׉�%l8w�(��|��DrS$�x��uQc}�&�K����)n1d��z�jTW[[�8������\�Q�k׮�m�]�-峍7^Ѷ�h�ՙg�Z૯��c�ȑ��zp�zԑGb�=v��[g���I=�4���t��ΰ��9X�r!�� � U�� U\$K� �����V�zg��[a�=���U˗��S�G�`�� �rV����@[�8aq!��e�����,:�<��aY�1������u�Օ"�v���� ��ͷ��h!�ɲ@�1�9UCb<*����� �z�A��AHY�>u%b|l&'ʉ�6�z�'g�y9���^L�藗������:��R	t��-Z�d��+ �x�L|8}:��|�h���pyä_�N.A��I!��g ����i��L�&�$�Ц23�A���'�u��w`]%G�j^��tƪ5!����1(�#?�$}C[w��a��޻Z��OU�PoZ�>Q�1|8�y��.�슃:�};��
vix�Zx\���R;6ث�a�ڂ�Ӥ����AM9��\!� D �|�����̄��fغ��8`?���10�,:�+VP���I��ˣ�ء=��V4�桌K.5!�9e"�;~,�L����Ԥ�@�y���
��3r�񩚂cR2ܕ�g�a�>��WR�S#0H�bɨ|k�b|��� :� $O$�S�q���iG7���D"ahߦv߹7:�m�����A�>D��bL��R-/j�ٹ�������e�x���/�o��/&M����yQ���t"� �+�� 7ք���%��X䮶������I��Df0:[�C����9hf4�jO��)]V�U������b�s�8m��EKd�>ѺU�.�?�||��׷������<w��s��?y�$������ʵ���݆��TΫ�VQ	��F�q����*���S��0��L38H|(͠}^$r����^{b�wK����`��.�Upx�N��r���;vD���:z��EE���q�ŝ/����<��|����q �tL�HP�}��]�ơ��������0-%'~Ȥ,,�0im�1�B��6��XEH��$Iq'��K X<��§�2�v��n�`�n]��%��1o�\$x��,Qw$q:�8�t��sjSP /cn`̼��������a��y��O�<q^���˂*mA��Q��)
C�g�� &��b��t�!����������h_}R�B���)#��t̅��a�����̆��'�qΜ�e�:�%�������2�'�|�n���B�"�����a'=~\����؆k������H�)�'q:g��0vr���݌D��<p&3�yi08��hJ �X��!;�Wz��2���;�?�?7���x���XΙ�yRB��}BN�K�N�y�СCdq��W�AXT����Ͽ��O?��?��I�Y�S�h�ӧCHփA�m����� 1�+8V�fȚ%�`��̛�M)!'i#RA%I�% ,��߃��3�5��H�<_�l�{�=
Z������-]�����9�9�Z:�̬,�����00�3N�ze��|����)��`��/cΜ�P��IN�K�|�u��ӝ�:Pv��uF�a��FQ#�����4��[z:�+'�6�L�yP�M��a��X��ʵW_aTz�}B/A�Q^�!����ƍCUm����5dE;-�Ѿ-0a�,^�;��n������j$����s �3'7�� uv7.��0�#�|>�A���#���Ӑ�ӱ$Aa���Rǉ�����''<k�tL%��k�|�.9�:�t</���ݱ���%�������p��x�Ϳb����W��Y�T��
f$U��O��TȄ$MIE����|E[��'_`�=�Tt�H�w� ͐;t���.Ow>|�զek��>ؑ^}�n�D� X?���|���5N�AWӡ�j�
�Ѻk/²���8-���\�x�_��.޺N�:t
��9����y;�1�3�d� ؍�$��i�ӒT<I˼�X)YE�f��G�Z|�� ����j�BL��+�kܧ`��.nr�	�])�ml_6��̌͊cƌ�,/?і�@�S�ذ�ft�W͘2e\[��i�m�E�v����ï��s^	.��9ˋ�P�!����,�ヴ )!�1�W$C�� &���\�%F� u1���'闝s�a�������v�Ȍ�q�֡��(A����;��RG��Ñ#����sбT|��h��V�X�O�H ��8��f�h ��O�L�33XK�`&�h��T!�F��4bZb#� �L���f!'(;ƨ���2����{�C��Z�맘4y��_0rBj-ۥs'^�A�I�[�
KK�p)�ɧ<��:p��,OP^�\��i��[��Xg)�#��)��O�gT&sYI��	��t�Hq��,,[x�����BT<k&f�Π��N]:q�#	�=�x\���h!;;9|`��-Y����%'�w�,���^���F4������{5\خGO��t6�+�qy�����fJЀW��
����A�A���p��H���t$a=�� 2�N��6�����w����� �(-ŧ\��6m��8o�k�..G\[]��+�PZV���@����H9*]�v.Z�|Й��K�糞>X#�H�	���G�͌���z���3ʦ�?��.����)M������ �@0�2�	l�Ɇ,ϯ�CAA[s�a�I�A�����WXXX��i�Zޕh�����<dq���/.��0���K żxϙ� �E�g��R�AL ��G|�a3��4�.��.�pSR���Dx`\���{�*��8���q���Ƭe�8��]"�CmU\/]�:pҢ����'O�
��v�G "�{���_��h�+a.m��}+x5�����Y���4�$�P�O�76�� p��ȱ�D�`ZÝzĠNW��	:�:���f�e���+���;�=�)^�_|1�'L�J��ͼ>U/&%t��/A�<�ir��Ӫ�l*�U��0$�^{R^M�����H��|R��g\Q��㈤��1lj7!�&��C������8��c��q�Nh)��>��c�_� Z�H�3������jx]N�,ԟ�����ע��|��)	�� �����j��x掠�F`?(gFZ @
�&����Q4��jl�wP/�V���E�6c&�VW!�M;��Б��+������3_./V�����cǁ��So�a�7R���G�I�-rr��6[c�vm��	� �8���Y-	�^:e�x��Ik0��Sc�a2}rh`;P���>����K�����k�W��)++��_�O>�s��ƪ�(�(Ì��� ��ai1e�?k�feõ���0� Z�q<�az��t`�H�/��N�)%iR�ɢSIaf����\r:�y8�k���$�ԥ3t�%ˊ0|�pL��~5�9�N��5�r�\-g��N��T�3�l^8Z�@�k��E�^�>c�1ʤΣˈ��3N5<{Z'&`�� ��w�S�Y/�~��q�nլ=w*y��U�nيU�i�D
>ۡ�t-m�Y]��
�e��h��3��A;k`3�A'+������?ӽ_���������"�Ȟ��n�q���v�d7��ך��	��B�� �i 4�)C
$8�tq�q�i�$�0���إ7����.��ʂ~t1g�\|��|NG3j�h,\�[�"XWߐաU�������k�PMmJ5��2:"�Φx  ��ڇ���j�Mi�HK*,�hZ<�g��Q����D38+����2+�t0�9�d��-{�v��#�̇��&N@��(���\}�_߽��fG���]IvF&�uꄭ�� xnd/�� >k�U��jqeHR�)i��dK�s��;���w3K�����C�RJ'�~�@{�B�(.F�̹ϋSgǽz�@Nnv��%���;�>�u�Xede:ݶ]i�}�r���]hg;�.�   IDATD:i��=r�eE��s���ݶؚ��gZ�`� m>)�������2C���8f<��Or��t ��ӱh�ENZu�xF��{r&��r�p�ű�r9
.Fa�b��i�of�fƘ�,C��>�`W�³9蘙�ˇ��8 �:8I�Ãq�:U!��BVP c*2��èt8�)P�s ������Q�J�Kw�z�ӫY
�:ew���Ѻ~��ymZ�����:Ϫ3g�X�x)�Q��t����s����ǫ�B\�تcG�=�������3����P�ŔWW��r� �Y��	�db(D=��$�� mW�I��4���3�;���#��Tb�R,��ӫVA�X�ʻ����s�>�`ҙ`F.c@��4�{}�ِ͢%��-X��$Щ��,��7_��k�z�m'>�ҡ=蟡�D-��4�	Ӡ1[��( ���`u���EI��T^^$@�'{a\3D�^��,\fF^�رG�m��c=c`��Qk,C��<�`1d�}�n�pܑ�s���ŵ|
h :h#mc��.�q�B���m�&�sH��k�J4.Cq��m����	p)K���ݣr�2h�,��hL���U+V����m��B�iϻ����	�>�PX̐�0�������̃Cpc��`_�� ���bB\�/�~���
�m�]�����h��3���0��3�EKQ�W��]ЮM[��8��$f3���c���K��ڹ+��$��8	�ƌi3P^R~����[����9����)S�3r�WTb�N����ۡ�5����$FGg�{0`&��48"4��$�#�{�� aNu�dDBy��d��u�e$i��d9�m�>�삟�[�3���ne�er}Tt��wuf]t�ؑ���r
��'h���Z`� ���� Hߘ?&��<�.�(R�d����q�S�O8�;��)��'Q���������ih��<�c��� A��'���DV��,�����}W����!Ë��Fˎ1�s65K�[���l��8 g��+t����r?+�<(� m�B_��v�Yc���D�",�ky!�0)[:�cM鼺���E��wZ�����h��~m̚��\[_ɋU��<m��H���P��и�㱲z�������Ao�.0����-�������=�Y3�4�5�������8����-9&H;;�S:�W2�(%D�$�HC�)���Fڣs��Z���'�8ᨣнsg�H�D���5x4p]H�5����.8��{4�r�e��U��X�1��A@
�ƴT]YG���]\X�^�y�V}B���]t��AZ�:�	Fl1�e�<��.8���m���$h[Av��D'ds������>p�z�]vF��Z.�f��3(�œp�9IÅ.������3����E2���c�@�c0T"ϳs�
����������%X�t)�s�#������,V�
��>�+Wa	�}4��'


�'ٹ9NNKA���}m�Y����-��ǟ���28pw�iGt��>r���8� ���{$ nL�ۓXm�I�484~��*�B!I�1�t��8�䨍�.Fg!x�c���n������[{�!؉��]:uB���еsG��f{�A����q��t���9�A&��A�1�d��5���{��g��I�n��OIT��Jl�F&�y\�����\F�Q�X������3���0��۷��;W�y:�9�@.�l����j������n�����/?��v.<�؟��b|��8����	O�߬I�|"�9���4.-E6&�.8�d��]
<�J3^|�gH��4�˫��s&�SLXQ����Џ�b�V�`��ǋZ�P�҉�tNVڷoϛ�L�����t��Aח/;�/������ٳ��;U��жe+�ؖ��*�O4ߣ�� �H::���.:��G�&����#L�@����]�������Ǵ��l��N8�W'�Z:ૉ+�;��s�:��.��^�+�;���'�ku�o�L3��҆Cr#a�� ���ʈv$�U����L
�"B&C3�Y=��n  CpS@P�q���F��$�<Aq1:J�C��fƶ�?f�y�Ա3N;�������ܳq�i�������7������5��8���+/��l���9�y<'+d �́E����7�d1,p[���e����夓�9ˇ '��_��EK0�zgӝ���|�c�<1σB-�UWU�s-�l���5Z�yX�6m��;І�"�cϙ5%%%ǡ�o^3o�o���c�Z�x1�o;��������I�:8֜g��1v�&��S`���l���Tl�'�n`%i�I�#���4�f�z3���Ж��'{�S�K����Ug����8��x"��c.(( �(@y�B��	�.epP:�h��F($��Yw�EP=�fV��N�׶������4j��/��h �H����xM�BjQ@�.�S�g,�3����g��+\}��n)H�AW�q:~s�1�k��h���h		e5�2��O2��f�&n�wiid�\�>!H��c�9e�$4����Y�X�y���]Te�X�d	&�����V�y�b���!33��3�4k�-"fgg���233���;ãS�������]��oM�����يU+��<�T�oe���8�cV�w���;,��" 7�x�5��ҷ�
#OeAe����M��w4.���J_m�C� z�e	f"ϯ�G#�����= F(��.�6Fć��D+-	�I��hX2�w�+=�-�&uB�l>˄����vD��K�!߅���:9�ϸf��j�J����FR&<yXUٶ^��nl6�s��Q�f� $ s�2C�b>�$|h��ր��϶��;��3�>,�l�%���bUU�/[��K�1���]!�9��,��� �~�y1d��f�we�p��ٴ.`et�,���;"��*s��q��I�5԰ٰ�f�����8�~=�@��<���h��8�Y���n!��,	vfr&�h(-)� �s0���R49�� ��|��g0�@q`�ƞ���G����OW�0�c0�g@:BE���N�H�@��&�$�6�98"MFd�K�r���I, �
�� �C�0$k�]����^M>,P!M�� �q�ă����e=B}��`��o��Jp�0+�]&L�v!%^��r)��\�%H��S݂��@2����N=���_��%E�S�
��۠{�n�xю�<x�
322Q�%�{���R�gpFm��}�͎����-Z�t��)S��Q��rD�ѾA,0n��O�̚��V�m����;l���L�3�Z�ةձ�\J���&(���Ѯò�*܀�%	��L���0C�q`7�@�h�t�i<"�HXY�\!Xa'�/�]����C^243�@6�vq�A�h1�p<\��V��b�^p�t����4�i���)�̄T*	��H��κ;���Zr�����>`� {o=b
�Wq����A�	b�e䙈$�~�q2Dxi�M�����;�"���@Rz�h[���M,��򥅘�%��K�����I�0x�U���J,+*BmMT��I|ځ�Q]S�N;`+�_gd�0�|b�t�^���D�m ����X�j�Ӷߞ{�C��朜f"���N��H����C��k�Q�� �Չ�W�$��/��\fK���� rɀ�9�c�	�N����!��O�p��2��;e�ppR���S�C2I�^�tܓ)�c��x�T��i�%O"f���C��	��<��c��p����I���V����	�~pީXm�JRɝʍ���ʙ�\�F���O�#pr��S.�3Q3�P���J[�d���>K���(GѲ���^,��w��\�qu��6�1���������S_�����^u������ddf`U�J̜1˗/o�߇��m����G|��G���E��O���-��3kp�g��r�6pt	V@#�gw �a�   IDAT���������F2���
. p9K�4p� B�<ŉ�]���#�a����, ��n2(lp�\�>�W>��b�`3�9�JZh(�����8]q3���I7�(�O��Tm����}��1K���v����Y��,&�8 ���'���m�����%�Q���HK
�d��7�*�.���NwQq)&W�@fV������S���Ǒ�8{.))Eff2�䱊�#ut�	>lt!'�l��KS�&bٲ�f��]��6 /Zt�$v�8gȝ;t�.�{#7'��w����z?��Mq�`����NJ�PwVH�Ss �"��yP���M�)I2�N�,�M�
.�3�'%0hjo��,�4��yLZ�Ni�cm��L��u
���AJ��:$�M�MȞt2��v��,�B=�1E�
'5����i���T�x<pO��DHy
"��+Ά}���j�,+���r,f�k����~�
9r�0�GZ�e��.Cey%�E.�9y�ݦ^�3��������n�����͘����n.�L��� '����1���2�u���;�u�Xq3$7%r�'�S.���,���̟��Q�=��B|Ѭ��$���u]����:�,�i�b��(�=L�9؄i�]��/�6D'�����4�O�F`*54�Q#�գ�>fv�H���X/����ʞ�+�DPh�O2�z2�Ë��SO*�d�|�$w	ԓi�$��N$�+'�Mm�|2�B7+��4��I��b9J�8{欸.�СK�j͖i��~zPXΥ�Ғ�Щ���C��kŊzS�r�CB}�0vh��7o�P��v��8�eeG|����q�y{��+�Z�D������x̃>�k�ԃ�TM�@��{'������|���<�e� w�J��&�i�03�6�f�x���d��%��Y:hr��6��������Xp�Mʡ����l���6���(��(�>A��J����5��C��u%O�ɥ��t�2�]����P2!�l�g�T9`�>�@&
. ~P��NB�^./��%�Ga��j��"��K��50ar���t���ԛ@b�r�?�L��DFf6z��l._Hl><��:r���JNn�Z䣪�
r�	�u��AפZ�B�ݐ�����
砋������xm����YXXx���;Y^n6v�e'�#'���Y5������r$8��*=��}7���N� ����|�'�����%������Q<�x���0��f3�l>�&A9�e:��)	c�:�Ph.^��d�/��]�kJ[��z��k�4�S��Hy����g��g�4"A�z�WeCxN��a�v�	t�V�ܮs�@	�:f��2��`$�&:��*d����C^��$�$�g�IB���rR��x����w�9���P�TjkPM:����	g��a�=��<��!3�컪_��B��l;�ܿW�����:�Y5��89�ʳ��Q���,z�n����e7���yx����}�^YY�G/�ϝ=>�m�kklӣ'��9�{��t
�ש(�����@1�x)��7���8�y��(�*d���u� ��0b �]p��[U砣�f�	��پ�f⢩3n�ZS�`��t�(N=�!f�#���\�8뤻��@'P琁Z:��c♨�̪�	�_��$��:���d�D,��t�e���:����u�W�1�ږ��4��O]�'K���Dǐ�e��H�c�:��:�v�xh��B�/C��;���y�{,���/N�����N���l�ɡ�䢎�_�LTW���3��@�����9f��:����Q���Q�%@�/k�9�vI��V��w����|��m��6���U�f�BIqI�}P�S������ˏ��믠��K�~{�����A�A�f��ep@�8h�����y����<i$8����w���`�rg�*�s���L�0�CR��9�.��D)��>�H!	ʥ#�x��q拓NPG�����gd���8�q��:t&��O�N�4u�4�E���x���#����s�S)����Q5�Q��¥5%#QG�:'��-Z�H��R<�2o�4I�5��c5L9�@'�.�SVh�F$���s��.tq�a��I�� ;���){���Y3�N�}'�D����?/+.�:h�i[m�mZ���s�%�t�	�J��Vr���?����c�$�j�J�Z�
�?��ſ�ݻ�E���3g�DѲe���AO�����̇Ǐ9*�0+;_}�%���C|@|�������'����>�gÇ�/�����ߌ�W#F�k��f�h�=�ƌ��1�1n�xL?z�h҄I�<q�L��)�&c��)�1y*fN��YӦc��s�����31���¬9X8{͙��9�X]x�X4>��/����E(Y�y%LJI�	�\�l9�*�E��\��a9���XQ�+/!�b�b���O������ռ��@��S���
�VV�v�r��]`���*$�����!�0���/g@�;�U�;	:ޙ���	�n"xs�4�*�33z���$9�3���� ���W���v��]�@�OCC<2xL#�&����Q�PH/F�Dm�y0�� �3 �q�T 6�q�M�A
cFx y�r��!��1���؆C���#�����̕+���VY��i�]^�f����ܬL����9��G]�����r�r���E@onp�Е�<��ܹ3:v�ȹC
ai�jj����fG�k�@QQ�)ӧOw�a���_~�G?��$��ăO�����ŃO=��i<��Ӹ��gp��O�OO+|���qe����C���������ߏ�C�tя��y�0��GI�����
�?F�X�ǈǅ�C�8����d�:�@��ĸ0�2��|
O
C��С�`�S���3���a��g�ǰ�^��Ͽ��^x	Ͻ�2�����x��W��kx���ҫ��k�+�^�����D��&^w�+�x�oxS����׿�K������������
������Ŀ�/���[��7�����zo��?x����������z����������w��;���w?�G����O>��~�1>��c|��'���O��'���O?�׼@��p���K���K��� ���R�
�I���KL$&}���S���_���oFb�7�0{�h�9#�`���1��3b�����a�0f����/ ����X8n���BN�K9XƉ�2��&LD1'
�cǢx�H�~�5�8�(=�N���1�K-[�B�n��+^�5�������x.�����X���sr4g�ǋ��&�	y���/��[�g�^�3���|!'EE�/D3�"�=NziYٯG����'''�8s�r�8|���'�	�����d�8|<v>3���F��ۣF�#��F|���������_�_��o����}��?���c�ƙ���G����/;���#�4^x�<���������?F<���[o������M������Đ����A����+�I� �x�<���x��/���N��?��#���G_{���*y�~�e8��^|��"z�<�<������s�}{���^��&я��������Ч� /4!��Ѻ>�.��@�b��ۃ�P�x�(9�i.L�}P<�/8���'������ӏe�c=b���i<�8/��΢v��P�0���B���axt��3P�#.��<B<J��ÞAC����7�~�2�=;�'i��g�.L��ĳ��	�@$1��� Z̋�`^\���E�I^��=cJ�ڶk��m�@?6��x}:]= 4�	-k,\� ��h��s�"?\:Qz���̹�����:J��w3����z��wOsf������:�fv�Y{7hs��q�:\)�s>��3�����3N'�8g���x��g����s`�iI���38<�   IDAT�p�i���SO�)��B���O=�9�d�����������_��_����I���~��N<�<�=��8����1�ѿ�����◤��Q?�9����p�q�����?v�8��18��q�Q?�~G��q8�9�0�}�!���C��!c���n�]: ��?v9p?��_��O��O�`�}��6{�^{���n�v�	]z�.;n�N�o�|���6[�DA�(����m��]��E�����	�|�ݡ=2۵A�MkX�V�[�D�e>���P���^����23��1C{s�pet��%/!�qY���K� jqu
�VaѪUX�j%�v}�R��}o�g��aFY)���`J�2L\��c,o��,Y�х0j��\4#��7���+b��9>o6>�3�Ξ��gN��3��S����x��;uޞ2��<��4��4��4���O���0o�'ƍ��cG:�y��:��<�k�8�K<��p<���x������O�4�1t�gx*�!_|�!_|���~�A�|���0�P��1���1���0��w�w�����w����c�M���]���1N��#�礡?g�C'���EE����c箜��A�q���,8�0�K�q�zY�2�M^^�[��GǬ1��<G��:tmm��ϟгgO��<��Ϙ9�z����-�E��Ko���Q^�r�ys�aꔩ�K�]�t�����?� �{���| <� |��G0�'�{���!�?��Gz�<�H�GZ�$~X�z<�|�{�鐾�K�U�+���~�������I+�������?�	����}����=�
���{�{ލ?����w�?܍;��������;�����=n���v����6���p˭��[n��7��p�M7�ƛn7ބn����_=q���z\{����kp��W�ʫ��p�W��+.��_��.��^z.!.��R\t�%�袋q�����\��w�p>�=�|�w�y8���pι�8��u�p6�<K8g�yN�E��3Nǩ����y�t���7���.��9�d��˓~���L�D^0E���_ᄓ~��O:���D���_�x~q��?}���9/��q�����c�s���?ñ���p�����^L��߱~����c��c�:u��8��#�S��#q�QđG���q��a8���?����ǁ��=��r0�=�8� ��>�>�����N={��R��V������В�f�
�E|FQ�g�y�y�����l�s6�s�[oz0��Qõn�C��҉�fϚ���s���}�.r��n[II�)&N@ɲeP��c����N; �O�s8�tK��:��?�O��٩����Q���Ϊu�<���f�e��S��-ЪEK�j�
�[�FA��- �mжm[�_+ڷo��iv���;u�:v>d���C�.P���I�+C��8k�޽zr�m����n�m�ӎ;`��;a�]w����}��?����d��Op�~�������C8�>���pg�G~�y$���S�����D~����K:���N8�8��$:�ߜt~���p�o��O�-�N�i���3�8g�u&�9�l�w޹������]@|!.��"\r��tЗ��+.ÕW^N'~�5����pÍ7�ƛn�E�&^n��V^,n�E�v^<���w�w�u'����܍{ｇ�{yA����'<���x��~��=�P?^(ƣ�<��������?���@bЀ4p �'A�1d�`���).�M��\y�K%Os�婐���.��rȳ�0��>=�rY�Y.o�ƥ�g��������u�a!(?��g�內�\�i��嗡,�I��$�5��G��� �yp�؎Ac �ٮ�	���'���lw��ã�>
Md��yaQ_�о=��?���+�kI�!-W:�l�">\�2G�Br��333݀�<0����Zk�9[����i�ҟ�1�w��͟�����m^3k�knaႫ�p-YW|�l��#�@,��6��O�kֹ����~-���W�1�;׻N��:��������H���#�����^N��շA�-��y|���"�6�KB��ڝ�$���+ ��m��O��S��h����R�c���f�n�E{�ӽ$b���K!�ˀ�˄>��Eg����:�^xs���.�tD
�rs����Vւk�-y�Z�6�����Dk^�xn�.�mЖk�)�M�۵i��Z�m�r��;�ܩcG^�;A�.��`+.u��o�=�w���_/.lӫ��zl�Ͷ�~�m��v�a���ǎ\rr���c�$���;쀝v��w�	�{��.;��w�{�7�=x���IB;��5��F�k���p;j����͠5;��EoohYç�B�������!�|>��ڲ{���:�J.I�nuɢ�W9����5��nЦΛ7� 0�y��w�G��kpk�C��b�epP��k�f�222�����99���z��_#�f�L�ˤ���2�tf2T<&���A6o��o��3!�!���ψ��q<=m�i��tIt<r>�.@td�%w�H�ɀ*)'~ ^��������ȸ���&\X����Qq]��0E+Mչ��c:ׅsssx���8/�����ֆL��e����uʟ��ה%kf�y1蜙�o��(���2BGݳgw�>4���r"���$���5��n��r=��)S�`��E����.;�^��r3 �/F��y��1/��1�N��:�;� ��X#�� �i)��@WW�T��H�S&=��C}�R��f�0��ZBσY��N���!��7�}�8 �<�#ԇF�`�Y*�7z34��rfCPS�@�f$C�l��O�0�Fh �4�e�x�<Y�9kD'ӌ!X��79K9f��e	9�%K�����3�h׮-t�.���P_\�h� У�-[p��!�,/��(LY����+��E�ܚ�jt�ڶ�7w�\�-�9�kN��Pm]X���IS'�6^�N�|����:��[4-;�:�����1�؏Y�Y�T�ٚ���æ�Rq�33ח�39ܢ�"�v�ц�1-[�����.{=�sLC�K���2��ТeK�p�m1��$H3+��<��j�
�[�Ks��u@�N�����S��@_�e�C({6�vn�6�j��_��=S������j��ff휉�P�ƐT=���?@p�J�]^�5�K!�)�w)���b�!w�LXQRdQ^�t�R<��Z�6�$Ý���0� L�S�i)f3��T܅��oK��5�/L��h����cS9��,=sC��,�q�:�f3R�7ҡ4��tfM������}��_iI	וѡơg/Y\7���b0�f�72����ŋ
��k��y|���;@jrYk�f�`P�g#�.�f�:Gu|���5�n\Go��wEE􃗢e��D3�"�-O6��Μ2u
��|>;�>0޳W��������f�ڕ�I& `��q�<��"�L��c(�0�Zc�>2�3s@����*<�z�	������FBf3�#�)b0KƔt0�d�����Xa��I5M1��*%F�������@B���N7�zYk�Dqs�1!	3����Y�!�7��q/òeE��ʄlj)���y��1��S����#i&�øf�����I��)��|�^m>���ѣ��$8�8�P�h�IJo.,�\Z��9o����M��f��$��^}��[0=�0cWM",�ѐ\w�^�&%����{
��@2}�!���$���e���jЩ�PI�JW@I��w�uI�g$���e��nw��x�H9r-9*X��X73s�1�+����`f.����I24/k�	&٪���$-q�őڔ��݌�� I)%�.1�[(�t��K��V�\��,�o�\I��&z�Y�W3�\�03�03��jf�l���V��
��B9mW�OQfa>�>ׯH+������)�$w���EZ�jE=�ҥE�#�.�L����'z��Y�Zu   IDATݦM��:Qǎ��>���8{`w2�;����Fb�6�A�C���kC����������.݌yfu��M�	e�$����Zaf����t3k�o*�$T��@���B�'��oL�� �t�ҝwH�~�hӱ5Y��k�*��6��ff0#`��d"��Է�8#��..DuUZ�l�&&R -F]������=g6����bвEθ�x����e ��Ov�Y�9@�W��rc�4k�kǉPױ�9s�;w.S��9�oq�����Θ1�-oh�ܫW/��{G���� ��;�B8(�U�;1����"�д�����Kϣ4�J�Ņ0�P�t�G��t�*l�B�}�]��pf��1̘v�	��T�,\��,�#w%;8>)3R�;yLi�Zc$]�Z�(V�rj���$��RJ{آ�a��K��YaG*���URְa6�Czm���������e�X�d�{k�}4#��4�"X����Ξ+�Wbႅn�Yoi)P�ޟ73s:~��#63���b:KP�֡�-�߭�����0w�7�e��A�ì�^�x�uS�MC	��o�����{���&> �����`f�Л���wC#8��49�,L�&e���r�d��k����րf[ӳ�����OK�
J�f{3c4 ­)^2����5�!�`E,��Rnm�M���e,�!��#�줰1d[�f�S�������Mаt�()-A,3�N��3���t���#F������ O@K99�0�SN����y�+�r�[	���Б'������B�1��g�t�-u\H5�b��E;�W#�i�H����N���-�����X�SUuO������꡼MA�TJ�K%����cP�� �%��hf0� �-��-4����l5�֤p��?
�
xk;�Bfu<��̩�8w�0yN(gTy�$g����M%�G�צ���$K�����ƶ�7U�u�CHG�t^H+\S��ۼd��A�֔W4���Q+�x�;o���x^^>����7�a#�h)ffV�3*��03�Z���еΖJ�b1�>�ޖR���s����4�C���$��jdEE���&M��ٳ�;�z�ܻ�N0cg�uF.nf.�Ь>D�-�O�iĘ����S~!��?�Y}d]T8F�!gɺ�bf�$�$�Dp` ���>��
�GGSyh��q1̌A=��&c	�c(0W �`7���	�2�g��|�h� �[�S<��K`����\�l]k�>�(4˭}�\g͜���}�O�5�v�ه�И��SL��n�b��N�������s݁w��A+���I�h&��7g���/�-+Z�e���a��U���If�BD��;��F��H
�p*��!-]�O� :f*�R,�)FH��*y�2L��6f�.-��A��0��o��YJ��hk�]�rp��rR,�ɐ��N:�����d�ҥ��r)�$F��`t��0���,����YQ�����1�1����(�B:7=.Z�z'��,^����?��:9gAK
��e�����EmM������C"N[1]kъ�y3�d
��u�p�-���2IAAk����99())��Y3$�,9��<�ӦL;W��R��G\v�uWh}L��L]��"3k���~���YW.��@d}�2�$ݞ�����cL Ǵ\d%���f3�v�$�,��u��k("�pՂ�jx43Y!H�v3�YC�׃0��y��3w�|����<���|r�B�z����9������`^�d'9g}����gA�qZ?8��ʄ>z���f�fͦc\��̜.ִn��g�f�u�8�L�/۵n�
�弋��r�F3�"��'YF�?>Թ�ަv�u�S񪯎%��zjK�I<	ut!��
R�%�iH����¸5����ѵ�|���%����Z�i�NF�z�@0��N�8�A�5R@t�:%�`�j�*u)=����1�iQɓ���<��KO\�|�з��fҳ�!��N�--�3K�k!ۅ�/$hE1�k�QXX�g�����!ۇ��dea����@nN�[-/�>z�1��r=bp4�a���U�ǗDKgVV6���S�Ψ�?_X�T��������8�n^����IӦM��7�p�G��ޣ�N��e�������R�� 89�1�Ԟ�%C���+4�!z59���f�km2�N��l$������6��nN������[�pHs�r8�	�!~:��N���lu4VF	� �8���̅���>n&Z�RU�$�d��z[a�b�f됟����L���&�!y3C��Y����i�!S>גc����bt;��׸�b</F��8��K�63�>�*�H��i=WI[<�-����3f�xuΜY�ʾU���{ǝQЦ�o8��Z
��&Uh���$H�x �cnb�G&#���CI��;��v]�$��G�2�=�'��x�tA�c�vPÂr\U>�����JQ�	1�!��v���	S�V���z5�5���:*OS2f�I����a���W��%Z6�9]�ˠí�4�u�s.�7�%^��-�5g�3�֭����69j �:�="�Aˈ��5 �I����-Ҳbee�9�9l^sh��m�ȑ�2�/X��l�ݶ�a���)`��u$3uK4��%��״ط�J��1cL�~R�Q�$B�u���԰.ٍ����qK����%�N���
3����8�aȣ�w��1�ϛ���R7����qz%k�p0��Ŝek�XiY��n���<h��tͦ�̚��f�g�����^���T-�t�G�6\�����ә���ޖ�����qc�a���n ���ۮ6s3����k|75Y��KM�����������@��~�kȺY��?�+l5Hg���D���� ��`V�ak\��rDz�&z�6*۬��g�ByE���*��h����lW�с1�c�K0s�σ�O�� 1'�ɉ����.��@kZXY�j���Q7��f�]�vE�N�ݝ�s�.~��nɈ�:���	F赞�+��C��n��ж][>�H@J33sŽ}�vJ	r�����P&�of�)�i�`�T~�fP~!�;]����p:�{���d'��Gk�x�ʕ+�b�J�Awт�騪�v����z76���wָ[a�u��P�� P]U�AT�B��0ߌ�I��` 0h3Sh0��N3��F��t�)�z4�ɽ!�g��sҔL�K�i������_�-\��͂����,HP6Y.�����<:h&�=x/�h�+g��s,#朳x.���N�S*mP��
��`-�Qx�ڵk�t�.��e�0k�~̾E^��5jD��E���Î�a��5�8o��x�03t��C��t!�cZ�Kō�A�]���>�!��빤�G ��B�Z�J��`f"SP��਴�T��.D���.Y�K�
�.���z %�{²}�E(�9XTX�����"�SHƃ��%(/�p�,U�4�l�z��B(&Z�y���;�o�����_}����#G���Q#�Q=z4ƌC��رc1n�8b<Ə���'`��81'��@M�43f�D�bWo9=!�t�2ꓒ���v�I�*0���~�RRR̙s���jF+ۄp�����J,Z��Ec1Z�ed T��y�=�W�r�uPp33��3/�	2͂<�ѽ�V��,~���5{���=h�����պo���K��c����ؖ3h9e��u��.�(�u��Ci2�f�u������o�5�]�CV>3UTTӐs.))EII	V�Z�Z8�vkkj�P�^��1]�R��a-g����CU5\H������<W�X=HҬ��`���Y�-8����ŷ�h�s��F��ԩS0k�L>���9sf�� �/K�9|�,̦Ә=k�c&fΜ���
�c:�Q�M��)S�b��)t��1�N]'�'t�����:*�� %H��B����n�.q�隚j.o�qw9��F6וC�!4�p��;VfF�s�X0�f���rff���.'(�R�sl`�R��3�����B��Q
5;//+Ǹ�㱥o�[kKo�h��)Sޞ8q"J��u���~��бS^�ٓ�'�X�>�W������5$;�Q�	<�   IDAT\`��]u[[zSif�����L����Rik+�.�r.ah��$�)�p�=i�0�0��H���z*�;u���� h�:2)�]=Pz:WK$ż�L�4��i.T]tQZ]m�[J��T���q�.@�����q	F߳p:�h-�L���q����;��n��P�6�2f�40�%�`�]��0�<s�|8�	��bא��ΔGɛ������\��-//�͸͌����,�<�Q/E`f
��ǴD���w"���1�D�6m������?�ۢ?��5i���,0r�Ⱦ�ū��{��/��I�W`���27u�gI�Ovpu��P�t���PZz\��}�:)s�N�W54��mք���3�U�s�<���L)FUI(`Yd$/z�qT�49�&���-$9 u
�,Y�i�%��!}��B��
5��9�Y1��"�� C�꫼�^��<Z�\c��`f��B�3�.B,��B?���{�k�[��42�Aٔl\�FrME�7�蠚XT���w�3a����c'V�r,�N��vi<�h�̬,R`[CVV�s�f̘p��%C�w�T���*�n��<m۶�$�#�<b����?o~&�y�
�A3�[�-�1�-_}�%�����	�Sot�ޝ����C(�T�fA�M%g���Ah��h\�Y}�iԣ�lz�II>�骓�4h�Y��)0vF�H;)��t����8.YBz�fh3�6��t�z'm*Z�2�S��2�$׃}h-T�S�IA������˛���2$�^�j4+h�lQ��S��>B��x�p��c�F����E�64{5cݒTf��}�B�c�-!g�z˗�y�9�=��jf03���t��|�(����ZCQ �&���f�.d\&���Ez'w��w�3���]��n���~nʮ���C��CH�Y�6u)vM��TG��H���5�Y�33J�Ml�*��s�0�q�7�A���w���@�(�@r�} ���M�t(�(gf"��1==��bn����H��U��꽼r9�+��N�ʣs�<�'�,��($yȈڻ!?H�2���c�Yb^n�[��kI�{n,�M�Qk�+�g�n+��?w�\h�E�ϺsT6Ʉ'Q�@縨h)�+�9���<���%�c��?���,@�8���̸]���,�	����j�����+�\C`����?Rᖆ�A��N�4����ң{ΠwBA���{�Ng0k��F�����A��i� b$�������DU���d��zj�U3P9<�I�I�ILa�t\;T'�	)�v%��flٜ���&��u鬏n�5c�7�ͨ�<w� �:�w�$9�� �kj*CR8�Md wp�q9�o�srr�$r�`��t�K��9��L��iFS���#�ROH&��),p�'�z���.C���<�a�k�JV��"ڌB4�ڔ��� ��`fY-�<2��k�n���3tQP�9�رZ�j��	�'���l��>�GSD{>�K�W�����={�t���f��%�o�����A��C�������J���#��5C���#�0UO���ZA*(S�K�d�I�97�)`�MuR)F�m42r��}��s�Y\�gN�%Z2f�,*	���Av�P��'�9y��Ü.d>ɰP�J�$�F�gNR�x� �+�f����о}�����w"k<�I����!$�#�<��Λ?��r�FF���j��z�*|��Ы�$af��FVV6i��@:���c�G���hj�]�Q�/V�Z���4��KN�]�v���G�f͙����lJ͖��Fl�6pu��o���˰^�c�ݡ�{R�$;������ӅH����ZcV��Ύ$7#M�14�]�t���DB��y�]m�S�LTk�A��q�������`�R<$7c(0��:�6����4Ϗ�B(�!υ�O�)TVT�V���C��Cg� IM��#y�]\�C8�;�7@r,�q5#���CAA���3�Y ��L���i`��̘����Ja�3V-oh�C���%&�繏"�J�ӮĘ�+'��Y�G�Ck�Cy���.�1F�n�%�`E}IuV��U]�t���e��L���y����7d�U}��M����*t��z��uAk�����`��c����Ą����lA�0�PqAY�L�RQj�E�.A>�A��M�(��|�-nf�d���Z����k�|^��Tp�T6G�!�U��g03J��W��r����2u���(������敜�)�xB�"��])kCR�Q���rS��朗YNL���t3[��f���SvEۜ����}JN��P� �`&%>Vrmw���n��"�ݍ4�O9}I���3/lf�E�U�V��{0�.@N9�w2<f�qaf0㝏��l~��(N�����*���x"�v�m���ѓ
u�jkk0y�d��ޖب�Ӧ�+�������,+)�C���^}�5h�n� �;��1:���`W������8�[�-�#]W:$��.v���f��V���^Sf-m�a���tiV��e�i\5W+�`0���G0��z�_Ϗ���x�ŝ��0��uz�6^O933��ƀ;��=L��]O@�ب����� ��P3m
������9I�c�x#�ׅ����f�Q 3�6���`�B,������[�����<x1Z~ЯA}>ċ1��5�-Z�4��Tnf�]�XL��&�Z��G�? PUU���s��h�W�:u�=(����7�l���i<w���\aժ��~��{I>�N����S���>v��g'����YE}{�� mf� ��	�\�T�IHc���v�$�,�ߒ���̨7@{�H3srZ�����e+�%r�R��SH#�Oc0��*s���
	��,3CFfb��x)�5�:���A��+�qY$��63�%D0�i�6C:�(n�5Oق���̐��= dMS�*]&EK�t�*d��:{�B�H����xڮ\Kڦ��Sy��_����e�����1���/ZT3sN�e�T �/Qԩt6פ5���$Uh���'(�P��V�_O���dҡcG�N��'N� M����尞��t�PzMG(Z����_}ݦ�h���;
ڶeg�ց�����"D(ƛ
Ai�csW���͌��4ַ"��:y��5��Ji��P��h���r$�H?#�c}r7��	��#�C�}� ����2�`�S\9����(��1q:�r��<F$x�&�0hC�i$ $7%�h�@��q����iy�ݬ��F���fժ*L�2��Z[�D^N�T��`��lT�e��EKQ�5`3��x���QJ�9��1OfV&�����7ـ#�%�#���+�/�rc����G��֭���#����(\�`�UA�-��mY��~����QcF�]V\���Ϟ��G��\�� �3�x@ӛ:U����}�����Х0�](���::�b�I�<���l�������ߠ%S��T!�!��lY\�T�P��b<H�Ar�<�9s.--CMM��	<�n�k�mkXL�SC$�2@k:�[����Ѹ�L��C��a	���B��.��}i�ܹ���B�vmi�L�F���Koe藎Zި�Z����%�np���,�-��x�!lC�űE�.Hq9y?G��R���%���Z�޺W/H�w��6u�)N�v��|��T�Uw���O���e=��oߞ:�u:����ԮN���� D7��UG$ػ�5)(��J3�#`�(իM!,Ϭ��<���P�F�7��Z$��),�&�!��cp��X�ʓȢs���t�l���|�YM4�)/+�֟U_3wfe� ����1��m�<�`Q�T���y�CZ!����������vP�RFD�ɰ�T���9$s6�M�`����0�5+^�h��ʠ�*Z��y�6���ʊJ�1�53dddr�&�m
**��~ G��Y5�75�q�0 Ý5v|���D�����*�E�r�e=,ԅ$��&[u��z�q|���Vly?��r&�������b������C�}�F�V`��f6g}|�   IDATfF�`W�ؚ�f���~!�� d���J	f�s'� �)��"JrD�A<!��0HRk�f�F!�ہ�:��TUW�0��	�<��)"fc<��6Ƹ�O�J��Z���!dp�9++���A��P-�뤼sr�,Tl0�B$7c(�	hsA�x2T��
�#�q��Kڧs�Kp��e�e�V��ӳA�V�5(�Y�Tekjk�ϫjFڪUk�1�4��
=/�,���r�iT�	�{�K6�TR��q&�����nKv	g��r� ԅCN�����>/	wW���hՂ�cF��PM7
lQ��E��{6f�ĉ��S��Bo�����kk��e9�f�>�1�ur!c����CNY\u�d��KXR��Q����â°qN��W3)g����Q(8���9W��sa�-��䥑�q�m}���\�I�d%wr��rb�)"���9gff9��S��BJu�
)/���������*+��C璠�OuVHO̝��O��M���	��8�oղ�tjVmP��E��>a���$ՃPr�K��ٳ9AI�5�[4�6
�89k�P����}C<]`Zp�9###h3@I���s:�1��-�3���T��ە��"�wkе\�O�2j�о�m:a�xp��8�y:D:y2/�����7��~hۦ-�<�3���QGQ��zn���FR`�T!����t}(n�zn@̷��Ѱ��k�SuT�L�I7��v�#���*=�#٥�l�xRw�STpq��Ywop�S1KQ���<eg�p�3�̦$�N���see�s`�j���'�A������ɭ���F����hU:k߁�4X^n.Z������7]�K���:�eQ4�d��x:�����e˰p�Bds�Y�-r�f�z��r�
>,rc��8C��odx1ϩ7w�s8���sO2��	!�X`��>�nmf��{��9��ŋ4����>�o����y#6D����~��G�p|�P�:���-G���"�6-��gn���P��hf�8����8�Ԅ Y>�3�ǣ����e�Tae��w�U��|>g0zU�K���	3s���qU� .1uP�	�[�s��#)O�03��Ȧ3��Z��9��B���d4��K�+W�D���`��h2n	ɐb�xTD �rwjd�n��aø���"z�#�*�H�|��L!�$O�FP~A�0����PZRBg�-y��8PZXc�L߉.u�Ժ�$�:��Ϲ Ӹ�m�k̋�;P�aԱ�!1FM�JL*��Y��Y�f-�l�kR@���kjj��e��{�kr�:̞9�������K��u�]9�Ȧ�欇���c�$f��Az�v�Ia3c?^���AX~:/E)��1��=�H����PWGmMm���R9�:8~�q�;�v%�s2�8�����1��r�͝+-��C�ƃ�|8�QRZ�n�\�f9~����83�cP�b�y�߭�t��S2�V��Al%'د����e˖���3y���5����G�V��v}޼��W��9?iQ�B��䔗��D�C�7�w.�H��eFm�����$̌��֒Qk�%K�< ) e��j7[Fr����~Q��Ň�T:f�X��^��-"�V|�Fpy��oF|�5�Jv������%{��~x;�r�Y �?�>�}�C�F}#Z��֘^�!�R@�>�����_�L��f���Fj�̸��>���r5�S`��(��G(Q|���4���8Z3�fϙ��0�53W��%3W�X}Z4�c:4�;�(���H�J�(=(5�c`��E..tyR�Ng���/��A���쀦7%'S�Cuqp)�� �SH����DW(H�>��g�mڶ�c�R���j�zS��N?b)�CB	�s=P��̂�T�G�·�Y��CA��p�I�a`"�!$a]���Pwi
���]�vE�	c�رÇ��r�v|�fp�픯���}(�����>�9�;�:[}�b�� h6mfk��l����4P�tޚh�5�e
�B��4J�	�E���i�$�D	ޮ��Ly0�6��c��EÃ��N[$�x�X�Ag���6�"L��PA'S�r���jiAmR<E]�zYt��:(/�>e0���;�4ֱI^X��1EP�zu
��݌�4xttf���:h���3c]0�=�m���	�%IU������^���t�t��̰0�
>\��� �	�<|�

*��A�Mv}₊�*�ΰ;/�M��k��]]u���Nf޺U]�ӳ���eŗ�ĉ'"#NFF�{+/'n]���߿�v��%�fi��=lo�T�c��l�y�$��^�:��ɐFQ~ҮS�n슀)"��Gy	}G�S��ϛ��N[,k׮���;�������>th�e�7oy�5�\�ap`���so���/?#EE�H�u��91�eF�\!����򸌩�eO,�<)o(�v�	&�)�N�Et!'e;?�"�E� CI㠐�úFF|�.ϸ�l��_׭�I�~��W�E�ri��!]��G2�g(��эJ�5�0��yv��s-�]�	N1:�	���������98��Mc�	9��>����j]�G!q\�F��P�%;�m۶j��������8\�e]�A�B�����J'�����6�I���M߶y���N	�F^N+��.��#�Y���ǀ����@R��={�l���,����.�Y����T;����8�Ϳ����{��o�I�}�}������Uj�Zʹ�_K��(j@��P�U��L:�Z:��:F�"&@Ļ`��uez�y�SG�I����FS/6����G�)"T�D�|�y C���8>e
IeL~P%DVN���ӦM�ɧW��$GDt����CC{5Z������3� V�'Y��1��>C�9")��Q|���v�v��������D3x���(:8|������Q͟??ojtͺ,�o߾]^m�k��Ur__���o���6ڴ�gD��{eMO���p��"8'��ą��;{�����}��:��sA=�n��f������ǡ���޸��kX���D����.3p8
�k?)�ux�5Q��P�\E�9ݓ?#wsbX�}�����.֠��'���&��F��In4qhS/��	�'��ѣ�j0"Q("���!!T���2M;��|��� ��k�F!"K����("*YwM��GD�f���ݧ��A���tD��:���ǀ�	2��;�(��,����X8'�/�x�9<Ψ8� KP�10'��Pg���d��ǂنFD��r�m�u�V١�A��*� �8�F��/��n�?�8�P_o�ZE�����z�-��Y�Y%4ouh��P��M�+hg��Y���^�u���>M>n��V������8��qh�}iö��z��W_�E̘9S�{�X��d<"T�l��˃�9Q�"��d�goPK#B��h�7��N�%4ot��Μ�]��Ⱥ��#G�s��a�mwH�Pu$%^��'��y��+y�I:�Z0�L�rdy�V�'K��N7\�aՈ�kY�ޮ];��"��	�q9ُ5߱�vU�+�2"(D��tд��?b��c��oL2�s���g�����F;L��o˖m��nϏ�v��l��߆س��>����/�yQ�"Gy������V��<�u��kXE4�����@yN�}WQ����M}���|�������Э�ެ�{�~Q?&G�cҎ{Ռ={�<�;�`�j��[��t]|Ƀ�� �ETh*�XV{ҕн9\Tw>ǍnYû�n �D�d���1:�d���$'�a0���	y+auN=X��Ȫ�;PF�O��1��)��
�[�xŻ��P-��CD���/_��SZ�tHDt��c���t�}��,�J��N2����K>;����w���24ʴC�"T-(�+�ϟ{��A��2:bB�:�Q�f@�z:+��i�8a�5�a�^�⯹�[�V�P��?��w%�(k�2�x/�3�e�����v�T��d�|/����*��&t5�l�vQ����ThI
����G��# �<   IDAT�Ԩ����z[rӦ�ڼy�t�u�~�ʏA+�e�l���n�^^Κ5K�_�̞��$":�#�,�}=��:D�"Ơ@j@N:����u작p^p�\��^͌���*������RȽ1�/˔"B�g���Np�1u'�۷W�wf�P�ϊ f(��&?�郜��PG�uQ��U����/���D�]C���.��'�ԙ��:Azwx�bÝ�)s5����AK��p��9����Wэ�O��S�b�)�d%���VQ4�I�J�2�>Yj�Q�c�-��#"���������w�w~�D��ѫYt<x�L<�O�{�o�=5��MO���k2�_���S2/r�j�U0(��C�:':��'қ*��kjS��T8n�Ĥ��<��B?'��1I)�6M����#Z�"�]8�P�#�5
Ǎ:.X΄N�f*�LJ��q@"���k�E���c��O�Ç�*�e�2mGD((��#�4Mqd]Yg{�rv�������KO� �	�G�"�l҈�OA}j�k���^z��u�q�)Ô������ʽ���0fQѕ����J���ù��K[�}��߯�����,�e�>q�i�	�/]W�LNgdu8�)C�ەL��?/��!ⶡ���|��]�c��5:t�ȏ�W������������z�Z�~�mj���z����*0�""��'��< M�-�'���.ϼa�lF7Rx���PD�����8p]�8=�8LDpV�1Ι3GE��A2A��͊���|$v�͋%ctt4_*�>emy���?�U�2H���)?"�l�ǣmooo�⺌�L8ET�6�y��Z��c�������P�en�i���k���(�D��K�	�{
����Y��8묳�x�"��G��1�O!���2o�w\����$��L�*���S'/m(��l����^M��Θ1�Ϻ�����j�3��;vj��Q'a{��r�(
� �����}}}�JLM0�2XV�dɐ�Z��$���_@9zD�;"4:2��+VhΜY��Q�w��O�E�҄�=�����oݶ��n��F�W��;�����0aG̀Q�18"B�f w��i���?�uEݨ5<�j���m��k��d�h?��;:�#B�*vN~4kp�\j��j 1�䙓���H�W���Z�Ŷ�L�������?�i̘1S3f��Y���Z�hq��#;���t"��=^u��EZ�t���i��d�d����7����zzz��-��)�:yA�y�+���0�ȡ��mJ���K��~��:�s��E�QfE�Q�,����ᛘ�N3���"�G5:��1k��f�ص�pSs�n���;�����u�>���~��1�V��Ѓ�ޱ}Nz7��L�/�͘>S�_
���+g�[D�RHv4�#��'���dR'L(=Ԧ��#��T�J�j1&�/_�7����q3ٱ�J<��m�v���֯{��]������?^~��m���Ԟ!�q�8��o���--����FjGv�OV�eMv��P�b@�Фw����ӂ��� +i�j�@'=w�`:�y�t���i���Z�`�|3\�p!�¢Ee��?.^�Xǁ	h�?fG�j�����LD("�v]2Z���~Dh�i��}�u�e��x�ez�cS��z�c��~4�GW:�=�Q�R���#�H�ǥz��G�?�����T���s�9;�aΦv�v��:7Fq�g�f{�����8h'�!�I[�
t�GSF���`�q�s�NmڼI9n������;�뫆_e��3N3쀧��A�:�uaE�q��(�l��	������$עH_���G�|:��{�g�yf:蝻vh��;�{!��Y��&��tb{c�Tk�X���ӗ��:�ڃ�w�O"�X�iF�6��NRDd��`1y:R��'�;mЭ?%�L"*T�����B^avÓt"<�'��B���~�O��G�~�8�I��׽8����"�Me7��o��M��A��d�����/]�T˗/�g�1+��
�����I�����Z���e�i/�"*�g'8�nhsm#Bnc�=ٷ����8x@~Y���;u��w�ƛo�u�_�k��VW]}���M
��ז-[�	�����M�˲��ڮm`�����c_��r=��VH�<t���6����r^����ED��F�y#"�3M
�)Y�G��Q_��S���s���O�=B��I���1x���:vlX������/wꩌ�����̝;w>���ڳ'?�y�9��&�����0��fM�G�"�c����#�2&�"���m����uyݨg��EM�)�-'*mG������V�E ��Ϝ`tr�D[�\�߀��d��W��N<)'kyuڊ���Y����7�q���9��Qy{���p��ͶGG��GD���رcZ�n������_?�o���>�?z����׿^��ۿ���������7�ox����oԛ�h�&���������w�K��G��������Jݵ�.�9�_�^��|��g͚-%7���E��v�v��q������N��MNio@"��`�ȟ�(�	�Ɖ�$ɔ3���G"9ʣr�s.�
��ް��nnU�y���S=�|���{����Sũl���}�-��f�����9���>\�r5P2<T!�:�GaH�Ϫs#�H#B!��{p��{�e���vP�0N�D� р��y�>�T�K��8+��J^�E�G� '%��;䵛Dq7%frT��19/��F�e��	W<WA�l'b��vZD�U��FFF�m�6}�?����?�������?џ������{�>�������������Y������_������o|�k��׿�o~���_�W���򗾤�|�_��O}J���C��������~������W�&��F�l�0SEOK�9Y֦�B����7�ul�G__?�e�|Ӊ�Q(��vЭVO�#*y}d�#)qX�7��`����*��Զ�A�&ƭ�J��Hn�-�=R�h�Z9VΩ�������5����v�,���e�y����E�
�����"���{�*`ZWgfM�s��m��8���ѝ��"�����*x>U,�˚2ojO<��
U>���
������&b,-"���:��ݐ�6�4�@;��2"��b\��,���6*�T�	Ys:;�����^��ʫ��?����|@�z�;����]�w���/�կ��n�����ق��K��'?I��ٟѳ~�z�s��_�������{����g���g���?V�ȿp�|�����~p�X���>����������˟���u�w��xi�������&x[��V�S�F�}8�i��P�hͷZ-^��R�*a��:����TGv��J�ap�6���e��ȑ�� w��w޲Z�re�� :�7�={�<������_Mq���.qێm/���۴e��fʏEg�{vN��P���$ HN4�{
�c8_D�t಍�`"���j��FG~�̽�s�Eg���>��u5H��T��'�/�Q("NQGG�{ytl��G��v2\�f44�z�:�p[�}b'�}e�r���`�����+�������z�{ޣ/}���ޱ_�>��O��x��Я����җ�\�����o��uz����~�-o֛��+��-з�����7�����ox�~�5������z�K^�����?�]t�y��/g��#�����J}�_Կ��g��/~I߹�;Z�f5���ߟ�زU��C�S�������G��}
���w���m^
B("�h(`$Wב����W��+Y����ۻ�7�?r������g��~�Y�ڽ3W��?���S�/N5�﫽�׮��m�ߖ+�E�������Ǡ񠃕 #��MM��4˙:y\�u�T�ufpZ�����
�"Q�5"Rcb9)�O��S�y�jOj�tWU�����8B�P�Qv���]=!����-M�M!U�؉��aP�{Ѹ��݊�:\T�-��]�^_��W����Oo`��mo�#}�s����]Z�r����)��   IDAT�'�9�y.��z�[ޢ�����{���z��_��������>M��R�{���7Y�%��Σ�iZ��4�v�-;c��#����_���ԋ_�z�+^�7����-��&��կү<�����<I���еm^&�պ�k��o~[��O��ϰ_��oKW^}/�b�1^!O�>Mv���\	;h�s����Ed�@v�@87���u��"T�������*�8kǭ;22�3�:3�]:<|L�֭Ӯ���C	�l(NY�����2}A���A=�J��"#���A*�)&���7��t�R�ɕ��@AMv\���2#�^g\�D�VC2�[�>k�(��=��Y'{���TD� ��)�cʔ{�P6��WD(b<�a�2MD9wrv��/宸�����W��;���>��v�M�5G�|�#��g=�����g��w��~��]�>��_��}���a�=�Q�G�x�衃=x@����j'��D6��G�}�����7��k�'������ҳ~�����/�il���o�~����[o�g��3���Nn�h�""��O���Ӟl�EΙ4����#�"-G���4M8m�'*Ss�cm��Gއ�jZ���3<<��ܰ�-�(�v�]�L(��?�y�{�m�ޮ�7�@:c�rV"���ypr�}�S��:EDH�&d�!WBScLV�Ff�QeV�wKi�&��u�Sk��乶��{�����*���d;�TȜ�SDw��I3v�U��&ds������#�;��0|6
Js��L�d)�9`)�m����;��L��_����G�}�V�Ί�	�{�^��W�/xy��?}�����j�9g��U��Hb�S�B,y�Xcm�'܃��T�T�e����slD���B[G��u�
�y���gH��v���rŲ3Xa�������?��?���~�h����xEzp�~�\\�`���KĞB��&(�-�y{��l�'�㴂^�՝TWQ�HŦ�ܨ��M���_s�W?}�f�mټ��s���S��{e����Э�ު�CCZ�p�.��"�[0_�p~�C,�	����Q������-kx���F�P^��O�^�~�c2����~1s�������Ox�1�a����r�müa���uچ4���#�	1F-��be�M)O�����L���6y�`[؎)��qZU��8�n�+�ɕ���s�ǺQ�!t#gLI��ep�v�ܥ�|����_�U����H�6�� �'������}�#�K_�2�s�y��i�}ޑ��\%��Q���N�������a'�¼�=���wG]��`��� o-�5]����إ�8�]r����蟾C���g���5�m��V�VQ� nTP��۱}���ɛ0��@�P�u�M�fRɒ��ȌN%�Cbw"��������(dh�Fkժ�ͱ�����Ν;9N�Sq
�|�M�馛.^��<+W��Cx�+vm�Ⱦ�5ҧ�"'I�q�*�q!")�s���N�r�-	��Lp�M$q˭���[t+:o�,�qԏ�n��v�q�����g-�o�lظ1�Aj��l#j��N����&�m3����l�E��O0	<6@��6�Q�X�lFoe붭�qSw�uW��Ύ;����ʡ��ڷo��nH���o\b�s�Ug�EDR�SDt�DO:�=F�wF�.�^NO,1x��g^2��z&�m�a~��z�;ߩ�ɾ��^)>�}�>����#��~�ٿ��%�4�#-Q��[�G�3|T-V�-�*�X�v�⺕	�C^�m�*��l��M9Z蒈�mP* ��e��߃�lR����)ժs���y	����s���~J�͚-��}�������ٹ+?��y�F9vT����SD�
���H&�=ȝBL�~4(��P��(#�8E�"*خ�l�D���7�U�V����޴i�v޵�M��F�S��{j/���V�]s��ĉ�����J8��s�r�O�܃�d*'�����;�ֱ�k�Ny2war@��䕽���	9Y-{��U�WӴ-���}������xB����qv'��?r�u�ھ^�S����<b�S����f�a�zm��v�+��v�Եe�fmf+i�ƍ�M�Sw�[�m��b�okV�$����n���7�ۀ?V��m��~����;�I��D�I1�WL��Ģ Og�K�ת��������:��W���"����Ώ��_�@�{��~��z�s��9s�f�Zҟ�*����(���-v�4WÔ8R18V�ӌ'U�=���.̩�/(��̤�8��R�h�mqtTŁa�z�E��7�A}����gk���i�;����ޱF7�x�<���PoOo~��N��5������8�ETDp(�����myE_d1ܸ�ԋ�%�/��ٳ$�k�7�y�~��Џ�1s�̫�ěn��[7�r3lH��:��3٫Z�q���a�d�4��jg���f����b�t�GDF#��d�3@��Zȡ�01`3�� O>�N�?/y��"H�\�0�֘A�ND�h�jӦM���Ы>����
-��7i����i���Q���V�(
q�L5��>c����Վ�7��8zߘ�����7�7`Z��6�|a���:fGe�|�����?|m��S��|W~�{�1}�~������ů���74k�<���v�-V�=��x�S����I��;w��	��\e�� �ܑa��C��<E���q�)w�����*�)�w���O���z���O�����0��~�:J����'?��xӍ����5{�����DՀ���x	©�	D�E`m���e��@^��Ej��y����z~j&���)i��0��믻�Ɠ~��3t��˿�X��"���z��x��-y�-��x)�N��dhR��Gq���G�S�`�9����*wuv�BG0�� 
���;�.��T��|��T���U�;����Gp {v�a��KdRQ�D�"8O�T�'L�u����2��qvg�&$�D.	zG֬��� >.D�q�q�#B��z6ev�.�,k�m����E!o�����������ڂ�X��������{�窏W�~,y�#�*X9�j�Wp��hUT������F7�Q�,F%V�NK�N:��Ȫ����4�j�Z�q�8�Z�i䍢Ւ���g��v��z	//��~I?{���f�Ri�3�[	wmݦ+�C������W�g��BY���n�����D�"B��AA9aN�Ї!#�F5���E��2M[�m�ڵ뼭vJnsx�]?�������R��3�ҹlo\h�� ���∨�� ����T�v�^��LVb2�%|�EY��T�a�d�n$�u'?
��Z�'�����P���*����*e�����GP9A�(F8C0׀h��HՈ�����z��ގ������BDt�"B:`袬3:}��h��rPN�(�U�� �����]��G?����o�o}�����z��]�\Kr��W�-�0
*��WPv
"�߹���c�QN���x#�>e��nȅw0AͮD8�#�K�������s5k�*=�����7���.��f�X8F;��W�#P���>�oڰac�\���i�Y�x���B#�E s���lDM1ҋ/:ZEK��G�{�4�8c�f͜!�Hܼy��m��U�`[���I��Rxﳁ���r�m�ɏ����\�e˖��7���@��J#B�U���POr��	
OZ��wE��y)��y��J8əiN�.�h�[����±�I�|*X��7���R�WbS�Q��&9&c�5m�٤�\�墼���|�#��PD������&e��J�x�JR��� ڤ�-�5��n ��VK޾�!��ü����W�ۿO�>�R��u�����ӵp�|y;c�=f<�O�)
�Xa���A������䃶W�A�^j�l��&���z�v���RAT0���J�]�vD�
�5�� ˾>�i��U+tޅ��O|�~���9�Jz�O�D�K�|�+���D	�ϙn����6H&)��0!�	�C�T   IDAT�c���SQ�
hD�/����eq��~��b{S>6mܬ�7\l�T��ũf�=���nxӆw�+�ŋ���9Ws���r
.rD(
�&��x��ΐ���!y�I�{G���i�'��}+�j�9)�X���R��:�Q�����z.q=��<�]gWU�a�R�ɫf�۱c��D"�>U\(I�qw
Wj�)�����I�=c�t�3��_CD�E�.5�)O�ѷ��$;�;�=RN��������F}���>�oڻG�~�c��W�JO{��_�奟��h-�z�Tps,�MS�G�gO�R�s����P��WT�,��8gu#ퟬ�� ڟ(
�6-	>"��s}�*�ӝ���}у��'?Y/��q�h�"����[�J�_�n����oh=��m�s����=�%K�8t2S0A������hn;?�C��c���Ӗ,��9sڼy���yg&㴯J�9qeNK?��ض��t��w�zY�!�z\5�Āܓ��I���<p@vt%������i��Չ����ʛx�(f��!��{|x�'ח�|�o4qr�Vy,?��9t���=Ϫxҫ"��;0#`T������L��$�R�G����?��ꖝ�M�����O��?QQ剈qI�t��N$T�`E�G��HD��ի���<��C���������S��d^�k��W�E�Ro�z��U��Z=l1����v���H��e�D��$�')�&44�6�t��y�O��|d{�t�6���f��-܁����z��C1��ףb���q�V���;��}�.Y�X�p(�M��֮ѷ���t��ܤ��kYbS��%6%��r�
��P(�yX��|�E:|�p�ϒr�|�؈�͝����3���c�vm�x�v���L��J���J��s[�o���k��.?^�G�.8_+�Sk�`D(b��1�q<ߝ��moz�ࡼӷ������rb�`��j	Eܩ!���GD("j>�$�R�o:+�i����It&y��@d
ŤJ�	c��c��s{>)����R2�<�}���͔�*��%ȼO2����A�q�)�u��0o8Ö��������������'��/�u=����//��W�|[8aS;��ya�����ЄÉ���	1O��9������xT%���J��B�呇1%��� �P�@
܁m�"`{�D��ʿX�H=˗j��g��s�~�1��%��=\1T>ZE�������������N�M�ZھD���uL"� u�a%N/%̑Ç5��y��¬Y��m�9s���о}?�<��S��{a�n�����_�N^���z��g˿[]̪Ĉj D��*�9W�)�v�D����(�����#Wno���
m&T�B�C�f� �噓�Z3QsS�)03Km���g�$��:U��Ș�>gTm&�����(U�qgJ��t��6!�4�}3G�P*qJ.r�Ooo4��;>�)�B�P�{)�;m2�Qq>��0�s$�ۿ_�(�����j�������ڋ��'=Q��{�R.��_׶s��s�>7ʌ-��iq��Za�y�r1V�D�x�P���ӧ����Q���˾i*�㮕�<�� )�"3�(�d�N2�8]�����Z�P}KO���G=R�r��t��D�l*�׮Y��	6�����N�0J�nd��uy��D���q�ˍ��g�ܹ\�Q��+m۲���$���������;w�T��\��,�dP�1�=��܍��Ň3IpBF@x߂?
t���������2�p������CTy`Q�q'�q��5Ј~���nR\��k�r��r��\����m���@�L��C&��"@%�B�yq�<tl�1�9�8������3�*����q`�WJS��sb�oD����J�$�|W�9��̉��/}I��G�K8�x���b���w��O�����8��Y�$�q�+����2�UJ6�v!����1�X��إ��ޮ]߿Rۿ�m����ët�m���qح
�Z'P��2dz*�JL���E�1'B��C�W��.�/�b�F��G��x�N�9S���`�?�[o�M�\{����-?�IUZR�YRDt ���L���=�9���!�9�V2f��~;}�i�;w��t�7nL�T:��O%{O���4CCCO��Wh�А���.�(���/�(��6�]�'�F�a�P��Dz�CD����:$?�9!�t�iX`�3S�+���<b��)K�5 ED&+�CY��д�ޘ�5H��n*����a>r(��ad��5(��"[¼���*>^�N�d�5e�ՓO��`��ĝ�B��9_�OF1�2�����膈Ky�/""��ƛo�{��^m���J�b��/��8����j�Y!�Z��j
�v���*y�� ukD���O��Vq��=��o}W�?��Z��w��?z�nz�[tӛߢ���6�~��k����\�t�l����0���@�+�5*�+��$��%G�� ���5i/[*�Z��,z��c��<�"�bU�V)5�_ʡ�u���x�M��֛姱���uD߰�g��֩x��ׯ�36F�iy���I�v�g~�7���&�Ϲ��2O`h~����ۃk׭��-7ߢC��Ϳ��䷻es�Y�w4Լ�a��΁؀� t�A^�:���^�d�r"����:t�(��Z�!��y\��}�%G��0i��Vu)w*3�m��>r�����*Ղ
��/c�9H��ш*��-�
��8G�{�|�`ۘ�����L#%�_p'��8�R�о}��g�~�n���bE�+�����'i�n�� ;f�HK"��1�h��mᘅ�
�k52�9eFJ0u	�b�`d�6���g��Oߧ������jϵ7j��4�z��_s��}������o{�����b�*�Nn_�J�R�����`ިbyvݶ!#Rf���P9}�t���a%�p�b�����.Qiv��k�u<t������^�Z%�.�e�2M�|�B��x��[\f����G�~�;;jD������:��%�={���-�7gکt��t����������X�����/Vs��ltx ���CŚ'FS����G<!=(-<�r-mK�L��0��u�|�ꙗ;3g�P�2�l,U�+c�����c�R��ږY��eA�2R����|ʦ�S��ݝ���Íu&�h����;g�/�""Y'Up��dʳ'{������u�/Y��������y����g>SK.T�l�����nE��ʺ��#A:|H�}�"BQ[_�1��+��9�k���I;X���왳��;M��%���}=���a_z���\y�n|ۻ��"��X�0�6/X>d�EB6*q�*Nw���ml��bk�X�L=�/˗ro|�t֜�8�Pe���ӣl�����:��z&��5� 3�%ɋJ�`L�+�$%��Ha!qX�X-��i&���'���}7�-[��>O�Sq��y����7��Ι���?�Q]҈�V�%rr��`�E~�Q�hQ�ٝ�)Ѻ��&�ï�t�]�84�#B�$���+�i8���#B�GSwC�%�'��'�����x�Յ�%��<Ad���D!~�3}�ta���R�ӛR�	�*Ch�NJbi2��m4:�k��	�y�z���>��u�Yg�%/��q�
���ҋVKE0����r����FT�BܤQ��+��U����2�B/�_u������wxT�Գ���!��l����h�Z��U�O���ڦ5������@X�����F*��1���5��V�2,@7@A���4f̐V�T1w�.y�����/�^춨��1Ů��_^wݵ:Ȋ���q���dJj52(�ICHU>t"�����R⥤VQ�?�x�it}[�w�Ԧ͛�D�)�S��{h�֭[_s����+�V��%�X���D��Y�`)�Bq�R'�:ލf&ѓ����#pW]�B@�N5q>H��N=}�7S*�TS���
U��>^Θ1�O�aP�y�������{z�/L��ü9;�
�MB�B   IDAT9ٝ2�Q{��Xz7�de�SD!�Tf��G�&]��>�4�e�vBcwGP3֛��Q�h��!��/>�;׬aX�^���^+>P�P���(h�Z*�ݐ��;��Y��D�֝���`�@��+���0Ż�l����Q#;vh�!mضU{(��.5��B/7�^V�=����MC��W���׫u�P��,ve�j>mAV٦�	 }dQC�S��p[��t���fN��2nd�*�b�~鱗�2��t�D4��\�_�(�;��7�xOF���6���a>�R�RI"�������Ւ�T�>�e��=~�{��ZȓN��ܽs7�����N�sq*yol�����dۖ�����E�t�h������Tp��.���Tq�<�VX�k��uvg�������t�Dt��%*��B	x;9oox�F�D��:���H��������ĄɒEL(nB��B�*#sH�ԇ�h���or��f�1,���N�@���� "pbgᘮ��'?���O��~꧟�Y����G��G����f��]�T��R�Wx�r�-��8����Bu�F�"B�@��c�3(�ܻ[C?�N�Ԏ}�u'�*��R���S��9����{T=����k���w�V�X�T�܉pZ:������c�6�9J��KX�Ν�����^�����i�νMe]����u�7j�Ν�����N:!�E�A�fK��Q�G:zm���Y�e'�y�c��'t
��S��{`�7��uc0G�.~�%Z�l�z�H\:ED�>Ǹ��|ǫɆ���8\q��������#	�*9��:t�JY� � <xg��iDx�<�J�Ƃ'QI<Y�r�������FV>[
��M�m�'M��}<"Og�/n6R�GDE�7���q]lSR%�ڀ���u΍��U򞩷Wv�٭����u��͝3K�~�+580(�
�|�VK����5	ǩ�H�8�E��SF�S��H8�7���}:�k���|�Q��v��:?lԢ0O�r:�P�@Fku���#E�c�������D�:��e ����\�ۖt��#�~�oX��x)�V�v��z��%�-�(G}s���(����u<��G�T�!�~,��,�����.3��fΚ)�>���A�Һukx��r�"Gq��y��ܽw�ӿ��+dSp�q�Z�x��\���I�*�&U�>7���JVq8�ѱ@��z����P���4��J�����|�<9`,1r�Xf��$���I#*ގf:oڽ͡qGÌt�,���}c��lDU�'{5��28Ũ&S���Γpk�r�Ug�h+�~���U�PdވP�A4�	���q��n�˓�p�o��}�_Woo�~����ο�"�p4A��V�������^/�B�(�H;7�PgJb��%-Q��i!��m�9Y�h�K�`���aW� u5�p[H�Wp崛2Ҭ�rr��F���t�����/�L8��1��c10 �j�3CϾ��Z2k��ݿA�z賞VK�٦Y������^���ں��a�ن$_�B�ў��Zj�g�f��}�6�@�p�B-��@G���mڲe��u�\�S��{`���k?yˍ7�+�y���a�x�LK_1����0$�Ϫ��gǍ�t���tI;lD���/�lC�*T0c""니ԍ�a>���c2К(� ?���bЏvU<���LJ&�����.�'2�dB��iuĂY�jeX� L�}"?A��q>�������-0j+:]R����Շˬ��	_�6+^S�#X��8��/}AC;�hc腿�"Ͳ��\Ll�Tڢ��Y�f5��/��?�C�@Y����	�:�QQoZΥ`�gF�
�5È�����2M�2�\y��X98�(�$���R����o����ˆK���z� Ɗ�[��Q���7$�Y�E
�~~�ٺ��>��a�"BEjA=μ�q[H��X�1:R�%�.&���"j�_mj0B�~�u���"B�O[��K�bj�?��f͚��9�j���'i�}�.��Ẇf�G<�R�����r������\�T�>9�H���5,��cAP�WvtV)�h�@J��'����YIB�걞p�e�:�"H'�VADS�:DL"#͎�/[���5Ph�Ċ�7��$3nKZ�.�q�Q������ճol)��D�a����8.}��u�9�q4�=�׬Y+�l�4�O��O�G<��3��ױ�#_��0�[�%རL��(Z�(�1#X(;�V�:�@9^�)�Ι%;�V��2��?���BUz!��>��%��\�8D�("A6���ؤ>��Ϥ����d�\B1��� p[�«i_���T��l���/�*����ـ�'�n��v�ٽ���}H��M���I p��E�O�~��	�_ׁ�-\�P�VK{��9�����?6���#�|��_g��H�����	-�%��/V� �����n��Pv��� �8�A�qt"B�������%4.���:(���>�r���ݑ4�S�Й3g�V��<.,�9�4H6L�G�ü<"����V���I�b�7�,���	-%�G�y�T�#� �H�<}�tczSp�D�_��]|D(�B-NR�Wڌ�^�}�{Whӝ5opP�z��5��̒UbI%}�t�!<#�fQ�%:��_��P��!��!rG�4��,�b��͝-�F�@��a��L�馽��3oP�cR�����)&d�����j�͎r7!oN$X�͸+-V���!�V�b�9����ɛ ����7�&�����Q(l�E D7"�P����d	�Ɩü�q��������|�8��>fϞ�t�{�L��Q�6�#�n������*��,&ե��Ts��!nGZ���#�̹�Q�4��܍1����u��Ӷ�:�@	��G�z�U�G�>7H���6P�xy=�a�P����7�jh���T�I'���ͽ�&px��>�LuD��Lj�
�8���heb���*Wq�z�ןޘ>�?�@�E�|>�l�o�ш�N�K�'_�6���U���/ң���$U������AAr]��_�ȕ��ע*Պ3�G��A�t��V��s!N��WϜ��ʝ��,��p�� 9���U�`��G�
�{�ԡ���P� ��pr�̛��� [f.U��P{��g���9z܊�:c�,y[���,D�%+�ȝ�6{�
���o|2Ь0�(r�5>Ť�>�*oğ;'NR���E����kppP��sky:ڽc�sP����Ɠ6p׮]ϼ�k��?K{R�w��:�3x��+�]��$Q]p?#�ww�U7��P�]�OAp'+2�Z�B]��Yy�׬	it�0�7���8�mF�]��j��%�Q�"BF%��Q0!��8�����ݰ�趯��VOyT��PD�� a�������^U�q��B�� C�u��ԍ��$��O���Wz�(pf�����喛u��7hp΀~�'��ysU;��:v"O
qW�X='�D6���	<:�v铻y�9^%(�H�B�q��
����K�;��+�O�l��'�Md��f�üi�w�R8�~�+}���qr�VƗ��\���O���b�fE����Q����5}���W�I�#��+H�5���4,;r䨎�6�$zL�M������]��ҝ�ֽ��tp��&��}�Z/�ַ�%��艏{"��ي�
*�6%z�6��x 1 �fD�֨���.=�/���^.ʐ#�;b���L(^�c�<��N�i	^�D�}�zx9�22��>�F����>�py� �PD�"P��N�I���1����X �>c:�OωAE�a�2]�;14�$�����. ��4��2���U{�(r�rӖͺꪫdG}�i�ɿ���޶H���zD�8�]�#�_��1���*6u?uö���;2�R�:��W�����tyb�A	r��ŲD8��҂m�֌�� B���RJ��<����H(�"�A}u<�2|D(�=�j�[� ���p	����Em�A��]��L��[nQo7�VK{�E�S4ʣ̆ӂ�?��N   IDAT%� �S
���^ ��[�hsS`�4^�K����G��Q�6���;w���|��?�;���D�1߂�PD�ڤ���fLHc(0�3�J$�8�_�LXK;٩�|�3��rR�J�D�$@P�pIu��(�����ǓG��h��Op�������F/�P�#B7i���Ǎ�i��Dp��vu@�Z�\q�ew���g�9�I�fb*�4�+�͏i�皶�:��&�:�2[_�n����jy���.�Y�#�G�)
;#�CXʃt.8���,%'q�w*#����#����ā˥���"������x��Y6<�#
��Pk&/3B�0��2[9��U�m2�e�j��,��JP"�'CRa�T�f�e�������Oי��P!��[�B���w�����E����P("�Q��e���kV���A^19t�2y�K�sX6s�-^�X}}}�{O�/�n������:}�5���r�J]p��i��ōE^thĸ&GDGg\�q�1A
Ę�\�b����l9	Js-G��CE05*�s�çD38ޕ�.#�e��Q4�:*��'��lD0i�[�)�'�'�ˏ�'I@�*���Zi}}����Ο� KJ+2�t��1."2��ۧ�����D�,��V�I"���b���J>��Mz�R@۫V��c��T�w����\=���ԏs�*"T�ZP%�L���A�IPnF�;4�:�+Z�f��O�q�xy����N�D0USU~J�]B�lS�e�G����<�������W�nˎ�]V7�Ⱥ�v�u��!�s�cZ �%|��;�蟦/�9��iZ݇��P��@k�{h��ks��R�\()��(m/\NbN���!<ֹ]����\��z���'��q����{������
7���g|�����#�q�=z�e�e���y�`��d�����S�0�>���@F��H�(":�B��ȸ�cl�%7VL�WuTB�m��{��V�&;���v���]w�O�<�LC�ȓ&���6��ocX�� Ӝ>�<�̏�*�e����l�DP���_��pd�P�9U*��Y�I[k~Ӧ����g��w~�C/A˜��6�Ovv^�Z���)��'_#c��RGN�TN�J}���R}��
�*jm���nJ)�	�Jli�K	���;_�ͮ�}	R].u�u0W��suDS�|d�N�+lH�X)`C�F�Z�� �6N�;W�-Z�Eӧ�{�-t�U(��m�ڵ9O#BJ8Q�l�F�2Bl��z�I
�\_o�.�~�Z������M�_O�:h��q������w2G__���y��(BQ�hR2x�w�UfJ���D.&���ꂑ�G�޾>���2�)�r��A�:Up�c��L������N��6������Q��������K�bm&n�n�l^Q(� ���N�����;�,/���n�&[U�cp�������Э�:���H�7�]%�9Ӛ�RR��lX��M��u�׬VOOK�rê��B�2��ݪ'��qBR���ԫa��)�r3w��){���'��Q�
���r��:V�}`7�Z����NI��U���Q��V�*Zʕ�W㵓e��(�u�.���6��YoR��#�}��c� �B�SHls�m��Y�t.���l��^Ԉd[��^(eEXn(��H�}�*���
��E`�("jqM�e��KN��m�ҭ������7=�����V��ڽn�Z�z��*$x9���>*�4�dQ]��ptr8���'{�*�shMR�q�s���x�-�4�V��P�E����x �^���`*����m-��9/[���s��QR��������T!��(���.�((�h�*�C�ڙ�hT<š@@�:�e(����[2��Q��w�=SR�f[ک���M��i�&͚1K��<[�G#�����B(��\�p���q�U6p|JX�I�:�NA��v��������y*z�It�����uh$�Ȇ�����%ۋ���s�겍�.�(}�`|�O&���x|��e���\r]K���y�u�#�2g�ݗ7n̗�y5������8q`�
�'���B��K-UU�7[��B��Y�\s����@7���۳{�/^���������kٲejs�J�g��GTԑ�PDA���!��t U1`~тZ�r���bd�E���O.�ki��̗1�I�����ܹL�a ��sfk&k�o]Lg�ۉ�O��Y�f��;Mg�u���T��S"Ա7"�o��.X�Y�W�0�T�L����ά���8:�sÎ�����L���іӝ��m�ou���Ե"�Bi�&���	Iwm�h�|E9Ԧ�[�/N�:\x����#�"n2ǒ8������q�H��2EP8j������S�8���z-�q����b){�hnܥՍ���!/�T ��	죽Yo�7���s�;�z����l��)�CA�BY��w
m�hJqԋyiٗ5q���}<�w/��+.�Teqn��*���?��5�/զ�G����sD��2ϟ��NW[.����7��h�X8�;v>�ꫯʎ�g ����9 ��X_���'9�7��+VhE��+W�X��Y�X�R�V�ҙg���y�>��sd�w�:��t����.����/8?酦��9W�o97�Y8r?A�ۦ��&p�+�{�-?���r-[�\K)���K��iK����E��-��7����\VIs�����\�&�~��Ĝ5{7�l@������*�>�������$��C�v=>v�ܩ͛7���9���/��q��r�^���
���}ƘS���0`�/�MW�ۧ��N��3*�{�Uk@���a
�s}�v���!5�ª9������U2���5�������%a�Js��ږ���6M�񔫒����qJ�^Gp�#\�v}Cj����4nZ�2>�5lgmٲ����z�5~��v�fmۺ���oR�*����'=�1�h��W�Ma���9��$���NpD�z�5��l���`��B�8����ju� ^ �Нf������듷���ӦiZ�
��w�<!�	�:��1&G-G;���4&���1��Rg1�OZ�p�r��}38ǽ��
n>�|�g�h�f���88�h�=�\��͹���������y�\d�)gV}c��{�e%��|�ܤOE#Э1�	�-[�h�m\��<�Wp3-�/��tԎLz� �i�]Q��Ho�tM��W��M7���������\�
�K5�%-�NF
�Lߢ*Z=XW(�@�"A���ހ8t��vd��Tn��"��L�7��v+g�T�����|�2��G�,�:DT��F��Y6%��@!�9�`��l�>|D��h��FMm_'��j�cv���;vl�I�y����=PM;9�6m����o�Y�v��/8\x�E�����׃B��r1��m(�U�_�`��I�u>��zȲ<*� q�������3�R��N��;D��B���Ǩʀ�ݜ)���9�h�Ab� Q������T!T�(�VQ��M��e�5������-˛
|C-sz�X��zXꍄy�c_c+��{���̈�����c��޵�14�-���82�~�3�ZΏ�e\₩�śWk�N�m]�'ْ:)s(�C�(��(jj����q�*Z�
ƉW�-I��
�D���qЭ�A�<�u�JJep7�R�Nl�Q�[��� �SF�^ B�rb�!u蟦��Y�cN_o�fo��g�;h��@�V%�:��&T<�8����36u�+h�ξM�5��Ƌ���\�+���ط��ѧ������]w�F�@sxt��1���ٳ<g'9J����/b��F��:R���*G�GT2�j���]W�w�{[��>q� ـL"B� gP����Ƞ����D�����`�v��[Ϩ�]�Z6���b�А�]��#]�p1/\g0��������ذx����9u9���W��1^5H.;EQ�Gp4�S�x���SF�\%O� �YMNBE2�Z��ٻT8�bT�3�L<�K�<'��:N����Ԩ;+�   IDAT,3Y�d4��<k��/��Z�f=�ۇWZ]��;$o?8�Ѯ�(��
���j��-3݋�JnG�Hv��W�T�}[R�4�eɒ�E+W�W]u����]���֭[_��S<��5W�柺ؼe˲o�Q���3��.�L
���t���2��YTr�
�g��B�A���*	� '�h�� � ����u�鍽�#�D6�}D�"NBǘ�Ka�M bE�8bRh��.6jy����A^�.�(9ˆ��X��M۬�������9c�泇�*pb�ai	+�o)�6G�H#���qbl#:i%'X��*�`2�-Q�p&���1���^�	��Eeΐ��Bb�K���˹[	=^��P����%��$�" H�2
 �\�!H|���4(a !��mA"�AQ�X���A�l�|]�}��::tX�QF+�Q���n8c��I�޶�6�_�����#��&I���E�408@ڈ֬�C��n�\��c��;p��g������۷�Կ���Y�eX~���V��7nȎ��.yp��`��"
Ex ��^�"�?��6���0��H�X�_Û:f:p�@��'P�OR��H�㠻9���a���1A,��s=���N��"�+DL���5�Z����ݶu���#��������go����#�aV�358w0K(��tLt�,�9��#�U=*��a�A�&��x/�ም�m�'�i.���9Wk�L�U����7KA�:�#�=b�OT1c&őò��!J���L-�2��(U�VIY2Rã��a�RA,�_�Co7��fS�S �A�r���}aj��M�/-w�����1np$ED�魵E�i��ejs=�ھMCC{ԃ㎠}d���ѣ#�;|��g���CCCO�������_^��U��M�r�7���#����ϟ��ܱ#BE:i_�Д���)�Hpcb�L������d�� �`tI= 02�R�%�]Myiw�i"S�r�d"��a��5��1X6�B׀��j�SsLX�3�u�埩A,�]����SD�E�"B@�#�p���V��l'̚=sh�4�Aw���{(��Q�(�5 J�a:��kE\ ��X�1',�����C+:�"K��њ��m�x�"rE�v�ĕq��8��(x���+i�Sٜ�m��'�D5L���J�$��P�b9*0�e�F�6�(x"��VQ�'L�]
ȳ��4�/�p��$�e�(}�|����@�����h�����F��z�m-�����
^p�v�n��;7�/^�g�Ѣ�#\�d'���8��/���B/
<�p����^�f��7\�Aԥ�|��Εܿ���(��FG|��1.�HDUVT���B�k�H;H4 SO�n�#Bc���m閡)�[6�w��������CD("ĩ�Ǝ�����ww�A1��$����#��_�Ա�c�$6��r���3f�iX&:�"�e�D��ԩ[ټ����!�4m�� ���#��Q�F��
_%���͛/��*�s@�����T�>���P�Pi�8R�|&�g.��Z7pЈ�@~��-�o�����G�e�ܦ�Kl�P�o��� �\4��U��F؂:�M��M�U)���{��˗�+z����[o��Zr��qo��Αc#���-�+w������B��mێ�r�-Z�fMv�����?�nM^�� ��N�_���$N�L�u|�J�P*����y�g�9�҈ =̞���7��E't��D� �cdY�5���`_��@>�� �;(&CD(���-K�n=Q����i��s"�z�ᅖ'��؜���2���WwY��u�VMXf��L���7\��	�P����Mv��K�v����]m2�R��@����\~�l�SyT��VE۟���`c��IC�6%Ōd�En�@)wĐ3!_;��Gl��t����:�ֳ3n�[�}�ݙ�L���'LPD$�"h������MG[���ׯ�K��GU]���6��V�J������R^ qئ�G�?����ݻw?�G��.��� ��ܹ�M7lX��o����!M�6]g�y�V�<��R=��#��u#�������D&a"Bc�D�y uȊE��_��#uF�0":u4b�ՠ�GC�O�BL��0��C٤av����A']�J��H#���A���Iyy,�Ѵ"i����9�ް�P:��5)D1�·��N) Zb����/�p����$X��^u�A�;0Wv�p�Yi�JQ�m������h�4MڐN��*PqD�"`j�bR&�*iʨFl�N�P���`y5��L[�����ƪ��D���a���I;ע�,��ӫ�O[�����m�t�Mڷw��R���s�[UV��;�cdd�C<}}���W�ر�9�˜|�޻���є���M�nu�Ç�|tx��#��_�}�j�̣�/������>G=M���ō���:��h�'��Ns����\P���Q2uh�L�q��6M�T�T���ɨ�Ǝ��u��w�N�2��CD(b<��'�#*���l�1Y�D���Օ�T��m1KL����\(G�ϊ�;(Ò� �� �׌Ϣ�:I�k����o^E��U-�F�;�c�e����̽�d�s���*oD�JΏ�*���Vf��S�9�� ����[L��p������,��)4�Q����I'j��偈PD� ���BQ�y��[WiEK>|�-Z,᪤�M�7i��Ͳ�,j�����gn�󸜊"!�>��O�߿���^���s_Q��~T��|�Сo9z��v�v�-A�n��6�_��n���Moo���F޺��,tY�oxS����\g.b#��` �N|�	Ze4�F�;�6�;�&mEp�lJ])n��%����D9�Np "�ގ���~mT#&)�u��$��Nj��/z��y�a�j��W�t��R���\��D ����$c�'�X��q�N�o?��F�PB��)4Bb �; V+�S.i��|����ѠF�~BwBUqDRT��RM�æ~�D���9�i��K�b���J�x�pZ���$�"����BA�#B0o_0<<��U;�k�l^�y��q����G�mt�|��:@��)���F���}C1�g�Ê�������m�^�g�����~@��1�1ӱ��:v�D?��(!��������aw0�W)Ӂ�݉����T2.��toי��_�q�#.p*X��nXft��M�|���{D����(("1���r��4��~-tBa}=}�>}z� ���4�\(Z��$���:�������wZ����T�HRp2QCP�4��*�~��Y�3���l#K�m#,XF:4pС��O��壄���DT5�خ�pܬi���lc �p��uAl�D��QB������z�����[G%RD(4v�ZЮ�PDHP�*���"�KV�f7�Q�!b�����Gg�u&qtx��6�1ltZ��%v&����<��oh�ѕ��3m�>|�C����Q�x�޽����GA���=f���������Ȏ.���Hw��wnؠ�<��c�G���>7�ǝH���)C����h�#b�|�.1������Ƀ��:�"籸� �S�r4hr��0�m���ҭ;O-M� VCA�	�7��?&"������-����c�9|D��:��� �Yg�:�A(Cy�S�*�S�8s�ѝ*eq�pX������Ұ�3G1w�F���I[�Rq}�m��1Z�zXm�-Y��O8ρ��E�� ��:)�y���.��l��� �L�g9���Q�舎���[YL63OR���V�RD��@&5",�|\UR	������{~�Xb�����|��2��}���nۨ��qS��M���4�<Qj�Fǉp�}�dl��С�ڷo�w�U�{��(��t���###��h6�#��Q (|ϭ_�f�6����yT~��PD�[Q"9;��ꈊܣsDP\�{���E9hH��!"��/u3w\�ǆ�����?@u���޳[�}��   IDAT�	Ǎ�P~��qg�QS��D�T!L�dfrdrT��]0b�*iƋN�Q������'j��[��t$����
��՚Q���i���OTk�R�)R��x!�PpYpF��	#pNj���Nq��&���/K�ć���y�TXV`OD��}���u1��v�aD�[B2�Hy/q�ǎ˿]b�1��%n��Z�x���o��V�ڹ#�JgT�#n�4����0Y�ݟlG����c�)�O���w�sL��o,�_̱b~��*t���UM�F�""�����޽CZ}���~�]��B˖/��?X�_�cό�ܝ��|�s�\.�I� ����q��My�Vݍ�ɶ*L���bBc�M0ojd_pM�E���MӁ��s�N|b��Bm�N[O��l@)�A�5!�Q�s�:C'�EcD��nP�����4W8��?�4=�e/Ӓ�?Ze�t�B����������y���O��_��U�W��A�B%�&��d;MO���B�M����F�ii�/��_U?tX�G�h���0q*�9�� Qm3�ֽ{�j8x����;������t����X����`x�������`!�tz�t��`�mٺU��~���@9.�c�*�=�3��d�N]2V��۲e�뽕ۥ1%[L��#L�q8�g������O���`�� E�h�Νڲe���(:�G�s�;_�-]"��b\.w2D���:�;6vG�_氺OEt2��n(:I�3�#&&�u�����ݰ����]aDU^#�������6��3:���s|p������34��O��J4s\mڐe��3��BC��F�+]���j%�U���b|笌#������q�����O�!�f=��oԹ��%��!����Ӆ/�5=��oҙ�|�Z�<v��Zr�.Ð�	� _SU�b~��&ֻS���MFd��bų�^N8���A8ڃ8��i?m�(bA�����~��0��	��v��-�#�ݻ�x���q4��G)�����=mn%7J'�-�x�nmd%�U(�7�_g�q��R��젇��m���]%��(adD���l@��YSq���I�mhh�[�w��Z�U"�Qh�����������ODD("$B�/���("t���u�9穟�*�`0 "H0ݛ#b|>�j4eE�}*�)ǔ����p�Bv�g�{��1;�:6GĽ)��y�"mwM�&iOGg��Wt�Ԉ�vZ��cO}(�(=��/X� b�����"���CX.�=1Ł�˪&(3�T֣2R֕��C�Z��"��B	N�LaNJɇ��xf�Z�PD�i�Nׂ�?U+_����W�W�B�_��}���;��DV�!)��[�u#H톪#��*�9g;hs�*?�A�Аny�x���#*X���)Ԟ��}�-���uRwDȿm�{�<�+dg|��n���O\xemǍ�#���¶� ��RЏ~ٻu�6�^�Zwݵ��1�E���(�H�t���k�M�6�J�崹��:&�=�\�L��Nrʤ���v���`+�6O��<�x�S�ޔi�k���Ç_��E�1w*�!n�!���
߻o��T0��,Y"��-j݆F�O *���||�E�G�VDtG��\����Y~���h�v���B�_]�'S~Ę~D�L��q������3"YSDE3�i���$�4�����A��	���]۷3'���"cVK�tJ1���e�g��UVi'yN�,�n�s	Ʒ
�EU�Z=��3[�-�7{�Z-�q,�n�$��-��1P��'	qP�T��i��nXމg��O�	��u�_1�#�Â�U�}�q�5��җ#�7s�L��G�;)��A�Y�� �ݰ���6�^�?v�ލ��.�uy�ޒ�[�۷ߥM�7k�y��5Z�v�6m٬�G�nʶ���SxS���6��N���Qɪ��ʨ������@P����&�~�����7�`�S1��~y��;�}g�Jf����prgA�Dl(��#� B.([Y�#P0�����m ����0[�n>�S�\��ZQ�71��#�2"b\.י_o##���i��V��t�=��W��NO����@���d8�o@��$���"�Fo�e,3ojt�'ܿ`bZ^����|��Z�<����uV���GagC��C C�[�-Q#���@V�1�.P&!���i�@��4���$�qހx{�-�g�#阡j��Q�)���h"�ҏ�6�F�Y+�\IK����~�#m�r��Jz�����L9�	�5iCI��Y8h����d�y�|v��'�{���o��>E;vl�6V���Ɇ�G|;�n��6��c�������ߏ#�+�G�o\�+����vL�����'[
	�����'��*	y#*��PDTrι�>x���p&���j?�p������٬�?]�U-�q�=�*^���e�"�'�KU�6+�6w@q�s[DX��dBp�ݢ���n>"QDd<":�1cz1eޓ�g��"�ʍ��T���=*�$�]f�GD���ny7��u�&ƻ��c�h�Ԛ�F���ޘ��˖j+Q;�n�A%��-�U��q�k�ӔQQ*&���'��N'ǞqqG��d%�q���%v8�2�A��A'$+itTMܴM$�|���'����{ƫ��v��>�AK��v;򒾍�e�鹂����D��N�G�u��Qɭ��lw ��y*���!��yǕ�ooq�=���=C��E.?�s�N��B�?%Fb�U���Q�y1�A�*�P���՟�����v\l~"~��J/��OzE����9�0��9��y��4�_Ti����\ _�t�|�'�i���"&�]gr,�E�����~#3ߍFnQ�c�A�����]Sǻa�ɠ�s2�q2j�X�D68�)��D4iSQ;�P(�G0Q%͘>]+W����O�^�8n������B�G��.��a{���bp��Y���x��N�C��#F:Z�
Ѭ�$���K�0L��'M��`k��ly���p0I��n�g��U�HT<�=�"��j*��̼DZ.Zm��KS^앬bw�űvh�v�5�Ǖp[@?m���Yɶs!6�����ŭ�-	�6��'`A�mJ�X������[!�ȝ���<��3g�BvD�ț�U��PD��"B4v�QI�܉:"Bc ��B�ǎ}h�޽ǽ4,�#:xy��sDe�����EDz�3���C��6���������ڞ$ӻ����שIs��M���P�,3�t��.�h�w�ݲ���퉨dM����>�|'қXfDe[�=Q��M���Uͱp�����qR���>�,�s�9L��ڲq�6oު��G�R��qή`�PF��c@����ds�'G��s�z�iG�V���'oÛ6j��ю�}N���3���������W����W�.���Đ�3d5ʃ�� J�FU���F	qD�ˢ��o��شKm^Z��9��;�_TA[B5k�����X��sA;��;ީ�_�q�ȴ�#�^���2�΁)2Z��Oqx;d?��}}�*q�wnب�n��P}�b�8�#ܠ�X��o��8I�

2�����4�'�J���FD�\��IaJ�B1.v?E�#z�����4�n��d��\�I!.6+���k��l��l۶5���c;�Ӟ4/i�����74"�]��]^7R8�ԤO����θwi�kh��#�wd��`��L�.��t""홪��*="�R�䏨t"*�dEN>ӕ+W颋$/ |���U2qKV�%NϫS1�M�:� P��㸂|�cOPG���8�̕v��1��*y1�����O��V����}����}�V��Z��W�ԁ�}_��l��%��<�)h7,K`��|�:4�N�jA/�"
	Zr�u�o����(+��w�ҝ�b����K��99���,-5��a�l��eul:m�	sEi)�s���� v�T���رK��^q��67�];w���K��s�9r[ūkZ��%�G�I�c�����q�'z��R"���"�E�F��?�������H4�,"��_c��s   IDATT�G�Nt�S�:��N��hם�o�m��;���^wm�����A{��8�,Jl�N�(���
""/J��;C"x��h���t�izDeG�/b|���(�ݵ'��%b<=�-��u"�$��LDtx�̟7O���X�"_z�Q~bce�����Q3�EA4���ZUR"�J g"�n9ΆU�*0v3e{E�޳[�?�%������O}Z۾w����SC�hךu�|��u�'��ֽ��ϯ)p���Ώ��x?%�+�mֱ;J��D��A�C^�?J���$*q~%[���a�mcK����B>rn��;[�$�,v�í�?���i�R���i%��p֢��W*p-�V��A��7��᭎�}����W�Zbv��/�\���X�a]�!�<t0�J�KSm��U��4d��2�r9��5�C��w=44�T:��ft���qg6�o�e��Ekg���a.‖-_�9lu���2��<ލ0 ݡ�L(��(%����7�7h�H�tӉiM�iFD(���Q�E�Ĥ�GD�w�)������;>"�2#*:��D�˟(�����swe�����QɽZ��фHX&�^��ʕ+u��x�OW_}7�mjM�&����Ua�G%����ˡ%T�e1�ar��B��n�#��dR�N�N�a�[N����m�g����kt���z��{��>Eo��y��x�UZ�����-���^QfIy%O�xU�˥~ϑRc�������5��ؒm���(
�F	m��Soɪ��{�JV�7�og;�06��B=
q�~��2c��q��Ht�vG�SD�}��uRZ�:��D2-Z����M�ܬ��W��/}Y;v��_�p����'��=p�(��"Ԧ�a��}JDX:GAD(��ꆢ�3l�Q��bk�>��uE��ǎ�Wp""+���T�7�i:�In�ȱcy!����e�~�m���g�c6���/r�^p�:-�v`��f�>�a�'�g��-w����>QyAb�w�'���9v&Q�R1y��JQQ*@2qt�3�X��=��*p|�6o�W���P�K��h��*㻌 �$�q籚��d|%�-���c��)M�L�H{[�=�ڏ����[�Q���ߦz\9��k��*���]?�WLv��wΣ"�4�˞��fQ<��9$�L`�7-��b��.�t�q�dպn�ޔ�����"�����S��
~$��M�䜔��X�	�~.ʠ�7��e%X�yٟ �7D���J}���)�SDh6/��ߞ�s�9�nŤlTr_rV�-���'���'�LPR~�F����^H'��:����=��2*�k����1��!2��)
*P"^r'u����f?���ŗ\,�x<����z��ߧ��E[��E��h3	J�4m3����[a�u�:Umm.��e�>�g8n�8>��N��-s�6���b���=��F>A|��My�.���c�d\���8m�"=�҇�s��^�|?��ϱ2Vns�|p����c3'��6y�ǁ1�2�t��ތO�']֭Q�T��އX=��p��7
�zA9�-�s'U�b`?�׍����޺Z�Nt�'�@'��-�OD�7�6���b3	N<�j��i�zTk��>��[��[�j�ѣ"E�T	����~��~��b�_*YÍhmb�֭_��wީ;7 Sc�m������M��t#~�-ڴi�6��ۼy>b���j�HfΜ�G?�2���<clv�/��=Ц����r//�+�SR�j}hyq�n�y��%"B1N�����G��#���f���E�>��vD������O�S��$]��IT�}�v}��׾����չ�_���J;<�t�$�uǶ� eX8	���o�Q�!�d�X�˛J�)���ď��˳�uLO��!Ǘu�et��|R��i��?uu�ٔ}_)�14Jز8-ߜ[8�U�����D=zDW����?�o�����ؖq�R��C��@=0�K��e��-s���˜�(C���F��p~�}���\�E��܇��c�؋���!�.{��Z6S�.j�x;��Q^�l=���Ӹ��Fvt%��6ٶ�ɣ �����j��]��=�|��~D ���w��/�v�ؙ?X��}��O���z򎃻�+���o��{���6S�&�e˖�2�.^Rz1畸��y�s����)��o�o��Mc�~��I��z�ت���g͜I�B�y�@�t����~3��=�Y.�q�	�����^�)�^1�fT�C3����æ�����i``�t巄����������7���� s��=L�V��
��v�<u/{�}�t"�����P��*T$\<��B��Bg<z��������P������c`Z�҉�x8��9�?Q�e>&�u;�"x�0�;9dS��	%���(q^<=����P�"�BZv���S��y�ih�>}�cSAgx��E�b���(b�j���t.�U���gz����\v)q����(Z��^��,�Y-�bgZ=���G����� �Uˋ��oޠ�J�6�.�h(�d�N%AbmU�"4I�z��m�x� <|D������ʊ�+���v�!0h7���Y�Kh�ДA	�u��ݳ@Y~i��1���1��_{�C����\/|�5mZ?�*��1�l�x~�b���.�3��(�v?�<ㄝs�&Қ�(YxW`L'x�u"�'SV52V'\���4�q4�ŚHD��Ռi3��?�����e7*����\�G?�a��O��~���~�~K�����C�Y�&��l��˟�κ�w`ߙ�S��eƮ�;�{�n�᥆q�5у��>�r�/�����*����ߕ�sJ�AҾ�N��r�f(�PM͏��
Nc��	<�x1A�+��>	���u�e�������t�P�� ���Ѽv��J�0�Fp�U�ml0�gJ�vT����v�.��B=�	Oԑ�G������ޕ��	SxYʤg֊���'e.�K����*� P#霫@���J-j�鉺J�mOH�|q�8�^�q�yr��ͷ�� g�Cn�����Up2߀hw��ۘyU��l�'��)����ڦR�9�k3���񯮿���ny`bf�Z�������睧��%��?��_z�����?W���ѳ��,��~Q����������3��3����Y=�g���>�iz�S���?��lS<Z�>�R=�{�C.���_\m�>���#u����'��y�~絯ի_�j=�!�a���D��wΜ9Z�p�N;�4�ǳ�M�Fo��߆*� ���"�RV���B��Z� 9�D���IQ��l�̙W�R}*jz��v�ݓ���Qb���G�$R:*SL���@Dp]gT0n�Z��4=ﹿ�_������%���cGu���r�M�ۿ�?z����^�����������z�+^�W��U����M��Z.��G^�ۯ�k��5��k^�Z�&~����5���f�u��:��o��R���F��������@o~��淼Y���?��?����Gz��߮w���;��w�S���?��?ӟ�����}�������>�����>����	�l>���?����������������'�˿��>����?�9}�_Կ����+��������o�������������^y����j]{������oM�r�-�=���e2��ֳ�痬���Ğ]>�w��ʛ֮��=ك<:�7�!��M����.�8��ka���ř�u}���2ME^�����P�8M�i� �e�������OG�<���$<��OS?�T��i�-�������yڻ����7����*�){���1<�h��*������M�mΉR!%4�@Jy%��8a���R�ӧ�5o@m���*�Ia�K	��������Tоp�-2�@(A��>J5ΥC}݆D;�'\"�ݗJ�&ʛn�h�W�]�F_[�AC����^�R�R�\V�?���Я�گ���{�~�/Ћ~�W�b�/y����x�^����W��ez�˙��x%�����W��y������w��ox����ox��<=�^+[   IDATAozc��}�������^��W��/��z��Ku���oZ��h1OI�/Y�ۦv�v�v���]�&��	�*8)%(T�g�eX�t�%�A?y���߳nbv��Dѽ�GDoNL���ؠ�* � 5��U4B5|!��O�괊�Y�,[�\/zѯ�\ o���U�����'\�'=鉺�K�x�b���h�=�Ç�?��g�P~�u'�杼u���V�qm�Kwmۦ��_ma�NkÆ��p���#��u��Y�"_�z���,��z��[�7�x���믻>���8ɫ��JW�0��������{�w���|G���7ӱ~�k_����?����/�����/�_��>�o�ӿ}�����|F�����?���������S��������'�Z���O��?��~���ȇ?�}�C��_��������~��=�џ���ys�Sn���w��z���M�7�?��?�;��'��	�̨�ߩ���yA�p���=��}��}�ޯ�n��~(o>��G�1�
>���>�I}��Z�7��C��S�����?�cu����͟�&�y��}�F���]_�F��o}+��+��w��=������nJ��6���oL7�|s^_+�����z^DmذA���&m�洉����ʕ+����{�c��~M��C쫶��_K��Xc,{��`������Z2Ѩ�0���J �m;U1��S�(Z�8x�5��5ʣ�HB��D�*�h��3���G�y�|��2EH�e�:ē�$���%�,M�g�EҶ���B�W}n���j�p��{��۫���Jmګ6}B�ȹS�T�/\�P�x�#)�N�*���(Z-��W=���Uo_��~�ٴ|ҙ1c�<�gϚ����3�080W������^�E8�����Ŕ�X��#}}e�ܢ.���>莌64#�ME�?[/�;��jI�B-�-)}ZѶz{{_6o޼/L,��(�/q*;�ywMz��b��fD;")T�8�Uʖ-[�_��_��b����/G��]y�e��S��ɧ�D:��?��z�c������u������P?]�`=�A�E]�.� ?{�������y<��{޹:��st�q��:���t�Yg��3�ԪU��b�
-?c���r� 0<�p�>��&߭}�^�p��/��?�388W�G��jb��Y�`�9s����Y����G��z�|�_^���'�������#G���x�{�����ުb�o��e�_���4��������/U6��7�u���O4V7��ӱ�|��jn<�^{����p�����C��wy�u7��|����7��׿�5}������?���|E_f��E��>�y}��g��_�����`'����Ts��_��>��O���D:����?�6�?�A�O�Pބx"y7�w��7"n>������z����|��S��x�y�[ߚO:~�1o��[�Po�÷�x
r���	�d�����A����ukײ�푊V=��\�L�t`�E�9�qX��ԮbR(Ã������L�`����_0(ox�5�q^�^p�i۱8�%8�ק%�z��3�1Drz�WeR�9y]�uT`@��\d���Mv�����i!�ey9��{.n�Mq�*h��|�{�7����6�5�SF��m�y��c��l3���y���'�gځ��6*q�;���&��P�j1G�򣸳g��ܹ�زX�*yqR;k���M����mD���.TQ�	*�-�s ����\�G#J��%��̙3��Ǒb\�>FZ��na3L�m�܉O�ED��@,��,�5]r���/>SO}�S2��z��fΚ�y8��h���{��EZ|�b�f,9�DKp�	�q8=��lO_�T�n
˗��3>�|��8����Dx%f�X�R����<s����Jg�β�7�9Gg�s���ˍ��oƹ��x���矟7��σ�e���7���G���2\��:�uۖ�霉m���V��JV�U���6/������-���7#��b�x���ܐ��7?ҳ�1͛;�	4W���`�o�={6����1c��sc���H}��ycb|ٯ��-=�A� �����𰆏�~�0��������u�>���OJ;��a�]ںu�6�.��,��K��c\�H����uOF�A�?�̝?/���۹A��v��-1�Jlh��)�*c���iD�eTL�(T�!"E%���a�3�!џGqp�Z��᠏����G�;B凐��ڝ�����
�Ϋ>#]��
t#B"(i2��kP��p���%1tvT��,�ܨ��Œw4W�v�>~���<�:$m�`S;f_+��q��c�D���M_���'k8�aAD��Ϝ���O�z�;�y��4��6����i}�p�v��8��i�!�tGu\���0U��l��K��qS��=��C�k8{���1����D���9sw�^oO��7\Q:�.��6u	"�u�#BQ�41oH�&-�GDȎ��Y��B����Z�vd/�" wz_�hq��5)z�xQ\�^�����d8�=0�A-7?}��3��	�d���3"c6��q�4g��8�9��;5cn��Ly<R� ��r3�#�B^|,\�(�*��X~���oN|s���%�˿�l)�s3�AߌV���^�<5��洂��+�r�
���x�0�\u���i�&t64�<�>+�@��M�0vC:��!����\��7�su>7�ο@^ �y"�7"�~ڹ���]�K�/�0��.����溤������y��Kj<$u����:�\�=��G�IOx����)��4��/~�K�{��ê���9�6�`�������#�&�C�8��#�вw�Nc���~Y�]�C<YbUy���Q�a�A��9[�.{��}�+4���ͻa���u��V�gdu�S�M�P�c�\�7�\��ܣ��o�ۃw�ݧw~�;�}ϐlzA�N4�w�\�2��c��~��w*
�?�IcdP^N�7�lo�P5�h.�����>n�\�鈱v�l��X,"��N��D��n�A�64 :EHN=��M�i����>����;զ�-X0�:*"QC5%n��0��`ހ�N-΀��gE `d������K���>&�mԍ7ܠ�w�!_ \uU y�q �����V�̋ 1��AX&%u�~'��K�H�#�����P�+�'i�qS��_!��"\��N�k��ws�^��׫V`ڀk���}ޓ���0L�~���e����0]�|�y�����f5:̘9S�L�̙�d��5k�lͮoZ�x	&$U�458w��:���<1�洘�Gߌ������xN�I,�S��e�ؗ�e<-��e��3����*�x.��b]��G�}�e�}��kX%�"���(}���B�}��& ��_!�j��تa0v�U{xD}K���g>Sg��eZ��_�������U댕��A��ԟҪ��Dg��eZ�OV�[�^�k0p}]�Qk%TG�q�u��u�`%0ޱ�m��{�k�5:�{�!�:����/mڨr��P���_I�>�R]�������9���Je�L}�I-Z-y�y�x��	l��?��lzl��hj�WP��V�9j;-9����
&M�e	��p>�7!d2��N?�}B�L>ݟ`�]������2C!N��Hj�#����e�(�xp竩y�3=�yϕ/"b�ڵ3_ m�p'׼T�����t�c�9CYz���+�hw�}�`��Z\�dHd�� 8��ewn'��42�]�L�"�)_a����p;Zk�������@���H_/�8��ij��ȩ�-ʬ�+A�B�8�u�յ��������k�B}ӹ��
�� ���y_��5k؏�U�0�c��!��IA���	i$�Φ%�c�6AcdT%N��΢'>Q�^�����霗�R���U8�k��|��0��Fyl�j�*P�e���!$��S���Zw��֍B:pP��*׮�С����u���oҁ[;yѧmV��n�=�A�^�   IDATzm��=�{W���c u������}����w�m��^��`�����`A]�XP���.�X���cǂP4��5v�1��hb�ھ7���潷�"`D)3;ߜs����{�;�f�Oc�Ǵ���Wqb�@��������'a �b��;T���A���̌��%F���#P��+�&'aС|\���U�������+g��i�oʘ�bf,l���x�ū!�S�	y�`g� ��kR�bpO�_���������Xz؟�P)�
�ӿ����G��E5c�����j.Γ��KE��HN�l�Q�$ұ���~�+�#�j�:`�H�T��d�W������
K/FeZd*�)T�C�"<�T�!J���|G���`f��y��(5�����Zq��qy9y�����|JLu�|xr�$󜌏�m�yo/RZd�WZ��,�M(�+���d���Bo��?݋;����#���!I�����\ ���O��!bPա��AL��fR�q�
����:��s���m��+soz�v@W��.ue�d�Yv,�m�!�bX Ty�B+�;�2̺K�'������:���<��;���g�&����j�7�A{�y�����b��Zk����I(C�|������0��*��X��Z��uǥU���|����_O�>�x�n�.���t�I*9��O����s����͌�f�����Nn4� �c!��b��/�E'�@��I�_#J�X�(��ӕ���{h/��?=��B<��Ә:e*�����H�� 5�YGţ��FR�����.^�e0�� ��TPu�J0`鬔�|���8`��<~>�U0A|%Oe��vFY;�d0�ø
Cϲ��0/^+O�$�
��<)�<)]>.F��LGy���Ó��JHC�{�H��>���)b��ň��P�,�������@h�)�[��x#��n|��p|� i.
��r!�A�f��`J��.��ɂG�\,mm� ݂w�Ps%js����P+�/���^x�����Ϛ����Y�Y`&^_��V�,�/��byJϘr���ؔq,Ѳ���Qx�M|���x��wq�_��4n�06
`\� A�Z<��jl��&Hq�/}�"����qA�t&����r}Cj�ť��~jkd!�h��	u������*y�K�2cA�(� rP:����:��[ (tq.@6�ե��`>�E8�"�]�2�ι��+P��:�|5l^o/bdcǁh��F�\��v?��ܳ��fc5�^��x�J�^/�=g�F�� ��\`p���'�pΡ�s^���a8sPxSZ�/��� �,�a�>ɲs���u;?Zȡ6�cL��nr�[�|��)}:��L�pt�|BE<:����:tk G��U~W��t���q�(?J(����4��g���EB&AqWzJi��V�
K0���Ӗ�7�Zk�텾���Ыw�s/~�����i���y>Ҫ�̢�`f0 �"{���R���.BF���1Z'�#����0Nai�!J����D���z��U���>��P4p�T ���"ϭ��?��+�wq�SO���߇c�4.RpL� �q0��縇�9��j �4a6^�pkLJ�^�[>��Q�sn�r���
����
ɇ��)6���(!�L�C�y��'�'Y9�օ2Vf!���
�Et��KؿH���Y	>g�U���M��)^��-R��OX'�tz���b����;��g��R�V[.�Y{8�]�SH�Gs$��=�w����f!�-#���=�����}�Ϲ
��_�q��w�+�<;{ԉB02MH	��0�03� A�"�ʇ�L�$D4�Jd���J��!�03�13��fFo�p0�����.�,������q}|�1��RN�9�w�=�#�#���ì�'�<�a:�R0j]j��N�w�4�@%7��x�]��l��,c���2d ��6�gCX`(��544b��[a�5�@W�Ͼ�.�ln�8	�͜��C�������t<�G�=:�Czt8i,T5�X�`�R\� h�XXU�z�-9!S��"e�v�`����sH��n !��������|���
�<��~�-��\�_��0���d������vB�U�Bc̒!X�H��X��5�ᘆ�0��@7C@��`��e#��`8z�T�����'A�: 03�0^���(����"N�ȟ�d�Gi��Ǉ�n�׮]��k�k�[�hM�����` #%�H]YiV�+�NU��w@V]��ҝ� �V# ����vl��f�h��m�ڂ3~qv�m7p��(�l����'ߍ�Ǝ�UW�ō7݈;�x��O�2�~���?c���_���k�<�G�)�O����S�'����|�/x�����3�x<����lZ����x��q2x���Ŀb{�7�6^��'����ɕ�����@���'������}^�׫���ZϜ�-ə���O����_�S�۸���'�<�H������5��&=8���H�&0�S�MO�3\�iR!�Z&��D�&RA����.��\�M4����bH	Tf��(%�nS8����É��%�I�� �,"J	t��O�c�}3d(�,
���9i�Z�'��Xg�uPýѧ�}_r1n��f̜5��*�Q4ʐq�.@�e	��O몼dd��[ h�%+<����9�~��t�P<T^§2M��#�~��39�W�&TL,t@��l�X�6�3��ǳ�{��FO{b�dY
�[`2>�bڎe�ۧ/~��O���� 0g�4�;g���6��ч|ੌ6��=K��L�W��tF閜����n�ݥ4�.ցb6Id�=�K���"2
̌�_5B�Y��ڙ�=���}�x����q*�ƳQ��R��{���(H=���E�'��+Ĭ�:/s�a��9h��'�r?�p�ɇ22���9����E#�6���x���'�u�d> ���>	o�&N�-�ފ�n���$��n�u�_�q�_���5���k��ث��Xo���W\��/�������K.��_���E��5q�E�qޅ��/�ࢋpe����"�T�ҋq�~5��o3�1W\�+���_y%�UW]=W]s5�f��v�w-��~�/�u7ހ�߈�7݄[&܊��߆;8�5�.�}�=(��z*|�A<�'�i���~��$oc��Ş{�9�����<^��<8ټ�ګx��7���o��w�}�O4��c<�|��G���O8�>�g�̀~F�If��Y���s�̆>ʞϷ���9(
l����F��|ۚ\�\᥹bMg�B���f��d���'�B���JNd��pN@�L�8!����Q������䲐�^}�U�ӎ;�{�U��x��9瞃K/�3��AM�}T����>����!�7+I+��ݴ6�(Fj�8�4T��3��P��a�pLN3f��J��q ��(:��+gN�z�:�"��WQ��K��ѿq�SO�\������|�	F��a�]�8h�A|����S�R,{p���bw8�<>��#���/L� %�"��#�Cr�l锼���L(�c��QT��)p2V�L&7�y@��Ɛ�W��'̋#��S���lv��}g\xE�	��ĸ0s��ͷ��ٳfq`�h�G�0^�}�ۗ�����Yh�Q�0&���y� �f��4� 0q�!E� ��`D3������=�D��``3�q�|[��N�\n�̚9��C�/>��}:�|�	>�׿����\����;x�7�7��I���kx����;W�/�o/�����y����/��g�óO?���|ү���0���z�ܧ�_�H�����m��n��[n�7Ѡ�p�з>�{��N�4�\v9.��2\<�\�	��̅�d.��B�w�8�8���q���)���w�8_a9]8�"\4�b��%�
��K/�%��.s.�|.�D�I誱Wa�&�q�b���qҹ.�����4o�ͷނ['��'��&ݎ�I�[w⏜���^����ǔ)S0e�TL%t����I/   IDATrBzq�K���O��}�G�c�?}?�i�N�z�����³/�駞�?�^k���{���í7y��y��c���o����A:���g\s�߶k4lwh�X�á")�ؗ�;h#��ʛ�M��F ���D�}�M��j��	{�/H�8�~�������xF��T9���cf0�k3����A[AG}4���tgr�
������]Ǘ��/�O7��!�jf� V��t�f��<b�vlf0�A��|�2�z}����f�G666�ٳet�.]:�E�|Z��-0�b�Jh_&��l��l� 5�G�˨�%Eb O��`�#�2�
Ŏ�F��>�^s͵�/]]>�Ry��xӍQW__J�}��h4ɨ,f��NcL��@8�a�N`tPg4����� �	!É�#�����dcZ�q��~�>|��4W�i�i*�)?��-��� ��9ֆ��z�J�W!�G��6�����
Y��}��g��N63>���ŇL��������M�y��7��k��W_ë|�������I�ox�z)c��3��H>��Ѐ<�����cx��G��Ccڃ����� ��7��!�d���wE����;�	���o�&��o�p��m�c"1a���D��:]���1�0n����ʫ1y�=x�����IUP)�~�͌�߁�q��w�U� ���~���6�}2O�F �};��10�!�����C��hH>B䦐�!:|��"�JKうEx��Y��
�,����;�?�����l�&L���M�[_~��$D��|��[KN���ЯY:�_����`��8�+3��T�Y�����}XD�
3?P�e��ʕ�G?�W��G_}U��V�#���tֻw�Q��0�%�&b�ۧ�>�`5�t%%̷$l=�L�Q�X^7d��(ScC��Rt��6v��]o=���H\v�eܖ�ߝ�[6�0�;��~l��}���X�KBM]�k���U�8�l.G��@#�J�� �df��2�5�0��s��3n#�r���1wN[s=�Ι��s�S�ln��f�/Wj%y��-*��b��Ρɬ�-�*��u�Dc�J��W��	�v�����)x�Vl�r��<�`��b
� ��:��TIjf0+����@c
�w-�N�a�U�6Nܢ�h�S�.��^�"�n[~.���Χ�x�/���9���]ӆg��?
�<�>F��+���@��G��鍸<"�e����N����X��陊���1�y�F�G�2��6���I:ϴCnc�����W�??����pޡ�̻���df�'d�AC�qk���vLg�W��g��M6݄E3��
#?�̼��H�v�a��i�C�}��9r1`�	dUA��A�j�q�Jy,S�
�ū�r��)ܾh�a>E��8��nq%�(��M�ښ�~�lvf�9	�>j*��`f��A��ˤ̐#I�@*>��+2M��/��Xw�M6�?��'8����_��]��2�_J�B�{޹8����g�g�qW�ओN����c�9Gy$F�����܇>?=�0z�!8���8�q���cذ���~��o���^��OZ�瞭hm���>��3v��������a�A;�/�m��1p��f���kJ�e�b�-��f�b�7�m ���V���j���>+���8Pz��ݻs�醮]���F44��_d����T�ɦ���( W��j<�Uw�#�Is�-��t���q Q逡���)��O�÷�_�g�����@�iD�n�"Иʘ��,�I�MqJ�<�4zm%��2͂���ʿ@#(^�������S8A�W�b>�c���G�Q�\�Fᢚ���1���5���1t��q'�a�. ��&��e�3�<��gF!)b�h�3�Q�H=L� �J��묲E( ���7�\���������:������k�����޻���nGs���G*�̌��/P6�pC�v��X�{�c>!��z0����$ 3�����W�8�,Ҽ�4c����|����3�+>C:ۣP����D�3�OM=�����39^�7�7�ի�Y���$�6ྍL&�'��֬����R��'����ʀQ*�ħ�T5��
O2�T5�D.�Ig��ro��Q���_�o���j+l��v|b?��.��!C�`��v'����N~7�����y�]hhilw�;�3v�Y����p����{`�=Zi���^���{o��>���q��pЁy�~�!����ň#��~8~�������#F�Iᘣ��q��(N8aN:�D�t��8唓�󟟂SO;��T��O?��v��p�?��0
��SN�>z~�I'��O�I'��O}��Q���?�X����>G9GpB���g?�)����F�I�`_��`������~��˺���кW+뽻��v�v�e'����4)������v�o���Ķb�m��V[o�-��Xټ��~r�I?l��F�`NP�_�	�>��:kc͵��k��UW_���
��郕z��J+�����+@ob���=z��^�l�D֭�Y���W��6���������u]�P˻�uu�~�ӄ��?[�jngT�Hk�>��>�>�N��/p���7�f�Rp�u(���id�۸:l�Q�����d<i C ���_�c3G� 3 �4>��3�P�\�7�m���o>��u��}<��a|^��U�+�=�sn�#�j������O>�,�ix���Ʋ8"dv!����#�:����Z̏�1��d�A���o0_Rʔ>"�REJ�b~��џ`x`���.PHW]�(�Q\���ݍuΥ���Fr;v0�
N�m[�X7��A�|�9.DvT�4�R�\Us�ci̼�6�ə9��J(Yu���PP��"b��N�!�b�8���9=��f�\Qf�겚+Mu���+c�A�ﭰ�
���͕��}VF߾�`�U���*�$���ݛ�[�W\	�z����нGOtoh,���ΉB_��ֵݺv��Fם�z�'���Ջ�f%���Y�w�����V_}u����:�`�u��z뭏�l����F�_�~�t����y��؂��?�V�2�[��l�5��fl���8���$���;`РA�q���?��v�	�p��u�]1d��>dwD�س�{��tg��O8����/�#��?�������4��C��C>�,CFzF�N����~�S.�Ew)�Éa��h�8Gq����G��9as��8�c�cq�w�q��ŭ�%�:nF��ǃ~���	�x��;V��dt,�K���c�c�,J�x��x��4��Q9�|6�hC-�ޯ�;��o�4	ǟz*~�9x�g9�h���i��\��4T�@������oo�/���)";0��HA����>@e�S�a������Y�_�oi�Fx�SO������[n�1nå�{~��w�	X�)�y��e9P�G@����ٞ�����7�%�e�GQ�]����t�f�U��'�,/3+�33�恤�<8����uZ���\�*H��s����5�]�64��_��,�d�;���(߅ʶ��Ư�'�`�Vc@ .E�[�$�`� l!��~d�cC�EԱ�(��2n�Å�]#�bP��x�@��j��	r�9�UT�_qu���+-��W֚����A�v�j���{mA��hjn��I���Wn]���V�p�{�9��2�8ҙ��c�r,;|�Yj&�Ņʮ���o�%�?��b|G��X�t*�t&��0�g�O��uUjjjQ�6ׅ���>�X_߀z���lllBTϮ�_W蕫�|��@N0�{�Dn�����,'��^�V�_����J+A�OoNh+�܇��/��%VY�rgUNF��������Ě| ������X{�u99���i=��	j��l�!6�pCNRd��?   IDAT�na#ҍ7�Ɯ�M^��m}m�c�M�d��曣��[@[K?��������-������W�[o��"?h�A~"�݁t#����Ǟ|
c�]�S�+���sq�?�><-�]�6f��6��1�v�6v���!�1oc;�����;�6��}!�8��ʘF|���ｏ��W0����ྻ��9'��?�W<�x�-����#0�����1��B߇ԏ�Q�n;�9���ɻ�2�Us���J����y	�f��| �m�q�4s<444 ���*�Y�=o03�<ʜw�{	�r��E���#��hh]]��=z�߭[�x.ľѷ1�-��I��[2BIi�MM��x��l KU2��(+�Ŷ/��0�H;��ol���yc�a¾�I�V��`f�4p.�"�P;v�\.K#^U4�4t올"#������o��l���MM�4|4~4�>Lc#굯\/Cم�Z���|��:!���C���A]���
�Z�N��P��WG����\>dm���\"�s�F��d�!
���e�Z��oC�pQ�6��-��dy�Wq�~�@i�]�PY4F��C2�l8�l(tr��4�f�2��p�P_�i���Kq�����K�ڷ�䥻�=��{�zQ���{|�)>�q7�ǅ�\�.��o���<��� k|�2�l
�Q
�y�ռH�p��g�
�
,�V�!�~��!|�5�f��d�O�s/n��\0�.��������zo��K��3+��!�IǪ�k���v�	��;��6��UmU��a`'"Dcx��ɒ��#�\��C-'��F����k�P�A'���$�2<��A�_8^��8H�	��lK��ꪪ�op}}}?. �7~[X���ߩ�w-��y��i*�� �;�Q�C �� �q��Q���~�����=*��8�S�w��NNy0q�#Ћ�x*_�`���.ż]���Hqp�؁2ht��s\]��j��u�X��Qoh��KI3�V!���`�J׾��ڛ�Ro������Q�X�z��z(]�fj����Y��]5o�U�*�W�����&ä2��)��^up2~FJ��uO1�0�?�m
�=ꛚF�T��{P�Q;(S(�e@*�0�&!",�	��[`�����g	BT�^ȸфB�<L��8j��j�a��=��~�a�������~T�h8�<� .;g�w>λ�"\|�帎���?�0^�Q�����̙�Çt��W�9(m3�1!�a4�c�L>������\%���x����,W��O���ߌ����;��1O=�����xg�Lh��`fLQZ6���׭��m��
+a�mb�C�3jF��
�7�B���q�W�}<�~M��~V������.4�(Z��f�qRhwf�t�#��)�e08@:g�եK�0�����Z#R�;u,��[B˵�Ū���Ne���� A$ZM��)�l��-�!����it	$���[�HKIɯ]�W�H������\3�b Q���ei'�!�˴�s\`�QL�3� ���J]FT�������u\���rpD+n꯴r�9X=�qi�Ro䊽,���\4FY}C=�z��c��s@���g-WJ��_ࠈ?��pߗ�[8UE�ܪCM �3ܕЊN�/�tp�c?�8'pB���m D�<	����(lGi���/PW(�pꮣ���r�8��ahm݃�%���C/�>f�_�{�����1^~%~q�o����^4���׎�	&݉�hh�N���?����M��g�M�SS���'c������q�5�p�ثq����o�Y�߁_O�=��`^/se=��8pԍ9V��,���p��������n�9Z�܋�0l���]�@���NH�I+d�5ݟf���bU�T�Գ�4�ί����iQ���+*Pg�t���à����(\���L���oTM�fd��:n_��ٳ��\��cߞ���d1�M�]�E,�����	��;��u���RJ������IN�Pq���㲷x7���W%�"S<F�`F�Q���_}*H�Yc)W��k>��<T$����N�`<.p�:����Hi�0����v��dd<5Ȫ���ѽ��ѭ�ت���k��\h�o�Ԋ�����4�\����=w���_���2ū�Ґ;J���s�`�[��o@4Q�C��C�D��C���D�}���1�D�	��]ͻ���U�t��d�;���ϲ��ɯ�-=(�JC��w���nCv�f�m�޽{s���3\�B>ć��?�8�ʰ�wN�����_�N��/q���¯~}~������;������o��}ֹ�W�/�����;aμ���U�o��i3>��\��	��)�����R�ߨ��D�g/>ؘ{�ٝp��;��p��[\Z5{cJ�*�W��hfP��������!�7�/4���w�FY��!�ܖ��;�rR+>;2Oj��|�+��������o6�=���k������g��nMܾh,�����pKUi����8�'k���U�Te���A�����E��	�Fgc���}'��'��Q^2�(]���Sr�̘|{��3 �c)N%{�Rn�A�|e��'ݞ"(��Ĉ��9��bDе�'�5�c�9���C\��`JsW�T�A6����,'�*n�Tq-cX9�q��5���4l]Pω���F4�I�Ɵ�]Ɵ��x�����n�ߌ����|h��W�Z�P.ȿ{�����Ѹ�r
��kkk�D� f)���ڲlP"����<po>���8�C����%������)68N�2:�s܃oçܺx�[{�<��Ӹ�+�{}w?����o/ᡷ��_��!^��x'l×i�zV:^�L;��ة�*+�<\�Ad�Kg�~�\e�U�����#�8
z%t%>�m�6��ٳ�(3*Tk3c���Ng�>�f�#���'��4���2�A�aB�2�B�������.03��1ϴ�p�!l��ܲ8�����]���p�Ő��$����ݚ��oii�����,;(��q���f��ʬ���
ю(*r�lXtT/g��8"t#�����(�R�QO��>E�B�]*�T�{�
F�S����K22<m> �ݡD!�zU�űV
!w�Q�R/�����x�g)n̔�I�hh�2����X63��G|�%�}2�t
)�"�3�i�,���	"6��h 8�dh��9(ei�aΠ�@_=P�a�ѳv�n;�N���=�~��ae�S+}���)�����m��V�h�t ����G���C��
�u!�P��Hg2��꡷f��ˮ��G�c�9���z��6����8;��a2�4�9�j����OsS3'�n��2�*;����,Ш��u<ؐ�}�3D�v���DƢ��pα-ң�m�� kL�&q���e�p�`���J��ե=k������W	�Vv�a�˝����n���P"a�$�S�,)qFy23W�J�����AY4�@<�J'�<���[�w�(��C���)G�%,(x'W?��8���LT4�)J/�Y;� 3^ �" H"�J�rqN�H���yV^!~��o�&0�I����ճ�\Bh�X��	hk���k�C��{�ƂF����ם@�w2T�TZAj�*�s�U0k�\d�Xo|��>8���r�����k���\���hŞ�dj!�r�q{@��͘9�z��3����-�|^�J��j�eC��޽W����>��ɧ���O;#9̿B���28>���Ȼ��--ݠ�ʿ�k3d�k�09�;�'���W�*�����Ca�S�t��y>�d�����f��M��_O�!S�c�/�����9k��>���Zs�2��b ;�� ��V��`��~�Dn��B����K]2]��%����\�@9��a%����ǼTWC�R�v#q�1Tf�;�}$#*e��*�QuK�pg�j#�]�X�+�(bJW��r8�]�fǕ���E�<
���v  �IDAT{N����U��5s���=ztG�=���IO���j[E�{Kwo���i4kP]]�������x�������g���8����C�c��v��[���_����EdKwm�h���n�h"�)o��+�Yk�����@�7l?�:��}�p�W��/ƨQ'`�A;b�5V����VQ��]Y~N:��inl��U�I"��B����c�\������Ai�<��JeD�7��?s����Y55�Gsr��8`�W<][\�/5����7��ҟ��ij����2���������� �90I9�e!�Sg��8�ɕN/.���Q:u�X�/�$S�.�0���`6/`�"��2�8�|R\
�����L0��@�!:�9@?�ټ���)n�0�2�o3c�ڎ0o��Y������ݲ<Z%k�=G�V�=t�#����� t�Җn]ѝF[ƻg��`�v�|���،u�Y?�#|�p�r��8����J�x�����[0�[p�-��f�7�|3n�[���N�m'���nä�o��	p�W��_����`�;b���DW����=m�qQ��+W鬻*խ�갷����J&�2:ב�I�q(}�#���ͱtfU.7���vxCs��UV�3�w�ާ��?���P�\��s�M�KW�\����f'S]S3�F{;�DR4��Hvao�C�C{��T%��0f�]P\e*_2�,S!˃l~������������R�c{Q��9���2/d�r��*�2 ���,J�R���W�4eE�7+U�n�.�[�:���tR�<*'�6nO̚5�ޜ��A�PÇ�ݸ�ݻ���5�X�+൰��kҽ��]�[+�W�^h��~��|���g�aƌ���ϙ�l(=L8GS`,3��b�r�,��K�a��Q0<�G�{�����8g�g2������s+�U+c�QZ�[M������Y.��-�5\L�*��m�V�=zt��6�O��U�岹!����+�a,�p���o������@V)����=+�S.*�v#�ҏ��1��#����|Z�.RJ*��`�]*�H_K�c�(���"�K�͌�@RyE���feHdf"Ti����ܼR«Ψ�e7e�x� %C��9X�G7Y�0��/hkE{�s��<g�\̙Cp/[���3g�s�7Fڸ��0m\!k�P9�J�pd���Lɖ�w��y�Y�����4��C��q�ӫ��FqA3�Kc��]�������������c�5�:dp�`��+mnu�nݺ��W��v�l&;(��agneG�p�p���~��%G��L�[�'S�D ���1�O�Ѐ�$	'2Z��h� 3^�ᐬ�
B�>b�0K�7�ҩ�P�eg��Q��a��N.a'��rj!�� !�ğF�;@.BE�Q�G��A=�R
F@|�)�HA��M 5�(<�?���ʋ�Nnѐ�&d�x�Fw�l�.�h�����f1\���u,/ReT���oA#|f����u�g_���4���c.T�Vת�a�����D�D�j,��s��O�Х��-�-ck���� v|�q{�mfC�vZ�!M��|��
y�F���%rwvU�����Ґ\(&`�}d1Ea���ZݱoL)�g����f)�8^L%�5T霗gĎ��n����Y.�}x�[�(��lo�c��1��cf����%Px3)Ai�(��a�{��%�raf����	�?x�W�Z;nK�Ges٣s55z�b(�� �?Wħs��xU���Uqb��X��bI7It!5�����_2�ZyWWW��f���w80�J�����M0�,p�a�)�`� �,�*?�0^c�]���>}p`��(m����.t<�w,���Ph>ŧ��*�����ǧYV�J?3������H�w�;�.N��$�Sy�A-3V��/F��.�ю���+��9��]=��i�(�h�+���}Y O�W���>c^�8 ��ݎ���L.7���zX]]�~�1�����ѭ��G�O-2|R��[Ӏ��rJ2Z$�pk@p���B�N����L8��ɀW�r8ȴ��<R�V\}��ˏ㗶�l�5�)�����U )�rW�b�`ZZ4��
�1�<2����VX��/Q%S���fF#��l;:od��R��%�<g>}3Q��Z�Q��"J���)��������ay/�����:W2������\u����*}�b�������[�X��=[ZFs{b��1��ɶ���-9EY�K���M�H�W�MMM�9��։V;2�g��8*�x�
��I�v��P�CLR
v��R��x�0T��/qpQ3I(�)�̼��3:�Q^-��r�!�a�!�@�fJ5J��5�É
\)G��� z�G��Ɣ�+�rzx^�
^Ry)�4*}�"��o�8������p�Ug�Og�#r���ꪪa����TW����j%<�K��55��G�ū`�b*e���K�82��2&\Dh�	\%M�`��iG#.C.�{?!��h5���W��R���T�1���4�.p0g2���`f�tf����q�N��2H�ް1�Z4z���Da�I���2�ܝȕ��\E=hqU�Π��[DQ<����9�A)"A#;��ʉ��|+'�!����6 � �����_[S�O��2��V[677O������k�Z_]?]� ɱ�j�-�%O
��h@X�!8��j��)|�Q����6���ꗩ��Oc�Aâ��a���Q�[.�[����2���T��@�h�V �աV�.����s���<<�-�0 afF�y�LDQ>�"?^s ��ᘖ	ft����`y\�rʭ��.���rI�ȎL��#�D&�A=���Q/C���Zkj���0���n`MM̀��Zm/��4��/u?I:����&���joh7�~��u�%��I��BTF���z�J�q�;�[dd��[.2<�޹�V|�߯�������P�-� ![]=�t�@7(���s9R"��#�7$�ɵf3UD�����~��\6B��jh.�Ӫ�U|���fs���0<��0�`����\M��\u�`�}9��M�����p����ӷ!F��ٓh)A�ī��k�Umc]]������%����^RZb9*��1���
�Fo� #�dg�я���0!B3itk�� �&�J^�Π0JS��G}�d�P_?��*��2�e_��,��w���@G�O�M4�h`��b�Bb�����$H4�u5�诫�$^��D�����$�h`��@R��V���o5��O4�h ��b�@b��b�d$H4��j 1���������X����@/PEI�D�|7H�w��$�D�,P��^��� ߅�<$ ��D�,�H��0I�$H4�襱$eN4�h`��@b���fN*�h ��Ҩ��@/����9�@���Bˠ�^.�-�d��Dˁ�4rR�D��N$z�l��ԉ,��X��@w�H�N4�h �����@/!�#�@��D5��I܉,�XK���ѓ*'H4�th 1�KG;%�L4�h`9�@b���FO��,j �Ӳ���@/����)�@��eB��^&�1�D��Dˢ�,�jR��H܉�J$z�l��Љ,H����I$X*5�襲پ�B'�%H4�dj��  ��Ah��   IDAT �ѩMFįh    IEND�B`�
```

### `src/flows/nudges/assets/protect/candles.png`

```tsx
�PNG

   IHDR  h  h   z�a�   IDATx�}	�E���zfs� ܄$  ��
(��5����K�� � B��D�[T4A`�Q�+@r_�dwg�����{f�Jd7���ԫ��ի�W�������DW�@�@�@��j� Ы�m	N��� ��S""�1#�� �nr�b�@�@ǌ@ �y߂�!!] ���MS�s� ��b�C�@�@��@ �Ny[äBB:C@w����a#�C:D@w���� ��z�s�@�@��@ �q����0Z�@���� Ы�}^���4�@ �f!	�����#�?�}�!!!�� ���0L�@�@����@ ��`"""�NX� �N^�aBBB�@@w���""�1# �c޷�u�@��J����] ����BBB� �BH!!!�c@��w%�"��E ��J" z��="""���^~��E�@�@��*�@ �U�0h�@�M�@�D  t��5�"""�# �c�0t"""�6 �6q�V"����� �1p�Y�@�@�@[G  t[G8�"""�# �#ne5������ ЭE&�CBBVq@���h-�7@��uЇ��t���79L1D D�cF  tǼo�����;+Ż �+%�������� �+?�������� �+%������`�b �bq
V!!!�� ���0`�@�@���E  ��i�X͝;w���|�کS���R:�t��Y�� �����O?=���n�����+���»��8 u[G=�"б# ���K/�4��nr���g?�	7\w=~���?>|a;�� �7��IO|呉��ӑ�� ^}�<��Cx��W��p}����� ��p��M����HQd��r(�b���L���h�+D D D���n!(+[կ_?t�у�r���$�3g|�'����RR�@�@�@��n��)�5
C��Q3�pW��_���s�+��M���N� ��p#?��cF�^�z!��d�B���ӧb����A�޽{?%(D D D@ �(�1:��O}�SXw�u�_)�y]D�0{�l<��G�؃�}�@�@G�@��Uy���̧6�th��P_�����?<\�g�~S�L�tU��X�" ���ɦ�7�{Í6B>�w�.�E��E̜5Ͽ���vr%""�A" ��nԠA��|����0�w�1�:4����1iҿ%
(G��eU�*�n�݂Ol�%Ϟc'3��a���x���0cƌ��j��o�@�@ǋ@ �v�g���t�O~rk�?�Y���ݺus�~��������ҎBBV�t9�~���?��������1?�{�=�O�~�9b$6�d�t>��@Z\߉~���ӝ0V�@g�@��G�觟~��K/���/� _|1�:��aW]yM<o��}���5򩭷��:�"�EK�.��|����
�"""�t�~�w��0a°{��&?�4^x�9L��'\w�u����6mZ�|�b�a��`˭�Ā`ϠEfhhh��o������ޗ�BBB�e z���'>��0{�ߵ��9~PW�o��~�S���_��E8p�#�F���#Gq�ؿjW*��ϙ3���X��u�t�.
����;�|���r�wϸ�����[o��K/Oh뿉1|��n�]���
�^t�XDm�b<2��+D D D@�2 =tȐ_}r�ѿ?�r\�a�����΀�O��뮻��v�W^{�����nV�I�h���b�O`@�����B����:���x����j��C�!!*]�7�l���k|��_AQ,�F郺\>B�G����Oy�q���<�M��6|�pl�Ŗ��9���"�9��;o���l�΅��#FX�#�e Z�`�����O:y�n�}�"��d�KGf�͊ŋkq��7��o�̳϶�Nv��?�s_�@/��*�������9s���)D D�G�K���v�ٮ�9��yl�WwG�>}|��t.��"�^r}}=~N���6|��g_E\Æ;o�ȑ�׷�X����-��s�b����j�aC�!!(]�uo��b�|�Eg��^�ӫ���	$���;��^{��ɓ���խL>l�������y�1w��¨]�d[ɫ���!!�2]�p�`/��CN�މ4p ����"و��w�.���M�W��;�o����9��J=z��t7�����`���+��t�tY��-_c�5�<��s���C�����ԕ�U��t��w=���?���u�~�c͡k�l�=�~��7݊C>��?.��<��y�<x���!P�@�@׍@�����c�ҋ����CP�K�8��Ӈb��G��3�:��s_�ߟ�����9�W��k��u7\g?���v��GZ�^������!!?��{����k��)��|�;�5��YߗN�������/�W^qu��ce{��"""�u~�{E��._��v�\uv��E9����q�~��{����rx���q����'W^;Y}���UQ""�h�t[8��}
l��f�ύ?�<�1z�����lf��b����z���s�;���
h��n�^�{=����8n�8t�AXc�������;ӹ\�S�w�~��`\<w�ܽ�t�!!!;���v�X��{�����[��F:�63t�V3��i��_ݍ�����N�0��.��g������剎;>��'�>��C�:��#��(~xhp`63D� �3f|����~<��sm��W�@�@��@ ����Ol���8h�;�9�|z�� �����_ϚΜ5����x�@�@��ʈ@ ��⦛nzȷ�o�3�9�X��N�ѽ��G�ռg��Xk�5�H"��#�׎��q�=�:�s�{�����F��Æ�A��Zk�_��tĈ�Ǎ:�·�~ �!�~�zϯ�a�ƍ{��SN�q��1c����?��A��?�!�
�!!!ˍ@ �冨���[n��q�k��~�vcOk#7�{s���sX� �1��#��>F��4D D D`� ��������U� Ы.�]o�0���� �*\�8D D D��" ��b�&#͛7�+/��߉��_�M����׶�@����v�@ �vyk~x��/�����;o��_�u�=��{�v�c��/���W�>|8C���.�W�[�bM�2��;n�c�-?��g���ll���믾����
�^ry �e�
Xm# z��5�v��'�3��XX�Q!�ϡ�[�5y�_0���]�}��K�X�#�Q z�1\<���g�<j֬Yϝ;w��6��sf�3|�#�q>jE�b����"9��\�B����N�������<p��~���w��o}k߉��o|�q���sN|������so<q�#�/�wҴiӎ��U_߀zi�q	�;ե8n��%�RM������x�@W�@�觟~z�W\�����x�����SO�����G��W���o�%_�3�<'��}|��÷?��C�=���N>q̘��.�o������>�����K �9s�Q��CP(�cs� -�Q�{	f� Y��(�(D D��#�1��� ����s�K/��:�&��<jx�x���a���9s&��}����x�v�>����c������M7݄K/��{ƍ�O���cN���?�%�q�ku$�!�J�Z\�Q�f��ih7
Y�@�@��@��3f��P������t���W�Ǌr�rQ�m"3���K�b޼y�:u*^�5��⋘<y2������5�\�G���ٳg���i��O�i�L����BB:h��w���?�5���b�����^��a
�b�%}7I`&r�	 s s�#�����֭�%���Kx����W���L��/�Iƣ�+젛�%9
�e   IDATW����_��sg��~��p��՛ ��X��˖|�\"x	�"�݊�2/��q�-�����zЮ�W���D�*,�`f�?����9
�H�>R�ըѰa��;ꨣ<i��q��w��!���8 ���7�կ��N_�"���v�|�ͱцa����k��~���G�<��9�y���v	n�>��8p����tˮ�r��`�!2B3��승�.�qMV<D D��E �x.7�xĈ�{u�Qv��ow�9��}���ƌ?����9w�#g��GK~x�1��q8�����c�?Gy���p �|�o|_���;ⳟ�,v��8��C��λ<��Zk��|�U�����	���t敎t�� H�3]�2��.��3�__%ӎw�СWm��c�5j��l�]�]w�ž������j'�p��6n��;�\;��s�;������?>.���_@@�����;�ȣ���O)�@Yd�=�7�,�	�@)���"�!#Щ �����k��I�5j����v���q��S���z��_{�G�8��#@�d�3	����C�"�A#��A=n{�2�2�A�q�|���Ps"Й# ���]b0w�1b~�)0�4�9O9�*�ApVt�t���x��=�'e"{M���;�I	�qN&""�1" �cܧf^���w��iT4�8N~�Yà�0 �anUcGK��XZ��H�ȏ?���*��!j���� ��%�%�0�Jg�dO�x�x/�?���VT�t�tQ��x7��ǾyN�q��"�ԃP�&# t��R�@�@ �r���I��.9���MU�eWW9D D�CE  t��]U�
�Q�͔rEEC���>��&騣l����� �C8�՜l������f����`~��P����P(�ϰN^�`��Q�CB:B@��wI�,`-
��ϟ�}�aؚ�>n��� >��WK	�x�������
��%�!<��N�Lr�ܒ�|����ga�Q.�}fɎY�i��d*O6 �P[���k���d�b,��Eݒ%������9��5#��f���N6��>�g͚u�{�7���_��K/�8��'�������o~����/<����0�N:hiI�R	uK�����W]�+��
W]}���j\�u���['�u�m�C��M��_�?=y�,���s.ܹ��.�"Й" z�͙3����������-���wŗ_qy|��=z���q�E�u��>���t��8��p���E �_��d1�Y�\�KX�x	��\u��	]y5���*\v����q�������������k&�v�����h<�)&��<D D`UE  �*����޻p���o�����뮿�+����K.���c����pɥ��j�vz㍸����~�G��O<7�)���������Ӧ�X,���H7�)6�-�F�z��}�c�>��i�X��}J��p����;x�����G�o|7������}|�/��^{����so��[o߲
B�l��N;Z��;���ߙs���7�ͷ�|��_�����.���t���?cʋ/s�a�)6��M�|�oO�ֿ/����1�^s�;d������ŀ����<�Hȶ'l�9�~r���V8a�O��7�1#F�����M6�~m�=�_;������zLy������W\�s�������G�=)F�BB�=��)�s��=�o��/\y������ｏ��mztî}�`�����8|���ސ�0v��8c�:8k�up6�,�g[��__]cM���Q����k��H5���V��� ���������8z�H�<r�"P_��V�d�mp�v���I�l�ö�_�hS|���/�ë/��^����xr��S��0!!i@��hk�����Í7܀���d	6��_����1��=箽6~8t(NYs��&�4���O��M����\O�B7�r�[4����A�K��b�8	Q�C���#����"�L�6�\w��ѧ�'����������6��?�i\��/���}��#�O��#�#��� �Bt�+�,D`��@��y�	�6m���7��ē�I4�<φO���N�����s�a(��'Aآ�G��r���"� �-����b�a����{a�|w�������s�QCk�a{޺#�3�<��(B��&�����(�]��yX��<xM������q�~`_ �<�����;�>���w����6�@Ԧ���=���굯��:��b�\��� ��o b,,Ũ�Ŝ�D ��c}Ǚ��"�!��6h��'����n�o4��'��!�%���p���<s�
�|�ϧ��]��#�u�ܽ�{w��GO�wo�<b���C<��!kb���Ş��]��G�l�5ΡP�d]W�,D D��#��a ̛;�/�.5F_�b�莈��u<>X�Ѐ%���+��2J�<C�)��mjc�w�555�ޭ;�s�<�{ol=h-���8��<v�V8u�O��-�ƾ#?���#8[�E9DA���z��!#�ZXl�p�>����7�B�[�@��O O _��� ����.�E�X�r�����@��C���}هy����(BM��G5ȕ�b}uK��@^(�(Qg� b"7��Eݐ��1xLRb�8��u�A���|�^�u��A���6�ᆰ�#m�)�N;�v���>��߆}�;�c�@t����'r;~�#"�ǳ����0�)=I�aI�����@Xs��R�h��bo��{q'ݏ��>��v'��@Lۘ�Ph@~P?���0��1p�Q����s���}�	�6�{�9�xԌ=�|9�sg����#�S��}�(�����7��. w�5�ӊ~�`7�����aOLF�A<o!��n>��|cx1d!!m� �+#����P"�ʬd�1P;�Ϟut o中��Ѓ���RD�ֳ'�뮋h�`:��l��a��]6d09i-��`���pݣ;,_#�x��Eڹs������g���7�W�������"ݣc����JEXl�0�o��""�N��k����0D`�@x'��iJ<��nY�.晴	��6RDx�V�׀?���C�������n�/�;�!�����[�����M��9ٍ�v3p�-�o������G�&?���i�eF@V��"�zI��v��8*�R�@�@;D j�1�<l�K F�Xe��6�1w�1w�� �;�HHSgs������� ޟ�K`}�=��w����Q~�g�o����)�o*0��3f�/����w֦��D��zr��(�|���ڌ�Q�#qjB
h�*�z�пYb�B�%at��\M�&P�шsM�w���Z���:b����������D,G䪗]2��i��"Djg��ķ�[� ɳ?u13�Fq �q)D�="����t�1���8b�� �fFn,�q�3m�	б�X��rL����w��y�>~Ȉ�<�'(;er�ٷ�"�O16/9K�)!�195�8�q<c���YAwEሃ�)D�]"���.�t�Ǎ��P	7K��\�K5��U�I��	�qY^X��"�5k�m	�qJ`�	Gz�-�'�_�c�� L/�ݘc��Cr�>&��h]*��Ő�t���	�n�; ��qf��&yL� ����%H�o�S�����5�=3��r�۫��v�$����Dgޒe����;c+!�FRm���v�@�N�t�a���9� &��1����Vܭ:z�ܜӈ6pbJИ�sB��*�~I�6\��%g��
AX@l�97kA]\_}`��1m3Ru����� W�FI" �"!4�37����r.���x��ҷ�Ωp�%���4�D��z�*�M�N\@fD�XGu�"\�=euH��B�@m���G$���,Uݘ$n�Y   IDAT��Q�	�p��ƪ�6�y���{q&
	�6�i�=6[Ҏe�E9k��KD� ���G��REZ��u��Y�7Y�@�@�G���c�<1�ѡ��L&�tc�0��c��e� �*9Gz�K�B�l�1��Xi�$Yf	�ލη�v"�c��e��t�P�&���ti��kv����K@�C�	��(q��.e�"������AZF$ի��?�N*p��,f/W���DV���k&3Q&@�;hb2S�`���b�V(�(D��G����wzX^�)�e���� J�!�ub-9���T��rZ�V�Qfʀ�(L�
w�,�.����bY)7
߃V4��K@�K�+�	���W�����$@RFz��8U�e]e�^�qp�dw�Z��H��X�i��S)f��bH!!�� ��������	%n�3ϕ�t��:�6��L��|�7��zQ��y|AS�)��j}kC���͎�X���@j�.VB
]���@@�@�>�����}$�)�$�q��o{X���QiƼQ�%Veb���
e`U9%��R	��̂�K���VC"\!!�� ����	|�X�TL����GNa�+>D���=�U�'z��T�� P�ٷ��F����E,}g�,����� �-n��ɱ�zA1�
��� H�d�V*�@�U��%	"U���j�Y!0懂:� e�	��V;���m��V��⨭��v��9��/����	"�" ��r���g��F���KIL^D�^*k�����.Z�C��C�;Q��*T�Z\m�g��7}q��[E��o�r�%��_��W'q�/�a�/}y�1�O�2��U�R6D��" �=BM��(���EV�9V��+V(�P��D43T.��sl����iZ�:��h֩��� @�X�@[�,'�}�7߼�Ɵ���.�O<������3���_�cN<��W_}����$�"�j"�� z���c��3hQ�N"��O����U��+�I$P7�g��zƂC�sϼ%V���;��A�<��������ɀ�?M�6K���y�&u�ݿ��Y3y�R��^�����������>s�Qm�D�8D`G  t;܀X�P��v�9;4�@R�Ĝ\W����4��6���5U�Y��$��jB�����A�ȕ��A@��e)�Y{�܅���+�`ڴ���� ����CN�T[[���1,��h���'�"�*"��A�ژµ䒙*c�c��:�c��$P}Q�Er��]�J�]+5��ҁ9��ErԁY�
@�@�/	�}8�E7���K�7�?4.��T>�C��Λ�b�08U"��G�C��=��ah�a" T�؛+Ŋ�ج��$�T���� ��)�z!C�s' ѳ��2=�B;h���-�A�����	�r �v���s���5%����$
��:�V�9	3�Z���^\�ٶ�[j_mgׄ�R�YJ�B����	�ܖ"Xs���d@�Y���Q�of&��W��g"�s3�v�\B�@��@ �v��q��T`���<Kd��6i��k(T��u�N�2�.�zV�Ec�EY�ݳ��jm��F��S�8��*��^���2ߪ�A�~7�@e4��6�@s�]WΜ+�#;Q���&ҿ	���րpJ-2�K�(-V�:Q��d@�$;P��Yr5�/+���x�e��>�EI�% �8��� ��pg*����!��Nr
�bϫ3���U�՞U�ЂuL���H,�3	�����,�;q[h5=u�72��N����q?�kDQ�\.��i](�t��n�;iM������{�z���,s+Ϥ)*�J˵ʆ'�@D�z# Zd�}����ou��Ya��Bb$�ˉH��}�.�!a:���V@���&����$�$Ts��<��.emʒb�\�ٮ�͹�lT��T���x}ֵ�$J��\ܢ� �)MB�A˫��@A��|t�Y���f�u!�t��n��jDD�@����M�=%J����ˤ�	Ȓ��Ե�W7od�T�fe�|���*��yYY3K� mR��J�Ng��hID�NƖ�	�Id�">�qΠ��>�uj�Ѽ��/��5�#���	�Q!%&*RCو�bc�>+��e��,�M�+݃�����
Pg�ف�v���5�l|�ѿ����� ��p_McxV�F�2&VSY/���IN�I2�UU�b���**��35��[�ҍG�����ژ��E��5�����r!!�0Q'���7%����+t�P��dڂ�A���%h�n��m�JSY��S�T�xF��~�0E�	q	Q�>G
���O24��%�tW�@�@ �v����-E������K太J�%&�)qʵ)n{k[�m���U�բ*Ӳ����ι�c]�����xκ(�
*�=�j�c�[�X�SF�,�Us`)���� ��rGf$���8 2'4�=�������jM
ƪ�Z\T�}fLR��3Mv����%��Pm��Q���`f��n�T*�z�?y��`�]��Tt!�%���N������-kP"�ò �r���L��iO�VmR�����I2x�/���Sی2�����g�]s�y&35�A�S	��=ͱ�h҉J�篦i}(�t�ty�n�� �N6��M�K��W)J��LDǴ��L8,*� ŉ��JV���ZX�c�/3Hf�k*�J=It���0^���"���B���*D�SD  t{�F�H�V�p�;]��S�@�0��ޘ�\ Y& ��2.�s,&��&/��􇑼���"�	��tť��G���L�n&�s /�@{TB�#u�I�ns23�_�~	�NͭGeP� ���7"o9�"���6�*U*j�>����39Gz^fu�ˇ��!�K��Y2����3A|tmm��W�@'����NxUL��0�!��E*9����̨,�ʉY~e-�c��x�<3rh���:T.��cȎGfƾ�? 4$�Y&%���mc���G�
��qtB��D  t;���nFЫ;*�l�,	x29�^�t�j�2�pe�]��bŒ3bс�T��y\�w�J �AS6�^�V.-��x�B��>e�ZG;�B�&-X�`����o��[ojB:D@��m230��U-KK,�3���f$��[ 5/������Y���PR;�H߃f9�ZH,�&tAy����� �$9g��x��d��U�>p���C���£<�����0Y@]eĮ�N1k��N1��{��W�2�<��/W���
(� ff D(_*eTV�&h���!{�	�E����]�"!�z����k�6�s��{�~*��o���t�=9�E�r9yFN�2䶿,��E�a0q�l�I����N��̡cM�(c�ǔ]'9�P�q"KYJ[�� �
Y���$�S�u�U�J3Ϟ!"@��Q�y	��$���x�\__���b��9X�p����`��2@�fɒ%x������o�u�o����zo����W_}��)S�\8cƌ�t�A�B:\@��-$�	�l|3ފ��ٮ���w=3�"���s�����,&�ɓ9��D1:P��g-��M+)��R�F7o޼�L�6����z�^|a��O<O�˄x�&L��7��/y7��^<��S&
�s�(�/�7��m�݆����t���Z\{�u���p�M?���[n;�}�����ѿ�����O?��[o�u��W��La�#���>	5���� 6R��e��]F��m�>#H@�lb[.��m���e&[ϛ�c4x���*���%�%A�C� h�ʝ�/��¤O�?�Ǉ�zh�]���ګ���.�`�q���O<��}�=�d�v�8\����?O>)��9.J��9_tӦN���ݏ;�w�un��V�|�M���kp饗��s��)cO�	'|cN��tΰ�z�<���'�Rx��7�U?�����<����#�H�O��ޅ��_��U� ��b:�r�r��D��T�g�A�Gz��^g0��.�Y�U�^F��   IDAT��D���ģ��Z;i�c!�~��w�<bX!��={�>/���s&���믿v�x��Gq$?�8��cq�����݀~� �|�?xo�{�]�ϒ���~���g��f����K6�l�	�o:�l�16�xcl��Xo����:�`�С8` �<K�1ȟ��0���R|���p��G㲟\q��C��;�\��VI���wo���N8ᄚc�9'�9e�v��?��s�_%��AW��n��s�I���,E?b���Ü �\6AJi2�(&)Q��'�$���9�Ŕ��)�bf��f��Pp0�5�VC	�VZ��I��g�~�ݟ����<蠭:�\~ٕ��_��w�L�Θ��鍵�Z믿�o6[n�>��Oc��v�W����Ϸ�����:65
� 0����"_S�n��|7�-��cǞ���?�wi|J��G?:�Ɲ��}�8����n�a뭷��l�^�5�W�t�Oq����3�:�g�}�Վ���^�0n��î��*<��3x���>�s�9��V����}��Nj5�@����)�1# �P��$<$f�|%��d�Kᚲ��T%��F̼o0oB��beN&%}��:�@�UG�ye��x!�Z������~v��??�3~����_\��F�g>�-���������1���9�w�G�]|�A��7��ѣGc�]wè�7G>�G�����\V��[��Н|��C���kcغ� �߈;��F�t0��_����:���8}�i8�G?�g���9���#^��~}ϯpڸq���[�Y�h�{�����?2�/�n�޽�u�ƹF>����5����6���Y��@�$t�i���c���%����&;('��,k�Z�Y�v�D�M5���&�Y�M��1V�̆�t�q�o�3����dP�3C�!I}@��o����ߎ�����3|�@x�A�;�9���?w�_�g?�=�%6Úk��^<��6p׾x�,�]���棁/���]�mTofБ��+
|�乓 ��9
���ԋ��S��ҥuX�x	���э�w�;�#t�r�%���s��'?�j��ĉqϽ�lK�<��٭<mmm���ٳf������a\�M/A�F+����)o��v�*�z����7�v��)�\�PL�	���ra*QVW�3ei"ETWP�(�Cbx)�|��
��u��9��g\6�:���՛���͔�Q��d�k����&�3�(��<އ��o���9
���	�K�� �ha--�%p�%�J0�{�/����v�,�(������������[n����yv���kﯣO�>�x�F����9i��`��XT��c�|�}��G�9��<������0u���%�5��N.��	_ �r~([�gRQu~�T��"u���	|�an���A���҈K�$���{d�E�5=��M͛����K���@���gEU3��R��K&�-��S�Ō�GϞ�`��	�kc�E�.��u�w�%%?	�%�Jܹ��1w�>�iF1���(t�!8唱���g����qcO�~��5�X˧hQ�v���b�,�9�ȠW�^�c��C�Ɔm�u�]�@v�b���Λ�@/���h�df�%Qh2��"H��(���?I@�V�D��G��!�W��ALPfB¹TY�d�$��ĘAQ�X�$�(�w��I~I��i��\͌��V��i<.0L��`�ʴ��P�
����v��aH]}���<�Q�����%��o�T@�;��s�n6&P�Br����G��P�����#�Ћ�ߧo_��? =)눣[�|9�E_��Q?h�`��֚���z믇7��l�	����Yu��}@��c�Q�ai�R86� bIp�vH����y9i�f�
ű�A�R���l�~�-�`�6�i!f�C�CL�LILz�d�dMZ�M�N�%%�^R&��8 DmZ�H��="�B MD�0�������:�j����\��Fl�,����BC�es(
�Di�c���	�C�]�f�m��#Gbs~P(��(�5�4���m�6�t���o����`����2d(������^�lf��4f�_%4�P*&������4��Ʃ����WՈ*F1�,�Se�.>]f��l�Z�����LhF�D�`.9���@[��u`�И���Ԩ$j�Qɠ��f����+����A�AՀa�Ǣ��6�v�4�:���5���;d߭r�<V),�-Ɵ�f[l��~n�ɦ��dCC�δ��5�\�	��� {&�A;�ݺqw��1�uuu<�ֹ3ϻ���|��/�ԟ�.QV#���^r��5�̬�p*f�3k\��0:}@��-��O�J����h*���	%��w��(�ֶ�i[��DmR�v�4,Y
"�g��A���h�-.dF3���Y�B2?@1�W�^0`���p�̛;s����ٳ1;%�Ns�b�fϞS��5kf̜�>� ӧO'Môi�ȧ;�6m*f͞���03����c�(@�T�_��E�/��'3+�D1��C*#\]4Q{λ���?f��$W02.
�r��g���b5��ͨ�qh�%�U_&d�$l�U*��,js7��\�.82��Q����(^����1/�p^�*�O���Qѝgɹ|�^L�K��ٳfC�;k�L�Li��Y.���������y�7o>.\�&k}��?��xwыb�ҥ�"�t�d��#3��@��^}!@'�T�L}� �����B��"u�	����viVv����:�M�T��DWɥ��T�j$	�*�Q��h	����=ǵ� ���h"� s���gЭ�E��\��銼N�Pu��	H�&� �ΆEE��b�� �O7𜸞G#�����Ȅ�������md�c�/qW�q`������*�yZ$�3��N�[咱�Y��,43	���V���?���a1�Ը(}h#t�̣J���E�Jee�u�� T$9���]�H�Uގ{��r&�ܐ�r�������bq$��*�T��L�γ�d9B�6u�ͽ�8m�~�nkTfđY�Jl��+f�eB%�$��P:�eQfc�� 㿈s��#J,S�Ў�����9e眊�����U3l�5����ob$^2�ř�Q���ƙi�;%j�=��YU�>�;Ti�a-��Ɇ��w���#�	�؊�f)��i��Kf��]N�%RI@[&͔x~^.�w�jNQ�I�^uf��$��l.���NZ�v��(*�%��L!O���+�N�R�N.�aV�D��?���L�P�Q�I�"��)�$%'�2�e#3:�"3���E,�a�I���F,��ge�XWVHr��#� kG��*\R�E�wQfv�hj	���DE��@�Jt0�5& )�����,���O^��%� ��N#������O�r.��Y�Ov�h��� &����q.tTS�˧T*��/Ϥ.�E Z�|�ԮhZy%
8�	��D����L�q�_03Sk[N��[��ʢT�E�՟Ȳ*q�4�tA���$= ;�`yóK��s�/9,��N�,@��f��)O�̤g�J�,�S͇j��r�'�Y�&Ⱦ
cf��y.]D�r�Oq3C{]%�[��h��|.1��J�x̗%�꾃�L"H+5�J�-t�r�����@&-J5t�U�����a��F�Y����Le3$��PID@�D�����P�~�N�IUi�X��*��53_D $E�ȍ\�ʬd�.&�MɫҨ%��.�.r���M|��t4�eb�~Q!�D�А���9"���K5`�Z��3�Μy̗$m@Wԥ��K�vM6&
0���EHE"���C�)��3����A�p���?B�U�TIENP(h�"E���ɼ2��H@N���:3�	��ɨ�"�VT��Nh�*�C��hy��J�fd^�({u�r		@��8.���E0�bJ��q6�%V�(�#Ƣ+�d�uř�����|�%.@��3�&���L�DvlK�/b3K����4�mKc�$��CQ   IDAT������y�[qI�<4cn�����"�2c]D2�̠��M/ibN?��/y��z'ƛ/�:j��V%[P)���*e��z�H\�Դ3��?�8vO�4�R��&������J��.4�U8U�Bk�wD��,.��
$�ހ�%�@J��!�\a�7��z$��S2�����~9�����}V)�r�T��UC��q<��(���7�$�),?ї��}Q`���ꨣ�����C�C������d^�㤙ز�@�c�J|��:"�8�}dߪM�� ���1H�cq�	�I\v,�)p�ĵ����z5Hʬ`�,Q/��&F���A:	"�D���g$D�o�I2���R.��C�,o�{Ѫ�D�X_�K���Y��$v���vU�t�=(k8\Y.jW.T�́�[B���~/�yڪ�^Ӻ����d��9>ji�k��9�{���T+&A݉#��׉��zM͗>3b2B A��6���މվx�a]ZGU�ĕ�T�Z�͢DI��؃4dIR�IY�j��9�j	r%�F�<Hk�ɚ&��Ǖ-d�^��۴�W�h&��E�c+�vв�^sX�^?����!&5���c�%�mB��D  t;��X���# H����RJM�$r �m��Jh�nZv���F%�C$���[�t)1h5������EPL�)3K��f�jI"��E�[��1��i_.��0�B̸��_/�N:�^:���ڄ騂�$�g��J�:-�$��D�Z���r� t��n�Kt �$��.
q�R���!FKڰS�W�r֘��%U�A̅�L��e�
�#�mF�5i�g��Ec������	���X_���,��,��U��q<i�Ye"��~Y�8Ք̖J�Q��#HB ���!����i����ST�_��!A.�`��bԙ�@���]�'x����'D�K1�SY�X`��+Xv�eD2�d�i�s��#��I�T�. T Yd�H�e�

��:��%}3�̇� �C�)��,�%+ b��2��M��n�HmJU��Bс�N3�eI�FW~�>�X,v�˄ai4�ܬV���r��V@����g�P-}�#�Bu �JI:n����V���T0ɶB�kE��X�$�m����-��R>���8>:7�9�"�af�6-	ļ<�K|O���;+Z�SSg1�Qp�q�H�F��I���q4�/�S��������ĠKvj��Z9I����ﱁ>b�ٲ�K�2^=RM7}���GuP��u�����r핗�d�81��1A%.{'���E�,3�M3�(�Ȗ��ڱl���+�"	0�����`?U��Q�Gو�,�O�	��I�2r����B��M2���3&@�J>���(�%q��4����0}����x�[�}��W�׿��ub����9k�|��(
(�N�N�����ˏ:���Sƞ�����~|ŕW�7��������������>��3�n���O�øN(��Y����JaIrJ�s���ٖ)�(��񅲌Ț$��V��6����IF�$P@�q�L9��q-^lKGʾ��K�*�^�I/b��@TyJ{K�*2�Z�X��0�I!�DIä"s��HZ��N��HS�L�����|�A���?/>�3=i�I7~�{'v��O>��Sp�i�p��W�w���
�A����<�~}Ͻ�뮻pם����݆�o�	�]{~r�Op��3�ĩc0줓��r�i��?��x��G�s����F  t�ܺ*�pQYB�/z�<����W+cu�Dm<�j��*�c}5�90��W�vbNIV�%�~Ń8� 4w�q��7
���gqB7@JD�
�͒���(5u2YU/jָlY����X��S�*�E��-�oj�z��W^y����]|�UW�?8���ƍ=��q�E?ƕW\��~v~��_��_��g����'�/��?��� ��'1�f�{�G�����^k��&菞=���1�.�ԩS�������_����;�W_}5Ɵ;��{�W^?���zg!�p ݎ�L�ΉH��K@4�F�)�+I��}aܜr�'�N�hX�i����M=K]He)p��*̌ �8�A��y(��.�2��E�cF螒�5�lX����rcxSe2!	�认�h��̤O�F^�J	)g_LR,�td��G�/���x����u�ŗp7|n��6<������'��W_����ѭ{7�����b�-����������9����8p����"�7G�`fN���;ᤓN�@�,��̳�ę�5���?�N�4|����Ď;�D�q�ᩧ��{~]���3��k��_��;�g�� +�B��v��cD Y�Zt�«��/2 	��Q}y3�ju#9fID��撖ArJDD�U��s2h���Qʡ�+gq�Ѣ�Rݹ3HG��		�EV�2�n��R�z�E2�T�[��  �Wc{*ZH:�}�?z���������^|�E��������?�=���	z(�����#���G���:G�]~����[�b�ZC�Kc�:����#G��W��e|�k�1z�h|}ϯ�������Á��;�{,ƌ�Sxtrꩧ:?�cb��1��x������/���������1" |��vd/��侙!�(�,��&Cz 
~��G��H	
Rf]U1S;gU9�m(�7�b����)5j�Q+g� �%�镀)xbA����WɩYӑ�*'�h�R#���Y/t���D�2�̌e�RcZ��Ν��n����1a�QWW�����w��C9�~�P��o�[��〺�.�b�v�v�m�-6�l��\s4���b�����t�	����O�����-E� Q6"������c0��t�M�����ַ�"8� =cǞ�o�@�������������,OD�:D��ю�d)%-,B��eNL����\�p�Hwxj�y�es�F�8����C�
�GQ�L���u���SҺ��6�N��Hl���<"�⸉��7G�xL�Mʲ��j*WxgY�yk׸o���"HG���Ck�[o�u�o�c~�'x41���+>� ���;ܯ᳟�,6>k��&����p�PW_�%K��X��x-j���6��v1z�,y�]v�g?�Yl��2d���믏-��_��y���F�^=9ø�b& X�%GeQ�]xMM�����1n�i�o����x��)�4��x�)��6��C��" L����(�Q���D &��䔨�$��͈f	��8�'�:Z�KϞ��`�3k�dP&Zer#�T)&�v*!�e���K��%+���8��.�8���q�D�<������z@�.#��"7���>��$S���D_��5#7,�z��ׇ=�ؿ|��&���F��w���a����h�",Y���ՋN�_�n�`�b܋ ���v��'��Gp�{w�Gq��;�w���~��ѭ�b�}��"��r�:_�� �[��0
�狡���k�{C����ӧa��9�@W�@�{�������� ��U�2���w�1�0gq9��F�He�=�M��v$��'؃���4�UIbblBbA}��.,摇�@��M�6���QH0�#E�3c��]��܀6�ٵ�L��;���4����� ���r�̪H�������7w�̞�nݺaȚk�W�^�9s�_�%K��ni]�gt���N^,$��7;6�H��w�Om��|cƜ���N��	�o���5�Z��7會qZ$��Dr]�TS�^� ;ce=}+�Ρ������Ɏ�a-ҙ�K�K@��ͭ(�sQ���Dv�FbF�c��g�a��ݗU�E���վL%�����ԗ�3�i��-'�Ò(�!��"#73���6a�Dɲ�q�*��h��*Nk�|*�̉���`�h���xI��[TZiof�b�@�e�YW��]r	�:�k��zႅ�ky�����Е�n�{���ӧ����c���?p����׷/zt�3c�E�%���rM��s���(�   IDAT(R����ff���0و�b��X�׼����9}�Q�g��gU��Q���(�vX?�D�|�2aҎY�EL��%�F�풆1и�p��-�h¤1dI1��:����<v��1w�(Rn!��8F���2"3hks0'p�j�>SYR��|��	��i�c&�I��Q'?�"�m����,�Ĳ��]���V?Yh'�s�R
�1c��������zQ�"xd4x�50|��0r���fγ�7���]k����h�v{�lZ��=ɻw뎼�9�C.�1�Cj�����b^Io��R��U2UM��nk ������}��������������ӧ�,��hu�j%E �E��ܛiFr�v��/d�T��20/w A�����W.JΨ�Loˌ+Uciܴ`_�9���耒+b�4X�%3�L�ԑ�*�x�O�&�K��T�13�[e*�3!�W<�Gu��U�.&/L�H7�2L*eɾ�8X�ة�P�=d�%e1�'I2�����p�<� <x� ��F��Q�硅��?���N1�u.��{��4EMC�N��^F�D�sfұkJ�~u�}���8��cp��������?����+�M�6�}��8��wg;���f��VmQD��U�Q�r�����5#�p�s�j�ep��t\�RBЕ5W��1	"Sn��-��{���	�5^h)���ےZ2)�b�O��&*$��eBK#��,5S�s&�+F̗�ǝ/�"Ie�и��k����+�Q3�*N���|J�?Gr5�E�<Z/:����;gff03J G�2F?!Չ���{̘ r�[T2zVQ[�,Vj�^z���cO=�ߟM.ϳs���|�5\w�����_�p���EmP��h�j!���*Z���y^9�B�EX���C�Z�X���:�,��!�٦x L0�� ���IP���&i,'�a����vw	���"f���".�X�!O�g�Z�`�R� ��t��S%c����4�J��|R)a�#3rT]*��T+$r<�W��	 �A� ��ֽi1��M��7cdF<E��?P��*�@KoFk��I�"6�df�3��"�22 "4���i�N���V��.�>ӊLن|Μ9��+�u�t�����4�K��O=3���x�5� o}cE(���+U�"1�q�.��uK�Q��u�K���.X�s.��0k�<'�
��g� ��8w�%z�[#�e.L���!ى�<�t`�"���r<n6L_��qT��C� ����F ����]3���س��!����e�Z]+��&G?
���m
Ұ�M�ԟ	���1���\Q.���YB�\���đ9g՘і���IB,.7��ʈ։�I��8RR��WE�X�E�>&�M���v[��2e�D�m	�s3��P_O�]��ԄT��JbE�?���|Ja>�LR]�`C$�ŵ�J��� ��TK0��nY�,`�B	�� �7 ��32=��;�G�kؿ(O�rIĺ"y�g���y4�
�r(ɶ����XW�9��93�Ы/�^���7l�w��G*'�
��̝X��	Up~�Z��FI��`��j+��UW�B]��C/TH�(,P( p�z�%��0�@�t|�M)�{�#�9O9吕�f0�����{����3S���f�l�z�T�M@�B%���'9�� WD��R�� ���PϨb�@C���z�A�[}����u�9������W���ݺa�3� �-���	�GT��Q�Ma5b��v}%���N䡕���"�Q�e�R�Дc��tM��"����sw��;��n��V�ￋ�|�Ξ��M7�[o����c��)��$�?B�'$��I55f�&�e�����$B�\5�ѱfu�]�JP^b�˻g��������)�rC��	�s9�8�r^dl�QU/�A�q��cR��̼`f0K��2�F/�,IM�M�"T�(2�h0�`&�����y�+7��QD�r���#R������f�mr���%l���X��g��p�����|X ^�e���(�L��^�O��ꊴ-��. 
_QQ@�r1���� �7��EY9�<y�)O�j�[��s�������OO��O��O�"����'�=��κ?B�WM��K�p��>c'.J�_nF�A����R���]�(�D�L0�[�ό2��S<�z�1�1Iu�P�ɬj�T23sע�Ef�E0r'3 $&��5o��Q�b2K��f3ȑ^�lĥR=	$c9#�Y23��R_�g$��lڇ�����&3K�3�	�j�����*�v��+?�k�=1t�ژ�P��	п.��^��߸�_�wn.B��(�͸�
�z������"���rH�9�D��0p��iGܝ;��=u�R��R����uxg�<;��������y�-���$��?O↗^£3g`�v��ǩg����vހ��Z�~=�ͅ�~t⭵8!���PP"��s5K8]��.�&�-���4�GʲKv��_�L+紀ǂI�"YZg ���X#b��4 �$U<U�q�5�K��`f�HeQE%�L�jQV��f����/���E,�EUVm/��Q�s��f)Q��n�B��@�ީꑻ����}Ё���w?#6�����_�5�E��O��9Ó�HS�G���k �u��xNl��v��f���:����3�.ƔE��ʼ�xf����)��@|�/�����x�����>�\��3�����o���O}�ϝ��7�o�1����q�9�qȁ�\�ΰagS�j������3���s�U-��'3&��fƲ��¥��-�20$g"
;( ��cB2�ےG���5-g^g0�0�2A�)[>�Y��$���%9#3�DցT)#��,ѓ�*g*
���@M�������4v�̋f�>���C�<��Ǥ�4[m��|��������A�d��燇oq��w�	qG}o��_S�;��>�O̚��f�Ɠ3f��S���d�/o��߽�*�{�%���q�s�ㆧ��U�y
?�L�%_�������O���í�{�xMy�6Oϟ��8�F[n����ǝ�=���3q�'}��������?˹0<)I@����,dLj��X�,Y����z� ueBv�?U�R���,�T)�Xj+�L�P(�x��/D}�Cf"�*FJ���JR=�L�;%�l0#���� 5������ʋf��03��DdM��2�*��`03D$3�h�myek�(�r���d\�3+@��j�K�v��#��fÿ��^{�����<���'�9������t�g/�O��w���N�<��s�T\��O����8逸p��ɸ��{��q�SO�r�UO?�k�{7��?�����˯��_���x�|*��=S٧��u6��~n{����8�;���O�3�:�;?$0��'�w�A��6�����>D���\S"����e�02�Q0cN�@:�l���R�ڱUˉ@�P[�L��q�9=q��������I��7`f�V]�SZ�n՜�U���HE�ʠ��$|H23�����1�4M���`Ε��̘�	�t���r��)���:3����G��.<�U6�A��?�喟�n���׎=�3Ɲz*N7����; ;�6�dS����L�;��`:&��>�<6{&͙��<�x~�<��`!�^�Ӗ.�,�Y��N�.�a�[�_�_��^8���q�q���5���q��0�;�O������o|����cO��g>c��Y�qF��e�\t\u�҃sQ�r����E%��+/XV2�a�@| gD�̇�S�%����$g&���`�Z#�L���Y�kU���Ģ��e��kf���)���)g=���}%r�h�+�E�ْ(����Fc7�`&���UG D�:�@^g�����v�ߵ�ǜx����q?��??{��8�������}��/���_ߏ ��vۡ{�(���c���	9�1C�>�q��G�䱧���SN��1c�s�Iv�����ѣ�s�oo[����k�}Y�^�����   IDAT�XӏQC�L��S�p��O��G��]�Y#b���Hr��%L�4�E7^E�Tp��,�#㭷����/�U�Ys]U�r�j�!D�M�"�����h�:��j0(9ypJh��w z5�yC�\�g�Y�k_�c�9�N?��]Ɵ{�E��?�a~`����=��s�9���_��}�@�
��Oz�E��sN555�e�/a�/|[m�	���0���V���&+��O��N���;��X"E��� �F��,�1#g��1Ow����^	�U�E3FӊN]��S�`*^������۠իQ5�3���Hv��˪0d�����dfe�e�3�ܫ*͌}�@�e\V�33�ˊ
�K��y�o�q� k2��5Q�b%�+�X����>���럡s�#7�}��6=`�M6:|�����G�%B��L��i\|�cnH��Й������@>�-'iƱ9��͌z����9���*>�a��d�,Q��D�J98KW,c�`?`&&R%���/V��A�S6��d����H���K�$���rhId*��,33�%Ԭ�Ja���X+"[^b���E�2M��\sM?y���$*V*��$j���ʠY�#��0tt��MAB+��|�ڭ湋!�8`@��c���L�߃�N�#�̬>f�ˌ2��T"���A ���p�Jאˠ�d$bMKɨ4�`� O��+�Y3�JM����I�
��ro��A���X�ո����
#5Nf�u��5S��W���b�G_�����`�����x�5�5�@ԸJ%����?�M ��0�	55�[�oc���BfV�h�T<2�^�Dٌ����"�d��_4�$k�*��2EO,/�[�^��8��4)�)73Xɒc��e�E���g1/�G�LO:Js�,%,�R[�2��J��τ��_rUυ�73�!����=�8�{�jQxӁ=��g̟hr��O���@�dVi��!"��;.6�VO���iFG��1S�-)���g0��G�>�7��T��q�J�Sb�$Ոg��L����ZU�1�{�L̌n�@�aN !s��"׃���3ZH����	2e ��pl��"��k�?>RR7�ʼ5wQ�����J��%q��r�ޅ6��B���fܲ������+Q&�d��W"U� u�$���xe�����Tؠ�����x���Fb�F�3#��� P���Z�Q�JJ����d�LIOҤ���Oj4�Y1&��,�O�A/�q��;N ���}.ǁ�/�r�Y����`f`�dN0�	UW֦J�L1fm5�����7�˲l�:��+�K��a��
3�L]6�B@��Y9�J���N�@n��KT�i{|���P3��`e�^N������64R2�D�2.c�dh�B#�܏%�wDJU��&W\�Ǳ�+����9Q'��^{��03��@'ɦ=I�HH�k���<�K
m�Gv�Q=��֖U�\B��
n�2T���3�L�I���h����ǌ2	�q��SL�'M�Q�NT<:-�.5L�����X����P�"y*�!_J�q۫[ȼ�~��o��'�dM4�33eYMs޸e��L��Cg�esv���$��C��F����~[�9�cOP3�wPf�+����@Tĥ��w�G�� ��65w�;VDZ��2�pB�%m��r��$-��iwڡ9�A\6�#s-D'�פ����E�ȉ^e�]12h03�_�c2�0#'��"(�&٤��'B��q�h�6���
�T7�0*|X	�[Kf����&Ǩ�)��H:�b����%R��S��Q\�w�nOq۩c�#�F�Xp�	��(5Jq>$l�� :�C�� LV)7� ���F��.ӯܚE�`Ц��d\3r��p�j������B�2H;�P_��E�U�t|8�5'𢁑U'�l�P�k?
+��d�Ît�agTS�t�F�mTH��6�{�oz)Ōyٸ�dH�?�H*�(�,с��j%ZU�T���Hߒ��'݌\Tv�`eH��T+]����\�/�Y#e��Q"Z茷X,���s�Gɪ� ��g}����X�ʊՋh!��`��\��'b1��% �rd����sJ[E�CFUZ�R;$�����f���s,v�D�*�JT�JDYf�X�u�,ء��0����~1q�`bUT�������o���Z�2�b���>Sn�Q��A3�EQ��^�G�폠h{�3�IP��)0t"Jk�F;��K���-�C6���h�qo�}T23���J$�$dD�R�	Y��qT�X�Di��V	�����B4Kfg0�RwN��ʒ*IN���ve���G��|Ze͜���!��Y��JJc4V������?��Ӓ����W��Al������G������Z[o&Z�b��&O���[�jY��3388�"T�"����t�H�͛��ܹswV9۩H��)�v��9���I��{e��2�~g����aH�;!��X�]�m0�¥�B���	$E�W[�r�F�Zef0Kȍ��f�_3m��+���jㅦY|�H �v��Y&��UgʖCj$Z�Yu��qƙ��{�>��,��%	X�q�u��]���cI�R���_�>����ԫ�^~	�y�;_�u�U�\_���n�%�󗿈���o�?M�?��ů������9m�%�y��g��d�P�C_B�Ś�&)����X�d	��£��P(4L(���������t��GEE��(�MC�0��P��(�J`��y��(O�b�H'&h��N,p56����Xe�)SMJ\����xF�e�X뤾�j�3�
��	ͯ�z�J#3���PD��8�13Kہ�����J�2��:�m����3;qو���h���.��t5k+�G����<mڴ�o���-O?���'�1�閛㫮���.� g�}6N?�t�yƙ�1}�� 4�G�����g��-7ߊ����\s���*\q����Kp�b��������g���Y��O���+�������'�S?k֬����l�*��Ə?�\��V;ӌ�S�H�9��&ȢD433�Y#�����d�
,�x!�Q�#Y�Dl�?�kF)%P���,97 6��*�%�	��7,XHZ���",������!�ŴEvh2�)�(�x�^���D2rc��̠�.��	�2Yc��3��ѽ��854�[��2�5��Te�j�uu���1�}u��_��"k��E5k��+��������_����#����ė_����.�x�?�t���9����좋q-����;n�w�◸��{����,��cWϚ�i�p�B���Ly�-L{k
�{�����x�����������?�z�!�v�m�^z	�?����/�����rk���Ͻ;����.; �
n� `��;���YG3��ٿ�v��%K�NZ�x�k?�t��	���u���m�X�
��$�q���e}I ̕YbYS��w��%W�6J¤F
���=�Ĕ` b�#����0}�t|0���X�9s&�Λ�ŋk��~J>p"�(�՗�$�nV�s�gMT��T6�`�:��HY�d�뱴�n��X(�bqɶ��@��]����L%HTL����ebgf,UQ�?B�:Mf�]Zl�X�H'_��7�kZ�:}��������k�~�Ǘ^|����^v�e����  ���;��_�
�����c�a�+�"�3�2ۨ[7lկ?F�����q #5M��G��*�|}�0�k��W���_�w����K���Ǯ�|�o�>�v�Y|���ϓ�����o�W��
�/��;���[o�ش��\V�:���w�Ƥ�P���K/y��;�􇆥K�n�β��b��0\����	�DM�8�E�,��KmK���1&kW+s��E��H� ��s�Vٰ�I�ĭ$�R���h�"]�pDr=v�={6�c)f�/Z�=�z ��IC2�df"�*u����*0Kd�
/IE0�c���@�|JI��aB���{��������\l�5�#�t����##���5J�l�Ȳ�`PWf���K;�ǟ|"���.��; �~���˟��W�{Kf�� �gD%j.   IDAT�>����u��[���7� G�Ǐ���|$�l�%���ObX�^�q��\y�\��n��w5'~}4N���1f�=0�_���|��N�o_�z�~�����c�������N���пGw������}�ƕW\�;��_y���R{v��`]e,�	�;��"���$��N$��P����c}�![pƅ��"s���F���F�E��'�1�yR�%����&P.�3�2�ʶ�WA�)�1f��d�*�jdA5��%�h�hb���|ٗ��-Z�]t�MfF�&�f�:��LeAJK�iǒ'�7SN���`��|43(�9,�Q> 5�6uQ$[x�23�I�ho�?�,%��f��R�7��P����f)k%�ʌ��~H�?
�U�i�e�-�����3�N�����K/��A�%K�y�^�u�5�Æ�;o��6�F��)[n�S��? �Q8f�f8� ��Fb������~z�`h������+�r�G�Ð�0�g/����z�A��0h�Xg�!�x�u���㋟����8�k�q�~��G��q�c����egl�q��]�v�m���͟�ND'��N0��b
�.9�!/�����D��;Jq����F\ ���͌�$�xW�LJd���pN��JO׼�̬�e�qK7摃�1��b̞X�1�HrK�Չ�d#�f�]�z.�PS�����K�;�-�,���k�Ĺ#���T�u!�Y"[���U�1#��^ԙ�$�%���v�SfQ.B���1s��cЯ_?�_j���D$C�yEl��� �^���y�c��4�e*�8Q��'lS��D���J��X�PIj_)%��%�2r��.�2�̼E���,�1u�?��f����5%l7p  (��tS�;j.9
?�t�����o���5�`���K�=z�[�;`5(�
�E���a`}o�\��C�(��_M�\{l4xM�����b��cX]��X\[Z@T2����[�|������q�p��c�#0��w�����<y%{��)��3X��;wa�]��5��*�/3k��>#��f�6�˔���2����2�&fʓ�� @rI�vZ�i�:�J�o���j.9�}�N�[��8x0�/�b�ֱ`�>��΀s�+���6ˆ�r�f��,�He.f��u���I�(Jd3򴎍Q& ^����?��(�r�3k.z�A� H�~d^s�5�#����gľ�sQ�@I-,�H/ΉS��0�zq�c3����<Q�r/Wg^A�8�GJ��23���`�*�\��o���>y������o�GD�a<G�w�?1���>��;�r�R]��R�@K֘`.P�J �9����R;o��|K|y����ZC�١kc�#F�]w�gGl���\b�y�t��<��b�>B����R�
��h�ˠol���8�#��λ�W�x��W�������}��h�9�]8wg�#Ϝ>������S(�!�f09!��s�����ɜ`��(8�	f�|0%���B���K�D]� ��Ջ�Mˉ6�����:�f��~��Tecf\�ݺ�`�f#0������/��*�����4?�="W�95N���  ��K�uTEԛʆ���H��x��E�~��
^y�e\}�5��/�E��0�?����@Ӕ^؇�����t��aƙxY��j�'�{R"6�N�(�q��[J�c_f	��1k���M��Tg���"C�)�=�����J�ʒ��Gp��y{
-�ٌ���@��n�R�xP�S��.�����S�D0o��Q�j� ���w���W��\�o���������֠A���I	҆��(�#����F06�ؐ��y|��!k#��^}�b���]}]�.Y��pE�am=���Γg̘qX]m�D�K�����PGd�ï��l���/@,Kpb��/#-T�A��,�2C���s�h���o���%^,�]�'��О_�C�E�ҥx����/��
�̟�B�7�֐Qd�r�PY�Qgf�����ׄ��/�\u-�YRof ́QG-��PgΜ~p�G��w�
������'�³��������#��n�~=z�`[�]�Ơ���~��3�*?̌6�U�cl�D�V\b�5�5f9���!�5��]f3+�O��ܔ̌���~�r9��9DQ4�$-����xo�/�d}Dtzqm�,�E��Z����:�̊�u쳈(��(�r _���"7` j�A���#Ǘv4rz��C>�l�ۗ�Ѯ_�z<O��sCւ�F[k�5�EZg(���!�xCDܽG���'�D����Gl�h�u�1ֻ`@��\X��k���!�����h�;�݅>�[�t�$.��R�3��Lh��jei�LU�*@*7!\Z�	��u\�t����J%-.�8�^��x�!�&�֢"-Lq3ֳ3c�bI�$��3�	���O�G����.�Zk�HfϚ�g�z���?������w�`�ܹ��"�w�l#����E)��r�r9��(sQ.B$N�=�Yw����ys��{�����>�~�����Ǐ����`,�:�,�����#���y&z�\t���ǑG��?�ϠcƺQ$x��8�T�eZQ�]��V�v�Q9N��#�M9�����O<#j�1/3�j���ˌ!�Yိ�¯�Ⳟ��s=o!�̝������(�\ƣ#h�>�Y�w�2j�����/�鋈?�yğ����a��,�3$QD��$xk�6���CGl�9�#@�ƺC��� �_.�5陡O_����E�Dȵy1�_���Y��J������v��N2waw�I���V���Ԛ\�i��ڂ����2�-r��R3�%��%�4'��\�q!fd��h#.����d�'���H�D��$ U�8깳Z���#�8^p��jk�����^��׫�����_���&�o���x���:�9{4�1/q�:&��з=�ӦM�o������a	����p�wફ�����1v�X�p�	�>iܩ���/�/~q7�x�	��`CWBw~0�o	�5r0n���`�����GZS,�4>_[�+�t�9�ε�U
�#�I�,1��5W�*�'��GKƬ����ԛ��*�\2�zc��Br���P���G�S/�>G�HQhX��3���P��T?:�m�j8 �����O}
`���F��Y���B�G����q����� �=z�1�E�ǣ���a��j �g�氊q�_���5��D>7�zS��)�N2��s/�ӧ�<���_g�e��k�T��A�5'�^�+Lz�h�E�<y8]h!�xTk3C.��u�sĲk3.9%�2c	$cyyI@��%[��Iw��޸�;���n������ުF�#�%\l3?���^}���g����O:���	8�`��1'��h�8�Hz�8���I�����1G��N�3�8]x���Z����_��<�̳��������B;�n��K��Om����o��g��;�=� .��Rl�m	.EowpyY�Vp�Y=qG<U��N$f���1����
	M)�W��
Qj�251�t��V�:y�XU���+��ʸ]6�9Gʳ.��x?�~�\g������!�ux��� �{�]D����#ϗm~�4�H�H�6x�=��ڽ�*��K��/�=Gzx�i��8~�M��A�i��q�P��+�1���)�����y���v�K��M����Cw�E��m�#�sy�y�ԊQ��f�����$�k�Y���`�A�& ��L*ff��d�
���8��-�GP	aࠁ8�@����'?��ml��V�ϝ�|g�������0�g�O=9/<�<^y�eL�2�?� ��q�D�z�H���6D��h�����:�`뭷���G���Ï/�w�y;���{��̏;�{�<�?�����@g�����[LT�Uf�@��L�`�3�*Ϊ���E�o�#Z�uk�)+[YYb�3�J���L#p0a��w��Y���(be.!Wu�L   IDAT(¦�^y�K/����k�K�� @z���/#~��_"	�E���Ҏ�Y��$��w�)��	�3f <�.ϱk�\(0�򇃻/F���tD�lp�Np�t�i|�)����c5w̺����Yc�J��s�����15m��{Yj�����^6iі� S.�{4֛�ծ�����e3��L��f��e
f��d�$�\!��a=����9�\����^��=�܋/�r��Î1r$�[o=6m�16�t�c��d�di2r���v�~
?��E�馛pǝw�w���~;���J�v�8��oc�����ц�MtV��g��a��y�٧x5Q� P���DD0��YV�T�ZMRrM*/�q��kY����j\�j��䊖�j�ԇ�+x�G�,�*�]�ϑ�,k�b%�s��2bY��<��3�6>�8��4a��1	�Xzrɴ�s��yDJ���Ks�S��Y2c%EO*F���5;�:���{��`�XL���RWf0��j]��$%>|�Pf2Q�O'eq?T*� ���l�a�p��q��8f���`V!)�L̩"y1�#�f����0�<�͌�AW�]u�s�V�k�=����8���p�y���;x�|�]w�;�ĝ<���k�M��l��#�K��~s��C�ۮ�b�]w�v��6�dSZc��Y�!�.�����029�(��u���jJ�U�c��<��e����GqM�41�4J[,�V��>Ψ�M��*%E靔���$��-X��qN*(�I8��`rB�EӤϘU"����>en�y�� q\�19�܅�[`�#�G9��`�c��Qj#��,���e�_x���%�X,���3$݃�0�5�9s�n��? �����2���P%'"$��Դ]��Q�sY/�ډ�ƮJ��� >rf�H,e�l��z1'�S�L(H�%�n����ꌬ:ɗ�˴�b!{��f&��dH�QE�X&im� �%�*O��ۧ/�\k6Xl6|3�G`��F`�7B�P�b���Q�K�wF5�v���DqZs��&V;��dq�؀b��q�ر,{R�g�����/��i#Ҝ�����8[�h��b�׵XN���V�C�&D�d꾹5���#f����'A���
U�%�$m�e�Q|H��c�1�2�����ǜ���X�@yLH��奬�Tk�;!��)�2-t\u\�?���9�Uh(�A�G�A�� �e�.ŵ����%�6���yj�y���]�\�xySQN���?�8��)r�2W�d-�i��8�q�2���~�Q��,��gѓƕ�|A�;��C�N��T��-�\S�j$.��)0�1�K(r7U*P�E̅�R$;-�\ ��B���B*�2-��h̦���d�,�=`�ƠÔ�D�I�mc�8��2�L�tP�Q�Z�97�c��QsPc&"KTt�8�Qa|�,G)y�p%K�1IL�b��۲N���J��q�S(�fU�*k�,αb���!)&!#���j�����9Iֽg�t>.���)���0�Ϟ={����b=0��|�7/+t�c�-�BD*�
-_|0�P��ej�Z�衫�)Q�*T�(B�U�\$9�m��,�W_0���A ��-��b�	��BY�����|0�И.S`�'1�H2���C?�J��Ke��5?sҲ�����������E�HjM�����̐]f�u��۲ ������b���'���E���6�zU�F)��V�*ⲥjCɢ���o��f,��rB�L"4��k���/1��(�^H2ٲk�q>k 8��rD �E !��l��G�8"�z�dr��f;�*e'��@$Q��	�I�7
�/f]̾Y��S��g�	� %;����V������Q@v�#�:�H5j�U��hf0����y�,�QU9��!�]t�^�ѫg/���8�,b�����<��Eɇ5Ny��ޒt"����ˉcg�Q�U%iDTU1�fs���c	��ci\�|�*�o%��1�I� �Y��RQ�p�N���!�ڌIrB��4�>�O6���_�e�'2�9-��[{O�L�q�2���価�eU�*3�Y���Z��e������$%�b�LSN�"�E��'�	Ԡ�N�U6���I{ɰDf.�B����٘~Pj�ܞ�0��%Q�}��M%۲��E�'��+�=�9��{g��8���GpW�on�����=U�F�Mv�j�:����8�r��)+	j���`��U03�Yj"n^6�(k�l^/�>|8��/�]ćX�55��H���(��+��#���Û=�i�;M3c��b�k�2���HrV�*���)���c���Ǚ/��2*�L�jd���Z
3�Yc���:�L`fN^H��c�I��T⸭S%��ذ����QjF�ǠY�df�t-)�_��,���Y��.#�fTb�E1�H��f.�0����2c"��9�E �	\o�JD�$DI	��W���){ǅHc��W9#5�\h�m�9b}�N@��Խ�,��N�}G�²���ihh������o��eA�,��r��z�.%�F&�o�Xv��҃���I��XFB7>�|8��p����Fm�5�ô"
|Hs�5�1�v�\I?�A'ɇ�%�G�N*��, IN/� ���  uNH.3)��29���w��D�8*��dA�%�.#q(&8i\����D@!$&/�ՋC����f�K�XӠDY~6�Č�D0���ZH��GRѽ�]2^�"�'Q���U�4H�Y��S�23s�d��+�D�#�(�u��R�A9��=��dUI��I�2�?3���*わ�7'p�3x�X���2��� ]__?��}t��>��HooZj��"�,�����0%�Jꩀ� �uŬ�C�����ԧH9�@w������k������Oo�il��������#�`�������jE�:@�"���u_]�9�E%�e��-6�x�6�T�sfe��pu�b�h�J��ƙ�1'���WH��X�)���`ּjR}̅�Y��yV�sꚌ��)�-P�	 rmr��)��p|��jǯ�"`V�_2%�O�iC��{(虦$�� ́�M���`H/6L�D�
&�-$��M<K�JsָEj�rAm� �#�|���I�g����2v_�'���y�hힹ�䇂�}jr�t�I~��3+�>�:�m��&!��DD�Bb���H�Բ$��d!��Q�)_��=t(��w�v�i8�S0椓pҘ1��߀~9DQ��,i���3��{*�6���ۨ�V��<�)R���iuK�Cޤ��(�H x��<"�YZm0Ji�R�R��DRg\2�C�,���>�?q���lJ����̝H��զc�*�T+��f��d#ζ^&W��)��c�I�(����"t�����;4���i�D��\/��SO����K�D����7Ϸ�U>�e���q�N�<���,���%���iYRӌ2=�3�HfAz���ޙ��H.V�9��N��MR�@�M�g嬝k��L:�����w�_�җ��&���7E,5�-Ɍ�x���[Y�*ɕ�P��������Ъ\��$w2�Z3���Y��Ef�lF.b}���=#��-�$&7&��r�T��Z����g�
�ܱ���ڍr��!�^�� p^�"�թ�C�2�5����23cK�+�"}b�D'���2��?Q�cL�K�;�瑴�q�T�&.��GZ��������T �9��H�NW-Y�I�>6���II�UnLik�L�@po��zt�S4w�}u����gƛ���,�����V���j�*uk��j���>q����*��)��sĒ�KP[�K�.%h7 O�L�� �H��%Y\dIf�?�,"k5U��Q�"5IҚѢKJ�γ!œ�$U�4����w�Q3}�J���`f Dh|�!jļ?	,/7U�o�YQ�}x��b���D�O�B�	`L��`$d���nFRRj��lO/��ԍ�&1;&vUj� [\ ��*{#fl��\ɔ9QrRN9���+���H����\�%��2ɤPER���W�j����:��/��fF���t���2��7��o��9g�d�����č*���h   IDATE��UMk�����ī�boe��`V�r�"�|�������<U%����]��*��|D�!"`i��eH���Ʋ���h�Ȩc�H�$3�MJ�1Ker���g556�\�0����  3��K}����(���"�33窆fFB�K}��L"*I$[�`�?
�d�H�.N����iu�h�@23�r!�+�2u��X�����p������+4���F�L���)��c8�2��Ŭ������^.�I�g�Pb-����&��r�/Ob�4��<kC7��xjҡYԡ�_�u#���,�I3Q�͖[cH�e���ԃ��L��2�r=T���m��zd��d�H���^fY-`V%�K�z�MF�?�G�2p��M�afĉ
��t2����L�e��I���	����ɐ�{�YO�'3���"K�s��V��������PY��������],U��[���~Ud��ڼ��fd�	#y�X{e� ք����p҉�L�l�,�F -r �q�s�I�ud"�۰���7j:v�� ����
�2�mef�r��h��3)��7�PK��h�R��d��X��+��i`\F�vҫ,r�2��ƛ������n���WTeI]�03��X4��y3q)Კq'�������K�!S�D�'%��JNU���� d_&2@�e��(����L����h�ʥ�K���I*�p?��U�Xb��I���R2fNF��4�7,����a/uC�8�0�70�$�[06>O/Le�hj�Z��7D��󊑊���#ٟw��v��Q��(k�"�m�>i�R�&�R�`|`D�ɔ�*&d�+tɬ)5i��DU����J���E�״^��+33e����`'L�q���S��.r3 ���W�m�Tb��L�L�H�CD���	
���E�lD�N �_/3vJ�I��ҭgyѳ�`�~h"3��%���.�둓@;�"2.9��II��hjI�)K
@RLr�H,���CV��k�*K��h�crm�]]m/E%F��z�nGQThdƛ��I�N�Q��e�T�H����[�iS��j��s�^RB̙��jYu7��eu���eif0kN-v�����L��rr�P��e�ѼΨ2�%" �9J�7�K�E�(�[g�%ȅB����z,^���/�'� �zr�d�%f�G�$�DJ-&�m����O������'�"�ȓ��P&ڲҌ"��k�!�F�M�"�GBN<��F���1��ɺKM��U�+{��^�/��H�Y�L��>�Mʢ��v�̖T7�=��Tm�+��6{]�P���׵��GŬ]ن�LJ�2�Hh|��H�R޸�����NI��˸t$�C:ʕ����Jdi�'��Q���3jf�	���ɕ�;�7j�mSI��Ǆ�*&�2ɛtըhf03D�YsJt�(B.���/��?��p�B,X���Y�ϛ��s�a���]T�%������Ǥ%�A�K^���gN��Kn�hب3��ʄ�b.E��6�V�7_��l��!�S*h�"9�a����r�ϸ�c�<69��#�t��^�"��ry�X2��:ub�����~C��A���$b���9��E)�;t�:���q���f���|u�a��)*��f/����׌KJ揎�BI6"����(�2Ք|Ͱ�DsO���X�ɐ�r��
cAD�$Q[nd0K�Bb�rYN4��(�*�*�Kj��J�I3�N����;37S�f���n�����K���f��/+�䭴���2�R��ifĕ�"�)�"��W�KXL ��вx����*��:�����F���>2n� �a��J|QZ"�Ti��msMUJ�o$�P"/1�%�1��(�pb�|����W�@�"�A9��UO2�I�)X�!�2�� �3t%y���q��q�����Z��Y�V�����oOU�N�f���������(���&ʌ�f�+\7��TSU�YΈ�'�"�B�Y�%�V$�H[��IRuU�I}���2Q���*EJUIces��\� 3�4%��6^��%�ed�	��ԙ�H�
�ef\��Av�� %|b����8jL_b�S�C�u��X�2�hL�.233��"���cR}C=1�@,0��F��s@�d�/:P�C`�:�C�e�ي7#7�qz�͓�5V���1���څ(�(��Pӭ��)�j�[��#���D.9��h ; �c��5s��=a��3"H3`���:����BitYD扲7a�"ԇ��%�ӂ�����2v�&��A���Q�?�4,���x���
��yw��Y�43���>���DD�%EY����@���R�?��R�O[���72����K*���jA�>��2���R����hv�^Ԭb
3cw���("/KW!xyF�8�I�4&�h���1Q���T��d���݈��>}��w�<gn����0�ЧwoDlӇc:���vr�﹤���9kyk�&%�7"Z�\R=�Dp`f�����t[���|M�{t�_��/0�w��x���U�!C���~���%�vE���%���2�%Sj( �9/���@��6��`{���K@�Eʰ�K��:���a���%��4��&��q��̸�Ap203RD2��Y'�^��0Ijx�¹;{Eˢ��v�_�~���y�Eg��[��xcyW�Ր2xe29k2����H�*'3�YBee-`e}EJT����Q�q�rX�$/./�?Yˊ)���潪��s$�9g�όR� %�TՈi'�330��I���dFƶ"�F)�	 c��bL@��]Tg�BU��U��\MҪ,^�:�r�0���Fa�OmK�*`��S��?�/��
�59�  r3@��������� W�V���Mr)�1�QJ)��w��guz���G�t��)�}���w��M��$�?��sf͚�u���m��$ėL=7�W"��_s�㻏�
�w� �n�1��ۀq��
vB
��9{� &^ETA$��D�L�����P]Jf^����r��z�dL�hg,$s+<P__����c޼y_������� ��УG��s���2%Y��]���Ė8�1�IN��T=��� Χ��v�n%�R3��Y#y�ag|�*�^Zq�v{/4�2��C�͔Xы��1�e]�R���f��,+QNĘ}	 �o�M˹�D���0�qb��2����DTT%iT��DIɜT.���o����hl@^��/��?��O"P����˘�`>�`����R s�uh��'��$�P��̱$kܘ (nfޯv�z��������xΟ"�C��ޛ��w�yƟs.Ɵ7����x���ѯ|c����|�w���TJ�Ә����O�9��c�aLP���,�YB�{ڋ�������p��8�+�������7�7�	ҬX/��E��T��,�J��C�	��`�v�,؁��u�Vk�V�s:��üx��eݸ��ޗ�[R�g~_�[�i�nhp�#`6�=�&AQQ�7cg�ND$��A�����'⚨h\ �3�H5�Č['�]Az�~˭����S���_��MCW���z�U��u�{/!����&��������<X�us4�t6�h@5�pT�3��q��U���*Ϭ�7��<]go�mdO'/%lfZp�8�I�w�0������m��]��m��ݮ]�n�y$�q�c5�گ&�z��Q�4	dHi-�NKB[�6;;�_��_��x�y�{�����o���o�������������_�g|�{��v��zzn�5�cQ�u�c$5�>��P�����ؾ7�tS<���׾�����Õ�8�~�e�����W��~��p�o�{��^\�����q�I'��I8�q���pG%����5�T/"�����J�8���a��:%Ć�q�"��"i߀zQ��VXˬi��y_Jv�2`��'^��YХ\�$
�E�W@�Jf���םޅ\�{n�z'�͛����ӳf͚�&'&6B'>|�M[��m�}ֆ6��eq�F��g �h�m�O�2��C��j註�%)T(�v�Yʴ���b   IDAT����9h�����+�
kS��~���g����	jN;J�q��;vD"۱};��vH�'�1�z|�;���-cU�	�l��`MM�cl]�0��ug��7������3O;�|<�a��۶���o��?|���#YR	�3����������D�޵{W$G'�9}ȸs�lݺ%��~�}|�[��W��U|�_�g?�Y\����W~�����/Ǜ��f\r���.��^w.��b��o����6\�����| ��ԧ��o|#vؿt������3��L<��q�{�eQ�T*�j�ym^r�Čڠ�w�=Q�I�I�Ћ��w�cg]'i�܏v�H׌:�U�Hp�`2 �����9�Ĭ$�L,��� �Bj�3����uy��OR�6�����;?w��͏�|~��+r�]������M�$i�>O��<�С9�h�(G��  ��И�9I���aH=��ȶ��x5iJ2�h�B�nk3�eaߨ��F��n<�$���흳��n,�9��F~6:���G��P�*� �B0dN:*�y߬��a���n(wY�ᪧu�s�~��x������;�#p�'bժU�p�H��K�^I�S�i|�Ϯ�W|(��ޯD��w�o���ַ�ozӥ���K#پ��oP�_t������׾��"�.ƛ�s�e�������?�p$����;����ߜ������x�S�ó4�g>�x��ϸ��n�eV�UJ�:�ZF,-�$$�u%�
9UJf��:�w��1Wz�ς��3��� ����gݛ�0R�Io9�Q��z.���έ&�@��E�}��(�3H50 
�����	IM��Ź���w����qVϨ��<�z����J�l���F�N�Ζ�_*] }�\�l7\����BFK)V t�2��O����P]����!M �I�"	�yR�`+;��S;��c�=�����|�[�]����͓��x2FIP7d�D���\0�IQ�8@5�A3Q��gx^�=NLNb�����_�����=-v�y�C��?��8����t���/��
=~x5^��.�3���W��J�)A�)����>|�c�s�O�s��_���q�oT�*�>���������SN�C��������?O9�<<C���>^���i����Ν�t爱w��L�U+L0 �ԱDs(�/&�L;��D�Xx'p�4d�i��=]�u{���Hב����JL<1�ā�:�Cz��gLEY�1�u�D�d�T�T�V� ���t�6~F�k����[x�[dx'�,���N�U���7���/(_6F��7�u�7��yI>.Tw��G��*�ۺ~�c��A��F���.V �>�`Ѫ6d�����Ǥe�j�8�[���z>��M�I����iP��e9����7����t�U�h	�&�a#	1�Cl�����>�>(A~� օ���� �E=�٥5L�gO�����>/{����o=�	x�#�nx N:�$�]�s�wc��L��;vm<�f$����)X.�EI��0���/��n��'�/\p�����ſ�{J��/{)�����w~�w�y&6l؀;));~��;A�Z�!q�B.X $!�����	W�y�t����<��Ws�a^׺��s�IH�}��fZ�\*N̕�#Vmz"��d%J%h��J$@��ڼ>S2�F��wq�=��Eu�#�8��c?ZNL4I�'%C�$�
�(ڇd�P�i�E|4�U����5&9�*�$G��j����}ZA��V�[$�����¡R]#���LM�1��	)�fX�L��|#M+A���Ŭ05=�n.M����7�&'q�q�bv�,zz֨���6�o�B7����)�K�ec��	X�
5/$��*lx��c�X���"�nd�5w����G�6m³���浯��^�*<�y�Ó��d<��g����s���/8_��p��ǣTbqb������P�{(��]�^��_�t�{�����_�SO�I'���?3ӳXX\�6%c׮��;��K�H�Q,A���<�Q���K���su$�U4?*%dFF)}����MLe�_=Ir���a'#�2�q_M{ODs�y����z~,Ϡǲ(@�EP�$
���8�ɇ$�$ARK�>���i%�G�R$��[�����6�l�u�s�`�1���*�/��Uq,d��JvÒ�@IB><���R;m�Z�s��G���Y�6���Іzs���H��M�Q�%��g�b�
a%fgf#�9L�3S8�����~�~�,'���N:n�~��}�C��W�q��$��� 	��g���R����;N���_����;w*QnǢ��}�j��/�b�����t�D�ޗ��ex���S��T<���;�j�����9���'&&�������e������M�B�w�$� �ϓ�L2uI��oB��E��(0!�E�t�E���܆ۺ��L5�^�P�w�Т�啊�F$f�<������E�:�+
��-Su���i+P񶍔E(���,޴,4�H�$T% b%#�~d'���+v~nzd�<tuq�:<G����6����u��4�3��Z���t��I!I�Ds��h4:_Y}a���&��W<D]�	_��s�e����d��-�᛭��&vHЍӴ�&�Mk�^I�Fm�y�0t�f$�xk?�GG�8
+W�d}��'�	O�-�_��4����0�w����?�l8�)=?��Q���tb�$��ʚ'��dR��Y!8>
�c"��.��rb0 ba~;�ގm;�+y~a�zYPb�$�����0%)-���A	»��̐��磳�����t�,۹�(�AI�,�̈�(^CQ`Q ��B�5O ��m��Bv��D��"K�X�*-֡
x�ޗÈxƭ8*����
͵,
=���LRn��!�f:�^I��<\����q7�|�Ò�������!��������y\!Z�D�u���FDׇn�PW�$����bG�Ov�I�:Q{ ?հ�c+�Ɔ�-QnYkź�Y�گO<ׄ���k�=k�ʌZ5H�Hڥ枬S~��9��vѓp�>F�=���ǣ�g>�x�c�'�����p	���'cZ�FK���}���(��%'*�eJa������ !k.��PHv�(�'���G��,Q�BQʛB*��{�k�HZ����{��Q��Q�m�s4��"�C2���F�<��D�
Ϲ,��	�B�U.Z	�sr�]>&&A��Sg���@ �gd�@J�`u��χ�m��1C��ui}PP�-��@��M�@��H�d��L<٧��f��I�S�!�2%�����k�[�Yw0��}0�����fժ�?��w�eyv{�q��3�H�n{��uY�o=�Z�Μ���x��yJ����h�a�_�OZ�n���ZX-��h������O�N�i<�\r�>�{)|ڃ���߬/�P�uϦ>,��ư>֢�����j!��EQX.@2G�~A}�����+'a�s��u��b��԰���R:��:PHB�RIs#)�DM=%����P�P&
T:'���X�85�9��@$�B��4�!U�m��n���i�iݱ�y���B�����̂ ��ē�~�U�bd��ר�'�>r(vӊ^3n�(�w�M��l�v��2|�juM|�LP��2�œ�f�f���Cdo�nF��Q��LC�T}�9�pD:B'�M�>���H٫<V�|��A�c�o2�z�!w�ڭg�[�lw+�n٢�ET=xf*ݦI�Hֺ��7�UA,���6�I�Jj
�𶂪�T,�!�4+�A-��b��段(1��I�&���$N19�n����0�m[e�Ԁb\�%	��FD�"A(%�	�p��yqR�J��@��R��vЕ����6ك0� b
�E` Z���A#k�Z�^�b-��Tk�љx�<�G6�u��	~P���u�^~�}�T������v��k��օy�׫�A��n],*�m��E|s@)CW���r.�&�͋��R��E�U�6��   IDAT�y���\Y��}�nm����\U)��C?켤Lčd H�H(L%�gu�4����ON��<pP��@GMĹXj`ŁA�i�5���9ZԪD��^�歄��������a��\���Z��v�{2���|]�g����YR[�Fu]��� �8�o�,���iQ;|��Y����Ryw��\�Y[*^������ �G�J�p�����^�~���PI�RL`ȅ$H�p�:>ѭ���M���h�b��xbE�@��o
������O�r��G���%�nݺ+������nz���J�N���x��V��8%G���ta��Lm�.������� Ͱel,���1�k������+c�3�C��� A�@Mk:��O�H�5�--�������M�~�5vXDS?!V�	V��^�c$[���(���A�
�_�YT�|�e�O ΐ���r'��
џD_<�7k$^�9�'� ���e���D�LR���=�j�a�k6��Ҍiuf^j�+I*5�Tԫj��7pr�d,�q��za�i��������bn�-��$�)����,�i[��l{�s�	U������o>� :Di��}P�I��u<���<}���Imc���=_4�z�x�Ӱ�ShtncdEm��i$�|�&�tm�	���i��5��,��mA�FR�>§�3�[�f P�d�e��$U�.R7���-�̾U�t�1G��&�c�B���2��6�&2'j!�wS'�C�"*��`����4�Ĩ����EZ��Z�&Y�q����&�u�����Tr���S��[�/U$H�k��	���I2�W`�I�����Gt�RWV��b��\�߼^��#�E��(IG�V��4�4_�gِ���k��
��Cj�|�X��S� �}���!�)]�^f�M�������CD]+��/�}�	qn���T�|�mI� �F>bh��xj��R@�CehV�����fXh.Yg��[�_�Vk�&Yz����3jqYD���V���3�5�v��,�cx1*h+��ȉT*��`���	����l���H�� W��4E�m�!�?ΐaDt�=��|OI�R�3��h���f���EL�^��b�)�&4\Y �ҩ���I���E%̦U�Le��.U�V��b����%���	z���m���Bs�)���ސ���j�O���@�1����՛o�|@�3]��	{����"N�CD=[���y\�A}z|�Z�K_����r0�P�"�hv��`�����Ť�PS���/�o]�2|j~��?+�>��k�Rh�G�-?+�"�~9�i�R4����$�jE����_Ĳ.�W�2�5^݁�F/u�!(�:)JQ)�hĿ�����^����h=/�2.�Ek'���\{,A�Q|�!��E��v�s��v���ɏo����pw���¼��"*%GZ�.�����1�P�DR��T�ж$�)ں�"��fD� X���klϣ�n_���V��G=��_IY��4�J�5�*|m�]�oPϊ��Z�� 8 �@���|o���CW}��U���kW_3}���?���Fs]:�*��TB���JJ�ԩ�x�'Ր���X�aE���X�\�7��Q�T��92�=���5�3��W6��5�f���!�PRF8F�5�rX���uh��>�'�%c>{�gc�v��SS�s��I4>�v���Z>
�4A��x��_�q��<�(Ai̴�L/\�KO�ϗq�(��?��������|����]|���WҾ��o��P�/�XX� �D�	�wG-���4�TZR
bI��ЄT� �t=9Դ���|+%�^�E%o�'[O�J��'T�O�;���W�#+2�D��1M3�e�v�𱰰p�O��w�a�#�zŊ�=�؏�C�ӕ�Ϯt�N�Nx#���i3g�+ t��8ř&��lRQ}Rc�,~�AKô��h��K@�z]m۞�h�sZ1W��I�*��
�
{9�d8}�RPm�C��:tg�6�Rj���D��Sl#��=�A�#o@
� ʢ���D�h6��ö" $Zȿ@�>�in $CO��M:Z�J��r���٢��,��U	mۮ9,��⶝Xز��[����ƛ�C��ގ���yP	:�	+���.Vbx��c
�ɢ@�6H�Z<������d]ɿ�
;w�������oj.j=�G��N��8*�C��B�k꿁�M�$A&H�d�G؜�����E��U�=��Ώ=r�vG>��|]V� _�#ƥv�Q�%<�T۪�t��J�AR$AL�
�^_#�S���1��1C�J#�}�o���Q��/�$��ˀ�7���Fۆ�|M�Ub�V��%�߂P�� �T�&1��^*�{M`!�LvR45)^ ��`���P	��,�r�
Ʉ���?���0�({�EbB(�+��Z�����{�n,�-���C$h���I2��i�wցE�.ۼ^�������"��ze�ބ09�ũI,NOaQ�4z�⥫d��!&5���׿�-��W����n���,�:j
Ů�$]Er�%.�R�ɹ!�G��( ��k��J�^0>��_�+�GW@r����9���.unL�Tg4ʆ�%�>��i9�.���G�E�WG*�P�U��3U�ՖR���y�v�w3���~Zs�ٷ���O�^KF�H6m�diO��ڤ���Ljq��I[��r�׆�OJ��j�Op��_��ԑ�J,5X�,JBM���$�I#D�5@�H5B2�@* ��0�dx׻�k�[�M��&v��#e	��1}V�:�����\�v�cA&VN��P�+pz~���w�Ԯ�@$�E���X��9����^�H΋J�B$��i,fЛ�4�R�����9��W��w�c��>�s�q�{�'�t��V ]^��
S �ה�	�-N�|5/-?��4�N� R4|��8�b+hG����g�
}�s��#�{-oŊ�f�6����d:Aq� ; /CP� ��;II���>�$Z�MW���^@F�(�'�s��ۄ0cgo�1�V
�o��b?#U��P�%��Z�t����������X�6����m�"�y�y'J��I蠬@�UM�H�@���"u!Y����F�z�r���Cz�]��������u��׋
?.��j��S��a��,�G�[�Yϣ+=�����{z���?ċ�۲�'�*?��NZ�J�W�J���&@%cjM�+�o^sڬ�}�{����O��k�ś�����k������Nw�3N����s?��z]XԪ ���W�I@%�,�vDy��^қԚ4�ݻw�����|	K����\��kW��&}LMǎ�L'���E�N�� ˪�ZZ���#	��ʵ�RU\�2�:�dH3Z�㩆����S52�t��*�O�Ūx�F��)�C.�EF������"�O2Q�"=�/���,�=b�u��@Z�8-$�����4"/,`^Ij�vq��<�zt�����o�?�5����ضm�v����%�o��j_5bd���y�4��S��U��2d/�d�$��Q@\�?~�=�8�AB�G
��d{eo'>���'��ϕ=|��S 7��v=B�Ӛ{����z�(��w��e�Ţ@�F%ZIW������G�o@�<��v�J�;��r3~��������7������g>�?��O�}���x����ǯ�?ܲw��]���<�x�#��5)Ak�'w.����T��(���(Ц�F�co�lT��z�R?�=|	UW���y��N:��;���ɍgS'2�d�l����mXB-��!3���@Uԣ�����H��:q�I�v�I��07�[4��}�l&	�YD�kTh���u��=���}zg����c��6lۺ۴�KpBޞ�!�vQ�8q�ڵ�����T�8��,������q�=����R��()&��w��|���/~������c�?��]��(���x��.�_��0�O�A���I���s;6��)d)0�~������%8�o�ߍ��މnߊo߼����� _��w�o~7|�k��/}	�7�c�i��O��;?��1{vi   IDAT�}���q9^z������'.|�{p��>������7c�q�����8�s��'��y�{��M �	�X��%v�X���B��>.Y	����xvs��Ũ$V����]Ա�Xf�%�e�q��ڴ��D]N����)��XJ])d�a��Otܜ�8��b=���P?= i��>Sw��l )w��Ҋ�,~��fmxDC]�la�a��4+���f~�z����2-R��e^�\�'5�����I��9=sݾc{�wi��������;k'�J=�����ښj"���>��r�����J��ü�я�e>d5��!s*�.I�	V�4�Hu����796��_�E��g?�����c�	'`�D������v���x��N\�����?�'�������У��n�?�������g��K���?��>�7�Ч�
�������~o��Cx� �~�{�w�ϻ��̷��x˛񜷽/��r�����?q5>z������H/~+fq���d<�i�Oą/�����w��+Z,�G%$�&�c��F)��B����k'}s��O��Y��br��+7o���Q�xM1^�iV��D=3���o%��	M7��:�}�N�/+��t9p�n�\�u#rXSjB��^��ԓ�>�������R�����Fh50�F�y!b�؈υ$Hf1F�����`��mm^f� %�8AT��AdP�,��4eb��ɧ='朤M�@7�lZ��|^����m	F�������O��TE�ۮ��qz���� ozӛ��'��| �~��c��c113�-,�u=O���.����k��y��O��x�%���7$���߈�q饸ୗ��N�����>~%����w}���������������~�ws�{z�J�9�X��w�]�vw�|��`ï�����Q8����5�}-��ַ��/x>��`jJ&j>
1
UԊ�Q�H��tԊ����V�Z�Hq�uԲ]����1N��T��旃.A/'J��1/=��:Cӹ$c���D:���hUnc�*��CmKH��@�'�:H������{ƒJf�=3X��e��h�8{��Js�0���E���7n�ͺ�X$133�U�V�_��oz�
%�)Q����$��z[�}�1�nAπ#)+AW����s�.�/M�B��I(E��j�����V֑zq��K�v�Q�I'���>�Y��/��]��V�>���^��'�)��Wڔ�������_�m��n݌ߺ�پ��r3n�;��J�
��]��|4��ʣV�vw��v�{�>J�|����?��Y����]��+~oU"~�{߃���x�o���t<����uǭ���<v�����,
QD�$E=B�̉i����\�R��6�m��2��?J�?�eT�2|:��?�N�i����:�OK����)6�B��3� ��F�;}�-S�u��$q	H��`*k	�Z�B������7n�j��W������ú0Rl�(�{�����4��'j=�R"�o�Xc@��"	�E�=a�d����?*������%O�K	v����L]�>ka,�mM����q4P�s�nlӮ��cV��u���/Ļ��.|�C������x6�iS|��a�q��
NӇ���~:N{������/����0�	'�����%�w����?�
����a=w~��ߋK.y���g㱏}��>w��=�K��Ν���غu���$Ɉu����L���Ҳ��,���D ��ăVf��y�\����F`͚U�/�����655��{��{��l 	������I�T�a��3����b�nUb0� (�!��@:��H����F^�"#���I1.� ����>�h�d�z�j������)�-;58���I��=�M/Αļ�&is�h��'''�'��P�K�43��՟�A͗,P��>x�E�ޢ���v�w���pƯ�^�g�z��я|��O�'� ��������^�xo��v@���L3��X��x��g��.p�*P����� Љx��-��wi7�,7�|� �F`m@v�#v+dɀe��I��Il	�~�G��<���ɞ�L��,����\q֬Ys�wճ+fO-��,��Fϔ'������,j��V���V�-�{nCېd�m��I�&��6<��P��Z�4�=���X�]��iR���F�c��F��V�?PϹ��.Q%���q�QG���Gc���UGavvV��I�"'p�1���'����(�K�%|�^	���u��o�Io�0<�a][��*(��	���e3�<|�c!7����nۡ��V�mz̰�z,R-,`Q�G�,��&��Z����¼|vi�>77'`�~�,�B 
^�am�����e@��H��J\Þ���������{u�[$z��Y�ӀU�V��[�Mdq�'�o:���(�v4k��q�l�_������J���l͐�h��6{�첈���s-V��o�Rr%?ٽ� ��6C.ÅR"M�l�B�J�Q�Ӷd�(���&��r�J���>F	��S�p�r�yx����Ůݻ��P/.��fݱx�K^���=th	�:$�e �_m9�UݲOR�V��'�ƒ�Xא&�PH-
��;����Ή�d�rE��:�(K��eaP4�eI�E����&jK$C\~��'��fi&���Fz��-%K:��M��U�Ξ���g��Sӹ��k��(��tTC�Eȯ����\
�Z]���=�Hl2�Gt&&S��D��iN
R�#� 7��!oI.�\��H�j�HU��襨��#C��S�V�A 	� �T �� IG�"e�j'=��}"^�W�o|����7�h��%/���~l�Ͽ��+c>��d�&I�X�ၵ'r��Pͨu�%����/�x�a^�$ �GH6���E�NQ�����(' �0
UJ^ZcQ��>HO�ds�" K�x����1_�O�����Ư�ՙ��$�E���ָ0�ZRt|�4v��/�U���[w�?Ԯ�����/����H�uF�fڠ]����WV_��}���V3VT���$�j���2 �dd�qt�a�����څn�Hz���HU������?7z����mӦ��K/����W࿟��q�_�������.I�R2��}*%��t-&�Z��	'	�撸�:����A}�I 
M��ҡQԧ�f�<I�Ȣ"Fm( �U��Yr��6dR^C@� )�H�S+��{�h��#8�{Ö�vQ,ױ�;�"p�1�|ҏ@��s����F�E_��l���9P�����^�u�K�+Q[%�����!+3dy���O@i@T���!�a���P�6�0�.�������m�g���3�W��h;j�h��W���~�\�r�ŗ�e�ֳ�c�����,R��M� �\D �Y�Z����c}M��f�<$2 �m��Q�DUt	���V�uy��O.�[E��(��I����x��C����L{F�A���O�:@�S5���K�UI�?U"M!y��_�(��t	z/�5��d�ڵ���ř���Yo҅pn�B���3�����Z������W���h5Fi��v�Q%�D�����H��n:,�;F4R[�1�]���6 �`�����}�'99TJf�p�ϡ��(*%6wGR}S,���t2$}�#�eذ��0z#
�%���P	��six]c��ɹ�����(U�'���v�*��b$K�i	$ŷ �F�ǲ�o��Î��а � t��.� 	U�b���(�r+����>�P���X�W��A���-%�ӵ���j���ҍ�������_�����t�m�����E	�ԇ��K�2��In�1�lAeZ�i^*�Y�-	9�)���w����d�(BT�Yr�6XS��1Y
:П���a�̔�HMU�)hgLTP5 ����8x���Q�V�k\�C\]di��Լc	^^�R��h䣞���^$�:Ak,뒛��Y'�q8�K�p1�pE�z�TN��BT6����܎�f�XmH����ۅ c�0�-���mئ���z�/]�^n�n�~J���y�wֳ���   IDAT�pQ�z��Y{)�h�ԅ�k0�A/p_r��()!���H��U��F�0�x�F�y���-wr���g���3®�.�Xh��_;�a7�G�%,��U!�*�êAJ�@2P"�!�*�;b�u9>��V5;�ؚ�̖40�"}�Z
Ç�T�MIZ��e�_��KH�Ty�FO~����մ��`	�X�ȇ���OI��lIFd��<мR�>��1hCb���L��m�r�b9N�ϭ?�pяA��zrr�����M����W�o4��F��$HUd�ࢲ��U91ŝ������Hm�3O1$�N�{*��L�����jP+��;�A��im�	��.#����ɰ^��~���ԝz4�1�a��JTE#�o�אT�\�=��PVp��}�!_�I�Yh�AV@2��$e  ��q{�X�ziT��_��Y�>z��aدw�Xm�x��K���Q5)���mIMk}�Q&1�6G��Qd(���u&�}X`�:�5kV]���UN�33ӧNLO�7�Q�n�A�q���Z����HE�6"C�>ƐzI�$��oK� 4��'��׌�d�j*v��m�?�іÚ�zX;(�'hxax���%5��-��xC")�� A�T�<ɽS���i*��L�:%鞮?��۰��˶R�W�s!�?��^W#CՆ��Y��9R
��V�~;�$���%���m��/��&?
Ѯz�p�^���t��"k�:��d�������~�wJ}M�(j�>������>F���3B���������^$է���˱do�G4�)�t�E>�D#���^n�u	�=��=��>�;7���nE�Q0�C&
d��;i2�D¿5�Z�w�㹇��|JкҔ�U�M�j&}j�f�7�Ʋ<�˱1�["� �?O԰�V�5j1�X�8�z��0R�h� ���tm����]�
ȑ,�F���*=�^?91y�Ԥ�Lg��܄��Q�|!���%���PS>��
I�l<���
��7�'A��Ȟ��5�|�}��!`T�e�V�3C-ɾ��3�,c�3���}<�Ԉ$�QH	$�� ����cg>[��lО��s8I��C�h9���\xV�T�cH���dV8�RV�f�hZ���V�^pL�$���q��rt	z_�u��y�uz�v�3�3�*Y��w�Y���q+���w�ʾ��v��nH]֮�����8��}�>��S�C�T��d\�0��
f��e�� �z�_ ��u��Ԭ��_���S+T�d�opҨ۪�$ڈ���k�$��FQ�	�wjjU|���$�_S�W����79������bx���=�#���*�Gz�@���>%����!���1|x�Fg�W�Z�k̃���V�ʢ�4Q�֬Z��;g�GQӎt�c�(Ļk?
�߱�c�ϏB�*����渞}�g�N�H�m���C_W-��)��&���Ý�.�Aٟ�����R�EK+%៤#��$A
�]��L�'�1�O�\�U��yJ�;�Ծ�hoq&B^s�[����k��ݻ�c�Nl߾C؎�/����k����V�l���E�u"���κ��e%�t_�q�܆d��h�e�q�9�$yZ�a�y��}��!v�W��(��%��#��fw�n��_̧�� �d��u+ �J����2�Y�:�~LM[ڥY��#���͸�a(1�42�E�1y=m��/��x%f`��$�c+U�هT�0��:tظ��7��ꁉ�5W����9�)n۶[�nl۶M	z�g@������>y�\�MO�+��S��7�=W)��ѕ⅊5i�|����%��Ya(�0��Hv��9�^v@U�yຝgO�6 z��x%�3tO\���t��.A�@���q�w��V�w�333��N�����d�/Y�e�����-mݞy�_}��M�Wr�m�����Tv�1�l�?H#�oKyԍY�a�Y��O����%�����j4���v�څ-[���I:�YP'1�$AR��"(i�HC���<`4�<�Lk��4j1�!��d"�I�=�#c�S���Ѩ]��Q�3f6���U�����.�����\��d�����6�Ey6�H�r[Z�~� 	�`o���+
���C}A �c�8�GJ�c��b��I�s��f��F�8�K�j�5�E&�#9�M;!�y�z�('������"���DQ��IE�ڀHG�H��h�F!F}�j�")������h5�u���E�m��������W�^qC�;д8�v�u���/dﮝ�gggO������G2��}�ݖlI�I�D�c��[_��$���6$Bz���>-q�m�c��P�A���p �&4� ���i�Ö*�F(͸A2��%���JW}��:�r�
��08	�Z)?�v�rWN��_�� 	D>�''h�	��5!W$``�6Ԧ��1ׂڱ%��1��/�c��\7MLLl��@=gb@��@8:�PD�	�o	�H�	��O;���F�9�����0{z��d`H+(y���XI��>�j#�ʐb��2�C�{/�:���������
�ZuV����g�~֜ЋoqT�p���רGEYbr���� ������L��{���jt��NGm��̲,��;���h�ĜgUd��]n��\�����W��������*�U�3�[9S7�ٚ[$�J	���Ew5I���)�Џd�� F@�0O�"�>� �`�in_��< �c�$�����݂6z��boF+�R����@����Aq�[C�~������6T:�Pz'�$��V�Ԯz%f��Q*���t�CjF��8z�j���K�EY@I/����
��,;��@ C��s�@�����qQϢjWR
j'f���@@U�ɉ������%o(|���A0�Ϯ�.?u�\�7�o��hD7q�l��}��z���}���[����5�����C�*71oX6m�V���-�}=I�lGYw�����q�S�ې�E*��TC<�A�L�P����f��D:99��+����J=���Q�.'��/hJp�������~��p��E�{��
)Lu�q�;��;�>-��A���T�����\B��9��r2����9�Y��ɩ�S}��7lW�8xϗ5�^K������p���Z���v��wD�Ӟ��l%���m�MRӭ�젻�4߀� t77�\�P��%M����4>�H���%�3��C�y��bA���.����YL�%�Z	�8J����ˇjG2���$�gf��cV�2�
=�����v�S�Sx���_{�$������B��<�Q��i���G(�Й�>I�` Q�b���p�y�ņd�Ю���_�8U'e_[~7�ꖓ�}�ž� D�7�?���;�+W�wҞ���8�o�LN����u�N��RnKHڥj��cl� �!2�n��"CPW�U�d)�������_��$�-�8�����V6�
�Pi��eo�~�7$(�~�155�_�j%�G�_�{����ſ�b��?��)����O�N��+��i༧<��׽��y֩Ϧ�9�󤅽��S���Z�>�(����>]�\�n��+|��:�K緈�KзH���G̀J�_��淧��[���v��N;����w<���cF����� ꆯ��N�a��SND���]�Ԧ������e�T� ���þ�gE��4-�K�����rF6rE���,��@Q�l����x�S�Å^�W��U���/Ó�}N:�d�Lji�����]�5#BR�/PNu�9�����o^�����d'd�B���֥KЇ���&w�"��1�ڵ�x�m8q��$������MJ��a#�n�ù#����6Z�Q;ʷ����_�ޫ��#��ĥ�h�$k�ؗ�d(�Ң��$_$��/$�fR�� ���ZU=����J��4N����~�z��������N�~a�_�X���r���)��zQ�d|��~�/��s�'��l�.~��2�n]n�8q�����_�s�VR��%J��}i�=�����e�w$�����SN|?1����4XQ���6�� e1D�F�.V
*�Sk�DhG{Xa��k�E���  IDATü�2�ቪ_� �&@�(�|N�����X����\�����P�7*��a%�e�0�z�U����T�d��S����.��\wkL�Z�H�4���t�.��t<.q������mLu�%�S���N���R�v��M~;��(�H�.�Z5gbI��lo�Di󡈊��1?�3\c���	1bP� ���T��Sa�d�H0b�ͳF��\h6Б垒��e� �CR/������/)��xffz�χ�����s���Q���-���A���~������k�q��w��#R��ӑȵ��/�115�qbjjcYNm����4)�e��[~%&�'"��Sj?�y��Д�**d��d��!}+QZ�[�$��I�����G
��FQ��ԇH'Q�4�U��]�\
���Հ�Ю,ϐ�!���1���{���������s|ڴK��ht|�'��H䫕ȍ���Q�ㄞ1;3�^����>ujz�T�`rrB���H�eY��~k�����B(���D(Jx�$�Kd��2���O�d���p��yl��8'���:C�F �w���3��(~/��t�����X9f�]>G.W�u�C�.�,NLNPNT��m��V	=am�Խ[o��/8�-������k���OMM6�Y=�Yo���8���)�z�Ðo<�X�b�^�!�m`�.A�Nb��.{���;�����}�6co�t��.A�xv�u�"p�D�V?�.A��Oa��.]n���m��v��"�E�V�.A��Oa��.������.A�稛a�.Gh�}���n�]�����������"pD�KЇ�I��E��@�q����t�.]���apn}S�f�E�����@��E��1�t�"���~�k�E��@�C�.A�(w=v�"�E��D�K�$�]']�t8���i�c�.]Hy�> ��:�"�E����.A'�[b�.��t	��y޺Yw�"p�#p�����y7b�.]��.A/+L�S�.]}�}�cލ�E��nM!]�>A���"�E�����@��D�>�t�"p"�%�Ԯ�.���.��.A�OԺ6]�t8��!r7D�.]�']�ޟ�uml�޺t�.A�K��"�E���-�.A��砛A�.]�F�K�c�r8)��t�"p�F�K�G����E���a�.A����`�.Gjn�	�H=oݺ�t8"��  ��s�   IDAT ��q�/5�E    IEND�B`�
```

### `src/flows/nudges/assets/protect/pnl-protect.svg`

```tsx
<svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="icon">
<path id="Vector" d="M10 2.5L15.8333 5V10C15.8333 13.75 13.3333 16.3333 10 17.5C6.66667 16.3333 4.16667 13.75 4.16667 10V5L10 2.5Z" stroke-width="1.33333" stroke-linecap="round" stroke-linejoin="round" stroke="#000"/>
<path id="Vector_2" d="M10.0002 5.83333V9.16667M11.5002 7.33333L10.0002 5.83333L8.50016 7.33333M10.0002 10.8333V14.1667M11.5002 12.6667L10.0002 14.1667L8.50016 12.6667" stroke-width="1.33333" stroke-linecap="round" stroke-linejoin="round" stroke="#000"/>
</g>
</svg>
```

### `src/flows/nudges/assets/protect/shield.svg`

```tsx
<svg width="80" height="80" viewBox="0 0 80 80" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="pause">
<path id="Vector" opacity="0.2" d="M40 0C27.7475 7.10508 20.326 10.5498 5 14.5455V36.3636C5 56.5455 19.9333 75.4182 40 80C60.0667 75.4182 75 56.5455 75 36.3636V14.5455C60.2032 10.5512 52.4859 7.44731 40 0Z" fill="#E5505F"/>
<g id="Vector_2" filter="url(#filter0_i_0_490)">
<path d="M40 8.75C30.373 14.3008 24.5418 16.992 12.5 20.1136V37.1591C12.5 52.9261 24.2333 67.6705 40 71.25C55.7667 67.6705 67.5 52.9261 67.5 37.1591V20.1136C55.8739 16.9931 49.8104 14.5682 40 8.75Z" fill="#E5505F"/>
</g>
<g id="downArrow">
<path id="Vector_3" d="M28 33.3338L36 41.3338L41.3333 36.0005L52 46.6672" stroke-width="3.2" stroke-linecap="round" stroke-linejoin="round" stroke="white"/>
<path id="Vector_4" d="M44 46.6662H52V38.6662" stroke-width="3.2" stroke-linecap="round" stroke-linejoin="round" stroke="white"/>
</g>
</g>
<defs>
<filter id="filter0_i_0_490" x="12.5" y="6.25" width="55" height="65" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
<feFlood flood-opacity="0" result="BackgroundImageFix"/>
<feBlend mode="normal" in="SourceGraphic" in2="BackgroundImageFix" result="shape"/>
<feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
<feOffset dy="-2.5"/>
<feGaussianBlur stdDeviation="3.125"/>
<feComposite in2="hardAlpha" operator="arithmetic" k2="-1" k3="1"/>
<feColorMatrix type="matrix" values="0 0 0 0 0.937255 0 0 0 0 0.588235 0 0 0 0 0.588235 0 0 0 1 0"/>
<feBlend mode="normal" in2="shape" result="effect1_innerShadow_0_490"/>
</filter>
</defs>
</svg>
```

### `src/flows/nudges/assets/protect/tpsl-candle.svg`

```tsx
<svg width="4.79167" height="11.9444" viewBox="0 0 4.79167 11.9444" fill="none" xmlns="http://www.w3.org/2000/svg">
<path id="candle" d="M3.99306 2.23958H3.19444V0.389493C3.19444 0.174382 3.0079 0 2.77778 0H2.01389C1.78377 0 1.59722 0.174382 1.59722 0.389493V2.23958H0.798611C0.359375 2.23958 0 2.57552 0 2.98611V8.95833C0 9.36892 0.359375 9.70486 0.798611 9.70486H1.59722V11.555C1.59722 11.7701 1.78377 11.9444 2.01389 11.9444H2.77778C3.0079 11.9444 3.19444 11.7701 3.19444 11.555V9.70486H3.99306C4.43229 9.70486 4.79167 9.36892 4.79167 8.95833V2.98611C4.79167 2.57552 4.43229 2.23958 3.99306 2.23958ZM1.59722 8.21181H3.19444V3.73264H1.59722V8.21181Z" fill-rule="evenodd" clip-rule="evenodd" fill="#000"/>
</svg>
```

### `src/flows/nudges/assets/protect/tpsl-sl.svg`

```tsx
<svg width="8.03918" height="1.25" viewBox="0 0 8.03918 1.25" fill="none" xmlns="http://www.w3.org/2000/svg">
<path id="sl" d="M0.625 0.625H7.41418" stroke-width="1.25" stroke-linecap="round" stroke="#000"/>
</svg>
```

### `src/flows/nudges/assets/protect/tpsl-tp.svg`

```tsx
<svg width="8.03918" height="1.25" viewBox="0 0 8.03918 1.25" fill="none" xmlns="http://www.w3.org/2000/svg">
<path id="tp" d="M0.625 0.625H7.41418" stroke-width="1.25" stroke-linecap="round" stroke="#000"/>
</svg>
```

### `src/flows/nudges/assets/protect/trend-down.svg`

```tsx
<svg width="22.6667" height="22.6667" viewBox="0 0 22.6667 22.6667" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="downArrow">
<path id="Vector" d="M2.83337 6.61117L8.50004 12.2778L12.2778 8.50005L19.8334 16.0556" stroke-width="2.26667" stroke-linecap="round" stroke-linejoin="round" stroke="white"/>
<path id="Vector_2" d="M14.1667 16.0558H19.8334V10.3892" stroke-width="2.26667" stroke-linecap="round" stroke-linejoin="round" stroke="white"/>
</g>
</svg>
```

### `src/flows/nudges/assets/protect/warning-glyph.svg`

```tsx
<svg width="56" height="56" viewBox="0 0 56 56" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="Frame">
<path id="Vector" d="M6.37004 49.0005C5.95004 49.0005 5.56115 48.8916 5.20337 48.6739C4.84559 48.4561 4.57337 48.1761 4.3867 47.8339C4.20004 47.4916 4.09115 47.1105 4.06004 46.6905C4.02892 46.2705 4.13781 45.8739 4.3867 45.5005L25.97 8.16719C26.2034 7.77831 26.5067 7.48275 26.88 7.28053C27.2534 7.07831 27.6267 6.98497 28 7.00053C28.3734 7.01608 28.7545 7.11719 29.1434 7.30386C29.5323 7.49053 29.8356 7.77831 30.0534 8.16719L51.6367 45.5005C51.87 45.8894 51.9789 46.2861 51.9634 46.6905C51.9478 47.095 51.8389 47.4761 51.6367 47.8339C51.4345 48.1916 51.1623 48.4716 50.82 48.6739C50.4778 48.8761 50.0889 48.985 49.6534 49.0005H6.37004ZM29.68 41.3239C30.1156 40.8883 30.3334 40.3361 30.3334 39.6672C30.3334 38.9983 30.1078 38.4461 29.6567 38.0105C29.2056 37.575 28.6534 37.3494 28 37.3339C27.3467 37.3183 26.7945 37.5439 26.3434 38.0105C25.8923 38.4772 25.6667 39.0294 25.6667 39.6672C25.6667 40.305 25.8923 40.8572 26.3434 41.3239C26.7945 41.7905 27.3467 42.0161 28 42.0005C28.6534 41.985 29.2056 41.7594 29.6567 41.3239H29.68ZM29.68 34.3239C30.1156 33.8883 30.3334 33.3361 30.3334 32.6672V25.6672C30.3334 24.9983 30.1078 24.4461 29.6567 24.0105C29.2056 23.575 28.6534 23.3494 28 23.3339C27.3467 23.3183 26.7945 23.5439 26.3434 24.0105C25.8923 24.4772 25.6667 25.0294 25.6667 25.6672V32.6672C25.6667 33.3205 25.8923 33.8727 26.3434 34.3239C26.7945 34.775 27.3467 35.0005 28 35.0005C28.6534 35.0005 29.2056 34.775 29.6567 34.3239H29.68Z" fill="#000"/>
</g>
</svg>
```

### `src/flows/nudges/assets/protect/warning.png`

```tsx
�PNG

   IHDR  h  h   z�a�   IDATx��Ց>����9H��s�9!!@"lc�Ý���g��pg�a������`�1����2
(����9��t��z3�Z%AhW۽]�R�z���}]]=3k�o�|��-�&-�t�<-�R�|� |�����ڧ:��>@w���Oѷ�o��i���y��-�[�X��p��)vD�s�,���p�9��-pQZ������-�[�b����Y���^-���h��]�&_I��:�|��gݟ�o���>@�����*��[��@۰��m�<�Z��-�[�4� }�I�
��|�� �^σ��[���o���>@D����-�[���{�����b>�o��>"|� �i��[���o�`�;�I���[��@�������Z��-�![�-���-�_'��|�>@���[���o��h���Y�u�-��,��sA,��1�?�o����>@���|��|\� }A��zqY���o��c�Ϗ]}��|��������[���o��c�Ϗ]}�',��|�x���}���[���o��m�Ϸ�}��|�x���}������-�[����,���,����-�[�[��|��}��-p6�m�>��~�o��:�|�� 'ٟ�o���>@����k�[��@۶������}!�|���-��oS_�o��>� �����[���{���{n�����s��-�[�#������}��-pn�����s���,���[ j������|�5� ��Έ��o����:j?i/���-�q,�t�9��L}�hg����0_]��:�|���ε?��."� }�L*�|\\���:��l|���,С �":o�T|�� ���d��|�O� �>ϛ��o��' �L֟�o��ړ|�nOg��շ�o�e�;���'�[ࢴ�E;)�/�S�O̷�o��n������-�[ࢵ�����'�[ b��~-�t�=w��|\���"?���|�h�����;_����m�>@����[��@Ƕ�������-�[�[��6|r.�j��|\H� }!���[���o�w����`�ɷ�o��>@���=}��-p^-��y5�/ܷ�o���>@���=}��-p^-p� ��j��-�[��@����$�S�����1g~�����\�3�-`-p�����x�i�����=���mۖͶ�?�����m�\����@������3�xw|�[������������?ſ�۝#x�A�	�;_� }A���[�÷������o�K�,���o����سw/V�X���|�mݶ�{|�v?�}�>���e���,PPPp��5k���M4���q����a���غu�8������#������-�[�<Y����敫V���	��	�"x��Q\TĴ��yR�{,`΃L_�o��������O~s�:��0D��b��&=��,�9qe��?��v����o�vb��fmm��}�����'/" I�:%%��A|R��[������T���8����?�֖�hnjV<�!�a%����CG�[��_JOO_sf)~m[���m��:�x�/8>R_�m/�y:" ���a��K�����2��vc��ͩ����[���b��C�q��~z����<ׅK�V��FVV&�L�B�N����_�>@�_���}�W�|K?�\^VJ�\�C� ��B}a�����}�a���7�WE|���>@���B}|48x���={�"
��8�au99�7v�������]Y��6s�|E|�w<x ����,�q0����:�t�Ä��������=*���[�� P\Vv�~���ѣ�K)���(Pq�q�ӷ�M�7���t;=q�����u�u�{v�zdﾽ���!0;֋QO�Opt��!����5V;����Լ�ھΟv�ލ�Ǐ�������Ė��~��b����?�O��f����ڷ@�@zz��xݶ�ې<�^sKx� ��sB|�������袙��ͩ�'ґ,p,��wv�ډ��20��D�Ya|�ڥ+��̜G�ͧh�0���x~W��;w�s�/�	�Ԃ�̣�=+B<� =� ������>-�t�<o���k׮CQq<�ӏչa�g���G�=���see�}���M�.��t�<m�������lټ�U�y��p(�P8��s���6l(��w��)�M�@�j���,���,���h�xs��O=rM�MV�p� #"11|�v�j��C���������w0���x�b�,e�������<x��k?ѡ?�ԽG���.����[������]������?"%}�����[�}X�.�KW������6�w��D"����=
�ٹ���o�G�~�'��~���=�������������?��Ӌ^x��/*�JW�#Q����� �>9r�+{��Ess��b�~���l�A�?=zvߐ�ٶ?�����/���?��>��}x�G�裏�O�#�cy��)/��c'ց>@w���O�}Y����w�߰�/+�ɂ@ ��Ai��HH�ǌ�3���m?��gG��ηw���Ï^s�o~�_y	��0��1�ex�٧��k����#?l�s�(u�����?ևj��&���O��|��3���f�y�ERR2z������3<s͡Ç���wϿ�����w�FXp����oE���ؽs7�?8�Uz��C�~����9ǎ�i�[V�0+�iE�	�S�N2|��iii+��-Q]e��m[�>�����C?�Ǫ�y�������r��7��*���X��|0y���}���Wܼs�N>��*+�Y����AZz:�N���Զ{���3/���?�/~uuuv���gD�@�w�ֳW/t��]��|��XO�?���ee�7�?������k�ax���B����7f2.|@�me���G�����^lܴ�z�"����1��CO�� ��2e
���ut��t�����-�.,��ܔ]�Pߢ��@Dl9..=�m�7�``��l�-[�n�����׿���t�8x3q,E Z���E�7� F���|�6̚=󕼼�_��o���ߟ�o�va�����OO9�z�l455�s]t��S&OE��]�$''oP�ГZ��ͦ��|�Ї|[6oF8�Ő��G��!8���a�Y���|ꓷ�vȐ��]�9���M[P���ѷ@��@׮�>s�L̹d6rrr�����d����lW^��J'�BϪ��r�ڵk���w����?
w1�7�����I�&�����+�,����*���0$�-p^,�G�qJ�Ex������IS�g?�ٯ��ow��O܂�}�6���w���7a\��6���ׯ���|��GPYY�J%�y%&�]ڝr;�o¯~��g.�B�M~���QC�ɇo}�V*�.�STTt[AA��J�/�,[���{�y�^}�~�g?w������w,�s�%S���s�_��?�}��gV�^�[�d�Ń��L3T�Yi����;����nРAמ���ם	�;�M��@����W^y�������s�w���.��s������z�g>��?����k_������_�����w�_��=��s���˼���:�{߾G��﨨���U�(�gff�Nz�����O��޻����s�#����q��~ƛ�P ���c�z.<�͛{���o���v�N����\���e��l\��_}�5﮻~�}�����O�S���?౿?�_x	˖.Ê7VXZ���/��'��{�����������n�������������{�[����������~J�����������|�roӦ�G�78p�z楥�7TUUM��Lۦ��f�Z�������oؾ};�-8�)��   IDAT+ [0v=�	$${L9��$|��[�}�̛�.]�����~� }����f�
z�+V���|�}��}������g�yk֬�N�Tנ��	�{šP��f��Ԣ���Ķ�[��ڵX�t9^}�e,b�'�<����ӟ��{	������{~�_�S��/��������g�s�O�����g?��w?�����?���?��l�r�:<]^^~͹���:W��U.x��������x��j����B-� m�޲G
�ۧ>��[�/_�gL�6yJ^^އ�m�u���vr�ڢ���=��x�����z��⥗^ġ����Hu=8�ABB��Ӑ���������DzR�c?b� l	0��m����֡����8J ߹m֭^�%�-Ƴ�>�G��O��?�	����/	ܿ�����o~���������c�^���^��o߁}��,*������@�P8t�o,{����O?�$���-0�H��.F
�t��'N��믻_��?o�6c�����E���dޕ�g�-p>|�gO<��]w���x��p��a��q��' 33�z���1�0k�\�`^u.��r�ay��q�߿?r�_�����r����� �q��%u'�rX�&@��IA�a�Kϼ��E��x{�N,]�>� ~���b������ y���6��i5u��b��=Z�mr�
��x��E�����>�*�*�S@�I��e��~10-=cǎ�?}����������i�6�t�Ulc8|��]?�������o@m�� "-5�'Lė����g��g�'���������������`��+�D�y�71m�t���pac�yAc��˕��s��t-��<� 0�4����=���H��#�uql������������7>s��ӟ�ם[�o]�� �v���OU��#ǖ<�������olڴ�
�D	b�����Dސ��������׾,��t��m��lsΜ>�oZ`�Ν���v��>���R�b�8�J��z�?�ٯ���/=��0i�t��F�ף��61l��C�JKǘ#�ɛo�o����={�4��D��6����@�c���`]��0��{�ƕaבn
{���I%���\�t��b���g�)�⡇�m����'=���G}o�6z�}׮����7���c�aχ�yw��ID B� -g����������&O�4����>,`�G�K���u��~��_-x�՗QUS�p8�@����q�ڿ~?���ƵW/D��}wNG||<��+�����0��}��SѳGO,X������/~�|���9���î"p ��$�O'�f��3A�u�M~��1�L�0����	��S�G'��\QU�-om�O~�#��s��M�og����_���?���SO>�b��<�=��A�X�a��φ&&$b�؉��/~��|��O���oF[��ӳN��5�6���N������?������{�q�
�o@����g���|��7a��AHOI�=)���C >Nk�KÀR|�`d�G�T�F��O}�3�̗���Ӧc+Ax)�� <4* �<�3�
�ڐ���c}I<�ui��a��̏#P�c�e�tH�|	�{�n<�����~��΋�.�4v��|������կ�l�2����[8��Ԑx�y�<�'��)��.������|n��7���������!,��y����ǽ��((ȷs6\��M��n�8.�t��n������\���W=� A8@@t��45 �XGb���$�q����A ��o ^}���c�F��A���{L�z�I.��(�)��i%��=h���i�ߋr�R/}֞H�r����Ç��_��	�k�\��.�N��g�Yt����Z��55���mH6�^����W\� �����w����/��y>0� ��Mx�شq�/��"�m�j'�������6\~�|t�˅K��p�.�FHI���0۶C6n����fd�:`�`� �����/���[���ʅ��O .+���Y_ ��A��k�����B֔����
��/*�t��HƬг�B�� �� Ǐâ�ß��Kp��C�V��MfS��c�mٲ�w�g�׬^�&�K�s�8�i��9\�XN C���_�җp��W�~����C�������.2=~���<�k֮������q_���q�es���6؅d(#���v턷t	���><�8�ؓ���<�� �?g�r8�������=�g���q���1}�l4��L/x����2��KH���[(Ї�%B!M	� @g3�=�`=��=8� ��x�q����Ǟ�bYi��l��ηw���Ob��M��-"֪1�(8{����c��a��Wo�/��|��)����>@8v�h������[�v5��v�����7w>���Jd�d�1U(�   K�!O���g�������R��5n�M��&� f������㽐W_�z�� =d��G_��?#1)G=��2s��	,��y�q�uE��43��6��u_&�#��ʡ� UTW�G|q�c���+*:��<p�/Q#���&��'�J�p	�a���`蠡���c7�xY��=�m�Çj�?Ts^\�4�������={����}�޽p�׿��t�ͺ�8ؔ/���>���ުu��ZH����9,m� 
����Q^����>Jp߶h!))Ç�U�܄Ԍt����A'hX9<�y��)�(+)����[�֓	з���D�h�3� �ļ>	4�U�7��=v���VuD=/J�&��~��!>�t�����g�P��3��L�����J+V?�!Z�+�C��QE]��^��Klۺ�UYp�}���5�܀��A�p�F���ŗ��*LQ1L�d�'�nc�H���HA���>a�b�!(c�6x/���&����,|��ϢS^g�� A��/��h:sڍ��y��<�XZvxp����<`i,ɡL!�]�K���(�ٙ�^ܵ]�v����=N>��
�
�A{��I����?|���xbРA����8�ׂ^��w_z��@~~��=�J����6))	�F�Ă��CX��v��r��k!�!+���Z��~�b�:\�5j"%w
���`��y{d�J`�.$�1z�p�7�Y�8�X�1�h�_xBM(��C�p-k��4J"0$�Ğ�P�(�ܟ����x饗�y�;��~������.��!�xv`x^rss��������+\����M�O�|�#��y�[��+V�l��ը���tР!�dޥ6b@p��̗z�-�Y�}�����ˉ ��^�!���C$k�A��`��R�Ry��	jk`�3���Rȱ��HN�5W^�~}�����P��~��6�$ġÔ�V��S�X�]XP2�#"�U�sp���~L'�9@�����X�l�����,v��O�>_����|�+_ƭ��4n���������U���oo�_R}T�9��#�78p�޿=���@c���٘9��&@�%&@�V��t�n��v�g�O�p|#�GPn!��%0�@ '.F�#L��!HKM��&H���N���c� ���{;Ǫ&
�.S�2�()L[}��k�� >CS��T Hy�LG�a�#Hd���ql�$���CA�:Ԯ�������}��?��<q�w\;�������h�2�������÷1ܾa����%���G�`5x�pL�9}���ǲGts+Jм��sa1�h,���(��ޮG���t^8J!�J��[��X_V���|�ؼ��6oB��i�f`��(����
����IJ	�!ɉC�D� 9�712���A=g.A�c�e ����O�K�t�@�`+_V���r�?�/:�֧O���7333��&���6tt�6g��w���'�D}]-@o8!�+.�S'M�`F��܌��^�s�}�'qQ���D��g'Fp=eҔ��ɻ�� ��`��z��������   IDAT�>XQ��E��`޴ɘ:n,���AAB"��YGcN����o���	�a|�~߭F�����.���>i螒���x�HdxDoB�����s螬K�\���q�&<�'���:�.����.�
��m��bp��uشi#U0s�L?�ٙ�C�¡�Mۡ���` �ǩ���G�f�PpV/��x�yL]m#����^4H^8��;�C�j�r� �d���V�BrC=Ə��Ǡ�|o4��pS=��t$t�B2)�k't���{tG�^�чq��b��!:lF���)#�c��q���<q�L�7�{����`4_�&R��ㇱz�kزe�vk��[�#� ��G8�?T���ڵ�~���/���
�������n��� ���˕�jxK�©ї��=Ô}@Pe�`B}U�����c�N�۹�ǎ������0��@��e��H��M+�[�1�zk3��A���0��x�	O?�b4�$��IJ@�$�3$�����$$�&#!-��$ư�22������\d��!�[7t��={�Dߞ�pi�޸.�3��n���ηw�>2����~y�M_��r�"��?��`�����d)�w�[o=A̟{&O����l.�UV ��9o�	# ����摀���9x�v��ڽ{���x��Alܻkw��VuQa���`_��Sz�J`(D�12,;�?ƺݭې�'N`hc��|y1�U���7'. ��Q�^Io�E�[r�ٔ���@�`&.��x����d%&an�<�#��AiI	^�k���/� mOq��ϻx���1�ڸ�S
K�X6G?VWYQ�h�CP�ŵ7܈�]��	`����m����3�$$@�b� Ȇj��R�6����qz�uG�	���J�9zFyY9�0t���;py��6Ջ4�D�}���]�������8@/zEi1
z	8�z��<�,��@T��<a�D�t�魫�No�����{wC@��L�����$�cA���?E%����||D0�8�0m������_¶m���cMKI�$��6{:�+��ݭ,��k7d�➁tAւ�;��&:�{��`C�:���2s:F^z)FͿ)7�kWVV"��4VVQ:w���@a��;7:�c`�+��܍��f\v�d��_/)Ʈ�
4S'��2���gp��׍��z�4�������q� �N����3�?���c�a���7����o�>��`�6n���}vܖ-�Q�Єczt�O|�HOK�X/�y�>�7o��5E ΂���	=�0j�˰e�vg�K���M����bܯ~�´C��ט�wc����1�]��#G�&�$丞PqTA_��:!8
=xa(�q@~��1t[��I����؀��8^[�f��� m�2b -���oB
�J�F����1l 7�9��wzf��b|j
\���<���GM�e��}|p�r��B|	���������c��$�w5rf͚0M<C��.�b=���3#Pj�/��(<|���5+�>w���:wL�~@V��������>���܌$z�%�%h��x#��7{�nB��� �D�A��B��c����нs��ʢ"l�_�c���l]���oER2�HfK��l�D^͂��>�7�+:�6�?��S��0O~~�W"5�ѷ����9�}�m����7��O����}h5����k���)Ipv�6C���u'��FX��5"0=_(X�7��/��'��`�5ס�ܹ��p 
���ת�k�$&!�ҹȚ7�&���� �v� ��՛ A�
�l"DO�#}�WUo��dd���];w�.�V��bC'����^b�^>o `lYH��S���A����|)�F'�d�$����� M��g���u��8���<�-�ߺ}���>�4*�"W��<L�>�LbɃ�����-8��m�H(��敧��E=��s�A�q��H������7�\�M�F�=�1u�F�DyI!����Z�W��(PCx�j��i䍢�rp?��r���x�-+��ׇ�;=`
A�Ԫ�����Գ3�2B�%8�d<���g��#o��d|�{7$�n�׮����ރ`��}�7�?o�}�m����E/�С�hnn���E��={�s�#�77on�����[�#�i
�T�X_��o1CNj�-X��aC�$$X~C J�D0Y�ЋN63g��!����3|!BN��%�e��mXCˬ��0\SSw�Nt��ƌ��ץ���aUI)�WqlB>%P_��<��G�U�@M���1U�G�3 ,�D҂q��)�SS�L���(�ڵkI�n����o��d�ϓh_l[��~�w����?��|d'�R�n]�b��?q"@�X�;
l�)� ూ�66z
��z�
���T��Fߏ߀��L�`�c�G��ʌ��0�r�gw�̜��!CQV����jFP\H�P>M��X	���Ne:�����<��&N!CP����J,�K��&
�J�������V2���pSN �p���X|7�|n����2�ر�/ƾ����e���%ڗ�~-p��9z�W_{���K�
�fL��)9d���x���u뀂"��k����H��G��7���sQE�Sg��d���	`~�=�����,�@D�MRD�5W�� ���� �W��Ƣ���(�S�(��#���MonĠ�L=]�vǑ�:���+�Ѥ7���"jsT��{"����D�"�4��Q�s� �A,��c33���7����k�����������χX_f[� ��q�-�@��23�0���1r�U��C���M��	��
�I� �)x50�PXZ��jz�~Ȼ�
8�;�M�(G�8��@8�Y-@ '��@����M�uP/
�Jgۉ�@�V�v/��=t�ѣ�3b$&���놺����Cm����K�u���*�ud��#��!���/���%��X��D��}��a��ϣ����7����
σT_d����5k��^[�C/���_���F#-3-W����+��j� / �SpPt� ǫ����.��"y��Fw�'8�$J,���0dB/V2D|�����#�����
�k�z�Ъ���@�}�8��qe�Ν�f�E�eb���o �X�(c�{*kP�)@=�.Sw;QM�pT�Q_�A�՛7	�LS����ج,d��Do}׶�x䡿�K	��!Y���|�~��ѣ?ܻw�۷�\�?V�i�[��m�[�z�����ޛk��v����4l�Õ�&�:�R~����ƞ_}�U���+p�	>��:�믇��!0��Z��}�� ��C�b|���/�����2��u�ht�|6L|  �dʊ�38���#���!��d��t-F�B]]A�^cܣU�f���L�������ٿ�r��`��W�w�_�_�rƪ�]Ʈ��������ao ���&�ޜ����a�!��X� 1��u���L�y(,( @?����� ���r�ƍ�<��s�c�=���o���~��~�;���������w��w�w��o����/z���g��o�ٻ���+��қw�\徭W-��ʅ�]y�߻��ko����|�c7����;��O&~����m��Y|�����O}��}��^~~�����E7#Bg����k_^�r
��!�
��p��WbȰ�HLN����:ٰ��WC���K���1D�%R�|�Wt�(*jk�ѳ�&LD����]D	�TD�$Pt����Q�D	L��,�ϝ���T�����
 �����V?M��h!�
�1C,C=�a2_������`wE9+7z��NYV#�JZ��M�H�0��Grat<��-�����ŤN�����zطO<����J;t<Z�ݿ�寫��v��/~�_��׸�{���;���_��-t=�   IDAT<��������O=��f{饗�NÒ%K�l�2�Z�o�}����-[�p�~�m�ڵ����{��7��0ݏm۷�7����?;|��]��]D���h6�T�j��Ǐ������M���{��ko�	�yy�[]	o�.ȶ���uG��O3(��h�&�@���NӦ#k�d��4�!����0�#3�k�2�-�:V�.e�,��fQ�܄�B��lFTA��t@�6`�0�O�@��%�#�4��k�́P���*�(,@A��h���ƚ� ��X�,�`�0�}�vYc�N�|�9�/E��C௫�ƣ�<�]{v�WUU5p���e˖����k���u|���7�M�6�{۶n�ηw� �C��;z��())Ayy9h7�Vנ�窉��0ϭ�)[[J�(^:�W%���������p���;Ѷ����y�=���\<w�\�
	z@fzfϝ����"���ݣ��m�)�4��3%�A=G�M���Pv��
���9��B����r=X�TPe\L�4#�S�JZ��\_���g΂���j�-��I�0�a�F)�/�ӋV�pa��.յ�j�T��M�K/..�v�Pju�A��%Ⱥ���E��K��D��u�9����lk������.��;).ھ�-,Z�>z����g�����1P@��֢�f��-y�1b�7U!�H�'���@7�H�����qw3�R��m3ۄ���nz)�>���8x��+	����뮿i�)Ћܫ���g�}�!��(����D)���F�ݱ�G"�u�d.�Ǝ����E�hg�T^��� ���T���S�0r�U���7E@���)	Sa?̓7�'kC��ǘp��4�4�dpn[꫱��G��q�.��Ӄ~��S�&!�S�=FЛ��ˋ��He����9��F�'���M��UTt��ן���XZV�b������^/����Hj�V�.�S1�S��Z��i�c땚�����|1����<�\���+/���ڵkPYUI,t��sg���Ps�E�J�[!|5�� �?!�YbA�6WU�� �!���=�{�U��
qL��H�M��	�Q��v��M�|�=R�d̘�o磩��C���.X���g �:[���Hc|��KfcP��Я�/+.�:z�!2��8��A�q��3�t�"!h��_I󠎖xS0!z�$-�M�/A����-)�/T�ۃ%�c��=/svbONNޠe�Ԕ��E�!*�m�0ϫ�s�Ѧ4��-�Dhs���y�����iv��A!���tM|ڛ>u:���VDE]4	/�f.�D�`����/�}�oP�X��bk����O"�p�HE)�5o�A�p-�IN.( 8�Ѐ�B!@�q���ې4x0bT��D���PΉ���Z\�d��L��Tz�M�(ݷ���~&A��8��k�4���܈���F��llg8f縇/5%!��7&�ME���8Ӧ�W����Ls�� ��g ��O��x!��8������c�Ç���ɮ�y�4��׋ƒ���� ���0�h)��8�0�0m���{|R�		�g��K�oV�<qqq���m���5C��q����E/�������Z@_��ʫ��拿�8�3�_�>�)�CO�ݸf�!"Q��],\Pjf<6���2���+(�g?d,�NV<.2K�@@���!��_="�/A�/��D �Bx�@,X�sR�M@ڨ�()/ESq	<�AŠ$���s��A?�kDp�\6j$����طTUaYQ<>	8b�ԅ���Q�J%1Ku����� %�a�7+!�(il\B.�yg��s'OIF�T����k���7(f�ԩ�o/�d�_��70m�T4����1h� 2#����ѣ�?��<y
�O���|�;o�<\v�e��+p�q��W��k�e�:�p���c7�c�>�����7�r>��O�_�"�����G����#�N��͕q1N˟�Z�o��z����4�ޞ.��\�I	�*-�l���
����� e)��\��((BQQ!����s�M���|D��4;("YoV')0+1kw�[�%�BP��5G@�%��̫����+?|���#��1>�F( -#0"px3
���8�a�Db�=�7'��8u��s��0
��4찼�P6�VG�3+"-���_���$
�L5nO�>	���[d:a�ڵk���/0DS�E
�p�v e���7�p��?���?��O�����O�ӟ�?f��߅����Ə~�#���~�����.����?�y���w��o��p�w�[w|��ַ��o~���7�����7���r�7�����|�+[n��'~>i�ĸv`����y_��Nm��w�~D?W�q�X��cF���Y3�o@_�o4����m�͇(X��)��O\�KX�)-C>��Z�bgzBy7\�P��+�!��M�Ow��l^�5��e�xF)z)jC*C)Ӧ"u�XU����n3C/�|��CJ���!�[q���1t����Tle��#G������X$�sT{xB=�Mg����g�����^�#}�%���r�E'!�z�ǲ���ʫ�;ܗW�w���y�.�k��F���ZK��ꪫd�B/Y.��r�?�̛7O�Ν+s�\"�gϖY�fY�9s�̘>C�O�.ӦN�)S�
=n�d�4iR�ĉ�&���>r��Q={��6��E��j�h�֡'�m�����:jj�,p������9r$�����UW!�� ]�Q�#�����nLB����	�����s�%��y�k��"�"Wk��Ӽ�	����Rp���z�Yx�'س'2��
��).Es�zѼd	��f>�޳a��A�X[�q�N�9O6Cz�FQc^�\v�,���n�_�̺"6�7ֳ��q�[�֐�*	6�_ut�'h�^q���Bw޸@�={w�ɧ��������}�/�
_��Nm�{��`Ū�ظi#��;Aǫ1�=�/�zv����Pw�~`�a2p2�>�`#�$H�\PWR�G�"�����n� 	�P"P�}o
��tV��2�';�.G�����D]i��8x��5�M�T��90=�Sw�J0s�@�;�/4w2����}(cL[A��t�g�*
�1b�m׃h�	�Z�̰= .����Ӑ����~�j���?<����xo�j|o|�o�U��ܺ|�r4���#P�e~���� x�I7<�\�/�Ăk����:Bj(?|%�����ySf�{ Q@��CRJ�Mò�[ם)Op����󄂣��N���㋡���VT T[p�,@�E���8�M�Z%O���3��уcH�>(%0?Vt;++P�vz���IQ	_ǵ:�SL����Qb�q��Ʋ�Ť��1(5s��089��@aq��7��u�X����P,`>)��6c�}ܷ���۷Yx���ǜٗbʌI��Έ�Y]	�w�={����ZA�.�*$ �����댩ȹb lDd�������E�N;j� F��Ȣ�4���:�����IKE���!}�h�76����s�e�@m����d� �^8ez��p�Ǩ�,\=k:<@1�;��;�c�9y0��ތ"}\�#٪ŜiW�˞�0#�;AA��N�0-;��)�8��ݻ���v��G�:�,�η�;Y��S����,��SOݶv����A�����/���ҽ��u9%�x>�u��h�e=�/����������c& o�%R����(u%�G��Y�-��H�c��Iuz�J&+��_�OOT������T�?S������p����_���F���������|I!V�%bI]=�eB�%p[�֛=2�]oBJV>�1v
c�ƣ��$&cfN�1�!l������a��wV��M&���8g�*?g^���[`���W����V��5NcXb���HHJB����ep��_�`FO�BQ�X��jK�p��Nr2r/���	c��`��>By"�`�7   IDAT�Ī;�NNϱ,��sl�����%u�H9!��E�73G��*��U/�ن`��*�Ju���2�p��q(hn���G���qmz��}@[(�Gh�Z�SbB��-^i��6�:8b02=3�s�Ű�K������%�q����T^�|��|�>WK�q>�M�g�}fܖ-�Q]U� �����񦛐�����K�7�w/��� U��F͂.��
y���<��t7��{��0������䌤l1��@bU8)�v(����$�����3g Ы'j���\\��ʠ� �
��~N�� �x�(55����,�e��a�0d��7�YSR���>=8� ��]�\���C�z��vjY[<\j�Q�.�	�N�VF�֠�v|���i���e����������Jm����b��]��?��(**�����b�ĉ�IpUаT^
o�Vx��A���`bAM�� ���2P�����ǐ����^��a��=��#.KB�"�DR��Fv�H�h^SV
	���`���M�k��IH�4	!qPu4��R
�����CBlӔ��t������EVZ:�mEi	�VT�YA�/%]�x�]ތ<����	3�Ė�p���Y�����0>y��%ٌ�vlۆe����CG~K.�-pN0���3�i���|�o?�=;w�����2d�P�ω��%CN��m���S]"Af(��]�m�@/���q�3��}�0�Ϟ�@�<�_"}Ј��VwME���$"��șS�	^����<uS}<�(H�6г;�x�	v���4��k �[۽(����,�3�p3��WY��#Gqݰ�����xl���:޸����LM�X<� ti�U��L�H$�,p�6�G�pB`�R���b|v6&��"�����K�.ź��{����8'�UxN�>S۴@iE�[�m����������ii�0a<�͘C���b�Uk�:��"n�mD����<����{�KH@�/�3�t�c傈*"���HMD "'*>hNe�H'�|ℑH�=u�5�� ja�����K@f�w&j�'Ip��/,��ƎFό4!���
l,����A����h�D�C	�TI��z�i;@=�ش���	�Z��Ȥ���w�������v�u?�[�l�k�lm����-�kǎ����P_[O!*P�q���g"IL^A��X	��0L�YϺ�r������I��+)C���KJA��3�<w&Lr��6���(K�l�R����9Fd�1���q���A�E��&O����#q�����!HG�hp�^�ڨͼ��(hR�f��ba����Y	��VS���������y
��v�4;7���"h��(/m(K�k
ֻ�8����9����J���>���E�6���Х��\>G����Ç�Z�f-֭[CL rP�tz��'L��#` >���d#��`-Y� ���El���Յ��,-Eb�<t��f8��܈.� 9	<Y�<6�4�p�s �޴�%=DD��ƅ)�� �F��W���(9�͌!�9L=[�ހ8AajH�4��p�N'P�0bFw�J�osUV��F����h�� `�[TM��� M��t��>a#��A�p�葘�'AQA֭Y��^]���'��`���P�W�l߱��_z	��e-�N�>S'OAg�$$���5ܥ� m(X�Â)q�#�x|,��x�HM�Iȝ0	sf����=��~ D��p�M��\(�����F!@+q@O�z�N��<k&2�M@au)j��/\� ����(K�m��T��P�<��S�u���=�����u5x���44�����6���~�v�¢�=���(i_�~yeRffde"/>h?�����x�ѿ�_;_�(�� �NO�����Y�jֿ�f����q�Wa���:x��+�A��AlB(Bp���C�u(<z����h�y�B8
�h3@pa^	�b_�*+Z-"d���[�4=��U��QfKKQ�4Ao&+�cl���oDS0���|4��a;�K>v`^��5%�oR_�f�0�Gw�#�3D��7���תF�1�b�2�<�A}�Z�(#R���ZV�<U�Lq�07#RR�@9e|JY��2,^������9��?�8�����v`�u��}e��U��(�pы&M����&�S����Tq���a��Y�?	R
BpV��
�Q\V���ǎGʴ��[e������{(��Ò-P4�P�F6�Ӯ�'�S@Dbt\�)�q\K�U�G�m&5���AF��������v�r�
f���8E�~�xg�q�!��#3�0M?c�DqS>tM��@���$j5
=i�@�`[�j�tu�/�_���i����<���/*,�_�� �K��غ���-���u�Ϸ=z�{/��
�\�&D'��u�羀޽{#���0Ί�� o�a\��3-�������G����QQW���w�B��L�� �G��=F� E�Q���l&�q��i���Oڵ]+4�Q��r(����)q��������9:]����oE�[WT�����^��NY�#z���TPSG���!��Թ���:z�O�cci!��f`h�d�pwc��Fd2�i'�	�S�v�|�#�DY�dga|z*�U��x�٧�n�7��������ڇtٶM}-[,��K/�p��M�#���K���S����*`�Y�&�Uu0�~źu�=㢢R|�V� ��ňOJAޔIH�6�D�!8
��)�E+���E%�]�Q���Y@Et���A5e����N)L��ؗ�v��mN�`T����:�n�Y�����U% C�h_���	�v�ޫ!�x�ʦ=*5W�`0
�����m8N��5ۗ�
ִ��6LT6;���C��1U�16n=.3s:�ORt�ǯ���?x�^-��[�T�S+�r۶�zϯ��2�Q\�AOz_��W���VU�}�a#8�$�B�m$���;h�kB����jlD��.C._.��xh��fy �B?��xf�mPЋ�]�]�u+�j��@$J�#Q2�f�%����h��-;�dcK�G�1r����!��臚�*��.�땭 +�2��E)�~��0E]#���+���+++���e{#F?>G]�%���R0wx����Μ�C/zZN���(�`ǖ��l�����{D��+����[@-����>�<O�y۶��_I3\�y��p�W`܄1��!L0:w�~�Gࢌb*J`*�XEa�WW 1�3r�M>P^�BH
FJ�A�xꕒ\z�.A�Ucl�Eع��G�af^z�,z~^}16oތ����ƣC��)��NT"��b+xGj4t�"�H�0�|1ZUR��	�y�E�0C/փ��7$��l��kY��ǉ�ǆGB �#�v� ;����]U}g&�V=()R��1��d�<�D��ƾht���^�I�G��$#�����#O=�Mo�u3�%''o`���|��fh�ܽ��P��O'7���x6�]�Ӓ	&��j�����(�^*%
}.�G��@�w�B��'3�4Cb!O;��@E����]�i�kcuMV�Z�?��>����?�!ӻ��_���������4���_��x�駱{��� ��P|�]k�c$���zv��C.Ơ���A������AS1_��䑢�h����Q�8J�<������\\>h0Rh�u��x��ż��O�piO׈\-GET�5��(�'��� &�;��S8��Vz���X�5B��o�V�
nU�m�eeeV����m[6�몃��[���;�ƨQ# �l.C��C`P|[b��X��&T�����i]{!�����PoQ��@�GtS��g��#�)�Ѵ�/��ۇg�~�ӟp������oX�hV�\��6m��7�cɒ�����G��ﻏ@�g<��Cx}�TTU"Ly"�a�:�h,+i^ɰ��ܨ��d�   IDATw"=�I��$�ыf�ªLd$l�a
K����xL5&��	>5z$�1&]�׺�Rl������Лǉ��G���n���R��*-�G4K�c�N\ �	b
���I'Pf=�U+Wa��7Ǒ��}�X����L����#G�������^����TL�4W,X���x�.t��r�(˄�T�D���/�d��WX����D���j�����| ASag!�(�2�fxP�c���aV�1S�P�_��X��e�/�ѷo_�?'M��a��%/qG8�����,x��w���׏���/�������:H���+Q�H����Sq��7� o0)3�!~�pTWU����N=��v�%���n�����w9���F����uGjb"֗�`)�@��x|��9.�yF`�2T�	�
���Gx<�f��H�:�	z$$�˽{��RA�m�V,}})�޽�e��o���
�9?i�(((���+�\������aȰ�d�\�9�8@��Q�nA`�>8�UQt ��f��A��e��ȯ(GV������#��v�NF���5���c����شq~����������4�t��ʿ�3��_��o�	3����A�йs'���FB��.p`����Ǻ�������O ?����Yv��������P���u8M�k�=a�X$/�.���HW�����!��-;g;om㤤��M���a���c͍XUV���A ��ఛp`�9���E�5�`,��c�JB�WF�H��K��`ZF:�i�Pc�2���^��}}�-����Om�{����GA�����Λ?�f̰j*
ax+V�TT���(��&0C��ʲ
䗔�!'}.�
���@?�z� H��� $!��f���n�>r��~�ڽ�\�o�����-�Ā�}�<�������G��wld������"2B���'>�<j_]]�_���,�~FX�=�ե^���<�*��C� /|�9Ƣ'OF�q�"�6WT�.2�6KB84� D���l������:ah^���0����7��!@=�s7��0�a�XN�VVW�����$G���[z�	�طg7�����zZy}�-���7h�]��;w�����-�ފ�&0L�2S�LF^���6TW���� C��dAG��c��5��AQI!���y��}�F�9��c�#"0
|D-͋�, �nM�/�+����.��7܀���c��w�#|�!��C�!���9o+�/0(�M�76����O`��<�UZI�J��{	/]GɁ�$�R��i����L�/D��	d��!B@=��� �y30�-�+�)��x�׽ʩ���2�-,�F�a�(�F��3,2��1+���dV8%-G��ߥ�ns#�r0=#]y���m[���5���xm�Fh�X�~���_z�~)EyrR"�Ͽ6�p	 .�<��Ր�0:�A }�1�CFEA����댞�f#��ާ�@D��H$�yrb��"�f�77�ǆ�ѳGOƚ�!5-��Q<�0�y�jBC ��z��1TG V%[�6����-[�`��-���@7�����eBM)�L��R�zď��)SQ�ԈPe�f}�0�OfO��D	��`]�M�͏��Ą�ݐ���#�ux��Q����*"`':�ԙ2<ÔU�q�lLg�[��sȓp�`�\�axM�NM��(**��W_f\�������p��˱�N���|㦷���t)�t�����c1u��vʅ�Gp�v�������< zj��A�Py����>jg�N�χ�^�'B>�P>4%�m,8HtlKZIV9������0|�p���Ōk/��˗-GEy9��Oo�D�[�t.�q�h;IE+���`۶mطo�a�ɝ8�-1UY�#�S��A�[7d\%<z���U�S� B_Y�:0$����fZ�0�o#��S��0Ǹ��QA/zYI16�"r��q�__2��!ʉ�+�ɬ����������2�a�q�����^	�h��`��ݸ�/�����L��ށ-�+����?ҹ[���j��%���\��MK�����}�����@����Z�m 4�(� �<� B�ѣ(��@|���4m���D�`u8�^{+�hj�F��Oώ/��D׮y�K]��o���˖Y]z�2�N��n��=���%Q��z�Z����[�ֲ9���]Ƿzi=�Dب�V�T���4�s3�^o�+�54d�^�ڇ�
�("�7��~,��cOIŴ.]�̗����GPH@�$��F��=��z,�T�8q{<q`J��q�/l�M
oP3�O��Dʬg�����[om�����w��`������&�&|����xc9�қR}���0�!����"3+���Ok�Œٱ�1�O�%"�E�z�����%��O��,����%(��	��x�,O$�MB��WT���]*�"���-9r�5;({SՁ9��a�ܭ�H��+?+��(�7^�	;GՑh�<��.�lI��h�ҋ6���r��e�����j�#��SSa�ݘj��z���y���@#SS1<;U����UY�:�v;v�\"*�N6�BO�V�n��+8[b̛X������,���@˅G���O���#�����:�LG�p{���?=n��m��eQ鬬l�x��у���5��o/��5p�=E 0H��hC��W��ET��8ZW���}�;c&�F�Db	����D��Pl���-����yP�ޡ��o�~�p9v0.xRW���"`}��euԇ�x�Q__��:�%�$��$�M�"�VG���J��)W�G`�P��֡��h�+UE��x�v�>�c�� q!�@c#3��O	� ����J�qkj��>�x"�Ξ�{Tr�Ix߄��-E��s��2����9�p��f��{k�|�{��kw�ƅ�/������Nؾ}��_{��l			8p n���HLK�+��8�-ۀ]�z�`L|�D���Q 87�����hjjF�+�@��q���:[���������B����G���aTEe9*>�DH%E��]�hI�<�G�.���6����i�z�Ǆz�JRk�K�D�����Uԯ��B����y�Ũ��>j�-����F�R�4�rf���<I��^^�F���Mʡ����Ƣ&P�"'6�;A��G�0����x�<�qEn6�'Dnr��Ux������-����:�LG�l{�+c�s��/�8 Bչw�޸�ƛ��)�q�Bgw���zc P� u�����wSUJ��1�IZ�Ȝ:qݻ�<x��J"(�L��&��0ꡟM�P@��	a�X7)%��O%�z�:>�Q�8!rFw� ��`����	T�@�B�XN�>�C��^�&� �� �G`ǧ|���M��p.IH��&��.��������]U�?�YS�瀢t�^�f�@�u��3�i�:{,;�`0C�꜇ ��w��5X�z�/��U���,`:�|��t��m�Ν��<��Y�[]ssr0e�$\��
�� �;���c� 5�BA�e�(`xu�-(�1�D{�W_��a� �Ɖ+��	»oʮ\�Y:�8m3onأ(C�<exR@nM������o��.Sk�N�g� &RM�G�L^�Μg� TV����QZ�@��°@K >!�/��w��L��<%'��삸��WKK�����8x�3��<���O3Qbbw�M�!��ؼ�K|.��㓓�@���R,Y�:V�Y{Y����u�,��ϓt_�{�@aq�m�<�(<�&z��ǌ���D��ݡ�X�S޸	���i�|2AFB�� C�O���r>�Rz�݆N@�y� �s.�@U�ݒ���7��T)"0엜�b��Fz�[A[�E���n	'6�D��PR.a%�'��F������%p\K���:)�*�8H�6�ӧ���y�� c�BЖ�M]�7��
ʖ\�e\x�
s���*n8���M   IDAT]8��|bXQV�-5US�0oZa�0\a��*���cd�*�'�	�	'o?rG����IK�gRɠ���w��X�l)�8p/��{���m�d���ްcǎ�<��3�/x�Z������Jr��.h).�l�SZ! 颶 FOP�[������������ވ��} ���*�P���,������%\C#_����:�@x)��[# ��ݘ���V�΋e�[�lI;�&[���KI8��[��	����Eh,*���  �l%{��� �ţ>�Cs�xƙ�w銑��H��VWы.!C �c��O	�T&-;E�Ͱ�H��&Q���
�$㰰[7�JIFz������7�b��7��P0j�mx��x����p�X���0m�t��%a&�Y��C�`0"\�d����ANcY9�
PG9�}"���IK�G�R�b�g��B��h�IQ~K>�(x���d=谍�9D� #"��y-EmR�U������h����-�rPPU��zJT��R'K�7q�p�\>������pM,����z��]	�y�������`�a�,	��~}�+-G�������A�7+�h�1�.�m-��\���.`XV�qy�;<��R��.]Пv0�m�v<��S���=,�{����2ն7����q�_^�yӦħ�|�E.U.�̌t\q�B��4�V�A��� V�����g.p�qq{����6�"�e|�������.��1�t�]Hܣ�b�qXu�.a�o:�E�~�A�X�T$���#%�	b[$/,*19î�IJJ���RJ�R��sK���x(���m�hƢ�NE��()8�fƢ��0<�/<��%6o�CRE)C���a]]#fw��Y�H�����j�t�8�	�r�����x�����<f\��)Q�+{��h^i{����͛���O}�]$����E4�v7�������;w>�|�r��� �O̞5�G�a�"|G����[�/�~BC�����r�ח����!H�#�q�e֓���'��,gHD�g�W7ėd�Ё e�dD4mM8i��IuZH&8����;	t��IE��(�mL����7^�&'�����BoX�eP�,O�a_%���(�d#�9N W��19�(��j�4�1�`@�[!XGdy�p�����Ub�>�$�c��sg��ӏP?�����=~W��Nv��-��>�e��V�^��+V@�bĠ�W^s5q4�b̳y�j������������(>v��H:y���G��׬@��l'�K>B�]	-�D9ZH���RD�������f� @�a7����RGD7��RRr2�E�Vk�Zi�tҹ��G�nIU��-Д�me22�4u2��N@Em�ԋ�o�r)�+�@�@D`�h�e�A�p�B����)�dƊ���a�L�f�w�)��ή@��vFA7��^ۣ/<O
C	,#Ԅ񙙸$7}�Ę��ݻ��c��Y]]=]e�tq[����=��>���z���V��3h(q�|/[x5ƍ���Tص\Y�����0��fѫ�X�=������EU|����S�2}*Գ�(�b3
�ĊДu
Lκ{d��/�RRS�/3���A�aU��J�H�,"�(���;e����X�Ɵ��E�x"�q�H���|�2:��%D�	~�}��~s>y�Iɨ+,Ase�&bT������t�x�G9��05�+�u��9���˰���jL����0��x����n�EY��U�Ox>����y�Fo��t�l�t� U�x����}�޻���|��Y/��\̓k�s�.���r�*lݲ���t��7܈�|�o�|�6���rp=�&z{���P0[L<�4��2��4�!e�dM���سEvDE��Rk�#lQSB[8�A�D� 
Y�vC:�D"1�J�r$5�n"y! &�n�R_*pE�Z��`�
DH-�̰��Sb)"F'���w�8g�G�B=m��!%��^m�y�A��f�c�e���e8=۩]� >���F<q�(
���<���.IS���2����D}X�*jJ�6k�H���3��?1	���12-��n��۶�W_C~Q����h-��<���lZ�z�J;r�?���%�\�Ӧ ==@JK oo��k����؁y!q}ӫk��\PV�`Zrf�B��q ��P&	�cx�&�3�A#B�i�@k�H�����T�y�0'�7���Tؗn,BD,�TI��l*_��%abRB���":iF�4}/��(�z:�z ���p�l���ʫ ����:1�X��ioMU%e��7ɋO�$z�#���D[-*)�&��˛C���>ʑ���ئ2#y1/�zϔ��f�mċ�x^��uF�c�h��O=	>}]�/�#����h^�����*��&?��?�c�� R�m���������`�v쀬^���\�����e�$@c������ȝ��E���p�v&?y�G��
��q�M���f�(" b���i�pGZ�O0.��DΓ�"�fX�$�� �٬�Ahrr�_Tц�.�;A��u��=8,��k	�)�,@�Ѩ�ͭ��nC0I�nLyT�4�ެ*§��!MK�5�{"�!�"/�E��WW���z��S�m���T���c�Q/�R��:�y�m�yS��t�KĬ��KOa���mx��W�g��G�����E:�6=-}�m���K/���Z��;�t�~!e�Ա@ `�ݲRx;w�A�P.�pӋ�R�p݇QO�C�E�$ �ƅ�a���;,�����d8Q�e��y'�c]�R󩩩З�M�1�x�lX�<2�V�vi]'�l������Ɵ��%"-��#��~����D�F`�!�#'Y�.�ׯ'*���TZ���#v�DϏ��0� ���wg���y���n��J������&�iu�)I�@xTb�l��G�������ց�	��d����$�(�zn֮{3���|�����iǳj��WVV���/~�|ƌ].� y̘1��g>=!.g�Z��]��lY�\�
4
Ь���A���(g���݄�Q#a�R$�4�	¿H�h`(@��Ӥ4%���~z `�$�[�'���%j{�Nny�� ��G�&$���k��H�4.�@�z��W�!�Q72@��#n����_2�.z�'�+ÆӋ���rIQ6WV���>Q)�����NS%;Ɉ�ew(����P�+=,����ٙ�H8�(*��%�c��KT�O���/�I���W��.]z��U�QSS���_���5s`=g��=�ض�1�r�� #<]��~�L��XUZ���z�e��'n@\���"#�3��V��f˶��6Ճ��]qD�"���$���P0�O�h���faS1Bt�r$����4՚��d$�'�(�R�	Nm}/�=I�A})�	̋0�(�SKƜو7
�Uh((4�EH2hB�@�x�a8����������tƢ'��Z�^Y]�U奨bH
`W.E�0p9��<��S�t�JvXmTb'ӱ������� >߭+�jH�m+����/��_뿕���"� W�E6�6>�#G���ѿ�j�ω��=S�MCbB<"��!Ȧ͐C� ����	.���tq�C��|4/-.BcZ
z^u5�F��II2��%w�� ٌ�6�RKа�g<x�hiK�8"bYo2�	��p�sFDǍ�(8�~<���p��ǝ��k�u��m=`S�B`�ߪ4�ǎB��)�Q��~.�7M��K�P��Tc�� �e�)�3#'�+{�@F|���++����h�X=����4l����o�
�Z硑�)YY����̠�R��|��uX�r��.��h38GEx��#����-p���;�-c���K����=zb"�h�F��~���
�I.hzNvp.P�(��A��T�7 y�`t��V:�B�aA�� ��B��X)D��!������d8�cZ=�w�q�   IDAT o4:��)Ʃ��I[#�Z�B im*_>��+��*-���/!s�/�c��	�
ҦK�L�����PR^���b�a�d�#oK4����Г�z��\��@
�g~�<KKG�^6��`YE*�� �;�g��*C� �F�G��QG�&��.!�mc��f׹�<;�yC�v�މ��~G��!�������f��'�e�ֻ�z�)Ti��^Z��y��7a�z�3�t9������W%�5�˴ezPWX�������^2�S&@�4n�9Ƞ�ڗ ��E(O�ށ��llQ�P0�!�_�i�XEz�i�t�HP�H��yS?^���hMD�MDX'�b$�bX$ϣ���|���zӱZ�$�Թ� ���������m�>�T�M�Lyv�� ��Or
t)�8ʛ慠rl)+�0��:(�B��2( ���5O�>Pg!i
��	�����n0��}Dj2�w:��Z�r^z���WWϱ���Ea�?��x���6lX��kWqD�R'z�3g���aC�H]>z���M��:�#�����:�����)� ��+���	�� E�	""6���,"�!�Dbu�NB�M��:�/>>�A70� �y��̳L�:�C6�O���HKOC_j>B�(��$�H�t<%V�q�X�f؇�hoK,�:#�7��!#QZZ�&>��)�^:cg��Y���8S%"A�r������m,zo]-^-,��K0�8�!;���\���f�@�J�LD7��=�=1�ā��<�fggb@RmΧ3<���(//����|�ՏY��2~z~-�t��;-z\j�t͕�a���HIK��Ϋ�D����مo��r
�.pp��w]@����C�is�ȗ\��i;AZ�ZA�� ���0� I���,lb�V�E�#pE:����P3ԛ���`'C�w�j��ǮPZZ	:"�Q������3�rr���b�Ќ%i@x����O�	��#G�W��@�n֖�ܨ���b��f�KI�ݻcdV&�Ћ~��*�E��h��h�^w�tǍ�����N�L{%p��!l۸�/Z�����[�o�|��N�C��^�j%�m�lGSo3�S..\�>���:���>^�[��qK�>mᢴ��f.�Fѱ#���G���Z0���BUP�PK>���E�� 556#�=3t�CT�nMZ&��"-�E2C=
�,�V�<Zw�&<[W����S�*/F�F��S2�?i��FYc-�߷/U=T����ð��IExC$tBD ��'��b)��)jj�C�&�# �_�#W��wI���G���.��wE�7�pIzf�������}8|��]�,�om/0�E�����/�r��5kP˗G��2-5���'1|�0�pqٹ��[����v\�Z��=!x_T<�R�7�A6�$aP?�<Va�����
9��nj�a�$�gVw��R�縸x��$@�[��t�^|�-�;�z.��XD��J����������y�2)�v��u`_uf9����Onz:j��XR	4� AdU�f��r�~F���d(�r����.y×x�,/*/�ֲBԁob��]r���>���]�ġ,�
�Cr�a�>ǟ@�����L>���޾�.z���ݻ�?M�_��,`ڝ��L�{�>�d�b8�ABB"���|r;w�CO�TW���پ&���K3��� ���+Pr�0צ ����i�!�	�dd?�i��*�U�`[�Zv�2�"��?�g��h"��! �'�ӑkF�� `����:+�� �L$����V�k]k�!`��� >�5o�㉜�*�$��Q��3�lG�b|=��M�qH�=icƢ����^]cT���/����</<O�;�I�`,C��uC��a���q�
�xy6�@��u�H�,ڄ'�2[�±��E@�Y\�:LtώO¤�l\��A>�!�z<��ظ�|�"���[�v�y;Q���Koݱm���cЉ�w�e�c�g8.Y��c��w�)��p�s�qv�t5��#���Py� ��H����&"�oOظ���.p��Z�� ��B�ʓS����u��D�����%�/
C�p(�D�C/NA�2p<Mc�i�m�ɥ�Jʧ�!�>]����q���˓���NDlѪV�1�=TOU��x�7����_
霋��
4�U��z<r�oL$��'�x����%1�:�atf��.^.-���2��I����c�29.wflA�|$��9���d��"pŁ�s ڼoj��� �7���۷aŪ8x��=�vm=��zmYy�Y���g�ő�G��9�w�����s_�������{{7��{�c�,�.\]�Dgx�!�E�C�8șw)�G� �L�J����1(WeCb'�d=��=�D���l=�@
�.�G��!��S6��R�:���_!���q��� "�P��R�K�S:�O۠��R�_��1c�D�������d!LI$O�WS��c:2#7��d'����X\T����DW� h��[�}tl��kw�fJn[)i��ew	�:�L�1�7��|ٜ��5����%X�jՀ���k���۩|�>O'NƳ/�p׶-��=W������/_�C£�����o_�{��=.\}i[Ph�PQX���2$u��+�"ا;�Fv�j�
]�L�Й�n�V�
W�Լ��H��&"�P��
Ì��=ҧɍt���F���)�ؔ���$��ɉu����]��2���U3�Jڨ@f�����*��FCC6�J�����Rx�������J6�aG!�������j��05�����<>�a�clV6�����`+��F�8t�D���Mx����{Gw���J:�ʵămra(G�~/'��xy<A��l�J��w�Q�~�-��Z;T���\R\r���;��Ze�3�0q<���J]r�Q8�6#�}�CG >�Z��!�2\��U��?vuqAt��$������T��(���b������1�Kk�@4yϔ��s<��8�������"��2*����i�=q�4$��j� a���X�\Y"Xz��%h�g���9)	�4I�p��F����j�9y���)�M%Er�xd_�׵i�O��eٙH�\\��5kV��%���vk��ڭ�mU����;�x�v�؁F�$�'7~2.�� ]�:[�u)zk�@v�_J<�]�\y
�����k��Ayq!��M��5W_� _.���+�D%+�@�����9�-}4#FX\��c���Q��yQ�#�e��N�֞� %9��	0��mm9�D�rK�]2-C��Gy��,#�ˁu��Mf6Rf�F�ԉ�m�F��� `�-�#`�u�s��}
Jtӻ�avv.R�t��/W���={���Dɥ%����/��$��D�+�G�#8B^,W�8�\����Yb�����x�u,~})%��ڡxE�C�۰ʕ�u��m���G}������l̘>�&OD ��
�T��Y��X>=���'p�#.p�W%
��M�*)FQ!=8�{_w�0��AoSSKZG�扬Zp�G��Z�$R�P6���p�D�II�0�!�Gz?G��E�@ل�'����
FJ��C�}Aoe�ز�HK�uFD "-U�Ӣ�-�gɈ<%0mE`@	���	c�4w6LZ:��Ģ	ʞc"}���Ğ7@���O�e�Y�x�ҷ�'%�X�oTT�����p�7�r)�Xzj���	� ;
<�Z�X
֬��{�%��*^o}5��pʦ����>�
�h����Y;|x�=K/��];[$�3ƏC^�@c��)���0����A�W��B�J��obhC��� ��o �����#��<��Ө����I	*/Z�DٴFl�hM��A��XӲ�Xl�l���8�4=C���W��+B����N& 55q
�2��������9I���Zuׂ�$6A�ٖ]�
O��W¸1�;U��h,)��7A�7<M$   IDAT�FW �ےDzS=3�XV�U��Х3�ef"9��������CM�L�]��J���[��(�=��Ќ�	�C�x\���Q��H�M����֮���+^���;pe�;�ϓ�\lYYقu�֎{����H=��̛7C�e���W�"zį/�)���9Q�q��A�W��BEQJ**�v�.��G��a =p�C;p';��@A҅�"�-��g��%�ZP�H�z�&	�´N�͊�����oXM^-'�֧'��� �^�֋�&-$"�P�R�py�R��=ddf@Z�J��n����6�m�Qv��1i�>�� �!Ҧ�#�u�����a����H�|.�))�:~�:��@蓋%� �Gq�=� p�@��2�~Y׮���#<�o��iKϫ쥻M����1�����(��ץ,�� �\c(ot��20�����8����W8r��3��ڰL֭ݩ�{���__�۷o璅�I�'a�)����4�$r�l�l�	il"�X���Y����r��^��#���k�g��D�4�
�22{��#s������Q�'*N�is<�����0=h劏4���꣤-��D�ʉ��SVV������%y�.ʯtB��[��:�-С-�M�Qj]�R�&-��<"�w�L�\ơ'!e�xTX�*��>m'8�`�P��+��'��JS�:w�D�҂A�o�3EŨ�B�l=a�|9D
8}�P�p�i��2� 33215=���k�c��W�|����~�M[��i�ڙr˖/�"XW��%����o�}������bL���U@}stvvi�Wr	���=���*���.�g!q�P�P��X��ܡ�œH+�t�h�8�i)Q�$��~�CV&�+���"��nW�!�DZX>A�8J��ҟ�"CDu9!�T_&'��D%�]�d-�	J�W�<�;8��4a=Ra��/���7_7=������P0����
��T f��+��!PKC�� f��b��E�jW�aoY\�ӏ�Yb�P�j���d�jc��V	�rކ�pl�2B.��%`ZZ'&�]���������n,`�QS��],�z�o��U8F`I<���s�c��H�㦮;�2��V��&�u-��͓K��2--F#z'�ϻ�
�tH1��yh��v#��AA0))Ɇ$����A�ԍ�;*�2�O-<�����J-�;#�&F���YƏ���A�%sP�T�����C�.���5O��`�&�in��E�z��،��j'gf!S45�O������h\DePx �Nٴ�D����؆ƻ�	��9&�/�ϼ�ƛ+�㕗����axm;ǫ�m+�^�{��g�a�z.v�����EW������	r��fn�����H\Ԉ.D���n3��G>cة�ǡ��9���D�8�����ew0�#F�I�ôB�z7j���ωq�,�`�'%&!>>�O�.��*	�)�<9��	 �DR�=M���Z��tk�Y6�9M�YxA�D�G� ��*k^����k��?�^puq	�+��g�6"	Z=hK̫�<�s)>-!s�1��F%۞��Ɔ�R��k��rTc�a9\��3oF�a�ǣ��n�S&�������4�IK%"��=�06n����ڼ�v�y�ے��/��\�%|c�ze�����1n�X$&%څ#�0;ކ�O)\<ʇHK�=&a�E�8��_�����Qϔ�D�(	�`*�<�Z�i]<)�tbtR�8�� ���3uc_�h���$�{�ۏ#��M�EI$����Z{����R�S�X��(d�骩��:M�F�}P�J?�Ce(�nQ}"9Bu���8���1v;��Ǡ��ԕ��RҞ ��z�t�5�!.�	*���V��!���9��2�/**DCZ.C �	������G`?��O%Z	�u&�U��Ck��_ov�S�07;� D�Ų7�a��(A���4}���'O���C?��;w��o�uQ�����-H������g�u'��FZ�KK�K����P]=J�e75 k��L����ݡ]	\쪮���"W(AË��^)���Q��#��ZE��#P:���x�t2��q>ȹ·]Nߩ3���2(����5p�q�Tt0[Kȫc)E�N���������Z���D�j#K�K�樢D���l�de#���!�;�����@�<���p��4��΃va�1)7�rrX�RQ�m5�"?��@���Q'e�iK�NI˖8���uJ�E���S|"�R�I�I,�u�x��W�b��e���ߧ�k�?�������l��%K�,FqQW��<zGS�N���3����ɸl��ې#0�!. C�I��*��P_R�C������t��H: �K�SR�NW�.\�;�b���<P�<~�]���	�Lcu*\��1�5�Bc���u�.�#VŲ�T���"����r�A�kjI�?F-�g�Xmi�s珘���"$@�8k:�ǎ����nu��#����(Q�l� Ϲ���U=z �2�+௕a_}-4l�78����d8+�Պ"��V5���#�A��q�obn����6�z�m,�O����f4�іw��ڲ~mZ��������?����O.s��XxŕHKO!�_��� ��il��3
tZ���jjP~�8
ɟ�w 2/��`�<.~�2�P��zYd�]��;G��9�@Z������p��A�:��T=�8�5\�j��2��';���
��4]9om�7R�S	B��������][D�x�&ylRbٕ�7RN0�m�w
i�g!з7����TR4�Eύ%͓tn$Q"PQ\xEy2� ��v�d�|�7^�KǍ�k�H�OS Չt\[�)ǰ5���*q<{�p,M�8�K;u�p�ے����uo�ŗ^Fmm�8���6j�F�j�j�߼y��_ya��뭾�s:a���3o�-���d�r����ʀ`�!b "0fIr�B�������$$��g?����!?����~,��NL��i�#"�Ӛp���L*/B�Z�sP��g|\c�M|��9�l��GE�io8��ζ��!�����@���&"��X�ӷ��8�=�G�N%�#S✙H�4��j���+�v�7!�DI����0�C�vX KB2�4hrx����h�_�`��p�e	�\u�'0{ا1��)�C��;3�5�Ao �)�2>q	���Fv\"�ֵz�\
ٿw7���o���Y��6j�F�j�j�ݽ����4��Q@Q`�;�R̿t>��_VEg�Y9rF��Ya,��\�ࢭ/�@Ia!���:�/����EG>��(8�LuѲ���
ʪ��D��+@kYC��B��IA���0�WfF����jU���\6�AD "�}D;��6״��Y�H�4�G���͇�j�^�\U�VS��<X��y֔\��!Yfu�N/:�N k�*���|�!6Z̮����k�%?'�wڬ|��2�C�=:˳;w����	8�a�������N"��l���	(((�}æMX�f���ӫ�L������:�P�)>��6��j�å���b��{ ]%��k���BO��D�Oތ S<�(�g^�-��62��ev�$Z{��l��ziݟ�+�&$�C��b!��q|*q�B񀵴���Y���GN� �����$�p#"�Rd9��9��ցuQҲ�뢤ej��b9M[�  E���`	r�e�|ܰ!H�>�����6���Q�z�;oY,�H�^���y����x�>��x��m5�x���6[���Sx��%��Z�dH�W�ڟl
�a����5��18)��@C4�V�ċ�-����$m�`ڜFmT�������n����Ey��W_�͝?�L�~��K��˹`W��s$��i��� �^,����(+)A�9��#��y.\��"��~�残��;����9	�;�㠈�&¬0��M��5�垦�A�0�]ABe��   IDATۉ�$�L�m�H{�(8��;u� �<'Z`ǵbyQ��7O�C*@3l��4�kxCI�4�G�����<�a�6Ε�Ν� ��z+9g�؏��g������<L��B��Vu^..@McD�4i+��,%k7���Ɲ�7c`�V�Z�q\���r1:=3�2�3>!�T<����AT�����Ϋ��)�5JNNޠz�޻���|�n�Z.��d8_Ν)z�����w�\��V{."Cs۔yv����BT�sJ������/�X��� ��|.4Ĉ��+��X�M�i�c�̻��5E��B��$ئyM"Y�:|=hA�� e#���ؤ],�P{MO1�|�](�!@w���P�}�ξ��HJ.D���GDNI'��)�<ɗχ�����|���X۴�z���T���j����[7IOG�e+�ծ-*1B 7��%JЛ��&���c�k����*Ws�xa����!�i�iH���>�X������b�􆿵)1ڔ>mZ��7����7�����2��Dz"^�a#G"15!R��᭛�cE.
��̰/|�(<åɴ���\���=��DY�9.Hl t=�&ְ��w�D�"GP�Y{h�42+AS�Iв��Њ8���	Ъ���%��\
�'��6ڏl��999փ��(G�D$�'��3u����=F�b�^�X��h�$%i/��:�fS�31&���0q"�F2���0�]���-��yhu4a��)����rr���{h��
�E�[�v�N�
԰��N������0�cd�x�l,zt"\�;��0|���Y��ħ6�K����PTX�Ev��6dӆti�>|���^{6D^|;�����k��]��njB8�8�U� ��ja]��25ϵ����؀���PYW��a��=o>�^=����zk�2��֡`��kr6va�i���$�
s�܄mL�."\ϒh�644r��!�6B3F.�Eɖ�m��0|��_�ӗ�N߂N�9v�D(Vw���Y;jz6JB����	�h�� 8�HψG/:Ч72>�	4�%����j��\�h!),�5 �#�7m/B�%����1�sg�!h����+U��H/��׉06ց/A�xP�DH�,�����,.��i*/�3�����ss�"@3��ǟxom�:�����[�� ��6�K�WdѢ�]�uU^�HNN�7�{�`,6^�`�Ȗ�`���ƒ� ��hi]��D��q���R�˛���2g@����$24�ȅ��i?C�V��Z�&q���Zv-� �GEN�&..�*455¥7�Pox�-)����TRQ�z��g�C_�D�g��Q/N-$B�7��+��(�x>**��G� ��|���>J�<��7���Y��)ɴG!��?=�J�2�ؗ8�^��duz�J�E��<��+e�~��1�cMM��P���g�E�޿���S۰�ij�}-�o߾��Ǟ={��I	�4` >��[�·������>�Mo�8\�����.�<Bu��߿�MȘ6��f�dg����*q�B����e�w�L�A�w#����-��o�f(JS&��"Q=��_���FX5������+OKڪ����p��8�I�32`=h��"��Xղ��XA���)��]��eR'�Q���9�!<=Ð�d~��hꔅ�R��b3�?��Sr@��Oa?7��z�*�76�o+��qvv�Y�B]VA=j��x%!�n�Z�W㨮q��lla�浬Ģ��?4!������Cz���v��`Qi�m��Ӆ� ���D{����=<g׮]hdhB��ի>��O�[�����ٲ��5mdEx�%i].h�@���ªr2��u�<��M~��1����Y�",�6�Pߡ���"z�qx��hM����he�����iSs3{c�6���DG�ă�1�S<�������}�dѧ����p��,P�U;�n$���'�$̝��Q��@��J�&�)���S� ����*��B��:�P�g���9]��S0��b?o�!��D��ׂ4�gutW;E��$�6Z�
�S��=�늃4Ą�T��HC�j+���˯`��u�E;��� ���A���zΦ��:����P������a�ȑ�7o.\|�I��Rعf�>�s��f���6��c,��/���C5c���@��	p�9�΂,SO�Yb��*c!�+[�(��{&�p�8�\��ɛ]�zP:�����D�/�D͜Oo>�:���'j�o� 0�8z�)
�rDޥ/Nl"��N!�\f-�S6���)�"'d�hf	r<��bϯg���P6�/�^�.���Dse���rH?(�����8N�tS��pXV�ff�#Ǫ�l��R�֣���S5l+KT�Rȩ;(JѢ&�ؤ�<1𨇫�����k ��vBm�����j�
�g�m_�pA-`.���gԊ��k���{�ٳ��YE���ܹ�ѻz5��Y�: ��	).�p@_�pq{��"�P���"p�2s��ګ�4x����{&?��<\T"Ҳ޴�������lU�t(���	�	[��*q�q�n�O�:D�Qw�hN���\$#��Grr2c"��p���Zw�9ƨ�^����e����N������!q�$��F�r5C^c:? $�(��=�<��q�(ڋ/ҋ�2��^+/Ǯ��]�oxc�NX��JTѭH�lh"� �c_�H�83s�1%=����X�b��\}7��[��W�W��)PUU5}��ݷ�����`-/m �򤉓1k��` ./�0���p����h�ٵ.<pQ����ፚ� :͘��)��͉��r�ځ��*<i�;S�4='�ꙪO�㺆�>�D	�����ӏ�52�a����"�N�EA�#��c��r���A�X�t���[L,S��%�F�OQ\��b ��N�o_�͝���eh,�C@o�B��D���`���gCY?F'L�x=M�����t�/ѭ�׺�r�74�� '��� AZm���0� ���SOp``x-�d4<�G��Kz�<jlzǶmx�E8z4�{����z�.��m{肂��,^���zpy���ӧ�O�`�x��x��AW���.W .�\��j�Q]T���
$�׭�D\�Δ��@(�n\H<��]�}���:�b敘���QO��䌎����D.p�scC#�@!�R�)��?�0/q��!B>�ֿ;�g����&�M)Z� ͞���S)-�2���3' K��A��H�2	M<���@3Ŋ�i�,���m��e��Dp�o��Nn|n���t �ɳ�^�֪*x:&���޶���R�G��Ԓt0%�p��gڡihc� �������SY�)/Ö����?d���b������Q�׮�ڹk�͏>�xC���8\:o>�Ιk=���,Ys������Bإ��Y^ua!�򏣑�־�.A*�÷���>"+�DD�k!�uL��T�SF$�7��S�wd��ї{"ii|4NKe���0�i��D��e���J�tw��1�v���f�h� U-F�4���󁒝S��U� m�L��PV	��M~��٣��@Jx���bx��u���|�{a�^��bC�k��
=��p����G���=1���n�ql�;<DR����yq9�02q��Os����o�^���PVY� �v�,���ޖ^�n����Qt�8�b�3�a���/q��ٱf�.��:�G&鰦�f�O^��*����^Pz�>�������ٹX��bI��s>*���;�1�G�H%V��."-�"b͒���nݺ#�îݻ���j�?��!����f��H�h�M�|�ױUXjJ*F�YB�!h�BDl�H$��S*#B�}�)��X���ޑ�D����D�ͩ~:6���ԋM�4i�ͅ�(޷^}�
��|��  �y(���D�ZV�5������Ϯ   IDAT�>��ױ�ơ�U�!���0��U���ՁL1m�w;���f�k��ےj����MJ���ls�73l�����������.���3X]�ҽq��|��/"R�).��j9����5�t���o칰�ʂ�. zF�47���?��e�Ӕ�0@Y�ZI��!£�)aJ�����Y�y!0
��o۟Ǔ�.e�zE��FD���!x�H���С�1v��	��+��)O��zS|љ(+���K�_
�����kں����|*�P��T�R�x�x@˦��k��y7�Y�������24�V�mv����������s� �')W?vG�����Qi�H�S�ۼ�^.+�_G0�"��v�ꃳo�kR�'J���^{�r*Ǚ���I�)��EiI	~�!<|�ʺ��g�ު��~����P�]¶m߶z��U�=�u/�/�9s.�ԩ���9�H����ݻش�އp�	��7�=zE�ps9��4�'���9W.��1�c�å�у�t���.���G�i���խU�9ec����ҁ��%��֤�Z6|8.X����ʧf0���~�$F�@"$��<}z���K/'���*@�K$<by9G��M�?�M̹�R-U��N������k�O	C#��>z��zD�����|��c�a�7L��i;m�K2��X1���5�XW\���V��c
�b"J��զ疤򔴅��˱�!���yC}��f��z�hl��>!>��"���ެ}}�h-��)�V�yٲe����C����t���-�}{��|�����w�^)�����.4���ʬ�0_�+@qE�z�B�YH=
 �DL��*���a���\�1�$a):����K�zy�Cnv6f͚�/|��1m�����,�eJv���$��1|n��F�p���/�����DN&v������L͝ 9Q��s�)��תR�VҪh��uF�̩H5U�h*-�����:Ҝ���N�y�l^@�b���	���ƛݑ�&<��~ج/cy#Iyc�j'��G�tY�;er6y�Kg����2��X���tL����4☏�;v�]�A���>2� }��������իq��!^�T���>}6�M�l_�Y��xG��۲�������Z�� �XY���B�x@�)Ȝ9�P�� ���x�]�6�D+MOk�V���?Z���&[��`>Z�8!K'ZJ���bL�~���C����O~_��Wp��C��ӳ'oJ��efe!�ԥKW<3�Oǧ>u+n��-5z�c�rE$:C!�*h��-3y�]�O�w��n�ԉJ��i���5/B�W����!н;2���� �K��fH���><�N��d<�^��e��B=YC��OY�1�7�!�l�ؾ���ˊ�D����!�'�bYw���x'�-�:���Z�<m��>	I����<Ƣ<�ڶK����#��&������#����SOؼe��qq|��ӻ��k_Gvf�>F��Mp�����,|Qc$�n�b=�0¡f�<�º
$�{Κ=	c�q�(� ���İ�a*h���KCk4�鹓�ɲι'���,̜C���`��n���+��'?�׿�|��[q��7���n��>�y��?¯�k�˗���= 瘬wVyb�zb��3]��#tBN�,"�*���\fG[�r�v���pK4�iH�f����.l,)��!ѕ`�iH�|jH��':���ceO��9��1�R��ߏEI��j���U;�|��MU{�f�E5�A��@l�^3�AZ[¼�$��ѩi�,3A��k���ÚիG��h5�GGD��n��>���o6���+8~�/�ܜ\\2w&O�����ȅ�G>�o䭭p_�¨��9;MM�>�GZ�A$�/ͺλcG��2��l �-��;�޵F�u]$/"�H!z['"њ�'"by����-"C��D�y
�>uL�:�������������������b���ٳ'|��EJD�>"�=Z���>���)ɿy"�>"��ݴ]���$"���GPS�4�9����夠���Pu&y��D
�vT�����13�3�1�Q�~�VV`CY!j�t����v��YIޑNڃ�]��+�>��'��.]�=!q<W����e�c�m��Q����Z rv?T��SXEE��{~�����"���������n8iB�g̶mp� j=%],��IxA3C ���
����S� س;�<++rdV�Q�Y���S��Df[�u̜���@Jv U�f"�oM�Z@DZܔG�a��~�.
A��n���W
A��㍌��."L�ęs|���m�-�c����d�e?�Tǣ���E{Pi�7
z����s�I�_��C��Ecq)Р��:����3�iy�<�p�V��$�]勻=z ��D�H-���n.�+��{�Q�,��"�j����ʬ�~4���f	���O­�:!����e�V��W_��>��#����G2P[������_y��eK����ªڻgoL����[��.)����wA�qbxe�cmЁxAõل���X9����Æ@�s�|��E�*��7ׄ B�n��ţ�bK���"Ģ�E"e���AD,o��~��b�,�w�/"'5���,��GI��80�zQB�-)��<����.�qBO��<�wNc=5���� 9�+��u���樜s �AD�ɘd�|�|g����p��3��l���9g!�r\�V��qf�����ٙ
�0��V�^�z��������ݕY�+>�Y(3+�a>ے#6f�N��+���0ȉ������E0v,zZ[�im��T�PC���`T֪8�Zƀ:�}XW��"��mo��h�V�Ǡ��#4��G�'MS��3����b�D-��Q#�Wq*9v�����Ï=rvoIxoI-o�J֬Y��lڴ	��q��w_y�Q(.-wC,y�e+��.X���g�qr��Q�s�]mmؼ~=?�Q1q�N8��c5w g#�� n�oD��N�'�ހ锷qɷ��E$��,��<��^6����C�%3!���}�m��CT!__�"y>�|k���g�g\|-�嘃f
9��fO���l
�'�<�H$��)�WWCЧ�@+c	�y���f�(H+gzrI)Μ8#cqla`�{S��p�;�S�Иl
.�iVD��8%�2m|Vx�M�W���J���S�I�ď�c�1��{��gpۭ���kw껷 �[P�ۺ��k�~�����#s��WNz��q�1�~�3w.S }��vd^~A�&����ʁ�.4N,�L_/:�lF3WЌ�y��(�}��R�0�41�&
)��Ýƌd�N3����S�aVAm{E�f6l�HG
/���8�>0��v� �P���Py�+33�#,[J�#d�1*�w��"QW���&mx�'������Ck��h}:�@^A�p���Ԙ$)�c�7ba�,���8O��b�Σ��U�嵅EX���C� �`�tt��hGA;�
pTU5f���3l�������?��':\'��K�!;������_x��ku�e53�������GeE�D�4Z��������c�>���\=w7oAK�FtruS1v<F�6b#뜾1�;�'�p`yMv�o�EA)���x�Z,ffln?(r��9ʹ�ht�ڥ}��K;�]Q�(x��_�@Ď�a���Y��z�P�D�B�0��kт���?=|�wl؀@?+�"#C��<e����ǲx�y��*����0��>݇77�-�`��o��Q��@S��.�OY;�Y����$�������2X�t)~q�/Q�iӥT�u��`�ى��榗.]z�C>�G}صT�F��������:���>��޽���DǦ�:O�E�n>WI�0��I���QP]�G����+-E8{�d%�<����${�v��'N�3c9��r���c�q13W�̶�����9C��n���Nv�
Ԣ��0W r�,ϓA� kP���ވ�0�^�Y�   IDAT(��v�-�8�Ҝ*�ț6%���)|��CzK+# {è��*�F�A:��뀬���X0n�*��['������t�G}xpZ��O�=p��4:ձ9���s& =7�C��jj�_Y9Jh�yK�!�v��?����0�v�;���d�����?q��wޅW9��_��}��PRV�$��{|/=�*XO/8�t�da`v�Ϗ��ܿn��vs&�L��Q�>����$��i�k!��0�F��zPn����1�����Ӟ�Po�k��~�|y��m̹��x+±��� ��\<oo�u8zzSh[���XF=���,�+)���*���p%�����܆���#M���6�S\ �1�Ȱ��>?X�3��:K�%q1Y��\p��� �#ö�-.����,N:�V>���ذ��#N��Sz��)V�	��?�}���E�^vN��q��߉�|��ҸU�'۝����`l�Rܨ���+21C�{�[�7����ISQ��8$�ٓ�+�i�K�u2<]�g�pg 6�C�n��Pe��i�
̔m�AW��-a^�hf03)8��it����с����`a�E�E���!���b�r�z@���
�2�f��7yɇ�c�[��\��R�vY	� F���#�&ND��CP��nhlހަ���FuR^y�{���0/�2�s/��Tcd"����[75�������ui�٤5W�
�����GpIC����
�ׇ��J��H���1ʥ���������W����]�N�� ̀�/?��OBS�����i���Y�0XTR�~�.�UB�嗀����Bgfp���L�'i�
h_�m��Љ+��u�8��M��Z�MU�uz�A0<
%�i�`f��a�Y��ـ4,�O����	�Ҽ]v Yǐ>S��������_��'?����m|��_�U��
������k��;�v;֬^��
�zS��T�iR�M��|cJy2��m��.%f��d�Y�Pv���Mgж��n���.!�#(��q�ВL(/Jb��јY^������xb�h�l�M���N����2�%��\��� */�cT������
��v��?�	��z��Vw弑��Я-_���������":ެY�q��g`����z�J�!U_��SςK���I����	�I#Ï�Mkע��I�v�t���A`p�tl&���Y0�I���3+���\�f�\@&�3�"((�D(�mf���|�!����I<��X���^�/�!����7��s��G?�w��]�?��OX�l9���l
o��;BA��L�֐Em�d��2.��!	o���ѣP|�B��9-�-�inE��S�֌T���Jg[vN`��:���EEX�Ӄ�7nDk�tM�>���ݰQ�g<̌"�	�L2x���|�x|��N���))�1U�HPW��/����}7^^��A�w����Ûk���ۖ����g<��3h�ޝY�W�SN9���Hr�-C�����|�j��`K��G�:H�Ѿ��[6��*�쏚C�WQ	8O�PyGA����U0�nf0ʏ�G��*���*xժU���p�]w�ŗ^D,�c�1�0a<F�����p�ո���{���p�����W�����./<d��-����0���!�Q��*g��+�i�IG?�5��Q�e�M ��QZ\���٨��|��M��q3��;�[V`欤�K0 �"|ku�b<r$���F3��|�{i���>A_U;ء��d��%h:�6�B��ȣ����d��1|� ��A�To/߈���O?}hss�����t�7��?��+V|�o���V�r�-f@�6u*N?�L�G�+��go�Jx/�������+4��Ǚ�W׬DK_/�8Q�=%{����s����y��r��Fu�����U=56���Ը	>� ��^�q�G���Ø�c��҆W-�
z618�O���7���駞�Oz���XǷ�^N����AU�fDś�0)��ࣄ��W=Љ���L	�^�7��/�����w�������W��f}ifi�m(�z��|Pu�nյ8��W�~]O?��~#��}���T�h3� 'c�A	y'�̵Q<5 j|������0��磌C�jߢE���W�]��<k��7��5o���wnji9���_}�t򣕚=e���31c��\�x-[��*�tM ��U/P�Ne��t����7���c�£Q��~JJ�2N{&ݘT�N����5'�֔�`�Y�&3x":���L��{�q�]�s�?�i��z��c��9x����Ǐ~���Cs���7XfƮ	��x<�8ucc#~��_⚫�����ص0��� �!N3�Y?�P���vV�������i���P=�eԞx"R���ljF_�V�ҡ)*#<��5���\)ֲ���\�L›8�[����Kښ�I^[u�P�&�	-!<��tҀ0&�@
���y�D`��#GcN�I�| �s�=���;�j�	�g?�&���	��t�xc��[v�O���R�iY9�� �<�l�M J��W����R
�
�\݁\����6�/[�-��'���㑘9� M 24ƓNMP��?�f�??���ƌ�����v����7��-<��hii���x<�����8��\�S Z%{��v~������u6�8|?�~����g���\�0�} (]q�i(�6=]��ܼ�*1޷17�X���1B2i�G�|L��qS&��}\��?�߀������8�d�����ރ���X���I�H8s��W��~��t����O;���z���Oa`�����w�úuk� 折��k�y8��c1rD��+Ծ��%���@��z��@�	pe��V�¯���P)�Q���b~dWEA_/S)�YO Ȯ��M&s��Q�r�a"{��I!?��\}f!-�C(33'6�Kd/�]]x�ɧP�c�������m�:��書��	��YXN��X����N�B@=����o$���������+�qT�켥�Z�Fȯ�������x�# �.�?�A:�j�?��Ao�$t��"��h�,���v����5�:ӴU�ŰgU�綒O�[k�hm���3���,�����yp1D�B�`��t{�B+@ $Y���58��u|������?����7��%tۖ�#_y��n�������uވ#q�ap��!���L�Ȭ�^^[���(�Ġ3��A> �Ѵ�k�a3�M���=�$�Ǎ��Bρ��f��oYI?aV6/���K��4����,,kf�
�Y�}��i�RD%����Wc��5��uII	?����v;6p����S騬Vɢ
J�܎g����m�Իj�J�_Re4�t�玲��f�e��y�^���1��k&WN��?d�Ly����t<����4ﯳa#ЙhUux��<p-�~t>F��p,7��'M��1�����M��X�湭�*�J��At6_T�ꐓ>�1��G���L����8��s������׋\�P��|�=�~~�F�����+w�u�.YB��鹿�q��G`̘��=9_����`\oJ �+蠚0�����A�J�0�w�x�,xR��	�-�m*��5M�oC�����~w���|[f���g�B_�������	�=�8�����}fAeE���	a&
�\Eo�����������vi0�`�p��Π��]��,��@�����f^w�)�N �t�<��{�06k:J;6m�[����3�Y,��-j��սr<���c6A<���}�jq����&�x{kn�.�'1|�֩kz���"�a�풑���2ɐ2O�wQ��y�+����aUWG/ߢ������?���»�7��,��,���zhSS�	r~�����;��F��aØ�c��ȅ�c�=����	�^Y[�
��c�y��4��   IDAT>����az�_7i
F��4��{�5�u�y ���4���d�if,� c	�|������9/��2a��_
�K���4�ǰf�,Z�
���z>�/��a`{
��U����Tom�Ŗ-|PR.=AQ�|2�DB�￨�@�_�xa����p:FE�u���79���}0tnjD�?��2�+�N�E��6��=f���X:�(?���&7����L
��c���-�c1�-8c�^&�:�)fꚃt0f�������
��ª*�QV�b�S��n��v,^���Ü�]����u�zjii9P�x���g(744\����`*��5��w�"���d�x��p��cq�!a��:x�>W~K�{��� �tBr�4ߐ��@#_���rţ�`�1�!���h�c�k6B~y��]$"��*5A�m�q�Rذqx�hg��\�
6�g:��uFeE�A;�[�s�ް~=��[���pBc�$�:��S�Aah}�g(��C�~e�U.!>�:�03XV!6���AѸ	�ڲ	����&�m�~��1�*���T���}�bB?�?f�<�ю;��nL�AӬ/�@{�*+�:,�R\x��Yp^�_9�8Ï���ۏ��C*+11Y�L_
�W,�o~�hlj>��7��*�(��������6\����(Wn�����ďN7�I��se��݃|w����d43��T�ލ�sX����n�{��+Ka}�0r�N"��!�>u3���z6TϞ����tl9�������	����\TW�y�ǚ�Bl���{[:[��/o֩�m�҂��.�e��]�m��m��V�ɖ���n��@�m0C+0�T�ˠ��w��\l�<3s}5���嘅v�
���f��33W�IJ���t@[���x޾(}�qH!�Ε��t�d��� �Шo�76�An�ko�2~�;y�x�(+G=�q��nA�1x��!mw���9v���hS��08#a;A�X,�fr��z>?V���
Q��ށ_^/Ztٮ�o�`���oI�-mmGj�\�iӥ�����tv���۫`|m~��8Qq��=�$z�al▄g����'��3�"YZLg�s��z3��+��A\!�B�W�#ýg}��ւ≓1b�a��˻&�&N����Y����s�Mh��	�h���O]l�����j��V%��9�K�(�
ճ������a�#�[
�ޤqH.<�93Ѷy%2-@o��w=Mg�\!{�RR��SW�=�+P�ǰ\?�Utwo//��(��v1������m�����J},
���9?4NsJKpDu%�',�����M7c��UWS��|�=��}�%wb1��{ss�6m:�mYtt��U�M���g��CM⡐��qѰi��׿�K���㊶����nԎ��)z[���ů X�
Tr�\h�!aӊU����a����B��G�X�~T�g:��;�-����$Q�`Di���t3��~D�ᨙ��&��7lĊ+��-	��:�´)Ϩ�T}�!�P�ᄏ'�1�!��?lyeDp���b?d���:�dk�TsJf6�ب�X�,�%��f�Oˏ�!��eg��V�V�o��ow� ��!�5Oޟdm0��k�isZ�E	9r$����������=� �b0�B��;���[ƫ��3��]H��<��s X)J�0؝�b�(/8?)����?�ľ��J����*@��[)��w<���}�-~��K]������(�C4CGp`:���宿ߍ�{�6mD��UU�8����^{"��5M����g���@W�O�a�?^��0 �ڻ�v�Z�vw�b��:�PϜ3/��BV�+�*?�C$̌�C��DfC盅r3sz��b�7���=�jk��v�p�	��s���d����p�C���q,ŏd`���М�.f��B�C\̆ϗ݁E�
��
��wZZ�
���9
���A�{��u3z��zS�/�E]�����N1yYs b}�WV��j�q.��ݯ8Zz;P��x�s�M�Q�� �90�/��7��|���8�c7%�!F;�6����E�3�^�]����u�zE�e�)����Cܔ�k�&-��ìʴ2 �"�Фˁ��&�f6��7��oǊ�+� ����N��3N?�t ��v�a-[`K���ճ1��uF���\�4q�u�A�C�5��C���C?�aF;Y�TL�|��à_mP��,r�}�}KO��]f!U�j������\x��V�K_��k��|��lD�fJ7����I�'���_5���٢�$9�����m��og(~�r�%g��D�q**�L"6i
��u:���-[��^?���_�rJ�r��rS�U�q%���}�c��*�ɭ�N����x�i3ڥò.8ӀE�1��Jb%W� �����0Ѓu�%�avI)��(C��3l��?��~���_`�]�� �bK�I���+���?���}Go_ߍ
�2o�3(�@�p��p蝋�g�	M�������=���ܒkUv��;��ܺ`!x|x���"xm�0nW����d�t�
����_{[�%�|�4�-8%��<v�����*/�F �ճ���X�?�b�_��=	�.)��[��v��͌�ӏH+�W�C=�2� >{���T�+਻ w���_7s𨩮��Y3�]�03�<�>:to�A���E��`�m,���lЏ7jVR��NCќ9���Bws3�>�E�-�>��� �+ q�i�P>��i������X��Z;�;��n�$��殼�F�j�9>��N�!�^h����oF�T7��#q�X���w���=�YYم�o��߸vSS�	��A�no�d�8�7��Bd��|7�$	¨,/���*�H���1W�Z�_��F�O[*;�c�=�ĩ����@G5B����+��gߠI�@k��Ӌ�5k���0�9����qU�����Zy;*�;~�d�~��TS����"҉�Q��Rmg�ޗ�y�{��0w�l$�?� -�>W�f�<���-����!T��D���Ɍ3Q�N셜�y�)m岭{V~T\�p�tD�X�V ��G��Oڄ���@#.�1����q�Qs��H��B;?��;��<�,T�,E��ң_˷%�hg4�f��*���n���sm�hF����>�\��}��k5��p��� � �ˁu��@�PK�?�y�gy%N��2����{�E����_I�]�� {p�߀�V�������v��U��fr�B��$?+�ݻ��%*�W�����?"�Õ�tG��}������M�b�pa�2���|�>� ���D�Z�c�7�`���h�CWW�Ĩw��Y�hVvH@]9����4ެ�ʹ5T�d?��|3�Y��bfN�MHNP�z���|'�L����^�����ԣnTF4�� ��� Zq��gf��N9�L�4	�z��=/[�mc��/����m�fQY͂6i�'m��Ȅnۀa��Q�)'�h�4������	tC� >�@;<�DtIG��#|�Ǭ�*�8v,tt�r_KV��$�K��� N�ծ~����>�%�S#�N����4�y��b8�{�i�c���-x��p�}��]���o�wLU�����ιޛ���[�����C�D@��J��_F��@����x��8���a\I��/��'���Ff�r`c#��|�����L��እ��M]�H��g���өK�N����W,�Lb��N9n�|]��t?O��O�-�s?�8ꨅP�?~<�7N8ƹv���AYP���|��7��Gyy9ο�b~�a�����,��k��,������{�F�� n���K1�}m�Ơ���M��ζ�[� � �*|R�+ؿ�<���&f���#�UqJ+d��.9|�h,��@�����\g:>8����C���V��s��������8@۪-C�����C�_Z����G[R}u���?��a�EJ���� Gy�wTk˖-�pE���M� ��c��!'I4��[I�3>��۰i�{��]�   IDAT�A�^���� �UL�<�zv�kw*�y)LÐ��s�v=��~A���S�Y:���ڸ��#ż�c�a�i'"1�������]�����A�p��8�]���<�f6���}[����/��*J��s�=\p>�N��T_�+�^vQƍ���QZPp�O�0bD�<�]����yc��+��T���,�y���f�4R�-!Jo/U��a8;��PSn��19�ɥ&�,yǱH����7�������� �w�1M8đq+c�Y1�/)ǅS�����B�}��K:;�q�C�p0�'kB�� <�0�L�!�2�@��}��C8�����5�oFS�������ͻ~�����'Gg{U�O����X�DFww�-i��=�Y�3^$
T��if0ˇ��݄^����C����u��/8�� ��JY9�V [Z 9c�w�������nlijBs{;J�j1��w�d�TxE	*DޙM��Y6)[�*�Я��B�r!�e�Û���hnMG7�P5JI�$�B�6��O;�T\��Kq��(Ҝ�}��)"-0-��qmcϽ���矏K.�3�vRTT3���H[;�ak:o߼!�M7���o�8�t0�@~XG��{��mvX��r��HA
��i����CY,�G��ee(��I���m����e5>�c�Y��p�4^x83����P+�V���G��"fb�����|K�bf=<7�rV�X�Z��:_��j\^oقrt�C�����3|Rszs y�hbF@AکPԯ�q/�����y �"��鯩���xu�b��3���Sp���b��9.�ш�6ٖͰ��a]]�*�|�R'�y��I��F4niB/m���ƞw��J�yΖtY ���vȇ��7p��;b��¶�F�B;���D#��4��]qlt�9�3�g��9看���2�����<�;���>Wrf,�����7v,�͛��O=����袋����h0�|�c&��Ֆ�3�?Ǻ����M.�l�nT�=g��m��D򐃑2���>�P�Y�ʇ]�fp6�=�y��hw�<�++�)��8*��nA<�Ҍŭ-�=�V��.تD d5
ޑ�{=�9��pi���m��[�P��jP^�R�lkkÓO=�{x�����/e�]�6z��F�ve���;::��캱����W:�hZTI�TJ�&I��k�iftB����^����kK��g�CgG;<χ�	�p�1�g��QU]E�	X����-z^c#��Z+����l�^̐��DcC=���(=�9
I~`�d�C;�Y�� ѭA�sd��SEd�0���>;��fo��jf�z�Q�#fF�Щ'�����
�����=�3N�	'��o ����G���v�����{f͚M꿰��kf�(�8Կ�C��uhB�Lm�oD��{(l��������5`�ubS&������_��؀��k,n1�����e]�Q�D�a3���"�ǉ'aw.4��_�*�~�%���M���惱:�,�r�R�v�s�	A<Aup=�V8�r�'�L���|��9�oF㹪�*�����`�ʵ?�6hgK灮�ː=�6d��
������v�>iL�4l�!p�����Y?�4��e�G�~�_��W�x�+NW�r~�8��c1v�h���{z�瞇��H�`y!O{��v6mAS�f��5ӧ����t�cWI_��rF������(q�hHI��#����J���Ɇ��Q��:��%ś�z�a�#�k����4i�u���<���}1��
�����U��
���p��|�������>w�U8����ns�,NB�`f���,l����9��|��UqX^c�#B}v��χ�7�*���<�# - }���h�\�u$�Ï��@7}�����Y`Y���7=�<�a�l�{��L���Q#FaRq	Vr{�Ѷf�&<��в���=8�-���P=!(sAڙ���:3D�s��6ک�����!>�щ��E�����>��y�ic�-]��G[[[Ůc���)�.�~B���������j�����y*!�]�PȊ��:<#u���{q4�c�k�_���� ��E�m��0g�l�0 ��:�V�==�l�x�>��� څz�;6�ۀF��1����/{�مgyT�LC@�p~L��@����|!f[CX�Y���+E!Sp5����X�=Tށ�n���c��0x�q��+7	=��=z&����Ƣ�o3>F��&7.�(3Z�<lՇ���u� �"�P2��L )�zPm�:��ɭ��h����FgVlF���_ؑ�h�ñ�Q|<���OF���H5��)�������.2d��P�6&�9i2���u�K���׍���cQ�t��%+���xj�'�p���zi�3w�'6������.�^��7lDw[F��QBWO'���\��e����7l��	��DVe�����;L�{zzo��s�9�	����
.1�e[��b�Z�'w�D"�UkWcC���"�JII1�;�TT�#Cg
�A���e+���@-E�YN(���|�7�������OC�>{¸�v�p��ƊU`ys�Z�#��V;��(-�/��ygX�SopV���a�=l� �\=߃������̠C���|��د>u=���A�dET�]t/�䭺�[�v�Ù��{>b�'�����q�]������.p*��������og��uF&���vv/-�F�;[Z���	}�L4G�ѣ+Ye8Ȳ�~J$����㷾�/�[�Ǘ-�+V╆Mh�� �D�l�h�'q�W^�&.��zX���_���x�> *X+��O;���z�] _?>��-03�� 8�Q��]${�&pe��%Cg�*mժUh�Ԁ�ӣ3��=z�!(-/C�Uj��U�ݍ@��T�2tI��������|�����䔉��"MK��B:��� ��k"Mˑ*7 X1�L�;ȧ�N>(p���:��'��������a��*Y��C�M��ٜ��\^T��g>��`Fa�4�8����e���ۏ!
�x��A�2R(R{#[a�G�[�*W�1�>�톚Av�W��'f�J.���о�F�?��~43���Ԡ���P<c7t*�nnz� �B��^p>"�`��5��zPu�g=���a�Z��|,��oׯG{�y�<mg��,���2�9��>2��t[�
^ԸOr���uX�m����n�=�Q�ۭ�nr���QYw�`��\����A~�a��?��=�[���--75oj|�����ګv��/��؁�Ok08�*G53@ H, <��HO|$/D���(T}H@ i���� :>ƕ��Q�1y����8dTt��E�+a��tGeK�Ge����Ω�<�8�$)�.�>@=ݍn��`0�p��L��TPA����خ��Z��`0� tl���
����f�`֠�,�Bjf�P^3���S?����t/���fBu�'���x��)����݁�dK�qJҕ c)%�1�&OA�Yg �7Ş��H���R��""B��rBn} 4o�Te���p��س�
�Խ��q%�ù�A�#�>�r�-����z�g݂E���B=�2?X�jm��vtqې����`36:h��\BV�h�!4�6ccC:;��s�J��Xئt_
�����imi�e���W666^��~�3�/r��k�o���s��v*`�`����,T�&��p�8d�P�5�9���#�f7W�76�����+@������/U�[S��Js��2��]!u�r^:��2�Oѡz�?�技���_��f������k8���)6�ȗ1�wf��
{&O.Vw<� Ux"B~��#J��JG�����\�f!���LHò��������]������E��j��Q�?�����S����F�u��ƨ��Evp@�H��<+)A��㐘9=�����p����F*x�>aZ|�v��w����#F@����|hs&�5   IDATZ�� ͙��0C��J�1 wbuK3^kj���MX���֟�M1����8�rq� � ��NZE'�ڒ��Uw�G��`fJf�ě�c��:�����~cgG�=ܳ�����_�?��X�o��L_��faG�7!0� �y9�x�S�`�(�D�B�l���9v=��s���ѡ@J��CyE%�Χ;ppU?a*� m]�?���
|�Ӗ�W�q�࣏N׺��}ڳfyOOx���${�4ζҬ�Ӓ'g��<��,]61��8�+]��i������
E��qұↄ�"'ߔ��̨±LEg~�i�"�a��6����q�~�KF�At��+[XW�1�,���ދP��#�ҽ0D�Y���}�͚����������L;�Z{�zeS�ȋj��~��#ޖT���_7��{��wniº�NN��CGo�۰���e~�{�[�l����Vt�MS����lX��B�
(ȝJ���SJ����������u�Q��4
�f�J��:�°��jn�\���r���755�� �/�?=��/nm�SG���p�`2x0�kx�2(�)�����LS���R�,���9y�`k��1����
����Զ��ye�
�h�����/� ����'�S\98>�}<��d���Ѳt	6>�$~��]"x�w����NG��W�\��큠(w<�9�(��fa[uE���3{�ND^�~h�4�R�`P�	3e�PN
��ǁ��I��!I�-07�q����@w�eF��f�`�������y�\vޅ��-3�3�	aj�k�_u����RU%����)- �~`���G���:�Ǝ`���B�G>}ZE�r(���sg.2 �GA��u _��i����~D]-�Ovu㹶f�w��a�,Z����O�^��������Z�d5I��1�{�	��ρb^�t��ɒ�l1�^�> ���v3���B0 [��B�(���=f�[ˠ���궖��6n����e����=u��@{?�t���{�q6���W|��ŔNㅫg��A��t� H��� �^Yki���D��*��h㇓��<��{���ɉAO�YV �]����:���S�9�0L�!`:L�:w��Vz��o�@E�Oַl�T�PY�^�j�@I�R�����N�fZ�J��5u�&Q��#�P�R��-�6�/KW���ѯ	�|��
9ɀ�3_A6�m&��u(�j�g���̥�hz{z�2h{ь9��@�E�!���B����꾖���k�~V{���_��=�����5C险�
s���QH(�$'"c�f� 	a0#0�ay2�_���٬ ���GY ��{�s�(F���o�ـ�@m��!*Y@�E:��c�� �l|u1���O����Ϣ�LA:NW��Ra�]��[ �W,ƕ�q�΁�r�g�W�a��'DN�JJGT���PP�F�N��u�}���öi��"��j�:�0�FQ��4�9�]X� -�J�nN-�ƪ8N���2��@�$@���`f�ۓP3seI�i��5u���T�8`���� �j�y`|�+�s.bcG!�7���0/ ��� �3��8���ed�Ne�4�**0��1�}����;��yQ����T�4b�7rHB"�0/��+b=�N�]j��A�ʌ�m2%`pg�u��gdy��_�����7sU]__�a�����\�V���T�	n�4�$A�.��'7i �	d�x1�{�Q����Ag�h@=�N:tP^�@�U�!W���]@�0/�"�H&O����uHu�cœ����}	�wމԖM�*�6�-�#��0h�y����Iޫ��	� �<��7 s3%0��"��+��|��A{�QnP6��4�le�8�>s}�te�ᎀWBzB�'�!̎��>�rGXTy��(���IA�������<��h[�$�=B�)+�l� "�H(^���T����X�?��b��#JcJ��S�=^Uˠ
�!\ߠ��q�5��Y�@mt��D1��T#A_n�l�~/K��@�cxZdt
a.����,`@nN��d��1������3��a3�,�>��	���}�8��v����6�W��S��?�������N�H��N���bf�`���`� L�yrDII���1�h==ݯis�����)8s���#�(H�W���	f�G�����1����+��;_�#��я��?G�~��?݌�[��������:�=�=��g�A�K/"�x1�˖"�j2�#��op/�(��N?��ȸ�p�Q���Ns�`���Mf�ˇ�"�p���P�p�\�#F���8dr}�or�6�*�d:�G���4
Ӵ����r��`߻:i_�I/���rS^���
���6��8��uj�m�B+����ؿԇ�|���yJl����l���T9a�Vp�� ��i0���ˢ*�t�	w�>�
Կ�)+�gnU��l�6*w���+S��.5G�c����x���d"�������������a(Kld>���5���fWg��\�ݲaC�e�l�Z}����Iv?��1��6�!���,2tJ�x9�Q9L�N�
�c^Y87<f�ᡁ�(+G�Z�OW�`/��ƍ�p�ɉ/'T -J8	���k&�I��Ɓ����JK0j�x̝5�ǌ������D��Æo}��m��η��XK~�w��u���^�?X��`=���뮻��S�gXw�ϰ�����?G��~�M��=��'l��V�pu�z߽h�!t>�8��}=�_A�kKзbRkV!ͯ陆����z���hm��Go7��lc��ea�1X;�פuB��eARp�՟�!�0p<(��0�:M���d�!�f�0�!U�NA��<�������=Di�Y���������|+�ZI�28D2�P�z���Q����rM��D�LQ�kV��"��!"��l���.8�)^�¸ þ�m���R�����U���*O�c��ҌLG@|��<�q���n�j,�~+	~���I�GE��&�s3o<p�;T7�l�;�l�%[�h�GeQ�J>�T�Q>k�~��M��qqU��b�ԠL���AY(P��c�h��~^�<HQ��t�����^tu�]���r��>�ZZN���W��v�0�_�Q�0(cH�4��2��f3���y:�G�GYY�2�V�k4��)����,���A#�Y,��?e
2�(�.�a	UŉAAG3D��C��u�a���sv���8	��oc�5�^�}�.C��/���Ǳ������۰�?��7�g`�%�~�:�������_Ǌ�}˯�,��SX�Wb�'?�՟��\��X��/b�W��uW���7��h`�����Ɵc�o~����=6�|6��Gl��?��ֿ���;�|�=h}�!�=�(�{�O>����Eǳϣ󅗸��݋���%�]�}˖�o�*�V�Az-�eC=��͛�m\Ku�ݝ ||=r����I�Y��D@�����q�&/����B����A�8�єc��΀4󢺆�　�`$�i@Ywo����R:Q^�L�䢃�����ԕa�>��H���8�Ϡw�J���`\t��V�G�)�:��-��� m9�ٺe_A�&�D1���-�k&�������%X[hQو �B�e��Ӏ֬m�m��ʽ�ێƺ�4@�i��T�0�-'��5)������Y�]eH�TG{�wZ��nm����m���ԗy�34[ZZ�4s��[$���>bw��!�b��"�[��P��\�i�:�����\�V��&�GeU�K�:P^|�����y�.��_���cL�����P٠�� �I+�=�y1�i�f�4L8`�.<3�9
s�ݎ^���=.�^������8s���{s����cʔ٘<a&���q��ad�HԔU��/BQW/�M\�/_����g�r��h��X��?a���U?�˾�#������/|�|�*��+��>��?�!<���w_���:���}!�0��{�K��,���X��a�9�   IDATWb�g���/|���4~����~�O��_݈v�N��߉އD��O���zeR�_��}2�\�7oF���+�6d:;�C���O��@�L��s�� �5a 32��Ʊ��7��Ai0�� Yϊ�(`�Upu���tz7�|���U>�4`����F�i���o@�%\Y~�XG��|*���ۨv��&���o��ưC�4�qy ����k�ߞN�,~Ak+�\��?��~t[]�À}��TF��48S���K2�'���mc��c;��r��)!��N��+� 1*j����V�������k��P���T��<�ޯ(�Q��#D2�9����b�T�j�p��h�h��i����/���ݨ�R���8�3��h$�O@-?�y�O����݃���/��|�֓�g0�y��?��|���!� �΃t �78���n�����<dh�9��ўOx�K�U����%#�Q>v*'�E��	9g*��1�����1h83��;��8s��GI,�nG�=���}��9�H�s����؇���`�}�c�����w�n��`��i�:z&T�`4��j��bK��oDl�*`ѫ�ϡ��G��r7W�E��nºnĪ^����^���X��/��E��!,��}X�.���¢�O���'`т��㱘���O�ғ���w��U�k��X�яb��>��_�<��-����G�7����C;�w�������cH-z���lZ�%U���z�A>��@ n�|@�H�d6��@�c��Ge�1R�N��9��i�@�`:,XN�;��� �I"kɝJN���M``f�`�� �	y�	�et�=��t}������ E�5���π�1�Um��?%ϓ�~`��'�Xߙ�=q�Q4�JN��#^U	1jD��w��H���(Ja�ȑ�(/w�R�r2�������M������^�z��7o�|ƛ^�4���.�Xl�`ŀ�oC��R�C���ށF9xf��V�2��2y�d��ʘ������O>�%K^��Ï��	�� ���{�WZ��98A���Go�۵��|���]����E%sy�t�e���iWS�@�hۧ�G�T�i�g���>�QG�8�x	Q�D��E�H�T 9�
%�kQ:n�&�AŔq��1ճ��v���kF�;F����:���ӈ����Ì�1�`��}1c�y�>ooL�sL���̚�IӦc��)=v<F����jT���<�@)ۜ��B�9���Y��|K�z�Y�sK��.���+6���������}�}�,���������]��.�0^�����y��˧���O<��;��;	K�q2^;�t,;�,�8��X������a��>����46~�+h�ַܪ�冟��7�B�oB��nC�}w���G���SH��ҋ_Fz�Rd֯��YnG��]]��-�1�xi���y�0��3��1�A/���)�B�|Y�V�
9``�+�O�+p烤���/�<��Es����^j���h��`����F����3���F��v3��$��!q,ۤ@-ȵHpD� dxf���! k&�e/�ճOM3-�5`��! &N���\\%���O_1��#ݤ�2-!o\i��$w�%/�)�M#*5$�u������>�펛6l� z�dox�ۈ�����NVG9���a]��N��n�2�`&�Zuh��U-ǁ,ݛ�K��C��(�ɓ'���Zb��Ҳw�u6l��}��q���R��"�3��$�	3뉠:A���FyL�|R���*Qy���8HG����\�n�:�9[N�Lh�͂ǋy݇���8�=�{�~2�xq⼏xi	�e��W�!QY�d�P���
��T����~DJGբl�����q�P9a�'�C͔	��6�3&�v�T�͞���31r����l��cF�N�6c���:�A}���5nFq?�n�V�ati%F�b��@m�CuoU]}�j�B��v�p[G+��Uk[���d�W�z�I�<�0���w݉~@�r�-h����7�������c����� +��_y��������/~˯�"���X�����{�+��4V�?�9����XK�_����o��uh��h������[�z�mh��.t<p:e;�z]�����л�5��^�T=P�@�������Vc�y03�xz e��!� ���+�c�" @H��;ŷ�"��ch����V��߽�kk >�a���X?@���� 5��K�a��}���1.G�S�.T�MQ�e���Z�8��>���t{�����"� =c�t�5�S�G�M�nN^iOs�-�B!�<�'ed;�I�'� ���O�af03W6�cWW������M��ٶ���1h�����ЉD�������3��2v���l2��a�s��h`�/*����e�e�m�̜1;��D��w݁'�|��
��W6��;9"�Na�> `���F�(Q��OH���C��8L�FR۝�^X?ԣ�x8�ƴĠ�0��
�;p��lf����lCD�ɘ)�u| (_[3�E����Q�i��>�o^<�+�XQ|��Ee%(��+YU�zqmJ�G֡��l�(T��ʉc�q��<
�5S&�v�d�`��$FO��1Ӧb,���Θ��3�c���t��9c�g��h�QL�b�ȩS1��~?�֍�MVWV�����*؉e�}(i�D����]o�*��אy���~}�=��C׽��{�q۝h�ʾ��?��w�G�~��_�ȭ�_��?æ��?�16����x��Q�?�b�����=����o��W}�[Xu�7���k����\s�]�M��深����z���������96����/���'4��������z'�s��=��'G�3O�����>��%��_���믯���b��L��ի���#h��o�����[oG�>� �2̠Id@.'T����J��O~͒�E�"��W�*W��6Ux��^ oT���9���� 3�4�FUu�k�]S5G���]!�X@m])��c� �2B4�!:�D6�m��[=�~����ۆ��1X��������J����moI��zU�QBݞ�ܠp(���0���#�(U1g�n���`�\{<N�e|�����?η�.��tT@מ���4�=v�!����ӭ�� ����������'�\�U�C����4��7%�'�W3F"P�03�� ry�Mg��0��҂�X/ۤ�- �W:�_,�{@�ǻ���!��Y��s`:���0�vy�7�7x|���cEqĊ��(M"Q�`_Q�"�⋫+Q\W�b��Q#P�@_�@_6a,�'�G�䉨dp�b0��95��u�#f��(�ѤcIC�ĸY30�z�X>��cYv����0��QS�`�ĉ1n<F��o����Deq1��J�����EM���7�_���
��%�<�R�X�����at�y?��z���W����h�9��O~��\������.��&���~5��u4|���ױ�נ�A|#���k��V���l`��p�����P���^������`����p�h��/���$nĦ����������{�CH���t�h�l>�����p�@?yG9��"<�t�tG�3$6��z��,@1 ��1R5
@9�By�B~�����Ź�~q@�R���2�?�y�h�@�Z<Es;p�]�D^r���腎�I�5w�yB�/����̢�`l��J�ͺ����Ύ�G�l�����簅�q-�*����T���y�f��~ w�.�Bԟ��
��)B�'0=�=7n��k�;�dB�wq���+�.]
g���q���$���8j!2��z���^���A�@��Wl�����F��`��;dӒ	LҠ��J"`/
�"e=�v��Jg`E�`g(�K{���KYBl����
�FH�/ u��A/Hq����х�Tc�D�   IDAT��
u��|0��W�Ϡ�%�����$�KP��b�x��KF�re?��F��+�*��MF݌�1k:FΞ��|C��Q���{쎱��I��0���������Ą���0gL�M��g��D~��8u&L���a��);f"F��U#PWV��d)��*��\y�����[k�U���"�^}������Sܾy��>����-�[��gl�*{�/à�sl��u��.W����5��+�W��~�����0���m��ݑ9gu����@���k�����](�����6t��DA�Ε=��9 ������6E�P�f�*,�8o ]��f>&O����:twu��q3Z[[���"��ۡy������6h�x�Cs<�iJ����aNWq.����!\���8���`���A��;�������1?v.�S<yf���N%͌�) f�H	Jx5{P�
�lJ���eHŇ\�Maw٣l9X)���,n����	W(|-�jø�
h_��K ��wp��H����;T+��(���H�1ic h��<R#\��`��C�tT� ȧf�Gy	(
(�;�H�xɁ�L�oU}�r��RB^�Ԥ�B"Â[�'@}!h�S΢a{hoX��V`,c,�(m8^������ ����B������=�c�|���u���IAzS�����8^nlx��~�b?�!�@,G����~��Ɋ2W������5(S��	���3u�'b?ʎ�m:F�5c�����	�ä����CƔC�a�!�a:1�C1��C0}��0c����ρ������~��1wf��3f�3��+���:mwL�:������S1~�$L�4�f�i��ø��G�̩�ʒ� ���E
�`�P�Np�p�$��(����--.@ˣ��O��?�
��?I�\�9P��A� 2��5/i�Ft�}TA�s���Cm]�۹�޴y36n܈ͤ��i��"���� ��,�.Ŧ�r,�F��<��0{�@����^=Dnill��	��z�1b���ąw����z,_��F���@��ޞn��^�1���|�����ZSSn��f|��Wa�ڵ��Ї�uR�IӉ����N:�� }��諬E��/0 �&�9���3p"
4�E��Q_�>�e��[>�/��̣���|:���%���n^��,����R�6�ux2Ux2 ��,��5�qH��À�d���?(�8���U97�svȸ��"�s�7`�ϰ���a$s�2�2%	dJ���bXE	��>?��jʸ%Q���J��B1?֖��C���(�0�۟2�[>Q=mjgNAͬ)��>	e���`9+���Xs�����;����M��;����Lj[���O73@�^�u�*��q&�8]�r�T[�^��"nF?�9�����P\\���R<d����إ��p�#���Vlܰ��6A�:ò4Ö��2���<���n|�fZc�n���x�L�]�i��QpH�g.[|
C�Y`V�8ҁ<��Z���e�=� ��03x\������V�{Ͻ��O��[��t|:H,�����8˒���:�v*2��{�;�3w.z+*��p����Y2i��BV��t�4 .IC^�?�g��1~�f}A��C�	FJ��4K��Y�/T��U7���	X�˗N.o@9��ᢒeU�����ppv��o;ǳ�F�4�)�<	�v��*-D2�lZ��gBY���j욀�R��j݁e�AyD@ \E�Ce"j;��v�p���s	�ࡲt[�3T���u��J�~�y9�alLS�c�<��;�U<��0"�3���./���#��������f�R���я;�ƱtK�u�����d�Z�I�%l>��rِ�S��%���2����p�=�z�S�K�{̘�8��������YC��0��������&.��������6��aA�NI"�@T��v3��!:TDpi1�K�_�4�]�]�ojz�~���o͎s���7'�qi�;���Rؙ���'�%`��Hw�eS4���![��tyy%�>��w�9��E�Nc �6nn�}�ދ��������N�ol��u� ~����a���q5�q&��:������@wm-z|�O�^��{2tx.�� -'���t���	���� �o ���91�f�+��ԥ��J��	D�L`:�SCi�@0�Y�9�t�"]рiA|,k��&��:M��T%T��O�SN͕'Q�F�@*���Fm+����f�@>��$�'�g/�hB&�	���xen>,��e"�M��yQ����l[ �V*��)b�
($lF(7h���㶆�`cg��B#X���fki�����$9W��ے\|����f���]��u�s��A���S��ѣq�!�Ϟ{�ÿ�3�*���'h.+0���������=0�	�3� L#w���Kd�AA�����+Ћ*���ڂ(�E��HW[�o[Z�ޒ��!wT��Q�6���8�;=2���o/��͘2�$���&���fL�����:F��睇c�>5յ�`K�`��������o~�[|�_ѯ�����o��+�/EK���� �%�ǍG�����w�1�N<v�I0�����#=i"R#��VV��{kA,0��1,F��B���<B����0���e)��9�@�<dX&�@�r!��N���B�!���89듍�tN��6����A��ID�jd
��o���<�#�60�F��k���# o�<�}1�Ү,�9P���@�'8�*�4�����K�W]Ȳ~2����i:� 
�!���]S_/�߲�6mF_��x.>�a�΄ޯ��<�Q�r�;, Ғ���:�g�xR�i��m�fT�Tc������q��i>�|e>���,��33��B�K������n��� �CA����r`:*c0��F��0K�1�W{{׭oŏ��EX�;k�+i��B�v��Jݧ��\�
�3x�� i&$ @="�s��xי��~�磢�)�@[	ni�\M�?n��g���ˏ�?¯�k��Oĝwށ��O>�8��9���5,om���r4Μ�-��Gˁ�u��Ѻ�>h�3mS��}�X����WQ�tI12���"��R��D��q������q�m�m�h�$�I%�[)���'J��v�2��|��D#0��2��3�<�1#D	eh���4�d#��\L
�Y�C� $�b���2ڥO�V� � ^f��#�v�2���O�mȁ:� /���b�y�$y�Y8�KA9�A�tFd`hn��c6�L���N%�ի|Q�9� Ȏd���,_H��n���vn�mj�}g��"b"l��(�fؘ�4�-�:�� ��1X��?�7�'�)lf�c;J���z衘8i@�0w�l�
��̘£z���v�z����MM�G�9=2J�@��ǉF���x? ���I#%t�p���7�z�)Z-T�.**Z�3`(-DS|!x�Y�����t�˲��<�e��9X̠�gV�[)�/��_x�8�pTWWg��my��
c;�;:�ҢŸ閿�K_�>�я�C������+����y\����}�_�c��+������3���u������Ex���Ѹ��,���=x����u���n,%�se��XM����z���>4p�d3z_?��-D+�X��C'ѝE�������f((k�,��(>
��q|�sA��e�00��휇�G�S����h��l,'�KK���a��<�`�)V���PK�Jf�  ��(pg��+�<IzH@q�2�܊��c!�]~NW^�p�/Ȧ3��zB���|�L�LV�|�o����~�2�� ]e������N��xJ�	)n�����?�i��*1��M���դ���-,MY Mǐ\v��p�&����ѻY�A�u7ч���Ŝ{ss�;ށ��[	   IDAT}��h��
�J�� �=��ў�1�� �~��a3f��E0�2�A�)LL����@���'[���dV�-٣���F��ԭ/[כB����-++��U�2�E��f��0��C��!̌� ��L�
�i���fF)!ʠ��������c��g�q:JJK����� �?�cp��mE�+[�!�X��^^��z���6��
�z|���]���ŗ^�.�����%8�×��|�_�m�r�8�׿Ù7�	���V\x����ow������W�� �������{�=�~��3��3��O�=�[_~���*]�ϭY�W���ZCVnތ�[���چ�N�ut������C��(f�'����y1x~�]�x~���E�"�)bԋs��=1/F��=��3�CF��,��3��B������Fp2�Ni� �<G� j��8�|�|�!A�@^��@�m�J�0T	�{ �S	�J��`嬛���0�`VN�4�S��̲����gьk���pL�@^�5N���O^�����p���qQ �>/{p�Gfno=v
(@Yg	��7�ǅ�t��Ε#��-�s�>����j3,�P�\y3�'�n���s��7�!��3cY��=����L;�����P���;�2��';��Ov��ޛmY�̢��())9����pD�@��U�쩳��q���:�M��~�2|������p�R�P�v��i�3x��TN��|ĸʎ��( ���"��}�*�~��tm�B�����X�ڊW���|S#ol�Cpw�zܺn-nZ��X�?��7����,~W-Z�O��.�Y��[,�~����q�cN��>�x�=8��w�d~�<�p�������n\r�=����p�}���U?�k��䓸���kڻ����%K�в�x�u?�f5^Z�K�PZ�i3��P�6o��D���{ҫ���"`��H�{��KKm�PϨ�G`�wD3�� We���;3Mm��4��� !�_6�N?�,hG���'�^�0�P>��^�m2my`}�(M�@//Mv��t�7�@�~�hdo(
����J3d�1�����iR����"|&��X�ǟ׭���_��E ��X�7��S�>�Uj�<�2#�x�25���}��5����!�H3R�!�d2�#�X��s!3}�Td� H�M���il���x�Y����G{f������8�Oj�#�+Ǉ4�ax�@�ej�?�k��2�uS��li;2?�����o��~[UUUw�3��������ޒ;�p0�w����<��EJ[֎��#�( �]W7�<������+��� ��> �	�������i!C��Rr����̃��H�4����y�V}�D@>�i����Mtqt�����:Z��9mu4љ�M����o�
YO��Asyw7wu���v<�֊G�?~?w75�M��WF�Y�?]�
׮X�o-[����_��s��">��������2��\�ԓ����~>���p�c��r�Ï?�+�|�)��s���=�o��~��K�~�"�v�ܲb�d����q��Lc#^ܲK�WpimO7����j��wp,��sz�?i�Y���؇����E�8���o=�� �d��_v3W�q�;�q\�����|�~�i8^i�������n��7�b�#'��N���x�4�>��KSוSy6�Q�ۊ���j"H�\dh7ò�]!�=��~
��6��
��B�|D�?AN}t��H]�	����R�"t&b�q�J\Ǳz���E-�d9���=��1
$t �
�����O��{P`�ŀ����J��q���8���p�{/��	�a���U��f-;�0��|���ҢYs�$��[�a3�Eyl6OV�k$|�T&������Ȓ�D&�[��l��}�Mګ�����8yPQQљ�i�ݝB7�4٩ ̌�./�ӧ̬_�,�QP�R����<C%?Ν����wთ_�{�%8��1q�$�7<d?MGRP�q�[Υ��:�F��y0N(��}x~�{��A=���o�dH�@��#�1I��3�ǲyAvϐb�׀nB{՚ ���l�fv����^M�TP����N�ʀ��_�_"^hk�s�.y���ɖ<� �����J��{�wml������O���k��w\��j�*�|�J����G��_��]����Ջ�����-z_�6��u>���[��W���Ï���7�\���Ar��5�Wuw�����7���x�y��`Y[;ְ��pj⃪�};|{2��K)�2dqBԷ�Ǿ&`>r��D.m�@�,���3|���"�HQ�⃣>�u)�M;c����3��>�4y��ee:/?jc��V�6��� �� <(����]A?ǮA���a���d��ܰf��8���rm�n1��0\��L�:��<ڨ��x����_g���^���m�"Ͱ\��\�-�=v���r*�9�(�7�{f>M��fH����F��`������:�G{�=����=#�m�J
H�G:��p�ٷ����l��s2�3�Ƌ
�v��at�������1QZ�0�H�i~X�n��l�+��C��}v�KS�q)�Ai@th�G�9�aҤI8�cp�{ރ���߇s�='�x:� ��m.Ǝ�V�ܦ�s$���<Wv�Z��`���B2�4��l�Ϊ~0�� 
(`��DP���QZT_2��!}�`+u�/�>�ck���	;/M��D'��-�͜x��q%���~)��/r���[Z�@��ݸkh�_����\����^�72����~=q��e�	���	m������ז���?px�������������q�ʕ�5���&�֩@;�]��wSlڄǶl���Mx���p������;��o�z�9Շ־:�{���#4�������~�#�7A�_�O���g?���7(``A��R��1mƔ�3� ��5 d�N��'�~��9��<�`���J�^C��Aw���| >�q��h�+ho<, F2���Ԏ )��z��$�"�w ���_��&�M'�B�c����sf���G�3N;�,<
cǌ�AOe;Y<w��\�1a�����]<�mQ2邳�M�4�k�
��B���l��:"�)��s�E��TS��^K����)V�1Z]^~������{� ��l��w������nࠄ P4X��9�ӓn�CAo��18��#p�%������?��_�!\���s��)���w��x,\����m��;��k̙33fLǔ)�1a���M{#G�B݈:��բ��U�ը��BEE�s2}�L�� A��s���뼧�6NjM��Z	*�9!���F��!��"vTZ 8���Eu�T0ce�qh�sE'��=������1�^���ﳜ�|���mh�Dn�ǪF�z����\���/r��t�<� _�&�U_�[���`����.?eP�����ܫ��{�_[�2�B|y�K�!�e����K��+/���~���֒W��_�k����?]�7p�~���5���z��u��m�����mĝ��!���6��-�	��)��m؈�_�V�b����Y����o"k�f��o)�|�5�a���ͼ�V���N>�9~�p3�!��Ab_�����e������J;őn��5=]x����{�!��G��Z¶�I��4V�o�a�fu��){���%nc����I*�:�b/��Rɢ$�|f̚�C,������<�t0�+ʠ�4˚@m�&y�1^�2L֯�)K�8/���Q^^~ׂ�Q������H�4p�V֣�P=�.˳YN�ltea#�,"�U�5;��v�٭[�u���A�\�T������QW�,�|(G��4@d-�҄����@�le݈�k���*���\�+>~�������E�������>�+��$>��=��   IDAT��.��K�
� g�{6N?�t�t�;q<�Q\�~��q<�`���w���׼y�}�=1g�\̘=S�OǤ�S0~�D��0�Ǝ��Q�P� _� ���
��I�R))-s?�� _D�-b�O0��\�3����m�&vn�z��doH��������"{h<\����j�z��^�1[Ȧ��{J{,k9�Y)�&3~ ô}���#t0X�052����`��
��/�Gٗ��e�Xs3��v�]ܓת����p��5�ን�β���e���U��/��O��">�����s��#�k������">K��3O�Kܷ����s������p�|�U�������3������a��s%�0??��O�Mϳm/1�/�i��ִw`Cg7����݃ͽ���ׇ&�-��fFp�ݷ�g�f�n@�����y�ת;`��*>��ni���k��E���n�ä��fv'��)S����G%�=�%�mp33�������]אv�.c�ǉ�xee�1r$(sp4����&���K���#0�~�7�>���,�!"�a�X$a���"V�����_o�ZؔrAcf\Ti5^����gf��%�Q1; Y��(%8I������ �R$;��v���4Z���#~WZR:���ܯ��T`a`� 3/aƁ�@�X�Nj�~���@���{s������i�$`Mm-&L����L��>8�8���q�ig����!��� .�����G>���q������������>�i�7�>���/�k_�2����񭫿��|�j��o��Ͽ�u|�k_�W��%|�����O}
W|���0����������<���<��w��c��wء�b��s�bڴ�8i2ƍ�}Uu����Gȋ�'�e����s0So����_� �1P80h���^�9D���}�K�7Y�Zt������Je��N���4�iN�\�i�Hm#�>W��V�|�Ac��[�h>�v���9�1�B<#����}�>���3杞��Z8�ئ�\���}-�
x1����y�[:3����훚��M�պ��A�{�W�j�R��ʫ��K�p��/��g�ťO>�{g?�(�x�!�v�}8��{p����3�g��w\x�=�����=�O>�(>��_x�)|��o�c�^z�3���[> ����?s�W�w�Y�;��t��e��K/��O>��<�8>G��liĺT�[��(	�q/�W|�W~�g<��XE�>HSYA.�� �1����c.,�<�|�S�ė>��� (����tr���o	.��������I � U]�7Q�oyy�ZUU�3��#�P="���G�B��I���TNH~�3R+�R�j��!�m.�y�Rt�7���TZZ�tmm���0���T^��E���{�v�r�Έϧ�� �WG��U5$O)�u�������\�tp�&t�5VA=�}K���'���}p;�UU5����nsp��骪jʅ*�T��RgW#1j�h�eP�8i2�Ϙ����y��㠃��b9���)��;뜳���\���ۿ�� >����z\�9|ዟ�W��� �暫�-}ᛤz(|]��+_��6�>�+?}%���+�}�]~.� ��]p�8����w���a�A����=��3����i�����Qu���BiE9�eň'�/J�g�8��c��S��X� �>w�YTA��oɈ4�d� �����5J�iU� �����{��y>��)g:!�>�K�}9*ށ��W9�i�#�Ը��=�x�h�#����gp:^��͐!���Cg���ƾ4V�����.<�-�{�4�6~��Q�����;?�~�w��s5W�_�J����i�گx�|�p���q��%�Q�:<�ӎF f�#���G���&HsK#�z���	��<���<�x�ØQ#��[{������y�˧p���`���bq��u���)އ+#�u�#X��3s <	��f� \���r΅�9����Vc����t]9
O
��y��Ëx�9�)�i'�3b��ƝU�����pOWWW����l~Iq�q���G��ȳ����]3#��J��i�!������A ��@H�:	ǜR1N�-��*m{0hb���Q?��B"�@����I����˝�UUU1hW��F�!j�k(�B%��Z�JJ�i'���^<A�1�~�����G���ճ�uT�F5������'O�̙3�;��{�����bW�G~�:�(w�8�'��N�駝���;�\\x���=��%_�K�P��� �����>�q��C|s���^v.��������Kq��އ�\�^���8���p���'��8�xs�1XxԑX��Pn�쇽�ً�9�1S{��0~�X��D���AEeJ�B+.I�_u�<���c�qp��u��"�U?W��4�>�
C�L���Dw�A4�V�C�啥I/�61�B}�&�#t�13�|�G���蹟����q�Sɝ,�A;�)�v���hxo���][M��яa
M��نv ����XO>`��=��"m��4����L����>��b|����]��;3g�D}�g`� �[8!<t5�_�+`F^u����`�O�}��[̷�Jb�1绛%%����fƹ�5�]���~�� �ȓl��VP�����!�0^�!kba�F�!����0������^���IvߐYꪪ�;G�yW����>Wef�<�f�m#WD��Bx@�s�rQ��9 0о3��e�q�����<���v�b1d�!���{b�-r?�'g-�>��r_�*����T�>�j�*D�h�s�
~t,/�p��}>�P��h>��4t�x"� ��x��b> J]���JTUV��+�u#�r����c��ɘ6efΘ�9�gC���{b���a��������#�8G-<�s,�?�x~X='��N�ɟ�SN=��~&�<�]8묳p�9������� ^����"�K.��cPכ����o�� �E��y����8��sq����)�� ��ۅ�ʂ������?��ޘ��n�ƶO�<	���_���U\�W �`g?x����󡀚�*���}��}�b
d��j_.�<�5�GS����\�M�O8?���/,m0��i�p�`D6<����e��ӢJ{���-�~Am`�D�ň�:���8���� =�y�{h:�><�ԩӸ����1`�my�'[T�x1�cx	O3c���Ť[��B>[U]E{5�o���?O�2�y�@�����E�2�2a����&���l"t�.�d�A�����P�>d/Q�@QQ�kCk�9R��1���	{���K�K$��S�ąrB3s�����YH�Qx�Ss��*W����Ңhѱf���	�3�(��S'pȳ
B^��"��|�ȡ�H��&(a�.���iY���5�5.�r;u����t����P���-���
ؾ��`f`�SH3eh� ��U�y��X,�&n�����-++��B%�`?r�H�'[ƍ��ɓ�`ڴ��1��Ȼ����w�~8������a��#�d�?�8���Γp�)���SO��g���Yg��@r.�9�\��p޻ߍw�p>�;?��!p޻��a �s�5t��gA?�g���π����7�w�p"���8�����<R?�s:����ߗ����}����&O����'4k�P��j������2$�:L�*��~��qn�#��6;T�A�\���AE��_�m7vҤi~Ѓ�`�]#8&ӦM��}��z�������<�]g┓NC`��Yз3=�}�NX�h��`��������ӟ�D���[YY\@��rouU�ՎVVV�Gʡ�,}_�
{<,d�}�:���"F� !� �Xc~=�yO�&����<!dEq�wiIɩ;s���<]�����uuu��#,�*�T:ǅf��zN�����܌y(ʝ݂ UGxQ���1ܙ���`Fxa�rP3���Am;��)�B$Y��4   IDATZ� ���JW=rf�/�b�[�?�5!��./'�&Ae�&�N�N����_�8Q��K���&M����6I2�q�� ��Wj1�6���'� ����
����)m)h�������q��DwI{����L�r,��C��E��!�Hpu�̭����_W7c��0a&MRП΀?����g�� r��8�#p�����w��SO>
�Z����n�xW���x�%���/a�b��}�ӹ���?[{�z�:�]8���4n��|��ܪ9�����B~��8l�W��>���g����U��Y���yPS1e�L�<'M�x~s7nƌ�Q�F��+�����*��PƷ�R���R$9�
��D~<���`.x���2��#�Dii��V3f���p_��H�ķ�s�����w�q&�<�0̚1U��C�1��j�}�G��x�����ZD8��6\ii	�����c����=�|#,�=�_�f3cc]Ś� ������As���2W���.��~��g�� |��.r�Q����<�	���?3k���N����3��5W�}���T3X���,�.��Ki�Ȼ�| �����<�,��y�I�:�B*^6Y�{�R�H�*e|�73@�ٖ�(7�� ]w�+��pAN"�	�ɑd0�JW����F����R�����AZ�Cu
!_�4�U;�ҭb���
n��2���(��l�^�X'��_���x�KO������i|A_�^;�=?���lww����G$;�����:;;!t�cn'e�Lw�J���p�f��<�[�A��AO��vF���d~����\����{o(�*���(�p��8���݊�ޗ^r	��?��|�r|�������ħ?u%�)|��+�)���������я~����~D���~)���Kp�o�O��g���es�1G���G��� �<~7�k����3��4�u��)�0i�M���'b�T������ۏ�to
�&�_��/|�����>�~x7?�0L�<�����1��ة_�e� ��[���4�z���ք~�����7}���5����J~w)僵ȍ=x�A5ù�1��33R��8!L��k��0F��Y�J	��$7wi�= �VmM%KK��y��!���"�M���S���:���hél¹�6έ8(���LPn9 :��@��s�a3��3���x�	/��c����	�����5�@}3�w�x<�&ZR�������
�
�|���~"W暜.�3p�|j��گI]]U�ʪJT2�k�F[/ZQs��d@�j����J�'	҄Vmy�������m	yYd�1�}?z�Oxww(P赿�؄޾0�w�t���NW�;;Bt�2ط;J����m��h%ژ���r=��7�(��؁�%��VG5�`4WǓ\П�U�n�7o:� ~��8���Q�$��=����C�_����
|�3��?�|��_�~���]����u?�	n��������o��������/y#~�_ⷿ�~��_�7�?������}���H�QL�2U�U(�8ru]ͱ��ݏ7c��5f4W�#1�h��v�_�+�=QQY���N�EEEH�A㸘y� n��c9���a.ٱ13��0Z�bc2قS�A6A���'2l������#F�d�m����+��,UQQ�V�|��.QZzP,;��.��>�����g�m��0�ٺ�й*Z�c��\�r#@8f��C�_]�
�{a̷e��z~>'i�{�	'M\uMbM�2���A�����ԕ�bp���v_A\�vQ��WWU��jxA^�-�l�r��A��J�(�L�(�+��heẊ��'_�DD�u��:Ig/�>�J��LT�J��	�ĭK�ʸMTF*>B�Ҕ������r�(Y�"�QTT�""�t��ń�KY�����|��qy�(ձ�0a�DL�0�tƌ��%%��<�[H)>x����H*��χX�A���ح����q�9~�S��y0�� g�V#�=3�8�qNi(F�LY�a1��*�NQ'�^"�hV��DETϐ���"��~-�yG<i��k[vȱ������ܑ#G�
ߚ���T���RYR�'�۳.N&pS�L3s���t��v�����*�ȃ`y8��i��B}@%d�� ̢4 �̲�4�F�03�'�0��9�mcrN3����Fx��п��<��O�3h/�g@�1�+@�	�+b�H�O�**�

�%%%(�>�P^V�r}���A�½�W(�U����
�U�V������*T��UP��Pżj�*�W	�(]U-�����8Tso���)-�j�'dO���؞
���BYy��*++aP/AIi�{�$K��E(��"�G�}kP?��ԏ�ah^��w��a>�a�w��Cc��LV��a�p|$@����:�"�1Ai�/��G0
��
���-�����k0GF"0�;�"��a�`l���NQS�;�Ň����N+k�v�\ZZ:���8�3 �8lQ��B��AA�T�
�����q-�X^J�B����	��3�3��|^����=T?�[�j-�����Ѷ RA�.��!�İLT��`BD�Aȋ�
"�L<߇�����6G��8�E�BJ�}"�"��\��I�(����d�b�<p��7�%!�ڪ��%Q� +�=q"�Cp#=��)��|��`&Xi�4����02�4��e!`:�tZT~�/}ԗ%3��E�K��!���f�B {�(�D�D�;/J烢�3�WlV�8��dh�"&�t/J�eySV$�d.�.a[�-d�[1�M�|�.������j�7���W��UUUw*Xs��L&�`}�� `6�;L=�ƌB(33�� C��I1E�%��n��R1�r��Y�Dg��J�f!U��x���)�Ay�4̇��C��:l���`^�|���ք�@�� b-LI$� ��a�b3#	�">�fCQ�e<xay��;�Ȕ���!�� 1��#jux����<���D���摧G�di��	F��a�?��t8 <�ČW����9�f�«���ʉPp�qac�,)E��h1��:D���l�1-*5H�4�&�|�~�8I��A�}���_ݲ��ǌ�}-�$�G������_gee�cQ�־WP�q�L�B��`�q`O�FYA�	�$��)�$���N:9�Я#N��lԉu���Qz0T����7^�)cb�SraP�<Y�?G��� N�#ʠ@sA �;ݗ�\��
K�.!�p��6�Fb3
�D�:���:�8��]\�2�� H���:�TȘ���O�!�WA<!��՗��J��:@D��y��֜��t�_ c*c��� jdԤȠ��oLD B��`�yBʐwy�dkgV%K��Q	���������rP"mJr�X!�c>�p�%�`��GS�s>��*��ڊڃ���-�Il���/����V��q�/*.>1�H��{������*C��!��	8�����|N7d�r�cYd0���~3��O�
����I[U7��Tfƌ,D�|*��� �J�PN��D�L��e)̞CX��Ȕ�j�3���!�DY6w*-x0f撚�BI� � �n('#/�H��!��)��&�f^���Ìy�IH��̌�Ȃi0��?��A� �~�|}u{N���;�О���S
�D�9Yxo0뇓3�2�Nו��������#5�j.�,yo��{�a����h+����6}��z���?I$���~9����Z��9�C���n�?�}N��;�9���B�ι��Uu1�ͮ�6�U�M_8bĈ���߭�.�iW�U���]z;;�	�%�O�p �L�.䇡S}�?�̐�}��/Y|4�#���`fL���c�l��+b��7���(si�,��<a`��f����CIo�Z*'DR##��fC��l
��0�J��]�ܐJ!��W�>6,���  �IDAT��t;�2wqWqTZ�(��F* {�;�L�!����03�xAt0!J���O�L�v�&�<e��\�,#�!f��f	��~6��73Ǜ�*������y�� P%��pB�3�����I�SPN�<� v@S���VB�Sd���P�uɺ��_�Hm]�q'N��ޚ�(S�����=i����{~�(��8Y|*���2hÌ^B�zR�1��%��TٮS�*aN,\�3˵����
��)Y
�aJ�stս
��z81Lp¼�yBȓ���dlg�� � C��
\6�>�>6� e��@2���B��u$�m�}�/�tmc�xf%yD�B�(�J.��@���10ω���!/�7����?�HCsEs.�䜗`�B�eb!Y��7(彵ر�v��!�9��3�n��������҅E%%'Ƌ���|�b��O��'*���aE"H:q~�:a�s�	&�D�bf0�n��a��d�Q���B2�!ى���66б��`[@e.BAƀ�JG�eeY���=�µ��S&�Z���Ȩh�l�ZU�p�X�r�D<uu�|`���C
B��4���Ŏ7w-���,'ӽ��Ю�\�0LTR4a��2ǳ.3��13�J�ɝ̇�,DN�Fm���d H��܏_r.r_����㸷|�V�\X���1���+@�3o@N�xZ�[L�>v����X_2��>����A0~�X���@iZ���!8��N���PY*2�2��>��Z��So�ӌe��f�G�<6�J,DjU}�,�T"��7*$��0�!M!�v���(��#��m�1�������,��s�d�ڟ��,- ������5����F,���Q@ͷ�7�x<��[��j/&N�JYA��a��/�E�.�s{��U�������[e���O��c<�<Q����
f��[�8�j�QA �4��!�eY�U��!_Q��<Y�X)r �:i~LF��RS�R�Che��:�4#���@П`1�0'݊��ϻ�	`�P��e*�{+f�kxw��	�%�D3fF�椹��BV��f%���N�ȂZ"�!�,l�AQt��̇��aW4��I;;�|RFs ��G��T\\�).�../�<q�ر_������ۤ�ό]�4zt&�-�Uv��}z�'J�Ƌ�N��qm�\x��s^�fF��QJ|���\챀�\�pG�2�Y8I\�Шc^�e�EyJ�2�Fl�`�)� I���?��\u0�$��T+�m�ކ�� �5�6����@���hρ����I����J6�%���`f�o��^zL9{쨜oSI�q�=�ri��LΛ��A��>(�{�^v�lG�]H�����Y���A���㉸~E�B�.�þ_m�>�Ї��J����z`=`�mh��j�_�}d�%y5��n~����5������.�O_�=��Z�0P?��Z����+@�c��j��H�J[�otΟ���,������/���w��������$��x�S�037mm�����/6j
ے�z!�sms���JKy��UT�U]���-�F(�3-�|�1��duN����&�Ek`���@i�A�+Gc��(���ܿ!
��QoP*E�5L�(�$TbPY,�,j0}c���i0_ )t`�:$U� 0�H���(ZT8�盞�!���X?q����ܦ8�ۂ�?��cƌ�>�?��C�9�u�"w���m�Q��/�(pӹR�.**Z�=��*�V�Z�h�YO��(�Pԟ?�S�|0_NЄ΁��@�#�s��,h�Qu��S��p[g��Ԇ2��ɕ���!d����Yq6�3-�J�8-��1��`��,�<��#�[�p%�`,`�<��x"�z%������e@>���r?�_�$�;)[�V����sW�;�����}/W��P��I0�A� ~LY� ~�S㉄��{���z�̵N�D�+n��\�Gʹ�k�fوȔ���
d�Y�<�$B�h���:dA�vQ�q�*3��<1�1D����Y�F�b()<�����ȆpɁ�!�y�����7#G�("�YȃY^Ó��r�P4�J��"�V�\ �*����+���EnU\RR�nG�C^ٙ��UVT,���P0��>�+�w����v���w���Y�������ih"h��n������%�p��������#����L`OX?���2
B�r�x泄;�?%���C�#�ձ۾d5X%�#ak�}�l�V�)K՛[��'Q�"L��Y�I�.bv���ɕ4r�N��0PO�,b����lh0���o�Nс�܍!^�A]3�)�j�s�}�x��ħ� �H2Y����s�2>�����s�܍�PT�G�XQ�fO{f�;BJBBBJ
BB��]\�d�ҥ%KJ̯ڙ{e+q;��΀�ھ9���$�z�Y׊춘���aY�x������|�#��>7�(� �pC�8h⬛3&�Y���H�^o�5�^���,�J�t/�6�a�Z[�u���r��:�8�k����E�|Ш)a�	vc�Z�"�>?���=�=zژ��k���`+3?�[{8�Zk6��'�eu��YVmXk�%�eB[(i�3�^�}���au�~�xC66A��gه^޻�/�~�m���~, �|��B���i�㺺x��v������UU��p`��ڣxc��q�e
��i1���#�����,�_bFηM��}��\[K1!��X���V��l� -�3�f��n�G�~C����0�<�By�������u��!����?*Yc����a��x�eO�Xn��І�C����^V� 6m����x}Ȳ���yW�f4�+����֝���Ef�OO'�����:�yx�^e�@�
��=	g���a͛3pZ
8�G��b�z3K*s`���b~����`��z�,�vD��ƨ.02	��P���Z�ڞ�,=|l��B��}�1���N�8�����ȳll��g�7��
�X��p,���G��&''�(��cwv��?�������%Я�u�τ��g�=9g�\F��s&���)�k���]��͇n���E��b�*���s��+���o"�<�f���,�M���U,a�=Ģ�?X��x����A!�Hi#��Ļ��>���"{���ʢ�	��֚d�ĤIjR��i��f�������G�\X�un��އ.n�3p�p�<����#�&�����"Km����I�Vw�1P2@1��|�xp�F�]p|K,|��BCPt"(D�����t��ԍ�3�5% @3�ls��g������[¾B�%Q���έi��񬋲p{�^�5�0�3ր�f�B;K���W�C����s�.Ч|���5���o��~�
��L������??����2j�^���ہ���"E��"V�Wo��x��<�R���d<�/orϥ�9Ӭ��:�e��Y�v�O�s���B��?y�-�����3 �n~�-e@����-1 �π��1T�ŀh5�V�WΉ1�d$�M���.�@�h�@�:nrN��0 ��@���d@�̸��b@����:2�T�1���@����;b@��Ȁ:2�T��f0С^J�;l�*�@��@7+^�b@ݡ`��.0 �Ā�Mє/b@��	t��)gĀh�6ES������F1�  ��!�ES   IDAT ����v    IEND�B`�
```

### `src/flows/nudges/components/SheetSwitcher.module.css`

```css
/* PROTOTYPE ONLY: the floating Layout · Case · State pill over the open nudge sheet. Tokens only. */

/* Starts top-left, under the floating settings button and above the sheet; once dragged, left / top come from the
   component. */
.pill {
  position: absolute;
  z-index: var(--app-layer-fab);
  left: var(--l3-spacing-12);
  top: var(--l3-size-64);
  width: max-content;
  display: flex;
  align-items: center;
  gap: var(--l3-spacing-04);
  max-width: calc(100% - var(--l3-spacing-24));
  padding: var(--l3-spacing-04);
  border-radius: var(--l3-radius-full);
  background: var(--l3-surface-primary);
  box-shadow: var(--l3-shadow-elevation-high);
  touch-action: none;
}

.grip {
  flex: none;
  display: grid;
  place-items: center;
  width: var(--l3-size-32);
  height: var(--l3-size-32);
  padding: 0;
  border: 0;
  border-radius: var(--l3-radius-full);
  background: none;
  color: var(--l3-content-secondary);
  cursor: grab;
  touch-action: none;
}
.grip:active { cursor: grabbing; }

.chip {
  flex: 0 1 auto;
  min-width: 0;
  display: inline-flex;
  align-items: center;
  gap: var(--l3-spacing-02);
  height: var(--l3-size-32);
  padding: 0 var(--l3-spacing-04) 0 var(--l3-spacing-08);
  border: 0;
  border-radius: var(--l3-radius-full);
  background: var(--l3-surface-secondary);
  color: var(--l3-content-primary);
  font: var(--l3-text-label-12);
  white-space: nowrap;
  cursor: pointer;
}
.chip > svg { flex: none; transition: transform var(--l3-motion-duration-short) var(--l3-motion-easing-standard); }
.chip[data-open] { box-shadow: inset 0 0 0 1px var(--l3-border-dark); }
.chip[data-open] > svg { transform: rotate(180deg); }
/* The short pills keep their size; the case (the long one) gives way so the bar never runs past the screen. */
.value { min-width: 0; overflow: hidden; text-overflow: ellipsis; }
.chip:not([data-wide]) { flex: none; }
.chip[data-wide] { min-width: var(--l3-size-64); }

/* The dropdown: a floating card with the full names. */
.menu {
  position: absolute;
  z-index: var(--app-layer-fab);
  box-sizing: border-box;
  min-width: calc(var(--l3-size-96) * 2);
  max-width: calc(100% - var(--l3-spacing-16));
  overflow-y: auto;
  padding: var(--l3-spacing-04);
  border-radius: var(--l3-radius-16);
  background: var(--l3-surface-primary);
  box-shadow: var(--l3-shadow-elevation-high), inset 0 0 0 1px var(--l3-border-light);
  animation: drop var(--l3-motion-duration-short) var(--l3-motion-easing-decelerate) both;
}
.menuTitle {
  padding: var(--l3-spacing-08) var(--l3-spacing-12) var(--l3-spacing-04);
  color: var(--l3-content-secondary);
  font: var(--l3-text-label-12);
}
.item {
  display: flex;
  align-items: center;
  gap: var(--l3-spacing-08);
  width: 100%;
  min-height: var(--l3-size-40);
  padding: 0 var(--l3-spacing-12);
  border: 0;
  border-radius: var(--l3-radius-12);
  background: none;
  color: var(--l3-content-primary);
  font: var(--l3-text-label-14);
  text-align: left;
  cursor: pointer;
}
.item:hover { background: var(--l3-surface-secondary); }
.item[data-picked] { background: var(--l3-surface-secondary); }
.itemLabel { flex: 1; }
.item > svg { flex: none; color: var(--l3-content-accent-success-default); }

@keyframes drop { from { opacity: 0; transform: translateY(calc(var(--l3-spacing-04) * -1)); } }
@media (prefers-reduced-motion: reduce) { .menu, .chip > svg { animation: none; transition: none; } }
```

### `src/flows/nudges/components/SheetSwitcher.tsx`

```tsx
import { useEffect, useLayoutEffect, useRef, useState, type PointerEvent } from 'react'
import { createPortal } from 'react-dom'
import { Icon } from '@l3/components/Icon'
import { msCheck, msDragIndicator, msKeyboardArrowDown } from '@l3/icons/material'
import { setFlowOption, useFlowOption, usePreview } from '../../../shared/prototype'
import { t } from '../copy'
import { activeMeter, caseOption, meterFillOption, meterLayoutOption, meterLevelOption, meterOption, stateOption } from '../options'
import styles from './SheetSwitcher.module.css'

type Option = typeof caseOption | typeof stateOption | typeof meterOption | typeof meterLevelOption | typeof meterLayoutOption | typeof meterFillOption
type Spot = { x: number; y: number }

const SPOT_KEY = 'nudges-switcher-spot'
const readSpot = (): Spot | null => {
  try { return JSON.parse(localStorage.getItem(SPOT_KEY) ?? 'null') } catch { return null }
}

/**
 * PROTOTYPE ONLY — not part of the design. A small floating pill over the order pad and the open nudge sheet: Layout ·
 * (Layout 1: Chip / Icon + tag) · Case · State,
 * each a dropdown pill (its own menu, with the full names), so versions can be compared on a phone without opening the
 * settings. A value that doesn't fit its pill is cut with an ellipsis; the menu shows it whole. Drag it by the grip; it remembers where it was left (this browser).
 *
 * The sheet makes everything inside the screen inert, so the pill is drawn just outside the screen (in the layer
 * that holds it), over the sheet.
 */
/** `open`: show it (on a pad that has a nudge to fire). */
export function SheetSwitcher({ open }: { open: boolean }) {
  const { interactive } = usePreview()
  const anchor = useRef<HTMLSpanElement>(null)
  const [host, setHost] = useState<HTMLElement | null>(null)
  useLayoutEffect(() => {
    const screen = anchor.current?.closest('[data-part="page"]')?.parentElement
    setHost(screen?.parentElement ?? null)
  }, [])

  return <>
    <span ref={anchor} hidden />
    {interactive && open && host && createPortal(<Pill host={host} />, host)}
  </>
}

function Pill({ host }: { host: HTMLElement }) {
  const pill = useRef<HTMLDivElement>(null)
  const [spot, setSpot] = useState<Spot | null>(readSpot)
  const meter = activeMeter(useFlowOption('nudges', meterOption.id, meterOption.default))
  const fill = useFlowOption('nudges', meterFillOption.id, meterFillOption.default)
  const [menu, setMenu] = useState<{ option: Option; chip: HTMLElement } | null>(null)
  const grab = useRef<{ id: number; dx: number; dy: number } | null>(null)

  // Keep it inside the screen (a phone turned, or a spot saved on a bigger screen).
  const clamp = (x: number, y: number): Spot => {
    const box = pill.current?.getBoundingClientRect()
    const w = box?.width ?? 0
    const h = box?.height ?? 0
    return { x: Math.min(Math.max(0, x), host.clientWidth - w), y: Math.min(Math.max(0, y), host.clientHeight - h) }
  }

  const down = (e: PointerEvent<HTMLButtonElement>) => {
    const box = pill.current!.getBoundingClientRect()
    setMenu(null)
    grab.current = { id: e.pointerId, dx: e.clientX - box.left, dy: e.clientY - box.top }
    try { e.currentTarget.setPointerCapture(e.pointerId) } catch { /* the pointer is already gone */ }
  }
  const move = (e: PointerEvent<HTMLButtonElement>) => {
    const g = grab.current
    if (!g || g.id !== e.pointerId) return
    const origin = host.getBoundingClientRect()
    // The preview may scale the phone: convert screen pixels to the host's own.
    const scale = origin.width / host.clientWidth || 1
    setSpot(clamp((e.clientX - origin.left - g.dx) / scale, (e.clientY - origin.top - g.dy) / scale))
  }
  const up = (e: PointerEvent<HTMLButtonElement>) => {
    if (grab.current?.id !== e.pointerId) return
    grab.current = null
    try { if (spot) localStorage.setItem(SPOT_KEY, JSON.stringify(spot)) } catch { /* storage off */ }
  }

  return <div ref={pill} className={styles.pill} role="group" aria-label={t('switcher.label')}
    style={spot ? { left: spot.x, top: spot.y } : undefined}>
    <button type="button" className={styles.grip} aria-label={t('switcher.drag')}
      onPointerDown={down} onPointerMove={move} onPointerUp={up} onPointerCancel={up}>
      <Icon icon={msDragIndicator} size={20} />
    </button>
    <Pick option={meterOption} menu={menu} setMenu={setMenu} short={(_, label) => label.split(' · ')[0]} />
    <Pick option={meterLevelOption} menu={menu} setMenu={setMenu} short={(_, label) => label} />
    {!meter.startsWith('gauge') && !(meter === 'soft' && (fill === 'splitWords' || fill === 'wholeWords')) && <Pick option={meterLayoutOption} menu={menu} setMenu={setMenu} short={(_, label) => label} />}
    {meter === 'soft' && <Pick option={meterFillOption} menu={menu} setMenu={setMenu} short={(_, label) => label} />}
    <Pick option={caseOption} menu={menu} setMenu={setMenu} short={(_, label) => label} wide />
    <Pick option={stateOption} menu={menu} setMenu={setMenu} short={(v) => t('switcher.state', { state: v })} />
    {menu && <Menu option={menu.option} chip={menu.chip} host={host} onClose={() => setMenu(null)} />}
  </div>
}

type MenuState = { option: Option; chip: HTMLElement } | null

/** A dropdown pill: the short value (cut with an ellipsis when it doesn't fit) and a chevron; a tap opens the menu. */
function Pick({ option, short, wide, menu, setMenu }: {
  option: Option; short: (value: string, label: string) => string; wide?: boolean
  menu: MenuState; setMenu: (menu: MenuState) => void
}) {
  const value = useFlowOption('nudges', option.id, option.default)
  const label = option.values.find((o) => o.value === value)?.label ?? value
  const open = menu?.option.id === option.id
  return <button type="button" className={styles.chip} data-wide={wide ? '' : undefined} data-open={open ? '' : undefined}
    aria-haspopup="listbox" aria-expanded={open} aria-label={`${option.label}: ${label}`}
    onClick={(e) => setMenu(open ? null : { option, chip: e.currentTarget })}>
    <span className={styles.value}>{short(value, label)}</span>
    <Icon icon={msKeyboardArrowDown} size={16} />
  </button>
}

/** The open dropdown: every value by its full name, the picked one ticked. Under its pill (above it when there's no
 *  room), kept inside the screen; a tap outside or Escape closes it. */
function Menu({ option, chip, host, onClose }: { option: Option; chip: HTMLElement; host: HTMLElement; onClose: () => void }) {
  const box = useRef<HTMLDivElement>(null)
  const value = useFlowOption('nudges', option.id, option.default)
  const [spot, setSpot] = useState<{ left: number; top: number; maxHeight: number } | null>(null)

  useLayoutEffect(() => {
    const origin = host.getBoundingClientRect()
    const scale = origin.width / host.clientWidth || 1
    const at = chip.getBoundingClientRect()
    const gap = 8
    const width = box.current?.offsetWidth ?? 0
    const left = Math.min(Math.max(gap, (at.left - origin.left) / scale), host.clientWidth - width - gap)
    const below = (at.bottom - origin.top) / scale + gap
    const above = (at.top - origin.top) / scale - gap
    const roomBelow = host.clientHeight - below - gap
    const height = box.current?.scrollHeight ?? 0
    setSpot(height <= roomBelow || roomBelow >= above
      ? { left, top: below, maxHeight: roomBelow }
      : { left, top: Math.max(gap, above - height), maxHeight: above - gap })
  }, [chip, host])

  useEffect(() => {
    const away = (e: Event) => {
      const target = e.target as Node
      if (!box.current?.contains(target) && !chip.contains(target)) onClose()
    }
    const key = (e: KeyboardEvent) => { if (e.key === 'Escape') onClose() }
    document.addEventListener('pointerdown', away)
    document.addEventListener('keydown', key)
    return () => { document.removeEventListener('pointerdown', away); document.removeEventListener('keydown', key) }
  }, [chip, onClose])

  return createPortal(<div ref={box} className={styles.menu} role="listbox" aria-label={option.label}
    style={spot ?? { visibility: 'hidden' }}>
    <div className={styles.menuTitle}>{option.label}</div>
    {option.values.map((o) => {
      const picked = o.value === value
      return <button key={o.value} type="button" role="option" aria-selected={picked} className={styles.item}
        data-picked={picked ? '' : undefined}
        onClick={() => { setFlowOption('nudges', option.id, option.default, o.value); onClose() }}>
        <span className={styles.itemLabel}>{o.label}</span>
        {picked && <Icon icon={msCheck} size={16} />}
      </button>
    })}
  </div>, host)
}
```

### `src/flows/nudges/copy.json`

```json
{
  "order.back": "Back",
  "order.switch": "Change contract",
  "order.product": "Product",
  "order.delivery": "Delivery",
  "order.intraday": "Intraday",
  "order.type": "Order type",
  "order.market": "Market",
  "order.limit": "Limit",
  "order.sl": "SL",
  "order.validity": "Validity",
  "order.quantity": "Quantity",
  "order.lots": "Lots",
  "order.unitSwitch": "Switch between quantity and lots",
  "order.lotHint": "({lot} = 1 Lot)",
  "order.limitPrice": "Limit",
  "order.trigger": "Trigger Price",
  "order.offset": "Distance from the market price",
  "order.tpsl": "Set TPSL",
  "order.margin": "Margin:",
  "order.leverage": "Leverage:",
  "order.autoClose": "This position will auto close by {time}",
  "order.available": "Avail.",
  "order.required": "Req",
  "order.buy": "Buy",
  "order.sell": "Sell",
  "order.placed": "{side} order placed · {name} {contract}",
  "silent.tpsl": "TP/SL",
  "silent.tpslOn": "Target +{target}% · Stop-loss −{stop}%",
  "silent.tpslOff": "Off",
  "silent.tpslEdit": "Edit TP/SL",
  "silent.tpslToggle": "TP/SL on this order",
  "silent.prefilled": "Pre-filled",
  "silent.limitLeft": "{left} left of today's loss limit",
  "silent.limitAdd": "Set a loss limit for today",
  "silent.limitBar": "Loss used today",
  "silent.limitNear": "Close to today's loss limit",
  "nudge.setPnl": "Set a loss limit for today",
  "nudge.storyPrimary": "Place an order with an SL limit",
  "nudge.storyNotNow": "Place without limit",
  "nudge.setTpsl": "Add TP/SL to this order",
  "nudge.notNow": "Not now, place order",
  "pnl.title": "Today's loss limit",
  "pnl.description": "When today's loss reaches this amount, new F&O orders pause until tomorrow. Open positions stay as they are.",
  "pnl.field": "Limit for today",
  "pnl.presets": "Quick amounts",
  "pnl.helper": "You can change or remove it any time today.",
  "pnl.save": "Set limit",
  "pnl.saved": "Loss limit set · {amount} for today",
  "tpsl.title": "TP/SL for this order",
  "tpsl.description": "Exits on its own when the price reaches your target or your stop-loss.",
  "tpsl.target": "Target profit",
  "tpsl.stop": "Stop-loss",
  "tpsl.atPrice": "at {price}",
  "tpsl.save": "Save TP/SL",
  "tpsl.saved": "TP/SL added to this order",
  "option.case": "Case",
  "option.state": "Data state",
  "option.stateA": "A · own loss",
  "option.stateB": "B · own, no loss",
  "option.stateC": "C · thin history",
  "option.everyBuy": "Show on every Buy",
  "option.everyBuyOff": "Off",
  "option.everyBuyOn": "On",
  "option.vibrate": "Vibrate when it opens",
  "switcher.label": "Prototype: switch the nudge",
  "switcher.drag": "Drag to move",
  "switcher.layout": "Layout {n}",
  "switcher.state": "State {state}",
  "option.actions": "Buttons",
  "option.actionsTwo": "Both guardrails",
  "option.actionsOne": "One guardrail",
  "nudge.tag": "Overtrading Detected",
  "gauge.low": "Low",
  "gauge.medium": "Medium",
  "gauge.high": "High",
  "gauge.tag.danger": "High Risk",
  "gauge.tag.caution": "Medium Risk",
  "gauge.tag.safe": "Low Risk",
  "gauge.heading.danger": "Your chances of losing money is high",
  "gauge.heading.caution": "Your chances of losing money is medium",
  "gauge.heading.safe": "Your chances of losing money is low",
  "gauge.sizeUp": "You are placing a bigger order right after loss",
  "nudge.lastLoss": "Last time you did this, you lost {amount}",
  "nudge.others": "{count} in 10 traders who did this lost more by the end of the day",
  "nudge.othersOtherDays": "{count} in 10 traders who did this lost more than on other days",
  "nudge.notNowPositions": "Not now",
  "nudge.barsLabel": "{now}: {ratio}× {base}",
  "nudge.usual": "Usual",
  "nudge.vsUsual": "vs your usual",
  "nudge.highRisk": "High risk",
  "nudge.levelLow": "Low risk",
  "nudge.levelMedium": "Medium risk",
  "nudge.levelSafe": "Safe",
  "nudge.levelMid": "Caution",
  "nudge.vsUsualPlain": "Compared with how you usually trade",
  "nudge.zoneSafe": "Safe",
  "nudge.zoneDanger": "Danger",
  "nudge.zoneLow": "Low risk zone",
  "nudge.zoneHigh": "High risk zone",
  "nudge.zoneHeadline": "Overtrading, you just entered the high risk zone",
  "nudge.overtrading": "You're overtrading",
  "nudge.overtradingRisk": "Your chances of losing money are high",
  "nudge.meterHeading": "You are overtrading",
  "nudge.meterSub": "Your chances of losing money today are high",
  "nudge.meterRiskHeading": "Your chances of losing money are high",
  "nudge.sizeUpNow": "You are placing a bigger {ratio}X order right now after a loss of {amount}",
  "nudge.sizeUpNowPlain": "You are placing a bigger order right now after a loss of {amount}",
  "nudge.biggerAfterLoss": "You are placing a bigger order right after a loss",
  "nudge.meterFirstSub": "A {ratio} bigger order right after a {amount} loss raises your chances of losing more today",
  "nudge.meterFirstSubPlain": "A bigger order right after a {amount} loss raises your chances of losing more today",
  "nudge.meterFirstSubOther": "{fact}. Your chances of losing money today are high",
  "nudge.numberFact": "You’re placing a bigger order right after a loss of {amount}",
  "nudge.everyone": "Everyone",
  "nudge.you": "You",
  "nudge.safeZone": "Safe zone",
  "nudge.dangerZone": "Danger zone",
  "nudge.safeZoneNote": "trading to plan",
  "nudge.dangerZoneNote": "chasing losses",
  "nudge.lossChance": "High chance of losing money",
  "nudge.factWhy": "You're in a loss today. This is based on your own trades.",
  "nudge.riskLow": "Lower risk",
  "nudge.riskHigh": "Higher risk",
  "nudge.scaleLabel": "{now} is {ratio}X {base}, at the higher-risk end",
  "nudge.setPnlShort": "Set loss limit",
  "nudge.placeOrder": "Place order",
  "nudge.meterLabel": "Risk meter: you are in the danger zone",
  "nudge.meterLabelSafe": "Risk meter: you are in the safe zone",
  "nudge.meterLabelCaution": "Risk meter: you are in the caution zone",
  "nudge.meterLabelRatio": "Risk meter: you are in the danger zone, {ratio}X your usual",
  "case.generic.name": "Generic",
  "case.generic.headline": "Down ₹2,500 today and still trading",
  "case.sizeUp.name": "1 · Size-up after a loss",
  "case.sizeUp.headline": "This order is 2X the one you just lost",
  "case.sizeUp.base": "Trade you lost",
  "case.sizeUp.now": "This order",
  "case.sizeUp.unit": "bigger than the trade you just lost",
  "case.orders.name": "2 · Orders in the session",
  "case.orders.headline": "3X more orders than usual today",
  "case.orders.raw": "14 orders today",
  "case.orders.base": "Your usual day",
  "case.orders.now": "Today",
  "case.orders.unit": "more orders than usual today",
  "case.flips.name": "3 · CE ↔ PE flips",
  "case.flips.headline": "Switched calls ↔ puts 3X more than usual",
  "case.flips.raw": "Switched calls ↔ puts 6 times today",
  "case.flips.base": "Your usual day",
  "case.flips.now": "Today",
  "case.flips.unit": "more call ↔ put switches than usual",
  "case.burst.name": "4 · Orders in 15 min",
  "case.burst.headline": "4X more orders than usual in 15 min",
  "case.burst.raw": "9 orders in the last 15 min",
  "case.burst.base": "Usual 15 min",
  "case.burst.now": "Last 15 min",
  "case.burst.unit": "more orders than usual in 15 min",
  "case.money15.name": "5 · Money in 15 min",
  "case.money15.headline": "3X more money than usual in 15 min",
  "case.money15.raw": "₹48,000 put in, in 15 min",
  "case.money15.base": "Usual 15 min",
  "case.money15.now": "Last 15 min",
  "case.money15.unit": "more money than usual in 15 min",
  "case.bigOrder.name": "6 · Big order vs money",
  "case.bigOrder.headline": "This order is 4X your usual size",
  "case.bigOrder.raw": "This order uses 60% of your money",
  "case.bigOrder.base": "Your usual order",
  "case.bigOrder.now": "This order",
  "case.bigOrder.unit": "your usual order size",
  "case.pace.name": "7 · Time between orders",
  "case.pace.headline": "Ordering 6X faster than usual",
  "case.pace.raw": "40 seconds between orders",
  "case.pace.base": "Your usual pace",
  "case.pace.now": "Now",
  "case.pace.unit": "faster than your usual pace",
  "case.strike.name": "8 · Far strike",
  "case.strike.headline": "Strike 10X farther than usual",
  "case.strike.raw": "Strike 1,200 points from NIFTY",
  "case.strike.base": "Your usual strike",
  "case.strike.now": "This strike",
  "case.strike.unit": "farther than your usual strike",
  "case.avgDown.name": "9 · Averaging down",
  "case.avgDown.headline": "Bought more 3 times while it fell",
  "case.rareSession.name": "10 · Unusual time",
  "case.rareSession.headline": "Trading at a time you rarely trade",
  "case.expiry.name": "Moment · Expiry, recovering",
  "case.expiry.headline": "3X more trades than usual, on expiry",
  "case.expiry.raw": "12 trades today, on expiry",
  "case.expiry.base": "Your usual day",
  "case.expiry.now": "Today",
  "case.expiry.unit": "more trades than usual, on expiry",
  "case.deposit.name": "Moment · Bigger deposit",
  "case.deposit.headline": "Added 5X more money than usual",
  "case.deposit.raw": "Added ₹20,000 today",
  "case.deposit.base": "Your usual top-up",
  "case.deposit.now": "Today",
  "case.deposit.unit": "more money added than usual",
  "case.givingBack.name": "Moment · Giving back profit",
  "case.givingBack.headline": "Gave back 79% of today's profit",
  "case.fomo.name": "Moment · Missed entry",
  "case.fomo.headline": "Buying after it already rose 38%",
  "case.returnBreak.name": "Moment · Back after a break",
  "case.returnBreak.headline": "3X your usual size, after a break",
  "case.returnBreak.raw": "First trade in 23 days, and a big one",
  "case.returnBreak.base": "Your usual order",
  "case.returnBreak.now": "This order",
  "case.returnBreak.unit": "your usual size, after a break",
  "case.afterWin.name": "Moment · After a winning day",
  "case.afterWin.headline": "2X your usual size, after a win",
  "case.afterWin.raw": "Big order the day after a ₹6,200 win",
  "case.afterWin.base": "Your usual order",
  "case.afterWin.now": "This order",
  "case.afterWin.unit": "your usual size, after a win",
  "option.layout": "Layout",
  "option.layoutBars": "1 · Centred + bars",
  "option.layoutNumber": "2 · Big number",
  "option.layoutCompact": "3 · Compact alert",
  "option.layoutGauge": "4 · Risk meter",
  "option.zoneRisk": "5a · High risk",
  "option.zoneEveryone": "5b · Everyone vs you",
  "option.zoneExplain": "5c · Why first",
  "option.zoneStory": "5d · Story",
  "option.zoneFact": "5e · Fact first",
  "option.zoneCard": "5f · One card",
  "option.zoneCompact": "5g · Compact",
  "option.meter": "Meter",
  "option.meterNeedle": "4a · Needle",
  "option.meterTicks": "4b · Ticks",
  "option.meterSweep": "4c · Sweep",
  "option.meterKnob": "4d · Knob",
  "option.meterLevels": "4e · Levels",
  "option.meterSoft": "4f · Soft dial",
  "option.meterBlocks": "4g · Blocks",
  "option.meterGauge": "4h · Speedometer · 0–100",
  "option.meterGaugeWords": "4i · Speedometer · Low–High",
  "option.meterLevel": "Risk level",
  "option.levelDanger": "High risk",
  "option.levelCaution": "Caution",
  "option.levelSafe": "Safe",
  "option.meterLayout": "Meter layout",
  "option.meterLayoutText": "Text first",
  "option.meterLayoutMeter": "Meter first",
  "option.meterLayoutTag": "Tag first",
  "option.meterLayoutNumber": "With multiple",
  "option.meterFill": "Meter fill",
  "option.meterFillWhole": "One colour",
  "option.meterFillBlend": "Blended",
  "option.meterFillSplit": "Blended · 3 blocks",
  "option.meterFillSplitWords": "3 blocks · Low–High",
  "option.meterFillWholeWords": "One colour · Low–High",
  "option.layoutZone": "5 · Risk bar",
  "option.badge": "Layout 1 header",
  "option.badgeChip": "Chip (✋ in the tag)",
  "option.badgeTag": "Icon + tag",
  "switcher.badgeChip": "Chip",
  "switcher.badgeTag": "Tag",
  "protect.section": "Trade protect · {group}",
  "protect.group.figma": "Figma designs",
  "protect.group.money": "Money moves",
  "protect.group.day": "The day's P&L",
  "protect.group.trade": "One trade",
  "protect.group.days": "Across days",
  "protect.group.tools": "Your positions and tools",
  "protect.actions": "Trade protect",
  "protect.dismiss.placeOrder": "Not now, place order",
  "protect.dismiss.ownTrade": "Not now, I will trade on my own",
  "protect.tag.highRisk": "High Risk",
  "protect.tag.pnl": "P&L: {pnl}",
  "protect.pnlLine": "P&L:",
  "protect.riskLabel": "High Risk",
  "protect.recommended": "Recommended",
  "protect.item.pnl": "Automate your portfolio with P&L Protect",
  "protect.item.tpsl": "Add TP/SL to this order",
  "protect.item.autoTpsl": "Auto TP/SL: {pct} target on every new order",
  "protect.price": "Set a stop loss to this order at",
  "protect.stat.todayPnl": "Today's P&L",
  "protect.stat.currentOrder": "Current Order",
  "protect.stat.orderSize": "Order Size",
  "protect.stat.todaySoFar": "Today so far",
  "protect.stat.added": "Added",
  "protect.stat.exitAt": "Exits at",
  "protect.stat.todayHigh": "Today's high",
  "protect.stat.todayPeak": "Today's peak",
  "protect.stat.now": "Now",
  "protect.risky.name": "High risk today",
  "protect.risky.heading": "Your trades are riskier today!",
  "protect.risky.body": "Protect your trade by setting a Stop loss",
  "protect.risky.cta": "Set a TP/SL for this order",
  "protect.sizeUp.name": "Size-up after a loss",
  "protect.sizeUp.heading": "You increased your size after a loss",
  "protect.sizeUp.body": "Protect your trade by setting a Stop loss",
  "protect.sizeUp.cta": "Set a stop loss for today",
  "protect.aggressive.name": "Trading more aggressively today",
  "protect.aggressive.heading": "You are trading more aggressively today!",
  "protect.aggressive.body": "Protect today's trade before placing another order",
  "protect.aggressive.cta": "Set a default stop loss",
  "protect.m1.name": "Deposits, loses it, deposits again the same day",
  "protect.m1.heading": "{added} added",
  "protect.m1.body": "Set a loss limit for today. P&L Protect exits all your F&O positions if today's P&L reaches {line}.",
  "protect.m1.cta": "Set a loss limit for today",
  "protect.m2.name": "Deposits while already down today",
  "protect.m2.heading": "{added} added",
  "protect.m2.body": "Set a loss limit for today. P&L Protect exits all your F&O positions if today's P&L reaches {line}.",
  "protect.m2.cta": "Set a loss limit for today",
  "protect.m11.name": "Lost all the money he added today",
  "protect.m11.heading": "You've lost all the money you added today",
  "protect.m11.body": "P&L Protect exits all your F&O positions at a level you pick.",
  "protect.m11.cta": "Activate P&L Protect",
  "protect.m7.name": "Today's loss passes his worst day",
  "protect.m7.heading": "Today is your biggest loss day on Lemonn so far",
  "protect.m7.body": "Set P&L Protect to exit all your F&O positions at a level you pick for today",
  "protect.m7.cta": "Activate P&L Protect",
  "protect.m8.name": "The day turns from green to red",
  "protect.m8.heading": "Your day turned from green to red",
  "protect.m8.body": "P&L Protect exits all your F&O positions at a level you pick.",
  "protect.m8.cta": "Activate P&L Protect",
  "protect.m17.name": "Given back half of today's peak",
  "protect.m17.heading": "You've given back half of today's gain",
  "protect.m17.body": "With Trail SL, P&L Protect moves your exit up {step} for every {step} you gain.",
  "protect.m17.cta": "Turn on Trail SL",
  "protect.m9.name": "Third losing trade in a row today",
  "protect.m9.heading": "Your last 3 trades closed in a loss",
  "protect.m9.body": "Add a stop loss of {stop} to this order. Protect your order to limit your loss.",
  "protect.m9.cta": "Apply SL to this order",
  "protect.m13.name": "A trade closed at half its value or worse",
  "protect.m13.heading": "Your last {contract} closed at {drop}",
  "protect.m13.body": "Add a stop loss to this order. Protect your order to limit your loss.",
  "protect.m13.cta": "Apply SL to this order",
  "protect.m14.name": "An option he held expired worthless",
  "protect.m14.heading": "Yesterday's {contract} expired at ₹0",
  "protect.m14.body": "A stop loss sells at the price you pick.",
  "protect.m14.cta": "Apply SL to this order",
  "protect.m15.name": "His biggest single-trade loss",
  "protect.m15.heading": "Your last trade was your biggest loss on Lemonn",
  "protect.m15.body": "Add a stop loss to this order. Protect your order to limit your loss.",
  "protect.m15.cta": "Apply SL to this order",
  "protect.m10.name": "First order after his worst day",
  "protect.m10.heading": "Yesterday was your biggest loss day on Lemonn",
  "protect.m10.body": "Set P&L Protect to exit all your F&O positions at a level you pick for today",
  "protect.m10.cta": "Activate P&L Protect",
  "protect.m18.name": "First order after his best day",
  "protect.m18.heading": "Yesterday was your best day on Lemonn",
  "protect.m18.body": "Keep today's gains safe: add a stop loss to this order.",
  "protect.m18.cta": "Apply SL to this order",
  "protect.m19.name": "His third red day in a row",
  "protect.m19.heading": "Your last 3 trading days ended in a loss",
  "protect.m19.body": "Set P&L Protect to exit all your F&O positions at a level you pick for today",
  "protect.m19.cta": "Activate P&L Protect",
  "protect.n3.name": "A second position, neither with an exit",
  "protect.n3.heading": "{count} open positions, no exits set",
  "protect.n3.body": "P&L Protect exits both at a level you pick.",
  "protect.n3.cta": "Protect both",
  "protect.n12.name": "His target filled",
  "protect.n12.heading": "Your target on {contract} filled at {price} ({pct})",
  "protect.n12.body": "Use {pct} as your target on every order?",
  "protect.n12.cta": "Set Auto TP/SL",
  "option.protectVersion": "Trade protect · version",
  "option.protectVersion1": "Version 1",
  "option.protectVersion2": "Version 2"
}
```

### `src/flows/nudges/copy.ts`

```ts
import { makeCopy } from '../../shared/copy'
import copy from './copy.json'

/** Every user-facing string of this flow is in copy.json: t('screen.title'), t('key', { count }). */
export const t = makeCopy('nudges', copy)
```

### `src/flows/nudges/data.ts`

```ts
/**
 * Overtrading nudges (product team draft, 2026-10-30 — playground, nothing built in the real app).
 *
 * Every nudge is ONE sheet; a case only fills its slots. The words live in copy.json under `case.<id>.*`; this file
 * says which cases exist, which guardrail each one leads with, and the sample account values. Every number in the
 * copy is an example: the real values are computed per trader (open item 1 in the brief).
 */

/** The two guardrails a nudge can offer. */
export type Guardrail = 'pnl' | 'tpsl'

/**
 * How much of the trader's own history we can use for this case:
 * - A: enough history, and the last time he did this he lost → the consequence is his own loss.
 * - B: enough history, the last time didn't lose → the consequence is what happened to other traders.
 * - C: thin history (no "usual" yet) → the headline is today's raw fact, no bars; the consequence as in B.
 * (D — the behaviour can't be scored — never shows its own sheet: the generic sheet fires instead.)
 */
export type DataState = 'A' | 'B' | 'C'

export type NudgeCaseId =
  | 'generic'
  | 'sizeUp' | 'orders' | 'flips' | 'burst' | 'money15' | 'bigOrder' | 'pace' | 'strike' | 'avgDown' | 'rareSession'
  | 'expiry' | 'deposit' | 'givingBack' | 'fomo' | 'returnBreak' | 'afterWin'

export type NudgeCase = {
  id: NudgeCaseId
  /** generic: fires with the revenge flag when nothing stands out · revenge: one of the 10 inputs of the v2.5 score ·
   *  moment: a journey moment that fires without the revenge flag. */
  kind: 'generic' | 'revenge' | 'moment'
  /** Where it fires: on the order pad (as he taps Buy / Sell) or on Positions (no order in hand). */
  where: 'order' | 'positions'
  /** The guardrail on the main button. */
  primary: Guardrail
  /** Today vs his usual (or vs the trade he lost), drawn as two bars. None = the fact isn't a multiple. */
  ratio?: number
  /** Traders who did this and lost more by the end of the day (%). None = not measured → no group line. */
  othersLostMore?: number
  /** State A: what he lost the last time he did this (₹). None = the case has no own-history version. */
  lastLoss?: number
  /** The group line compares with the same traders' other days, not the end of the day. */
  othersVs?: 'otherDays'
}

/** The 17 cases, values from the product team's compare file (2026-11-01). */
export const nudgeCases: NudgeCase[] = [
  { id: 'generic', kind: 'generic', where: 'positions', primary: 'pnl', othersLostMore: 67 },
  { id: 'sizeUp', kind: 'revenge', where: 'order', primary: 'pnl', ratio: 2, othersLostMore: 69, lastLoss: 2900 },
  { id: 'orders', kind: 'revenge', where: 'order', primary: 'pnl', ratio: 3, othersLostMore: 68, lastLoss: 3600 },
  { id: 'flips', kind: 'revenge', where: 'order', primary: 'pnl', ratio: 3, othersLostMore: 69, lastLoss: 3400 },
  { id: 'burst', kind: 'revenge', where: 'order', primary: 'pnl', ratio: 4, othersLostMore: 68, lastLoss: 4800 },
  { id: 'money15', kind: 'revenge', where: 'order', primary: 'pnl', ratio: 3, othersLostMore: 68, lastLoss: 6100 },
  { id: 'bigOrder', kind: 'revenge', where: 'order', primary: 'tpsl', ratio: 4, othersLostMore: 66, lastLoss: 5200 },
  { id: 'pace', kind: 'revenge', where: 'order', primary: 'pnl', ratio: 6, othersLostMore: 70, lastLoss: 2500 },
  { id: 'strike', kind: 'revenge', where: 'order', primary: 'tpsl', ratio: 10, othersLostMore: 72, lastLoss: 1700 },
  { id: 'avgDown', kind: 'revenge', where: 'order', primary: 'tpsl', othersLostMore: 66, lastLoss: 3900 },
  { id: 'rareSession', kind: 'revenge', where: 'order', primary: 'pnl', othersLostMore: 67, lastLoss: 2200 },
  { id: 'expiry', kind: 'moment', where: 'positions', primary: 'pnl', ratio: 3, othersLostMore: 66, lastLoss: 6800 },
  { id: 'deposit', kind: 'moment', where: 'order', primary: 'pnl', ratio: 5, lastLoss: 4100 },
  { id: 'givingBack', kind: 'moment', where: 'positions', primary: 'pnl', lastLoss: 2300 },
  { id: 'fomo', kind: 'moment', where: 'order', primary: 'tpsl', lastLoss: 1800 },
  { id: 'returnBreak', kind: 'moment', where: 'order', primary: 'pnl', ratio: 3, lastLoss: 9800 },
  { id: 'afterWin', kind: 'moment', where: 'order', primary: 'tpsl', ratio: 2, othersLostMore: 60, lastLoss: 2700, othersVs: 'otherDays' },
]

export const caseById = new Map(nudgeCases.map((c) => [c.id, c]))

/** The order being placed when the nudge shows — the F&O commodity options order pad's sample (fno/order-pad/data.ts). */
export type OrderSide = 'buy' | 'sell'
export type OrderProduct = 'delivery' | 'intraday'
export type OrderType = 'market' | 'limit' | 'sl'
export const orderContract = {
  name: 'Gold',
  contract: '5 OCT Fut',
  exchange: 'MCX',
  ltp: 153580,
  change: 2.62,
  /** Units per lot: the quantity steps by one lot. */
  lotSize: 100,
}
export const sellMargin = { margin: '7.00%', leverage: '14.3X' }
export const funds = { available: 1105002, required: 1075060 }
/** Intraday positions are squared off automatically at this time (MCX evening session). */
export const intradayCloseTime = '11:30 PM'
export const validities = ['Day', 'IOC']

/** Silent help: the TP/SL the order pad pre-fills (% of the entry price). */
export const prefilledTpsl = { targetPct: 20, stopPct: 10 }

/** P&L limit: quick amounts and the sample day (lost so far today). */
export const limitPresets = [10000, 25000, 50000]
export const defaultLimit = 25000
export const lossToday = 0
/** "Near the limit" sample: ₹21,000 of the ₹25,000 limit used. */
export const lossNearLimit = 21000

// ---- Trade protect sheets (Figma "Nudges", LM → F&O Playground 6928:31781, 23 Nov) -----------------------------------
// One bottom sheet for every use case: a picture of the moment, a tag (the P&L, or High Risk), the heading he'd
// recognise, one line, then what to do about it — a recommended tool, his figures, or the stop-loss price — and the tool
// as the primary button. Five use cases are drawn in Figma (two of them in two versions); the rest of the shortlist
// ("TP/SL and PnL Protect nudges — shortlisted triggers", 20 Nov) is laid out the same way. Every ₹ figure is an example.

/** The groups of the screen list: Figma's five designs first, then the shortlist's groups. */
export type ProtectGroup = 'figma' | 'money' | 'day' | 'trade' | 'days' | 'tools'
export const protectGroups: ProtectGroup[] = ['figma', 'money', 'day', 'trade', 'days', 'tools']

/** What the primary button opens: PnL Protect (today's loss limit) or TP/SL for this order. */
export type ProtectTool = 'pnl' | 'tpsl'

/** The picture. Illustrations are Figma's own artwork (shield, calendar, warning, candles), on a pink wave when
 *  `wave`; icons are L3-coloured glyphs on discs — `dot` (Figma's 80: a solid disc on a light one) or `hero` (100: the
 *  glyph on a light disc). */
export type ProtectArt =
  | { kind: 'illustration'; name: 'shield' | 'calendar' | 'warning' | 'candles'; wave?: boolean; riskLabel?: boolean }
  | { kind: 'icon'; style: 'dot' | 'hero'; glyph: 'trendDown' | 'trendUp' | 'warning' | 'wallet' | 'candles' | 'calendar' | 'shield' | 'flag'; tone: 'error' | 'success' }

/** What sits under the words (Figma's content slot). */
export type ProtectContent =
  | { kind: 'none' }
  /** "RECOMMENDED" over the tools he could use (Figma 1). */
  | { kind: 'list'; items: ('pnl' | 'tpsl')[] }
  /** One recommended tool with a Recommended tag (Figma 2). */
  | { kind: 'card'; item: 'pnl' | 'autoTpsl' }
  /** His figures side by side (Figma 4, 5): a label and a value each; the last one may carry an up arrow. */
  | { kind: 'stats'; stats: { label: string; value: string; tone?: 'loss' | 'profit'; up?: boolean }[] }
  /** The stop-loss price we'd set, with a Recommended tag (Figma 6). */
  | { kind: 'price'; value: string }

export type ProtectVersion = {
  art: ProtectArt
  /** The tag over the heading: a copy key (protect.tag.*) with its tone. */
  tag?: { key: 'highRisk' | 'pnl'; tone: 'loss' | 'profit' }
  /** The line under the heading: copy key protect.<id>.<body>, or the P&L figure in its colour (Figma 2). */
  body: 'body' | 'pnlLine'
  content: ProtectContent
}

export type ProtectUseCaseId =
  | 'risky' | 'sizeUp' | 'aggressive'
  | 'm1' | 'm2' | 'm11' | 'm7' | 'm8' | 'm17' | 'm9' | 'm13' | 'm14' | 'm15' | 'm10' | 'm18' | 'm19' | 'n3' | 'n12'

export type ProtectUseCase = {
  id: ProtectUseCaseId
  /** The shortlist's code (M1 … N12), or none for the three Figma cases that aren't on it. */
  code?: string
  group: ProtectGroup
  /** Figma node of its design, where there is one. */
  figma?: string
  tool: ProtectTool
  /** The secondary button: "Not now, place order" (an order in hand) or "Not now, I will trade on my own". */
  dismiss: 'placeOrder' | 'ownTrade'
  /** The figures the copy uses ({placeholders} in protect.<id>.*). */
  values: Record<string, string>
  /** Version 1 and version 2 (prototype setting "Trade protect · version"): Figma's two where it drew two; otherwise
   *  Figma's design and the other kind of picture (icon ↔ illustration), or for new cases an icon and an illustration. */
  versions: [ProtectVersion, ProtectVersion]
}

const pnlStat = (value: string) => ({ label: 'todayPnl', value, tone: 'loss' as const })

/** Every use case, Figma's first. */
export const protectUseCases: ProtectUseCase[] = [
  // Figma — 1 · High risk today: the shield, RECOMMENDED P&L Protect · TP/SL.
  { id: 'risky', group: 'figma', figma: '6925:29872', tool: 'tpsl', dismiss: 'placeOrder', values: {},
    versions: [
      { art: { kind: 'illustration', name: 'shield', wave: true, riskLabel: true }, body: 'body', content: { kind: 'list', items: ['pnl', 'tpsl'] } },
      { art: { kind: 'icon', style: 'hero', glyph: 'warning', tone: 'error' }, tag: { key: 'highRisk', tone: 'loss' }, body: 'body', content: { kind: 'list', items: ['pnl', 'tpsl'] } },
    ] },
  // Figma — 4 / 5 · Size-up after a loss: today's P&L, the order, how much bigger.
  { id: 'sizeUp', group: 'figma', figma: '6928:30386', tool: 'pnl', dismiss: 'placeOrder', values: {},
    versions: [
      { art: { kind: 'icon', style: 'dot', glyph: 'trendDown', tone: 'error' }, body: 'body',
        content: { kind: 'stats', stats: [pnlStat('−₹4,800'), { label: 'currentOrder', value: '₹18,000' }, { label: 'orderSize', value: '3x', tone: 'loss', up: true }] } },
      { art: { kind: 'illustration', name: 'warning', wave: true }, body: 'body',
        content: { kind: 'stats', stats: [pnlStat('−₹4,800'), { label: 'currentOrder', value: '₹18,000' }, { label: 'orderSize', value: '3x', tone: 'loss', up: true }] } },
    ] },
  // Figma — 7 · Trading more aggressively today: the candles.
  { id: 'aggressive', group: 'figma', figma: '6925:20058', tool: 'pnl', dismiss: 'placeOrder', values: {},
    versions: [
      { art: { kind: 'illustration', name: 'candles', wave: true }, body: 'body', content: { kind: 'none' } },
      { art: { kind: 'icon', style: 'dot', glyph: 'candles', tone: 'error' }, body: 'body', content: { kind: 'none' } },
    ] },

  // Money moves
  { id: 'm1', code: 'M1', group: 'money', tool: 'pnl', dismiss: 'ownTrade', values: { added: '₹5,000', line: '−₹9,800' },
    versions: [
      { art: { kind: 'icon', style: 'dot', glyph: 'wallet', tone: 'error' }, body: 'body',
        content: { kind: 'stats', stats: [{ label: 'todaySoFar', value: '−₹4,800', tone: 'loss' }, { label: 'added', value: '₹5,000' }, { label: 'exitAt', value: '−₹9,800', tone: 'loss' }] } },
      { art: { kind: 'illustration', name: 'warning', wave: true }, body: 'body',
        content: { kind: 'stats', stats: [{ label: 'todaySoFar', value: '−₹4,800', tone: 'loss' }, { label: 'added', value: '₹5,000' }, { label: 'exitAt', value: '−₹9,800', tone: 'loss' }] } },
    ] },
  { id: 'm2', code: 'M2', group: 'money', tool: 'pnl', dismiss: 'ownTrade', values: { added: '₹3,000', line: '−₹5,400' },
    versions: [
      { art: { kind: 'icon', style: 'dot', glyph: 'wallet', tone: 'error' }, body: 'body',
        content: { kind: 'stats', stats: [{ label: 'todaySoFar', value: '−₹2,400', tone: 'loss' }, { label: 'added', value: '₹3,000' }, { label: 'exitAt', value: '−₹5,400', tone: 'loss' }] } },
      { art: { kind: 'illustration', name: 'warning', wave: true }, body: 'body',
        content: { kind: 'stats', stats: [{ label: 'todaySoFar', value: '−₹2,400', tone: 'loss' }, { label: 'added', value: '₹3,000' }, { label: 'exitAt', value: '−₹5,400', tone: 'loss' }] } },
    ] },
  { id: 'm11', code: 'M11', group: 'money', tool: 'pnl', dismiss: 'ownTrade', values: { pnl: '−₹5,000' },
    versions: [
      { art: { kind: 'icon', style: 'hero', glyph: 'wallet', tone: 'error' }, tag: { key: 'pnl', tone: 'loss' }, body: 'body', content: { kind: 'card', item: 'pnl' } },
      { art: { kind: 'illustration', name: 'warning', wave: true }, tag: { key: 'pnl', tone: 'loss' }, body: 'body', content: { kind: 'none' } },
    ] },
  // The day's P&L
  { id: 'm7', code: 'M7', group: 'day', tool: 'pnl', dismiss: 'ownTrade', values: { pnl: '−₹6,200' },
    versions: [
      { art: { kind: 'illustration', name: 'calendar' }, body: 'pnlLine', content: { kind: 'card', item: 'pnl' } },
      { art: { kind: 'illustration', name: 'calendar', wave: true }, tag: { key: 'pnl', tone: 'loss' }, body: 'body', content: { kind: 'none' } },
    ] },
  { id: 'm8', code: 'M8', group: 'day', tool: 'pnl', dismiss: 'ownTrade', values: {},
    versions: [
      { art: { kind: 'icon', style: 'dot', glyph: 'trendDown', tone: 'error' }, body: 'body',
        content: { kind: 'stats', stats: [{ label: 'todayHigh', value: '+₹2,000', tone: 'profit' }, { label: 'now', value: '−₹300', tone: 'loss' }] } },
      { art: { kind: 'illustration', name: 'candles', wave: true }, body: 'body',
        content: { kind: 'stats', stats: [{ label: 'todayHigh', value: '+₹2,000', tone: 'profit' }, { label: 'now', value: '−₹300', tone: 'loss' }] } },
    ] },
  { id: 'm17', code: 'M17', group: 'day', tool: 'pnl', dismiss: 'ownTrade', values: { step: '₹500' },
    versions: [
      { art: { kind: 'icon', style: 'dot', glyph: 'trendDown', tone: 'error' }, body: 'body',
        content: { kind: 'stats', stats: [{ label: 'todayPeak', value: '+₹3,000', tone: 'profit' }, { label: 'now', value: '+₹1,500', tone: 'profit' }] } },
      { art: { kind: 'illustration', name: 'candles', wave: true }, body: 'body',
        content: { kind: 'stats', stats: [{ label: 'todayPeak', value: '+₹3,000', tone: 'profit' }, { label: 'now', value: '+₹1,500', tone: 'profit' }] } },
    ] },
  // Figma — 6 · Last 3 trades closed in a loss (M9): High Risk, the stop-loss price.
  { id: 'm9', code: 'M9', group: 'day', figma: '6928:31435', tool: 'tpsl', dismiss: 'ownTrade', values: { stop: '₹96' },
    versions: [
      { art: { kind: 'icon', style: 'hero', glyph: 'warning', tone: 'error' }, tag: { key: 'highRisk', tone: 'loss' }, body: 'body', content: { kind: 'price', value: '₹96.45' } },
      { art: { kind: 'illustration', name: 'warning', wave: true }, tag: { key: 'highRisk', tone: 'loss' }, body: 'body', content: { kind: 'price', value: '₹96.45' } },
    ] },
  // One trade
  { id: 'm13', code: 'M13', group: 'trade', tool: 'tpsl', dismiss: 'ownTrade', values: { contract: 'NIFTY 24000 CE', drop: '−52%' },
    versions: [
      { art: { kind: 'icon', style: 'hero', glyph: 'warning', tone: 'error' }, tag: { key: 'highRisk', tone: 'loss' }, body: 'body', content: { kind: 'price', value: '₹48.00' } },
      { art: { kind: 'illustration', name: 'warning', wave: true }, tag: { key: 'highRisk', tone: 'loss' }, body: 'body', content: { kind: 'price', value: '₹48.00' } },
    ] },
  { id: 'm14', code: 'M14', group: 'trade', tool: 'tpsl', dismiss: 'ownTrade', values: { contract: 'NIFTY 24000 CE' },
    versions: [
      { art: { kind: 'icon', style: 'hero', glyph: 'calendar', tone: 'error' }, body: 'body', content: { kind: 'price', value: '₹42.10' } },
      { art: { kind: 'illustration', name: 'calendar', wave: true }, body: 'body', content: { kind: 'price', value: '₹42.10' } },
    ] },
  { id: 'm15', code: 'M15', group: 'trade', tool: 'tpsl', dismiss: 'ownTrade', values: { pnl: '−₹4,100' },
    versions: [
      { art: { kind: 'icon', style: 'hero', glyph: 'warning', tone: 'error' }, tag: { key: 'pnl', tone: 'loss' }, body: 'body', content: { kind: 'price', value: '₹88.20' } },
      { art: { kind: 'illustration', name: 'warning', wave: true }, tag: { key: 'pnl', tone: 'loss' }, body: 'body', content: { kind: 'price', value: '₹88.20' } },
    ] },
  // Across days — Figma 2 / 3 · Yesterday was his biggest loss day (M10).
  { id: 'm10', code: 'M10', group: 'days', figma: '6928:30718', tool: 'pnl', dismiss: 'placeOrder', values: { pnl: '−₹4,800' },
    versions: [
      { art: { kind: 'illustration', name: 'calendar' }, body: 'pnlLine', content: { kind: 'card', item: 'pnl' } },
      { art: { kind: 'illustration', name: 'calendar', wave: true }, tag: { key: 'pnl', tone: 'loss' }, body: 'body', content: { kind: 'none' } },
    ] },
  { id: 'm18', code: 'M18', group: 'days', tool: 'tpsl', dismiss: 'placeOrder', values: { pnl: '+₹8,400' },
    versions: [
      { art: { kind: 'icon', style: 'dot', glyph: 'trendUp', tone: 'success' }, body: 'pnlLine', content: { kind: 'price', value: '₹96.45' } },
      { art: { kind: 'icon', style: 'hero', glyph: 'shield', tone: 'success' }, tag: { key: 'pnl', tone: 'profit' }, body: 'body', content: { kind: 'price', value: '₹96.45' } },
    ] },
  { id: 'm19', code: 'M19', group: 'days', tool: 'pnl', dismiss: 'placeOrder', values: {},
    versions: [
      { art: { kind: 'illustration', name: 'calendar' }, body: 'body', content: { kind: 'card', item: 'pnl' } },
      { art: { kind: 'illustration', name: 'calendar', wave: true }, body: 'body', content: { kind: 'none' } },
    ] },
  // His positions and his tools
  { id: 'n3', code: 'N3', group: 'tools', tool: 'pnl', dismiss: 'ownTrade', values: { count: '2' },
    versions: [
      { art: { kind: 'illustration', name: 'shield', wave: true }, body: 'body', content: { kind: 'card', item: 'pnl' } },
      { art: { kind: 'icon', style: 'hero', glyph: 'shield', tone: 'error' }, body: 'body', content: { kind: 'card', item: 'pnl' } },
    ] },
  { id: 'n12', code: 'N12', group: 'tools', tool: 'tpsl', dismiss: 'ownTrade', values: { contract: 'NIFTY 24000 CE', price: '₹120', pct: '+18%' },
    versions: [
      { art: { kind: 'icon', style: 'dot', glyph: 'flag', tone: 'success' }, body: 'body', content: { kind: 'card', item: 'autoTpsl' } },
      { art: { kind: 'icon', style: 'hero', glyph: 'shield', tone: 'success' }, body: 'body', content: { kind: 'card', item: 'autoTpsl' } },
    ] },
]

export const protectById = new Map(protectUseCases.map((p) => [p.id, p]))
```

### `src/flows/nudges/index.tsx`

```tsx
import type { Flow, Go } from '../types'
import { t } from './copy'
import { lossNearLimit, protectUseCases } from './data'
import { nudgeOptions, protectScreenIds } from './options'
import { OrderPad } from './screens/OrderPad'

/** Back to wherever the order pad was opened from; the Gold MINI asset page (fno-21) when opened directly. */
const back = (go: Go) => () => { if (window.history.length > 1) window.history.back(); else go('fno-21') }

/**
 * PLAYGROUND — overtrading nudges (product team draft, 2026-10-30). Not a Figma flow: built from the brief in
 * playground/overtrading-nudges/README.md. Each screen is the order pad in one state; within a
 * screen, sheet → sheet changes swap over the same page.
 */
export const nudges: Flow = {
  id: 'nudges', title: 'Overtrading nudges (playground)',
  description: 'Journey-aware P&L limit and TP/SL prompts: silent help on the order pad, and one nudge sheet when the revenge flag and the journey engine agree.',
  figmaFile: '',
  options: nudgeOptions,
  sections: [
    { id: 'meter', title: 'Risk meter' },
    { id: 'figma', title: t('protect.section', { group: t('protect.group.figma') }) },
    { id: 'money', title: t('protect.section', { group: t('protect.group.money') }) },
    { id: 'day', title: t('protect.section', { group: t('protect.group.day') }) },
    { id: 'trade', title: t('protect.section', { group: t('protect.group.trade') }) },
    { id: 'days', title: t('protect.section', { group: t('protect.group.days') }) },
    { id: 'tools', title: t('protect.section', { group: t('protect.group.tools') }) },
  ],
  screens: [
    { id: 'nudges-01', section: 'meter', name: 'Order pad · silent help', figma: '8671:18433', note: 'The default — no interruption. The F&O commodity order pad (fno-25) as it is, plus silent help: “Set TPSL” becomes a TP/SL row, pre-filled and on (Target +20% · Stop-loss −10%); “Set a loss limit for today” is the first line of the dock. Buy fires the nudge picked in the settings (Case, Data state), once: the shared cap is 1 per session.', render: (go) => <OrderPad nudge="options" onBack={back(go)} /> },
    { id: 'nudges-02', section: 'meter', name: 'Nudge · from settings', figma: '', note: 'The one nudge sheet — the risk meter — filled by the case and data state picked in the settings. Pills on the floating switcher: Meter (4f Soft dial · 4g Blocks), Risk level, Meter layout, Meter fill, Case, State.', render: (go) => <OrderPad nudge="options" initialSheet="nudge" onBack={back(go)} /> },
    { id: 'nudges-03', section: 'meter', name: 'Nudge · generic', figma: '', note: 'Fires on Positions with the revenge flag when no single behaviour stands out, or the trader is too new to compare (state D). The meter and its own fact under it. Dismiss says just “Not now” (no order in hand).', render: (go) => <OrderPad nudge={{ caseId: 'generic', state: 'B' }} initialSheet="nudge" onBack={back(go)} /> },
    { id: 'nudges-04', section: 'meter', name: 'Nudge · size-up · A (own loss)', figma: '', note: 'Size-up after a loss, own history and last loss (A): the meter at high risk, “You are placing a bigger order right after a loss”.', render: (go) => <OrderPad nudge={{ caseId: 'sizeUp', state: 'A' }} initialSheet="nudge" onBack={back(go)} /> },
    { id: 'nudges-05', section: 'meter', name: 'Nudge · orders today · B', figma: '', note: 'Orders today, own history (B): the meter, and the fact “3X more orders than usual today” under it.', render: (go) => <OrderPad nudge={{ caseId: 'orders', state: 'B' }} initialSheet="nudge" onBack={back(go)} /> },
    { id: 'nudges-06', section: 'meter', name: 'Nudge · orders today · C (thin history)', figma: '', note: 'Too few past sessions for “your usual”: the fact under the meter is today’s raw fact (“14 orders today”), no multiple.', render: (go) => <OrderPad nudge={{ caseId: 'orders', state: 'C' }} initialSheet="nudge" onBack={back(go)} /> },
    { id: 'nudges-07', section: 'meter', name: 'Nudge · averaging down (TP/SL first)', figma: '', note: 'Averaging down: the main button is TP/SL; the fact under the meter is the case\'s own (no multiple).', render: (go) => <OrderPad nudge={{ caseId: 'avgDown', state: 'B' }} initialSheet="nudge" onBack={back(go)} /> },
    { id: 'nudges-08', section: 'meter', name: 'Set today’s loss limit', figma: '', note: 'From the nudge’s “Set a loss limit for today” or the order pad dock. Pre-filled ₹25,000, quick amounts as pill tabs. Set limit → back to the pad with the limit shown.', render: (go) => <OrderPad nudge={{ caseId: 'sizeUp', state: 'A' }} initialSheet="pnl" onBack={back(go)} /> },
    { id: 'nudges-09', section: 'meter', name: 'TP/SL for this order', figma: '', note: 'From the nudge’s “Add TP/SL to this order” or the TP/SL row. Target and stop-loss in %, the exit price under each.', render: (go) => <OrderPad nudge={{ caseId: 'avgDown', state: 'B' }} initialSheet="tpsl" onBack={back(go)} /> },
    { id: 'nudges-10', section: 'meter', name: 'Order pad · limit set', figma: '', note: 'Silent help once a limit exists: “₹25,000 left of today’s loss limit” with a bar in the dock (tap to change it).', render: (go) => <OrderPad limit={25000} onBack={back(go)} /> },
    { id: 'nudges-11', section: 'meter', name: 'Order pad · close to the limit', figma: '', note: '₹21,000 of ₹25,000 used: the bar and the line turn warning. Still no interruption.', render: (go) => <OrderPad limit={25000} loss={lossNearLimit} onBack={back(go)} /> },
    // Trade protect (Figma "Nudges" 6928:31781, 23 Nov): one sheet per use case, over the order pad (as Figma draws it).
    ...protectUseCases.map((p, i) => {
      const say = (k: string) => t(k as Parameters<typeof t>[0], p.values)
      return {
        id: protectScreenIds[i], section: p.group, badge: 'new' as const, badgeNote: 'Trade protect sheet (Figma Nudges, 23 Nov)', figma: p.figma ?? '',
        name: `${p.code ? `${p.code} · ` : ''}${say(`protect.${p.id}.name`)}`,
        note: `Trade protect${p.code ? `, ${p.code}` : ''}: ${say(`protect.${p.id}.name`)}. "${say(`protect.${p.id}.heading`)}". ${p.figma ? 'Drawn in Figma (Nudges).' : 'Not drawn in Figma: laid out like the Figma designs.'} Main button "${say(`protect.${p.id}.cta`)}" opens ${p.tool === 'pnl' ? "PnL Protect (today's loss limit)" : 'TP/SL for this order'}; "${say(`protect.dismiss.${p.dismiss}`)}" ${p.dismiss === 'placeOrder' ? 'places the order' : 'closes the sheet'}. Setting Trade protect · version: V1 / V2.`,
        render: (go: Go) => <OrderPad protect={p.id} initialSheet="protect" onBack={back(go)} />,
      }
    }),
  ],
}
```

### `src/flows/nudges/options.ts`

```ts
import { t } from './copy'
import { nudgeCases, protectUseCases } from './data'

type Key = Parameters<typeof t>[0]
const onOff = [{ value: 'off', label: t('option.everyBuyOff') }, { value: 'on', label: t('option.everyBuyOn') }]

/**
 * PROTOTYPE ONLY: the flow's settings (preview panel / phone settings sheet) and, for the ones that change the sheet,
 * the floating switcher over the open nudge (components/SheetSwitcher). A real app ships one version.
 */
// Size-up after a loss is the default and heads the list.
export const caseOption = { id: 'case', group: 'Nudge', label: t('option.case'), picker: 'dropdown' as const, values: [...nudgeCases].sort((a, b) => Number(b.id === 'sizeUp') - Number(a.id === 'sizeUp')).map((c) => ({ value: c.id, label: t(`case.${c.id}.name` as Key) })), default: 'sizeUp' }
export const stateOption = { id: 'state', group: 'Nudge', label: t('option.state'), picker: 'dropdown' as const, values: [{ value: 'A', label: t('option.stateA') }, { value: 'B', label: t('option.stateB') }, { value: 'C', label: t('option.stateC') }], default: 'A' }
/** The meter (19 Nov, cut down to the two in use): 4f Soft dial (default) or 4g Blocks; 20 Nov: 4h / 4i the Figma
 *  speedometer (0–100 or Low–High scale, its own layout). A stored older style falls back to the default (activeMeter). */
export const meterOption = { id: 'meter', group: 'Nudge', label: t('option.meter'), picker: 'dropdown' as const, values: [{ value: 'soft', label: t('option.meterSoft') }, { value: 'blocks', label: t('option.meterBlocks') }, { value: 'gauge', label: t('option.meterGauge') }, { value: 'gaugeWords', label: t('option.meterGaugeWords') }], default: 'soft' }
export const activeMeter = (value: string) => meterOption.values.some((v) => v.value === value) ? value : meterOption.default

/** Where the reading stops (19 Nov) — the meter's three versions. */
export const meterLevelOption = { id: 'meterLevel', group: 'Nudge', label: t('option.meterLevel'), picker: 'dropdown' as const, values: [{ value: 'danger', label: t('option.levelDanger') }, { value: 'caution', label: t('option.levelCaution') }, { value: 'safe', label: t('option.levelSafe') }], default: 'danger' }

/** Where the text sits around the meter (19 Nov): Text first · Meter first · Tag first · With multiple. */
export const meterLayoutOption = { id: 'meterLayout', group: 'Nudge', label: t('option.meterLayout'), picker: 'dropdown' as const, values: [{ value: 'text', label: t('option.meterLayoutText') }, { value: 'meter', label: t('option.meterLayoutMeter') }, { value: 'tag', label: t('option.meterLayoutTag') }, { value: 'number', label: t('option.meterLayoutNumber') }], default: 'text' }
/** Soft dial only (19 Nov): the whole ring changes colour as the needle moves, or each part keeps the colour
 *  it was filled with, blended (green → yellow → red); or (20 Nov) blended and cut into three blocks where the colour
 *  changes; and that with Low · Medium · High round it, as on the speedometer; and (20 Nov) the one-colour ring with the same scale and tag. */
export const meterFillOption = { id: 'meterFill', group: 'Nudge', label: t('option.meterFill'), picker: 'dropdown' as const, values: [{ value: 'whole', label: t('option.meterFillWhole') }, { value: 'blend', label: t('option.meterFillBlend') }, { value: 'split', label: t('option.meterFillSplit') }, { value: 'splitWords', label: t('option.meterFillSplitWords') }, { value: 'wholeWords', label: t('option.meterFillWholeWords') }], default: 'whole' }

/** Trade protect sheets (Figma "Nudges", 23 Nov): one screen per use case, nudges-12 … nudges-29, Figma's five first. */
export const protectScreenIds = protectUseCases.map((_, i) => `nudges-${12 + i}`)
/** Their version: Figma's two drawings where it has two (M10 · size-up), else Figma's design and the other picture
 *  (icon ↔ illustration). A floating V1 / V2 button on those screens flips it while presenting. */
export const protectVersionOption = {
  id: 'protectVersion', group: 'Trade protect', label: t('option.protectVersion'), picker: 'dropdown' as const,
  values: [{ value: 'v1', label: t('option.protectVersion1') }, { value: 'v2', label: t('option.protectVersion2') }], default: 'v1',
  floatOn: protectScreenIds,
  quickSwitch: { on: protectScreenIds, values: [{ value: 'v1', label: t('option.protectVersion1'), short: 'V1' }, { value: 'v2', label: t('option.protectVersion2'), short: 'V2' }] },
}

export const nudgeOptions = [
  caseOption,
  stateOption,
  meterOption,
  meterLevelOption,
  meterLayoutOption,
  meterFillOption,
  protectVersionOption,
  { id: 'everyBuy', group: 'Nudge', label: t('option.everyBuy'), picker: 'toggle' as const, values: onOff, default: 'on' },
  { id: 'vibrate', group: 'Nudge', label: t('option.vibrate'), picker: 'toggle' as const, values: onOff, default: 'on' },
  { id: 'actions', group: 'Nudge', label: t('option.actions'), values: [{ value: 'one', label: t('option.actionsOne') }, { value: 'two', label: t('option.actionsTwo') }], default: 'one' },
]
```

### `src/flows/nudges/screens/OrderPad.module.css`

```css
/* The F&O commodity options order pad (fno/order-pad, Figma 8671:18433) + the nudge's silent help, on L3 tokens. */
.contract { display: flex; flex-direction: column; align-items: flex-start; gap: var(--l3-spacing-02); color: var(--l3-content-primary); }
.contractName { display: inline-flex; align-items: center; gap: var(--l3-spacing-04); font: var(--l3-text-heading-14); }
.expiry { margin-left: var(--l3-spacing-04); font: var(--l3-text-label-12); color: var(--l3-content-tertiary); }
.contractPrice { display: inline-flex; align-items: center; gap: var(--l3-spacing-08); font: var(--l3-text-label-12); }
.exchange { font: var(--l3-text-label-12); color: var(--l3-content-primary); }

.body { padding: var(--l3-spacing-16); }
.validity.validity { min-height: var(--l3-size-32); border: 1px solid var(--l3-border-dark); border-radius: var(--l3-radius-full); padding-inline: var(--l3-spacing-12); }

/* Margin · Leverage (Sell): a grey strip. */
.margin { display: flex; justify-content: space-between; padding: var(--l3-spacing-12); border-radius: var(--l3-radius-12); background: var(--l3-surface-secondary); font: var(--l3-text-label-12); }
.margin strong, .funds strong { font: var(--l3-text-heading-12); color: var(--l3-content-primary); }
.muted { color: var(--l3-content-tertiary); }

/* A field row: label, value / hint, compact stepper at the right — bordered, 12 radius. */
.field { display: flex; align-items: center; gap: var(--l3-spacing-08); min-height: var(--l3-size-40); padding: var(--l3-spacing-04) var(--l3-spacing-04) var(--l3-spacing-04) var(--l3-spacing-12); border: 1px solid var(--l3-border-light); border-radius: var(--l3-radius-08); }
.fieldLabel { flex: 1; font: var(--l3-text-label-12); color: var(--l3-content-secondary); }
.fieldValue { font: var(--l3-text-heading-12); }
.unit { display: inline-flex; align-items: center; gap: var(--l3-spacing-02); padding: 0; border: 0; background: none; color: var(--l3-content-primary); font: var(--l3-text-label-12); cursor: pointer; }
.hint { flex: 1; font: var(--l3-text-label-12); color: var(--l3-content-tertiary); }
/* Steppers are the L3 Stepper Small as it is (dark + / −) — the design system's style wins over Figma's grey / blue. */

.tpslRow { display: flex; align-items: center; gap: var(--l3-spacing-12); padding: var(--l3-spacing-12); border: 1px solid var(--l3-border-light); border-radius: var(--l3-radius-08); }
.tpslText { flex: 1; display: flex; flex-direction: column; align-items: flex-start; gap: var(--l3-spacing-04); padding: 0; border: 0; background: none; color: var(--l3-content-primary); text-align: left; cursor: pointer; }
.tpslHead { display: inline-flex; align-items: center; gap: var(--l3-spacing-08); font: var(--l3-text-heading-12); }
.tpslValue { font: var(--l3-text-label-12); color: var(--l3-content-secondary); }

/* Dock: optional auto-close note (intraday), then Avail. · Req and the action. */
.dock { background: var(--l3-surface-primary); }
.autoClose { margin: 0; padding: var(--l3-spacing-12) var(--l3-spacing-16); font: var(--l3-text-label-12); color: var(--l3-content-tertiary); text-align: center; }
.dockBody { display: flex; flex-direction: column; gap: var(--l3-spacing-12); padding: var(--l3-spacing-12) var(--l3-spacing-16) var(--l3-spacing-16); border-top: 1px solid var(--l3-border-light); }
.funds { display: flex; justify-content: space-between; font: var(--l3-text-label-12); }


/* Silent help · loss limit, first in the dock: what's left of today's limit (bar), or the link to set one. */
.limit, .limitAdd { display: flex; width: 100%; padding: 0; border: 0; background: none; cursor: pointer; text-align: left; }
.limit { flex-direction: column; gap: var(--l3-spacing-08); }
.limitText, .limitAdd { display: inline-flex; align-items: center; gap: var(--l3-spacing-04); font: var(--l3-text-label-12); color: var(--l3-content-secondary); }
.limitText[data-tone='warning'] { color: var(--l3-content-accent-warning-default); }
.limitAdd { min-height: var(--l3-size-32); color: var(--l3-content-accent-discover-default); }
```

### `src/flows/nudges/screens/OrderPad.tsx`

```tsx
import { useState } from 'react'
import { Actionbar } from '@l3/components/Actionbar'
import { Aerobar } from '@l3/components/Aerobar'
import { Button } from '@l3/components/Button'
import { Icon } from '@l3/components/Icon'
import { PriceChange } from '@l3/components/PriceChange'
import { ProgressBar } from '@l3/components/ProgressBar'
import { Select } from '@l3/components/Select'
import { Stack } from '@l3/components/Stack'
import { Stepper } from '@l3/components/Stepper'
import { Switch } from '@l3/components/Switch'
import { Tabs } from '@l3/components/Tabs'
import { Tag } from '@l3/components/Tag'
import { lmSwitchArrowVertical } from '@l3/icons/lemonnade'
import { msChevronRight, msShield } from '@l3/icons/material'
import { inr } from '../../../shared/data/format'
import { SHOWCASE, useFlowOption } from '../../../shared/prototype'
import type { RiskLevel } from '../sheets/SoftDial'
import { Screen } from '../../../shared/ui/Screen'
import { t } from '../copy'
import { activeMeter } from '../options'
import { caseById, defaultLimit, funds, intradayCloseTime, lossToday, orderContract, prefilledTpsl, sellMargin, validities, type DataState, type NudgeCaseId, type ProtectUseCaseId, protectById, type OrderProduct, type OrderSide, type OrderType } from '../data'
import { LossLimitSheet, TpslSheet } from '../sheets/GuardrailSheets'
import { NudgeSheet, type MeterLayout, type MeterStyle } from '../sheets/NudgeSheet'
import { TradeProtectSheet, type ProtectVersionId } from '../sheets/TradeProtectSheet'
import { SheetSwitcher } from '../components/SheetSwitcher'
import styles from './OrderPad.module.css'

type Modal = { kind: 'nudge' } | { kind: 'pnl' } | { kind: 'tpsl' } | { kind: 'protect' }

type Props = {
  side?: OrderSide
  product?: OrderProduct
  type?: OrderType
  /** The nudge that fires on Buy / Sell (once — the shared cap is 1 per session). `'options'`: the case and state
   *  picked in the prototype settings. Leave out for an order with no nudge. */
  nudge?: { caseId: NudgeCaseId; state: DataState } | 'options'
  /** Opens with this sheet up (a direct link). */
  initialSheet?: 'nudge' | 'pnl' | 'tpsl' | 'protect'
  /** A trade protect sheet (a use case from Figma "Nudges" or the shortlist), up when the pad opens (initialSheet 'protect'). */
  protect?: ProtectUseCaseId
  /** Today's loss limit, if one is set (null: none yet). */
  limit?: number | null
  /** Lost so far today, against the limit. */
  loss?: number
  onBack: () => void
}

/**
 * The F&O commodity options order pad (fno/order-pad, Figma 8671:18433) — the same screen, copied because flows
 * can't import each other — with the nudge's two layers added:
 * - Silent help (always there): "Set TPSL" becomes a TP/SL row that is pre-filled and switched on; the dock shows how
 *   much of today's loss limit is left (or a link to set one) above Avail. · Req.
 * - The nudge sheet (only when both engines agree): fires on Buy / Sell, once. Not now places the order; a guardrail
 *   opens its sheet in place (sheet → sheet), and saving returns to the pad.
 */
export function OrderPad({ side = 'buy', product: initialProduct = 'delivery', type: initialType = 'market', nudge, protect, initialSheet, limit: initialLimit = null, loss = lossToday, onBack }: Props) {
  const c = orderContract
  const caseValue = useFlowOption('nudges', 'case', 'sizeUp')
  // A stored Layout 5 version ('everyone' … 'compact', removed 19 Nov) isn't a case: show the default case for it.
  const optionCase = (caseById.has(caseValue as NudgeCaseId) ? caseValue : 'sizeUp') as NudgeCaseId
  const optionState = useFlowOption('nudges', 'state', 'A') as DataState
  const actions = useFlowOption('nudges', 'actions', 'one') as 'one' | 'two'
  // Prototype setting: fire the nudge on every Buy / Sell instead of once (the real cap is 1 per session).
  const meterStyle = activeMeter(useFlowOption('nudges', 'meter', 'soft')) as MeterStyle
  const meterLevel = useFlowOption('nudges', 'meterLevel', 'danger') as RiskLevel
  const meterLayout = useFlowOption('nudges', 'meterLayout', 'text') as MeterLayout
  const meterFill = useFlowOption('nudges', 'meterFill', 'whole')
  const meterBlend = meterFill === 'blend' || meterFill === 'split' || meterFill === 'splitWords'
  const meterSplit = meterFill === 'split' || meterFill === 'splitWords'
  // Low · Medium · High round the dial and the risk tag in it: on the 3-block or the one-colour ring.
  const meterWords = meterFill === 'splitWords' || meterFill === 'wholeWords'
  const everyBuy = useFlowOption('nudges', 'everyBuy', 'on') === 'on'
  const vibrate = useFlowOption('nudges', 'vibrate', 'on') === 'on'
  // A screen with a fixed case (03–09) shows it until the case or data state is changed in the settings; from then on
  // it follows the settings too, so the dropdown always changes the sheet that's open.
  const [opened] = useState(`${optionCase}.${optionState}`)
  const changed = `${optionCase}.${optionState}` !== opened
  const picked = nudge === undefined ? undefined
    : nudge === 'options' || changed ? { caseId: optionCase, state: optionState } : nudge
  const fired = picked

  const [product, setProduct] = useState<OrderProduct>(initialProduct)
  const [type, setType] = useState<OrderType>(initialType)
  const [validity, setValidity] = useState(validities[0])
  const [lots, setLots] = useState(false)
  const [quantity, setQuantity] = useState(c.lotSize)
  const [limitPct, setLimitPct] = useState(20.3)
  const [triggerPct, setTriggerPct] = useState(20.3)
  const [tpslOn, setTpslOn] = useState(true)
  const [tpsl, setTpsl] = useState(prefilledTpsl)
  const [limit, setLimit] = useState<number | null>(initialLimit)
  const [modal, setModal] = useState<Modal | null>(initialSheet ? { kind: initialSheet } : null)
  const [nudged, setNudged] = useState(initialSheet !== undefined)
  const [toast, setToast] = useState<string | null>(null)
  const buy = side === 'buy'
  const priceAt = (pct: number) => inr(Math.round(c.ltp * (buy ? 1 - pct / 1000 : 1 + pct / 1000)), 0)
  const priceRow = (label: string, pct: number, setPct: (n: number) => void) => <div className={styles.field}>
    <span className={styles.fieldLabel}>{label}</span>
    <span className={styles.fieldValue}>{priceAt(pct)}</span>
    <Stepper size="sm" className={styles.stepper} label={t('order.offset')} value={pct} onChange={setPct} min={0} step={0.1} format={(n) => `${n.toFixed(1)}%`} />
  </div>

  const place = () => { setModal(null); setToast(t('order.placed', { side: t(buy ? 'order.buy' : 'order.sell'), name: c.name, contract: c.contract })) }
  const submit = () => { if (fired && (!nudged || everyBuy)) { setNudged(true); setModal({ kind: 'nudge' }) } else place() }

  // Trade protect: the tool on the main button opens its own sheet in place (PnL Protect or TP/SL); Not now closes it.
  // "Not now, place order" places it (as the risk meter's Not now); "Not now, I will trade on my own" just closes.
  const protectVersion = useFlowOption('nudges', 'protectVersion', 'v1') as ProtectVersionId
  const protectCase = protect ? protectById.get(protect)! : undefined
  const protectSheet = protectCase && modal?.kind === 'protect'
    ? <TradeProtectSheet key={`${protectCase.id}-${protectVersion}`} useCaseId={protectCase.id} version={protectVersion}
      onTool={() => setModal({ kind: protectCase.tool })} onDismiss={protectCase.dismiss === 'placeOrder' ? place : () => setModal(null)} />
    : undefined

  const sheet = protectSheet ?? (modal?.kind === 'nudge' && fired
    ? <NudgeSheet caseId={fired.caseId} state={fired.state} meterStyle={meterStyle} meterLevel={meterLevel} meterLayout={meterLayout} meterBlend={meterBlend} meterSplit={meterSplit} meterWords={meterWords} vibrate={vibrate} actions={actions} onGuardrail={(g) => setModal({ kind: g })} onNotNow={place} />
    : modal?.kind === 'pnl'
      ? <LossLimitSheet initial={limit ?? defaultLimit} onClose={() => setModal(null)} onSave={(amount) => { setLimit(amount); setModal(null); setToast(t('pnl.saved', { amount: inr(amount, 0) })) }} />
      : modal?.kind === 'tpsl'
        ? <TpslSheet onClose={() => setModal(null)} onSave={(v) => { setTpsl(v); setTpslOn(true); setModal(null); setToast(t('tpsl.saved')) }} />
        : undefined)

  const top = <Actionbar onBack={onBack} backLabel={t('order.back')}
    title={<span className={styles.contract}>
      <span className={styles.contractName}>{c.name}<Icon icon={lmSwitchArrowVertical} size={16} /><span className={styles.expiry}>{c.contract}</span></span>
      <span className={styles.contractPrice}>{inr(c.ltp, 2)}<PriceChange value={c.change} unit="percent" size="sm" /></span>
    </span>}
    actions={<span className={styles.exchange}>{c.exchange}</span>}
    bottom={<Tabs aria-label={t('order.product')} value={product} onChange={setProduct} items={[{ value: 'delivery', label: t('order.delivery') }, { value: 'intraday', label: t('order.intraday') }]} />} />

  // Silent help in the dock: what's left of today's loss limit, or a link to set one.
  const left = limit !== null ? Math.max(limit - loss, 0) : 0
  const near = limit !== null && left <= limit * 0.2
  const lossLimit = limit !== null
    ? <button type="button" className={styles.limit} onClick={() => setModal({ kind: 'pnl' })}>
      <ProgressBar size="sm" value={(loss / limit) * 100} status={near ? 'warning' : 'default'} label={t('silent.limitBar')} />
      <span className={styles.limitText} data-tone={near ? 'warning' : undefined}><Icon icon={msShield} size={16} />{t('silent.limitLeft', { left: inr(left, 0) })}</span>
    </button>
    : <button type="button" className={styles.limitAdd} onClick={() => setModal({ kind: 'pnl' })}>
      <Icon icon={msShield} size={16} />{t('silent.limitAdd')}<Icon icon={msChevronRight} size={16} />
    </button>

  const dock = <div className={styles.dock} data-surface="primary">
    {product === 'intraday' && <p className={styles.autoClose}>{t('order.autoClose', { time: intradayCloseTime })}</p>}
    <div className={styles.dockBody}>
      {lossLimit}
      <div className={styles.funds}>
        <span><span className={styles.muted}>{t('order.available')}</span> <strong>{inr(funds.available, 0)}</strong></span>
        <span><span className={styles.muted}>{t('order.required')}</span> <strong>{inr(funds.required, 0)}</strong></span>
      </div>
      <Button variant={buy ? 'brand' : 'sell'} size="lg" fullWidth onClick={submit}>{t(buy ? 'order.buy' : 'order.sell')}</Button>
    </div>
  </div>

  return <Screen top={top} bottom={dock} sheet={sheet}
    toast={toast ? <Aerobar floating type="success" heading={toast} onDismiss={() => setToast(null)} /> : undefined}>
    {!SHOWCASE && <SheetSwitcher open={fired !== undefined} />}
    <Stack gap="16" className={styles.body}>
      <Stack direction="horizontal" align="center" justify="between">
        <Tabs aria-label={t('order.type')} appearance="pill" size="md" value={type} onChange={setType} items={(['market', 'limit', 'sl'] as const).map((value) => ({ value, label: t(`order.${value}`) }))} />
        {type !== 'market' && <Select size="sm" aria-label={t('order.validity')} className={styles.validity} onClick={() => setValidity(validities[(validities.indexOf(validity) + 1) % validities.length])}>{validity}</Select>}
      </Stack>
      {!buy && <div className={styles.margin}><span><span className={styles.muted}>{t('order.margin')}</span> <strong>{sellMargin.margin}</strong></span><span><span className={styles.muted}>{t('order.leverage')}</span> <strong>{sellMargin.leverage}</strong></span></div>}
      <div className={styles.field}>
        <button type="button" className={styles.unit} aria-label={t('order.unitSwitch')} onClick={() => setLots(!lots)}>{t(lots ? 'order.lots' : 'order.quantity')}<Icon icon={lmSwitchArrowVertical} size={12} /></button>
        <span className={styles.hint}>{t('order.lotHint', { lot: c.lotSize })}</span>
        <Stepper size="sm" className={styles.stepper} label={t(lots ? 'order.lots' : 'order.quantity')} value={lots ? quantity / c.lotSize : quantity} onChange={(n) => setQuantity(lots ? n * c.lotSize : n)} min={lots ? 1 : c.lotSize} step={lots ? 1 : c.lotSize} />
      </div>
      {type === 'sl' && priceRow(t('order.trigger'), triggerPct, setTriggerPct)}
      {type !== 'market' && priceRow(t('order.limitPrice'), limitPct, setLimitPct)}
      {/* Silent help: the draft's "Set TPSL" link becomes a TP/SL that is already on and pre-filled. */}
      <div className={styles.tpslRow}>
        <button type="button" className={styles.tpslText} aria-label={t('silent.tpslEdit')} onClick={() => setModal({ kind: 'tpsl' })}>
          <span className={styles.tpslHead}>{t('silent.tpsl')}{tpslOn && <Tag size="sm" variant="secondary" color="success">{t('silent.prefilled')}</Tag>}</span>
          <span className={styles.tpslValue}>{tpslOn ? t('silent.tpslOn', { target: tpsl.targetPct, stop: tpsl.stopPct }) : t('silent.tpslOff')}</span>
        </button>
        <Switch aria-label={t('silent.tpslToggle')} checked={tpslOn} onChange={(e) => setTpslOn(e.target.checked)} />
      </div>
    </Stack>
  </Screen>
}
```

### `src/flows/nudges/sheets/BlockDial.module.css`

```css
/* 4g · Blocks (BlockDial.tsx), in the soft dial's design language. SVG drawing units. Resting styles = the end state;
   the component (Web Animations) runs the sweep, the tip's bloom colour and the level word; CSS runs the glows. */
.dial { margin: 0; }
/* The drawing area has room for the whole blurred glow (it reaches ~50 past the ring): 16 past the ring on each side
   (that's the sheet's edge) and 70 above the dial, so nothing draws outside the svg — mobile browsers (Safari) clip
   SVG content at the svg's box, overflow: visible or not, which cut the glow off in a hard edge (19 Nov). The svg is
   that much bigger and pulled back by negative margins (relative to the width, like the viewBox), so the dial sits
   exactly where it did and its box ends at the ring's base line: viewBox −16 −64 372 × 280 for the dial's 340 × 170. */
.svg {
  display: block;
  width: calc(100% * 372 / 340);
  height: auto;
  margin: calc(100% * -70 / 340) calc(100% * -16 / 340) calc(100% * -40 / 340);
  overflow: visible;
}

/* The sweep's resting point (the component animates it). */
.sweepStroke { fill: none; stroke: white; stroke-dasharray: 1; stroke-dashoffset: var(--sweep-rest); }

/* Layer blur per level, as on the soft dial: lighter than the level colour (mixed half with white); on as the fill
   reaches the level, off as it moves on; the last one stays and breathes. */
[data-tone='safe'] { --tone: color-mix(in srgb, var(--l3-surface-accent-success-default) 50%, var(--l3-static-white)); }
[data-tone='caution'] { --tone: color-mix(in srgb, var(--l3-surface-accent-warning-default) 50%, var(--l3-static-white)); }
[data-tone='danger'] { --tone: color-mix(in srgb, var(--l3-surface-accent-error-default) 50%, var(--l3-static-white)); }
.glow { fill: none; stroke: var(--tone); stroke-linecap: round; opacity: 0; animation: glowPass var(--glow-for) linear var(--glow-in) both; }
@keyframes glowPass { 0% { opacity: 0; } 20% { opacity: 0.55; } 70% { opacity: 0.45; } 100% { opacity: 0; } }
.glow[data-last] {
  opacity: 0.35;
  animation:
    fadeIn var(--l3-motion-duration-long) var(--l3-motion-easing-decelerate) var(--glow-in) backwards,
    breathe calc(var(--l3-motion-duration-long) * 4) var(--l3-motion-easing-standard) calc(var(--glow-in) + var(--glow-for)) 2;
}
@keyframes breathe { 50% { opacity: 0.6; } }
@keyframes fadeIn { from { opacity: 0; } }

/* The bloom riding the fill's tip (turns about the ring's centre with the sweep). Resting colour = the reached level. */
.turn { transform-box: view-box; transform-origin: 170px 176px; transform: rotate(var(--to-deg)); }
.bloom { fill: var(--l3-surface-accent-error-default); opacity: 0.4; animation: fadeIn var(--l3-motion-duration-medium) linear var(--bloom-in) backwards; }
.dial[data-level='safe'] .bloom { fill: var(--l3-surface-accent-success-default); }
.dial[data-level='caution'] .bloom { fill: var(--l3-surface-accent-warning-default); }

/* The level word: the reached level's word rests visible; the component swaps them on the way. */
.value { font: var(--l3-text-heading-36); fill: var(--l3-content-primary); animation: fadeIn var(--l3-motion-duration-long) var(--l3-motion-easing-decelerate) var(--word-in) backwards; }
.word { font: var(--l3-text-heading-20); fill: var(--l3-content-primary); opacity: 0; }
.dial[data-level='safe'] .word[data-word='safe'],
.dial[data-level='caution'] .word[data-word='caution'],
.dial[data-level='danger'] .word[data-word='danger'] { opacity: 1; }

@media (prefers-reduced-motion: reduce) {
  .dial * { animation: none !important; }
}
```

### `src/flows/nudges/sheets/BlockDial.tsx`

```tsx
import { useEffect, useId, useRef, type CSSProperties } from 'react'
import { t } from '../copy'
import { easeTimeAt, needleKeys, OVER, RUN, RUN_EASE, type RiskLevel } from './SoftDial'
import styles from './BlockDial.module.css'

/**
 * 4g · Blocks (19 Nov, from the user's reference image; in the soft dial's design language). The half ring as 13 thick
 * rounded blocks with gaps, grey at rest. A fill sweeps in from the left the way the soft dial's needle moves — fast,
 * eased, a little past the reading, back and forth, settling on the last lit block's edge — and the blocks it covers
 * show their level's colour: green (safe), yellow (caution), red (high risk), each with depth (deep inside, light
 * outside; no glass, 19 Nov). The block under the fill's head lifts outward and settles back as it moves on — a wave
 * that travels with the fill. Behind, each level's blurred glow comes on as
 * the fill reaches it; a bloom rides the fill's tip in the colour of the level it's in. In the middle, only the level
 * word, swapping Safe → Caution → High risk as the fill passes. Reduced motion: the end state.
 */
const CX = 170
const CY = 176
const RO = 158
const RI = 104
const RM = (RO + RI) / 2
const BAND = RO - RI
const COUNT = 13
const GAP = 0.018
const ROUND = 7 // corner rounding: each block is drawn this much smaller and stroked this wide, round joins
const SAFE_END = 0.45
const CAUTION_END = 0.65
const LEVEL_AT = { safe: 0.3, caution: 0.56 } as const
/** Fast (19 Nov, "it should fill up fast"): the run to the overshoot takes 0.6 of 1.8 s. */
const DELAY = 250
const TRAVEL = 1800
/** How far the block under the fill's head lifts outward (drawing units). */
const LIFT = 7
/** Progress (0–1) of a cubic-bezier easing at time fraction x. */
function easeTimeInverse(x: number, [x1, y1, x2, y2]: number[]) {
  const b = (s: number, p: number, q: number) => 3 * p * s * (1 - s) ** 2 + 3 * q * s ** 2 * (1 - s) + s ** 3
  let lo = 0, hi = 1
  for (let i = 0; i < 28; i++) { const m = (lo + hi) / 2; if (b(m, x1, x2) < x) lo = m; else hi = m }
  return b((lo + hi) / 2, y1, y2)
}

function point(f: number, r: number) {
  const a = Math.PI * (1 - f)
  return [CX + r * Math.cos(a), CY - r * Math.sin(a)] as const
}
function arc(from: number, to: number, r: number) {
  const [x1, y1] = point(from, r)
  const [x2, y2] = point(to, r)
  return `M ${x1} ${y1} A ${r} ${r} 0 0 1 ${x2} ${y2}`
}
/** One block: an annular sector from f0 to f1, inset by ROUND / 2 so its round stroke brings it back to size. */
function block(f0: number, f1: number) {
  const inset = ROUND / 2
  const ro = RO - inset
  const ri = RI + inset
  const [x1, y1] = point(f0 + inset / (Math.PI * ro), ro)
  const [x2, y2] = point(f1 - inset / (Math.PI * ro), ro)
  const [x3, y3] = point(f1 - inset / (Math.PI * ri), ri)
  const [x4, y4] = point(f0 + inset / (Math.PI * ri), ri)
  return `M ${x1} ${y1} A ${ro} ${ro} 0 0 1 ${x2} ${y2} L ${x3} ${y3} A ${ri} ${ri} 0 0 0 ${x4} ${y4} Z`
}
const toneAt = (f: number) => (f < SAFE_END ? 'safe' : f < CAUTION_END ? 'caution' : 'danger')
const levels = [
  { from: 0, to: SAFE_END, tone: 'safe' },
  { from: SAFE_END, to: CAUTION_END, tone: 'caution' },
  { from: CAUTION_END, to: 1, tone: 'danger' },
] as const
const ms = (v: number) => `${Math.round(v)}ms`
/** Where the reading lands at high risk: 2X at ~75 %, further with a bigger multiple (as the one-colour soft dial). */
const nowAt = (ratio?: number) => (ratio === undefined ? 0.8 : 0.72 + 0.23 * Math.min(1, Math.max(0, (ratio - 1) / 9)))
/** Gradient stops per level: the content colour deep inside, the surface colour through the band, the light tint outside. */
const shades = {
  safe: ['--l3-content-accent-success-default', '--l3-surface-accent-success-default', '--l3-surface-accent-success-light'],
  caution: ['--l3-content-accent-warning-default', '--l3-surface-accent-warning-default', '--l3-surface-accent-warning-light'],
  danger: ['--l3-content-accent-error-default', '--l3-surface-accent-error-default', '--l3-surface-accent-error-light'],
} as const

export function BlockDial({ ratio, level = 'danger', showRatio = false }: { ratio?: number; level?: RiskLevel; showRatio?: boolean }) {
  const number = showRatio && ratio !== undefined
  const uid = useId().replace(/[^a-zA-Z0-9]/g, '')
  const id = (name: string) => `bd-${name}-${uid}`
  const root = useRef<HTMLElement>(null)
  const target = level === 'danger' ? nowAt(ratio) : LEVEL_AT[level]
  const width = (1 - GAP * (COUNT - 1)) / COUNT
  const blocks = Array.from({ length: COUNT }, (_, i) => {
    const f0 = i * (width + GAP)
    return { f0, f1: f0 + width, tone: toneAt(f0 + width / 2), lit: f0 + width / 2 <= target }
  })
  const lit = blocks.filter((b) => b.lit)
  // The fill rests on the last lit block's outer edge, so whole blocks show; it overshoots into the next one and back.
  const end = lit.length ? lit[lit.length - 1].f1 + 0.004 : 0.001
  const END = Math.min(1, end + OVER)
  const reach = (f: number) => DELAY + TRAVEL * RUN * easeTimeAt(Math.min(1, Math.max(0, f / END)), RUN_EASE)
  const amberAt = reach(SAFE_END)
  const redAt = reach(CAUTION_END)
  const label = t(level === 'safe' ? 'nudge.meterLabelSafe' : level === 'caution' ? 'nudge.meterLabelCaution' : 'nudge.meterLabel')
  const words = [['safe', 'nudge.levelSafe'], ['caution', 'nudge.levelMid'], ['danger', 'nudge.highRisk']] as const

  useEffect(() => {
    const el = root.current
    if (!el || window.matchMedia('(prefers-reduced-motion: reduce)').matches) return
    const keys = needleKeys(end)
    const timing = { duration: TRAVEL, delay: DELAY, fill: 'backwards' as const }
    const running: Animation[] = []
    el.querySelectorAll<SVGElement>('[data-turn]').forEach((n) => running.push(n.animate(
      keys.map((k) => ({ offset: k.at, easing: k.easing, transform: `rotate(${(k.f - 0.5) * 180}deg)` })), timing)))
    const sweep = el.querySelector<SVGElement>('[data-sweep]')
    if (sweep) running.push(sweep.animate(keys.map((k) => ({ offset: k.at, easing: k.easing, strokeDashoffset: `${1 - Math.min(k.f, END) / END}` })), timing))

    // Keyframe offsets must never go backwards: at this speed one level can pass in less than two fades.
    const forward = <T extends { offset: number }>(keys: T[]) => { let last = 0; return keys.map((k) => ({ ...k, offset: (last = Math.max(last, k.offset)) })) }
    // The tip's bloom takes the colour of the level the fill is in (oklab blends at each edge).
    const total = DELAY + TRAVEL
    const at = (v: number) => Math.min(1, Math.max(0, v / total))
    const css = getComputedStyle(el)
    const c = (name: string) => css.getPropertyValue(name).trim()
    const g = c('--l3-surface-accent-success-default'), y = c('--l3-surface-accent-warning-default'), r = c('--l3-surface-accent-error-default')
    const mix = (a: string, b: string) => `color-mix(in oklab, ${a}, ${b})`
    const w = 120
    const bloomKeys = level === 'safe' ? [{ offset: 0, fill: g }, { offset: 1, fill: g }]
      : level === 'caution' ? [{ offset: 0, fill: g }, { offset: at(amberAt - w), fill: g }, { offset: at(amberAt), fill: mix(g, y) }, { offset: at(amberAt + w), fill: y }, { offset: 1, fill: y }]
        : [{ offset: 0, fill: g }, { offset: at(amberAt - w), fill: g }, { offset: at(amberAt), fill: mix(g, y) }, { offset: at(amberAt + w), fill: y },
          { offset: at(Math.max(amberAt + w, redAt - w)), fill: y }, { offset: at(redAt), fill: mix(y, r) }, { offset: at(redAt + w), fill: r }, { offset: 1, fill: r }]
    el.querySelectorAll<SVGElement>('[data-bloom]').forEach((n) => running.push(n.animate(forward(bloomKeys), { duration: total, fill: 'backwards' })))

    // The level word swaps as the fill passes each edge (out, then in).
    const fade = 90
    const word = (tone: string, from: number, to: number) => el.querySelectorAll<SVGElement>(`[data-word="${tone}"]`).forEach((n) => running.push(n.animate(forward([
      { offset: 0, opacity: from <= 0 ? 1 : 0 }, { offset: at(from), opacity: from <= 0 ? 1 : 0 }, { offset: at(from + fade), opacity: 1 },
      { offset: at(to - fade), opacity: 1 }, { offset: at(to), opacity: to >= total ? 1 : 0 }, { offset: 1, opacity: to >= total ? 1 : 0 },
    ]), { duration: total, fill: 'backwards' })))
    if (level === 'caution') { word('safe', 0, amberAt); word('caution', amberAt, total) }
    if (level === 'danger') { word('safe', 0, amberAt); word('caution', amberAt, redAt); word('danger', redAt, total) }
    // The wave (19 Nov): the block under the fill's head lifts outward (LIFT) and settles back as the head moves on, so a
    // wave travels with the fill — over the overshoot and back-swing too. The head's path is sampled from the same keys.
    const samples = 90
    const headAt = (p: number) => {
      const i = keys.findIndex((k, n) => n < keys.length - 1 && p >= k.at && p <= keys[n + 1].at)
      const a = keys[Math.max(0, i)], b = keys[Math.max(0, i) + 1]
      const local = (p - a.at) / (b.at - a.at || 1)
      const m = /cubic-bezier\(([^)]+)\)/.exec(a.easing)
      const e = m ? easeTimeInverse(local, m[1].split(',').map(Number)) : local
      return a.f + (b.f - a.f) * e
    }
    const heads = Array.from({ length: samples + 1 }, (_, n) => headAt(n / samples))
    el.querySelectorAll<SVGGElement>('[data-block]').forEach((n) => {
      const b = blocks[Number(n.dataset.block)]
      const mid = (b.f0 + b.f1) / 2
      const reachWidth = width * 0.9
      const a = Math.PI * (1 - mid)
      const lifts = heads.map((h) => Math.max(0, 1 - Math.abs(h - mid) / reachWidth))
      if (!lifts.some((l) => l > 0)) return
      running.push(n.animate(lifts.map((l, k) => ({ offset: k / samples, transform: `translate(${(Math.cos(a) * LIFT * l).toFixed(2)}px, ${(-Math.sin(a) * LIFT * l).toFixed(2)}px)` })), { duration: TRAVEL, delay: DELAY, fill: 'backwards' }))
    })
    return () => running.forEach((a) => a.cancel())
  }, [end, END, amberAt, redAt, level]) // blocks / width follow from level and ratio, as end does

  const big = { x: -80, y: -80, width: 500, height: 400 }
  const shape = (b: (typeof blocks)[number], i: number, paint: string, extra?: string) =>
    <path key={`${extra ?? 'b'}${i}`} d={block(b.f0, b.f1)} fill={paint} stroke={paint} strokeWidth={ROUND} strokeLinejoin="round" className={extra} />
  return <figure ref={root} className={styles.dial} data-level={level} role="img" aria-label={label}
    style={{ '--to-deg': `${(end - 0.5) * 180}deg`, '--sweep-rest': 1 - end / END, '--bloom-in': ms(DELAY), '--word-in': ms(reach(end)) } as CSSProperties}>
    <svg viewBox="-16 -64 372 280" className={styles.svg} aria-hidden>
      <defs>
        {(['safe', 'caution', 'danger'] as const).map((tone) =>
          <radialGradient key={tone} id={id(tone)} gradientUnits="userSpaceOnUse" cx={CX} cy={CY} r={RO}>
            <stop offset={RI / RO} style={{ stopColor: `var(${shades[tone][0]})` }} />
            <stop offset={(RI + BAND * 0.45) / RO} style={{ stopColor: `var(${shades[tone][1]})` }} />
            <stop offset="1" style={{ stopColor: `var(${shades[tone][2]})` }} />
          </radialGradient>)}
        {/* Unlit blocks: a soft grey, a touch lighter outside. */}
        <radialGradient id={id('grey')} gradientUnits="userSpaceOnUse" cx={CX} cy={CY} r={RO}>
          <stop offset={RI / RO} style={{ stopColor: 'var(--l3-surface-tertiary)' }} />
          <stop offset="1" style={{ stopColor: 'var(--l3-surface-secondary)' }} />
        </radialGradient>
        <mask id={id('sweep')} maskUnits="userSpaceOnUse" {...big}>
          <path d={arc(0, END, RM)} pathLength={1} className={styles.sweepStroke} strokeWidth={BAND + 30} data-sweep />
        </mask>
        <filter id={id('blur')} filterUnits="userSpaceOnUse" {...big}><feGaussianBlur stdDeviation="14" /></filter>
      </defs>

      {/* Layer blur: each level's glow comes on as the fill reaches it and fades as it moves on; the last one stays. */}
      {levels.filter((l) => l.from < end).map((l) => {
        const last = end <= l.to
        const on = l.from === 0 ? DELAY : reach(l.from)
        const off = reach(Math.min(l.to, end)) + 250
        return <path key={l.tone} d={arc(l.from + 0.02, Math.min(l.to, end) - 0.01, RM)} className={styles.glow} data-tone={l.tone}
          data-last={last || undefined} strokeWidth={BAND + 16} filter={`url(#${id('blur')})`}
          style={{ '--glow-in': ms(on), '--glow-for': ms(off - on) } as CSSProperties} />
      })}

      {/* Each block: grey, with its gradient over it where the sweep has reached (no glass, 19 Nov). Each block is its own
          group so it can lift outward as the fill passes it — the wave. */}
      {blocks.map((b, i) => <g key={i} data-block={i}>
        {shape(b, i, `url(#${id('grey')})`)}
        <g mask={`url(#${id('sweep')})`}>{shape(b, i, `url(#${id(b.tone)})`, 'c')}</g>
      </g>)}

      {/* The bloom riding the fill's tip. */}
      <g className={styles.turn} data-turn>
        <circle cx={CX} cy={CY - RM} r={BAND / 2} className={styles.bloom} data-bloom filter={`url(#${id('blur')})`} />
      </g>

      {number && <text x={CX} y={CY - 38} className={styles.value} textAnchor="middle">{ratio}X</text>}
      {words.map(([tone, key]) => <text key={tone} x={CX} y={number ? CY - 6 : CY - 22} className={styles.word} data-word={tone} textAnchor="middle">{t(key)}</text>)}
    </svg>
  </figure>
}
```

### `src/flows/nudges/sheets/GaugeMeter.module.css`

```css
/* 4h / 4i · the speedometer (GaugeMeter.tsx), from Figma LM → F&O Playground 6917:62779 (20 Nov). The dial's colours
   are Figma's illustration; the labels and the wave are L3 tokens. */

/* Above the wave (which is positioned too, and comes first). */
.gauge { position: relative; display: block; overflow: visible; }

/* The scale: L3/Heading/12 in content/primary. */
.label { font: var(--l3-text-heading-12); fill: var(--l3-content-primary); }

/* The parts that move turn / scale in the dial's own drawing units (origin = the needle's hub). */
.part, .needle { transform-box: view-box; }

/* The wave behind the top of the sheet: the level's light tint, blurred. It never takes a tap. */
.wave {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: var(--l3-size-96);
  overflow: visible;
  filter: blur(var(--app-gauge-wave-blur));
  pointer-events: none;
}
.wave[data-level='danger'] { fill: var(--l3-surface-accent-indicator-down-light); }
.wave[data-level='caution'] { fill: var(--l3-surface-accent-warning-light); }
.wave[data-level='safe'] { fill: var(--l3-surface-accent-indicator-up-light); }
```

### `src/flows/nudges/sheets/GaugeMeter.tsx`

```tsx
import { useEffect, useId, useRef, type CSSProperties } from 'react'
import { t } from '../copy'
import { GAUGE_H, GAUGE_W, NEEDLE_DRAWN_AT, NEEDLE_PIVOT, face, needle, ring, segments } from './gaugeArt'
import { needleKeys, RUN_EASE, easeTimeAt, RUN } from './SoftDial'
import type { RiskLevel } from './SoftDial'
import styles from './GaugeMeter.module.css'

/** 4h (0 · 30 · 50 · 80 · 100) and 4i (Low · Medium · High): the speedometer from Figma (LM → F&O Playground
 *  6917:62779, 20 Nov). */
export type GaugeScale = 'numbers' | 'words'

/**
 * The scale around the dial, as Figma lays it out: each label's centre (x) and top (y) in the 103-tall group, and
 * where the dial sits in it. Figma geometry, in drawing units (1 = 1 px at 1×).
 */
const SCALES = {
  numbers: {
    width: 213.83, dialX: 36.78,
    labels: [{ text: '0', x: 14, y: 79 }, { text: '30', x: 35.92, y: 32 }, { text: '50', x: 106.71, y: 0 }, { text: '80', x: 178.92, y: 32 }, { text: '100', x: 202.83, y: 78 }],
  },
  words: {
    width: 214.66, dialX: 34.62,
    labels: [{ key: 'gauge.low', x: 12, y: 78 }, { key: 'gauge.medium', x: 105.04, y: 0 }, { key: 'gauge.high', x: 200.66, y: 78 }],
  },
} as const
const DIAL_Y = 24.38
const HEIGHT = DIAL_Y + GAUGE_H // 103

/** Where the needle stops, as a fraction of the scale: high risk where Figma draws it (78), medium straight up, low on
 *  the green. */
export const GAUGE_AT: Record<RiskLevel, number> = { danger: NEEDLE_DRAWN_AT / 100, caution: 0.5, safe: 0.15 }
/** The needle as drawn, turned to fraction f of the scale (0 = pointing left, 1 = right). */
const turn = (f: number) => `rotate(${(f - NEEDLE_DRAWN_AT / 100) * 180}deg)`

/** Motion (once, on open): the six colour segments light up left → right with their scale labels, then the needle
 *  swings up from 0 with the soft dial's run (ease in-out a little past the reading, back a touch, settle). */
const SEGMENT_IN = 260
const SEGMENT_STAGGER = 70
const NEEDLE_DELAY = 320
const NEEDLE_TRAVEL = 2000

export function GaugeMeter({ scale, level = 'danger' }: { scale: GaugeScale; level?: RiskLevel }) {
  const root = useRef<SVGSVGElement>(null)
  const uid = useId()
  const s = SCALES[scale]
  const now = GAUGE_AT[level]
  const label = t(level === 'safe' ? 'nudge.meterLabelSafe' : level === 'caution' ? 'nudge.meterLabelCaution' : 'nudge.meterLabel')

  useEffect(() => {
    const el = root.current
    if (!el || window.matchMedia('(prefers-reduced-motion: reduce)').matches) return
    const running: Animation[] = []
    el.querySelectorAll<SVGGElement>('[data-segment]').forEach((n) => {
      const i = Number(n.dataset.segment)
      running.push(n.animate([{ opacity: 0, transform: 'scale(0.92)' }, { opacity: 1, transform: 'none' }],
        { duration: SEGMENT_IN, delay: i * SEGMENT_STAGGER, easing: 'cubic-bezier(0.2, 0, 0, 1)', fill: 'backwards' }))
    })
    // A label comes in with the segment under it (by where it sits along the dial).
    el.querySelectorAll<SVGTextElement>('[data-label]').forEach((n) => {
      const at = Number(n.dataset.label)
      running.push(n.animate([{ opacity: 0 }, { opacity: 1 }], { duration: SEGMENT_IN, delay: at * 5 * SEGMENT_STAGGER, easing: 'ease-out', fill: 'backwards' }))
    })
    const pointer = el.querySelector<SVGGElement>('[data-needle]')
    if (pointer) running.push(pointer.animate(
      needleKeys(now).map((k) => ({ offset: k.at, easing: k.easing, transform: turn(k.f) })),
      { duration: NEEDLE_TRAVEL, delay: NEEDLE_DELAY, fill: 'backwards' }))
    // The segment the needle lands on gives a small pulse as it arrives.
    const landing = el.querySelector<SVGGElement>(`[data-segment="${Math.min(5, Math.floor(now * 6))}"] [data-band]`)
    const arrive = NEEDLE_DELAY + NEEDLE_TRAVEL * RUN * easeTimeAt(1 - 0.02, RUN_EASE)
    if (landing) running.push(landing.animate([{ filter: 'brightness(1)' }, { filter: 'brightness(1.25)' }, { filter: 'brightness(1)' }],
      { duration: 500, delay: arrive, easing: 'ease-in-out' }))
    return () => running.forEach((a) => a.cancel())
  }, [now, scale])

  return (
    <svg ref={root} className={styles.gauge} width={s.width} height={HEIGHT} viewBox={`0 0 ${s.width} ${HEIGHT}`} role="img" aria-label={label} data-gauge={uid}>
      {s.labels.map((l) => (
        <text key={l.x} x={l.x} y={l.y + 8} className={styles.label} textAnchor="middle" dominantBaseline="central" data-label={l.x / s.width}>
          {'text' in l ? l.text : t(l.key)}
        </text>
      ))}
      <svg x={s.dialX} y={DIAL_Y} width={GAUGE_W} height={GAUGE_H} viewBox={`0 0 ${GAUGE_W} ${GAUGE_H}`} overflow="visible">
        {segments.map((seg, i) => (
          <g key={i} data-segment={i} style={{ transformOrigin: `${NEEDLE_PIVOT.x}px ${NEEDLE_PIVOT.y}px` }} className={styles.part}>
            <path d={seg.rim.d} fill={seg.rim.fill} />
            <path d={seg.band.d} fill={seg.band.fill} data-band />
          </g>
        ))}
        <path d={ring.d} fill={ring.fill} />
        <path d={face.d} fill={face.fill} />
        <g data-needle className={styles.needle} style={{ transformOrigin: `${NEEDLE_PIVOT.x}px ${NEEDLE_PIVOT.y}px`, transform: turn(now) } as CSSProperties}>
          <path d={needle.d} fill={needle.fill} />
        </g>
      </svg>
    </svg>
  )
}

/**
 * The soft pink wave behind the top of the sheet (Figma "Ellipse 1 / 2": the level's light tint, blurred 11.3), drawn
 * in the 360-wide frame it was designed in and stretched to the sheet's width. 4h and 4i place it a little apart.
 */
const WAVE = { numbers: { x: -20, y: -43 }, words: { x: -17, y: -56 } } as const
export function GaugeWave({ scale, level = 'danger' }: { scale: GaugeScale; level?: RiskLevel }) {
  const w = WAVE[scale]
  return (
    <svg className={styles.wave} data-level={level} viewBox="0 0 360 96" preserveAspectRatio="none" overflow="visible" aria-hidden="true">
      <path transform={`translate(${w.x - 22.6} ${w.y - 22.6})`} d="M415.6 89.1133C415.6 125.848 411.184 132.915 214.684 113.447C106.16 113.447 22.6 209.162 22.6 89.1133C22.6 52.379 110.576 22.6 219.1 22.6C327.624 22.6 415.6 52.379 415.6 89.1133Z" />
    </svg>
  )
}
```

### `src/flows/nudges/sheets/GuardrailSheets.module.css`

```css
/* Loss limit and TP/SL sheets. */
.body { padding: 0; }

/* 24 more above the content (L3's 16 top space + 24, as since L3 2.3; 2.4 made the 16 the content's own padding).
   Same in NudgeSheet. */
.sheet [data-sheet-content] { padding-top: calc(var(--l3-spacing-16) + var(--l3-spacing-24)); }
```

### `src/flows/nudges/sheets/GuardrailSheets.tsx`

```tsx
import { useId, useState } from 'react'
import { BottomSheetHeader } from '@l3/components/BottomSheet'
import { Button } from '@l3/components/Button'
import { ButtonGroup } from '@l3/components/ButtonGroup'
import { KeyValueList, KeyValueRow } from '@l3/components/KeyValueList'
import { Stack } from '@l3/components/Stack'
import { Stepper } from '@l3/components/Stepper'
import { Tabs } from '@l3/components/Tabs'
import { TextField } from '@l3/components/TextField'
import { inr } from '../../../shared/data/format'
import { Sheet } from '../../../shared/ui/Sheet'
import { t } from '../copy'
import { limitPresets, orderContract, prefilledTpsl } from '../data'
import styles from './GuardrailSheets.module.css'

/**
 * "Today's loss limit" (PnL Protect, set from the nudge or the order pad). Amount field (focused, as with the keypad
 * up) with quick amounts as pill tabs under it; the dock saves it. Pre-filled with a sample amount so one tap sets it.
 */
export function LossLimitSheet({ initial, onSave, onClose }: { initial: number; onSave: (amount: number) => void; onClose: () => void }) {
  const id = useId()
  const [amount, setAmount] = useState(initial)
  const preset = limitPresets.includes(amount) ? String(amount) : ''
  return <Sheet labelledBy={id} onClose={onClose} className={styles.sheet}
    header={<BottomSheetHeader headingId={id} heading={t('pnl.title')} description={t('pnl.description')} />}
    footer={<ButtonGroup aria-label={t('pnl.title')}><Button size="lg" disabled={amount <= 0} onClick={() => onSave(amount)}>{t('pnl.save')}</Button></ButtonGroup>}>
    <Stack gap="16" className={styles.body}>
      <TextField label={t('pnl.field')} inputMode="numeric" autoFocus value={amount ? inr(amount, 0) : ''}
        onChange={(e) => setAmount(Number(e.target.value.replace(/[^\d]/g, '')) || 0)} helperText={t('pnl.helper')} helperIcon={false} />
      <Tabs aria-label={t('pnl.presets')} appearance="pill" value={preset} onChange={(v) => setAmount(Number(v))}
        items={limitPresets.map((n) => ({ value: String(n), label: inr(n, 0) }))} />
    </Stack>
  </Sheet>
}

/**
 * "TP/SL for this order": target profit and stop-loss as % of the entry price (steppers), the price each one exits
 * at beside it. Opens with the order pad's pre-filled values.
 */
export function TpslSheet({ onSave, onClose }: { onSave: (tpsl: { targetPct: number; stopPct: number }) => void; onClose: () => void }) {
  const id = useId()
  const [targetPct, setTarget] = useState(prefilledTpsl.targetPct)
  const [stopPct, setStop] = useState(prefilledTpsl.stopPct)
  const at = (pct: number) => t('tpsl.atPrice', { price: inr(orderContract.ltp * (1 + pct / 100)) })
  const pct = (n: number) => `${n}%`
  return <Sheet labelledBy={id} onClose={onClose} className={styles.sheet}
    header={<BottomSheetHeader headingId={id} heading={t('tpsl.title')} description={t('tpsl.description')} />}
    footer={<ButtonGroup aria-label={t('tpsl.title')}><Button size="lg" onClick={() => onSave({ targetPct, stopPct })}>{t('tpsl.save')}</Button></ButtonGroup>}>
    <div className={styles.body}>
      <KeyValueList>
        <KeyValueRow label={t('tpsl.target')} caption={at(targetPct)} value={<Stepper size="sm" label={t('tpsl.target')} value={targetPct} onChange={setTarget} min={1} step={1} format={pct} />} />
        <KeyValueRow label={t('tpsl.stop')} caption={at(-stopPct)} value={<Stepper size="sm" label={t('tpsl.stop')} value={stopPct} onChange={setStop} min={1} max={99} step={1} format={pct} />} />
      </KeyValueList>
    </div>
  </Sheet>
}
```

### `src/flows/nudges/sheets/NudgeSheet.module.css`

```css
/* The overtrading nudge — the risk meter sheet (NudgeSheet.tsx), on L3 tokens. Everything is centred. */

/* 24 above the content, as these sheets have looked since L3 2.3 (L3's 16 top space + 24; 2.4 made the 16 the content's
   own padding). Same in GuardrailSheets. */
.sheet [data-sheet-content] { padding-top: calc(var(--l3-spacing-16) + var(--l3-spacing-24)); }
/* 32 from the last text to the dock's line (19 Nov, user; L3's sheet content has 24). */
.meterSheet.meterSheet [data-sheet-content] { padding-bottom: var(--l3-spacing-32); }

.riskText { text-align: center; }
/* The text is drawn over the meter's glow, which now reaches up behind it (the dial's drawing area is taller). */
.riskText h2, .riskText p, .overtradingTag { position: relative; z-index: 1; }

/* "You are overtrading": a step up from the sheet header's 20 (19 Nov, user). */
.meterHeading { margin: 0; font: var(--l3-text-heading-24); color: var(--l3-content-primary); }
/* "Your chances of losing money today are high" under it. */
.meterNote { margin: 0; font: var(--l3-text-label-14); color: var(--l3-content-secondary); }
/* The fact under the meter, as body text in secondary. */
.meterFact { margin: 0; font: var(--l3-text-description-14); color: var(--l3-content-secondary); }

/* Tag first: the risk as the heading, 18. */
.meterRiskHeading { margin: 0; font: var(--l3-text-heading-18); color: var(--l3-content-primary); }
/* Tag first · the "Overtrading Detected" tag (19 Nov, user): 8 in from each side and 2 between the icon and the label.
   L3's Medium Tag has 2 at the sides and 6 icon → text (its label's own 4 padding); no prop for this (L3 gap). */
.overtradingTag.overtradingTag[data-size] { --tag-padding-inline: var(--l3-spacing-08); --tag-label-padding: 0; }

/* 4h / 4i · the speedometer layout (Figma 6917:62779): 24 from the sheet's top and 24 from the fact to the dock's line
   (Figma: the header's 24 top and 8 bottom + the sheet's 16 top space). The wave is drawn from the content's top. */
.gaugeSheet.gaugeSheet [data-sheet-content] {
  position: relative;
  padding-top: var(--l3-spacing-24);
  padding-bottom: var(--l3-spacing-24);
}
.gaugeHeading { margin: 0; font: var(--l3-text-heading-20); color: var(--l3-content-primary); }
/* The fact: L3/Description/14 (20 Nov, user; Figma had Label/12). */
.gaugeSub { margin: 0; font: var(--l3-text-description-14); color: var(--l3-content-secondary); }
/* Soft dial · 3 blocks · Low–High: the speedometer's 24 from the fact to the dock's line. */
.wordsSheet.wordsSheet [data-sheet-content] { padding-bottom: var(--l3-spacing-24); }
```

### `src/flows/nudges/sheets/NudgeSheet.tsx`

```tsx
import { useEffect, useId } from 'react'
import { Button } from '@l3/components/Button'
import { ButtonGroup } from '@l3/components/ButtonGroup'
import { Icon } from '@l3/components/Icon'
import { Stack } from '@l3/components/Stack'
import { Tag } from '@l3/components/Tag'
import { msWarningFill } from '@l3/icons/material'
import { Sheet } from '../../../shared/ui/Sheet'
import copy from '../copy.json'
import { t } from '../copy'
import { caseById, type DataState, type Guardrail, type NudgeCaseId } from '../data'
import styles from './NudgeSheet.module.css'
import { SoftDial, type RiskLevel } from './SoftDial'
import { BlockDial } from './BlockDial'
import { GaugeMeter, GaugeWave } from './GaugeMeter'

/** The meter (prototype setting "Meter"): 4f Soft dial (default), 4g Blocks, 4h / 4i the speedometer (0–100 / Low–High). */
export type MeterStyle = 'soft' | 'blocks' | 'gauge' | 'gaugeWords'
/** Where the text sits around the meter (prototype setting "Meter layout"). */
export type MeterLayout = 'text' | 'meter' | 'tag' | 'number'

export type NudgeSheetProps = {
  caseId: NudgeCaseId
  state: DataState
  /** 4f Soft dial (default) or 4g Blocks. */
  meterStyle?: MeterStyle
  /** Where the reading stops: safe, caution or high risk (default). */
  meterLevel?: RiskLevel
  /** Text first (default) · Meter first · Tag first · With multiple. */
  meterLayout?: MeterLayout
  /** Soft dial only: the blended green → yellow → red fill (default: one colour for the whole ring). */
  meterBlend?: boolean
  /** Soft dial, blended only: the ring cut into three blocks where the colour changes. */
  meterSplit?: boolean
  /** Soft dial (3 blocks or one colour): Low · Medium · High round the dial, the risk tag in it. */
  meterWords?: boolean
  /** Buzz the phone once when the sheet opens (two short pulses: "stop, look"). */
  vibrate?: boolean
  /** 'one' (default): the case's guardrail (primary) + Not now (secondary) · 'two': both guardrails + Not now (ghost). */
  actions?: 'one' | 'two'
  onGuardrail: (g: Guardrail) => void
  /** Not now: the order goes ahead (on Positions: just closes). Also a scrim tap, drag down or Esc. */
  onNotNow: () => void
}

type Key = Parameters<typeof t>[0]

/**
 * The overtrading nudge — the risk meter (19 Nov, cut down to the versions in use). ONE sheet for every case; a case only
 * fills the slots. It opens on a trader who is mid-order and stressed: what this is, the meter that shows how far from
 * his usual he is, and one plain line on what he is doing — then the guardrail, or Not now.
 *
 * Meter layouts (all centred, 24 between blocks, the body text 16 under the meter, 32 to the dock's line):
 * - Text first: "You are overtrading" (heading-24) over "Your chances of losing money today are high", the meter, the fact.
 * - Meter first: the meter, then "You are overtrading" and the fact.
 * - Tag first: a red "Overtrading Detected" tag (filled warning icon), "Your chances of losing money are high"
 *   (heading-18), the meter with the multiple in it, the fact.
 * - With multiple: as Text first (since 20 Nov no version shows the multiple in the dial, so the two now match).
 * The fact: size-up says "You are placing a bigger order right after a loss"; every other case its own fact
 * ("3X more orders than usual today"). Motion plays once on open; none with reduced motion.
 */
export function NudgeSheet({ caseId, state, meterStyle = 'soft', meterLevel = 'danger', meterLayout = 'text', meterBlend = false, meterSplit = false, meterWords = false, vibrate = true, actions = 'one', onGuardrail, onNotNow }: NudgeSheetProps) {
  const id = useId()
  // On open only (switching case or version keeps the sheet open, so it doesn't buzz again).
  useEffect(() => { if (vibrate) buzz() }, []) // eslint-disable-line react-hooks/exhaustive-deps
  const nudge = caseById.get(caseId)!
  const key = (slot: string) => `case.${caseId}.${slot}` as Key
  const has = (slot: string) => key(slot) in copy

  // C (thin history): no "usual" to compare with → today's raw fact, no multiple.
  const thin = state === 'C' && has('raw')
  const headline = t(key(thin ? 'raw' : 'headline'))
  const ratio = thin ? undefined : nudge.ratio
  const fact = caseId === 'sizeUp' ? t('nudge.biggerAfterLoss') : headline

  const other: Guardrail = nudge.primary === 'pnl' ? 'tpsl' : 'pnl'
  const label = (g: Guardrail) => t(g === 'pnl' ? 'nudge.setPnl' : 'nudge.setTpsl')
  const notNow = t(nudge.where === 'positions' ? 'nudge.notNowPositions' : 'nudge.notNow')
  const footer = <ButtonGroup aria-label={headline} direction="vertical">
    <Button size="lg" onClick={() => onGuardrail(nudge.primary)}>{label(nudge.primary)}</Button>
    {actions === 'two' && <Button size="lg" variant="secondary" onClick={() => onGuardrail(other)}>{label(other)}</Button>}
    <Button size="lg" variant={actions === 'two' ? 'ghost' : 'secondary'} onClick={onNotNow}>{notNow}</Button>
  </ButtonGroup>

  // No multiple ("2X") in the dial in any layout (20 Nov): the disc shows the level word only.
  // The speedometer's text under a meter: the risk tag, 16, the heading (heading-20), 8, the fact (description-14).
  const tagColor = meterLevel === 'danger' ? 'loss' : meterLevel === 'caution' ? 'warning' : 'profit'
  const riskTag = <Tag size="md" variant="secondary" color={tagColor} iconLeft={meterLevel === 'safe' ? undefined : <Icon icon={msWarningFill} />}>{t(`gauge.tag.${meterLevel}`)}</Tag>
  const headingAndFact = <Stack gap="08" align="center">
    <h2 id={id} className={styles.gaugeHeading}>{t(`gauge.heading.${meterLevel}`)}</h2>
    <p className={styles.gaugeSub}>{caseId === 'sizeUp' ? t('gauge.sizeUp') : headline}</p>
  </Stack>
  const meter = meterStyle === 'blocks'
    ? <BlockDial key={`${caseId}-${state}-${meterLevel}-${meterLayout}`} ratio={ratio} level={meterLevel} />
    : <SoftDial key={`${caseId}-${state}-${meterLevel}-${meterBlend}-${meterSplit}-${meterWords}-${meterLayout}`} ratio={ratio} level={meterLevel} blend={meterBlend} split={meterSplit} words={meterWords} badge={meterWords ? riskTag : undefined} />
  const meterAndFact = <Stack gap="16" align="center">
    {meter}
    <p className={styles.meterFact}>{fact}</p>
  </Stack>

  // 4h / 4i · the speedometer (Figma 6917:62779, 20 Nov) has its own layout, whatever the Meter layout setting: the pink
  // wave at the top, the dial with its scale, 16, the risk tag, 16, "Your chances of losing money is high" (heading-20), 8, the
  // fact (label-12). 24 from the top of the sheet, 24 from the fact to the dock's line.
  const gaugeText = <Stack gap="16" align="center">{riskTag}{headingAndFact}</Stack>
  if (meterStyle === 'gauge' || meterStyle === 'gaugeWords') {
    const scale = meterStyle === 'gauge' ? 'numbers' : 'words'
    return <Sheet labelledBy={id} onClose={onNotNow} className={`${styles.sheet} ${styles.gaugeSheet}`} footer={footer}>
      <GaugeWave scale={scale} level={meterLevel} />
      <Stack gap="16" align="center" className={styles.riskText}>
        <GaugeMeter key={`${caseId}-${state}-${meterLevel}-${scale}`} scale={scale} level={meterLevel} />
        {gaugeText}
      </Stack>
    </Sheet>
  }
  // Soft dial · 3 blocks · Low–High (20 Nov, user): the speedometer's layout under the dial (no word in the dial), and
  // the speedometer's 24 to the dock's line; Meter layout doesn't apply.
  if (meterWords) {
    return <Sheet labelledBy={id} onClose={onNotNow} className={`${styles.sheet} ${styles.wordsSheet}`} footer={footer}>
      {/* The risk tag sits in the dial (where the level word was) and fades in as the needle lands; 24 from the dial to
          the heading (20 Nov, user). */}
      <Stack gap="24" align="center" className={styles.riskText}>
        {meter}
        {headingAndFact}
      </Stack>
    </Sheet>
  }

  let body
  if (meterLayout === 'meter') {
    // Meter first: other cases add the risk to their fact ("3X more orders than usual today. Your chances … are high").
    const line = caseId === 'sizeUp' ? fact : t('nudge.meterFirstSubOther', { fact: headline })
    body = <Stack gap="24" align="center" className={styles.riskText}>
      {meter}
      <Stack gap="04" align="center">
        <h2 id={id} className={styles.meterHeading}>{t('nudge.meterHeading')}</h2>
        <p className={styles.meterFact}>{line}</p>
      </Stack>
    </Stack>
  } else if (meterLayout === 'tag') {
    body = <Stack gap="24" align="center" className={styles.riskText}>
      <Stack gap="12" align="center">
        <Tag size="md" variant="secondary" color="error" className={styles.overtradingTag} iconLeft={<Icon icon={msWarningFill} />}>{t('nudge.tag')}</Tag>
        <h2 id={id} className={styles.meterRiskHeading}>{t('nudge.meterRiskHeading')}</h2>
      </Stack>
      {meterAndFact}
    </Stack>
  } else {
    // Text first and With multiple (the same since the dial's multiple was removed, 20 Nov).
    body = <Stack gap="24" align="center" className={styles.riskText}>
      <Stack gap="04" align="center">
        <h2 id={id} className={styles.meterHeading}>{t('nudge.meterHeading')}</h2>
        <p className={styles.meterNote}>{t('nudge.meterSub')}</p>
      </Stack>
      {meterAndFact}
    </Stack>
  }

  return <Sheet labelledBy={id} onClose={onNotNow} className={`${styles.sheet} ${styles.meterSheet}`} footer={footer}>{body}</Sheet>
}

/** Two short pulses. In the Lemonn Android app the page calls its native bridge (works without a tap, and uses the
 *  phone's haptics); in a browser, the Vibration API (Android Chrome only, and only right after a tap; iPhone: none). */
const BUZZ = [70, 60, 70]
function buzz() {
  const app = (window as { LemonnApp?: { vibrate?: (pattern: string) => void } }).LemonnApp
  try {
    if (app?.vibrate) app.vibrate(BUZZ.join(','))
    else navigator.vibrate?.(BUZZ)
  } catch { /* no vibration here */ }
}
```

### `src/flows/nudges/sheets/SoftDial.module.css`

```css
/* 4f · Soft dial (SoftDial.tsx). SVG drawing units, not CSS px. Resting styles are the END state (red / High risk);
   the component (Web Animations) runs the needle, sweep, colours and level word from green before it. CSS keeps only
   the timed fades: --travel-in / --travel-for (the needle's run) and each glow's --glow-in / --glow-for. */

/* The drawing area has room for the whole blurred glow (it reaches ~50 past the ring): 16 past the ring on each side
   (that's the sheet's edge) and 70 above the dial, so nothing draws outside the svg — mobile browsers (Safari) clip
   SVG content at the svg's box, overflow: visible or not, which cut the glow off in a hard edge (19 Nov). The svg is
   that much bigger and pulled back by negative margins (relative to the width, like the viewBox), so the dial sits
   exactly where it did and its box ends at the ring's base line: viewBox −16 −64 372 × 280 for the dial's 340 × 170. */
.svg {
  display: block;
  width: calc(100% * 372 / 340);
  height: auto;
  margin: calc(100% * -70 / 340) calc(100% * -16 / 340) calc(100% * -40 / 340);
  overflow: visible;
}

.dial { position: relative; margin: 0; }
/* Resting colours = the end state (red); the component animates them from green. */
.deep { stop-color: var(--l3-content-accent-error-default); }
.mid { stop-color: var(--l3-surface-accent-error-default); }
.light { stop-color: var(--l3-surface-accent-error-light); }

/* The sweep's resting point (the component animates it). */
.sweepStroke { fill: none; stroke: white; stroke-dasharray: 1; stroke-dashoffset: var(--sweep-rest); }

.dot { fill: var(--l3-static-white); }
/* Grains left on the fill: quiet; the component fades the green and yellow ones away as the needle moves on. */
.dotsPassed { opacity: 0.45; }
.dotsPassed[data-grains='safe'], .dotsPassed[data-grains='caution'] { opacity: 0; }
/* …except on the level the reading stops in. */
.dial[data-level='safe'] .dotsPassed[data-grains='safe'], .dial[data-level='caution'] .dotsPassed[data-grains='caution'] { opacity: 0.45; }
/* The grains in the soft wedge riding behind the needle: a little brighter than the rest (kept gentle, 19 Nov). */
.dots { opacity: 0.6; }

.rest { fill: var(--l3-surface-accent-error-light); opacity: 0.5; }

.tick { stroke: var(--l3-content-primary); stroke-width: 2; stroke-linecap: round; opacity: 0.12; }
.tick[data-filled] { opacity: 0.3; }

/* Bloom at the tip: comes in as the fill lands. */
.bloom { fill: var(--l3-surface-accent-error-default); opacity: 0.45; animation: fadeIn var(--l3-motion-duration-long) var(--l3-motion-easing-decelerate) calc(var(--travel-in) + var(--travel-for) - var(--l3-motion-duration-medium)) backwards; }

/* Layer blur per level: on as the fill reaches the level, off as it moves on; the last one stays and breathes. */
/* Lighter than the level colour itself: the level colour mixed half with white. */
[data-tone='safe'] { --tone: color-mix(in srgb, var(--l3-surface-accent-success-default) 50%, var(--l3-static-white)); }
[data-tone='caution'] { --tone: color-mix(in srgb, var(--l3-surface-accent-warning-default) 50%, var(--l3-static-white)); }
[data-tone='danger'] { --tone: color-mix(in srgb, var(--l3-surface-accent-error-default) 50%, var(--l3-static-white)); }
.glow { fill: none; stroke: var(--tone); stroke-linecap: round; opacity: 0; animation: glowPass var(--glow-for) linear var(--glow-in) both; }
@keyframes glowPass { 0% { opacity: 0; } 20% { opacity: 0.6; } 70% { opacity: 0.5; } 100% { opacity: 0; } }
.glow[data-last] {
  opacity: 0.35;
  animation:
    fadeIn var(--l3-motion-duration-long) var(--l3-motion-easing-decelerate) var(--glow-in) backwards,
    breathe calc(var(--l3-motion-duration-long) * 4) var(--l3-motion-easing-standard) calc(var(--glow-in) + var(--glow-for)) 2;
}
@keyframes breathe { 50% { opacity: 0.6; } }

/* The needle and the grain wedge turn about the ring's centre (170, 176). */
.turn { transform-box: view-box; transform-origin: 170px 176px; transform: rotate(var(--to-deg)); }
/* The needle is black in both modes. */
.needle { fill: var(--l3-static-black); }
/* Glass on the fill. */
.glassLine { fill: none; stroke: var(--l3-static-white); stroke-linecap: round; opacity: 0.55; }
.glassRim { fill: none; stroke: var(--l3-static-white); stroke-width: 1; stroke-opacity: 0.5; }

.disc { fill: var(--l3-surface-primary); }
.level { font: var(--l3-text-heading-20); fill: var(--l3-content-primary); }
/* "With multiple": the multiple above the word (L3's largest heading, 36), in once the reading lands. */
.value { font: var(--l3-text-heading-36); fill: var(--l3-content-primary); animation: fadeIn var(--l3-motion-duration-long) var(--l3-motion-easing-decelerate) calc(var(--travel-in) + var(--travel-for)) backwards; }

/* The level word: only the reached level's word rests visible; the component swaps Safe → Caution → High risk on the way. */
.level { opacity: 0; }
.dial[data-level='safe'] .level[data-word='safe'],
.dial[data-level='caution'] .level[data-word='caution'],
.dial[data-level='danger'] .level[data-word='danger'] { opacity: 1; }

/* Resting colours of the safe and caution versions (danger's are the defaults above). */
.dial[data-level='safe'] .deep { stop-color: var(--l3-content-accent-success-default); }
.dial[data-level='safe'] .mid { stop-color: var(--l3-surface-accent-success-default); }
.dial[data-level='safe'] .light { stop-color: var(--l3-surface-accent-success-light); }
.dial[data-level='safe'] .rest { fill: var(--l3-surface-accent-success-light); }
.dial[data-level='safe'] .bloom { fill: var(--l3-surface-accent-success-default); }
.dial[data-level='caution'] .deep { stop-color: var(--l3-content-accent-warning-default); }
.dial[data-level='caution'] .mid { stop-color: var(--l3-surface-accent-warning-default); }
.dial[data-level='caution'] .light { stop-color: var(--l3-surface-accent-warning-light); }
.dial[data-level='caution'] .rest { fill: var(--l3-surface-accent-warning-light); }
.dial[data-level='caution'] .bloom { fill: var(--l3-surface-accent-warning-default); }
@keyframes fadeIn { from { opacity: 0; } }

@media (prefers-reduced-motion: reduce) {
  .dial, .dial * { animation: none !important; }
}

/* "3 blocks · Low–High": the scale round the dial, as on the 4i speedometer (L3 heading, content/primary; in drawing
   units the dial's 340 is about the content's width, so 14 ≈ 14 px). */
/* 16 (20 Nov, user: 2 bigger again). */
.scaleWord { font: var(--l3-text-heading-16); fill: var(--l3-content-primary); }

/* 3 blocks · Low–High: the risk Tag in the disc, centred where the level word sat (top set by the component). */
.badge { position: absolute; left: 50%; translate: -50% -50%; }
```

### `src/flows/nudges/sheets/SoftDial.tsx`

```tsx
import { useEffect, useId, useRef, type CSSProperties, type ReactNode } from 'react'
import { t } from '../copy'
import styles from './SoftDial.module.css'

/**
 * 4f · Soft dial (Anshul_Risk_Meter, 19 Nov; from the user's reference image): a thick half ring filled from the left
 * end to the reading with a soft radial gradient (deep at the inner edge, light at the outer), a dotted texture and
 * small ticks on the filled part, a short dark marker at its tip, and a white disc in the middle holding the number,
 * the level and a sub line. The unfilled rest is a faint tint that fades out, with a blurred bloom at the tip.
 * The colour follows the level the fill is in: green → yellow → red as it sweeps (gradient stops animate), the level
 * word in the disc changes with it ("Low risk" → "Caution" → "High risk"), and each level gets a blurred glow behind
 * it as the fill reaches it. The lower ends fade into the sheet, as in the reference.
 * Reduced motion: the end state.
 */
const CX = 170
const CY = 176
const RO = 160 // outer edge of the ring
const RI = 96 // inner edge = the disc
const RM = (RO + RI) / 2
const BAND = RO - RI
/** Level edges of the BLENDED fill (19 Nov, user): yellow starts further left and red is kept to the right — green
 *  0–33 %, yellow 33–60 %, red 60–100 % of the ring. The one-colour fill keeps the earlier 45 % / 65 % (19 Nov, user:
 *  "a little less, like the previous version"). */
const SAFE_END = 0.33
const CAUTION_END = 0.6
/** "3 blocks · Low–High" (20 Nov, user): three equal blocks, so Medium sits over the middle of the yellow one. */
const EDGES = { blend: { safe: SAFE_END, caution: CAUTION_END }, whole: { safe: 0.45, caution: 0.65 }, thirds: { safe: 1 / 3, caution: 2 / 3 } } as const
const DELAY = 300
/** The needle's run (19 Nov): ease-in-out up to a little past the reading (fast in the middle), then back a touch,
 *  forward a touch, and it settles — a soft bounce. Offsets are of TRAVEL; f = fraction of the scale. */
const TRAVEL = 2400
export const OVER = 0.05
export const RUN = 0.6
export const RUN_EASE = [0.42, 0, 0.3, 1] as const
export const needleKeys = (now: number) => [
  { at: 0, f: 0, easing: `cubic-bezier(${RUN_EASE.join(',')})` },
  { at: RUN, f: Math.min(1, now + OVER), easing: 'cubic-bezier(0.45, 0, 0.55, 1)' },
  { at: 0.79, f: now - 0.022, easing: 'cubic-bezier(0.45, 0, 0.55, 1)' },
  { at: 0.91, f: now + 0.007, easing: 'cubic-bezier(0.3, 0, 0.3, 1)' },
  { at: 1, f: now, easing: 'linear' },
]
/** Time fraction (0–1) at which a cubic-bezier easing reaches progress p. */
export function easeTimeAt(p: number, [x1, y1, x2, y2]: readonly number[]) {
  const b = (s: number, a: number, c: number) => 3 * a * s * (1 - s) ** 2 + 3 * c * s ** 2 * (1 - s) + s ** 3
  let lo = 0, hi = 1
  for (let i = 0; i < 30; i++) { const m = (lo + hi) / 2; if (b(m, y1, y2) < p) lo = m; else hi = m }
  return b((lo + hi) / 2, x1, x2)
}

function point(f: number, r: number) {
  const a = Math.PI * (1 - f)
  return [CX + r * Math.cos(a), CY - r * Math.sin(a)] as const
}
function arc(from: number, to: number, r: number) {
  const [x1, y1] = point(from, r)
  const [x2, y2] = point(to, r)
  return `M ${x1} ${y1} A ${r} ${r} 0 0 1 ${x2} ${y2}`
}
/** An annular sector of the ring, from f0 to f1. */
function sector(f0: number, f1: number) {
  const [ox0, oy0] = point(f0, RO)
  const [ox1, oy1] = point(f1, RO)
  const [ix1, iy1] = point(f1, RI)
  const [ix0, iy0] = point(f0, RI)
  return `M ${ox0} ${oy0} A ${RO} ${RO} 0 0 1 ${ox1} ${oy1} L ${ix1} ${iy1} A ${RI} ${RI} 0 0 0 ${ix0} ${iy0} Z`
}
const ms = (v: number) => `${Math.round(v)}ms`
const levelsFor = (e: { safe: number; caution: number }) => [
  { from: 0, to: e.safe, tone: 'safe' },
  { from: e.safe, to: e.caution, tone: 'caution' },
  { from: e.caution, to: 1, tone: 'danger' },
] as const

/** Where the reading stops (19 Nov): in the green, yellow or red level. Danger lands by the multiple, as before. */
export type RiskLevel = 'safe' | 'caution' | 'danger'
/** Where the needle stops. Blended: well into the red (2X at ~85 %); one colour: as before (2X at ~75 %). */
const LEVEL_AT = { blend: { safe: 0.2, caution: 0.47 }, whole: { safe: 0.3, caution: 0.56 } } as const
const multiple = (ratio?: number) => Math.min(1, Math.max(0, ((ratio ?? 1) - 1) / 9))
const dangerAt = (ratio: number | undefined, blend: boolean) => blend
  ? (ratio === undefined ? 0.86 : 0.84 + 0.12 * multiple(ratio))
  : (ratio === undefined ? 0.8 : 0.72 + 0.23 * multiple(ratio))

/**
 * Blended fill (19 Nov, user): each part of the ring keeps the colour it was filled with — green, then yellow, then red —
 * melting into each other over a soft band at each level edge, so it reads as one ramp, not three blocks. Drawn as thin
 * slices along the arc (SVG has no conic gradient), each in its own oklab mix of the level colours, under a radial shade
 * that keeps the ring's depth (darker inside, lighter outside).
 */
const BLEND = 0.07 // half-width of the soft band at each level edge, as a fraction of the scale
const SLICES = 90
function blendColour(f: number, split = false, edges: { safe: number; caution: number } = EDGES.blend) {
  const g = 'var(--l3-surface-accent-success-default)'
  const y = 'var(--l3-surface-accent-warning-default)'
  const r = 'var(--l3-surface-accent-error-default)'
  const mix = (a: string, b: string, t: number) => `color-mix(in oklab, ${a} ${Math.round((1 - t) * 100)}%, ${b})`
  const ease = (t: number) => t * t * (3 - 2 * t) // smoothstep, so each band starts and ends softly
  if (split) return f < edges.safe ? g : f < edges.caution ? y : r // three blocks: each its own colour, cut at the edges
  if (f <= SAFE_END - BLEND) return g
  if (f < SAFE_END + BLEND) return mix(g, y, ease((f - (SAFE_END - BLEND)) / (2 * BLEND)))
  if (f <= CAUTION_END - BLEND) return y
  if (f < CAUTION_END + BLEND) return mix(y, r, ease((f - (CAUTION_END - BLEND)) / (2 * BLEND)))
  return r
}

/** "Blended · 3 blocks" (20 Nov, user): the gap cut across the ring at each colour change, in drawing units. */
const CUT = 6

/** "3 blocks · Low–High" (20 Nov, user): the dial drawn at this size about its base centre, so Low · Medium · High fit
 *  round it — Low and High beside the ends, Medium over the top — as on the 4i speedometer. */
const WORDS_SCALE = 0.84
const WORDS_GAP = 18 // from the ring to a scale word, in drawing units

/** The badge in the disc (3 blocks · Low–High): its centre, in drawing units, where the level word sat. The figure's box
 *  runs from y 6 to the base line (CY) and x 0–340 (see .svg in the CSS). */
const BADGE_Y = CY - 26 * WORDS_SCALE
const BADGE_FADE = 300

export function SoftDial({ ratio, level = 'danger', blend = false, split = false, words = false, badge, showRatio = false }: { ratio?: number; level?: RiskLevel; blend?: boolean; split?: boolean; words?: boolean; badge?: ReactNode; showRatio?: boolean }) {
  const uid = useId().replace(/[^a-zA-Z0-9]/g, '')
  const ids = { fill: `sd-fill-${uid}`, sweep: `sd-sweep-${uid}`, fade: `sd-fade-${uid}`, fadeMask: `sd-fademask-${uid}`, dots: `sd-dots-${uid}`, trail: `sd-trail-${uid}`, trailBlur: `sd-trailblur-${uid}`, blur: `sd-blur-${uid}`, glass: `sd-glass-${uid}`, shadow: `sd-shadow-${uid}`, shade: `sd-shade-${uid}`, cut: `sd-cut-${uid}` }
  const root = useRef<HTMLElement>(null)
  const number = showRatio && ratio !== undefined
  // Three equal blocks wherever the ring is cut into blocks or carries the Low · Medium · High scale (20 Nov, user).
  const edges = EDGES[words || split ? 'thirds' : blend ? 'blend' : 'whole']
  const levels = levelsFor(edges)
  // Equal thirds: low and medium stop in the middle of their block; high as the blended dial.
  const now = level === 'danger' ? dangerAt(ratio, blend) : words || split ? { safe: 1 / 6, caution: 0.5 }[level] : LEVEL_AT[blend ? 'blend' : 'whole'][level]
  // The fill is drawn to END (a little past the reading) so the overshoot has colour under it; the sweep shows f / END of it.
  const END = Math.min(1, now + OVER)
  // When the needle first reaches fraction f (during its run).
  const reach = (f: number) => DELAY + TRAVEL * RUN * easeTimeAt(Math.min(1, Math.max(0, f / END)), RUN_EASE)
  const amberAt = reach(edges.safe)
  const redAt = reach(edges.caution)
  const timing = { '--travel-in': ms(DELAY), '--travel-for': ms(TRAVEL * RUN), '--to-deg': `${(now - 0.5) * 180}deg`, '--sweep-rest': 1 - now / END } as CSSProperties
  const label = t(level === 'safe' ? 'nudge.meterLabelSafe' : level === 'caution' ? 'nudge.meterLabelCaution' : 'nudge.meterLabel')
  const [tipX, tipY] = point(now, RM)

  // The motion, in one place (Web Animations), so the needle, the fill, the grains, the colours and the level word all
  // follow the same eased, bouncing path. Reduced motion: none — the CSS end state shows.
  useEffect(() => {
    const el = root.current
    if (!el || window.matchMedia('(prefers-reduced-motion: reduce)').matches) return
    const keys = needleKeys(now)
    const timingOpts = { duration: TRAVEL, delay: DELAY, fill: 'backwards' as const }
    const running: Animation[] = []
    el.querySelectorAll<SVGElement>('[data-turn]').forEach((n) => running.push(n.animate(
      keys.map((k) => ({ offset: k.at, easing: k.easing, transform: `rotate(${(k.f - 0.5) * 180}deg)` })), timingOpts)))
    const sweep = el.querySelector<SVGElement>('[data-sweep]')
    if (sweep) running.push(sweep.animate(keys.map((k) => ({ offset: k.at, easing: k.easing, strokeDashoffset: `${1 - Math.min(k.f, END) / END}` })), timingOpts))

    // Colours: green → yellow → red as the needle crosses each level, each change spread over a short window and
    // passing through an oklab mix (no muddy midpoint). Driven on the elements themselves (gradient stops, tints).
    const css = getComputedStyle(el)
    const tone = (name: string) => css.getPropertyValue(name).trim()
    const total = DELAY + TRAVEL
    // Green holds until just before the yellow level, blends to full yellow at the middle of the yellow level, then
    // blends on to red just past it — one continuous change, each blend at least 0.25 s (oklab: no muddy midpoint).
    const win = 250
    const yellowAt = (amberAt + redAt) / 2
    const at = (v: number) => Math.min(1, Math.max(0, v / total))
    const shift = (g: string, y: string, r: string) => {
      const mix = (a: string, b: string) => `color-mix(in oklab, ${a}, ${b})`
      // Safe: green throughout. Caution: green, then blends to yellow as the needle enters it, and stays yellow.
      if (level === 'safe') return [{ offset: 0, c: g }, { offset: 1, c: g }]
      if (level === 'caution') return [{ offset: 0, c: g }, { offset: at(amberAt - win), c: g }, { offset: at(amberAt), c: mix(g, y) }, { offset: at(amberAt + win), c: y }, { offset: 1, c: y }]
      const gEnd = Math.min(amberAt, yellowAt - win)
      const rStart = Math.max(redAt, yellowAt + win)
      return [
        { offset: 0, c: g }, { offset: at(gEnd), c: g }, { offset: at((gEnd + yellowAt) / 2), c: mix(g, y) }, { offset: at(yellowAt), c: y },
        { offset: at((yellowAt + rStart) / 2), c: mix(y, r) }, { offset: at(rStart), c: r }, { offset: 1, c: r },
      ]
    }
    const deep = shift(tone('--l3-content-accent-success-default'), tone('--l3-content-accent-warning-default'), tone('--l3-content-accent-error-default'))
    const mid = shift(tone('--l3-surface-accent-success-default'), tone('--l3-surface-accent-warning-default'), tone('--l3-surface-accent-error-default'))
    const light = shift(tone('--l3-surface-accent-success-light'), tone('--l3-surface-accent-warning-light'), tone('--l3-surface-accent-error-light'))
    const colourOpts = { duration: total, fill: 'backwards' as const }
    const paint = (sel: string, prop: 'stopColor' | 'fill', keysC: { offset: number; c: string }[]) =>
      el.querySelectorAll<SVGElement>(sel).forEach((n) => running.push(n.animate(keysC.map((k) => ({ offset: k.offset, [prop]: k.c })), colourOpts)))
    paint('[data-stop="deep"]', 'stopColor', deep)
    paint('[data-stop="mid"]', 'stopColor', mid)
    paint('[data-stop="light"]', 'stopColor', light)
    // The ring behind starts plain grey; its tint only comes in as the needle starts (0.25 s), then follows the colour.
    const grey = tone('--l3-surface-tertiary')
    const tintIn = DELAY + 250
    paint('[data-paint="light"]', 'fill', [{ offset: 0, c: grey }, { offset: at(DELAY), c: grey }, { offset: at(tintIn), c: light[0].c }, ...light.filter((k) => k.offset > at(tintIn))])
    paint('[data-paint="mid"]', 'fill', mid)

    // Grains left on the green and yellow levels fade away once the needle leaves the level (over 0.5 s); red keeps them.
    el.querySelectorAll<SVGElement>('[data-grains]').forEach((n) => {
      const level = levels.find((l) => l.tone === n.dataset.grains)!
      if (level.tone === 'danger' || level.to >= now) return
      const leave = reach(level.to)
      running.push(n.animate([{ offset: 0, opacity: 0.45 }, { offset: at(leave), opacity: 0.45 }, { offset: at(leave + 500), opacity: 0 }, { offset: 1, opacity: 0 }], colourOpts))
    })

    // The level word cross-fades with the colour.
    // The level word swaps (0.1 s out, 0.1 s in) where the colour turns: Low risk → Caution (entering yellow) → High risk (entering red).
    const fade = 100
    const word = (tone: string, from: number, to: number) => el.querySelectorAll<SVGElement>(`[data-word="${tone}"]`).forEach((n) => running.push(n.animate([
      // Out, then in (never both at once): the old word fades out just before the change, the new one in just after.
      { offset: 0, opacity: from <= 0 ? 1 : 0 }, { offset: at(from), opacity: from <= 0 ? 1 : 0 }, { offset: at(from + fade), opacity: 1 },
      { offset: at(to - fade), opacity: 1 }, { offset: at(to), opacity: to >= total ? 1 : 0 }, { offset: 1, opacity: to >= total ? 1 : 0 },
    ], colourOpts)))
    const toYellow = (Math.min(amberAt, yellowAt - win) + yellowAt) / 2
    const toRed = (yellowAt + Math.max(redAt, yellowAt + win)) / 2
    if (level === 'caution') {
      word('safe', 0, amberAt)
      word('caution', amberAt, total)
    } else if (level === 'danger') {
      word('safe', 0, toYellow)
      word('caution', toYellow, toRed)
      word('danger', toRed, total)
    }
    // The badge in the disc fades in as the needle reaches the reading (not before: it names where the needle lands).
    const badgeEl = el.querySelector<HTMLElement>('[data-badge]')
    if (badgeEl) running.push(badgeEl.animate([{ opacity: 0, scale: 0.9 }, { opacity: 1, scale: 1 }],
      { duration: BADGE_FADE, delay: reach(now), easing: 'cubic-bezier(0.2, 0, 0, 1)', fill: 'backwards' }))
    return () => running.forEach((a) => a.cancel())
  }, [now, END, amberAt, redAt, level])

  const big = { x: -80, y: -80, width: 500, height: 400 }
  return <figure ref={root} className={styles.dial} data-level={level} data-blend={blend || undefined} style={timing} role="img" aria-label={label}>
    <svg viewBox="-16 -64 372 280" className={styles.svg} aria-hidden>
      {words && <>
        <text x={CX - RO * WORDS_SCALE - WORDS_GAP} y={CY - 14} className={styles.scaleWord} textAnchor="end" dominantBaseline="central">{t('gauge.low')}</text>
        <text x={CX} y={CY - RO * WORDS_SCALE - WORDS_GAP} className={styles.scaleWord} textAnchor="middle" dominantBaseline="central">{t('gauge.medium')}</text>
        <text x={CX + RO * WORDS_SCALE + WORDS_GAP} y={CY - 14} className={styles.scaleWord} textAnchor="start" dominantBaseline="central">{t('gauge.high')}</text>
      </>}
      <g transform={words ? `translate(${CX} ${CY}) scale(${WORDS_SCALE}) translate(${-CX} ${-CY})` : undefined}>
      <defs>
        {/* Deep at the inner edge, the level colour through the band, light at the outer edge. */}
        <radialGradient id={ids.fill} gradientUnits="userSpaceOnUse" cx={CX} cy={CY} r={RO}>
          <stop offset={RI / RO} className={styles.deep} data-stop="deep" />
          <stop offset={(RI + BAND * 0.45) / RO} className={styles.mid} data-stop="mid" />
          <stop offset="1" className={styles.light} data-stop="light" />
        </radialGradient>
        {/* The sweep: a band-wide stroke drawn from the left end, following the needle. */}
        <mask id={ids.sweep} maskUnits="userSpaceOnUse" {...big}>
          <path d={arc(0, END, RM)} pathLength={1} className={styles.sweepStroke} strokeWidth={BAND + 4} data-sweep />
        </mask>
        {/* The lower ends fade into the sheet. The mask reaches well past the ring, so the blur is never cut. */}
        <linearGradient id={ids.fade} gradientUnits="userSpaceOnUse" x1="0" y1={CY - RO} x2="0" y2={CY}>
          <stop offset="0.55" stopColor="white" />
          <stop offset="1" stopColor="white" stopOpacity="0" />
        </linearGradient>
        <mask id={ids.fadeMask} maskUnits="userSpaceOnUse" {...big}>
          <rect {...big} fill={`url(#${ids.fade})`} />
        </mask>
        <pattern id={ids.dots} patternUnits="userSpaceOnUse" width="19" height="19">
          <circle cx="9.5" cy="9.5" r="1.1" className={styles.dot} />
        </pattern>
        <filter id={ids.blur} filterUnits="userSpaceOnUse" {...big}><feGaussianBlur stdDeviation="14" /></filter>
        {/* Glass on the fill: a sheen bright at the outer edge, clearing toward the middle of the band. */}
        {/* Blended fill's depth: a little darker at the inner edge, lighter at the outer, over the coloured slices. */}
        <radialGradient id={ids.shade} gradientUnits="userSpaceOnUse" cx={CX} cy={CY} r={RO}>
          <stop offset={RI / RO} stopColor="black" stopOpacity="0.14" />
          <stop offset={(RI + BAND * 0.45) / RO} stopColor="black" stopOpacity="0" />
          <stop offset="1" stopColor="white" stopOpacity="0.4" />
        </radialGradient>
        <radialGradient id={ids.glass} gradientUnits="userSpaceOnUse" cx={CX} cy={CY} r={RO}>
          <stop offset={RI / RO} stopColor="white" stopOpacity="0.18" />
          <stop offset={(RI + BAND * 0.55) / RO} stopColor="white" stopOpacity="0" />
          <stop offset={(RO - 10) / RO} stopColor="white" stopOpacity="0.28" />
          <stop offset="1" stopColor="white" stopOpacity="0.55" />
        </radialGradient>
        {/* The grains travel with the needle: a soft wedge just behind it, turning with it, lifts them; the rest stay quiet. */}
        <filter id={ids.trailBlur} filterUnits="userSpaceOnUse" {...big}><feGaussianBlur stdDeviation="7" /></filter>
        <mask id={ids.trail} maskUnits="userSpaceOnUse" {...big}>
          <g className={styles.turn} data-turn>
            <path d={sector(0.4, 0.5)} fill="white" filter={`url(#${ids.trailBlur})`} />
          </g>
        </mask>
        <filter id={ids.shadow} filterUnits="userSpaceOnUse" {...big}><feGaussianBlur stdDeviation="1.5" /></filter>
        {/* 3 blocks: everything but the gaps — a straight cut across the band at each colour change. */}
        {split && <mask id={ids.cut} maskUnits="userSpaceOnUse" {...big}>
          <rect {...big} fill="white" />
          {[edges.safe, edges.caution].map((f) => {
            const [x1, y1] = point(f, RI - 4)
            const [x2, y2] = point(f, RO + 4)
            return <line key={f} x1={x1} y1={y1} x2={x2} y2={y2} stroke="black" strokeWidth={CUT} />
          })}
        </mask>}
      </defs>

      <g mask={`url(#${ids.fadeMask})`}>
        {/* Layer blur: a glow of each level's colour behind it, on as the needle reaches it, off as it moves on. */}
        {levels.filter((l) => l.from < now).map((l) => {
          const last = now <= l.to
          const on = l.from === 0 ? DELAY : reach(l.from)
          const off = reach(Math.min(l.to, now)) + 300
          return <path key={l.tone} d={arc(l.from + 0.02, Math.min(l.to, now) - 0.01, RM)} className={styles.glow} data-tone={l.tone}
            data-last={last || undefined} strokeWidth={BAND + 16} filter={`url(#${ids.blur})`}
            style={{ '--glow-in': ms(on), '--glow-for': ms(off - on) } as CSSProperties} />
        })}

        {/* The unfilled rest: a faint tint of the current colour. */}
        <path d={sector(0, 1)} className={styles.rest} data-paint="light" mask={split ? `url(#${ids.cut})` : undefined} />

        {/* The fill, its glass and grains, revealed by the sweep. */}
        <g mask={split ? `url(#${ids.cut})` : undefined}><g mask={`url(#${ids.sweep})`}>
          {blend
            ? <>
              {Array.from({ length: SLICES }, (_, i) => {
                const from = (i / SLICES) * END
                const to = Math.min(END, ((i + 1) / SLICES) * END + 0.003) // a hair of overlap: no seams between slices
                return <path key={i} d={sector(from, to)} style={{ fill: blendColour((from + to) / 2, split, edges) }} />
              })}
              <path d={sector(0, END)} fill={`url(#${ids.shade})`} />
            </>
            : <path d={sector(0, END)} fill={`url(#${ids.fill})`} />}
          <path d={sector(0, END)} fill={`url(#${ids.glass})`} />
          <path d={arc(0.02, END - 0.01, RO - 9)} className={styles.glassLine} strokeWidth={3} filter={`url(#${ids.shadow})`} />
          <path d={sector(0, END)} className={styles.glassRim} />
          {/* The grains the needle leaves on each level: they fade away from the green and yellow levels once the needle
              has moved on; only the red level keeps a few. */}
          {levels.map((l) => <path key={l.tone} d={sector(l.from, Math.min(l.to, END))} fill={`url(#${ids.dots})`}
            className={styles.dotsPassed} data-grains={l.tone} />)}
          <g mask={`url(#${ids.trail})`}>
            <path d={sector(0, END)} fill={`url(#${ids.dots})`} className={styles.dots} />
          </g>
        </g></g>



        {/* Ticks near the inner edge, all the way round; quieter on the unfilled part. */}
        {Array.from({ length: 13 }, (_, i) => {
          const f = (i + 0.5) / 13
          const [x1, y1] = point(f, RI + 12)
          const [x2, y2] = point(f, RI + 20)
          return <line key={i} x1={x1} y1={y1} x2={x2} y2={y2} className={styles.tick} data-filled={f <= now || undefined} />
        })}

        {/* A soft bloom at the tip. */}
        <circle cx={tipX} cy={tipY} r={BAND / 2} className={styles.bloom} data-paint="mid" filter={`url(#${ids.blur})`} />
      </g>

      {/* The needle: solid black, standing on the disc (its foot tucks under it), most of the way across the band. */}
      <g className={styles.turn} data-turn>
        <rect x={CX - 3} y={CY - RO + 18} width={6} height={RO - 18 - RI + 8} rx={3} className={styles.needle} />
      </g>

      {/* The disc: the multiple and the level word (no sub line, 19 Nov). */}
      <circle cx={CX} cy={CY} r={RI} className={styles.disc} />
      {/* "With multiple" (19 Nov): the multiple, big, above the level word. */}
      {number && <text x={CX} y={CY - 38} className={styles.value} textAnchor="middle">{ratio}X</text>}
      {/* 3 blocks · Low–High: no word in the dial (the risk is in the tag under it). */}
      {!words && (['safe', 'caution', 'danger'] as const).map((tone) =>
        <text key={tone} x={CX} y={number ? CY - 6 : CY - 22} className={styles.level} data-word={tone} textAnchor="middle">
          {/* 3 blocks · Low–High: the word follows the scale — Low risk · Medium risk · High risk. */}
          {t(tone === 'safe' ? (words ? 'nudge.levelLow' : 'nudge.levelSafe') : tone === 'caution' ? (words ? 'nudge.levelMedium' : 'nudge.levelMid') : 'nudge.highRisk')}
        </text>)}
      </g>
    </svg>
    {badge && <div className={styles.badge} data-badge style={{ top: `${((BADGE_Y - 6) / (CY - 6)) * 100}%` }}>{badge}</div>}
  </figure>
}
```

### `src/flows/nudges/sheets/TradeProtectSheet.module.css`

```css
/* Trade protect sheet (TradeProtectSheet.tsx), from Figma "Nudges" (6928:31781), on L3 tokens. Figma sizes L3 has no
   token for are the marked --app-protect-* local tokens (src/local-tokens.css). */

/* Figma's sheet: 24 above the picture (the L3 header's own top), 24 under the last part, then the dock. The wave is drawn
   from the content's top and clipped by it. */
.sheet [data-sheet-content] { position: relative; padding-top: var(--l3-spacing-24); padding-bottom: var(--l3-spacing-24); }

/* The picture, then the words; the gap between them by the picture (Figma: 12 icon · 16 illustration · 24 alone). */
.head { position: relative; display: flex; flex-direction: column; align-items: center; text-align: center; gap: var(--l3-spacing-16); }
.head[data-gap='12'] { gap: var(--l3-spacing-12); }
.head[data-gap='24'] { gap: var(--l3-spacing-24); }
.words { display: flex; flex-direction: column; align-items: center; gap: var(--l3-spacing-08); width: 100%; }
.heading { margin: 0; font: var(--l3-text-heading-20); color: var(--l3-content-primary); text-wrap: balance; }
.body { margin: 0; font: var(--l3-text-description-14); color: var(--l3-content-secondary); text-wrap: pretty; }
.pnl { font: var(--l3-text-label-14); }
.pnl[data-tone='loss'] { color: var(--l3-content-accent-error-default); }
.pnl[data-tone='profit'] { color: var(--l3-content-accent-success-default); }
.slot { position: relative; margin-top: var(--l3-spacing-16); }

/* Figma's pink wave (Ellipse 3): the error light tint, blurred, behind the top of the sheet. */
.wave {
  position: absolute; top: 0; left: 0; width: 100%; height: var(--l3-size-96);
  overflow: visible; fill: var(--l3-surface-accent-error-light);
  filter: blur(var(--app-protect-wave-blur)); pointer-events: none;
}

/* Illustrations: Figma's 120 crops (calendar, warning, candles). */
.illustration { display: block; width: var(--app-protect-illustration); height: var(--app-protect-illustration); }

/* Figma 1 · the shield: 80 in a 100 box, its lower half fading into the sheet, "High Risk" (Label/10 at 12, 2 apart) over it. */
.shield { position: relative; display: block; width: var(--app-protect-hero); height: var(--app-protect-hero); }
.shieldArt { position: absolute; top: var(--l3-spacing-10); left: var(--l3-spacing-10); width: var(--l3-size-80); height: var(--l3-size-80); }
.shieldFade {
  position: absolute; left: var(--l3-spacing-08); top: var(--app-protect-fade-top);
  width: var(--app-protect-fade-width); height: var(--app-protect-fade-height);
  background: linear-gradient(178deg, color-mix(in srgb, var(--l3-surface-primary) 0%, transparent) 3%, var(--l3-surface-primary) 76%);
}
.riskLabel {
  position: absolute; left: 50%; top: var(--app-protect-risk-label-y); translate: -50% -50%;
  font: var(--l3-text-label-10); font-size: var(--l3-font-size-100); letter-spacing: var(--app-protect-tracking);
  white-space: nowrap; color: var(--l3-content-accent-error-default);
}

/* Icons on discs. dot (80): a light disc (66.67) holding a solid one (48) with a white glyph (22.67).
   hero (100): a light disc (83.33) with the glyph (56) in the accent colour. */
.disc { display: grid; place-items: center; }
.disc[data-style='dot'] { width: var(--l3-size-80); height: var(--l3-size-80); }
.disc[data-style='hero'] { width: var(--app-protect-hero); height: var(--app-protect-hero); }
.inner { display: grid; place-items: center; border-radius: var(--l3-radius-full); background: var(--disc-light); }
.disc[data-style='dot'] .inner { width: var(--app-protect-dot-light); height: var(--app-protect-dot-light); }
.disc[data-style='hero'] .inner { width: var(--app-protect-hero-light); height: var(--app-protect-hero-light); }
.glyph { display: block; color: var(--disc-solid); }
.disc[data-style='dot'] .glyph {
  width: var(--l3-size-48); height: var(--l3-size-48); border-radius: var(--l3-radius-full);
  background: var(--disc-solid); color: var(--l3-static-white);
  padding: calc((var(--l3-size-48) - var(--app-protect-dot-glyph)) / 2); box-sizing: border-box;
}
.disc[data-style='hero'] .glyph { width: var(--l3-size-56); height: var(--l3-size-56); }
.disc[data-tone='error'] { --disc-light: var(--l3-surface-accent-error-light); --disc-solid: var(--l3-surface-accent-error-default); }
.disc[data-tone='success'] { --disc-light: var(--l3-surface-accent-success-light); --disc-solid: var(--l3-surface-accent-success-default); }
.disc[data-style='hero'][data-tone='error'] .glyph { color: var(--l3-content-accent-error-default); }
.disc[data-style='hero'][data-tone='success'] .glyph { color: var(--l3-content-accent-success-default); }

/* The tool icons: 32 box (radius 8) in the list, 36 (radius 9) in the card; icon 20 / 22.5. */
.toolBox {
  display: grid; place-items: center; flex: none;
  width: var(--l3-size-32); height: var(--l3-size-32); border-radius: var(--l3-radius-08);
  background: var(--l3-surface-secondary); color: var(--l3-content-primary);
  --tool-icon: var(--l3-size-20);
}
.toolBox[data-size='lg'] { width: var(--app-protect-tool-box); height: var(--app-protect-tool-box); border-radius: var(--app-protect-tool-radius); --tool-icon: var(--app-protect-tool-icon); }
.pnlIcon { display: block; width: var(--tool-icon); height: var(--tool-icon); }

/* Auto TP/SL (Figma's animated icon): candle 4.8 × 11.9 in the middle, the target line above-left, the stop below-right. */
.tpsl { position: relative; display: block; width: var(--tool-icon); height: var(--tool-icon); }
.tpsl > span { position: absolute; left: 50%; top: 50%; display: block; }
.tpslCandle { width: 24%; height: 60%; translate: calc(-50% + 1.4%) calc(-50% - 2.2%); animation: tpsl-candle 2s infinite; }
.tpslTp { width: 34%; height: 6%; translate: calc(-50% - 8.6%) calc(-50% - 40%); animation: tpsl-line 2s infinite; --line-in: 0.15; }
.tpslSl { width: 34%; height: 6%; translate: calc(-50% + 10.7%) calc(-50% + 35.6%); animation: tpsl-line-2 2s infinite; }
@keyframes tpsl-candle {
  0% { opacity: 0; transform: scaleY(0.15); animation-timing-function: ease-out; }
  17.5%, 100% { opacity: 1; transform: none; }
}
@keyframes tpsl-line {
  0%, 15% { opacity: 0; transform: translateX(30%); animation-timing-function: cubic-bezier(0.2, 0, 0.2, 1.3); }
  27.5%, 100% { opacity: 1; transform: none; }
}
@keyframes tpsl-line-2 {
  0%, 22.5% { opacity: 0; transform: translateX(30%); animation-timing-function: cubic-bezier(0.2, 0, 0.2, 1.3); }
  35%, 100% { opacity: 1; transform: none; }
}
@media (prefers-reduced-motion: reduce) { .tpsl > span { animation: none; } }

.rowText { font: var(--l3-text-label-12); color: var(--l3-content-primary); text-align: left; }

/* Figma 1 · RECOMMENDED: a grey head (Label/12, 2 apart, capitals) over the rows, one bordered box. */
.list { width: 100%; text-align: left; }
.listHead {
  margin: 0; padding: var(--l3-spacing-08) var(--l3-spacing-12);
  border: 1px solid var(--l3-border-light); /* 1px: Figma stroke weight has no variable */
  border-radius: var(--l3-radius-12) var(--l3-radius-12) 0 0;
  background: var(--l3-surface-secondary);
  font: var(--l3-text-label-12); letter-spacing: var(--app-protect-tracking); text-transform: uppercase; text-align: center;
  color: var(--l3-content-primary);
}
.listBody {
  display: grid; gap: var(--l3-spacing-12); padding: var(--l3-spacing-12);
  border: 1px solid var(--l3-border-light); border-top: 0; /* 1px: Figma stroke weight has no variable */
  border-radius: 0 0 var(--l3-radius-12) var(--l3-radius-12);
}
.listRow { display: flex; align-items: center; gap: var(--l3-spacing-12); }

/* Figma 2 · one recommended tool. Figma 6 · the stop-loss price. */
.card, .price {
  display: flex; align-items: center; gap: var(--l3-spacing-08); padding: var(--l3-spacing-12);
  border: 1px solid var(--l3-border-light); border-radius: var(--l3-radius-12); /* 1px: Figma stroke weight has no variable */
  background: var(--l3-surface-primary); text-align: left;
}
.price { align-items: flex-end; justify-content: space-between; }
.cardText { display: flex; flex-direction: column; align-items: flex-start; gap: var(--l3-spacing-04); min-width: 0; }
.priceValue { font: var(--l3-text-heading-14); color: var(--l3-content-primary); white-space: nowrap; font-variant-numeric: tabular-nums; }

/* Figma 4 / 5 · his figures side by side, 50-tall rules between, white fading to the error tint. */
.stats {
  display: flex; align-items: center; padding: var(--l3-spacing-12) var(--l3-spacing-16);
  border: 1px solid var(--l3-border-light); border-radius: var(--l3-radius-12); /* 1px: Figma stroke weight has no variable */
  background: linear-gradient(var(--l3-surface-primary), color-mix(in srgb, var(--l3-surface-accent-error-light) 45%, var(--l3-surface-primary)));
}
.stat { flex: 1 1 0; display: flex; flex-direction: column; gap: var(--l3-spacing-08); min-width: 0; }
.stat + .stat { border-left: 1px solid var(--l3-border-light); } /* 1px: Figma stroke weight has no variable */
.stat[data-align='start'] { align-items: flex-start; text-align: left; }
.stat[data-align='center'] { align-items: center; text-align: center; }
.stat[data-align='end'] { align-items: flex-end; text-align: right; }
.stat { min-height: var(--app-protect-stat-rule); justify-content: center; }
.statLabel { font: var(--l3-text-label-12); color: var(--l3-content-tertiary); }
.statValue { display: inline-flex; align-items: flex-start; font: var(--l3-text-heading-18); color: var(--l3-content-primary); font-variant-numeric: tabular-nums; white-space: nowrap; }
.statValue[data-tone='loss'] { color: var(--l3-content-accent-error-default); }
.statValue[data-tone='profit'] { color: var(--l3-content-accent-success-default); }
.up { display: block; width: var(--l3-size-24); height: var(--l3-size-24); color: var(--l3-content-accent-error-default); }
```

### `src/flows/nudges/sheets/TradeProtectSheet.tsx`

```tsx
import { useId } from 'react'
import { Button } from '@l3/components/Button'
import { ButtonGroup } from '@l3/components/ButtonGroup'
import { MaskIcon } from '@l3/components/MaskIcon'
import { Tag } from '@l3/components/Tag'
import { msAccountBalanceWallet, msCalendarMonth, msCandlestickChart, msFlag, msShield, msTrendingUp } from '@l3/icons/material'
import { Sheet } from '../../../shared/ui/Sheet'
import { t } from '../copy'
import { protectById, type ProtectArt, type ProtectContent, type ProtectUseCase, type ProtectUseCaseId } from '../data'
import shieldArt from '../assets/protect/shield.svg'
import calendarArt from '../assets/protect/calendar.png'
import warningArt from '../assets/protect/warning.png'
import candlesArt from '../assets/protect/candles.png'
import trendDownGlyph from '../assets/protect/trend-down.svg'
import warningGlyph from '../assets/protect/warning-glyph.svg'
import arrowUp from '../assets/protect/arrow-up.svg'
import pnlProtectIcon from '../assets/protect/pnl-protect.svg'
import tpslCandle from '../assets/protect/tpsl-candle.svg'
import tpslTp from '../assets/protect/tpsl-tp.svg'
import tpslSl from '../assets/protect/tpsl-sl.svg'
import styles from './TradeProtectSheet.module.css'

type Key = Parameters<typeof t>[0]

/** Prototype setting "Trade protect · version": Figma's two drawings where it has two, else Figma's and the other picture. */
export type ProtectVersionId = 'v1' | 'v2'

const illustrations = { shield: shieldArt, calendar: calendarArt, warning: warningArt, candles: candlesArt }
const glyphs = { trendDown: trendDownGlyph, warning: warningGlyph, trendUp: msTrendingUp, wallet: msAccountBalanceWallet, candles: msCandlestickChart, calendar: msCalendarMonth, shield: msShield, flag: msFlag }

/**
 * Trade protect — the nudge sheet from Figma "Nudges" (LM → F&O Playground 6928:31781, 23 Nov). ONE sheet for every use
 * case; a use case fills its slots (data.ts protectUseCases, copy.json protect.<id>.*):
 * - the picture — Figma's illustration (shield with "High Risk", calendar, warning, candles) on a pink wave, or a glyph
 *   on discs (80 "dot": a solid disc on a light one · 100 "hero": the glyph on a light disc);
 * - a tag (the P&L figure, or High Risk), the heading (Heading/20), one line (Description/14) — or the P&L figure itself;
 * - under it: RECOMMENDED tools, one recommended tool, his figures side by side, or the stop-loss price;
 * - the primary button opens the tool (PnL Protect or TP/SL); the secondary is "Not now, place order" (an order in
 *   hand) or "Not now, I will trade on my own".
 * Spacing as Figma's L3 sheet header: 24 above the picture; 12 (icon) / 16 (illustration) / 24 (illustration alone)
 * from the picture to the words; 8 between the words; 16 to the content; 24 to the dock.
 */
export function TradeProtectSheet({ useCaseId, version = 'v1', onTool, onDismiss }: { useCaseId: ProtectUseCaseId; version?: ProtectVersionId; onTool: () => void; onDismiss: () => void }) {
  const id = useId()
  const useCase = protectById.get(useCaseId)!
  const v = useCase.versions[version === 'v2' ? 1 : 0]
  const say = (slot: string) => t(`protect.${useCase.id}.${slot}` as Key, useCase.values)
  const wave = v.art.kind === 'illustration' && v.art.wave
  const gap = v.art.kind === 'icon' ? '12' : v.content.kind === 'none' && !v.tag ? '24' : '16'

  const footer = <ButtonGroup aria-label={t('protect.actions')} direction="vertical">
    <Button size="lg" onClick={onTool}>{say('cta')}</Button>
    <Button size="lg" variant="secondary" onClick={onDismiss}>{t(`protect.dismiss.${useCase.dismiss}` as Key)}</Button>
  </ButtonGroup>

  return <Sheet labelledBy={id} onClose={onDismiss} className={styles.sheet} footer={footer}>
    {wave && <Wave />}
    <div className={styles.head} data-gap={gap}>
      <Art art={v.art} />
      <div className={styles.words}>
        {v.tag && <Tag size="md" variant="secondary" color={v.tag.tone}>{t(`protect.tag.${v.tag.key}` as Key, useCase.values)}</Tag>}
        <h2 id={id} className={styles.heading}>{say('heading')}</h2>
        {v.body === 'pnlLine'
          ? <p className={styles.body}>{t('protect.pnlLine')} <span className={styles.pnl} data-tone={useCase.values.pnl?.startsWith('+') ? 'profit' : 'loss'}>{useCase.values.pnl}</span></p>
          : <p className={styles.body}>{say('body')}</p>}
      </div>
    </div>
    {v.content.kind !== 'none' && <div className={styles.slot}><Content content={v.content} useCase={useCase} /></div>}
  </Sheet>
}

/** The picture. */
function Art({ art }: { art: ProtectArt }) {
  if (art.kind === 'illustration' && art.name === 'shield') {
    // Figma 1: the shield (80) in a 100 box, its lower half fading into the sheet, "High Risk" over the fade.
    return <span className={styles.shield}>
      <img src={shieldArt} alt="" className={styles.shieldArt} />
      <span className={styles.shieldFade} />
      {art.riskLabel && <span className={styles.riskLabel}>{t('protect.riskLabel')}</span>}
    </span>
  }
  if (art.kind === 'illustration') return <img src={illustrations[art.name]} alt="" className={styles.illustration} />
  return <span className={styles.disc} data-style={art.style} data-tone={art.tone} aria-hidden="true">
    <span className={styles.inner}><span className={styles.glyph}><MaskIcon src={glyphs[art.glyph]} /></span></span>
  </span>
}

/** Figma's pink wave across the top of the sheet (Ellipse 3: the error light tint, blurred 17.65). */
function Wave() {
  return <svg className={styles.wave} viewBox="0 0 360 96" preserveAspectRatio="none" overflow="visible" aria-hidden="true">
    <path transform="translate(-55.3 -98.3)" d="M428.3 101.813C428.3 193.3 439.216 184.953 231.8 115.8C123.276 115.8 35.3 221.862 35.3 101.813C35.3 65.079 123.276 35.3 231.8 35.3C340.324 35.3 428.3 65.079 428.3 101.813Z" />
  </svg>
}

/** Figma's Auto TP/SL icon: a candle that grows in, then the target and stop lines slide in (2 s, looping). */
function TpslIcon() {
  return <span className={styles.tpsl} aria-hidden="true">
    <span className={styles.tpslCandle}><MaskIcon src={tpslCandle} /></span>
    <span className={styles.tpslTp}><MaskIcon src={tpslTp} /></span>
    <span className={styles.tpslSl}><MaskIcon src={tpslSl} /></span>
  </span>
}

const toolIcon = (item: 'pnl' | 'tpsl' | 'autoTpsl') => item === 'pnl'
  ? <span className={styles.pnlIcon}><MaskIcon src={pnlProtectIcon} /></span>
  : <TpslIcon />

/** What sits under the words. */
function Content({ content, useCase }: { content: Exclude<ProtectContent, { kind: 'none' }>; useCase: ProtectUseCase }) {
  if (content.kind === 'list') {
    return <div className={styles.list}>
      <p className={styles.listHead}>{t('protect.recommended')}</p>
      <div className={styles.listBody}>
        {content.items.map((item) => <div key={item} className={styles.listRow}>
          <span className={styles.toolBox}>{toolIcon(item)}</span>
          <span className={styles.rowText}>{t(`protect.item.${item}` as Key)}</span>
        </div>)}
      </div>
    </div>
  }
  if (content.kind === 'card') {
    return <div className={styles.card}>
      <span className={styles.toolBox} data-size="lg">{toolIcon(content.item)}</span>
      <div className={styles.cardText}>
        <Tag size="sm" variant="tertiary" color="discover">{t('protect.recommended')}</Tag>
        <span className={styles.rowText}>{t(`protect.item.${content.item}` as Key, useCase.values)}</span>
      </div>
    </div>
  }
  if (content.kind === 'stats') {
    return <div className={styles.stats}>
      {content.stats.map((s, i) => <div key={s.label} className={styles.stat} data-align={i === 0 ? 'start' : i === content.stats.length - 1 ? 'end' : 'center'}>
        <span className={styles.statLabel}>{t(`protect.stat.${s.label}` as Key)}</span>
        <span className={styles.statValue} data-tone={s.tone}>
          {s.up && <span className={styles.up}><MaskIcon src={arrowUp} /></span>}{s.value}
        </span>
      </div>)}
    </div>
  }
  return <div className={styles.price}>
    <div className={styles.cardText}>
      <Tag size="sm" variant="tertiary" color="discover">{t('protect.recommended')}</Tag>
      <span className={styles.statLabel}>{t('protect.price')}</span>
    </div>
    <span className={styles.priceValue}>{content.value}</span>
  </div>
}
```

### `src/flows/nudges/sheets/gaugeArt.ts`

```ts
// GENERATED from the Figma speedometer (LM → F&O Playground 6916:62677 "_x2014_ÎÓÈ_x5F_3", 20 Nov): its paths and
// fills exactly as exported, in a 141.435 × 78.6169 box. A brand illustration (like L3's selected nav icons): its
// colours are Figma's own, not tokens. Split so the parts can move: the six segments left → right (thin rim + thick
// band), the black ring, the dark face and the white needle (pivot = the hub's centre).
export const GAUGE_W = 141.435
export const GAUGE_H = 78.6169
export const NEEDLE_PIVOT = { x: 70.7165, y: 68.9279 }
/** The needle as drawn points 39° above the right horizontal: 78.3 on a 0–100 scale. */
export const NEEDLE_DRAWN_AT = 78.3
export const segments: { rim: { d: string; fill: string }; band: { d: string; fill: string } }[] = [
  { rim: { d: 'M9.47328 35.2943L10.6659 35.9811C4.76477 46.1627 1.38627 57.9803 1.38627 70.5896H0C0 57.7234 3.43846 45.6646 9.45391 35.2841L9.47328 35.2943Z', fill: '#97FF64' }, band: { d: 'M22.211 69.0994C22.2156 68.9521 22.2221 68.8057 22.2276 68.6584C22.2415 68.2956 22.2599 67.9347 22.2821 67.5748C22.2913 67.4265 22.2996 67.2774 22.3106 67.1292C22.342 66.6799 22.3789 66.2315 22.4232 65.785C22.4269 65.7454 22.4296 65.7058 22.4333 65.6672C22.4822 65.1792 22.5412 64.694 22.6049 64.2097C22.6215 64.0809 22.6408 63.952 22.6593 63.8231C22.7109 63.4576 22.7653 63.093 22.8253 62.7302C22.8474 62.5931 22.8696 62.4559 22.8936 62.3196C22.9673 61.8924 23.0457 61.468 23.1306 61.0454C23.1407 60.9957 23.149 60.946 23.1592 60.8963C23.257 60.4157 23.363 59.9379 23.4746 59.4628C23.4986 59.3616 23.5244 59.2612 23.5484 59.1599C23.6397 58.7825 23.7356 58.4068 23.8362 58.0321C23.8685 57.9134 23.8998 57.7937 23.933 57.6749C24.0474 57.2606 24.1673 56.8472 24.2927 56.4375C24.3075 56.3897 24.3213 56.3409 24.3361 56.293C24.4818 55.8207 24.6349 55.3521 24.7954 54.8853C24.8185 54.8181 24.8424 54.7518 24.8664 54.6846C25.0029 54.2915 25.145 53.902 25.2916 53.5135C25.3294 53.4132 25.3673 53.3137 25.406 53.2143C25.5609 52.8111 25.7214 52.4096 25.8874 52.0119C25.9059 51.9677 25.9234 51.9235 25.9419 51.8793C26.1346 51.419 26.3348 50.9624 26.5423 50.5094C26.5571 50.4781 26.5718 50.4468 26.5866 50.4146C26.7729 50.0086 26.9657 49.6062 27.163 49.2067C27.2045 49.1229 27.246 49.04 27.2875 48.9562C27.4812 48.5705 27.6786 48.1875 27.8815 47.8073C27.9055 47.7631 27.9286 47.718 27.9526 47.6728C28.1905 47.2309 28.4349 46.7936 28.6858 46.36L10.6671 35.9805C4.76602 46.1611 1.3866 57.9806 1.3866 70.5881H22.1861C22.1861 70.09 22.1963 69.5947 22.211 69.0994Z', fill: '#7BDB44' } },
  { rim: { d: 'M35.3587 9.45586L36.0468 10.6463C25.5248 16.7226 16.7534 25.4781 10.666 35.981L9.47347 35.2942L9.4541 35.2831C15.6605 24.5648 24.6099 15.6316 35.3477 9.43652L35.3587 9.45586Z', fill: '#E2FF64' }, band: { d: 'M28.6829 46.3626C28.9283 45.9391 29.1819 45.5202 29.4402 45.1049C29.4854 45.0322 29.5315 44.9595 29.5767 44.8867C29.8229 44.4945 30.0738 44.106 30.3311 43.7212C30.3477 43.6963 30.3643 43.6715 30.3809 43.6466C30.6659 43.2231 30.9565 42.8042 31.2544 42.3899C31.2784 42.3568 31.3033 42.3236 31.3272 42.2896C31.5929 41.9222 31.8631 41.5595 32.1389 41.1995C32.1906 41.1323 32.2422 41.0651 32.2939 40.9979C32.9035 40.2107 33.5362 39.442 34.192 38.6935C34.2354 38.6447 34.2787 38.5959 34.3221 38.5471C34.6117 38.2193 34.9059 37.8962 35.2038 37.5767C35.2573 37.5196 35.3108 37.4616 35.3643 37.4045C36.0459 36.6818 36.7487 35.9803 37.4728 35.2999C37.5299 35.2465 37.5871 35.194 37.6443 35.1406C37.9653 34.8423 38.2899 34.5487 38.6183 34.2586C38.6672 34.2154 38.7151 34.1721 38.764 34.1298C39.5139 33.4742 40.284 32.8427 41.0735 32.2341C41.14 32.1826 41.2073 32.131 41.2746 32.0804C41.6352 31.8051 41.9996 31.5344 42.3676 31.2693C42.4008 31.2453 42.4331 31.2214 42.4663 31.1975C42.8813 30.9001 43.301 30.6091 43.7262 30.3247C43.7511 30.3081 43.776 30.2924 43.8 30.2759C44.1855 30.019 44.5756 29.7677 44.9695 29.5219C45.0423 29.4767 45.1143 29.4307 45.1871 29.3865C45.604 29.1287 46.0237 28.8755 46.448 28.6307L36.0478 10.6465C25.5267 16.7228 16.7544 25.4792 10.667 35.9812L28.6829 46.3626Z', fill: '#A6DA45' } },
  { rim: { d: 'M70.7164 0V1.38375C58.0842 1.38375 46.2451 4.75521 36.045 10.6465L35.357 9.4561L35.3459 9.43676C45.7461 3.43314 57.8268 0 70.7164 0Z', fill: '#FFFF6B' }, band: { d: 'M47.7632 27.8969C47.8075 27.873 47.8527 27.8499 47.8969 27.8269C48.2779 27.6235 48.6625 27.4264 49.0489 27.2331C49.1319 27.1917 49.215 27.1502 49.2989 27.1097C49.7001 26.9127 50.1032 26.7203 50.5099 26.5334C50.5413 26.5187 50.5726 26.5039 50.604 26.4901C51.0578 26.2839 51.5153 26.0841 51.9764 25.8908C52.0207 25.8724 52.065 25.8549 52.1083 25.8374C52.5077 25.6717 52.9098 25.5115 53.3138 25.3568C53.4134 25.3191 53.513 25.2813 53.6126 25.2436C54.0019 25.0972 54.3929 24.9554 54.7868 24.8191C54.8532 24.7961 54.9196 24.7722 54.9869 24.7492C55.4536 24.5899 55.924 24.4361 56.3972 24.2907C56.4451 24.2759 56.4931 24.2621 56.541 24.2483C56.9524 24.1231 57.3656 24.0034 57.7816 23.8893C57.9006 23.8561 58.0195 23.8248 58.1385 23.7926C58.5139 23.6922 58.8902 23.5965 59.2684 23.5053C59.3689 23.4805 59.4694 23.4556 59.5709 23.4317C60.0468 23.3203 60.5255 23.2144 61.007 23.1168C61.0568 23.1067 61.1066 23.0984 61.1564 23.0883C61.5797 23.0036 62.0059 22.9253 62.4329 22.8517C62.5694 22.8277 62.7068 22.8056 62.8443 22.7836C63.2077 22.7246 63.5729 22.6694 63.9391 22.6178C64.0682 22.5994 64.1973 22.581 64.3265 22.5635C64.8107 22.5 65.2977 22.442 65.7865 22.3923C65.8262 22.3886 65.8658 22.3858 65.9046 22.3821C66.3519 22.338 66.8011 22.3011 67.2512 22.2698C67.3997 22.2597 67.5482 22.2505 67.6976 22.2413C68.0582 22.2192 68.4207 22.2008 68.7832 22.187C68.9298 22.1814 69.0774 22.175 69.225 22.1704C69.7203 22.1557 70.2165 22.1455 70.7155 22.1455V1.38281C58.085 1.38281 46.2441 4.75611 36.045 10.6465L46.4461 28.6288C46.8824 28.3775 47.3205 28.1344 47.7632 27.8969Z', fill: '#EAEA4E' } },
  { rim: { d: 'M106.088 9.43676L106.076 9.4561L105.388 10.6465C95.1883 4.75613 83.3465 1.38375 70.717 1.38375V0C83.6075 0 95.6873 3.43314 106.088 9.43676Z', fill: '#FFD073' }, band: { d: 'M72.2075 22.1686C72.3551 22.1732 72.5017 22.1797 72.6493 22.1852C73.0127 22.199 73.3743 22.2174 73.7349 22.2395C73.8834 22.2487 74.0328 22.257 74.1813 22.268C74.6314 22.2993 75.0806 22.3371 75.5279 22.3804C75.5676 22.384 75.6072 22.3868 75.646 22.3905C76.1348 22.4393 76.6209 22.4982 77.106 22.5617C77.2352 22.5783 77.3643 22.5976 77.4934 22.616C77.8596 22.6676 78.2248 22.7219 78.5882 22.7818C78.7256 22.8039 78.8631 22.826 78.9996 22.8499C79.4275 22.9235 79.8546 23.0018 80.2789 23.0865C80.3277 23.0966 80.3766 23.1049 80.4246 23.1141C80.906 23.2117 81.3847 23.3176 81.8616 23.429C81.963 23.4529 82.0636 23.4787 82.165 23.5026C82.5432 23.5938 82.9195 23.6895 83.2949 23.7899C83.4139 23.8221 83.5338 23.8534 83.6527 23.8866C84.0678 24.0007 84.4819 24.1204 84.8924 24.2456C84.9403 24.2603 84.9892 24.2742 85.0372 24.2889C85.5103 24.4343 85.9798 24.5881 86.4474 24.7474C86.5147 24.7704 86.5811 24.7943 86.6485 24.8183C87.0423 24.9545 87.4325 25.0963 87.8217 25.2427C87.9213 25.2804 88.0218 25.3182 88.1214 25.3569C88.5263 25.5124 88.9285 25.6717 89.3279 25.8374C89.3712 25.8558 89.4155 25.8724 89.4588 25.8908C89.92 26.0842 90.3784 26.284 90.8322 26.4902C90.8635 26.504 90.894 26.5187 90.9244 26.5335C91.3312 26.7194 91.7351 26.9128 92.1364 27.1098C92.2203 27.1512 92.3033 27.1926 92.3863 27.2341C92.7728 27.4274 93.1565 27.6244 93.5374 27.827C93.5817 27.8509 93.6269 27.8739 93.672 27.8979C94.1148 28.1354 94.5529 28.3794 94.9873 28.6298L105.388 10.6475C95.1893 4.75709 83.3484 1.38379 70.7179 1.38379V22.1456C71.216 22.1437 71.7122 22.1539 72.2075 22.1686Z', fill: '#FFAA00' } },
  { rim: { d: 'M131.981 35.2804L131.959 35.2942L130.767 35.981C124.679 25.4781 115.908 16.7226 105.389 10.6463L106.077 9.45586L106.088 9.43652C116.826 15.6289 125.775 24.562 131.981 35.2804Z', fill: '#FF935E' }, band: { d: 'M94.9863 28.6287C95.4106 28.8736 95.8303 29.1268 96.2462 29.3846C96.3191 29.4297 96.392 29.4757 96.4648 29.5208C96.8577 29.7666 97.247 30.0171 97.6325 30.2739C97.6574 30.2905 97.6823 30.3071 97.7072 30.3236C98.1315 30.6081 98.5521 30.8991 98.9671 31.1955C99.0003 31.2194 99.0326 31.2434 99.0658 31.2673C99.4338 31.5325 99.7981 31.8031 100.159 32.0784C100.226 32.13 100.293 32.1815 100.361 32.2331C101.15 32.8416 101.92 33.4732 102.669 34.1287C102.718 34.1711 102.766 34.2143 102.815 34.2576C103.143 34.5467 103.468 34.8413 103.788 35.1387C103.845 35.1921 103.903 35.2455 103.961 35.2989C104.685 35.9783 105.387 36.6808 106.069 37.4035C106.123 37.4606 106.176 37.5186 106.23 37.5757C106.528 37.8951 106.823 38.2192 107.112 38.547C107.156 38.5958 107.199 38.6436 107.241 38.6924C107.897 39.4409 108.531 40.2097 109.14 40.9969C109.192 41.0641 109.244 41.1313 109.295 41.1985C109.571 41.5585 109.842 41.9221 110.108 42.2895C110.132 42.3226 110.156 42.3548 110.18 42.388C110.478 42.8023 110.769 43.2212 111.053 43.6456C111.07 43.6704 111.087 43.6953 111.103 43.7202C111.361 44.105 111.611 44.4935 111.858 44.8857C111.904 44.9585 111.949 45.0312 111.994 45.1039C112.252 45.5191 112.506 45.938 112.751 46.3615L130.766 35.9793C124.679 25.4773 115.907 16.7209 105.386 10.6445L94.9863 28.6287Z', fill: '#DF632D' } },
  { rim: { d: 'M141.435 70.5894H140.049C140.049 57.9801 136.669 46.1625 130.767 35.9809L131.959 35.2941L131.981 35.2803C137.997 45.6644 141.435 57.7195 141.435 70.5894Z', fill: '#FF6E6E' }, band: { d: 'M112.752 46.3628C113.003 46.7964 113.247 47.2338 113.485 47.6757C113.509 47.7199 113.532 47.765 113.556 47.8101C113.759 48.1903 113.958 48.5733 114.15 48.9591C114.192 49.0419 114.233 49.1257 114.275 49.2086C114.472 49.6091 114.665 50.0114 114.852 50.4183C114.866 50.4496 114.881 50.48 114.896 50.5104C115.103 50.9633 115.303 51.4209 115.496 51.8812C115.515 51.9245 115.531 51.9687 115.55 52.012C115.716 52.4106 115.876 52.812 116.031 53.2162C116.07 53.3156 116.108 53.4151 116.145 53.5154C116.291 53.903 116.432 54.2934 116.57 54.6865C116.593 54.7537 116.618 54.82 116.641 54.8872C116.8 55.3531 116.954 55.8226 117.1 56.2949C117.115 56.3428 117.129 56.3916 117.143 56.4394C117.269 56.85 117.388 57.2625 117.503 57.6768C117.536 57.7956 117.568 57.9143 117.6 58.034C117.701 58.4078 117.796 58.7834 117.888 59.1618C117.913 59.2631 117.938 59.3634 117.962 59.4647C118.073 59.9398 118.179 60.4176 118.277 60.8991C118.287 60.9479 118.295 60.9967 118.305 61.0446C118.389 61.4681 118.468 61.8943 118.542 62.3215C118.566 62.4578 118.588 62.595 118.61 62.7321C118.669 63.0949 118.724 63.4595 118.776 63.825C118.794 63.9539 118.813 64.0827 118.83 64.2116C118.894 64.695 118.952 65.1811 119.002 65.669C119.006 65.7086 119.008 65.7482 119.012 65.7869C119.056 66.2334 119.093 66.6818 119.125 67.1311C119.135 67.2793 119.144 67.4275 119.153 67.5767C119.175 67.9366 119.194 68.2985 119.208 68.6603C119.213 68.8067 119.22 68.954 119.224 69.1013C119.239 69.5957 119.249 70.091 119.249 70.5891H140.049C140.049 57.9815 136.669 46.1621 130.768 35.9814L112.752 46.3628Z', fill: '#D83123' } },
]
export const ring = { d: 'M119.224 69.0989C119.219 68.9516 119.213 68.8053 119.207 68.6579C119.193 68.2961 119.175 67.9343 119.153 67.5743C119.144 67.4261 119.135 67.277 119.124 67.1287C119.093 66.6794 119.056 66.2311 119.012 65.7846C119.008 65.745 119.005 65.7054 119.002 65.6667C118.953 65.1788 118.894 64.6936 118.83 64.2093C118.813 64.0804 118.794 63.9515 118.776 63.8226C118.724 63.4571 118.67 63.0926 118.61 62.7298C118.587 62.5926 118.565 62.4555 118.541 62.3192C118.468 61.892 118.389 61.4657 118.304 61.0422C118.294 60.9935 118.286 60.9447 118.277 60.8968C118.179 60.4162 118.073 59.9384 117.961 59.4624C117.937 59.3611 117.911 59.2608 117.887 59.1595C117.796 58.782 117.7 58.4064 117.6 58.0317C117.567 57.9129 117.536 57.7932 117.503 57.6745C117.388 57.2602 117.269 56.8468 117.143 56.4371C117.128 56.3892 117.115 56.3404 117.1 56.2926C116.954 55.8203 116.801 55.3516 116.64 54.8849C116.617 54.8177 116.593 54.7514 116.569 54.6842C116.433 54.291 116.291 53.9016 116.144 53.5131C116.106 53.4137 116.069 53.3133 116.031 53.2139C115.875 52.8097 115.715 52.4083 115.549 52.0097C115.531 51.9664 115.514 51.9222 115.496 51.8789C115.302 51.4186 115.102 50.961 114.895 50.5081C114.882 50.4768 114.867 50.4464 114.852 50.416C114.666 50.01 114.472 49.6067 114.275 49.2062C114.233 49.1225 114.192 49.0396 114.15 48.9567C113.956 48.571 113.759 48.188 113.556 47.8078C113.532 47.7636 113.509 47.7185 113.485 47.6733C113.247 47.2314 113.003 46.7941 112.752 46.3605C112.507 45.937 112.253 45.5181 111.995 45.1029C111.949 45.0301 111.903 44.9574 111.858 44.8847C111.612 44.4925 111.361 44.1039 111.104 43.7191C111.087 43.6943 111.07 43.6694 111.054 43.6445C110.769 43.221 110.477 42.8012 110.18 42.3869C110.156 42.3538 110.132 42.3215 110.108 42.2884C109.843 41.9211 109.572 41.5574 109.296 41.1974C109.244 41.1302 109.193 41.063 109.141 40.9958C108.531 40.2077 107.899 39.439 107.242 38.6914C107.199 38.6426 107.156 38.5947 107.113 38.5459C106.823 38.2182 106.529 37.8941 106.23 37.5746C106.177 37.5175 106.123 37.4595 106.07 37.4025C105.388 36.6797 104.685 35.9782 103.961 35.2978C103.904 35.2444 103.846 35.191 103.789 35.1376C103.469 34.8393 103.144 34.5457 102.816 34.2566C102.767 34.2133 102.719 34.17 102.67 34.1277C101.92 33.4731 101.15 32.8406 100.361 32.232C100.294 32.1805 100.227 32.1289 100.159 32.0774C99.7986 31.8021 99.4343 31.5314 99.0663 31.2663C99.0331 31.2423 99.0008 31.2184 98.9676 31.1945C98.5526 30.8971 98.1329 30.6062 97.7077 30.3226C97.6828 30.306 97.6579 30.2894 97.633 30.2729C97.2475 30.016 96.8583 29.7656 96.4654 29.5198C96.3925 29.4737 96.3196 29.4286 96.2468 29.3835C95.8308 29.1257 95.4111 28.8725 94.9868 28.6277C94.5524 28.3772 94.1143 28.1333 93.6716 27.8957C93.6273 27.8718 93.5821 27.8488 93.5369 27.8248C93.156 27.6223 92.7723 27.4244 92.3859 27.2319C92.3029 27.1905 92.2189 27.1491 92.1359 27.1076C91.7347 26.9106 91.3307 26.7182 90.924 26.5313C90.8926 26.5175 90.8622 26.5028 90.8317 26.488C90.3779 26.2809 89.9196 26.0811 89.4584 25.8887C89.415 25.8703 89.3708 25.8537 89.3274 25.8353C88.928 25.6696 88.5259 25.5094 88.121 25.3547C88.0214 25.316 87.9218 25.2783 87.8212 25.2405C87.4329 25.0942 87.0419 24.9533 86.648 24.8161C86.5807 24.7931 86.5143 24.7682 86.447 24.7452C85.9803 24.586 85.5099 24.4322 85.0367 24.2867C84.9888 24.272 84.9399 24.2582 84.8919 24.2435C84.4806 24.1183 84.0673 23.9995 83.6523 23.8844C83.5333 23.8513 83.4143 23.82 83.2944 23.7877C82.92 23.6874 82.5437 23.5916 82.1646 23.5005C82.0631 23.4756 81.9626 23.4508 81.8611 23.4268C81.3852 23.3154 80.9065 23.2096 80.4241 23.112C80.3752 23.1019 80.3264 23.0936 80.2784 23.0844C79.8541 22.9997 79.4271 22.9214 78.9991 22.8478C78.8626 22.8247 78.7252 22.8017 78.5878 22.7796C78.2244 22.7207 77.8591 22.6655 77.493 22.6139C77.3638 22.5955 77.2347 22.5771 77.1056 22.5596C76.6214 22.4961 76.1344 22.4381 75.6455 22.3883C75.6059 22.3847 75.5662 22.3819 75.5275 22.3782C75.0801 22.334 74.631 22.2972 74.1809 22.2659C74.0324 22.2558 73.8839 22.2466 73.7344 22.2374C73.3738 22.2153 73.0113 22.1968 72.6489 22.183C72.5022 22.1775 72.3546 22.1711 72.2071 22.1665C71.7118 22.1517 71.2156 22.1416 70.7166 22.1416C70.2176 22.1416 69.7214 22.1517 69.2261 22.1665C69.0785 22.1711 68.9319 22.1775 68.7843 22.183C68.4218 22.1968 68.0593 22.2153 67.6987 22.2374C67.5502 22.2466 67.4008 22.2548 67.2523 22.2659C66.8022 22.2972 66.353 22.334 65.9057 22.3782C65.866 22.3819 65.8264 22.3847 65.7876 22.3883C65.2988 22.4381 64.8127 22.4961 64.3276 22.5596C64.1984 22.5762 64.0693 22.5955 63.9402 22.6139C63.574 22.6655 63.2088 22.7198 62.8454 22.7796C62.708 22.8017 62.5705 22.8238 62.434 22.8478C62.0061 22.9214 61.5809 22.9997 61.1575 23.0844C61.1077 23.0945 61.0579 23.1028 61.0081 23.1129C60.5266 23.2105 60.048 23.3164 59.572 23.4278C59.4706 23.4517 59.37 23.4775 59.2695 23.5014C58.8913 23.5926 58.5141 23.6883 58.1396 23.7887C58.0207 23.8209 57.9017 23.8522 57.7827 23.8853C57.3667 23.9995 56.9535 24.1192 56.5422 24.2444C56.4942 24.2591 56.4462 24.272 56.3983 24.2867C55.9251 24.4322 55.4547 24.586 54.988 24.7452C54.9207 24.7682 54.8552 24.7922 54.7879 24.8152C54.3941 24.9515 54.003 25.0932 53.6138 25.2396C53.5142 25.2774 53.4145 25.3151 53.3149 25.3529C52.91 25.5085 52.5079 25.6677 52.1094 25.8335C52.0652 25.8519 52.0209 25.8694 51.9775 25.8869C51.5164 26.0802 51.0589 26.28 50.6051 26.4862C50.5738 26.5 50.5424 26.5157 50.511 26.5295C50.1043 26.7154 49.7003 26.9079 49.3 27.1058C49.217 27.1472 49.1331 27.1877 49.0501 27.2292C48.6627 27.4225 48.279 27.6205 47.8981 27.823C47.8538 27.8469 47.8086 27.869 47.7643 27.893C47.3216 28.1305 46.8835 28.3745 46.4491 28.6249C46.0239 28.8698 45.6051 29.123 45.1883 29.3808C45.1154 29.4259 45.0425 29.471 44.9706 29.5161C44.5777 29.7619 44.1875 30.0132 43.8011 30.2701C43.7762 30.2867 43.7513 30.3023 43.7273 30.3189C43.3021 30.6034 42.8824 30.8943 42.4674 31.1917C42.4342 31.2156 42.4019 31.2396 42.3687 31.2635C41.9997 31.5287 41.6364 31.7993 41.2757 32.0746C41.2084 32.1262 41.1411 32.1768 41.0746 32.2284C40.2851 32.8369 39.515 33.4685 38.7651 34.124C38.7162 34.1663 38.6683 34.2096 38.6194 34.2529C38.291 34.5429 37.9664 34.8366 37.6454 35.1349C37.5882 35.1883 37.531 35.2408 37.4739 35.2942C36.7498 35.9745 36.0461 36.6761 35.3654 37.3988C35.3119 37.4559 35.2584 37.5139 35.2049 37.5709C34.907 37.8904 34.6128 38.2145 34.3232 38.5413C34.2798 38.5901 34.2365 38.6389 34.1931 38.6877C33.5373 39.4353 32.9046 40.204 32.295 40.9921C32.2433 41.0593 32.1917 41.1265 32.14 41.1937C31.8652 41.5537 31.594 41.9165 31.3284 42.2838C31.3044 42.3169 31.2795 42.3501 31.2555 42.3842C30.9576 42.7985 30.667 43.2173 30.382 43.6409C30.3654 43.6657 30.3488 43.6906 30.3322 43.7154C30.0749 44.1003 29.824 44.4888 29.5778 44.881C29.5317 44.9537 29.4865 45.0264 29.4413 45.0992C29.183 45.5144 28.9294 45.9333 28.684 46.3568C28.4332 46.7904 28.1887 47.2277 27.9508 47.6697C27.9268 47.7139 27.9037 47.759 27.8798 47.8041C27.6768 48.1843 27.4785 48.5673 27.2858 48.9531C27.2443 49.0359 27.2028 49.1197 27.1613 49.2035C26.9639 49.603 26.7711 50.0054 26.5848 50.4114C26.57 50.4427 26.5553 50.474 26.5405 50.5062C26.3339 50.9592 26.1338 51.4158 25.9401 51.8762C25.9216 51.9203 25.9041 51.9645 25.8857 52.0087C25.7196 52.4065 25.5601 52.8079 25.4042 53.2111C25.3655 53.3105 25.3277 53.4109 25.2898 53.5103C25.1432 53.8979 25.0021 54.2883 24.8646 54.6814C24.8416 54.7486 24.8167 54.8149 24.7936 54.8821C24.6341 55.348 24.48 55.8175 24.3343 56.2898C24.3195 56.3377 24.3057 56.3865 24.291 56.4343C24.1655 56.844 24.0465 57.2574 23.9312 57.6717C23.898 57.7905 23.8667 57.9092 23.8344 58.0289C23.7339 58.4027 23.6379 58.7793 23.5466 59.1567C23.5217 59.258 23.4968 59.3584 23.4728 59.4596C23.3612 59.9347 23.2552 60.4125 23.1574 60.8931C23.1473 60.9428 23.139 60.9925 23.1288 61.0422C23.044 61.4648 22.9656 61.8902 22.8918 62.3164C22.8678 62.4527 22.8457 62.5899 22.8235 62.7271C22.7645 63.0898 22.7092 63.4544 22.6575 63.8199C22.6391 63.9488 22.6206 64.0777 22.6031 64.2066C22.5394 64.6899 22.4813 65.176 22.4315 65.664C22.4278 65.7035 22.4251 65.7431 22.4214 65.7818C22.3771 66.2283 22.3402 66.6767 22.3089 67.126C22.2987 67.2742 22.2895 67.4224 22.2803 67.5716C22.2581 67.9315 22.2397 68.2934 22.2259 68.6552C22.2203 68.8016 22.2139 68.9489 22.2093 69.0962C22.1945 69.5906 22.1843 70.0859 22.1843 70.584H29.1175C29.1175 63.0189 31.1448 55.928 34.6856 49.8194C38.3381 43.5184 43.6018 38.2642 49.9143 34.6184C56.034 31.084 63.1378 29.0604 70.7166 29.0604C78.2954 29.0604 85.3992 31.084 91.5189 34.6184C97.8313 38.2642 103.095 43.5184 106.748 49.8194C110.288 55.928 112.316 63.0189 112.316 70.584H119.249C119.249 70.0896 119.239 69.5933 119.224 69.0989Z', fill: 'black' }
export const face = { d: 'M106.747 49.8245C103.095 43.5235 97.831 38.2693 91.5185 34.6235C85.3989 31.089 78.2951 29.0654 70.7162 29.0654C63.1374 29.0654 56.0336 31.089 49.9139 34.6235C43.6015 38.2693 38.3377 43.5235 34.6853 49.8245C31.1445 55.9331 29.1172 63.024 29.1172 70.589H70.7153H112.315C112.315 63.024 110.288 55.9331 106.747 49.8245Z', fill: '#212121' }
export const needle = { d: 'M111.117 36.1662L74.1669 59.8714C73.0943 59.4644 71.9321 59.2389 70.7165 59.2389C65.3559 59.2389 61.0099 63.577 61.0099 68.9279C61.0099 74.2788 65.3559 78.6169 70.7165 78.6169C76.0771 78.6169 80.4231 74.2788 80.4231 68.9279C80.4231 68.2494 80.3521 67.5865 80.2193 66.9466L111.134 36.1865C111.146 36.1754 111.131 36.1579 111.117 36.1662Z', fill: 'white' }
```

## Source — shared app parts it uses

### `src/shared/copy.ts`

```ts
/**
 * UI copy. Every user-facing string of a flow lives in ONE file, `src/flows/<flow-id>/copy.json` — flat keys
 * ("empty.title") → the text. Screens read it through the flow's `t`:
 *
 *   t('empty.title')                       → "No search results found"
 *   t('group.results', { list, count })    → "Stocks (8)"   ({name} placeholders are filled in)
 *
 * Sample data (stock names, prices, watchlists) stays in the flow's data.ts — copy.json is only the words the app
 * itself says: titles, labels, buttons, empty states, accessible names. Porting a flow: this file is the string
 * table (Flutter ARB / iOS Localizable.strings).
 */
export type CopyVars = Record<string, string | number>

export function makeCopy<Copy extends Record<string, string>>(flow: string, copy: Copy) {
  return function t(key: keyof Copy & string, vars?: CopyVars): string {
    const template = copy[key] ?? key
    return vars ? template.replace(/\{(\w+)\}/g, (m, name: string) => (name in vars ? String(vars[name]) : m)) : template
  }
}
```

### `src/shared/data/format.ts`

```ts
/** ₹ with Indian grouping: inr(123456.5) → "₹1,23,456.50"; inr(1000, 0) → "₹1,000". */
export const inr = (n: number, decimals = 2) =>
  '₹' + n.toLocaleString('en-IN', { minimumFractionDigits: decimals, maximumFractionDigits: decimals })

/** $ with US grouping: usd(1234.5) → "$1,234.50"; usd(1000, 0) → "$1,000". */
export const usd = (n: number, decimals = 2) =>
  '$' + n.toLocaleString('en-US', { minimumFractionDigits: decimals, maximumFractionDigits: decimals })

/** "9876543210" → "98765 43210" (how Indian mobile numbers are read out). */
export const phone = (digits: string) => (digits.length > 5 ? `${digits.slice(0, 5)} ${digits.slice(5)}` : digits)

/** Keep the last `visible` characters: mask('ABCPM1234K', 1, 5) → "ABCPM****K". */
export const mask = (s: string, keepStart: number, keepEnd: number) =>
  s.slice(0, keepStart) + '•'.repeat(Math.max(0, s.length - keepStart - keepEnd)) + s.slice(s.length - keepEnd)
```

### `src/shared/prototype.ts`

```ts
// Prototype behaviour the flows use — the ONLY way a flow touches the preview (src/preview). In a real app: interactive
// is always true, `go` is the app's navigation, and useAutoAdvance is "when the server answers, go on" (a loader /
// polling step).
import { createContext, useContext, useEffect, useSyncExternalStore } from 'react'

export type Preview = {
  /**
   * Prototype (true): real modal L3 BottomSheets, taps move to the next screen, loaders advance on their own.
   * Board (false): every screen frozen as in the Figma board — sheets are drawn as static surfaces.
   */
  interactive: boolean
  /** Go to another screen of the flow (by id). Does nothing on the board. */
  go: (id: string) => void
  /** The screen being shown — a new id gives the sheet a fresh mount while the page behind it stays put. */
  screenId?: string
  /** Back to the screen shown before this one in the prototype (any flow); false when there's none to go back to. */
  back?: () => boolean
  /** The screen was reached by going back (a back button, or a screen earlier in the app) — a page can come back as it was left. */
  cameBack?: boolean
  /** An `over` screen (a sheet over the screen the user is on): the screen under it — closing the sheet goes there. */
  under?: string
}

export const PreviewContext = createContext<Preview>({ interactive: false, go: () => {} })
export const usePreview = () => useContext(PreviewContext)

// ---- Which way the next move goes ------------------------------------------------------------------------------------
// The preview guesses a move's direction (a screen visited before, or one earlier in the same flow, is "back"). A tap can
// say it instead: Deposit opens Add money (listed earlier in the flow) as a page going forward; a back button's fallback
// (nothing in the history) is back, and replaces the page instead of adding to the history.
let intent: { id: string; direction: 'forward' | 'back' } | null = null

/** Say the move to screen `id` that is about to happen is forward (a page opening) or back. */
export const markMove = (id: string, direction: 'forward' | 'back') => {
  intent = { id, direction }
}

/** The preview: the direction said for a move to `id`, if any. */
export const moveIntent = (id: string) => (intent?.id === id ? intent.direction : undefined)

/** The preview: the move happened. */
export const clearMoveIntent = () => {
  intent = null
}

/** Prototype only: after `ms`, go to `next` (loaders, "Verifying…"). */
export function useAutoAdvance(next: string | undefined, ms: number) {
  const { interactive, go } = usePreview()
  useEffect(() => {
    if (!interactive || !next) return
    const t = window.setTimeout(() => go(next), ms)
    return () => window.clearTimeout(t)
  }, [interactive, next, ms, go])
}

/** How long a loader or "Verifying…" state stays up in the prototype. */
export const LOADING_MS = 1600

// ---- Flow options (prototype settings such as a design version) ----------------------------------------------------
// Picked in the preview (desktop panel, or the settings sheet on a phone), remembered per browser. A real app has no
// such switch: it ships one version.

// The key carries the option's default: when a flow changes its default (e.g. to a new version), earlier picks reset.
const optionKey = (flow: string, option: string, fallback: string) => `prototype-option:${flow}.${option}@${fallback}`
const optionListeners = new Set<() => void>()

function readOption(key: string): string | null {
  try { return localStorage.getItem(key) } catch { return null }
}

/** The preview sets an option (and every screen reading it re-renders). */
export function setFlowOption(flow: string, option: string, fallback: string, value: string) {
  const key = optionKey(flow, option, fallback)
  try { localStorage.setItem(key, value) } catch { /* storage off: this visit only */ }
  memory.set(key, value)
  optionListeners.forEach((l) => l())
}

const memory = new Map<string, string>()

/**
 * Showcase links (20 Nov): `?showcase` shows one screen as it is shared (e.g. the risk-meter page for leadership) — no
 * prototype controls over it. `?o=nudges.meter:soft,nudges.meterFill:split` sets options for this page only (never
 * stored, so several showcase frames side by side can each show their own version).
 */
// A showcase frame can't always carry a query (a packed, single-file page loads the app from a blob: URL), so its
// settings can also come in the frame's name: "showcase:?showcase&theme=dark&o=…".
export const linkParams = (() => {
  try {
    const named = window.name.startsWith('showcase:') ? window.name.slice('showcase:'.length) : ''
    return new URLSearchParams(named || location.search)
  } catch { return new URLSearchParams() }
})()
export const SHOWCASE = linkParams.has('showcase')
// A showcase frame sits in a page of phones: the app focusing its sheet must never scroll that page to it.
if (SHOWCASE) {
  const focus = HTMLElement.prototype.focus
  HTMLElement.prototype.focus = function (options?: FocusOptions) { focus.call(this, { ...options, preventScroll: true }) }
}
const linkOptions = new Map((linkParams.get('o') ?? '').split(',').filter(Boolean).map((pair) => {
  const [key, value = ''] = pair.split(':')
  return [key, value] as const
}))
const picked = (flow: string, option: string, fallback: string) => {
  const key = optionKey(flow, option, fallback)
  return linkOptions.get(`${flow}.${option}`) ?? memory.get(key) ?? readOption(key)
}

/** A flow's prototype option: the picked value, or `fallback` (the option's default) when none is picked. */
export function useFlowOption(flow: string, option: string, fallback: string) {
  return useSyncExternalStore(
    (onChange) => { optionListeners.add(onChange); return () => { optionListeners.delete(onChange) } },
    () => picked(flow, option, fallback) ?? fallback,
  )
}

type OptionLike = { id: string; default: string; showIf?: Record<string, string[]> }

/** Every option of a flow as it's set now (the settings panel's show / hide and nesting). */
export function useFlowOptionValues(flow: { id: string; options?: OptionLike[] }): Record<string, string> {
  const snap = useSyncExternalStore(
    (onChange) => { optionListeners.add(onChange); return () => { optionListeners.delete(onChange) } },
    () => JSON.stringify(Object.fromEntries((flow.options ?? []).map((o) => {
      return [o.id, picked(flow.id, o.id, o.default) ?? o.default]
    }))),
  )
  return JSON.parse(snap)
}

/** Whether an option matters right now (every option it depends on has one of the listed values, all the way up). */
export function optionShown(options: OptionLike[], option: OptionLike, values: Record<string, string>): boolean {
  return Object.entries(option.showIf ?? {}).every(([id, allowed]) => {
    const parent = options.find((o) => o.id === id)
    return allowed.includes(values[id]) && (!parent || optionShown(options, parent, values))
  })
}

/** How deep an option sits under the ones it depends on (0 = top level) — the panel indents it that much. */
export function optionDepth(options: OptionLike[], option: OptionLike): number {
  const parents = Object.keys(option.showIf ?? {}).map((id) => options.find((o) => o.id === id)).filter(Boolean) as OptionLike[]
  return parents.length ? 1 + Math.max(...parents.map((p) => optionDepth(options, p))) : 0
}

/** How many of a flow's options are off their default (the settings panel's badge). */
export function useFlowOptionsChanged(flow: { id: string; options?: { id: string; default: string }[] }) {
  return useSyncExternalStore(
    (onChange) => { optionListeners.add(onChange); return () => { optionListeners.delete(onChange) } },
    () => (flow.options ?? []).filter((o) => {
      return (picked(flow.id, o.id, o.default) ?? o.default) !== o.default
    }).length,
  )
}

/**
 * Typing on a phone uses the phone's own keyboard (a touch screen, `pointer: coarse`) — the prototype's drawn keyboard
 * stays hidden. On a laptop the drawn keyboard shows (for the look) and the laptop's keys type into the focused field.
 */
export function useSystemKeyboard() {
  return typeof window !== 'undefined' && window.matchMedia('(pointer: coarse)').matches
}
```

### `src/shared/ui/Screen.module.css`

```css
/*
 * One phone screen: the OS status bar, then the page — top bar, a body that scrolls and fills the space, the bottom
 * bar / button dock — with an optional toast just above the bottom and a sheet over everything.
 */
.screen {
  position: relative;
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
  overflow: clip; /* clip, not hidden: a sheet taking focus while it slides in can't scroll the screen */
  background: var(--l3-surface-default);
  color: var(--l3-content-primary);
  /* A size container: a sheet can be a share of the phone screen's height (cqh), in the mockup and on a phone alike. */
  container: app-screen / size;
  /* An app, not a page: swiping and long-pressing never select text (fields still do — see below). */
  user-select: none;
  -webkit-user-select: none;
  -webkit-touch-callout: none;
}

.screen :is(input, textarea, [contenteditable='true']) {
  user-select: text;
  -webkit-user-select: text;
}

.page {
  display: flex;
  flex-direction: column;
  flex: 1;
  min-height: 0;
}

.middle {
  position: relative;
  display: flex;
  flex: 1;
  min-height: 0;
}

/* Like a phone: no scrollbar that stays on screen — the page, rails and open sheets still scroll (touch, wheel, keys). */
.screen,
.screen * {
  scrollbar-width: none;
}

.screen ::-webkit-scrollbar {
  display: none;
}

.body {
  display: flex;
  flex-direction: column;
  flex: 1;
  min-height: 0;
  overflow-x: hidden; /* a screen never scrolls sideways — only rails inside it do */
  overflow-y: auto;
  padding-bottom: var(--app-body-end);
}

/* Bottom navbar V2 (floating, shared/ui/FloatingNav): the body runs on behind the pill; its end clears the pill
   (14 up + 56 tall) plus the usual 24. */
.page:has(> [data-floating-nav]) .body {
  padding-bottom: calc(var(--app-body-end) + var(--l3-spacing-14) + var(--l3-size-56));
}

/* The body owns the page's end spacing: whatever comes last adds none of its own (no 24 + 24). */
.body > :last-child {
  padding-bottom: 0;
  margin-bottom: 0;
}
/* A page's last block nested deeper (inside tabs or a panel) is marked data-page-end so it adds none either. */
.body [data-page-end] { padding-bottom: 0; margin-bottom: 0; }

/* Floating toast: sits on the bottom edge of the body, above the dock / navbar (L3 Aerobar rule). */
.toast {
  position: absolute;
  inset: auto 0 0;
}

/* The prototype's modal L3 sheet is portalled into this screen — lift it above the bottom bars. */
.screen.screen > [data-contained] {
  z-index: var(--app-layer-sheet);
}
```

### `src/shared/ui/Screen.tsx`

```tsx
import { Fragment, useState, type ReactNode } from 'react'
import { usePreview } from '../prototype'
import { SheetHost } from './Sheet'
import styles from './Screen.module.css'

type ScreenProps = {
  /** Actionbar (or nothing on full-bleed screens like the welcome screen). */
  top?: ReactNode
  /** Bottom navbar, button dock (ButtonGroup) or the keypad. */
  bottom?: ReactNode
  /** A floating Aerobar toast — shown just above `bottom`. */
  toast?: ReactNode
  /** A Sheet over the screen. */
  sheet?: ReactNode
  /** Screen content: scrolls when taller than the space between `top` and `bottom`. */
  children?: ReactNode
  /** A flow's own styling hook on the screen root (e.g. an experiment scoped to one flow). */
  className?: string
}

/**
 * The frame of every screen: top · body · bottom, a toast above the bottom, and a sheet over it all. It fills the
 * space between the OS status bar and the OS navigation bar (the preview draws those — real apps get them from the
 * OS, edge-to-edge insets), so nothing sits under the gesture handle. The screen is the sheet's container, so sheets
 * and their scrim stay in the app; its SheetHost keeps one sheet open while the screen's sheet changes (no scrim flash
 * between two sheets). Mark a bottom part with data-surface="primary" | "secondary" if the navigation bar should take
 * its colour (the button dock and the bottom navbar are recognised already).
 */
export function Screen({ top, bottom, toast, sheet, children, className }: ScreenProps) {
  const [el, setEl] = useState<HTMLDivElement | null>(null)
  const { screenId } = usePreview()
  return (
    <div ref={setEl} className={[styles.screen, className].filter(Boolean).join(' ')}>
      <SheetHost container={el}>
        <div className={styles.page} data-part="page">
          {top}
          <div className={styles.middle}>
            <div className={styles.body}>{children}</div>
            {toast && <div className={styles.toast}>{toast}</div>}
          </div>
          {bottom}
        </div>
        <Fragment key={screenId}>{sheet}</Fragment>
      </SheetHost>
    </div>
  )
}
```

### `src/shared/ui/Sheet.module.css`

```css
/* Board only: the static sheet sits on the bottom edge of the screen, over the L3 Overlay — shown at rest, no fade-in. */
.scrim {
  z-index: var(--app-layer-scrim);
  transition: none;
}

.dock {
  position: absolute;
  inset: auto 0 0;
  z-index: var(--app-layer-sheet);
  display: flex;
  flex-direction: column;
  max-height: calc(100% - var(--l3-size-48));
}

/* A top sheet (placement="top") hangs from the top edge instead. */
.dock[data-placement='top'] {
  inset: 0 0 auto;
}
```

### `src/shared/ui/Sheet.tsx`

```tsx
import { createContext, useCallback, useContext, useId, useLayoutEffect, useState, type ReactNode } from 'react'
import { BottomSheet, BottomSheetSurface } from '@l3/components/BottomSheet'
import { Overlay } from '@l3/components/Overlay'
import { usePreview } from '../prototype'
import styles from './Sheet.module.css'

/** Lets the L3 sheet play its exit before the next screen replaces it (≈ motion/duration-medium). */
const SHEET_EXIT_MS = 240

type SheetProps = {
  header?: ReactNode
  children?: ReactNode
  /** The button dock — a <ButtonGroup>. */
  footer?: ReactNode
  /** Id of the header's heading (BottomSheetHeader `headingId`). */
  labelledBy?: string
  /** Accessible name when there's no header (loaders). */
  label?: string
  /** Prototype: where a backdrop tap, drag down or Esc goes. Leave out for sheets that can't be dismissed (loaders). */
  onClose?: () => void
  /** A screen's own styling hook on the sheet surface (e.g. a sheet that brings its own layout and no padding). */
  className?: string
  /** 'top' (L3 isBottom=False): drops from the top of the screen, for menus tied to the top (a market or sort picker). */
  placement?: 'bottom' | 'top'
}

type Publish = (id: string, sheet: SheetProps | null) => void
const SheetHostContext = createContext<Publish | null>(null)

/**
 * An L3 bottom sheet over the screen.
 * Prototype: the real modal <BottomSheet> (focus trap, drag to close, scrim tap), drawn by the screen's SheetHost —
 * so when one sheet leads to another over the same page, the scrim stays and only the sheet's content changes.
 * Board: the same surface drawn statically with the L3 Overlay — dozens of open modals on one page would fight
 * over focus, so the board shows <BottomSheetSurface>, which is what the modal renders inside.
 */
export function Sheet(props: SheetProps) {
  const { interactive } = usePreview()
  const publish = useContext(SheetHostContext)
  const id = useId()
  const hosted = interactive && publish !== null

  // Hand the latest content to the host on every render; take it back when this sheet goes away.
  useLayoutEffect(() => { if (hosted) publish(id, props) })
  useLayoutEffect(() => (hosted ? () => publish(id, null) : undefined), [hosted, publish, id])

  if (hosted) return null
  const { header, children, footer, labelledBy, label, className, placement = 'bottom' } = props
  return (
    <>
      <Overlay open className={styles.scrim} />
      <div className={styles.dock} data-placement={placement} role="dialog" aria-labelledby={labelledBy} aria-label={label}>
        <BottomSheetSurface header={header} footer={footer} className={className} placement={placement}>{children}</BottomSheetSurface>
      </div>
    </>
  )
}

/**
 * Prototype: one modal L3 BottomSheet per screen, kept open while the screen's sheet changes (sheet → sheet swaps
 * the content in place, no scrim flash or slide). It closes with its exit animation when the screen has no sheet.
 */
export function SheetHost({ container, children }: { container: HTMLElement | null; children: ReactNode }) {
  const [shown, setShown] = useState<{ id: string; sheet: SheetProps; open: boolean } | null>(null)
  const publish = useCallback<Publish>((id, sheet) => {
    setShown((s) => (sheet ? { id, sheet, open: true } : s && s.id === id ? { ...s, open: false } : s))
  }, [])

  const close = () => {
    const onClose = shown?.sheet.onClose
    if (!onClose) return
    setShown((s) => s && { ...s, open: false })
    window.setTimeout(onClose, SHEET_EXIT_MS)
  }

  return (
    <SheetHostContext.Provider value={publish}>
      {children}
      {container && shown && (
        <BottomSheet
          open={shown.open}
          onClose={close}
          container={container}
          header={shown.sheet.header}
          footer={shown.sheet.footer}
          aria-labelledby={shown.sheet.labelledBy}
          aria-label={shown.sheet.label}
          className={shown.sheet.className}
          placement={shown.sheet.placement}
        >
          {shown.sheet.children}
        </BottomSheet>
      )}
    </SheetHostContext.Provider>
  )
}
```
