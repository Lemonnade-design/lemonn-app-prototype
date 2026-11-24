# Flow: F&O (`fno`)

> One self-contained file for converting this flow to another platform. Read https://lemonnade-design.github.io/lemonn-app-prototype/CONVERT.md first. Design system: Lemonnade V3 @ `ed10506` (components, tokens and rules: https://lemonnade-design.github.io/lemonnade-v3-docs/llms.txt).

Equity F&O home: P&L, indices, chart metrics, watchlists, Smart Options, Futures Heatmap and Smart Futures.

Prototype: https://lemonnade-design.github.io/lemonn-app-prototype/#/fno · machine-readable: https://lemonnade-design.github.io/lemonn-app-prototype/flows/fno.json

## Screens

| Id | Screen | Figma | Taps go to | Note |
|---|---|---|---|---|
| `fno-34` | Splash | — | `fno-01` | The launch splash: the Lemonn logo centred for 2 s, then it fades into Equity home (a tap skips ahead). Hidden at launch for now (src/shared/ui/Splash: SPLASH_SCREENS is empty), so the app opens straight on the home; this page still plays it. |
| `fno-01` | Equity home | [11569:41100](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=11569-41100) | — | From the main F&O tab. Home returns to Stocks; DASH, Search, Profile and Wallet open their existing flows. Selectors, chart metrics, filters, sorting and watchlist creation work locally. Destinations outside this frame open an explanatory sheet. |
| `fno-02` | Home · watchlists & Smart Options | [11569:41100](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=11569-41100) | — | The same long screen, scrolled to watchlists. |
| `fno-03` | Home · Futures Heatmap | [11569:41100](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=11569-41100) | — |  |
| `fno-04` | Home · Smart Futures | [11569:41100](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=11569-41100) | — |  |
| `fno-05` | Scalper | — | `dash-20` | From ScalpPro on F&O home, the Expiring cards, the Expiry calendar or the Scalper bottom-nav tab — always a new page in from the right; back returns to the page it was opened from. The chart-tools sheet groups personal DASH AI indicators separately from Lemon indicators. |
| `fno-06` | Scalper · DASH indicator | — | `dash-20` | From DASH AI’s View indicator. Opens the chart-tools sheet directly on Indicators, the saved DASH AI indicator under Your indicators with a focus guide. Tap rows to add / remove indicators (several at once); search filters the list. |
| `fno-07` | Scalper · indicator applied | — | `dash-20` | With the saved DASH AI indicator on the chart: “1 ▾” at the chart’s top-left and illustrative EMA 9 / 21 lines on the NIFTY 50 candles. |
| `fno-35` | Break Even · position + breakeven line | [11756:78739](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=11756-78739) | `dash-20` | Version C (Boxed chip): an open position on the option chart — TP pill (drag ⠿ to move, ✕ removes), entry row (Exit · +65 · live P&L), SL pill (+ Add Trail), and the solid warning-light breakeven line with a boxed “Breakeven ⓘ” tag on it, 8 left of the price axis (Figma’s “B/E 105.55”: spelled out, no price — designer’s call; the label still reads the price) (tap → How breakeven works). Breakeven = entry + round-trip charges per unit (data.ts breakevenPrice). Buy at Mkt on fno-05 opens a position the same way; the first buy also opens How breakeven works. Exit buttons are 24 tall to sit on the pills (Figma), not Large. |
| `fno-36` | Break Even · How breakeven works (sheet) | [11783:5569](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=11783-5569) | `dash-20` | Two versions (setting “Breakeven sheet”, floating card beside the phone): Version 2 (default) — heading “What is breakeven line?” (no description; “price” → “line”, 19 Nov), the charges table, no info lines; Version 1 — “How breakeven works” with the two info lines, no table. Opens on the first buy and from the B/E chip’s ⓘ (and Settings → Breakeven line ⓘ). The example card loops (a tap replays it): every play opens with the “Introducing Breakeven Line” intro (2.5 s), then a 9.3 s chart copied from the designer’s recording: on a white chart the buy at ₹100; the chart zooms in 2× and the orange charges zone fills one band per charge from the F&O options rate card, in ₹ on the ₹100 buy (top down: STT ₹0.15, transaction ₹0.07, stamp duty, SEBI, then brokerage ₹0.02 last at the bottom with a smaller tag; they come in top down — no GST band: it’s charged on the charges; heights by cost), then zooms back out to one thin zone, the tags sliding down under it and stacking into one “Order charges ≈₹0.26” tag (GST included); the dashed B/E line at ₹100.30 draws along its top with the chart’s “Breakeven” tag (text only, no price), an LTP bubble rides the price line up through B/E (a ringed marker pulses) to “Sold at ₹102”, the green Net Profit zone fills; it holds, then plays again from the intro. “I understand” is locked until the chart has played once (intro + chart, 11.8 s), a loader line filling along its top edge, then turns primary (Figma’s button variants). Reduced motion: the finished chart, button ready. Under the example, the same trade as a calculation table (a card on the secondary surface, no heading, compact L3 key-value rows, one line each, no lines inside): Bought at ₹100.00 · Order charges (incl. GST) ≈₹0.26 — tap the row to open the breakdown (closed by default: STT, transaction, brokerage, stamp duty, SEBI, GST 18%) — and Breakeven price ₹100.30 in bold (L3 total row). Labels are L3’s 12 styles (the recording’s are ~11). The zoomed-in charges aren’t in Figma or the recording (designer’s brief). A V2 (starts zoomed in on a blue ₹0 → ₹100 fill, zooms out true to scale, sold 12% up at ₹112) is archived in fno/archive/BreakevenExplainerV2.tsx. |
| `fno-37` | Break Even · chart settings (breakeven line) | [11754:69563](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=11754-69563) | `dash-20` | The chart-tools sheet on Settings: Auto TP/SL (animated mark, Applied), Chart type (Candles / Heikin Ashi / Line), Stop Loss Preference (radio), View on chart (Breakeven line ⓘ New, Buy/Sell executions, Sync Charts). Changes are a draft: Apply keeps them (unticking Breakeven line hides the B/E line and chip), Cancel or closing drops them. Figma’s rail (Bolt, Indicators, Drawings, Settings) is the live app’s six groups here. |
| `fno-39` | Zing signals · All signals | [6900:23855](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6900-23855) | `dash-20` | From the Active chip at the tool row’s right end (Zing). Figma: file 9r61YQp7QQZAQovDyz8hLF (Enrich signal filter), old Lemonn design system, rebuilt in L3. Top row: filter button | All Signals (4) · Win rate ≥ 50% · Commodity · Nifty · Sensex (L3 pill tabs, Small; counts are worked out from the signals). Active signals (n) with Total P&L, then a card per signal: avatar, strategy, market + win rate tags (or a P&L tag), View; under a line Buy Call 23950 • RR • the rule. A chip with no signals shows the L3 empty state. Filter → fno-40. |
| `fno-40` | Zing signals · Filter · Indices | [6900:26203](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6900-26203) | `dash-20` | The filter takes the signals sheet over in place, in the Scalper’s Settings sheet look: L3 Side nav Indices · Win rate · Call/Put · Strategies, the white panel with its Heading/16 title row and Clear All, card rows with a checkbox (Indices, Strategies) or radio (Win rate, Call/Put; the chosen one tinted blue), the picks as pills over Cancel / Apply (primary). Cancel or a scrim tap brings the signals back; Apply saves them as Your filter (→ fno-45). |
| `fno-41` | Zing signals · Filter · Indices picked | [6900:29666](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6900-29666) | `dash-20` | NIFTY 50 and SENSEX ticked (All Indices unticks itself; untick both and it’s back). The side tab shows how many it picked (Figma: a red 1 — L3 Side nav’s corner flag, in blue). The picks sit as chips over Cancel / Apply; ✕ takes one off. |
| `fno-42` | Zing signals · Filter · Win rate | [6900:27042](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6900-27042) | `dash-20` | Win rate: All · ≥ 50% · ≥ 30% (pick one). |
| `fno-43` | Zing signals · Filter · Call/Put | [6900:27889](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6900-27889) | `dash-20` | Call/Put: All · Call · Put (pick one). |
| `fno-44` | Zing signals · Filter · Strategies | [6900:28736](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6900-28736) | `dash-20` | Strategies: one row per Zing strategy with its picture (L3 Avatar 24), pick several. A long name is cut at 140 in its chip (Figma dev note). |
| `fno-45` | Zing signals · Your filter saved (tip) | [6900:30528](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6900-30528) | `dash-20` | Right after Apply: Your filter (n) comes in first, selected, with ✕ to remove it; the filter button gets a red dot; a blue tooltip “Filter applied & saved for quick access” with ✕ points at it once (Figma’s colour on the L3 tooltip). Figma keeps All Signals selected; here the saved filter is, so the list shows what it picked. |
| `fno-46` | Zing signals · Your filter saved | [6900:24637](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6900-24637) | `dash-20` | The same without the tip: next time the sheet opens, Your filter is one tap away. |
| `fno-47` | Zing signals · All Signals (plain) | [6900:25420](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6900-25420) | `dash-20` | Figma’s plain look: an “All Signals” header and every signal. Figma’s ← back is left out: L3 gives the first sheet over a screen no back button. |
| `fno-08` | Commodities home | [6754:63637](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6754-63637) | — | The Commodities product tab. Gold / Silver / Crude Oil / Natural Gas shortcuts open the Lot summary (Gold Summary). The chart’s instrument selector (“Gold”) opens the contract picker. Popular commodities: Options ⇕ Futures switch; Futures Heatmap: Bullion / Energy / Metals. |
| `fno-09` | Commodities · heatmap & Smart Futures | [6754:63637](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6754-63637) | — | The same long screen, scrolled to the Futures Heatmap. |
| `fno-10` | Contract picker · Commodities | [6754:65111](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6754-65111) | — | From the chart’s “Gold ⇕”. Equity / Commodities tabs in the sheet header’s bottom slot, commodity chips (All, Gold, Silver …) under them; contracts grouped by commodity as radio rows (Gold Mini tagged “Lowest Margin”). Picking one updates the chart and closes the sheet. |
| `fno-11` | Contract picker · Equity | [6754:65054](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6754-65054) | — | The same sheet on its Equity tab: the 8 index contracts. |
| `fno-38` | Commodity calendar (View all) | — | `fno-08`, `fno-21`, `fno-17` | From View all on Expiring This Week (fno-08). All / Options / Futures / Events (flat tabs with icons, sticky; All merges them by day). Options rows: option chain (→ fno-17, back returns here) + ScalpPro; futures: ScalpPro only; events: no buttons. Days from today under a month section header (SectionHeader, content-primary): weekday over the date in one grey block (surface-secondary; today inverted (surface-inverted)), beside it one card with that day’s contracts — one day can hold several. A row is only the name with flat ScalpPro (→ fno-05) and open-contract (→ asset page fno-21) icon buttons. Back → Commodities home. Layout after the user’s reference (Expiry Calendar screenshot, 2026-11-17; no Figma frame yet). |
| `fno-12` | Gold Summary · by price | [6754:65113](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6754-65113) | `fno-08`, `fno-17` | From a commodity shortcut on fno-08. Gold lot tabs (Gold, Gold Mini, Gold Guinea, Gold Ten, Gold Petal) in the Actionbar’s bottom slot; Futures (View all) and Options (View option chain, expiry month, category pills, Filter, sort). The sort opens a sheet: By Price · By Volume · Margin per lot. |
| `fno-13` | Gold Summary · by volume | [6754:65288](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6754-65288) | `fno-08`, `fno-17` | Sorted by volume: each option shows its traded volume, no change. |
| `fno-14` | Gold Summary · margin per lot | [6754:65444](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6754-65444) | `fno-08`, `fno-17` | Sorted by margin per lot: each option shows the margin for one lot, no change. |
| `fno-15` | Strategies · Equity | [6754:64178](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6754-64178) | — | The Strategies product tab with Equity selected in the pill group: shortcuts, Zing Trades, Smart Invest, Pre-build Strategies (Nifty 50 ⇕, Bullish / Bearish / Neutral / Volatile), Quick Trade. Card footer buttons stay Small (32) as in Figma. |
| `fno-16` | Strategies · Commodities | [6754:64607](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6754-64607) | — | The same tab with Commodities selected: commodity Smart Invest baskets, GOLD as the underlying. |
| `fno-17` | Option chain | [11630:16785](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=11630-16785) | `fno-21` | From Option chain on the F&O chart (any product tab), the Expiry calendar’s option-chain button or the Option Chain bottom-nav tab; Back → the page it was opened from (F&O home when opened directly). Opens scrolled to the spot pill. BankNifty ▾ and Expiry ▾ open sheets; Σ shows delta instead of the day change; the basket and Zing tile open the explanatory sheet. Column heads: Call / Put metric (LTP, OI, OI Chg, IV) and the strike range (All, ±5, ±10). Tap a price to Buy, tap it again to Sell, a third time to clear. |
| `fno-18` | Option chain · Buy selected | [11630:16184](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=11630-16184) | `fno-21` | A put price tapped once: B badge, green wash, the order dock with the contract, Balance / Req, quantity in lots and Buy (brand). Buy places a sample order (toast) and clears the selection. |
| `fno-19` | Option chain · Sell selected | [11695:26269](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=11695-26269) | `fno-21` | The same put tapped again: S badge, red wash, Sell (secondary) in the dock; Req becomes the margin per lot. |
| `fno-20` | Option chain · illiquid contract | — | `fno-21` | Illiquid contracts (deep in-the-money calls, far out-of-the-money puts) carry a block icon beside the price, like Groww. Unlike Groww, a tap never selects them: a tooltip opens just above — “ILLIQUID contract” / “Can’t be traded” ⓘ; tapping away closes it, ⓘ opens a sheet with why it’s blocked, its traded lots and buy–sell gap, and a tip. Opens on the 25,700 put with the tooltip up. |
| `fno-21` | Asset page · Gold MINI | [6754:61613](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6754-61613) | `fno-17` | A commodity contract page. Entry (one of several): the contract name in the option chain order dock (“25,400 Put ›”). Back returns where it came from; Option chain → fno-17; Buy / Sell open the sample sheet. Equity contracts get their own (similar) page later. |
| `fno-22` | Asset page · illiquid | [6754:61613](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6754-61613) | `fno-17` | Product rule (commodities only): an illiquid contract’s page shows the ILLIQUID tag next to its name and Buy / Sell greyed out, with “Trading is not allowed as this contract is illiquid” above them — whatever screen it was opened from. |
| `fno-23` | Gold Summary · Buy / Sell sheet | — | `fno-08`, `fno-17` | Tapping any futures or option card opens the Buy / Sell sheet (live app, 2026-10-29): name › (asset page fno-21) · price, expiry · change, Buy (brand) / Sell (secondary). |
| `fno-24` | Gold Summary · illiquid sheet | — | `fno-08`, `fno-17` | Product rule (commodities): an illiquid contract carries the ILLIQUID tag on its card (edge case — illiquid contracts shouldn’t be listed, but the state is built) and in the sheet; Buy / Sell are greyed out with “Trading is not allowed as this contract is illiquid”. Only the name › (asset page fno-22) or tapping outside works. |
| `fno-25` | Order pad · Buy · Market | [8671:18433](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=8671-18433) | — | Commodity option chain order pad (other order pads differ a little). From Buy on the commodity asset page or the Gold Summary Buy / Sell sheet. Delivery / Intraday tabs, Market / Limit / SL pills, Quantity (⇕ lots) in steps of one lot, Set TPSL, Avail. · Req, Buy. Placing shows a sample toast; no order is sent. |
| `fno-26` | Order pad · Buy · Limit | [8671:18433](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=8671-18433) | — | Limit adds the validity (Day ⇕ → Day / IOC) and a limit price row with a % stepper from the market price. |
| `fno-27` | Order pad · Buy · SL | [8671:18433](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=8671-18433) | — | SL adds a trigger price row above the limit row. |
| `fno-28` | Order pad · Buy · Intraday | [8671:18433](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=8671-18433) | — | Intraday: “This position will auto close by 11:30 PM” above the dock. |
| `fno-29` | Order pad · Sell · Market | [8671:18433](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=8671-18433) | — | Sell adds Margin · Leverage (grey strip) above the quantity; the action is Sell (red). |
| `fno-30` | Order pad · Sell · SL | [8671:18433](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=8671-18433) | — |  |
| `fno-31` | Order pad · Sell · Intraday | [8671:18433](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=8671-18433) | — |  |
| `fno-32` | Order pad · Buy · ILLIQUID (edge case) | [8671:18433 + product rule](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=8671-18433 + product rule) | — | Should never be reached — every entry point blocks illiquid contracts — but if one slips through: ILLIQUID tag in the header (tap → “What does illiquidity mean?”), the blocked note in the dock (tap → same sheet) and Buy disabled. Inputs stay usable. |
| `fno-33` | Order pad · Sell · ILLIQUID (edge case) | [8671:18433 + product rule](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=8671-18433 + product rule) | — | The same edge case on the Sell side: Sell disabled. |

## Spec (README.md)


> **ILLIQUID contracts** span this flow and others — read [`docs/ILLIQUID.md`](https://lemonnade-design.github.io/lemonn-app-prototype/ILLIQUID.md) (rule, data flag, UI patterns, every place) before building any of it.

The F&O tab, implemented with Lemonnade V3 components from Figma [F&O Home → Equity](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=11569-41100) and the [F&O Home section](https://www.figma.com/design/nLs24dTJdPz9A5pu3AWMbe/?node-id=6754-63073) (Commodities, asset selection, lot selection, Strategies — drawn in the old D2 system, rebuilt in L3 with the same look).

- **Local prototype:** `http://127.0.0.1:5202/#/fno-01`; board: `#/fno`
- **Status:** implemented · 2026-10-26
- **Entry:** F&O in the main bottom navigation. **Exit:** Home → Stocks.

### Screens

| Id | What it shows | Figma |
|---|---|---|
| fno-34 | Splash: the launch splash (`src/shared/ui/Splash`), the Lemonn logo centred (it rises in). Shown for 1.5 s, then it fades into fno-01; plays whenever the app opens or reloads on F&O home | — |
| fno-01 | Equity home, top | 11569:41100 |
| fno-02 | The same page, at Watchlists / Smart Options | 11569:41100 |
| fno-03 | The same page, at Futures Heatmap | 11569:41100 |
| fno-04 | The same page, at Smart Futures | 11569:41100 |
| fno-05 | Scalper | Screenshot supplied 2026-10-26 |
| fno-06 | Scalper, with DASH indicator sheet open | — |
| fno-07 | Scalper, with the saved indicator applied | — |
| fno-35 | Scalper, a position open: TP / entry / SL pills and the breakeven line (version C, Boxed chip) | 11756:78739 |
| fno-36 | Break Even · How breakeven works (animated explainer sheet) | 11783:5569 (dark 11783:6220) |
| fno-37 | Chart tools sheet on Settings | 11754:69563 (dark 11783:9335) |
| fno-39 | Zing signals (Scalper → Active chip): quick chips, Active signals, signal cards | 6900:23855 (file 9r61YQp7QQZAQovDyz8hLF) |
| fno-40 | Zing signals · filter on Indices (chart tools layout) | 6900:26203 |
| fno-41 | Filter · Indices with NIFTY 50 + SENSEX picked | 6900:29666 |
| fno-42 | Filter · Win rate | 6900:27042 |
| fno-43 | Filter · Call/Put | 6900:27889 |
| fno-44 | Filter · Strategies | 6900:28736 |
| fno-45 | Your filter saved, with the "saved for quick access" tip | 6900:30528 |
| fno-46 | Your filter saved | 6900:24637 |
| fno-47 | All Signals, plain (heading + every signal) | 6900:25420 |
| fno-08 | Commodities home | 6754:63637 |
| fno-09 | Commodities home, at Futures Heatmap | 6754:63637 |
| fno-10 | Contract picker sheet, Commodities tab | 6754:65111 |
| fno-11 | Contract picker sheet, Equity tab | 6754:65054 |
| fno-12 | Gold Summary (lot selection), by price | 6754:65113 |
| fno-13 | Gold Summary, by volume | 6754:65288 |
| fno-14 | Gold Summary, margin per lot | 6754:65444 |
| fno-15 | Strategies · Equity | 6754:64178 |
| fno-16 | Strategies · Commodities | 6754:64607 |
| fno-17 | Option chain | 11630:16785 |
| fno-18 | Option chain · Buy selected | 11630:16184 |
| fno-19 | Option chain · Sell selected | 11695:26269 (Sell frame) |
| fno-20 | Option chain · illiquid contract tooltip | — (Groww reference, 2026-10-29) |
| fno-21 | Asset page · Gold MINI (commodity) | 6754:61613 |
| fno-22 | Asset page · illiquid commodity | 6754:61613 + product rule |
| fno-23 | Gold Summary · Buy / Sell sheet | live app screenshot 2026-10-29 |
| fno-24 | Gold Summary · illiquid Buy / Sell sheet | live app + product rule |
| fno-25 … 28 | Order pad · Buy (Market, Limit, SL, Intraday) | 8671:18433 |
| fno-29 … 31 | Order pad · Sell (Market, SL, Intraday) | 8671:18433 |
| fno-32, 33 | Order pad · ILLIQUID edge case (Buy, Sell) | 8671:18433 + product rule |
| fno-38 | Commodity calendar — View all on Expiring This Week: expiry days with their contracts | — (user's reference, 2026-11-17) |

### Structure

- `screens/Home.tsx`: page composition, scrolling, modal state, local watchlists.
- `components`: F&O sub-navigation, the Stocks-home-matching header, P&L and indices, chart, discovery, contracts, heatmap.
- `sheets/HomeSheets.tsx`: single-choice sheet, create watchlist, contract details and unavailable-destination sheet.
- `data.ts`: typed snapshot contracts, indices, watchlists, chart series and heatmap cells.
- `copy.json` / `copy.ts`: translatable UI copy. Market names and values live in data.
- `commodities/` — the Commodities product tab and its pages: `components/CommoditiesFeed` (the tab's sections in order), `CommodityShortcuts`, `PopularCommodities`, `CommodityHeatmap`; `sheets/ContractPickerSheet` (“Choose options contract”); `screens/LotSummary` (Gold Summary); `data.ts` (commodities, contracts, heatmap groups, picker groups, gold lots — the API contract for this tab); `assets/` (commodity artwork exported from Figma, resized to 2× / 3×).
- `option-chain/` — the Option chain: `screens/OptionChain` (top bar, selectors, stats, column heads, strike rows, spot pill), `components/OrderDock` (the order panel), `data.ts` (underlyings, expiries, chain quotes — the API contract).
- `strategies/` — the Strategies product tab: `components/StrategiesFeed` (pill group, Zing Trades, Smart Invest, Pre-build Strategies, Quick Trade cards); `data.ts`.
- `screens/Home.tsx` renders the shared header, P&L, indices and product tabs once, and the selected tab's feed under them (`product` prop). Equity, Commodities and Strategies reuse the same sections where Figma does (watchlists, chart, contract cards, sheets).
- `assets`: exported Figma artwork for Zing, product tabs, shortcuts and chart actions. Monochrome paths use L3 MaskIcon; detailed shortcut artwork keeps its original SVG with inversion in dark mode.

### Navigation and behaviour

Main F&O → fno-01. Home → stocks-01. Search → search-25 (F&O selected, Back → fno-01). ScalpPro and the Scalper tab → fno-05; Back → fno-01.
Profile → profile-01; Wallet → deposit-01; DASH → dash-02. These shared flows retain their existing return behaviour.
The other F&O navbar items open a sheet explaining that those destinations are outside this prototype; they do not switch the selected Equity tab.

- Total / Day P&L switches the displayed example.
- Index selector uses a sheet of Radio rows. Chart metric tabs update the example series.
- Watchlist shortcut scrolls to the section. Add watchlist validates a nonblank name (40 characters max), adds a local empty list and shows a success toast. Changes last while the home is mounted.
- Contract cards open details. Instrument scope changes Index / Stock. Category pills select example orderings; By Price / By Volume changes the displayed value and sorts volume descending. Calls / Puts filters include an empty result when the sample has no puts.
- View all on Smart Options / Smart Futures opens the existing combined signals list (index / stock scope respectively); these are shared prototype lists, rather than newly designed destinations.
- Heatmap filters show subsets of the example snapshot. Stock / Index changes labels. Tiles open details.
- Sheets use shared Sheet hosting and L3 focus management, Escape and backdrop dismissal.
- **Scalper (fno-05)** is rebuilt from the live app's screenshot (2026-10-26, dark), measured to it at 392 wide:
  - top: back · strategy tabs (L3 ribbon "All", recoloured with the Tabs' own variables so it runs into the tool row)
    · Add more strategies (Zing-edged ring); the tool row (36, surface/primary, dashed line under it): Positions ·
    Orders · Option chain, then the Active chip (Zing tint, count 14 on its icon) running off the right edge — the row
    scrolls sideways;
  - two chart panels on surface/primary, a 16 band with a drag handle between them: instrument (name ⇅ underlined,
    Spot ⇅, link-charts), price · change · ▲ (percent) in the up colour; the spot panel's buttons are chart type
    (US-stock blue tint) and chart tools, the option panel has chart tools only;
  - each chart (`components/TradingPane`): candles, a 50-wide price axis with round steps and the last price tagged in
    the up colour (dashed line to it), the session high / low marked with value · dot · line, zoom in / out against the
    axis, a time axis every 50 minutes (12:15 … 15:25 / 12:25 … 15:35) and "5m ▾" in the corner;
  - order dock: Market / Limit-Trigger (L3 pill group, outlined), Buy at Mkt (brand) · quantity in lots (L3 Stepper
    Large, steps of one lot = 65) · Sell at Mkt (secondary), the margin each needs and the funds under the stepper.
  Values and candles are illustrative (`data.ts`, traced from the screenshot, high / low pinned to its markers); no
  order is submitted.
- **Chart tools sheet** (`sheets/ChartToolsSheet`, from either panel's tools button; fno-06 opens with it up): a 96
  **Side nav** column (L3 `SideNav`, discover tone, Zing flag: Range · Zing NEW · Indicators · Drawings · Templates · Settings) and the
  chosen group beside it. Indicators: **Your indicators** (made with DASH AI, Create indicator, or "No indicators
  created yet.") and **Lemonn indicators**, each a starred 32-tall row. DASH's View indicator opens it with the saved
  indicator listed. Picking one closes the sheet and applies it (fno-07): its name under the spot quote and two
  illustrative moving-average lines (EMA 9 / 21 of the sample candles) on the spot chart.

#### Scalper position and breakeven (fno-35 … 37)

Figma: "Scalper screen · C · Boxed chip" (the yellow chip version; A / B are not built).

- **A position on the option chart** (`components/PositionOverlay`, laid over `TradingPane` via its `overlay` prop,
  which hands it the pane's price ↔ pixel scale):
  - dashed lines across the plot at TP (up colour), entry (content/primary) and SL (down colour); the entry price is
    tagged on the axis (inverted), the last price keeps its own tag;
  - **TP pill** (from 64 in): drag handle ⠿ · green Tag "TP Qty:65" · the P&L if it fills, (TP − entry) × qty · ✕
    (removes the TP);
  - **entry row** (from 12 in): Exit · blue Tag "+65" · live P&L, (last − entry) × qty · ✕ (exits too). With TP or SL
    removed, "+ TP" / "+ SL" buttons appear here and put it back 10 from the price;
  - **SL pill**: ⠿ · red Tag "SL Qty:65" · the P&L if it fills · ✕ · Add Trail (toggles; "✓ Trailing" when on);
  - **dragging** a ⠿ (or focusing it and ↑ / ↓, Shift = ×20) moves TP / SL in ₹0.05 ticks. TP stays above the last
    price and SL below it, both at least 30 px clear of the entry row and 12 px inside the plot. The P&L updates live;
  - **the breakeven line**: solid 1px `border-accent-warning-light` at the breakeven price (Figma 11756:79330), with the
    boxed tag "Breakeven ⓘ" on it (Figma reads "B/E 105.55"; spelled out without the price, designer's call 2026-11-03 — its accessible label keeps the price) 8 left of the price axis (Figma 11756:79332: warning-light surface and 1px
    edge all round, radius 4, Label/10 in warning, 16 tall, Figma's 12 info_outline tinted in the text colour). Tap → How breakeven works. Hidden when Settings → Breakeven
    line is off.
- **Breakeven price** (`data.ts` `breakevenPrice`): entry + the round trip's charges ÷ quantity, rounded **up** to the
  ₹0.05 tick, so selling at it is never a loss. Charges (`optionCharges`): brokerage ₹20 × 2 orders, STT 0.1% of the
  sell premium, NSE transaction 0.03503% of turnover, SEBI ₹10 / crore, stamp 0.003% of the buy, GST 18% on
  brokerage + exchange + SEBI. 1 lot (65) at ₹104.60 → ₹105.55; at ₹100 → ₹100.95. The API should send the real
  breakeven (it knows the user's brokerage plan); this is the client-side fallback.
- **Buy at Mkt** opens a position at the last price (TP / SL 10 either side) or adds to the open one (average entry);
  **Sell at Mkt** sells the dock's quantity (all of it closes the position). With a position, the option chart shows
  its last 18 candles and its scale takes in the TP / SL as they were when it opened (not while dragging, or the scale
  would run away), and the option pane takes 3 parts of the height to the spot pane's 2.
- **First buy** → How breakeven works opens by itself, once (prototype: remembered in this browser,
  `fno.breakevenIntroSeen`; in the app, per user).
- **How breakeven works** (`sheets/BreakevenSheet`, fno-36): L3 sheet, heading only. The example card ("Example:
  Bought 1 lot at ₹100") plays the explainer once and stops on the finished chart; a tap on it plays it again from the start (`components/BreakevenExplainer`), copied from the
  designer's screen recording (Figma's own export holds only the intro), plus a charges breakdown before the B/E line
  (designer's brief, 2026-11-03). Data: `data.ts` `breakevenCharges` — the F&O options rate card worked out in ₹ on
  the ₹100 buy, one unit so a % reads straight as ₹ (brokerage 0.01% each way ₹0.02, STT 0.15% on the sell ₹0.15, NSE
  transaction 0.03553% each way ₹0.07, SEBI 0.0001% each way ₹0.0002, stamp 0.003% on the buy ₹0.003). No GST band:
  GST is charged on the charges, not the trade (designer's call) — but it counts in the total: `exampleGst` = 18% of
  brokerage + transaction + SEBI (≈₹0.016). `breakevenExample` — bought ₹100, B/E = ₹100 + the charges with GST
  (≈₹0.26) up to the next tick = ₹100.30, sold ₹102, the price path's five turns.

  **Versions** (F&O setting "Breakeven sheet", also a floating card beside the phone on fno-36; 2026-11-16):
  **Version 2** (default) — heading "What is breakeven line?" (was "… price?" with a description
  under it; both changed 19 Nov), the example, then the charges table; the two info lines are hidden. **Version 1** — the sheet as it
  first shipped: heading "How breakeven works", the example, then the two info lines; no table.
  **Charges table** (under the example card, `ChargesTable` in the sheet; 2026-11-16): the same trade as a calculation,
  on a secondary-surface card (radius 12, no edge, no lines inside) so it stands out on the sheet (no heading): compact
  L3 key-value rows (4 / 16), one line each: Bought at ₹100.00 · Order charges
  (incl. GST) ≈₹0.26 · Breakeven price ₹100.30 (the L3 total row: bold label, larger value, on the same grey). The
  charges row is closed by default; a tap anywhere on it (its label is the toggle, ⌄ turns) opens the breakdown under it
  as sm rows on a tertiary-surface panel (radius 8): STT, Transaction, Brokerage, Stamp duty, SEBI, GST (18%).

  **Charges, zoomed in:** at the normal scale the charges zone is ~13 tall, so the chart zooms in 2× (106 per rupee;
  the zone ~27 tall; ₹100 stays at y 209, ₹102–₹103 move up out of view — only 2× so the charges don't look big) and
  the zone fills one band per charge, top down — STT, Transaction, Stamp duty, SEBI, then Brokerage last at the bottom. They come in top down, so Brokerage comes in last (its tag the small one: Label/10, 1 / 4 padding — designer's call, brokerage is a small part) — each band, stacked bottom to top Brokerage → Stamp duty, as tall as its share
  of the charges (at least 2; 1 apart), in the charges-zone orange. Each band gets a white tag like the B/E chip (name
  Label/12 primary · ₹ amount secondary: ₹0.15, the tiny ones to their first digit, ₹0.003) in a column 140 from the plot's right, at least 24 apart and 10 from the top,
  joined by an orange leader to a dot at its band's middle. Zooming out, the bands close into one zone and the tags
  slide straight down, stacking into one tag that reads "Order charges ≈₹0.26" (orange name, the total secondary with ≈ as it's rounded; white pill) 6 under the zone, in
  the same column — the zone is too thin to hold a label (so the label comes from the charges, not out of nowhere). By
  the rate card brokerage is ~8 % of the charges (STT ~62 %, transaction ~29 %, stamp ~1 %, SEBI ~0.1 %), so its band
  is thin next to STT's — the numbers aren't bent to make it the smallest.

  The stage is white (surface/primary), 286 tall. Plot: ₹100 at y 209, 53 per rupee; gridlines from x 53.5 to 12.5 short
  of the right edge (dashed 4 / 3 border/light; ₹100 solid); axis labels at x 12.5 (₹101–103 Description/12 tertiary,
  ₹100 Label/12 primary). Orange charges zone ₹100 → B/E; green net-profit zone B/E → ₹102 (green 100 → 50 → 40 % fade);
  dashed orange B/E line with a white chip at the right ("B/E" tag on orange, ₹100.25). The price line (1.75, primary)
  turns at 2.9 / 23.9 / 40.7 / 60.8 / 86 % across the plot (₹100, 100.10, 100.25, 101.10, 102). Callouts are white pills
  with a light edge and a soft shadow: "Bought at ₹100" 12.5 under the buy dot (notch up), "Sold at ₹102" 10 left of the
  sell dot (green edge and text, check icon, tail right), LTP 8.5 above the line's head.

  | t (ms) | What |
  |---|---|
  | 150 | axis and gridlines fade in (250) |
  | 400 | buy dot pops in (200, back-out); 650 "Bought at ₹100" fades in and rises 4 → 0 (150) |
  | 1000 | zoom in on ₹100 → B/E (500, ease-in-out): 53 → 283 per rupee, around ₹100 |
  | 1550 | the bands fill up one every 350 (STT, transaction, stamp duty, SEBI, then brokerage): each grows up from the one below (300, ease-out) as its tag fades in rising 4 → 0 with its leader; the last is in by 3600 |
  | 4100 | zoom out (600, ease-in-out); the leaders fade (150); the whole zone fades in over the bands, closing their gaps; the tags slide to the zone's label spot (8.5 in, 10.5 under B/E), top tag first, each 30 later (450, ease-in-out), stacking up |
  | 4600 | the stacked tags cross-fade (150) into one white "Order charges" tag in the charges orange; 4950 its pill fades (250), leaving the label |
  | 4750 | B/E line draws left → right along the zone's top (450, ease-in-out); 5200 its "Breakeven" tag (text only, as on the chart) fades and scales 0.9 → 1 (200) |
  | 5550 | LTP bubble pops in at ₹100.00 (150) |
  | 5800 | the price line draws at a steady pace to ₹102 (2150); the bubble rides its head showing the last turn passed (cross-fades 100 ms at each); at B/E a ringed marker appears and pulses (r 7.5 → 14, fading, 400 ms) |
  | 7950 | the line ends: a green ring; 8000 the bubble fades (150), the green dot pops in (200), 8200 it pulses (500) |
  | 8250 | "Sold at ₹102" fades in sliding 6 → 0 from the right (150) |
  | 8450 | net-profit zone grows up from B/E to ₹102 (550, ease-out); 9150 "Net Profit" fades in (150) |
  | 9300 | it holds on the finished chart (2.2 s), then the next play starts with the intro, on loop. A tap (or Enter / Space) after the first play starts it again from the intro |

  **Every play opens with the intro** (19 Nov): for 2.5 s before the chart's t = 0 — the Breakeven mark, INTRODUCING,
  Breakeven Line, the one-liner (Figma's reveal), fading (300) into the blank chart — on open, on each loop and on a tap.
  The times above are the chart's own, from when the intro has gone. "I understand" unlocks when the chart first
  finishes (2.5 + 9.3 s).

  **V2 — archived 2026-11-04, not in the app** (`archive/BreakevenExplainerV2.tsx` + its CSS, with the steps to bring it
  back): starts zoomed in, the line rises from the bottom to the buy at ₹100 over a blue ₹0 → ₹100 fill, the charges
  fill and merge into Order charges, then it zooms out true to scale (₹100 stays put, the chart shrinks down to ₹0) and
  runs 12% up to "Sold at ₹112" (10.25 s). Copy `breakeven.chartLabelV2` is kept for it.

  "I understand" is disabled until the chart has played once (Figma's button variants 11783:12460, dark 11805:374): a
  4 track (surface/tertiary) across the button's top edge fills (surface/inverted, linear) over 9.3 s, then the button
  turns primary. Reduced motion: the finished chart, no loop, the button ready. Dark mode (the recording is light only):
  L3's warning / success colours. The info rows (20 icons, Description/12 with bold parts) are as Figma.
- **Chart tools → Settings** (`sheets/ChartSettingsPanel`, fno-37): Auto TP/SL card row (animated mark · Applied tag
  · ›; nothing behind it yet), Chart type (Candles / Heikin Ashi / Line, selected = discover tint; the chart doesn't
  redraw yet), Stop Loss Preference (At Market Price / At Limit Price, radio cards), View on chart (Breakeven line ⓘ
  New, Buy/Sell executions, Sync Charts, checkbox cards). Edits are a draft: the sheet's dock shows Cancel · Apply
  only while Settings is open; Apply keeps them, Cancel / closing the sheet drops them. The ⓘ opens How breakeven works.
- **Auto TP/SL mark** (`components/AutoTpSlIcon`) — Figma's motion (11756:79819 / 79827 / 79835): 1.198 s, played
  forward then back. Candle: opacity 0 → 1 and scaleY 0.15 → 1 by 29%, ease-out. TP bar: from 25% to 46% it fades in
  (ease-out) and slides 5 → 0 (cubic-bezier(0.2, 0, 0.2, 1.3), a slight overshoot). SL bar: the same from 38% to 58%.

#### Zing signals (fno-39 … 47)

From the Active chip at the right end of the Scalper's tool row (Zing). Figma: "Enrich signal filter" 6900:23853 in file
`9r61YQp7QQZAQovDyz8hLF` (drawn in the old Lemonn design system), rebuilt in L3, light and dark. `sheets/SignalsSheet.tsx`;
sample signals in `data.ts` (`zingSignals`, `SignalFilter`, `matchesFilter`).

- **Signals sheet.** 75% of the phone screen's height whatever the number of signals (the list scrolls inside). In the header's place a chip row: the filter button (Tertiary Small, a red dot once a filter is
  saved) | L3 pill tabs (Small): Your filter (n) ✕ once saved · All Signals (n) · 🔥 Win rate ≥ 50% (n) · Commodity ·
  Nifty · Sensex. Counts are worked out from the signals. Body: "Active signals (n)" (Heading/14) with a Total P&L tag,
  then one L3 Card per signal: Avatar 32, strategy (Heading/12, secondary), tags (market · Win rate n% in green, or a
  P&L tag), View (Small primary); under a hairline the trade in Label/12: Buy Call 23950 • RR 1.4 • the rule (EMA 9 >
  EMA 21, Price ≥ EMA 9, PCR 1.55). A chip with no signals shows the L3 empty state.
- **Filter** (filter button): the sheet turns into the filter in place, in the Scalper's Settings sheet look (chart tools
  → Settings; it reuses `ChartToolsSheet.module.css`): the 96 L3 Side nav (Indices · Win rate · Call/Put · Strategies),
  the white panel with its sticky Heading/16 title row over a hairline (Clear All on the right empties the group), 48
  card rows 8 apart. Checkboxes for Indices (All Indices, NIFTY 50, SENSEX, BANKNIFTY, F&O Stocks, Commodity — All
  Indices = none picked) and Strategies (with the strategy's avatar); radios for Win rate (All, ≥ 50%, ≥ 30%) and
  Call/Put (All, Call, Put), the chosen one in the discover tint like Stop Loss Preference. A group that narrows the
  list shows how many it picked in the tile's corner. Shorter than Settings: the list area is 412; the picks sit under
  it in Figma's 44 strip as pills (surface-primary, border-light, Label/12 secondary, ⊗ 16; ✕ removes one; long names
  cut at 140); then the dock: Cancel (secondary) · Apply (primary, black — Settings' Apply is brand).
- **Apply** saves the choices as Your filter: it comes in first and selected, with an L3 tooltip "Filter applied &
  saved for quick access" (✕) once. Applying nothing removes it. Cancel (or a scrim tap) drops the changes. ✕ on Your
  filter removes it and goes back to All Signals.
- **Commodity signals** (20 Nov review, settled 24 Nov): users couldn't tell an MCX signal from an index one. The sheet
  starts with the filter button | the chips — All Signals · Win rate ≥ 50% · Nifty · Sensex · F&O Stocks · Commodities
  (sideways scroll) — and a line under them (no segment tabs: removed 24 Nov). A commodity card's tag is amber, with the
  commodity's logo and name (index and stock cards keep the grey tag), and the nudge strip sits over it. The other
  versions tried on 20 Nov (grey tag, MCX tag, logo on the avatar, segment tabs, commodity picture, header with tabs)
  were removed on 24 Nov.
- **Commodity nudge strip** (setting "Commodity nudge strip", Figma 6946:42446, 24 Nov): commodity cards still didn't
  stand out, so a 28 strip peeks out from behind a commodity card's top edge with a reason to look (data: `nudge` on the
  signal — how many traded it today, today's move). It's the sheet's only setting; Off hides it.
  Motion: once the sheet is up the strip slides out from behind the card (0 → 28, 400 ms, decelerate; one card after
  another, 250 ms apart), its line rises in, then a light shimmer sweeps left → right every 3 s. Switched on while the
  sheet is up, it comes out at once; switched off, it reverses — the line fades, the strip tucks back behind the card
  (400 ms) and the ring fades, the card sliding up with it (the card itself never changes size). Switching between
  versions keeps the strip out; only its picture and line rise in anew. Reduced motion: none.
  On a phone, a floating S0 … S4 bubble (left, over the chart) flips it.
  1. Gold glow (Figma, default) — the strip warm in its top-left corner (halfway zing light → honey 200) fading to zing
     light 64 across, a 1 gold ring round strip and card (zing light → honey 300 at the bottom; Figma 6947:45037, 24
     Nov), the gold bars (18; other commodities: their logo) on a soft white glow, "**2.1K+ people** have traded on gold
     today" (Heading/10 + Label/10, honey 800). Versions 2 and 3 use the same shape in their own colours.
  2. Colour per commodity — as 1, in the commodity's colour (gold honey, crude oil / silver grey, natural gas
     tangerine), its logo, and a pulsing green Live dot on the right.
  3. Dark ticker — the inverted surface, an orange flame, "**Trending on MCX** · 2.1K+ traded today" in honey.
  4. Rotating facts — 1's strip, without the shimmer; the line and its picture turn over every 5 s (rising in together): traded today ·
     "**Trending on MCX** · 2.1K+ traded today" with the orange flame (as 3) · "Gold is +1.2% today" with a trend arrow
     (up or down, in the strip's brown text colour) · "MCX is open till 11:30 PM". The soft white glow sits only under the gold bars
     (no glow under logos or icons, in every version).
  (The grouped-list version was removed, 20 Nov. Setting values stay v1, v2, v3, v5, v6, v7, v8.)
  Chips not picked read in text secondary (all versions).
  The setting is a dropdown (desktop panel and phone settings); on a phone (app mode) a floating V1 … V7 bubble on the
  signals sheet screens (fno-39, 45, 46, 47) steps to the next version in one tap. It starts on the chart, above the
  sheet (`quickSwitch.spot`), and can be dragged.
 · fno-40 … 44 the filter on each group (41: NIFTY 50 + SENSEX picked; 44: plus a
  strategy) · fno-45 / 46 Your filter saved (with / without the tip) · fno-47 the plain All Signals look.

#### Commodities (fno-08 … 14)

- Product tabs: Equity → fno-01, Commodities → fno-08, Strategies → fno-15. The header and tabs don't move; only the content below slides (forward = from the right, back = from the left). On scroll the tabs stick right under the top bar (`position: sticky` in the page — they sit mid-page under the overview, so not in the Actionbar's bottom slot); a tab switch while scrolled lines the new content up under them. Once stuck, the tab row takes the scrolled top bar's colour (surface/primary, not the active tab's gradient); the active tab stays as it is.
- **Shortcuts** Gold · Silver · Crude Oil · Natural Gas (artwork, name, day change in up / down colour) → Gold Summary (fno-12).
- **Expiring This Week** (`ExpiringThisWeek`, between the shortcuts and the chart): a sideways rail of contracts expiring soon (`expiringThisWeek` in `commodities/data.ts`), in three variants (`kind`): **option**, **future** (one GOLDM future sits second, for testing) and **event** (third), snapping to the 16 inset. Each card: the symbol (GOLDM) over the expiry as plain description text (12) — option “OPT Expiry Today / Tomorrow / <weekday>”, future “FUT Expiry 3 Dec” (no Tag; the future's expiry line is not shown); on the right the trend read-out (`TrendBadge`, the same component as the chart's header: Strong Uptrend / Downtrend in up / down colour over “Since 3:25 PM” (description 12 here, 10 in the chart), double arrow); a hairline; then two columns, label (description 12) over value — the ATM option (₹ premium + change) — or LTP (₹ + change) for a future — left, Margin Per Lot right. Action footer (no fill, 16 under the details like the other parts): ScalpPro (secondary, Medium) → fno-05 and Buy (primary, Medium) → the contract sheet. A tap on the card → the contract's asset page (fno-21). The trend read-out (the whole top right — label, since, the i, the arrow; hit area grown 12 around it) → the **trend info sheet** (`TrendInfoSheet`, live app reference 2026-11-17): no header; the trend on the left (arrow first, text left-aligned) and the symbol with its day change on the right over a hairline, Dash's two bullets on what's behind the trend (`trendNotes` in `commodities/data.ts`), a grey disclaimer (warning icon, “Disclaimer:”), a dashed rule, “Analyzed by Dash” with the Dash orb (24), then Okay (Large). The event card's Bullish read-out has the i too and opens the same sheet. The read-out is a `role="button"` span, not a button, because the card body is already a button; its tap doesn't open the card. The commodity art is hidden (`SHOW_ART = false`, kept). Prototype setting “Expiring card buttons” (Commodities, toggle, default Shown) hides the whole button footer; on a phone (app mode) a floating “BTN ON / BTN OFF” switch on the Commodities home (fno-08 … 10) flips it in one tap.
- **Expiring This Week, Version 2** (`ExpiringCalendar`; prototype setting “Expiring This Week”, Commodities, Version 1 = the card rail above; Version 4 is the default): the same section as a short calendar. The calendar's first 3 entries (`expiryPreview(3)` in `commodities/data.ts`) on their days, drawn like the calendar page (`CalendarDay`, shared with fno-38): the grey date block left (today not marked, not sticky here), one card per contract or event (8 apart), days 16 apart, so it's three rows on one day or spread over two or three days. Within a day events come first (they're timed) and stay short (name over time, then the asset cards; the readings are on the calendar page). Contract rows as on fno-38: kind under the name, option chain (options) → fno-17 and ScalpPro → fno-05, row → asset page fno-21. View all → the Commodity calendar (fno-38).
- **Expiring This Week, Version 3** (`ExpiringCalendarCard`): Version 2's three entries in **one card**. Each day is a band: the date (weekday over the number, every date the same weight) as the card's grey left column, attached edge to edge and as tall as that day's rows, the rows beside it. Hairlines between days (across the date column too) and between a day's rows. Rows behave as in Version 2; View all → fno-38.
- **Expiring This Week, Version 4** (`ExpiringDayPicker`, **default**): a day picker over the next month (31 days) of the real MCX calendar. A row of small date cards (weekday over the number, 48 wide, 10 apart), only days that have something; it scrolls sideways and runs edge to edge (the screen's 16 inset as padding inside the row), fading at an end only while there's more to scroll that way (CSS mask, `data-more-before` / `-after`). Weeks run Monday to Sunday; each later week starts with a thin grey pill the cards' height (18 after the last day, 10 before the next), its text turned 90° in 8 upper case: “NEXT WEEK”, then the week's Monday (“7 DEC”). The selected day (first, to start) has a dark border on grey. Under the row, that day's contracts (option chain + ScalpPro) and events (on one line), one card each, 8 apart. View all (a Ghost Small button with a calendar icon before the label, `ExpiringHeader`, shared by all versions) → fno-38.
  - **Event card** (third; data from the user's reference card, its layout kept to the option card's): a market event
    on the contract's commodity today. NATGASMINI over “NG storage · Today 9:00 PM”; the trend read-out says the outlook
    (“Bullish” over “Smaller build”, up arrow, no info icon); hairline; then the ATM option (305 CE ATM ₹7.40 +4.20%) and Margin Per Lot (₹1,850), and
    the same ScalpPro / Buy footer. The same report sits today on the Commodity calendar's Events tab (fno-38).
- **Chart**: same as Equity, the instrument selector reads “Gold ⇕” and opens the contract picker (fno-10). Picking a contract renames the chart and closes the sheet.
- **Contract picker** (`ContractPickerSheet`): header “Choose options contract”, underline tabs Equity (8) / Commodities (7) in its bottom slot; on Commodities, pill chips All / Gold / Silver / Crude Oil / Natural Gas / Copper / Aluminium / Zinc filter the groups. Rows: ListCell Small with artwork, name, price + change, a “Lowest Margin” discover Tag where it applies, Radio. The selected row is highlighted (ListCell `selected`).
- **Watchlist** — same as Equity.
- **Popular commodities**: Options ⇕ Futures switch (secondary pill), divider, pills Top traded / Top gainers / Top Losers / Advanced declined, Filter (sheet) and By Price ⇕ By Volume. Option card: name + type | expiry left, price + change right. Future card: price and change on one line, “Margin / lot : …” under it. Options shows the frame's own rows (three calls and one future).
- **Futures Heatmap**: Bullion / Energy / Metals pills, 3-column tiles in profit / loss surfaces; a tile opens its details.
- **Smart Futures**: the Equity section with commodity contracts.
- **Gold Summary** (`LotSummary`): Actionbar back (→ fno-08) + “Gold Summary”; lot tabs with artwork (Gold, Gold Mini, Gold Guinea, Gold Ten, Gold Petal) in the bottom slot, scrolling sideways. Futures (View all) — two future cards. Options (View option chain → the F&O options list) — expiry month pill (October ⌄ → month sheet), divider, Top traded / Most active / OI gainers / Top gainers, Filter, sort. Sort opens a sheet: **By Price** (price + change), **By Volume** (traded volume only), **Margin per lot** (₹ per lot only) — fno-12 / 13 / 14 open on each. Filter Puts shows the empty state (the sample has calls only).

#### Commodity calendar (fno-38)

- **Layout (every version):** months, each with a sticky title (L3 SectionHeader at heading-20, 12 above and below it — also 12 above while stuck at the top), then its days 32 apart (no line between days). Each day is the grey date block on the left and **one card per contract or event** on the right, 8 apart (`CalendarDay` with `separate`). Between two months a 2 line (border/light) runs edge to edge, 24 above and 24 below to the next title. (The V4 week-section view of 24 Nov is archived: `commodities/archive/DayPickerByWeek.tsx`.)
- **Entry:** View all on Expiring This Week (fno-08). Back → Commodities home. Layout after the user's reference
  (an Expiry Calendar screenshot, 2026-11-17): only names and simple buttons, no prices.
- **Tabs:** All · Options · Futures · Events — flat L3 Tabs (underline) with a 16 icon each (apps, candlestick chart,
  trending up, event), in the Actionbar's bottom slot (sticky). The body slides with the tabs: a tap slides the new tab's list in from its
  side, and a left / right swipe on the list drags it to the next / previous tab (rubber-band at the ends; shared
  `useSwipeBetween`, as on Market's tabs and the stocks theme page). All (default) merges the three by day — options, then
  futures, then events — and says under each name which it is ("Options", "Futures", "Event").
- **Events:** for now only the US EIA weekly reports that move MCX energy — crude oil inventories (Wed 9:00 PM IST)
  and natural gas storage (Thu 9:00 PM IST). There is no event page, so the row shows everything upfront — the fields every
  economic calendar carries (Investing.com, Zerodha's markets calendar, broker commodity dailies):
  - top: event icon (Avatar 24), the event's name (up to two lines, then ellipsis), under it the release time in IST ("9:00 PM"); no buttons, no country, no impact tag;
  - Previous / Forecast / Actual in a 3-column Grid (caption secondary over label 14); Actual reads "Due" until it's
    out. Left out for an event with no number;
  - what it moves, one per commodity in a row that scrolls sideways; tap → that asset's page (fno-21): an L3 Tag
    (tertiary, small, profit / loss colour) with an up / down arrow (msArrowUpward / msArrowDownward) and the name — the
    arrow says bullish / bearish, so the tag stays small. 10 below the readings.
    An event can move several commodities in different directions (crude inventories: down Crude Oil, Natural Gas; up
    Gold). One tag per commodity, never its contract sizes — Gold and Gold Mini move together, so it's just "Gold"
    (same for Crude Oil, Natural Gas, Silver). Data `moves: {name, trend}[]`. No buttons on an event row, no line on how it moves prices.
  The details line up with the name (indented past the icon). The row itself isn't tappable.
- **Days** (`ExpiryTimeline`, data `expiryCalendar`) run from today under a month section header (L3 SectionHeader, content-primary:
  "Nov 2026"; repeated when the month turns), 24 apart. Left (48 wide): one date block (surface-secondary,
  radius 12, padding 08 / 04) with the weekday (description 12, secondary) over the date (label 16); today adds a
  border-dark ring. Right: one static card
  (flat) with that day's contracts — one day can hold several, split by hairlines.
- **Contract row** (tappable → asset page fno-21; hover and press turn the row surface-secondary, clipped to the card's corners; 12 from every side of the card, content centred vertically): the commodity's icon (L3 Avatar 24, circle, without its 1px edge — the commodity art from `assets/`; Zinc, Copper,
  Aluminium and Lead have no art yet, so their Avatar shows the chemical symbol as initials: ZN, CU, AL, PB), 12 gap, then the contract's name (label 14) and icon-only Tertiary Small buttons, flat (`raised="none"`, no shadow). Options: option chain (link icon → option chain
  fno-17, its back returns here) on the left, ScalpPro (→ Scalper fno-05) on the right. Futures: ScalpPro only (no option chain). Small, not Large: they sit inside a list row, like the reference.
- **Sticky while scrolling:** each month's section header sticks at the top of the page (surface-default behind it)
  until the next month's pushes it out; each day's date block sticks 08 under it for as long as that day's card is in
  view (a day with several contracts keeps its date until its last row has scrolled past). Section-level stickiness in
  the page itself, not the Actionbar's bottom slot: it changes as you scroll, unlike the tabs.
- **Data:** `inDays` from today, so the dates always lead from today.

#### Strategies (fno-15, 16)

- Shortcuts (as Equity), then a full-width **pill group Equity / Commodities** (fno-15 / fno-16).
- **Zing Trades** (Explore): rail of cards — trader avatar, strategy name, “Built with DASH Ai”, today's return; divider; Last week (M T W T F dots: green = profit, grey = no trade, red = loss), Avg. trades, Win rate (trending icon); grey footer: ☆ save · Learn in 30 Secs (play ▶ ›) · Apply (primary).
- **Smart Invest** (View all): rail of cards — logo, basket name, By lemonn, min. deposit; 7 Days P&L ⇕ 30 Days (switcher) with an eye to hide it, AUM, Slots left (🔥 80/100); grey footer: Monthly charges ₹0 ~~₹300~~, Invest now (primary). The card itself isn't tappable (it holds buttons).
- **Pre-build Strategies** (Explore): underlying pill (Nifty 50 / GOLD ⇕ → sheet), divider, Bullish / Bearish / Neutral / Volatile; rail of cards — Probability of profit, strategy name, Funds Req, Max Profit (Unlimited or ₹) / Max Loss, payoff sketch (loss area left, profit area right).
- **Quick Trade**: ⚡ Quick Trade · Beginner friendly; “Which way will GOLD ⌄ move?” (underlying → sheet); Up • Bullish (green outline) and Down • Bearish (red outline).
- Destinations outside this prototype (Explore, Apply, Invest now, Learn, Up / Down) open the explanatory sheet.

#### “What does illiquidity mean?” sheet (shared)

`sheets/IlliquidSheet` — one explainer for every illiquid entry point in F&O: the ⓘ in the option-chain tooltip, and a tap on any ILLIQUID tag (asset page, Buy / Sell sheet, Gold Summary card). Same pattern as DASH's Pine Script sheet: small header (“What does illiquidity mean?” + “{contract} is illiquid right now”, or a general line from a tag), a card with three icon + one-line points (very few people trade it · buy and sell prices are far apart, which increases chances of slippage · Lemonn doesn't allow orders, to protect you), Got it.

#### Commodity options order pad (fno-25 … 31)

`order-pad/screens/OrderPad` (Figma 8671:18433) — **commodity option chain only**; other order pads (equity, futures) differ a little and get their own. Opened from Buy / Sell on the commodity asset page and in the Gold Summary Buy / Sell sheet; Back returns there.
- Actionbar: back · “Gold ⇕ 5 OCT Fut” over price + change (contract switch) · MCX; **Delivery / Intraday** tabs in its bottom slot.
- **Market / Limit / SL** pills; Limit and SL add the validity pill (**Day ⇕** → Day / IOC).
- **Sell** only: Margin · Leverage grey strip.
- **Quantity ⇕** (switches to Lots) · “(100 = 1 Lot)” · compact stepper in steps of one lot (grey −, blue +, as in Figma).
- **Limit**: a limit price row (price + % stepper from the market price); **SL**: a Trigger Price row above it.
- **Set TPSL ⊕** (right). **Intraday**: “This position will auto close by 11:30 PM” above the dock.
- Dock: Avail. ₹ · <u>Req</u> ₹ (Req opens its breakdown), then **Buy** (brand) or **Sell** (L3 sell, red). Placing shows a sample toast; no order is sent.
- Steppers are the L3 Stepper Small as the design system draws it (dark + / − on the grey track), not Figma's grey / blue.
- **ILLIQUID edge case** (`fno-32` Buy, `fno-33` Sell): should never be reached, but if an illiquid contract slips through — ILLIQUID tag in the header, the blocked note in the dock, Buy / Sell disabled (see docs/ILLIQUID.md).
- Data: `order-pad/data.ts` (contract, lot size, margin / leverage, funds, auto-close time, validities).

#### Buy / Sell sheet (fno-23, 24)

`commodities/sheets/ContractSheet` (live app, 2026-10-29): any futures or option card on Gold Summary opens it. Name › (asset page) · price; expiry · type · change; Buy (brand) / Sell (secondary) docked. **Illiquid** (commodities, product rule — same from any entry point): ILLIQUID tag in the sheet, Buy / Sell greyed out with “Trading is not allowed as this contract is illiquid”; only the name › (→ the illiquid asset page) or tapping outside work. The card itself also carries the ILLIQUID tag — an edge case kept in development (illiquid contracts aren't meant to be listed in discovery, but can still reach a list). Sample: GOLD 24000 CE.

#### Commodity asset page (fno-21, 22)

`commodities/screens/AssetPage` (Figma 6754:61613), data `AssetPage` in `commodities/data.ts`:
- Actionbar: back · ☆ (watchlist, toggles). Head: name + contract (“Gold MINI 5 OCT Fut”), price + change, commodity art.
- Chart (the Scalper's trading pane: candles, price axis with last-price tag, high / low, zoom, time axis, 5m) and the tool row Range · 5m Interval · Indicators · Drawings · Settings; Option chain (→ fno-17) and ScalpPro (→ Scalper fno-05) side by side (Figma 6754:62688: two Secondary, 40 tall, light outline). ScalpPro is disabled for an illiquid contract; tapping it shows the illiquid tooltip (as in the option chain: tap only, 5 s, ⓘ → the illiquidity sheet).
- Contract Info (key–value rows with dashed separators: days to expiry, margin, leverage, price unit; the tender-margin notice with ⓘ); {NAME} Futures rail; Performance (24H low / high bar with the last traded price, Prev. Close / Open / circuits / tick size / price unit); Trading details; Market Depth (bids | asks, totals). Buy (brand) / Sell (secondary) docked.
- **Illiquid (commodities only, product rule):** ILLIQUID tag (error, secondary) next to the name, Buy / Sell disabled, and “Trading is not allowed as this contract is illiquid” above them — whatever the entry point.
- Entry so far: the contract name in the option-chain order dock (“25,400 Put ›”). More entry points (Gold Summary cards, search, watchlists) to come. Equity contracts get their own, similar page.

#### Option chain (fno-17 … 19)

How option chains behave (Sensibull, Dhan, Zerodha, the live Lemonn app) and how this one does it:
- **Layout:** strikes ascending down the page in a grey middle column; calls on the left, puts on the right. Each side shows the chosen metric (LTP by default) with the day change under it.
- **Spot:** a black pill (“25300.40 +5.56%”) on a thin band between the two strikes the spot falls between; the chain opens scrolled so the pill is in the middle (at the money). Calls above it / puts below it are in the money.
- **OI bars:** a 2px line on each row's bottom edge — call OI in red running left from the middle, put OI in green running right, scaled to the largest OI in the chain.
- **Strike tags:** OI Support (the strike below spot with the most put OI, green), OI Resistance (above spot with the most call OI, red), Max Pain (blue, the stats row's value).
- **Selecting:** tap a call or put price → selected to **Buy** (green B badge on the strike side, green wash from the outer edge) and the order dock rises. Tap it again → **Sell** (red S badge, red wash, Sell button). A third tap clears it. Tapping another price moves the selection there (as Buy).
- **Order dock:** B / S + “25,400 Put ›” (contract details) · “Set Limit • TP/SL ›”; Balance and Req (buy = premium × quantity, sell = margin per lot); quantity in lots (L3 Stepper, steps of one lot, “1 lot”); Buy (brand lime) or Sell (secondary). Placing shows a success toast and clears the selection — no order is sent.
- **Top:** back (→ F&O home) · ribbon “Option chain” · Add more strategies (+); BankNifty ▾ (underlying sheet) | Expiry: 09 Oct ▾ (expiry sheet), Zing signals tile with count; Σ (Greeks: shows Δ instead of the day change) · basket · PCR • Max Pain • ATM IV; column heads: “Call LTP” / “Put LTP” (metric sheet: LTP, OI, OI Chg, IV), “All” (strike range: all, ±5, ±10 around the spot). Changing underlying or expiry clears the selection.
- **Illiquid contracts** (`quote.illiquid`; here deep in-the-money calls 24,700–24,900 and far out-of-the-money puts 25,700–25,900): a block icon (Material `block`, content/tertiary) beside the price on the strike side, as in Groww. Unlike Groww, a tap never selects them: an L3 Tooltip grows out of the block icon (fade + scale from its arrow), above or below to fit — two lines: “Illiquid contract” (label) over “Can’t be traded” (secondary), then ⓘ — on a tap only (never hover or focus). It closes by itself after 5 s, when another contract is tapped, on tap-away or Esc. ⓘ opens the shared `sheets/IlliquidSheet` (see “What does illiquid mean?” below).
- **Entry:** Option chain on the F&O home chart (all product tabs), the Option Chain bottom-nav tab, and View option chain on Gold Summary.

Differences: lot size 35 (BankNifty) so the stepper starts at 35 / 1 lot (Figma's “10000 · 91 lots” is placeholder); quotes are computed sample values (Figma repeats 292.15 / 25100); the stepper is L3 Stepper Large (Figma draws a bordered box with round ± buttons); Max Pain 25,400 so its tag sits where Figma draws it. L3 gaps: an option-chain row / table (strike column 107, row 54, dock header 44 → local tokens `--app-size-chain-*`), B / S order badges, OI bars.

### L3 components

Scalper: Screen, Button (ghost, tertiary, brand, secondary), Tabs (ribbon, pill group), Stepper, BottomSheet,
ListCell (card, Small), SideNav, Icon, Stack. New here, from L3 tokens only:
- **Side nav** — now L3 `SideNav` 1.0.0 (added to the design system from this sheet; was a flow copy).
- **Trading pane** (`components/TradingPane`) — L3 gap: L3 Chart is a fixed 360 × 200 picture without high / low
  markers, zoom, a timeframe control or a real-size price axis.

Screen and Rail are shared app composition helpers. The F&O header matches Stocks home in its profile, search, DASH and wallet controls; other controls use BottomNavbar / NavIcon, Button, Card, Tabs (including the explicitly requested Ribbon), Select, Chart, PriceChange, Tag, SectionHeader, BottomSheetHeader, Radio, TextField, EmptyState and Aerobar. Layout uses Stack and Inset. CSS uses semantic L3 tokens, including profit/loss heatmap surfaces.

### Differences and prototype limits

Scalper vs the live screenshot: L3 sizes win where they differ — the order buttons are L3 Medium (40, the live app's
are 35) with radius 16; the sheet's top corners are L3's 24; type is Manrope (L3), a little wider than the live app's,
so the tool row reaches the Active chip slightly later. The Zing glyph on Active and the Zing tile is Material
swap_horiz (L3 has no Zing mark icon). Colours map to the nearest L3 tokens (panels surface/primary #161616 vs the
live #1d1d1d).

The source uses old D2 controls alongside L3; their code equivalents are L3 components rather than hand-built lookalikes, including L3 shortcut buttons. The header matches Stocks home, including its search pill, DASH entry and wallet. The profile uses the app's fictional Rohan Mehta instead of AG. The misspelled watchlist name “Specail 25” is corrected to “Special 25”. Chart candles are representative data rendered by L3 Chart; chart metrics and data are illustrative, with no market/API or order execution integration. Repeated Figma quotes, historical expiry text and the red/green JSWSTEEL pattern are preserved, including the source's inconsistent negative percentages in green cells. The product tabs match Figma exactly (approved exception to L3 Ribbon): grey row, green baseline (local token `--app-fno-tabs-baseline`, green 300), Label/12, and the selected tab's success-green outline over a green-50 → white wash. The Zing signals card matches Figma too: flush with the left edge, open on the left, honey outline (border/accent/zing) and a honey-50 → white wash, content left-aligned.

#### Commodities & Strategies vs Figma (6754:63073)

- D2 parts → L3: section titles → SectionHeader (View all / Explore), D2 pills → Tabs pill / Tab action, the asset list cards → ListCell Small inside a bordered group, D2 tabs → Tabs underline (sheet header bottom slot, Actionbar bottom slot), card buttons → Button, D2 tags → Tag, card shells → Card (footer / footerFilled for the grey strips).
- Commodity shortcut buttons match Figma exactly: 52 white circles with a light outline, 32 art (L3 Tertiary button overridden; local token `--app-size-commodity-shortcut`). Figma's faint glow is dropped: L3 buttons have no drop shadow.
- Card footer buttons (Zing Trades, Smart Invest) and Quick Trade stay Small / Medium as in Figma, not the app's Large default — the user asked for the same UI as the frames.
- Price changes show their sign (“+0.10%”, L3 PriceChange); Figma shows “0.10%”.
- Figma's “Gold Gunia” tab → Gold Guinea; “1,65,4500.23” margin → 1,65,450.23; western “₹186,456” → ₹1,86,456; “ViewAll” → View all.
- The Zing trader photo is replaced by initials (fictional trader); the Smart Invest logo by the basket's initials.
- Equity (8) in the picker lists 8 indices (Figma draws 6). Copper, Aluminium and Zinc have no artwork yet, so their chips and rows show the name only.

#### Scalper position and breakeven vs Figma

- Pills, Exit and Add Trail are 24 tall (L3 Secondary Small resized to sit on the pills, as in Figma), not Large.
- Figma's rail (Bolt · Indicators · Drawings · Settings) is the live app's six groups here; its chart-type cards read
  "Line, Heiken Ashi, Line" — built as Candles, Heikin Ashi, Line.
- How breakeven works: Figma's explainer is a video fill (11802:369) whose export holds only the intro; the loop
  (chart + intro) is rebuilt from the designer's screen recording, measured frame by frame (theme-aware, no video
  file). The recording's labels are ~11 px; here they're L3's 12 styles (Label/12, Description/12, Label/14), so text
  runs ~8 % wider. Its orange (charges zone, B/E line and tag) isn't L3's warning (a yellow) — kept as local tokens.
  The zoomed-in charges (3 s, before the B/E line, which now draws after the zone instead of before it) aren't in
  Figma or the recording: added from the designer's brief with the F&O options rate card; everything after is the
  recording's timing moved 3 s later.
- Figma's breakeven marks and the Auto TP/SL mark couldn't be downloaded (asset links fail here), so they're drawn in
  SVG on L3 tokens to match (`BreakevenIcon`, `AutoTpSlIcon`).
- The explainer card's stage keeps the sheet's 24 gap (L3 Stack has no 20; Figma 20).
- Figma's entry tag reads 119.20 and B/E 13.86 (placeholder numbers); here they're worked out from the sample position.
- The charts tick (prototype): every second the last candle's close steps (a random walk pulled back to the sample
  price), its high / low stretch, and every 15 steps a new candle opens and the oldest drops off (`useLiveInstrument`).
  The header price, change, %, the last-price tag (green up / red down) and the entry pill's live P&L follow. In the
  app this is the market feed.
- Candles are at most 4 wide, however few there are. With a position open the option chart shows the 19 candles since
  the 13:55 spike with 8 empty slots after them (Figma: the candles stop about three quarters across).

#### L3 gaps (Scalper position and breakeven)
- An expandable key-value row (a row that opens a breakdown under it, e.g. order charges): built from KeyValueRow with a button label stretched over the row and a breakdown panel (`BreakevenSheet` `ChargesTable`). And a table / calculation layout (compact rows on a surface card): local CSS on KeyValueRow.

- No chart overlay parts: position pill (handle · tag · P&L · ✕), price lines, axis tags, the boxed B/E chip.
- No breakeven / Auto TP/SL icons; no overline text style ("INTRODUCING": heading-12 + `--app-overline-tracking`).
- No "button with a loader" (a locked button that unlocks after a timer): drawn as a track over L3 Button.
- Motion timings for the Auto TP/SL mark (`--app-auto-tpsl-loop`, `--app-auto-tpsl-ease`) and the breakeven explainer's
  sequence (`--app-be-*`; the chart's own timeline is in `BreakevenExplainer`): L3 has no stagger / sequence timings.
- No chart callouts (a white pill with a notch / tail pointing at a point, the LTP bubble) or chart zones; no orange
  accent (`--app-be-charges-zone`, `--app-be-orange`, `--app-be-orange-text`, `--app-be-tag`) and no green 100 semantic
  (`--app-be-profit-top`).
- Stack has no 20 gap.

#### Zing signals vs Figma (6900:23853)

- Old design system → L3: chips are L3 pill tabs, Medium (32 tall, 8 padding, Label/12 — Figma's size); the filter
  button is a Tertiary Small button made round; tags are L3 Small tertiary tags; View is L3 Small primary, 60 wide as
  in Figma.
- The filter follows the Scalper's Settings sheet (user's call, 20 Nov), not Figma 6900:28736: it takes the signals
  sheet over in place (Figma stacks it), L3 Side nav tiles at their own size (Figma 78 × 68), the white panel (Figma
  grey), 48 rows (Figma 44), 412 + picks + dock tall (Figma 492). Kept from Figma: the picks strip and the black Apply.
- The tooltip is Figma's (6900:31347): L3 Tooltip in the discover blue, white Label/12 on one line, pointing at Your
  filter. L3's tooltip is dark with Description/12 — L3 gap: no discover tone.
- Figma keeps All Signals selected after Apply; here Your filter is selected, so the list shows what the filter picked.
- The side tab's count is the number picked in that group (Figma shows a red "1" for two picks), in L3 Side nav's corner
  flag colour (blue).
- Figma's "← All Signals" back arrow is left out: L3 gives the first sheet over a screen no back button.
- Sample data made consistent across frames: Booming Bulls trades on SENSEX (Figma shows it as NIFTY, Gold and SILVER
  100 in different frames), so the Sensex and Indices filters have something to show; no signal is on a commodity yet,
  so Commodity shows the empty state. Prime scalper EMA has no win rate (Figma shows its P&L), so Win rate filters leave
  it out. Counts are computed (Figma's "Win rate ≥ 50% (1)" reads 2 with these signals).
- The lemon mascot avatar is rendered from Figma's vector parts to a 128px PNG (`assets/signals/lemon.png`); Figma
  only exports the component at 16. Neeraj's photo and the Booming Bulls logo are Figma's images.

#### L3 gaps (Zing signals)

- No dividers inside a Tabs row: Figma's separators between the filter button, the main chips and the market chips are
  one hairline after the filter button here.
- No removable (input) chip: the picks over Cancel / Apply are Secondary Small buttons with a ⊗ icon; Your filter's ✕
  is an icon inside the pill tab, caught by where the tap lands (the tab's press layer covers its icons).
- Side nav has no count badge, only the corner flag.

#### L3 gaps (Commodities & Strategies)

- Avatar has no borderless option: fno-38 hides its 1px edge locally (`.calendarAvatar`).
- Commodity art: no images for the base metals (Zinc, Copper, Aluminium, Lead); fno-38 shows L3 Avatar initials until art exists.
- Expiry calendar: L3 has no calendar / date-grouped list (Steps is a progress list). fno-38 draws its own date column (weekday + date in one grey block) and the hairlines between a day's rows with L3 tokens (`.calendar*` in `Commodities.module.css`).
- Card action footer spacing: the unfilled footer sits 12 under the body (the body's padding) with no prop to change it; the Expiring cards want 16, so `Commodities.module.css` adds 4 on top of the footer (`.expiryCard`).
- Card action footer hover: L3 greys only the tap body on hover, so details and buttons read as two parts; the Expiring cards grey the whole card (`.expiryCard` in `Commodities.module.css`).
- No-shadow clickable cards: L3 gives every clickable Card / card ListCell elevation-soft with no prop to turn it off; F&O wants all its cards flat (border only), so every F&O screen carries `flatCards.module.css` (Screen className), which keeps only the 1px border.
- Commodity artwork (L3/Image/Commodities/… in Figma) isn't in the code package — exported PNGs live in `commodities/assets`; Copper / Aluminium / Zinc missing.
- Outlined Buy / Sell buttons (Quick Trade): L3 Button has filled Buy / Sell only; the flow tints Secondary with the up / down tokens.
- Payoff sketch on strategy cards: no L3 mini payoff chart; drawn as a small SVG on L3 tokens.
- Weekday result dots (Zing Trades): no L3 component; 16 circles on the up / down light surfaces.
- Date strip (Expiring This Week V4): L3 has no date picker / day strip; drawn from buttons on L3 tokens (`.dayPicker*` in `Commodities.module.css`), with a hand-made edge fade (mask) and the turned week pill at 8 (`--l3-text-label-08` / `--l3-font-size-local-08`; L3 has no 8 description or caption style).
- Section header with a leading-icon View all: L3 SectionHeader's `view-all` takes only a chevron after the label, so Expiring This Week puts a Ghost Small button (calendar icon left) beside the header (`ExpiringHeader`).
- Divider: L3 has no divider component or border-width token; the month line on fno-38 is a 2 border-top with the local token `--app-week-divider`.
- Section header size: L3 SectionHeader's title is heading-14 with no size option; fno-38's month titles are set to heading-20 locally (`.calendarMonthHead h2`).

### Changelog
- 24 Nov 2026 — Zing signals: no shimmer on nudge strip 4 (Rotating facts).
- 24 Nov 2026 — Zing signals: the nudge strip animates out when switched off (tucks back behind the card) and comes out at once when switched on with the sheet up.
- 24 Nov 2026 — Zing signals: nudge strip gradient from Figma 6947:45037 — warm top-left corner fading across, and a gold ring round strip and card.
- 24 Nov 2026 — Zing signals: Rotating facts turns every 5 s (was 3), the picture comes in with its line, the move line has a trend arrow; the glow only under the gold bars.
- 24 Nov 2026 — Zing signals: nudge strip 4 (Rotating facts) adds the trending line with the flame.
- 24 Nov 2026 — Zing signals: the All · Index · Stocks · Commodities tabs are removed; the sheet starts with the filter button | chips and a line under them.
- 24 Nov 2026 — Zing signals: the Commodity signals versions are removed; the sheet keeps the segment tabs and the commodity logo tag, and the nudge strip versions are its only setting.
- 24 Nov 2026 — Zing signals: Commodity nudge strip (Figma 6946:42446) — a strip over commodity cards with an entry slide and a shimmer; four versions + Off (setting, S0 … S4 bubble). L3 gaps: no text token on the zing / orange light tints (honey 800), no shimmer highlight, no 29 glow size.
- 24 Nov: Equity shortcuts copy Figma 6754:62886 — Analysis · IPO · Watchlist · Referral, 40 discs (surface primary, 1px subtle edge, soft glow) with Figma's two-tone green icons (assets/shortcuts), no card round each. Commodities shortcuts back in one row of four (their own Inset + 4-column Grid). FLAG (L3 gap): the disc glow is raw; the two-tone icons are artwork, not L3 icons.
- 23 Nov 2026 — F&O sub-nav (floating V2): the chosen F&O icon is black and white, like the main nav's.
- 23 Nov 2026 — Home shortcuts (Trade Calls · Watchlist · Smart Invest · Referral) drawn as the Stocks Home's: 40 circles with a green-edged wash and green icons (lightbulb, bookmark, smart toy, redeem — Home's icons for these features), names in secondary text, via the new shared part src/shared/ui/ShortcutCircles. The old outlined tertiary buttons and their SVG art are no longer used (assets kept).

- 2026-11-24 — Expiring This Week V4: the day count tag is removed; date cards 10 apart, 8 more before each week pill. V2: one card per contract or event (8 apart), days 16 apart.
- 2026-11-24 — Commodity calendar (fno-38): the week-section view is archived; the page is the month and day list again, one card per contract or event (8 apart), days 32 apart, month titles at 20 (12 above and below, sticky), a 2 line edge to edge between months (24 above and below). Expiring This Week V4: the selected day's contracts and events are separate cards too.
- 2026-11-24 — Expiring This Week Version 4 (now the default): a day picker over the next month (week pills “NEXT WEEK” / “7 DEC”, edge-to-edge row with fading ends, a count tag on each day) and the selected day's card. In V4 the calendar page (fno-38) shows week sections (“November 23 – 29”) each with its own day picker, a 2 line edge to edge between them.
- 2026-11-24 — Expiring This Week: View all has a calendar icon before its label (all versions); real MCX data everywhere — the “Calendar days” sample weeks are archived (`commodities/archive/expiryPreviewSamples.ts`). Calendar event icons are content/primary.
- 2026-11-24 — Commodity shortcuts: the faint glow is dropped (L3 has no drop shadow on buttons).
- 2026-11-24 — The Diwali search bar is archived (`src/shared/ui/archive/DiwaliSearch.tsx`); the F&O home's search pill is plain again.
- 2026-11-20 — Zing signals: the sheet is 75% of the screen's height (Screen is a size container, cqh).
- 2026-11-20 — Zing signals: under the tabs' All, more chips (Nifty, Sensex, F&O Stocks, Commodities); version 7's header has no line and a shadow once the list scrolls.
- 2026-11-20 — Zing signals: version 7, Header with tabs (Active signals + Total P&L in the sheet header, tabs and chips under it).
- 2026-11-20 — Zing signals: Commodity signals is a dropdown; a floating V1 … V6 bubble on the signals sheet screens (phone). Preview: a quick switch can set its starting spot (`quickSwitch.spot`).
- 2026-11-20 — Zing signals: signal cards get a smooth drop shadow (L3 elevation low + soft).
- 2026-11-20 — Zing signals: strategy names in text primary; grey tags (market, win rate) in text secondary; Commodity picture's tag grey.
- 2026-11-20 — Zing signals: grouped list removed; Logo on avatar's tag is the name alone; no icon on the Commodities tab; Commodity picture puts the logo on a circle (colour per commodity, or grey — new setting).
- 2026-11-20 — Zing signals: segment tabs 16 below the top edge, 16 from their text to the line and selected bar.
- 2026-11-20 — Zing signals: Segment tabs get 20 above them and chips per tab (Index: Nifty · Sensex · Bank Nifty; Stocks: Win rate ≥ 50% · ≥ 25%; Commodities: Gold · Silver · Crude Oil · Natural Gas); unpicked chips in text secondary; versions 6 (logo tag, no tabs) and 7 (commodity picture); sample feed adds Bank Nifty and Natural Gas signals.
- 2026-11-20 — Zing signals: the sheet is 512 tall (under 60% of the screen), the list scrolls inside it.
- 2026-11-20 — Zing signals: Segment tabs (version 5) is the default.
- 2026-11-20 — Zing signals: five ways to tell commodity signals apart (setting "Commodity signals"); sample feed adds Gold, Crude Oil and a Reliance signal.
- 2026-11-20 — Zing signals: the sheet keeps Figma's height with one or two signals; the saved-filter tip in Figma's blue, pointing at Your filter.
- 2026-11-20 — Zing signals filter in the Scalper's Settings sheet look (side nav, white panel, title row, 48 rows, tinted chosen radio); list area 412, picks strip and black Apply kept.
- 2026-11-20 — Zing signals filter to Figma 6900:28736: 492 tall, Figma side tabs and spacing on the secondary panel, the picks strip as Figma's pills, Apply primary (black).
- 2026-11-20 — Zing signals filter on the chart tools sheet's layout (side nav, Heading/16 title row, card rows, Cancel / Apply dock), in place of the stacked sheet.
- 2026-11-20 — Zing signals: chips at Figma's size (L3 Medium pills, 32 / Label/12), round filter button and picks, View 60 wide, side tabs and sheet heights as Figma; the filter sheet opens inside the phone on desktop (it covered the whole page).
- 2026-11-20 — Zing signals sheet (fno-39 … 47) from Figma 6900:23853, in L3, light and dark: the Active chip on the Scalper opens it; quick chips, signal cards, the filter sheet (Indices · Win rate · Call/Put · Strategies) and the saved "Your filter".
- 2026-11-17 — Expiring This Week: events card third in the rail (EIA natural gas storage today on NATGASMINI: outlook, ATM option, margin — like the other cards; the readings stay on the calendar); the calendar's gas report moved to today with the same readings.
- 2026-11-17 — Event assets: the arrow tags are the only version; the earlier cards (Bullish / Bearish over the name) and the "Event assets" setting are archived (removed).
- 2026-11-17 — Event assets: one per commodity (no Mini alongside the full size); natural gas storage moves Natural Gas, Crude Oil; crude inventories Crude Oil, Natural Gas, Gold.
- 2026-11-17 — Event assets Version 2 (default): L3 Tags with an up / down arrow and the asset; the cards are kept as Version 1.
- 2026-11-17 — Expiry calendar: the body slides with the tabs (tap or swipe), like Market's tabs.
- 2026-11-17 — Event rows: country (US), impact tag and the how-it-moves line removed; no buttons; "Moves …" is now one small card per asset (Bullish / Bearish over the name, radius 8, scrolling row, tap → asset page); an event can move several assets.
- 2026-11-17 — Expiry calendar: All · Options · Futures · Events tabs with icons (All default); Events = the EIA crude and natural gas reports with time (IST) · country, impact, previous / forecast / actual, how it moves prices and what it moves; futures rows have ScalpPro only; option chain (→ option chain page fno-17) left, ScalpPro right; Option chain's back now returns to the page it was opened from. ScalpPro anywhere in F&O now opens the Scalper as a new page (in from the right) and its back returns to the page it was opened from.
- 2026-11-17 — Commodities: View all on Expiring This Week opens a new Expiry calendar (fno-38): Options / Futures tabs, expiry days (weekday + grey date pill) each with one card of contract names (several per day), each row with the commodity's icon (Avatar 24), its name, and ScalpPro and open-contract icon buttons.
- 2026-11-17 — Commodities: new Expiring This Week section between the shortcuts and the chart (sideways contract cards: symbol over its option expiry day, trend, ATM premium and margin per lot as label-over-value columns, ScalpPro + Buy in a grey footer; card → asset page fno-21; art hidden). Product tabs stick under the top bar on scroll (their row then takes the top bar's colour). The trend read-out is one shared component (`TrendBadge`) in the chart header and the Expiring cards. Expiring cards: option and future variants (a GOLDM future second for testing); the expiry as plain text under the symbol (no Tag); trend “Since” at 12 (the chart keeps 10) with the info (eye) icon after it, content-secondary; buttons without the grey strip, the card's three parts 16 apart; card → asset page fno-21; “Expiring card buttons” setting hides the button footer. All F&O cards lose their shadow (border only).
- 2026-11-16 — Breakeven sheet Version 2 (default): heading What is breakeven price? + a description, the charges table, info lines hidden; Version 1 (the first sheet) kept behind the new F&O setting "Breakeven sheet".
- 2026-11-16 — The three breakeven screens are named “Break Even · …” in the screen list (fno-35, fno-36, fno-37), so a search for break even finds them; the sheet's heading stays How breakeven works.
- 2026-11-16 — How breakeven works: a charges table under the example (bought at, order charges incl. GST, breakeven price in bold, one line each, on a grey card); the charges row opens the breakdown. GST now counts in the example: order charges ≈₹0.26, B/E ₹100.30 (was ≈₹0.24 / ₹100.25).

- 2026-11-04 — How breakeven works V2 (F&O setting "Breakeven explainer", V2 by default; V1 kept): starts zoomed in, the line rises from the bottom to the buy at ₹100 with a blue ₹0 → ₹100 fill, the charges fill and merge into Order charges, then it zooms out true to scale (₹100 stays put, the chart shrinks down to ₹0 at the bottom): the ₹0.25 of charges a hairline on the blue ₹100, the run up 12% to Sold at ₹112, Net Profit. 10.25 s, then it stops.
- 2026-11-04 — V2 archived (`archive/BreakevenExplainerV2.tsx`) and the "Breakeven explainer" setting removed: V1 ships.
- 2026-11-04 — How breakeven works: the explainer plays once and stops on the finished chart (no loop, no intro); a tap replays it. The launch splash is hidden.
- 2026-11-04 — How breakeven works: the charges stack STT on top, then transaction, stamp duty, SEBI, and brokerage last at the bottom, so brokerage no longer sits on STT's band; they come in top down (brokerage last), its tag the small one.
- 2026-11-03 — How breakeven works: the Order charges tag shows the total (≈₹0.24).
- 2026-11-03 — How breakeven works: the charges in ₹ on the ₹100 buy (no %), no GST band, B/E ₹100.25 (a thinner charges zone); zooms in only 2×; "Order charges" stays a tag under the zone.
- 2026-11-03 — How breakeven works: before the B/E line the chart zooms in and the charges zone fills one band per charge (brokerage first at the bottom, then STT, transaction, GST, SEBI, stamp duty — F&O options rate card, heights by cost, each tagged with its rate), then zooms out to one zone, the tags stacking into its "Order charges" label; loop 15 s, button lock 9.3 s. Breakeven mark tile flat surface/inverted; the Scalper's ribbon tab has no outline.
- 2026-11-03 — Scalper charts: thin candles (max 4), the charts tick live, the last-price tag turns red on a down candle; TP line grey and SL line light red as in Figma C.
- 2026-11-03 — Scalper breakeven (Figma version C, Boxed chip): positions on the option chart with draggable TP / SL pills, Exit, Add Trail and the yellow breakeven line + chip (fno-35); the How breakeven works sheet, its 12 s explainer (chart building up to a sell above the breakeven line, then the intro) copied from the designer's recording, with the locked "I understand" (fno-36); the Auto TP/SL mark on Figma's exact easings; chart tools → Settings with Auto TP/SL, chart type, stop-loss preference and View on chart, Cancel / Apply (fno-37).

- 2026-11-02 — Diwali, final: the Garland splash and the Diwali search bar are what ship (both on by default; settings are now two switches). The Lanterns splash and the profile avatar's diya flip are archived (`src/shared/ui/archive/`). Spec for developers: `docs/DIWALI.md`.
- 2026-11-02 — Splash (fno-34): the launch splash as a page, listed first.
- 2026-11-02 — Diwali (App settings → Diwali, on by default for now): a Diwali splash, and the home's profile avatar flips to a diya twice (`src/shared/ui/Diwali`).
- 2026-11-02 — Diwali splash: a quiet night scene in L3 dark with "Happy Diwali" in gold, in two versions (Lanterns / Garland); the avatar's diya is now a lotus diya.
- 2026-11-02 — The splash lasts 1.5 s (was 2 s) and its logo rises in; the Diwali splash's art, lights and wish come in within it. Diwali *Diya flip*: Off / Profile / Search bar (default) — the search pill's icon and label slide up and fade out, and a diya and "Happy Green Diwali" slide up and fade in (held 3 s, twice, each time the home shows, once the splash starts leaving), with a slow sparkler round its edge whose sparks rise out of the edge and sink back in; here, beside DASH, the pill is too narrow for the whole wish, so it slides along once to show its end.
- 2026-11-01 — US MARKETS · LIVE banner on the Equity home (fno-01…04), under the quick actions and above the chart (teammate's design 9001:3). One tap target → US Stocks home, US tab (`stocks-09`). Equity only. Component `components/UsBanner`; flag is a static still (`assets/us-flag.png`) of the animated GIF; the sparkle stars are left out. L3 gap: no banner component, so a card-like button from L3 tokens (blue-900 background, `--l3-border-accent-discover-light` ring).
- 2026-10-29 — Commodity options order pad (fno-25 … 31) from Figma 8671:18433; asset page and Gold Summary Buy / Sell open it.
- 2026-10-29 — Illiquid explainer simplified (small header, three icon points like the Pine Script sheet) and shared: opens from the chain's ⓘ and from every ILLIQUID tag.
- 2026-10-29 — Buy / Sell sheet from Gold Summary cards (fno-23) with the illiquid state (fno-24: tag on the card and in the sheet, Buy / Sell disabled).
- 2026-10-29 — Commodity asset page (fno-21) with the illiquid state (fno-22); opened from the option-chain order dock's contract name.
- 2026-10-29 — Illiquid contracts in the option chain: block icon, tooltip instead of selecting, ⓘ details sheet (fno-20).
- 2026-10-29 — Option chain (fno-17 … 19) from Figma 11695:26269: chain with spot pill, OI bars and strike tags, Buy → Sell → clear selection, order dock; opened from the chart's Option chain button and the bottom nav.
- 2026-10-29 — Product tab switch: every home tab screen is one page (group `home`), so the header, P&L, indices and tabs stay put and only the content under the tabs slides in from the chosen tab's side (scrolls back to the tabs if they were scrolled away). Product tabs and the Zing card rebuilt exactly as in Figma.
- 2026-10-29 — Commodities tab (shortcuts, Gold chart, Popular commodities, Bullion / Energy / Metals heatmap, Smart Futures), contract picker sheet (Equity / Commodities), Gold Summary lot page (by price / by volume / margin per lot) and the Strategies tab (Equity / Commodities: Zing Trades, Smart Invest, Pre-build Strategies, Quick Trade) from Figma 6754:63073; product tabs now switch between the three.

- 2026-10-27 — Chart-tools sheet states from the live app: nothing on the chart (“Indicators” · search); some on the chart (“Indicators (N)” · bin · fx with the count · search, each one a blue row with ✕, several at once — tapping toggles, the sheet stays open); search (field in the title's place, results wrap, full height). Focus guide from DASH: dimmed sheet, Your indicators lit, one-line tooltip with ✕. Scalper top as the live light screenshot: grey header band, Zing ring on Add, tools spread with Active cut at the edge, one tools button per chart, “N ▾” at the chart's top-left, reset on the option chart; light mode greys (surface/secondary) the header, the band between the charts and the order dock (dark keeps black).
- 2026-10-27 — Chart-tools sheet uses L3 SideNav 1.0.0 (design system moved to 571a418); the flow's own copy is removed.
- 2026-10-27 — Scalper rebuilt from the live app's screenshot: measured layout, trading chart panes (price axis, last-price tag, high / low markers, zoom, time axis, timeframe), the tool row with the Active chip, the order dock, and the chart-tools sheet with a new Side nav.
- 2026-10-26 — Added Equity home and board positions, connected the F&O tab and existing flows, added local selectors, filters, watchlist creation and details sheets.
- 2026-10-26 — Reused the Stocks home header on F&O, including its scrolled surface and all four actions.
- 2026-10-26 — Added Scalper: an L3 workspace from the ScalpPro shortcut, with two intraday charts and order controls.
- 2026-10-26 — Added the Scalper chart-tools bottom sheet and Indicators list from the supplied reference.
- 2026-10-26 — Grouped the chart-tools list into Your indicators and Lemon indicators; linked DASH AI's View indicator
  action to the saved custom indicator in the open sheet.
- 2026-11-17 — Header: 48 tall (`--app-topbar-height`, like every navbar tab's Actionbar), and the wallet is the shared round `TopBarAction`.
- 2026-11-17 — Expiring cards: the trend read-out (Strong Uptrend / Downtrend, and the event card's Bullish, which gets the i) is one tap target over the whole top right and opens the new trend info sheet (trend + symbol and change, Dash's bullets, disclaimer, Analyzed by Dash, Okay).
- 2026-11-17 — Expiring This Week Version 2 (setting “Expiring This Week”): a short calendar of the first 3 entries on their days, events first; View all → fno-38. The calendar day (date block + card) is one shared part, `CalendarDay`, for fno-38 and the home.
- 2026-11-17 — Expiring This Week Version 3: the short calendar in one card, dates as its attached grey left column (`ExpiringCalendarCard`; `CalendarDate` / `CalendarEntry` split out of `CalendarDay`).
- 2026-11-17 — Prototype setting “Calendar days” for Expiring This Week v2 / v3: 3 today · 2 today + 1 tomorrow · 1 a day.
- 2026-11-17 — Calendar days: “2 today · 1 tomorrow” is the default.
- 2026-11-17 — Calendar today: on the calendar page (fno-38) today's date block is inverted (surface-inverted, content-inverted text) instead of ringed; the home's short calendar no longer marks today.
- 2026-11-18 — The profile avatar in the top bar has its 1px indigo ring back (only the user's profile; other avatars and logos stay borderless).
- 2026-11-19 — Break Even · How breakeven works: the example opens every play with the "Introducing Breakeven Line" intro (2.5 s, fading into the chart) — on open, on each loop and on a tap — then the chart, which holds 2.2 s and loops (it had stopped on the chart, the intro unreached, since 4 Nov). "I understand" unlocks when the chart first finishes (11.8 s).
- 2026-11-19 — Breakeven icon in the "Introducing Breakeven Line" intro matches Figma (11989:36412): Figma's own arrow (`assets/breakeven-tile-arrow.svg`, lime gradient) in a 48 tile, radius 12, 12 padding, a dark gradient with a soft lift at the top — and the same colours in light and dark mode (fixed base neutrals, not theme tokens).
- 2026-11-19 — Breakeven tag and line on the chart match Figma (11756:79332 / 79330) in light and dark: the line is solid 1px border/accent-warning-light (was a dashed warning line); the tag is boxed on all four sides (radius 4, 1px warning-light border, warning-light fill, Label/10 warning text, 16 tall), 8 left of the price axis (was flush, open on the right), with Figma's own info_outline (12) tinted in the text colour. All L3 theme tokens, so dark mode follows.
- 2026-11-19 — How breakeven works · example: the "B/E ₹100.30" chip on the animated breakeven line is now the chart's own "Breakeven" tag — text only, no price (warning-light fill and edge, radius 4, Label/10 warning text, 16 tall), in light and dark.
- 2026-11-19 — Breakeven sheet Version 2: the description under "What is breakeven price?" is gone (heading only). Copy `breakeven.descriptionV2` is kept, unused.
- 2026-11-19 — Breakeven sheet Version 2 heading: "What is breakeven line?" (was "What is breakeven price?").
- 2026-11-20 · Zing signals version 6 · Commodity picture now also carries version 2's amber "MCX · Gold" tag (was the commodity name in grey): the commodity's picture and the MCX tag together.


## Source — this flow

### `src/flows/fno/archive/BreakevenExplainerV2.module.css`

```css
/*
 * How breakeven works · the example (copied from the designer's recording). L3 tokens; the orange and the profit fade
 * are local tokens (src/local-tokens.css: the recording's orange isn't in L3). Positions come from BreakevenExplainer:
 * each callout gets its anchor as --x / --y and places itself around it.
 */
.stage {
  position: relative;
  overflow: hidden;
  background: var(--l3-surface-primary);
  cursor: pointer; /* a tap plays it again */
  -webkit-tap-highlight-color: transparent;
}

.chart {
  position: absolute;
  inset: 0;
  display: block;
}

/* ---- Price axis: ₹101–₹103 grey on dashed gridlines; ₹100 (the buy) bold on a solid line. ---- */
.gridline,
.baseline {
  stroke: var(--l3-border-light);
  stroke-width: 1;
}

.gridline {
  stroke-dasharray: 4 3;
}

.axisLabel,
.axisEntry,
.zoneLabel,
.chip,
.bought,
.sold,
.ltp {
  position: absolute;
  left: var(--x);
  top: var(--y);
  white-space: nowrap;
}

.axisLabel,
.axisEntry,
.zoneLabel {
  transform: translateY(-50%);
}

.axisLabel {
  color: var(--l3-content-tertiary);
  font: var(--l3-text-description-12);
}

.axisEntry {
  color: var(--l3-content-primary);
  font: var(--l3-text-label-12);
}

/* V2: what the buy cost (₹0 → ₹100), L3's light blue. */
.boughtZone {
  fill: var(--l3-surface-accent-discover-light);
}

/* ---- Zones: orange charges (₹100 → B/E), a green fade for the net profit (B/E → ₹102). ---- */
.chargesZone {
  fill: var(--app-be-charges-zone);
}

.profitTop {
  stop-color: var(--app-be-profit-top);
}

.profitMid,
.profitBottom {
  stop-color: var(--l3-surface-accent-success-light);
}

.profitBottom {
  stop-opacity: 0.4;
}

.zoneLabel {
  font: var(--l3-text-label-12);
}

.zoneLabel[data-zone='charges'] {
  isolation: isolate;
  display: inline-flex;
  gap: var(--l3-spacing-04);
  color: var(--app-be-orange-text);
}

/* "Order charges" is the tag the charge tags stack into (the same white pill, behind its text), under the zone. */
.zoneLabel[data-zone='charges']::before {
  content: '';
  position: absolute;
  inset: calc(-1 * var(--l3-spacing-02) - 1px) calc(-1 * var(--l3-spacing-06) - 1px);
  z-index: -1;
  border: 1px solid var(--l3-border-light);
  border-radius: var(--l3-radius-06);
  background: var(--l3-surface-primary);
  box-shadow: var(--l3-shadow-elevation-low);
}

.zoneLabel[data-zone='bought'] {
  color: var(--l3-content-accent-discover-default);
}

.zoneLabel[data-zone='profit'] {
  color: var(--l3-content-accent-success-default);
}

/* ---- The breakeven line and its chip (white, a B/E tag then the price), the chip's right edge on the plot's. ---- */
.breakevenLine {
  stroke: var(--app-be-orange);
  stroke-width: 1.25;
  stroke-dasharray: 4 3;
}

.chip {
  display: inline-flex;
  align-items: center;
  gap: var(--l3-spacing-04);
  padding: var(--l3-spacing-02) var(--l3-spacing-04) var(--l3-spacing-02) var(--l3-spacing-02);
  border: 1px solid var(--l3-border-light);
  border-radius: var(--l3-radius-06);
  background: var(--l3-surface-primary);
  box-shadow: var(--l3-shadow-elevation-low);
  color: var(--l3-content-primary);
  font: var(--l3-text-label-12);
  transform: translate(-100%, -50%);
  transform-origin: right center;
}

.chipTag {
  padding: 1px var(--l3-spacing-02);
  border-radius: var(--l3-radius-02);
  background: var(--app-be-tag);
  color: var(--l3-static-black); /* like L3's warning Tag: black on the solid, in both modes */
  font: var(--l3-text-heading-10);
}

/* ---- The price line, the buy dot, the ringed crossing marker, the green sell dot and their pulses. ---- */
.priceLine {
  fill: none;
  stroke: var(--l3-content-primary);
  stroke-width: 1.75;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.buyDot {
  fill: var(--l3-content-primary);
}

.crossingRing {
  fill: var(--app-be-charges-zone);
  stroke: var(--app-be-orange);
  stroke-width: 1.25;
}

.crossingPulse {
  fill: var(--app-be-orange);
}

.sellRing,
.sellRingDrawing {
  fill: var(--l3-surface-accent-success-light);
  stroke-width: 1.25;
}

.sellRing {
  stroke: var(--l3-border-accent-success-light);
}

.sellRingDrawing {
  stroke: var(--l3-border-accent-success-default);
}

.sellDot,
.sellPulse {
  fill: var(--l3-surface-accent-success-default);
}

/* ---- Callouts: white pills with a light edge and a soft shadow. ---- */
.bought,
.sold,
.ltp {
  border: 1px solid var(--l3-border-light);
  border-radius: var(--l3-radius-08);
  background: var(--l3-surface-primary);
  box-shadow: var(--l3-shadow-elevation-low);
}

/* "Bought at ₹100": under the buy dot, a notch on top pointing at it. */
.bought {
  padding: var(--l3-spacing-04) var(--l3-spacing-08);
  color: var(--l3-content-primary);
  font: var(--l3-text-label-12);
}

.bought::before,
.sold::after {
  content: '';
  position: absolute;
  width: var(--l3-spacing-08);
  height: var(--l3-spacing-08);
  background: var(--l3-surface-primary);
  rotate: 45deg;
}

.bought::before {
  top: calc(var(--l3-spacing-04) * -1 - 1px);
  left: var(--l3-spacing-16);
  border-top: 1px solid var(--l3-border-light);
  border-left: 1px solid var(--l3-border-light);
}

/* "Sold at ₹102": left of the sell dot, green edge and text, a tail pointing right at the dot. */
.sold {
  display: inline-flex;
  align-items: center;
  gap: var(--l3-spacing-06);
  padding: var(--l3-spacing-04) var(--l3-spacing-08) var(--l3-spacing-04) var(--l3-spacing-06);
  border-color: var(--l3-border-accent-success-light);
  box-shadow: none;
  color: var(--l3-content-accent-success-default);
  font: var(--l3-text-label-12);
  transform: translate(-100%, -50%);
}

.sold::after {
  top: calc(50% - var(--l3-spacing-04));
  right: calc(var(--l3-spacing-04) * -1 - 1px);
  border-top: 1px solid var(--l3-border-accent-success-light);
  border-right: 1px solid var(--l3-border-accent-success-light);
}

/* V2: the sell sits on a thin strip next to the B/E chip, so "Sold" goes above the dot (its right edge 10 past it), no tail. */
.sold[data-place='above'] {
  transform: translate(-100%, -100%);
}

.sold[data-place='above']::after {
  content: none;
}

/* LTP: rides the line's head, centred above it — the last price the line passed. */
.ltp {
  display: flex;
  flex-direction: column;
  padding: var(--l3-spacing-02) var(--l3-spacing-08);
  transform: translate(-50%, -100%);
  transform-origin: center bottom;
}

.ltpName {
  color: var(--l3-content-secondary);
  font: var(--l3-text-description-10);
}

.ltpValue {
  color: var(--l3-content-primary);
  font: var(--l3-text-label-14);
}

/*
 * The intro the loop ends on (the stage cuts to surface/secondary): Figma's reveal (the video on 11802:369, 1.23 s,
 * measured frame by frame) —
 * - the mark: opacity 0 → 1 from 30 ms over 250 ms (linear); scale 0.55 → 1 from 100 ms over 400 ms on L3's pop easing;
 * - INTRODUCING, Breakeven Line, the one-liner: from 300 / 470 / 670 ms, each 400 ms (L3 long): opacity 0 → 1 linear,
 *   8 up → 0 ease-out.
 */
.intro {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: var(--l3-spacing-24) var(--l3-spacing-16);
  background: var(--l3-surface-secondary);
  text-align: center;
}

.introIcon {
  margin-bottom: var(--l3-spacing-16);
  animation:
    fadeIn var(--app-be-icon-fade) linear var(--app-be-icon-fade-delay) both,
    popIn var(--l3-motion-duration-ai-pop) var(--l3-motion-easing-ai-pop) var(--app-be-icon-pop-delay) both;
}

.overline,
.introTitle,
.introText {
  animation:
    fadeIn var(--l3-motion-duration-long) linear var(--app-be-rise-delay) both,
    riseIn var(--l3-motion-duration-long) ease-out var(--app-be-rise-delay) both;
}

.overline { --app-be-rise-delay: var(--app-be-overline-delay); }
.introTitle { --app-be-rise-delay: var(--app-be-title-delay); }
.introText { --app-be-rise-delay: var(--app-be-tagline-delay); }

@keyframes fadeIn {
  from {
    opacity: 0;
  }
}

@keyframes popIn {
  from {
    scale: 0.55;
  }
}

@keyframes riseIn {
  from {
    translate: 0 var(--l3-spacing-08);
  }
}

/* INTRODUCING: 12 bold, tracking 0.96 (Figma) — L3 has no overline style: heading-12 + local tracking. */
.overline {
  margin: 0;
  color: var(--l3-content-tertiary);
  font: var(--l3-text-heading-12);
  letter-spacing: var(--app-overline-tracking);
  text-transform: uppercase;
}

.introTitle {
  margin: var(--l3-spacing-04) 0 var(--l3-spacing-08);
  color: var(--l3-content-primary);
  font: var(--l3-text-heading-24);
}

.introText {
  margin: 0;
  max-width: calc(var(--l3-size-128) * 1.75);
  color: var(--l3-content-secondary);
  font: var(--l3-text-label-12);
}

/*
 * Zoomed in, the charges (designer's brief, 2026-11-03): a tag per band — white like the B/E chip, the name then the
 * rate — joined to its band by an orange leader and dot.
 */
.chargeTag {
  position: absolute;
  left: var(--x);
  top: var(--y);
  display: inline-flex;
  align-items: center;
  gap: var(--l3-spacing-04);
  padding: var(--l3-spacing-02) var(--l3-spacing-06);
  border: 1px solid var(--l3-border-light);
  border-radius: var(--l3-radius-06);
  background: var(--l3-surface-primary);
  box-shadow: var(--l3-shadow-elevation-low);
  color: var(--l3-content-primary);
  font: var(--l3-text-label-12);
  white-space: nowrap;
  transform: translateY(-50%);
}

/* Brokerage's tag is the small one (designer's call: Lemonn's brokerage is a small part of the charges). */
.chargeTag[data-size='small'] {
  gap: var(--l3-spacing-02);
  padding: 1px var(--l3-spacing-04);
  font: var(--l3-text-label-10);
}

.chargeRate {
  color: var(--l3-content-secondary);
}

.leader line {
  stroke: var(--app-be-orange);
  stroke-width: 1;
}

.leader circle {
  fill: var(--app-be-orange);
}
```

### `src/flows/fno/archive/BreakevenExplainerV2.tsx`

```tsx
import { useEffect, useId, useLayoutEffect, useRef, useState, type CSSProperties } from 'react'
import { Icon } from '@l3/components/Icon'
import { msCheckCircleFill } from '@l3/icons/material'
import { inr } from '../../../shared/data/format'
import { t } from '../copy'
import { breakevenCharges, breakevenExample, exampleChargesTotal } from '../data'
import { BreakevenIcon } from '../components/BreakevenIcon'
import styles from './BreakevenExplainerV2.module.css'

/*
 * ARCHIVED 2026-11-04 — not in the app. V2 of the How breakeven works explainer (and V1, the version that ships, as it
 * was then). To bring it back: move this file and its CSS to components/ (as BreakevenExplainer), put
 * `breakevenExampleV2` back in data.ts, and add the F&O option `breakevenExplainer` (V1 / V2) that BreakevenSheet reads
 * with useFlowOption, passing `version` and `explainerLength(version)` for the button's lock.
 */

/**
 * V2 of the explainer, true to scale once it zooms out: ₹0 → ₹100 (the buy), the ₹0.25 of charges on it, and a 12% gain
 * to the sell at ₹112. `path` runs after the buy (`at` 0 → 1 of the plot after it).
 */
const breakevenExampleV2 = {
  entry: breakevenExample.entry,
  breakeven: breakevenExample.breakeven,
  exit: 112,
  axis: [100, 0],
  path: [
    { at: 0, price: breakevenExample.entry },
    { at: 0.1, price: 100.1 },
    { at: 0.2, price: breakevenExample.breakeven },
    { at: 0.36, price: 103.5 },
    { at: 0.48, price: 102.6 },
    { at: 0.66, price: 107 },
    { at: 0.76, price: 106 },
    { at: 0.9, price: 112 },
  ],
}

/**
 * The example in How breakeven works — copied from the designer's recording of the explainer (measured frame by frame),
 * plus the charges breakdown (designer's brief, 2026-11-03). A 15 s loop on a white stage:
 * 1. the price axis (₹100–₹103) and its dashed gridlines fade in; the buy dot pops in at ₹100 with "Bought at ₹100";
 * 2. the chart zooms in 2× on ₹100 → ₹100.25 (the charges are thin at the normal scale): ₹102–₹103 move up out
 *    of view and the charges zone fills one charge at a time, each a band as tall as its share of the charges, with a
 *    tag (name · ₹ on the ₹100 buy). Top down: STT, transaction, stamp duty, SEBI, and brokerage last at
 *    the bottom. They come in top down, so brokerage comes in last (₹0.02, a thin band, its tag the small one);
 * 3. it zooms back out: the bands close into one orange charges zone and the tags slide down under it, stacking into one
 *    tag that reads "Order charges" and stays under the zone; the breakeven line draws across its top at ₹100.25
 *    and its B/E chip comes in;
 * 3. an LTP bubble rides the price line as it draws up to ₹102 (showing the last price it passed); where it crosses the
 *    breakeven line a ringed marker pulses;
 * 4. at ₹102 the bubble goes, a green dot pulses, "Sold at ₹102" slides in and the green net-profit zone grows from the
 *    breakeven line up to the sell price, labelled "Net Profit"; it holds;
 * 5. it plays once and stops on the finished chart (at 9.3 s); a tap on it plays it again from the start.
 * (The recording looped on into an intro — the Breakeven mark, INTRODUCING, Breakeven Line, the one-liner — at 11.75 s;
 * kept below but not reached while it stops on the chart.)
 * `still` (reduced motion) shows the finished chart and no intro.
 */
export function BreakevenExplainer({ still = false, version = 'v1' }: { still?: boolean; version?: ExplainerVersion }) {
  const stageRef = useRef<HTMLDivElement>(null)
  const width = useWidth(stageRef, FIGMA_WIDTH)
  const [run, setRun] = useState(0)
  const played = explainerLength(version)
  const elapsed = useElapsed(!still, played, run)
  const loop = Math.floor(elapsed / LOOP)
  const time = still ? played : elapsed % LOOP
  const replay = () => { if (!still && elapsed >= played) setRun(run + 1) }

  return (
    <div
      ref={stageRef}
      className={styles.stage}
      style={{ height: HEIGHT }}
      role="button"
      tabIndex={0}
      aria-label={`${t(version === 'v2' ? 'breakeven.chartLabelV2' : 'breakeven.chartLabel')} ${t('breakeven.replay')}`}
      onClick={replay}
      onKeyDown={(e) => { if (e.key === 'Enter' || e.key === ' ') { e.preventDefault(); replay() } }}
    >
      <ExampleChart time={time} width={width} version={version} />
      {!still && time >= INTRO_AT && <Intro key={loop} />}
      {!still && loop > 0 && time < INTRO_OUT && <Intro key={loop - 1} fade={1 - ramp(time, [0, INTRO_OUT])} />}
    </div>
  )
}

/**
 * V1: the recording's order — the buy, zoom in for the charges, zoom out. V2 (designer's brief, 2026-11-04): it starts
 * zoomed in; the price line rises from the bottom of the chart to the buy at ₹100 ("Bought at ₹100") and a blue fill
 * rises under it to the ₹100 line (₹0 → ₹100, what the buy cost), the charges fill and close into one "Order charges"
 * zone, and only then it zooms out — all the way, true to scale (₹100 stays put, the chart shrinks down to ₹0): the blue ₹100, the ₹0.25 of charges
 * a hairline on it, then the B/E line, the run up 12% to "Sold at ₹112" and the green Net Profit.
 */
export type ExplainerVersion = 'v1' | 'v2'
type Timeline = Record<keyof typeof SHOT_V1, [number, number]>

/**
 * Where each part comes in: [start, duration] in ms (t = 0 is the chart starting on a blank stage). From the B/E line
 * on, it's the recording's timing moved 3 s later for the charges breakdown. `leadIn` (V2 only) is the line rising to
 * the buy; a start of -1 means already there at t = 0.
 */
const SHOT_V1 = {
  axis: [150, 250],
  leadIn: [-1, 1],
  boughtZone: [Infinity, 1], // V2 only
  buyDot: [400, 200],
  bought: [650, 150],
  boughtOut: [Infinity, 1], // V2 only
  boughtLabel: [Infinity, 1], // V2 only
  zoomIn: [1000, 500],
  chargeFill: [1550, 300], // the top band and its tag first; each one below CHARGE_STEP later, brokerage last
  zoomOut: [4100, 600],
  leadersOut: [4100, 150],
  zoneMerge: [4100, 600], // the bands close into one zone
  tagsMerge: [4100, 450], // the top tag first; each one below TAG_MERGE_STEP later
  tagsOut: [4600, 150], // the stacked tags cross-fade into the one "Order charges" tag under the zone
  chargesLabel: [4600, 150],
  breakevenLine: [4750, 450],
  breakevenChip: [5200, 200],
  ltpIn: [5550, 150],
  priceLine: [5800, 2150],
  crossingPulse: [120, 400], // after the line reaches the crossing
  ltpOut: [8000, 150],
  sellDot: [8000, 200],
  sellPulse: [8200, 500],
  sold: [8250, 150],
  profitZone: [8450, 550],
  profitLabel: [9150, 150],
} satisfies Record<string, [number, number]>

/** V2: zoomed in from the start; the line rises to the buy, the charges fill and merge, then it zooms out. */
const SHOT_V2: Timeline = {
  axis: [100, 250],
  leadIn: [300, 1100],
  boughtZone: [1400, 450], // the blue ₹0 → ₹100 fill rises from the bottom to the buy
  buyDot: [1400, 200],
  bought: [1600, 150],
  boughtOut: [4600, 150], // the callout hands over to the blue zone's own label (the Order charges tag takes its place)
  boughtLabel: [5600, 200], // zoomed out: "Bought at ₹100" inside the blue zone
  zoomIn: [-1, 1],
  chargeFill: [2000, 300],
  leadersOut: [4100, 150],
  zoneMerge: [4100, 450],
  tagsMerge: [4100, 450],
  tagsOut: [4600, 150],
  chargesLabel: [4600, 150],
  zoomOut: [5000, 600],
  breakevenLine: [5700, 450],
  breakevenChip: [6150, 200],
  ltpIn: [6500, 150],
  priceLine: [6750, 2150],
  crossingPulse: [120, 400],
  ltpOut: [8950, 150],
  sellDot: [8950, 200],
  sellPulse: [9150, 500],
  sold: [9200, 150],
  profitZone: [9400, 550],
  profitLabel: [10100, 150],
}
const SHOTS: Record<ExplainerVersion, Timeline> = { v1: SHOT_V1, v2: SHOT_V2 }
/**
 * V2's line before the buy: rising from the bottom of the chart to ₹100, in the plot's first 28% (the trade after the
 * buy takes the rest). It comes in from the left, above "Bought at ₹100", so the callout stays clear.
 */
const BUY_AT: Record<ExplainerVersion, number> = { v1: 0, v2: 0.28 }
const LEAD_IN: Record<ExplainerVersion, { at: number; price: number }[]> = {
  v1: [],
  v2: [
    { at: 0, price: 99.28 },
    { at: 0.06, price: 99.5 },
    { at: 0.1, price: 99.42 },
    { at: 0.15, price: 99.62 },
    { at: 0.2, price: 99.9 },
    { at: 0.28, price: 100 },
  ],
}
const CHARGE_STEP = 350
const TAG_MERGE_STEP = 30
const LOOP = 15000
/** How long one play takes (ms): it stops on the finished chart, its Net Profit label in. */
export function explainerLength(version: ExplainerVersion) {
  const { profitLabel } = SHOTS[version]
  return profitLabel[0] + profitLabel[1]
}
/** The hard cut to the intro, and how long the intro takes to fade when the loop starts again. */
const INTRO_AT = 11750
const INTRO_OUT = 200
/** The LTP value cross-fades for this long when the line passes a turn. */
const LTP_SWAP = 100

/** The plot, in px (measured at the card's 326 width in Figma; it stretches with the card). */
const FIGMA_WIDTH = 326
const HEIGHT = 286
const PLOT_LEFT = 53.5
const PLOT_RIGHT_INSET = 12.5
const AXIS_X = 12.5
const ZONE_LABEL_INSET = 8.5
/**
 * "Order charges" is a tag in the charge tags' column, 6 under the zone (its middle 17 under ₹100): the zone, ₹0.25
 * tall, is too thin to hold it. A tag's text starts 7 in (its 6 padding and 1 edge).
 */
const CHARGES_LABEL_DROP = 17
const TAG_TEXT_INSET = 7
/** Callouts around their dots: "Bought" hangs 12.5 below with its notch 20 in; "Sold" ends 10 left; LTP sits 8.5 above. */
const BOUGHT_GAP = 12.5
const BOUGHT_NOTCH_X = 20
const SOLD_GAP = 10
const LTP_GAP = 8.5
/** V2's green strip is too thin to hold its label: "Net Profit" sits 10 above it. */
const PROFIT_LABEL_ABOVE = 10
/** ₹100 sits at 209 and every rupee is 53 higher; zoomed in, 2× that (the charges zone twice its final height). */
const BASELINE = 209
const RUPEE = 53
const ZOOM = 2
const ZOOMED_RUPEE = RUPEE * ZOOM
const priceY = (price: number, perRupee: number) => BASELINE - (price - breakevenExample.entry) * perRupee
/**
 * V2 zoomed out, true to scale: ₹100 stays where it was and the chart shrinks down to it — ₹0 comes up to 12 above the
 * stage's bottom, so everything (the ₹0.25 of charges, the 12% to ₹112) is at that scale.
 */
const TRUE_ZERO_Y = HEIGHT - 12
const TRUE_RUPEE = (TRUE_ZERO_Y - BASELINE) / breakevenExampleV2.entry
const EXAMPLES = { v1: breakevenExample, v2: breakevenExampleV2 }
/**
 * Zoomed in, each charge is a band of the zone, as tall as its share of the charges (at least 2, so SEBI's ~0.1% still
 * shows; the rest shrink to make room), 1 apart. Their tags sit in a column 140 from the plot's right, at least 24
 * apart and 10 from the top, each joined by a leader to a dot 20 left of it at its band's middle.
 */
const MIN_BAND = 2
const BAND_GAP = 1
const TAG_COLUMN = 140
const TAG_SPACING = 24
const TAG_TOP = 10
const LEADER = 20
const BANDS = chargeBands()

function ExampleChart({ time, width, version }: { time: number; width: number; version: ExplainerVersion }) {
  const gradientId = useId()
  const SHOT = SHOTS[version]
  const { entry, breakeven, exit, axis, path } = EXAMPLES[version]
  const zoomIn = ramp(time, SHOT.zoomIn, easeInOut)
  const zoomOut = ramp(time, SHOT.zoomOut, easeInOut)
  // V1 zooms out to 1 rupee = 53; V2 all the way to true scale (on a log scale, so the 50× zoom reads as one move).
  const perRupee = version === 'v2'
    ? ZOOMED_RUPEE * (TRUE_RUPEE / ZOOMED_RUPEE) ** zoomOut
    : RUPEE + (ZOOMED_RUPEE - RUPEE) * zoomIn * (1 - zoomOut)
  const y = (price: number) => priceY(price, perRupee)
  const plotRight = width - PLOT_RIGHT_INSET
  const buyAt = BUY_AT[version]
  const plotX = (at: number) => PLOT_LEFT + at * (plotRight - PLOT_LEFT)
  const points = path.map((p) => ({ x: plotX(buyAt + p.at * (1 - buyAt)), y: y(p.price), price: p.price }))
  const leadIn = LEAD_IN[version].map((p) => ({ x: plotX(p.at), y: y(p.price) }))
  const leadInDrawn = leadIn.length ? lineTo(leadIn, ramp(time, SHOT.leadIn)) : []
  const start = points[0]
  const end = points[points.length - 1]
  const crossing = points.find((p) => p.price === breakeven) ?? points[0]

  // The price line draws at a steady pace across the plot; its head is where the LTP bubble rides.
  const drawn = ramp(time, SHOT.priceLine)
  const headX = start.x + drawn * (end.x - start.x)
  const passed = points.filter((p) => p.x <= headX)
  const next = points[passed.length]
  const last = passed[passed.length - 1] ?? start
  const head = next ? { x: headX, y: last.y + ((headX - last.x) / (next.x - last.x)) * (next.y - last.y) } : end
  const crossedAt = SHOT.priceLine[0] + ((crossing.x - start.x) / (end.x - start.x)) * SHOT.priceLine[1]
  const lastTurnAt = SHOT.priceLine[0] + ((last.x - start.x) / (end.x - start.x)) * SHOT.priceLine[1]

  const axisIn = ramp(time, SHOT.axis)
  const boughtZone = ramp(time, SHOT.boughtZone, easeOut)
  const zoneBottom = Math.min(y(0), HEIGHT)
  const profitZone = ramp(time, SHOT.profitZone, easeOut) * (y(breakeven) - y(exit))
  const ltp = ramp(time, SHOT.ltpIn, easeOut) * (1 - ramp(time, SHOT.ltpOut))
  const sellIn = ramp(time, SHOT.sellDot, easeOutBack)
  const chargeIn = (order: number) => SHOT.chargeFill[0] + (BANDS.length - 1 - order) * CHARGE_STEP
  const bandFill = (order: number) => ramp(time, [chargeIn(order), SHOT.chargeFill[1]], easeOut)
  const leadersShown = 1 - ramp(time, SHOT.leadersOut)
  const tagsShown = 1 - ramp(time, SHOT.tagsOut)
  const tagX = plotRight - TAG_COLUMN
  const labelX = tagX + TAG_TEXT_INSET
  const labelY = y(entry) + CHARGES_LABEL_DROP
  const tagMerge = (order: number) =>
    ramp(time, [SHOT.tagsMerge[0] + (BANDS.length - 1 - order) * TAG_MERGE_STEP, SHOT.tagsMerge[1]], easeInOut)

  return (
    <>
      <svg className={styles.chart} width={width} height={HEIGHT} viewBox={`0 0 ${width} ${HEIGHT}`} aria-hidden>
        <defs>
          <linearGradient id={gradientId} x1="0" y1="0" x2="0" y2="1">
            <stop offset="0" className={styles.profitTop} />
            <stop offset="0.6" className={styles.profitMid} />
            <stop offset="1" className={styles.profitBottom} />
          </linearGradient>
        </defs>
        {/* V2: what the buy cost, ₹0 → ₹100 — blue up from the bottom of the chart to the ₹100 line. */}
        <rect className={styles.boughtZone} x={PLOT_LEFT} width={plotRight - PLOT_LEFT} y={zoneBottom - boughtZone * (zoneBottom - y(entry))} height={boughtZone * (zoneBottom - y(entry))} />
        <g opacity={axisIn}>
          {axis.map((price) => (
            <line key={price} className={price === entry ? styles.baseline : styles.gridline} x1={PLOT_LEFT} x2={plotRight} y1={y(price)} y2={y(price)} />
          ))}
        </g>
        {/* The charges zone: the bands fill up one by one; zooming out, the whole zone fades in over them and closes the gaps. */}
        {BANDS.map((band, order) => {
          const top = y(band.from + (band.to - band.from) * bandFill(order))
          const height = Math.max(0, y(band.from) - top - BAND_GAP)
          return height > 0 && <rect key={band.charge.id} className={styles.chargesZone} x={PLOT_LEFT} width={plotRight - PLOT_LEFT} y={top} height={height} />
        })}
        <rect className={styles.chargesZone} x={PLOT_LEFT} width={plotRight - PLOT_LEFT} y={y(breakeven)} height={y(entry) - y(breakeven)} opacity={ramp(time, SHOT.zoneMerge, easeInOut)} />
        {leadersShown > 0 &&
          BANDS.map((band, order) => {
            const shown = ramp(time, [chargeIn(order), SHOT.chargeFill[1]]) * leadersShown
            const middle = y((band.from + band.to) / 2)
            return (
              shown > 0 && (
                <g key={band.charge.id} className={styles.leader} opacity={shown}>
                  <line x1={tagX - LEADER} y1={middle} x2={tagX} y2={band.tagY} />
                  <circle cx={tagX - LEADER} cy={middle} r={2} />
                </g>
              )
            )
          })}
        <rect fill={`url(#${gradientId})`} x={PLOT_LEFT} width={plotRight - PLOT_LEFT} y={y(breakeven) - profitZone} height={profitZone} />
        <line
          className={styles.breakevenLine}
          x1={PLOT_LEFT}
          x2={PLOT_LEFT + ramp(time, SHOT.breakevenLine, easeInOut) * (plotRight - PLOT_LEFT)}
          y1={y(breakeven)}
          y2={y(breakeven)}
        />
        {leadInDrawn.length > 1 && <polyline className={styles.priceLine} points={leadInDrawn.map((p) => `${p.x},${p.y}`).join(' ')} />}
        {drawn > 0 && <polyline className={styles.priceLine} points={[...passed, head].map((p) => `${p.x},${p.y}`).join(' ')} />}
        <circle className={styles.buyDot} cx={start.x} cy={start.y} r={4.5 * ramp(time, SHOT.buyDot, easeOutBack)} />
        {time >= crossedAt && (
          <g>
            <Pulse cx={crossing.x} cy={crossing.y} time={time - crossedAt} shot={SHOT.crossingPulse} className={styles.crossingPulse} />
            <circle className={styles.crossingRing} cx={crossing.x} cy={crossing.y} r={7.5} />
            <circle className={styles.buyDot} cx={crossing.x} cy={crossing.y} r={4} />
          </g>
        )}
        {drawn >= 1 && (
          <g>
            <Pulse cx={end.x} cy={end.y} time={time} shot={SHOT.sellPulse} className={styles.sellPulse} />
            <circle className={sellIn > 0 ? styles.sellRing : styles.sellRingDrawing} cx={end.x} cy={end.y} r={7.5} />
            <circle className={styles.sellDot} cx={end.x} cy={end.y} r={4.5 * sellIn} />
          </g>
        )}
      </svg>

      {axis.map((price) => (
        <span key={price} className={price === entry ? styles.axisEntry : styles.axisLabel} style={at(AXIS_X, y(price), axisIn)}>
          {inr(price, 0)}
        </span>
      ))}

      <span className={styles.chip} style={{ ...at(plotRight, y(breakeven), ramp(time, SHOT.breakevenChip, easeOut)), scale: `${0.9 + 0.1 * ramp(time, SHOT.breakevenChip, easeOut)}` }}>
        <span className={styles.chipTag}>{t('breakeven.beTag')}</span>
        {inr(breakeven)}
      </span>

      <span
        className={styles.zoneLabel}
        style={at(labelX, labelY, ramp(time, SHOT.chargesLabel))}
        data-zone="charges"
      >
        {t('breakeven.charges')}
        <span className={styles.chargeRate}>{t('breakeven.chargesTotal', { amount: chargeInr(exampleChargesTotal) })}</span>
      </span>
      <span className={styles.zoneLabel} style={at(PLOT_LEFT + ZONE_LABEL_INSET, version === 'v2' ? y(exit) - PROFIT_LABEL_ABOVE : y(exit) + 32.5, ramp(time, SHOT.profitLabel))} data-zone="profit">
        {t('breakeven.netProfit')}
      </span>
      <span className={styles.zoneLabel} style={at(PLOT_LEFT + ZONE_LABEL_INSET, (y(entry) + zoneBottom) / 2, ramp(time, SHOT.boughtLabel))} data-zone="bought">
        {t('breakeven.bought', { price: inr(entry, 0) })}
      </span>

      {/* Zooming out, the tags slide into the zone and stack where its "Order charges" label comes in. */}
      {tagsShown > 0 &&
        BANDS.map((band, order) => {
          const shown = ramp(time, [chargeIn(order), SHOT.chargeFill[1]], easeOut)
          const merge = tagMerge(order)
          const tagY = band.tagY + (labelY - band.tagY) * merge
          return (
            shown > 0 && (
              <span key={band.charge.id} className={styles.chargeTag} data-size={band.charge.id === 'brokerage' ? 'small' : undefined} style={{ ...rise(at(tagX, tagY), shown, 0, 4), opacity: shown * tagsShown }}>
                {t(`breakeven.charge.${band.charge.id}`)}
                <span className={styles.chargeRate}>{chargeInr(band.charge.amount)}</span>
              </span>
            )
          )
        })}

      <span className={styles.bought} style={rise(at(start.x - BOUGHT_NOTCH_X, start.y + BOUGHT_GAP), ramp(time, SHOT.bought, easeOut) * (1 - ramp(time, SHOT.boughtOut)), 0, 4)}>
        {t('breakeven.bought', { price: inr(entry, 0) })}
      </span>
      <span
        className={styles.sold}
        data-place={version === 'v2' ? 'above' : undefined}
        style={version === 'v2'
          ? rise(at(end.x + SOLD_GAP, end.y - SOLD_GAP), ramp(time, SHOT.sold, easeOut), 0, 4)
          : rise(at(end.x - SOLD_GAP, end.y), ramp(time, SHOT.sold, easeOut), 6, 0)}
      >
        <Icon icon={msCheckCircleFill} size={16} />
        {t('breakeven.sold', { price: inr(exit, 0) })}
      </span>

      {ltp > 0 && (
        <span className={styles.ltp} style={{ ...at(head.x, head.y - LTP_GAP, ltp), scale: `${0.9 + 0.1 * ltp}` }}>
          <span className={styles.ltpName}>{t('breakeven.ltp')}</span>
          <span key={last.price} className={styles.ltpValue} style={{ opacity: last === start ? 1 : ramp(time, [lastTurnAt, LTP_SWAP]) }}>
            {inr(last.price)}
          </span>
        </span>
      )}
    </>
  )
}

/**
 * The charges as bands of the zone, bottom to top (in rupees, so they follow the zoom), and where each tag sits when
 * zoomed in: at its band's middle, pushed up to stay TAG_SPACING apart, then back down to stay under TAG_TOP.
 */
function chargeBands() {
  const { entry, breakeven } = breakevenExample
  const zone = breakeven - entry
  const total = breakevenCharges.reduce((sum, charge) => sum + charge.amount, 0)
  const heights = breakevenCharges.map((charge) => Math.max((charge.amount / total) * zone, MIN_BAND / ZOOMED_RUPEE))
  const fit = zone / heights.reduce((sum, height) => sum + height, 0)
  let from = entry
  const bands = breakevenCharges.map((charge, order) => {
    const band = { charge, from, to: from + heights[order] * fit, tagY: 0 }
    from = band.to
    return band
  })
  bands.forEach((band, order) => {
    const middle = priceY((band.from + band.to) / 2, ZOOMED_RUPEE)
    band.tagY = order === 0 ? middle : Math.min(middle, bands[order - 1].tagY - TAG_SPACING)
  })
  for (let order = bands.length - 1; order >= 0; order--) {
    const above = bands[order + 1]
    bands[order].tagY = Math.max(bands[order].tagY, above ? above.tagY + TAG_SPACING : TAG_TOP)
  }
  return bands
}

/** The polyline `points` drawn `progress` (0 → 1) of the way along x, ending at its moving head. */
function lineTo(points: { x: number; y: number }[], progress: number) {
  const first = points[0]
  const headX = first.x + progress * (points[points.length - 1].x - first.x)
  const passed = points.filter((p) => p.x <= headX)
  const next = points[passed.length]
  if (!next || passed.length === 0) return passed
  const last = passed[passed.length - 1]
  return [...passed, { x: headX, y: last.y + ((headX - last.x) / (next.x - last.x)) * (next.y - last.y) }]
}

/** A charge in ₹: paise to 2 places (₹0.15); the tiny ones to their first digit (₹0.003, ₹0.0002). */
function chargeInr(amount: number) {
  return `₹${amount >= 0.01 ? amount.toFixed(2) : Number(amount.toPrecision(1))}`
}

/** A ring that grows from the marker (7.5 → 14) and fades. */
function Pulse({ cx, cy, time, shot, className }: { cx: number; cy: number; time: number; shot: [number, number]; className: string }) {
  const p = ramp(time, shot, easeOut)
  if (p <= 0 || p >= 1) return null
  return <circle className={className} cx={cx} cy={cy} r={7.5 + 6.5 * p} opacity={0.4 * (1 - p)} />
}

/** The intro the loop ends on: Figma's reveal (its timings are CSS animations, so it plays each time it mounts). */
function Intro({ fade = 1 }: { fade?: number }) {
  return (
    <div className={styles.intro} style={{ opacity: fade }}>
      <BreakevenIcon variant="tile" className={styles.introIcon} />
      <p className={styles.overline}>{t('breakeven.introducing')}</p>
      <p className={styles.introTitle}>{t('breakeven.lineName')}</p>
      <p className={styles.introText}>{t('breakeven.tagline')}</p>
    </div>
  )
}

/** A callout anchored at (x, y) on the stage; each callout's CSS places itself around that point. */
function at(x: number, y: number, opacity = 1): CSSProperties {
  return { '--x': `${x}px`, '--y': `${y}px`, opacity } as CSSProperties
}

/** Comes in by `progress`, moving from (dx, dy) px away to its place. */
function rise(style: CSSProperties, progress: number, dx: number, dy: number): CSSProperties {
  return { ...style, opacity: progress, translate: `${dx * (1 - progress)}px ${dy * (1 - progress)}px` }
}

/** 0 → 1 over [start, duration], eased. */
function ramp(time: number, [start, duration]: [number, number], ease = linear) {
  return ease(Math.min(1, Math.max(0, (time - start) / duration)))
}
const linear = (x: number) => x
const easeOut = (x: number) => 1 - (1 - x) ** 3
const easeInOut = (x: number) => (x < 0.5 ? 4 * x ** 3 : 1 - (-2 * x + 2) ** 3 / 2)
const easeOutBack = (x: number) => 1 + 2.70158 * (x - 1) ** 3 + 1.70158 * (x - 1) ** 2

/** Milliseconds since the play started, every frame, stopping at `until`; a new `run` plays it again from 0. */
function useElapsed(playing: boolean, until: number, run: number) {
  const [elapsed, setElapsed] = useState(0)
  useEffect(() => {
    if (!playing) return
    let frame = 0
    let start: number | undefined
    setElapsed(0)
    const tick = (now: number) => {
      start ??= now
      const passed = Math.min(now - start, until)
      setElapsed(passed)
      if (passed < until) frame = requestAnimationFrame(tick)
    }
    frame = requestAnimationFrame(tick)
    return () => cancelAnimationFrame(frame)
  }, [playing, until, run])
  return elapsed
}

/** The element's width, kept current. */
function useWidth(ref: React.RefObject<HTMLElement | null>, fallback: number) {
  const [width, setWidth] = useState(fallback)
  useLayoutEffect(() => {
    const element = ref.current
    if (!element) return
    const observer = new ResizeObserver(() => setWidth(element.clientWidth))
    observer.observe(element)
    setWidth(element.clientWidth)
    return () => observer.disconnect()
  }, [ref])
  return width
}
```

### `src/flows/fno/assets/breakeven-info.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="12" height="12" viewBox="0 0 12 12" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="D2 &#226;&#134;&#146; info_outline">
<path id="Vector" d="M5.5 3.5H6.5V4.5H5.5V3.5ZM6 8.5C6.275 8.5 6.5 8.275 6.5 8V6C6.5 5.725 6.275 5.5 6 5.5C5.725 5.5 5.5 5.725 5.5 6V8C5.5 8.275 5.725 8.5 6 8.5ZM6 1C3.24 1 1 3.24 1 6C1 8.76 3.24 11 6 11C8.76 11 11 8.76 11 6C11 3.24 8.76 1 6 1ZM6 10C3.795 10 2 8.205 2 6C2 3.795 3.795 2 6 2C8.205 2 10 3.795 10 6C10 8.205 8.205 10 6 10Z" fill="#9F7502" style="fill:#9F7502;fill:color(display-p3 0.6235 0.4593 0.0078);fill-opacity:1;"/>
</g>
</svg>
```

### `src/flows/fno/assets/breakeven-tile-arrow.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g id="Frame">
<g id="Union">
<use xlink:href="#stroke0_0_4" fill="#0F9958" style="fill:#0F9958;fill:color(display-p3 0.0588 0.6000 0.3451);fill-opacity:1;"/>
<use xlink:href="#stroke0_0_4" fill="url(#paint0_linear_0_4)"/>
</g>
</g>
<defs>
<linearGradient id="paint0_linear_0_4" x1="12.0001" y1="3.00098" x2="12.0001" y2="22.9896" gradientUnits="userSpaceOnUse">
<stop stop-color="#EDFBBF" style="stop-color:#EDFBBF;stop-color:color(display-p3 0.9294 0.9843 0.7490);stop-opacity:1;"/>
<stop offset="1" stop-color="#B1E50E" style="stop-color:#B1E50E;stop-color:color(display-p3 0.6941 0.8980 0.0549);stop-opacity:1;"/>
</linearGradient>
<path id="stroke0_0_4" d="M11.9728 2.00098C12.2803 2.00098 12.5498 2.11606 12.7804 2.34668L18.0499 7.62793C18.2805 7.85851 18.3925 8.13119 18.3849 8.44629C18.3772 8.76147 18.2581 9.035 18.0275 9.26562C17.7969 9.48087 17.5274 9.59192 17.2199 9.59961C16.9124 9.6073 16.6429 9.49623 16.4122 9.26562L13.1261 5.97852V14.3066H14.3058C14.9426 14.3066 15.459 14.8232 15.4591 15.46C15.4591 16.0968 14.9426 16.6133 14.3058 16.6133H13.1261V20.8359C13.1261 21.151 13.0149 21.4237 12.7921 21.6543C12.5692 21.8849 12.2957 21.9969 11.9728 21.9893C11.6501 21.9815 11.3773 21.8695 11.1544 21.6543C10.9316 21.4391 10.8205 21.1664 10.8205 20.8359V16.6133H9.6935C9.05678 16.6131 8.54018 16.0967 8.54018 15.46C8.54027 14.8233 9.05683 14.3068 9.6935 14.3066H10.8205V5.97852L7.53334 9.26562C7.30286 9.49592 7.03394 9.60725 6.7267 9.59961C6.41925 9.59192 6.14969 9.48082 5.91908 9.26562C5.68078 9.035 5.55763 8.76147 5.54994 8.44629C5.5423 8.13119 5.65434 7.85851 5.8849 7.62793L11.1662 2.34668C11.3967 2.11616 11.6655 2.00107 11.9728 2.00098ZM6.23451 14.3066C6.87126 14.3067 7.38774 14.8232 7.38783 15.46C7.38783 16.0968 6.87132 16.6132 6.23451 16.6133H1.62221C0.985364 16.6133 0.468889 16.0968 0.468889 15.46C0.468981 14.8232 0.985421 14.3066 1.62221 14.3066H6.23451ZM22.3781 14.3066C23.0148 14.3067 23.5313 14.8232 23.5314 15.46C23.5314 16.0968 23.0149 16.6132 22.3781 16.6133H17.7658C17.1289 16.6133 16.6124 16.0968 16.6124 15.46C16.6125 14.8232 17.129 14.3066 17.7658 14.3066H22.3781Z"/>
</defs>
</svg>
```

### `src/flows/fno/assets/commodities.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="commodities">
<path id="Vector" d="M7.99977 2.00024C9.24085 2.00024 10.382 2.12556 11.2276 2.33693C11.6464 2.44163 12.022 2.57458 12.3051 2.74191C12.5537 2.88887 12.9028 3.16594 12.9029 3.61133C12.9029 4.02792 12.5971 4.29675 12.3541 4.45022V6.95002C12.66 7.21206 12.9029 7.56141 12.9029 8.00024C12.9028 8.42724 12.6699 8.77266 12.3847 9.02556C12.3749 9.03423 12.3641 9.0419 12.3541 9.05047V10.7901C12.6599 11.0521 12.9029 11.4016 12.9029 11.8403C12.9027 12.2672 12.6698 12.6128 12.3847 12.8657C12.0988 13.119 11.7144 13.3237 11.2838 13.4852C10.4184 13.8097 9.2568 14.0002 7.99977 14.0002C6.74284 14.0002 5.58187 13.8096 4.71652 13.4852C4.28591 13.3237 3.90154 13.119 3.61568 12.8657C3.33049 12.6128 3.0976 12.2672 3.0974 11.8403C3.0974 11.4015 3.34038 11.0522 3.64621 10.7901V9.05047C3.63619 9.0419 3.62547 9.03423 3.61568 9.02556C3.33042 8.77266 3.09749 8.42724 3.0974 8.00024C3.0974 7.56134 3.34031 7.21207 3.64621 6.95002V4.45022C3.40325 4.29675 3.0974 4.02792 3.0974 3.61133C3.09754 3.16594 3.44659 2.88887 3.69523 2.74191C3.97825 2.57468 4.35335 2.4416 4.77196 2.33693C5.61752 2.12554 6.75867 2.00026 7.99977 2.00024ZM11.2838 9.64508C10.4184 9.9696 9.25684 10.1601 7.99977 10.1601C6.74279 10.1601 5.58189 9.96957 4.71652 9.64508C4.70234 9.63976 4.68882 9.63282 4.67474 9.6274V11.0432C4.67457 11.2139 4.58951 11.3736 4.44814 11.4691C4.15334 11.6681 4.12592 11.8057 4.12592 11.8403C4.1261 11.8683 4.14013 11.956 4.29788 12.0959C4.45612 12.2361 4.71424 12.3864 5.07731 12.5225C5.80014 12.7936 6.83353 12.9717 7.99977 12.9717C9.16595 12.9717 10.1994 12.7935 10.9222 12.5225C11.2855 12.3863 11.5442 12.2361 11.7025 12.0959C11.8602 11.956 11.8742 11.8683 11.8744 11.8403C11.8744 11.8057 11.847 11.6681 11.5522 11.4691C11.4107 11.3736 11.3258 11.2139 11.3256 11.0432V9.6274C11.3115 9.63282 11.298 9.63976 11.2838 9.64508ZM11.2276 4.88654C10.382 5.0979 9.24082 5.22323 7.99977 5.22323C6.75867 5.22321 5.61752 5.09793 4.77196 4.88654C4.73909 4.87832 4.70705 4.8678 4.67474 4.85922V7.20314C4.67467 7.37387 4.5896 7.53342 4.44814 7.62901C4.15321 7.8281 4.12592 7.96556 4.12592 8.00024C4.12601 8.02789 4.13955 8.1154 4.29788 8.25577C4.45611 8.39601 4.71413 8.54625 5.07731 8.68245C5.50233 8.84182 6.03495 8.96704 6.63858 9.04484C6.65612 9.06394 6.6724 9.08427 6.69081 9.10269C7.03793 9.44982 7.50887 9.645 7.99977 9.64508C8.49076 9.64507 8.96154 9.44988 9.30873 9.10269C9.32701 9.0844 9.34271 9.0638 9.36015 9.04484C9.96408 8.96704 10.497 8.84186 10.9222 8.68245C11.2856 8.5462 11.5442 8.39606 11.7025 8.25577C11.8607 8.11543 11.8743 8.02789 11.8744 8.00024C11.8744 7.96556 11.8471 7.8281 11.5522 7.62901C11.4106 7.53343 11.3257 7.37394 11.3256 7.20314V4.85922C11.293 4.86786 11.2607 4.87826 11.2276 4.88654ZM7.99977 3.02877C6.8175 3.02879 5.76446 3.14928 5.02186 3.33492C4.66856 3.42324 4.41136 3.52087 4.24806 3.61133C4.41135 3.70183 4.6684 3.80019 5.02186 3.88855C5.76446 4.07418 6.81753 4.19468 7.99977 4.1947C9.1822 4.1947 10.2358 4.07422 10.9785 3.88855C11.3316 3.80027 11.5882 3.70176 11.7515 3.61133C11.5882 3.52095 11.3314 3.42316 10.9785 3.33492C10.2358 3.14925 9.1822 3.02877 7.99977 3.02877Z" fill-rule="evenodd" clip-rule="evenodd" fill="#161616" fill-opacity="0.6" style="fill:#161616;fill:color(display-p3 0.0863 0.0863 0.0863);fill-opacity:0.6;"/>
<path id="Vector_2" d="M8.72732 8.5215C8.53444 8.71439 8.27283 8.82275 8.00006 8.82275C7.72728 8.82275 7.46568 8.71439 7.2728 8.5215C7.07992 8.32862 6.97156 8.06702 6.97156 7.79425C6.97156 7.10858 8.00006 6.08008 8.00006 6.08008C8.00006 6.08008 9.02856 7.10858 9.02856 7.79425C9.02856 8.06702 8.9202 8.32862 8.72732 8.5215Z" fill="#161616" fill-opacity="0.6" style="fill:#161616;fill:color(display-p3 0.0863 0.0863 0.0863);fill-opacity:0.6;"/>
</g>
</svg>
```

### `src/flows/fno/assets/downtrend.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="keyboard_double_arrow_down_24dp_E3E3E3_FILL1_wght400_GRAD0_opsz24 7">
<path id="Vector" d="M10.0004 13.477L13.2504 10.2478C13.4032 10.095 13.5942 10.0152 13.8233 10.0082C14.0525 10.0013 14.2504 10.0811 14.4171 10.2478C14.5699 10.4006 14.6462 10.595 14.6462 10.8311C14.6462 11.0673 14.5699 11.2617 14.4171 11.4145L10.5838 15.2478C10.5004 15.3311 10.4101 15.3902 10.3129 15.4249C10.2157 15.4596 10.1115 15.477 10.0004 15.477C9.88931 15.477 9.78514 15.4596 9.68792 15.4249C9.59069 15.3902 9.50042 15.3311 9.41708 15.2478L5.58375 11.4145C5.43097 11.2617 5.35111 11.0707 5.34417 10.8416C5.33722 10.6124 5.41708 10.4145 5.58375 10.2478C5.73653 10.095 5.93097 10.0186 6.16708 10.0186C6.40319 10.0186 6.59764 10.095 6.75042 10.2478L10.0004 13.477ZM10.0004 8.47698L13.2504 5.24781C13.4032 5.09503 13.5942 5.01517 13.8233 5.00823C14.0525 5.00128 14.2504 5.08115 14.4171 5.24781C14.5699 5.40059 14.6462 5.59503 14.6462 5.83115C14.6462 6.06726 14.5699 6.2617 14.4171 6.41448L10.5838 10.2478C10.5004 10.3311 10.4101 10.3902 10.3129 10.4249C10.2157 10.4596 10.1115 10.477 10.0004 10.477C9.88931 10.477 9.78514 10.4596 9.68792 10.4249C9.59069 10.3902 9.50042 10.3311 9.41708 10.2478L5.58375 6.41448C5.43097 6.2617 5.35111 6.07073 5.34417 5.84156C5.33722 5.6124 5.41708 5.41448 5.58375 5.24781C5.73653 5.09503 5.93097 5.01865 6.16708 5.01865C6.40319 5.01865 6.59764 5.09503 6.75042 5.24781L10.0004 8.47698Z" fill="#E5505F" style="fill:#E5505F;fill:color(display-p3 0.8980 0.3137 0.3725);fill-opacity:1;"/>
</g>
</svg>
```

### `src/flows/fno/assets/equity.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="candle icon">
<rect id="Rectangle 240662752" x="9.60156" y="5.60156" width="3.2" height="4" fill="#DEF4EA" style="fill:#DEF4EA;fill:color(display-p3 0.8706 0.9569 0.9176);fill-opacity:1;"/>
<path id="Vector" d="M10.5582 13.7616V10.2989H9.62276C9.40431 10.2989 9.22113 10.2251 9.07322 10.0773C8.92545 9.92938 8.85156 9.7462 8.85156 9.52775V5.70418C8.85156 5.48558 8.92545 5.3024 9.07322 5.15463C9.22113 5.00686 9.40431 4.93298 9.62276 4.93298H10.5582V2.24156C10.5582 2.06023 10.6196 1.90826 10.7423 1.78567C10.8651 1.66293 11.0171 1.60156 11.1984 1.60156C11.3799 1.60156 11.5319 1.66293 11.6543 1.78567C11.7769 1.90826 11.8382 2.06023 11.8382 2.24156V4.93298H12.7735C12.9921 4.93298 13.1753 5.00686 13.323 5.15463C13.4709 5.3024 13.5449 5.48558 13.5449 5.70418V9.52775C13.5449 9.7462 13.4709 9.92938 13.323 10.0773C13.1753 10.2251 12.9921 10.2989 12.7735 10.2989H11.8382V13.7616C11.8382 13.9429 11.7769 14.0949 11.6541 14.2175C11.5314 14.3402 11.3793 14.4016 11.198 14.4016C11.0165 14.4016 10.8646 14.3402 10.7421 14.2175C10.6195 14.0949 10.5582 13.9429 10.5582 13.7616ZM10.1316 9.01895H12.2649V6.21276H10.1316V9.01895Z" fill="#0F9958" style="fill:#0F9958;fill:color(display-p3 0.0588 0.6000 0.3451);fill-opacity:1;"/>
<rect id="Rectangle 240662751" x="3.19922" y="4" width="3.2" height="8" fill="#DEF4EA" style="fill:#DEF4EA;fill:color(display-p3 0.8706 0.9569 0.9176);fill-opacity:1;"/>
<path id="Subtract" d="M4.7998 1.59766C4.98128 1.59766 5.13341 1.65949 5.25586 1.78223C5.37823 1.90471 5.43937 2.05623 5.43945 2.2373V3.30469H6.375C6.59345 3.30469 6.77689 3.37846 6.9248 3.52637C7.07251 3.67412 7.14648 3.85762 7.14648 4.07617V11.916C7.14648 12.1381 7.07242 12.3227 6.9248 12.4697C6.77689 12.6169 6.59345 12.6914 6.375 12.6914H5.43945V13.7578C5.43942 13.9391 5.37856 14.0913 5.25586 14.2139C5.13319 14.3365 4.981 14.3974 4.7998 14.3975C4.61842 14.3975 4.46617 14.3365 4.34375 14.2139C4.22119 14.0913 4.16019 13.9391 4.16016 13.7578V12.6914H3.22461C3.00601 12.6914 2.82257 12.6167 2.6748 12.4688C2.52716 12.3211 2.4532 12.1382 2.45312 11.9199V4.0791C2.45312 3.85706 2.52705 3.67241 2.6748 3.52539C2.82257 3.37819 3.00601 3.30469 3.22461 3.30469H4.16016V2.2373C4.16024 2.05628 4.2213 1.90469 4.34375 1.78223C4.46644 1.65953 4.61856 1.5977 4.7998 1.59766ZM3.73438 4.58594V11.4131H5.86816V4.58594H3.73438Z" fill="#0F9958" style="fill:#0F9958;fill:color(display-p3 0.0588 0.6000 0.3451);fill-opacity:1;"/>
</g>
</svg>
```

### `src/flows/fno/assets/option-chain.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="link (1) 1">
<g id="Union">
<path d="M8.23225 6.05078C9.41705 6.05087 10.5534 6.52186 11.3914 7.35938C11.8205 7.78957 12.1587 8.30273 12.3836 8.86719C12.6085 9.43169 12.7157 10.0371 12.7 10.6445C12.6938 10.8632 12.6012 11.0704 12.4422 11.2207C12.2832 11.3709 12.071 11.4524 11.8524 11.4463C11.6336 11.4401 11.4255 11.3465 11.2752 11.1875C11.1251 11.0285 11.0445 10.8162 11.0506 10.5977L11.0487 10.3857C11.0264 9.89431 10.8758 9.41598 10.6102 8.99902C10.3065 8.52244 9.86656 8.14818 9.34749 7.9248C8.82838 7.70147 8.2539 7.6389 7.69905 7.74609C7.14438 7.8533 6.63463 8.12494 6.23616 8.52539L3.52522 11.2412C3.13154 11.6352 2.8634 12.1373 2.75471 12.6836C2.64611 13.2298 2.7019 13.7959 2.91487 14.3105C3.12784 14.8251 3.48818 15.2654 3.951 15.5752C4.414 15.8849 4.95939 16.0503 5.51643 16.0508C5.88756 16.0522 6.25553 15.9798 6.59846 15.8379C6.94129 15.696 7.25295 15.4878 7.51448 15.2246L8.37483 14.3643L8.38069 14.3574L8.3885 14.3516C8.54735 14.2201 8.74996 14.1528 8.95588 14.1631C9.16183 14.1734 9.35686 14.2605 9.50178 14.4072C9.64669 14.554 9.73131 14.75 9.73909 14.9561C9.74685 15.1622 9.67729 15.3642 9.54378 15.5215L8.67268 16.3926C8.25864 16.8086 7.76579 17.1387 7.22346 17.3633C6.74888 17.5597 6.24423 17.6724 5.73225 17.6963L5.51253 17.7012C4.62938 17.7002 3.76598 17.4375 3.03206 16.9463C2.29817 16.455 1.72598 15.7566 1.3885 14.9404C1.0512 14.1244 0.962966 13.2263 1.13557 12.3604C1.30824 11.4943 1.73462 10.6986 2.35921 10.0742L5.0721 7.35938L5.23323 7.20703C6.05298 6.46514 7.12139 6.05082 8.23225 6.05078ZM8.51546 14.5059C8.5455 14.481 8.57845 14.4591 8.61213 14.4404L8.51546 14.5059ZM9.53889 14.9639L9.5301 14.877C9.52903 14.871 9.52646 14.8653 9.52522 14.8594C9.53238 14.8936 9.53756 14.9285 9.53889 14.9639ZM11.7352 11.2305L11.8573 11.2461C11.7787 11.2438 11.7026 11.2254 11.6317 11.1953C11.6652 11.2095 11.6995 11.2223 11.7352 11.2305ZM11.2498 10.6035L11.2586 10.7266C11.2647 10.7623 11.2748 10.7971 11.2869 10.8311C11.2611 10.7587 11.2476 10.6817 11.2498 10.6035ZM6.43538 8.08887C6.39246 8.1207 6.35163 8.1553 6.31038 8.18945C6.35811 8.14995 6.40622 8.11097 6.45588 8.07422L6.43538 8.08887Z" fill-rule="evenodd" clip-rule="evenodd" fill="#161616" style="fill:#161616;fill:color(display-p3 0.0863 0.0863 0.0863);fill-opacity:1;"/>
<path d="M14.4803 2.2998C15.0673 2.2998 15.649 2.41599 16.1912 2.64062C16.7334 2.86527 17.2265 3.19435 17.6414 3.60938C18.0712 4.04026 18.4097 4.5546 18.6346 5.12012C18.8595 5.68562 18.9665 6.29106 18.95 6.89941C18.9172 8.03859 18.449 9.12258 17.6414 9.92676L17.6405 9.92578L14.9276 12.6416C14.5135 13.0579 14.0208 13.3886 13.4783 13.6133C12.9361 13.8379 12.3543 13.9518 11.7674 13.9502L11.7635 13.9512C11.1667 13.9507 10.5759 13.8302 10.0262 13.5977C9.47645 13.3651 8.97833 13.0248 8.56233 12.5967C8.14641 12.1686 7.82006 11.6616 7.60335 11.1055C7.38669 10.5494 7.28396 9.955 7.30061 9.3584C7.30676 9.13966 7.39943 8.9316 7.55842 8.78125C7.71738 8.63104 7.92966 8.55059 8.14827 8.55664C8.36701 8.56279 8.57507 8.65545 8.72542 8.81445C8.87556 8.97347 8.95617 9.18568 8.95003 9.4043C8.9394 9.78056 9.00486 10.1551 9.14143 10.5059C9.27805 10.8567 9.48361 11.1772 9.74592 11.4473C10.0082 11.7171 10.3222 11.9315 10.6688 12.0781C11.0155 12.2248 11.3881 12.3005 11.7645 12.3008C12.1343 12.3017 12.5009 12.2293 12.8426 12.0879C13.1842 11.9464 13.4948 11.7386 13.7557 11.4766L16.4715 8.76074C16.9937 8.23133 17.2853 7.51709 17.283 6.77344C17.2807 6.02912 16.9841 5.31537 16.4578 4.78906C15.9316 4.263 15.2185 3.96624 14.4744 3.96387C13.7302 3.96158 13.0147 4.25438 12.4852 4.77734L11.6268 5.63574L11.6229 5.63867C11.467 5.78672 11.2597 5.86887 11.0448 5.86621C10.8297 5.86341 10.6236 5.77612 10.4715 5.62402C10.3196 5.47199 10.2331 5.26666 10.2303 5.05176C10.2275 4.83667 10.3087 4.62862 10.4569 4.47266L11.3201 3.60938C11.7351 3.19437 12.2282 2.86528 12.7703 2.64062C13.3125 2.41605 13.8935 2.29989 14.4803 2.2998ZM16.494 3.00488C16.5477 3.03363 16.6007 3.06373 16.6532 3.09473C16.5408 3.02826 16.4257 2.96612 16.3074 2.91016L16.494 3.00488Z" fill-rule="evenodd" clip-rule="evenodd" fill="#161616" style="fill:#161616;fill:color(display-p3 0.0863 0.0863 0.0863);fill-opacity:1;"/>
</g>
</g>
</svg>
```

### `src/flows/fno/assets/referral.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="Gift-2--Streamline-Core" clip-path="url(#clip0_0_8)">
<g id="gift-2--reward-box-social-present-gift-media-rating-bow">
<path id="Vector" d="M17.5384 17.1422V9.8457H2.46484V17.1422C2.46484 17.9312 3.10444 18.5708 3.89342 18.5708H16.1098C16.8988 18.5708 17.5384 17.9312 17.5384 17.1422Z" fill="#E8E8E8" style="fill:#E8E8E8;fill:color(display-p3 0.9098 0.9098 0.9098);fill-opacity:1;"/>
<path id="Vector_2" d="M18.5725 6.84459V8.41716C18.5725 9.20614 17.933 9.84573 17.144 9.84573H2.85826C2.06929 9.84573 1.42969 9.20614 1.42969 8.41716V6.84459C1.42969 6.0556 2.06929 5.41602 2.85826 5.41602H17.144C17.933 5.41602 18.5725 6.0556 18.5725 6.84459Z" fill="#161616" style="fill:#161616;fill:color(display-p3 0.0863 0.0863 0.0863);fill-opacity:1;"/>
<path id="Union" d="M17.5342 9.14355C17.9208 9.14355 18.2344 9.45715 18.2344 9.84375V17.1406C18.2342 18.316 17.2809 19.2686 16.1055 19.2686H10.0283C10.0189 19.2689 10.0095 19.2715 10 19.2715C9.99048 19.2715 9.9811 19.2689 9.97168 19.2686H3.88965C2.71422 19.2686 1.76095 18.3161 1.76074 17.1406V9.84375C1.76074 9.45715 2.07434 9.14355 2.46094 9.14355H17.5342ZM10.7002 17.8691H16.1055C16.5077 17.8691 16.8348 17.5428 16.835 17.1406V10.5439H10.7002V17.8691ZM3.16113 17.1406C3.16134 17.5428 3.4874 17.8691 3.88965 17.8691H9.2998V10.5439H3.16113V17.1406Z" fill="#161616" style="fill:#161616;fill:color(display-p3 0.0863 0.0863 0.0863);fill-opacity:1;"/>
</g>
<path id="Vector_5" d="M9.99868 5.41583C9.99868 4.21941 8.60285 1.42773 6.50909 1.42773C3.10288 1.42773 4.34368 5.41583 5.97399 5.41583" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round" stroke="#161616" style="stroke:#161616;stroke:color(display-p3 0.0863 0.0863 0.0863);stroke-opacity:1;"/>
<path id="Vector_6" d="M10 5.41583C10 4.21941 11.3958 1.42773 13.4896 1.42773C16.8959 1.42773 15.655 5.41583 14.0247 5.41583" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round" stroke="#161616" style="stroke:#161616;stroke:color(display-p3 0.0863 0.0863 0.0863);stroke-opacity:1;"/>
<path id="Vector_4" d="M18.5725 6.84459V8.41716C18.5725 9.20614 17.933 9.84573 17.144 9.84573H2.85826C2.06929 9.84573 1.42969 9.20614 1.42969 8.41716V6.84459C1.42969 6.0556 2.06929 5.41602 2.85826 5.41602H17.144C17.933 5.41602 18.5725 6.0556 18.5725 6.84459Z" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round" stroke="#161616" style="stroke:#161616;stroke:color(display-p3 0.0863 0.0863 0.0863);stroke-opacity:1;"/>
</g>
<defs>
<clipPath id="clip0_0_8">
<rect width="20" height="20" fill="white" style="fill:white;fill-opacity:1;"/>
</clipPath>
</defs>
</svg>
```

### `src/flows/fno/assets/scalppro.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="score_24dp_E3E3E3_FILL0_wght300_GRAD0_opsz24">
<path id="Vector" d="M4.09507 17.5C3.64934 17.5 3.27206 17.3456 2.96324 17.0368C2.65441 16.7279 2.5 16.3507 2.5 15.9049V4.09507C2.5 3.64934 2.65441 3.27206 2.96324 2.96324C3.27206 2.65441 3.64934 2.5 4.09507 2.5H15.9049C16.3507 2.5 16.7279 2.65441 17.0368 2.96324C17.3456 3.27206 17.5 3.64934 17.5 4.09507V15.9049C17.5 16.3507 17.3456 16.7279 17.0368 17.0368C16.7279 17.3456 16.3507 17.5 15.9049 17.5H4.09507ZM10.8824 14.3101L16.1765 9.01596V4.09507C16.1765 4.02713 16.1482 3.96493 16.0915 3.90846C16.0351 3.85184 15.9729 3.82353 15.9049 3.82353H4.09507C4.02713 3.82353 3.96493 3.85184 3.90846 3.90846C3.85184 3.96493 3.82353 4.02713 3.82353 4.09507V14.3101L6.79463 11.3387C6.95419 11.1793 7.14029 11.0996 7.35294 11.0996C7.56559 11.0996 7.75169 11.1793 7.91125 11.3387L10.8824 14.3101ZM7.35294 12.4774L3.82353 16.0068C3.82912 16.0351 3.85596 16.0704 3.90404 16.1129C3.95213 16.1553 4.01581 16.1765 4.09507 16.1765H15.9049C15.9729 16.1765 16.0351 16.1482 16.0915 16.0915C16.1482 16.0351 16.1765 15.9729 16.1765 15.9049V10.7127L11.4407 15.4485C11.2811 15.6081 11.095 15.6879 10.8824 15.6879C10.6697 15.6879 10.4836 15.6081 10.324 15.4485L7.35294 12.4774ZM3.82353 15.9049V16.1765V3.82353V15.9049Z" fill="white" style="fill:white;fill-opacity:1;"/>
<path id="Vector_2" d="M9.03272 8.62368L7.79858 8.56247C7.66228 8.55572 7.56538 8.49097 7.50789 8.36825C7.45033 8.24559 7.46385 8.13082 7.54845 8.02394L10.3947 4.35662C10.4531 4.28357 10.5253 4.2352 10.6115 4.21154C10.6976 4.18794 10.7856 4.19466 10.8756 4.23169C10.9655 4.26865 11.0297 4.32747 11.0682 4.40816C11.1067 4.48884 11.1182 4.57426 11.1028 4.66443L10.6766 7.09345L12.19 7.1685C12.3346 7.17567 12.4333 7.2449 12.4863 7.3762C12.5392 7.50743 12.5159 7.62611 12.4163 7.73225L9.30455 11.0741C9.24237 11.1403 9.16839 11.1814 9.08259 11.1976C8.9968 11.2137 8.91452 11.2014 8.83574 11.1609C8.75696 11.1203 8.69719 11.0613 8.65643 10.9839C8.61568 10.9064 8.60302 10.8226 8.61848 10.7325L9.03272 8.62368Z" fill="white" style="fill:white;fill-opacity:1;"/>
</g>
</svg>
```

### `src/flows/fno/assets/shortcuts/analysis.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="19.8232" height="19.8213" viewBox="0 0 19.8232 19.8213" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="ai-smart-assistant-square--ai-smart-assistant-square-intelligence-helper">
<path id="Subtract" d="M9.11459 3.48246C8.78715 3.9418 8.60119 4.5007 8.60119 5.0896C8.60119 6.14081 9.19585 7.09496 10.1246 7.5617L10.3144 7.6482L12.0847 8.37643C12.1507 8.4037 12.2061 8.4504 12.2452 8.50896L12.2786 8.57034L13.0069 10.3407C13.4337 11.3774 14.379 11.5777 15.5001 11.5777C16.0892 11.5777 16.1249 11.5777 16.3393 11.5777V17.7682C16.3393 18.5572 15.6997 19.1967 14.9107 19.1967H2.05357C1.26459 19.1967 0.625 18.5572 0.625 17.7682V4.91103C0.625 4.12206 1.26459 3.48246 2.05357 3.48246H9.11459Z" fill="#DEF4EA" style="fill:#DEF4EA;fill:color(display-p3 0.8706 0.9569 0.9176);fill-opacity:1;"/>
<g id="Vector 6273">
<path id="Vector 6269_3" d="M13.7585 2.55993L14.4872 0.790156C14.5284 0.690243 14.6258 0.625035 14.7338 0.625035C14.8418 0.625035 14.9392 0.690243 14.9804 0.790156L15.7091 2.55993C15.9992 3.26446 16.5587 3.82392 17.2632 4.11402L19.033 4.84276C19.133 4.88389 19.1981 4.98126 19.1981 5.08932C19.1981 5.19738 19.133 5.29475 19.033 5.33588L17.2632 6.06462C16.5587 6.35472 15.9992 6.91418 15.7091 7.61871L14.9804 9.38849C14.9392 9.48839 14.8418 9.55361 14.7338 9.55361C14.6258 9.55361 14.5284 9.48839 14.4872 9.38849L13.7585 7.61871C13.4684 6.91418 12.909 6.35472 12.2044 6.06462L10.4346 5.33588C10.3347 5.29475 10.2695 5.19738 10.2695 5.08932C10.2695 4.98126 10.3347 4.88389 10.4346 4.84276L12.2044 4.11402C12.909 3.82392 13.4684 3.26446 13.7585 2.55993Z" fill="#0F9958" style="fill:#0F9958;fill:color(display-p3 0.0588 0.6000 0.3451);fill-opacity:1;"/>
</g>
<g id="Vector 6270">
<path id="Union" d="M8.66113 2.85742C9.00612 2.85765 9.28613 3.13738 9.28613 3.48242C9.28613 3.82746 9.00612 4.1072 8.66113 4.10742H2.05371C1.60991 4.10742 1.25 4.46733 1.25 4.91113V13.8379L3.38965 11.6689L3.39062 11.668C3.63619 11.4225 3.94341 11.3 4.2998 11.2998C4.65637 11.2999 4.9643 11.4224 5.20996 11.668L6.52344 12.9941L9.00684 10.5352H8.52246C8.32334 10.5351 8.14795 10.4662 8.00879 10.3271C7.86965 10.1879 7.79983 10.0127 7.7998 9.81348C7.7998 9.61419 7.86964 9.43905 8.00879 9.2998C8.14796 9.16072 8.3233 9.0909 8.52246 9.09082H10.7451C10.9441 9.09101 11.1197 9.16083 11.2588 9.2998C11.3978 9.43901 11.4668 9.61432 11.4668 9.81348V12.0352C11.4668 12.2342 11.3976 12.4096 11.2588 12.5488C11.1197 12.6878 10.9441 12.7576 10.7451 12.7578C10.546 12.7577 10.3696 12.6879 10.2305 12.5488C10.0916 12.4097 10.0225 12.2342 10.0225 12.0352V11.5488L7.43164 14.1396C7.18603 14.3851 6.87891 14.5077 6.52246 14.5078C6.16602 14.5077 5.8589 14.3851 5.61328 14.1396L4.2998 12.8262L1.47363 15.6533C1.40758 15.7193 1.3321 15.7682 1.25 15.8018V17.7686C1.25023 18.2122 1.61004 18.5713 2.05371 18.5713H14.9111C15.3546 18.5711 15.7136 18.212 15.7139 17.7686V11.9941C15.7139 11.6492 15.9939 11.3694 16.3389 11.3691C16.684 11.3691 16.9638 11.649 16.9639 11.9941V17.7686C16.9636 18.9024 16.045 19.8211 14.9111 19.8213H2.05371C0.9197 19.8213 0.00022674 18.9025 0 17.7686V4.91113C0 3.77697 0.919556 2.85742 2.05371 2.85742H8.66113ZM10.3486 12.4316C10.3733 12.4562 10.4004 12.4772 10.4277 12.4961C10.4005 12.4773 10.3741 12.4561 10.3496 12.4316C10.3252 12.4073 10.304 12.3806 10.2852 12.3535C10.3039 12.3806 10.3243 12.4073 10.3486 12.4316ZM14.7334 0C15.0494 0 15.3386 0.167004 15.498 0.432617L15.5586 0.551758L16.2871 2.32227C16.5138 2.8725 16.9507 3.30952 17.501 3.53613L19.2705 4.26465C19.605 4.4022 19.8231 4.72791 19.8232 5.08887C19.8232 5.44999 19.6051 5.77645 19.2705 5.91406L17.501 6.64258C16.9507 6.86921 16.5138 7.30617 16.2871 7.85645L15.5586 9.62598C15.421 9.9601 15.0946 10.1787 14.7334 10.1787C14.3724 10.1785 14.0467 9.95997 13.9092 9.62598L13.1807 7.85645C12.954 7.3062 12.517 6.86924 11.9668 6.64258L10.1963 5.91406C9.86231 5.77644 9.64453 5.45008 9.64453 5.08887C9.6447 4.72784 9.86246 4.40223 10.1963 4.26465L11.9668 3.53613C12.517 3.3095 12.954 2.87247 13.1807 2.32227L13.9092 0.551758L13.9697 0.432617C14.1291 0.167157 14.4175 0.000147311 14.7334 0ZM7.97656 9.92676C7.98238 9.95835 7.99195 9.98845 8.00293 10.0176C7.99127 9.98636 7.9817 9.95386 7.97559 9.91992L7.97656 9.92676ZM14.3369 2.79785C13.9834 3.65649 13.301 4.33882 12.4424 4.69238L11.4775 5.08887L12.4424 5.48633C13.301 5.83989 13.9834 6.52222 14.3369 7.38086L14.7334 8.34473L15.1309 7.38086C15.4845 6.52225 16.1667 5.83989 17.0254 5.48633L17.9893 5.08887L17.0254 4.69238C16.1667 4.33882 15.4845 3.65646 15.1309 2.79785L14.7334 1.83301L14.3369 2.79785Z" fill="#0F9958" style="fill:#0F9958;fill:color(display-p3 0.0588 0.6000 0.3451);fill-opacity:1;"/>
</g>
</g>
</svg>
```

### `src/flows/fno/assets/shortcuts/ipo.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="19.999" height="19.9991" viewBox="0 0 19.999 19.9991" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="announcement-megaphone">
<path id="Vector 3878" d="M0.713867 16.1284L10.3567 5.7998L15.3567 14.4569L1.59958 17.6427L0.713867 16.1284Z" fill="#0F9958" style="fill:#0F9958;fill:color(display-p3 0.0588 0.6000 0.3451);fill-opacity:1;"/>
<g id="Union">
</g>
<path id="Union_2" d="M9.71193 4.67366C10.0533 4.47671 10.4901 4.59337 10.6875 4.9344L16.2705 14.6043C16.4675 14.9459 16.3502 15.3827 16.0088 15.5799C15.6672 15.7769 15.2304 15.6597 15.0332 15.3182L15.0039 15.2684L9.78713 16.4793C9.91962 16.9502 9.92929 17.4511 9.80275 17.9325C9.61582 18.6431 9.15429 19.2506 8.51955 19.6209C7.88487 19.9912 7.12889 20.0952 6.41799 19.908C5.70732 19.7211 5.09983 19.2594 4.72951 18.6248L4.72853 18.6219L4.23537 17.7684L1.75685 18.3446C1.45065 18.4156 1.13376 18.2779 0.976579 18.0057L0.0957194 16.4793C-0.0613575 16.2071 -0.0222558 15.8632 0.192399 15.6336L9.47951 5.69905L9.45119 5.64925C9.25427 5.30781 9.37074 4.87097 9.71193 4.67366ZM5.68947 17.4305L5.96291 17.9041C6.14232 18.2116 6.43714 18.4356 6.78127 18.5262L6.91213 18.5535C7.21686 18.6021 7.53077 18.5445 7.79982 18.3875C8.10725 18.2082 8.33131 17.9135 8.42189 17.5692C8.48876 17.3146 8.47797 17.0484 8.39552 16.8026L5.68947 17.4305ZM1.59572 16.2225L1.94826 16.8328L14.2578 13.9744L10.2266 6.99202L1.59572 16.2225Z" fill="#0F9958" style="fill:#0F9958;fill:color(display-p3 0.0588 0.6000 0.3451);fill-opacity:1;"/>
<path id="Union_3" d="M2.63574 9.28516C3.03023 9.28516 3.35059 9.60453 3.35059 9.99902C3.35059 10.3935 3.03023 10.7129 2.63574 10.7129H0.713867C0.319378 10.7129 0 10.3935 0 9.99902C0 9.60453 0.319378 9.28516 0.713867 9.28516H2.63574ZM19.2842 9.28516C19.6787 9.28516 19.999 9.60453 19.999 9.99902C19.999 10.3935 19.6787 10.7129 19.2842 10.7129H17.3623C16.9678 10.7129 16.6484 10.3935 16.6484 9.99902C16.6484 9.60453 16.9678 9.28516 17.3623 9.28516H19.2842ZM2.92773 2.92773C3.20668 2.64879 3.65856 2.64879 3.9375 2.92773L5.29688 4.28613C5.57582 4.56508 5.57581 5.01793 5.29688 5.29688C5.01793 5.57582 4.56508 5.57582 4.28613 5.29688L2.92773 3.9375C2.64879 3.65855 2.64879 3.20668 2.92773 2.92773ZM16.0596 2.92773C16.3385 2.64879 16.7914 2.64879 17.0703 2.92773C17.349 3.20663 17.349 3.6586 17.0703 3.9375L15.7109 5.29688C15.432 5.57558 14.9801 5.57558 14.7012 5.29688C14.4222 5.01793 14.4222 4.56508 14.7012 4.28613L16.0596 2.92773ZM9.99902 0C10.3935 0 10.7129 0.319378 10.7129 0.713867V2.63574C10.7129 3.03023 10.3935 3.35059 9.99902 3.35059C9.60453 3.35059 9.28516 3.03023 9.28516 2.63574V0.713867C9.28516 0.319378 9.60453 0 9.99902 0Z" fill="#0F9958" style="fill:#0F9958;fill:color(display-p3 0.0588 0.6000 0.3451);fill-opacity:1;"/>
</g>
</svg>
```

### `src/flows/fno/assets/shortcuts/referral.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="18.3926" height="18.3926" viewBox="0 0 18.3926 18.3926" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="gift-2--reward-box-social-present-gift-media-rating-bow">
<path id="Vector" d="M16.7337 16.3395V9.04297H1.66016V16.3395C1.66016 17.1285 2.29976 17.768 3.08873 17.768H15.3051C16.0941 17.768 16.7337 17.1285 16.7337 16.3395Z" fill="#DEF4EA" style="fill:#DEF4EA;fill:color(display-p3 0.8706 0.9569 0.9176);fill-opacity:1;"/>
<path id="Vector_2" d="M17.7679 6.04165V7.61422C17.7679 8.40321 17.1283 9.04279 16.3393 9.04279H2.05363C1.26466 9.04279 0.625061 8.40321 0.625061 7.61422V6.04165C0.625061 5.25266 1.26466 4.61308 2.05363 4.61308H16.3393C17.1283 4.61308 17.7679 5.25266 17.7679 6.04165Z" fill="#0F9958" style="fill:#0F9958;fill:color(display-p3 0.0588 0.6000 0.3451);fill-opacity:1;"/>
<path id="Union" d="M12.6846 0C13.657 0 14.4099 0.287715 14.8984 0.829102C15.3815 1.3647 15.5188 2.05189 15.4639 2.67383C15.4231 3.13433 15.276 3.59147 15.0527 3.98828H16.3389C17.473 3.98828 18.3926 4.90783 18.3926 6.04199V7.61426C18.3925 8.37684 17.9756 9.04034 17.3584 9.39453V16.3398C17.3582 17.4738 16.4387 18.3926 15.3047 18.3926H3.08887C1.95486 18.3926 1.03537 17.4739 1.03516 16.3398V9.39551C0.417362 9.04147 7.40396e-05 8.37728 0 7.61426V6.04199C0 4.90784 0.919594 3.98831 2.05371 3.98828H3.34082C3.11754 3.59149 2.97044 3.13438 2.92969 2.67383C2.87472 2.05188 3.01109 1.36471 3.49414 0.829102C3.98264 0.287562 4.73556 5.99149e-05 5.70801 0C7.04718 0 8.08333 0.886404 8.74512 1.80469C8.91192 2.03617 9.06313 2.28114 9.19629 2.53027C9.32936 2.28112 9.48065 2.03619 9.64746 1.80469C10.3092 0.886372 11.3454 0.000144661 12.6846 0ZM2.28516 16.3398C2.28537 16.7835 2.6452 17.1426 3.08887 17.1426H8.57031V9.66797H2.28516V16.3398ZM9.82031 17.1426H15.3047C15.7484 17.1426 16.1082 16.7835 16.1084 16.3398V9.66797H9.82031V17.1426ZM2.05371 5.23828C1.60994 5.23831 1.25 5.59821 1.25 6.04199V7.61426C1.25011 8.05795 1.61001 8.41794 2.05371 8.41797H16.3389C16.7826 8.41797 17.1425 8.05798 17.1426 7.61426V6.04199C17.1426 5.59818 16.7827 5.23828 16.3389 5.23828H2.05371ZM12.6846 1.25C11.9303 1.25015 11.2216 1.7597 10.6621 2.53613C10.307 3.02898 10.0649 3.55811 9.93457 3.98828H13.2197C13.3646 3.98828 13.5852 3.89269 13.8105 3.60449C14.0289 3.32521 14.1853 2.94106 14.2188 2.56348C14.2518 2.18879 14.1618 1.87897 13.9707 1.66699C13.7849 1.46092 13.415 1.25 12.6846 1.25ZM5.70801 1.25C4.9778 1.25006 4.60868 1.46095 4.42285 1.66699C4.23158 1.87907 4.14163 2.18945 4.1748 2.56445C4.20829 2.94173 4.36392 3.32536 4.58203 3.60449C4.8072 3.89245 5.02795 3.98812 5.17285 3.98828H8.45898C8.3286 3.5581 8.0865 3.02896 7.73145 2.53613C7.17187 1.75958 6.46244 1.25 5.70801 1.25Z" fill="#0F9958" style="fill:#0F9958;fill:color(display-p3 0.0588 0.6000 0.3451);fill-opacity:1;"/>
</g>
</svg>
```

### `src/flows/fno/assets/shortcuts/watchlist.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="19.8223" height="19.8221" viewBox="0 0 19.8223 19.8221" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="task-list-edit--task-list-edit-work">
<path id="Subtract" d="M16.3392 6.93546C15.7591 6.98869 15.213 7.24336 14.7981 7.65912L8.08379 14.3877C7.70114 14.7711 7.45342 15.2685 7.37786 15.805L6.94929 18.8478C6.9329 18.9641 6.92485 19.0805 6.92483 19.1964H2.05353C1.67465 19.1964 1.31129 19.0458 1.04338 18.778C0.775469 18.5101 0.624959 18.1467 0.624959 17.7678V2.05353C0.624959 1.67465 0.775469 1.31129 1.04338 1.04338C1.31129 0.775469 1.67465 0.624959 2.05353 0.624959H11.3392L16.3392 5.62496V6.93546Z" fill-rule="evenodd" clip-rule="evenodd" fill="#DEF4EA" style="fill:#DEF4EA;fill:color(display-p3 0.8706 0.9569 0.9176);fill-opacity:1;"/>
<path id="Vector" d="M19.1972 12.0544L12.4686 18.7829L9.42578 19.1972L9.85435 16.1543L16.5686 9.42578L19.1972 12.0544Z" fill="#0F9958" style="fill:#0F9958;fill:color(display-p3 0.0588 0.6000 0.3451);fill-opacity:1;"/>
<path id="Union" d="M16.5684 8.80078C16.7341 8.80071 16.8935 8.86621 17.0107 8.9834L19.6387 11.6123C19.7559 11.7295 19.8223 11.8889 19.8223 12.0547C19.8222 12.2203 19.7558 12.379 19.6387 12.4961L12.9102 19.2246C12.8135 19.3212 12.6881 19.3839 12.5527 19.4023L9.50977 19.8164C9.31588 19.8427 9.12047 19.7764 8.98242 19.6377C8.84467 19.499 8.77949 19.3039 8.80664 19.1104L9.23535 16.0674L9.25781 15.9688C9.28769 15.8727 9.34038 15.7848 9.41211 15.7129L16.126 8.98438C16.2431 8.86696 16.4025 8.80087 16.5684 8.80078ZM11.3389 0C11.5045 1.07367e-05 11.6641 0.0655475 11.7812 0.182617L16.7812 5.18262C16.8984 5.29982 16.9639 5.45926 16.9639 5.625V6.33887C16.9638 6.68401 16.684 6.96385 16.3389 6.96387C15.9939 6.96364 15.7139 6.68389 15.7139 6.33887V5.88379L11.0801 1.25H2.05371C1.84059 1.25 1.63605 1.33465 1.48535 1.48535C1.33465 1.63605 1.25 1.84059 1.25 2.05371V17.7676C1.25001 17.9807 1.33474 18.1853 1.48535 18.3359C1.63611 18.4866 1.84067 18.5713 2.05371 18.5713H6.33887C6.68398 18.5713 6.96379 18.8512 6.96387 19.1963C6.96385 19.5414 6.68401 19.8213 6.33887 19.8213H2.05371C1.50902 19.8213 0.986615 19.6047 0.601562 19.2197C0.216455 18.8346 1.07878e-05 18.3121 0 17.7676V2.05371C0 1.50906 0.216446 0.986681 0.601562 0.601562C0.986681 0.216446 1.50906 0 2.05371 0H11.3389ZM10.4443 16.4473L10.1592 18.4658L12.1738 18.1924L18.3125 12.0537L16.5684 10.3096L10.4443 16.4473ZM6.90234 9.39062C7.10293 9.10981 7.49355 9.04465 7.77441 9.24512C8.05529 9.44574 8.12053 9.83631 7.91992 10.1172L5.58984 13.3789C5.48306 13.5283 5.31586 13.6235 5.13281 13.6387C4.94993 13.6537 4.76948 13.5877 4.63965 13.458L3.24121 12.0596C2.99748 11.8155 2.99743 11.4198 3.24121 11.1758C3.48529 10.9317 3.8819 10.9317 4.12598 11.1758L5.00195 12.0518L6.90234 9.39062ZM6.90234 3.58594C7.10293 3.30512 7.49355 3.23996 7.77441 3.44043C8.05529 3.64106 8.12053 4.03162 7.91992 4.3125L5.58984 7.57422C5.48306 7.72365 5.31586 7.81883 5.13281 7.83398C4.94993 7.84905 4.76948 7.78299 4.63965 7.65332L3.24121 6.25488C2.99748 6.01085 2.99743 5.61509 3.24121 5.37109C3.48529 5.12701 3.8819 5.12702 4.12598 5.37109L5.00195 6.24707L6.90234 3.58594Z" fill="#0F9958" style="fill:#0F9958;fill:color(display-p3 0.0588 0.6000 0.3451);fill-opacity:1;"/>
</g>
</svg>
```

### `src/flows/fno/assets/signals/booming.png`

```tsx
�PNG

   IHDR   �   �   ��E-   sRGB ���   DeXIfMM *    �i            �       �       �       �    ���  =IDATx�	�Օ��릛��fߑU\0nq��w$�����Q�ct0�F4��e��Q�A�A\��������b\�2��N�l�����|o������-U��է�=��]~u��޺�F���j �k '��d-�SF�zM�
�`4�@��@��To� F�zM�
�`4�@��@��To� F�zM�
�`4�@��@��To� F�zM�
�`4�@��@��To� F�zM�
�`4�@��@��To� F�zM�
�`4�@��@��To� F�zM�
�`4�@��@��To� F�zM�
�`��1���q�Y�\��6��G}��)f}rF�K�.�իW[���۶���[O>��M3H-��V ظq�A���l���t��^����̙3o���֦���@�QO��c���O=��رc�)v)Y}}��iNXCCCnn����_|�EWG/A�I$�IR�MR9�
����* �袋\v��L]�ಥ5`��5�#�g:u�+�����^� �U3-�0ڢ���5k�p�8�opii)�*��p�Y�=�̊�a��q����=����������@�G�_W>��;�����;�[n���/N���������'�7� ���R�{��Ǔ���j �( �'��?��Ϫ XG�� �7�;＃���
�$5أ��fbb�J�q��-^���ȓ&Mz��g7l�p�A5)�5`Ԯ�f�UUU�;wV�/��r���z��(++�޽;�[�l�۷o"��סּ`�䭓&8�s�J`�6��w���^��ׯ�W_}�)D�5��&����)�����+kϞ=���b (ӗ�L�#hS�Z�e���FL���N;�(�&�=5���"K��+F��T645�f}}mm�~n7�]�>�`�W]u�> ��3l�"�=zѢE��b?Jn'�ż> wo�M���S0衇�IG�?��sU��ۚ����� T�I��qŃ��D�;z��Gu�< �H�B�SM͛7O�Deee+o'SI��秎�WTT�B-�V�]��FG��@�@��@�eA�}G�=@�<���v�ԛ](vh��i�Q�f�F����MjV�Y��E���5�����ڔ��sQm��ij��r*��i�	����ʵ/���X�v�Jw�ڵ�4h� T~�(�'e��ĉ�heA��A��FzS��^���F���*���hN]�����l.��2�I�92���qm
�����ڏ\��c�$z��^�4�����I'��8��Dc������#���ǴL�h�&߈'��k�I�x~4j���i|1�o/LѸ;w[p�y��U��G�� ��.�N�l�kv?��m5��i�q}��� 5�Ճ�(�.ǟ�%�Ϙ�u<�y����8�ɺ�<� �Nu�F���V
��H"L�m�ݼ-�P��܅��1F�]+��dtWfR�2�0J��d]�� �"��Z�`%���@0�xX��S����ӧ�Iq����9��t�(È�T�>��|�'m�6q�ϒ;��
Ss��r�ڤ�A�'��sI���e��0��Nm��� �9@����n�T2��%�Ѡ`t��%�NN��$�V����P��8��������N��!N�6��?^�n����A'u�Q�`b��{�,qɷ�2��Ή�B��eKk�<>�a��~�Ӊg��sĖA9t�N,?]�l���u��?��۶m��b�9|�k_;�p�'�k��$�fW��́b�FY&\^^�)�T�K�,�B/����B�/((`;v���GC�p$'T�ڋ{N/k��6b���P8;�u�h�/]�|���sG�����>ߺ]#vh���6q/@I���g��|�`ϔ<j����
~q�h��P���c mV�,��Ŝ�F��M}���d8�f�G�����20���F8��u+֍9��P�hä�;�:�T:�_���I5
冁_�I:f@��q�G��L>��e�1���{��o���F�zp���c΃ۆ>����B!U��>�<5�9v	b-H�rV�} X���l���h�.]\�����T��tX�+��>�^1��?�_^(D/_��W"ݺćJ��uNa|V$؂XI��hM*�B�i����Kon@�t��:��b��k*G���F�W[x��'��?ӌ�Zr�8kV~X��߰
Ц�o�U]-)�[6��L�;��}���܋636�;3x�y�x^���݉z۴ˇ��3.	�b����Ү;��K^�+*�c�{�>�0�����O�>WW�D�رc�$�T*������h�R,۵漳�NO��:�c���͙�F�NE>7�Vm�1��a�M��
�ݚ)�T�N�|=*�����&��ynt����F׭�H�qB��vlolв�s7t�:h�+ܙ�ݩ� ��SO+�h��^Zܷ�"�D�V.G��=ץ.�]&җ�;jN����B�S��ˠi��� ����3O����Q��N~�De�� ��������P����У�߾��p���:����K��z7���t��D��	���l�4�VzS��A����������ᥖ�����_��x�D4z�6(#�����������ŕh�A�<�{���6>��,�6N�5ɥF��+ &����!1~��9�����C�J�͜:.Y��ڙ2���P�w��r��r:�5� D٬�b��A�	4q{mk2�m.ۯ�m�O��o=z�����G?V0��mV86a8T�T�G�G���=�,.:u\=[�D+�^a������З�d��,����y �5�����v|���F��9P�t¨�<�>4 H�$	��S_k~4��}$
���^a��.�@-76<2f��`��=R�05O�(��|��f'Hҙt�y0�ñB�GZ"�Ig��K��1���j/39��թ�sˢ�\V�6�Įp�<�(4�%-�i�gt&:w&�M�s��l��L�Ad��c����wg�Ɯu��i��w^~?��nA=��k�#~@�Cx�J'� K���D��6_܃�^�]�\s��(�^��BCo�1�>c��D����s��Q�D��-�}�tI��W�߰�O����
NT(���QZ	�*��D:a�w��Dze���hf��K�f�n�T}�掯.Ak���Gw��t����4��=�$�rF���o��*�&0�~(s$�mfRI�,�|�(�O�s:a�w\�[�R�(�$m����4�]�R\�ϐ������S��]|��Ƣ��7x������E��C"��M&�U�����H��}��ޙ�N:�0�GKJJUe�^[�qI�f"(�ec�Jq���T�(g����w���8��� &l~.��K�e��t�`��Q�hМ�����3=�-�u���x��?�O�B�ۑ��4Jb<x8 ���H3nٿ����%b4[���a�<�o��R
A��h`�Ql{B���i�c��ٴa�����z!�i�?<�� �705�<	��"Q< _N�@&T%]�h��;z�f0�CSf�n�'�^�����< ���(h$�:ڱc��)�i6�PK��H�dyi�DԝNRV1=ʈcHn$L8�~�D�֚^��-(.*Bw�B��:��wɨ��P�_%��u'|c�g=D����uy�U`7�[����6o����:�lb'h-��"�v�$5�<��q@�{3%y%R�H����g���*f�_3cA=�� �˨Ѡ�8
�$�t����bz��6}4���E��'՞{Vɷ&�H*��^�+�����2I�d!�K���q�7��������)%�R���}��'����o��+�ߩ�����i���"��jI��%�E��r�m��$�ku�.�e`R�p�u>�X�pHi� P������' 5Ũ�����s����z���]��$e����(��N���=���L��0o�8��=zhR6!7���3��j�z�[�n;�����=_�z��'�VF���ꦑ�nym	����HyaT��;�)��%O?f�s8K:��g�ؤ �>����u���y��AJ��:����ϩ��;;w8wQ��D'M~����S\��v�ܙH��&1fP�,���@��(q�(��D�a��Cqգ(�;�%\`�&d���%Al��rf}zr0��e��%}µ�X�K��8�h���3�ƏY��>�e�$��B0���'q�J�J��p�����d�<0�|��7Q�s7s��E�:��6B�J������@�F};&Q8��0��i�$��
�qt�#� 4(6���&v���۩��������ILϜ�� ��!bz�L�Mkﺿ�ĳ\���)AA�R�]�T��(����נ!\��"�J���9�~�)boQ���V���/�"�)��K�AR�����6�0`D�����֍�Z٦����&���]��I�m����	4�/f�3N4sF��h��>2-Ց*��.V�]!�W��P%�8��S�H3�R�޽9�C��Q��Dd��;B�Np�����!�����?�t� �>��9�|��z�XF�,�ki���V�`S^�A��&���Qc�H�A!^*�[��%R�Ԇw]ժU�\��bWh�\�F�:�,W݉z��9���L�3��
���	��ΌP��E��ݺ��7ϭ��b�7�y��;G���6��M�][}J��<�cX/G�7ң��i�J��'EV�MPR��o~�[����R�2�0�z�J�X��m�#�[�4'�jcQĈH,ל�Q��h���bџ�̟���v� ��u����jP��ȡG�:����B�V�Ho��#��0��3�^��ʷaK=;��ྒ�vk���V���2��l��8b�$� �ى8��F�.�u4Y�+��D�~i�óK'O G�X%?:�$?dI��gR�^��6.x:�)���'����^�坤��Al�ﭷ��u�U���L?=�:��{�����їĥ[�����lW?}.򝊊
�OC���s�*:����{��1;?�ӓw�����v�匱P��X�K�*gI����1`rTx,w�|�ѵk�z+A�`tz��ddK�����D>W[���Q�즛nrU��Q�h$t	� ",�M�~=��}`��x+��0Q;�q��a�zm�T2r^R,QlC��v'��ʆ���bP}y�wawJϙ|#&�U���3M5O��Oy�x�$��T��_>AD�ٳ'��-/�+���b^w�u.Nj^�%F�>�hWm>��6��Ac)oá���vkU��4}U��=~�SLF`�e�&����NɆ�N��y���ě���~	�*|E'x�ٳ����g�=�}�^�/f�Kh����5ɜ�X�vjcǎ�/S�NK�~��_wU���L<��i�5k����ޔ��9��d��݇Bt�lL[6@����!��	�G,�#�/,y�Q�$[�<<7I�!g������F�:������<]�J}5�ʕ+9�	�����]�c������N��K���n�w���g��O'b�w߾x�Y�a����:+��u��A�x|�.���9횊>%�*R|`�g���YM�"����{~	����.���g�v����.'�._Ky _W?I��o�l| �z�>��L���Q�wp>��W��M�BP�X��[�,=����
m���_u����0k/ȳ*��̪�i� LЩ�,
M
�u����N��z�o��:p�b&�����7H�<!�0�%��'y�"�<F�w�����GZ�3g΄V�F�)H�+F�9�Wm>���.�43����Q!4�˥O���*�|4�<�q�S@�,[����"#ݽ�N�����M9��Y"�E��圳m��u+���+��R�<Q`�W�&��);k���}��`�i�QZssܸqvu����Mͺ�.�U��Gc��@��pL@�o�N�o���d�f�J�6��� =z�����P�Z�)��SU�
LM�P�S4�r��d;ę䌽%�<Q�J���a�z�H鰰������%�i�Q�.������x�bo�~��ީj�M�,4�׌B{�}�q�޺�IM�y��ŷ��1�S�P�x�Z���>��f��ݻ����.AO�W���L�#�긁,��yD��yI\�7�ln�.GZbT*w���Z~��}U)���7����UUո{j>�d��t��V}����82�sA���P�	�!�U슘��B�&�S��r�?���=���$��%�D���B�$��ʋJ�g��[A�y��K&u.��(B�ȉ�����)N��IT)�5��:z�X�.0�M�l�(�~�t�ٓ�%���R�:�B��U���}�lJ]����{yp�%�}{�"�Z��XXD��.���K�����K:�1J%z�{��o�Y�V5c~ѳ[=�Y!�=�*-^�Ǟ1 K�D�
�9ӕ���^Jf��E ���_�I����D!����^�}�'zX,Q��:s�`��!*إ�@�����Fb�ԩ.N�_�ӷ}�2f%�����O�E�_�wÇJ��(0j"�YVٙƴA�(�Uh� f��N=.�V���_L�0��v��T�3�Wq�  �%���P���C�;��<�x����99��y��ZZ�'Ry��&�<�Z|W��,�<웦>ݨ�R?���>jτo��B�.az7 J�/Z���]�b@%�n�KA�hP�M�w��]���Yw�]������	�T�D���6@A� ��wߏ��ֺp�kCt��{e��X�k��?���bz�rŉ�8I�^}��X��<�@�L��i������fb���^��Iyyi=����v����U}�T�H.�u���-�[Z>�_�E������>�h�����{�������76*Q��ʪ\*@�Ә��8�<Ep��_)��#r������s��)C��z�u�)S��8���}=U<i�$�|=���6޳���c��d�[��̸�q '�@�3?�;]ye���	�熾�P��?��Z]�y���v-?���cO��w��5�_�Q�oZ�`�w���iK*�l�P�P�h�o9��W�֫!R�F���q��������b��,55�t �\���OC!-�7��F&��	�m�?�x�1��q�Xft|�Q��4+EJ6n,]�v�I2�)��u8�5�Eo��p�I9��D�wע?�}3�b�8v��>Р`q�#u}���'�M�:w9�%��X��-!X�����z���8����"8��mx,ǌ��Y�f͘1C/!R�#�v>]t�cT�C{����3ϰ�͸9�E�IK1�`���i��C�8�n�����K���J��Q��GE`zG~>q������Y�Q�X���]"�������|ܮ�3�{�9��5*�0Ov�k�X5 �J��k���w	����D�cT*���k�W,�q���������-O?�*$ы��p�C�eR���:e�d�TeT
'	:E���T@��[Uc��s6�]����Th+Kb�shw0.\8y�dISμ��}���tڏ�����]u������yBlP�p8l��� �y
S�()���X�����m��3���Pњ�]�Ih�s�U{jO_�w�#s�v\�v5�:t��&�E��=#�W\q�-�R�4(���J��/ح�O
����`x�Pi������6�	Y��
J��⨘�w�R�*Δ:�	.�}
:�	*hFeJ�Zg�hC����y:�hq9�EzsV��XO�)W��ܒkﱻ���Ozљ�QPH���t-��3g�4�`�L��!b�EQ�6��"/Z���st� *�T�	(�uȐ��_V8�Ҝ��ζx �2\ ���4'Z
���ώ�8�桗�!�-O1��Č�IG!O)q���[4�(Q��@�ә�Q�b�p�2�u�(�)J��Ep6�ȳi����m���RtjDЙ7㺱>=c�g��_�s��ϩ�pʪ���3�Ngn���R����k�_2�8�̧��L�>�k��(�b������|�E��ְo� ߾L;:C�LZ隆r�믿������z+mɰG/v8�ͩe)F^�	�M�&l�S�.�)Lѝ�ҭמ|҈���a�A:��޾nŚ�f�s�tdEYK<V-�������އ�w¸�a�9f���ѡ�Q4(݂�����MY�mo�,>Q�U��3�4�ko=��Q�"���ʣ��bxm0E'�D �B�����"���s̱U�|��_��{>N%<Jg?8�)�O�:��� %^$vOgɒ��<]�Dpf�0,IS<Mt���
��ӵ�F�7��c��󌲹ꪫ�{�W����O#k'4凰0� ���P���X�zk4(�B�=���oM^��]��Kw�y��# ���'3I%/�!�=06b�
 
":h��#�����#d��u���q�k�����\�#�iz�6�����`?ZtU~^7�-"���>����^\
��$g�)#w��#g=��̣�2�&�e`��)#wFEpvT���y��;y��a�"����3�i.�#+`�#Q���L�B�4k���R�i���)���iz���r޼yvA��U}�	�v�i_��צ�t�C�Y%�������=\f5�(@I3/�ׯ��S.ﻻ'(v'&��DY�e�n�H�C��A��z{"��]�\ ����.N�Й�Q�7�]v�k���_? �G����Ju�$eT�D:0"t��8�B�'��9d�e��1���N��JT=޹�>�A�KX��?g�K:u�PA�r�����{.��C%�MR6?���iچW+�+�4t~�0/ۈ�̷s�q)�6.�����v�2r�m�^3M<�8>q-ń�.^%!��ᚪ����Y��e����`T.3�^���Ze3�y�� ׾izљ�G��i9{�����W)A�G3�Dk���aÇ��ک@�) �龽s�*]��� M,Q΀� (�{ѩرS��y]dx�S JI���J;e��:Ʋ�iJg&Fi`ڃ���ѽeetϨ�֔&��4(�tT�Oo�q��_Ϗ�|r���')l�d%.R�Ƣ1:q�:���)�}q�#/ ���0@��O{�1J�����r2�
�(1;R�}�hP;:@m1:5���F�F\*4��	唆s��Ƈ��ܸq=>|���,KF �zQ�(T�V��GO<�DM�N_zyJ���D&c���;h�5�Sm��b�޺�P��|ѝ�>���I,;�=*���֚���Tr�}���e����l�w82��[Sܜpd�^�?��BS���o_f���2�<v)D���d���ʿaW��z) �R	�	�·�]���O;)_:ǙCz�ѧ$t���<`����YP���
CY�0����4A<n.Ǿ�5��������_ۮ�Y�d6��V�@�D�����$kkP8�Β�=o�[���yQԫ�������穳���^�8��i�3��|��6����?]X�cHRw^�;w��m���)꓅�r P��]@)��P�) %z�1���A�J����xO������v,Q��锓ID��3�L~e���E4����˔��D�N�*)��Nר�Dq|�"�HqjC�K��llzk1�Q�41*"�\���E����%�cKo�������l�(�Ǭ�=̿��~[��b����C��ۜD&2�gڒЅ�]@Dw��|/yZ�������L(�ĸTg�Y���U��[����'�1|SNkfa�v�;غQǗ���a�1�ڿ;W1���=6��|5����ՠbit��?s�5��.�*_��W��{Ȥ<�Uz�v�s]��2���1��K��$ᯨ��]\8�������HІ&���%#l��4Ьs~ʁ ����B�o[�"4�u��9"���M�]�},kJrrrР �����~��_�������sυFL8y����&����dvq�Q���MM�5$�:5T	��4bΘ]�P#h
%
�۹(���o�~�Ύ�(G�C* E��F��:�k����]�VT�b��O�/�扡gX}���{1
���`Tѩ� �H���voh�C��3�ԳԣM9�+���=����(��0=8�7��S��n�)=�6����KIЅNť�N��u���Pn�ࡧ��{���\@�A�J=d5F��4.��s���t��!7���U�0����N���g�@S�(�e�����J�J�3�֎7k��8��I���G�qȃ�� tz�ḫ�pt*@A��]��^�!��ȪA㌬���u� �SyM��ʿv��B'=��\p����)�-���Hi���)| �3'�v$�ֹfAS�=l��0{�l��ii1�n��v��?��ml�n������f}�=���V��8	����	� � !| ��ܬ�b��c$�l;����.����ԋND��ӥ;����	�)H��ߢP��.{I{�ġ��*��G���G��Q=�&�\脓�6:�5�d�8%��/�Ȃ|���sVۣv{KE����͋%yQ���]
"�'��Ps�:�~hP;��Fu�8+9@/B	L;ʷD-)���)?����S�>�q)ДX�S$�8�P�csE�kw�H�]�$�=ժ0����|���n ��Ƿ�hj��&q�����6.%�F'�[���e����j�YK�h��Ǒ�K�h��-<��"UU���BP�(A�a�܅�0�R�:U^��N}�����6@�P�ce�Q���H�ER����O>�u� �F��Q�lkP����G]������rVi��n�a�ڵ��-�Oβ��ф�N�O_>f��[꾫���8�	:Ee�2%����BPt�z=mŉ$���3}�Jд�mY�͉ �	�4��\�un�6����~n����
:�����K�������vh�g�y�,��Y><�m� ��ղ�) u��BE����&�y�J��tA09:��1�_{ظ	�(r�����5`to]$�4	2J���y�c�ݿ��G���tuߚ�bԅ]���)SN��z^�@}ƭO�ӚT6F[����*�/�����"�BPA)���
tn�ϛ9w���������LdS�`\��֦�Щ��~O�����)� 	:�x��Q�6}~�w.5��k�4B�G����=����u+~s�%�#	�ZS����5O=m�?v��(���*JBMR9ɂ�"�_����. ����<���c�NQ��}��MV����6���\ŜS��8R���ܕ/{w�*���~�\wu(� u>��h��%w�^� �m���/b>�Mbe�~˒��u�=����W��t���忯5`t_k�q<���g��f�!��w����TC�O��Z1�a�@4�%�Q��5G��Ӯ�}�=��֌(�PC4��lFE5C�]0�L�gv�,�6�`�"�p�i�	�M-8;9����H:v��C*�ť�)����oK�O����n|��_�~`4S�>�h��x�{��쟽Q�'G+l	��~:�Ton߾}o�l���d;��>n)��W�������ڟN�R
jI��S�h���d������$��;/�>ϡ�'�(ݟ���������v�Z�J�����Tr���1����brhu�S'�F�A*�̇� D�	F�߸^:�C9D+���tU���l��h�"i-�?�x6aTV#dK�G����ǊP3�t�Q�S�N��=�	������l��}B�$
L,�/���ɼ��{|�a^�0�蜃oz(�Ȥ�	nV�>�����'l�%tʔ)|��/�f�B�g�1n]n�B|(�M�a��#�[i���;�Wy�E�Sg�>5���)���o<h���9�f�LF�A��2��T)7�={�ҥKO9唩S���ű�i�{"ϳDN^~�eԪpZ{n���W��_K���.�c!`���,q�$���jp�c�ĉT�<�pD�(����ϷV��"T?��w\J:���ȳ��&��a���e�eډ�(G��jѸ^B�HS���h>�d�,Q9ʷ��r�K���I�畔
��S.J��]2O�}�L�t���Fm;W-��__/�R#uܸqvF��J���� :*�0��3�Uj�xj�Ē�4 o��v�
�q��$"g�����4eT�D!n��[#���V�7�dEທ�3d��t�ٗ�m�l�M�lw�W*Q%�)&٦u8�I_�0[v���V=J5��*�1iB)�&�XtU@Y�X��XtAI⊤b�J�F��*	�I��7�`]�C@njcTW�$�4�ݨZv%l����I��4.�ǐ�$�dޅH�\5�z��6���rkכd�Ξ���D����H�����Z�|��UhJ,EJ�v�R�B�F\�/���k�	���vI�g3_z�%�H��[�r�ܹXo�<����_���
'!�����^�=�P�������ca�J!f%����rot�����8B>#Iْ�I�9mN���I����;�8�����iPk���Q�h@�H�xhc~8�hɺ|�Zvytd ���(K��d[+^.5Y.q��(��]���a��Nzɒ%J
��\�|��p�QmF|��$��M�F�1�A]�`s;�@�{7I�G��~��#�����ǽ�i���]�U`ᨩ�e�(�X�}��}-��ݭV�A7�ln��!���KIJ�|���oh&�t��6��1^v�ҩ)�/)^lM��}�С��o'b�aT:W����`#F���%�{�职ZW^ jy�;_|���}����?ZJ�[J����|�ۛ�<N�)2.��Rs��>+�|rΩ���8t���x��@8���B���H�r�u���7���0�\�5p�	'�eII�K+V8� !�b��Ըj�� X�ʥ;�ښNJZK���%::���#�����9�vxWD^�����[��v�QJ�#���}�j�*Q�0`��gW�]X ����&�ض���Q�.�Z F�R��h2A�i���|����GMg���Ml�"qIS�Y����S	�@3/�Qi*�ZhD���x�!ȿb1��=1g���r>��3h�=���5��J`�j��L%$A���,vQ{�Ȫp��w$JAue���u��ID���l��TQ��$��8�}��Z�>v�xIAe�����.۾���1a5"�})٠\.�fC\EE����j�Tas/)��w|���w�$����Kٕ#�=��z&H���ߓ�P��0CM�]�v�R�v�R��Flxi�(�� 9# 4騀T��/�J���0"UG�JՓ+���G�� �V�֢i�A�A��Z�i0���;
S!W���Dlh egώ�H\�d�4�X�;� U
�3�Iu�#LN�� YeLG`��%�#Sdt8���Oe�:A�Knm�]�vY?*ݺtjr�����\]�
@`�oݺ�/cK�.Ul�5.��H�W>f��#۝,A0%�(��-U&2�D���t \�,c>�o���@�w��e��b�h�]hɭ+�",9y;:4L�<�/_@�߿�̞���K]rr#�%�J"����x�!�E�3_z�O0��x���X�T�jC"���]0�����c�Ԯey-��輔��wi���3��VL�@�ʱ��ivi��*q"�("⹑�$g������;3��1�u��(�#ɛ��Dc錻�ྞ�;���h��62ڦ��Pi���d�����`!)w�)�ٛ��3iŐ�dƈ�	�(vag�\œj��x�?c1괲�����%������q	�\L��p�����("� #�� ����95���X�jd"d��!�	�D+�V��4�p6��2V�";�ߜ���Wl�v�󠳿�b;;��s������ϖv?�8�d�g���Ӳ�j��&B��G�$k�r�TU�-��Б��Aߞ��E5iV/_^��{�.��]�Pn��u;�{����t�f��/��q�?z��l|���7J�7�:�[vq�7������: �7�����;�g��ϟ�E�i4t�ó0���o��D�������� �DL,�JM(��������a�C�����FJ�sェ�Dyu����?��P�d�d�/�yA"��!L��F�刭x~���[��|���Y����j��?]�Ll���Pa�S�35ʲ�bӿ]�㒩pB�.���SgLc*!�Gá��e/�4���v��C$�;:���a�����Za�!#_yv˿\hR�ŏv��'(Z �@4��,ҭ����ȩ��_n��^"�D��s��]��!�R�?����hF���#F�����f���Ĩ�",'T��'�9�߯/y������7�����+�ۉ/0�Qc|t/�:��>/�qѴ��Q�,�� �#��EWn�dU���\n]��g���Y�j����vbE���eKK_{�Ǆ3Jwl#���E����s�c�Oc�j֝�\e��5[�5T�|�ү*6o��33*���1P���^���9(H��ѠЩ�	A��}�=� |�e���������߉�?����!FpÞ�^�<�����^���;�{�c\���[��@���X�����-�N(8l����n��m��3�R��ekr�p�I�'N�s�Y��<D;mm�D�".��}����jV.߱�s���dî�g�t�Ry��O�:�̼:G�@�(�͟�;Ia������y�@��U�t��s�m����s��7r�x��hie]��:�9j��-'�S�vͶ��C@�%Q���M�϶U���s�fR\IV?����=��6�`�h�#W�E�y#�@�]9h�Pٮe��4|䨢Q��w������j���WF�V\T\VQ�W���K��z� �����*v�o���|�`lM��n:j�|a��!]ס��!#��䁃|�Y�+6vxm}-��SÖ�����%�*I�7�h��R��|�"�ź�d�931j@�\�s��Z��g:Gg�Eh��1	�$��������X��xFR�� L�"э��~�rm�E"l��^��q��1<�b�T�����'����2�fb��2Ps�0򶽑�!&_��7� �A�Ń-phN��8�yl:�ֹ���4ƨ�!8�ӳ7�qn�h���%�x.2��b4�.��g�<YT젨iTFӨ��4�F���Ө�FӨ��4�F���Ө�FӨ��4�F���Ө�FӨ��4�F���Ө�FӨ��4�F���Ө�FӨ��4�F���Ө�FӨ��4�F���Ө�FӨ��4�F���Ө�FӨ��4�F���Ө�FӨ��4�F���Ө�FӨ��4�F���Ө�FӨ��4�F���Ө�FӨ��4�F���Ө�FӨ��4��3(�>ˑ�    IEND�B`�
```

### `src/flows/fno/assets/signals/gold-bars.png`

```tsx
�PNG

   IHDR   H   H   U��G  ciCCPkCGColorSpaceDisplayP3  (�}��K�PƿV��u2�C��
�8�DqU�ꔾ����G�"7�����
�n�::8�������y/��"z��~|��8 9npn��;�[\�+��-%��� �񜮯J��?��>��N�Y�������1����]H�����%����qK���r��g�X �&VXͨ�������`�r���l��9�X�<p�0Є�?�����]r7�R��|�ɑ"'���p�0�XC�R�w��w�O���'`�#�����p6G'k���<02\�����G��V��S`���P϶W�j���<0�(��$�:�-!>���S�p�|�b��[   cICP n��   8eXIfMM *    �i            �       H�       H    ��d�  YiTXtXML:com.adobe.xmp     <x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="XMP Core 6.0.0">
   <rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
      <rdf:Description rdf:about=""
            xmlns:xmp="http://ns.adobe.com/xap/1.0/">
         <xmp:CreatorTool>Figma</xmp:CreatorTool>
      </rdf:Description>
   </rdf:RDF>
</x:xmpmeta>
�\�  IDATx�[i�]U��^��^ͯ�R�T*		!!$! �$Ddꀍ��Z��ݸ\�liY���i��;2hC�[�A����P��TR�<�s�z������nQa�U	"?rVN�{�=������}�9�8�N p��@�]p�ק7~���|�@��㘆�(:��с��=�p���iol�X�����a�S���҇ �Y��Q��������t�� Y��Ș]�rk���ڵ{�w��u��k*��s����?h+���hw/���������!cVF�쮁���+�m����"j���3h���q��޸e�ݭ�e_��O��%@ @^�$^�X�X�d��7���hOOlK}E���~���;10ݧ��C�Ӷ.�zo�]��WD�G�ę#��,�:�g�^އR�H�-���GKS������7^n|�G봴�F��:@N�%��R����qM4:�@(���G�q�K����(@�	8���ŘH*@[�XmCy�#������/P7�ڄs��K�Ug�,{���Ί��E�bH��"�R�'J���k�!P\V���쌏�~d�}YsW��f`���PG��(;9G�4P�nM���g:*[W������g���J?M�L��<�'���=|��8\����D	�9C��(���uX|<
�<uX{uUq�����x���#�B���ѵ���	�T��Ԏ�%�e�/��+����8��n�5�5W�KN�t=�y�cU�gPG��7��>����!�p��$3��eZf^,����`d�1J��5K�=I�d7� ��Q��~D���[����X8/v���{$��� �n��*w�yo_SG���Bܬ:]'�-�s%_#S��)��<�P�?�>��w"J?�B���hjC�sfA&V}��8�u�<}gݞ�;�:{}�q��|�I��S 2�#c{�Y{�0�Y|?���>U۶ #s
�Q��
~���FG���}hr��Rj_}�g�oB(��H8]�cG(�:`+Yo��dvW2� ��S�ͻ�;vc$��-���5��J�H���7�8�<qؿ\rz?�|�_6l�.:2�@2N��-b@"Ki]���ڢ�D��Mm��9�`���;�L�"#���jL0~r8��(��T���#��Xɚ=3�Vb�E�SqA���߶�T]7Np䌵U0��R�e�$J�d3n�!����\v����Ϳ
�;wch��������q�&8�O�!��>Syy�(�~��4R�fa͞�G;ʛ>>N��d��Cʋ���U�{SD�R��n�E��V��P*|�.B��V��eyQ����#dDM���sfaWr>�?�r�Lf�(���z�W�Q�������I΄m:MQ
:�!Ki37ֻ��L'aR ��Tp|���}
��؁ѱ(�s��!8j�e?.Hf]�#s��c�� V�l5�9�������.8���������t�-P���A3,�Lq2�{K��A	f�4���Y��\��=;��@v�u%�q�-�	U�w�c���X�9d��љ���Ơ�}�/��Q�?m5�mF�)+�eZb�{m��zk�zf8��V.���!��i�9[1���3�ƒ�8k����$`�힥|������Q,��3�� Լ��kJw5����?[ ��6*E}���k������1�5;1)9������Ș������H^�V�(i���a� �ű(��k����j�q���rooS��)HA���V"�6�V��j�k���$�P���}���q�*z#� ��1�S&�G�E*�w��fl"�{9?	�p�����<.�����rh{����:Ǳ-��?	.%Y��$���.C\`�uYe��Pr*�\�j�^Bd�f����CU.�Qq�9�o�~&ѵ�:k�	�}ڿ��O��O���Lm�g�ޖ���Z^�r�p�a�c���c� �fN,PRjRy���ѭ�uU,�C�_�ʢ�sdf��Y^aP��nj��k^*@��a���|�?p�/��Yr���կ��q�ޖ[����|�$��,��2�c����IY�|?�B�ʿU۷`hd���訨7_�2PL1��b2���5^\ž~�w�[,%��~r�U��~WEq�?�u� � P�	 �Y��@�� 1�L(�-�S��M�^�|!�����o��ӃY���7Y?.8�_`۸�wc7�%=J�ң�-�|��xz�ڽ{�i�8˨~�sCݾ��GF��M�$0R����3$%A�?�]�dRJ�l����I(�KN�Ϲ�;_�C&s�|h/k��:2�t�н��4��#^�wc�?����� S�69=k�J�����@�գC��(��2���zS��f&�k�/�i[��g�n�ޗ�Χ��;1d���S�b��຀�����K���T����%���2q��_whǞ(�ѓ�N΁-��7\=4�\��!�V>FY�HH�^�;�@��F ����Q�Vf��9��D�Ν!8a/��Z���U�]۵k�V�{E̒��ر�c�)���ܽ}�x���yp8���i�~iA��G��^�F+� 0��е9g*�k���9Aq�q�p�5鋴��^��]o`ppy~��j)��騐`������Wï�����-� S;��ĉ�3�=-�}%z4��� 9�.(���Xsi�~S1����I��B-�v�.p�陀�4)^s����$�+�]��]E"8s�h-m�ۼ����R,�i(�[�HC�h:1,o�y�c#���W��<3=���T\}��,����ʙ����ц+O������Һ�NWAcK ����
��+��3���Rn&��@j
��A���C��T��Yg�������݀
(M��Z��A���f�h� �
3�>=�@��L:ey��e��]{Μ��'�M���; zr=��Y��5�8;2<f�hZ��r�{4KD�f�6:S{k�{3)���!�s5*��Fw��C���7#��5'G,`b�J�3�0j�W��Q��qfg3��s���@�S�@X0IYR	ZN~:f�_0/oN��:+��-n��lz@k�$�K^N�u�9���X$�΂afEE��嚔���1J`�ڟ�L�������	9sC(/j3��������J8#sK&8;+��<F���EdY!��d�$���C����9��\��ϥ�L�[z�𤼵�O���`aw���8:�� �ۧ#��u?Zx�)y��1̚[���<�n���@P@hN8�չlѵ�(fV*Y'v(ip�ߢ�x:�[1wQ��u 27�1�$�)Gm�e�-���L2ag��'��`���eh!�s�{����G��f�J/�\��
:k~^an���._9\�`x���=8�?���3����xh���q6��Mx�;o�<}�����,iy�
��S4F��̿�{����y�8�z+��Ł�`�g��׶�T��!'�
��畃��O����]I�"k2��q��ŀ��<��	w�H!���<��
%�QawZ8�/\<��檶���E6�Z���oK������v'��p#2�7b՚Ӑ��t��ws!�Gw[5�G'}��5�P8&���>.w��uh�[�ֺjd�a����i�8���iF�I=�:��w�l9ٓ�K� /  s.<݃�;��,M�9�b����̝���S�/�b�TY���@O+W�ȧ���;֯�}e�z�o�# ���P�͝/�b�Z,��x����0r�,�_�Et��`LL�:�JR�ɘ��!ˬ��p%�/�F�k��gZ���jdJ�<��/�����s��=�b�_|��L��,}�h�@[ X�щc!�Ğ@�G�|����8���'%c��-�o�`��X�3:/-��2��pķ� 1����Gʙ����ָ	�V���O`�k��1�f���c�&��߳���R�.�����Z[��%���Z�1G}k����ղm��u" }�+Ķ2��w4��}X��,�?r6�Z:�t�OԤ��P��z+���t>�;#�'cz�Y����/-^�%��!#k,w��X����Qd����V%��M���ڈ���Êի�w�j��a"��Ԝ�1>x��Մ���4n
?�vn��G�)��ks%FF�5����#�8.0��0��F)���֜vE��6�?��ũˇ���Ol�&���ĒH'&H�K����?�	OJ}]O#�re��}8��<�l&`��ap��ۖl5!(�[��/�ŌT/�.P�e��|�
�����^x*�9�1���*@0#�I�w���?���-C���=i6�^�"8�f�F�
��$@2S�jnd6eM�r�-�����sFP8g���H��Gl�E��B%���D ���:KA[m���kH
�Sp��T���~"��󹖔?�G��"�c�(Tc����`�fǰU�hmxN���U�!J�#�f~��+X�Ίh&s机;��cc֝@a�qXؖ�����P�ʥQ��6�)KV��W� ��tt���3���� >}yeR(9�'�u��*01֊��\ҡD{[�'R�����AwG���M7�o�2�ư�ur1&&�W����)|���RRI0�
��Ku�75�Zq:[i;���iH_v�NT��wW`�ڳQ��^tv���3��NdJL�5g��庶#>��P�����i�rZ��j�hi��%�	B�@�y��O��h���0�6��Ųn�U�`x86��^cJ%�(й%��c�=��aO����x_�?X,��%�X4	)Zʇ�pE��������JQZ9��@*�'qlo�P)*��9g
5J3SR�
�jyl!aE}�W�)=yt"V�^>Jf��C}y7����t���#��3�߃��Pv��'Q��+ݔM�cQ(�ɽer 	���<8E�ġ�W�� /,:ˁ��KRD�I ��	Jp	���	R��.�o���(���Տtp�m�_�w4���/1T2�<K�pL1Ƕ3�1��wŤ�.�m|�����V�jط����lEc�qPXj|�!y����>%�8����&��M�&�%Q4�HsҬ�ȔRG�EL`��� �O 98�ÒS���A����W�ڄ���u<y�qcg���>�� �#5���AI��?�gq�ՊG�/�`���,�a������{%�c}%t3�Xab���B�Ab��VJ���m�Cr�.PJ����b$���	z&)̰���Β��SG[���p�Fm��]��^NF
�p�~��?S��p���.�1c1ۋmR�K�Z�������a�Zm��g6��Ih�w��u�q���V�#~��x->�5wbs�0�8�Dm)%'�Ā��S
���r<�AJJ�C�<��č5�CB�Z��Ҫc���-,��߸��K ��U�n*��C�d38�(�Bk�&�J��@�S
`��ήb(VD>6ƹ��]�!y��z�����3�d�)�F; ��w�i~L���pv�r�C�I7L���K)o3�#�+��3�4H��Ysߵ�����I�w�����z���U�@E�0E�X�,Gj\M9����Q�vP⑍m~RJN�n�jr�Տ�W� �o��aK� H��=����_���:���4?�Ir %c��M̆@�0�	�c�H�_R�H�2�̺�yMF~�0�������n!��b��BiH\�j���K��aq��Lz�|�;¤-�����3�؅_R��>��{�[���r\�h�v��!ՙ�Dyr6(�fKԥ�C8�c;t�w��RY���桏���<�myo�dG��Rq��ǵ"r�k�*1G�pe�{����:1yT���'�fsm��o�p��_��<7U >:z��9�|�.��ՏO��)�>���2�Po�L/6�6��o�o)���G�HǦy���k�S�i��輗/��!ܑ���3e��,p�4�\$�xh�dfJ*l�(��(҃�AC{'n=P��w<�'��?l2���.ttm�+?�Fv���gIq1��(Q�f��9��p��	!y��;%w�w�ppf�Ǭ1���sOF3A�� %ۦ��Hq/5^�<�%=�|��/.�M�R1KH)���ώ�n���7߽ϗ��?z�K�6@z��c<�{V/�S���y��?�1���R_Spb_I���L���&r�5?P7Ǟv�bϪ��I���/dIie��e+�q��������ي%P��)s�Me=����xt_#z�&şy��N���]���?k;$�K�F���)@w�:&Q=�����Mr%��e�̥��l�)� ��%������[-0�ˢ��x������p���������w�ta>x�w��(H0������8b[
k��7oހ���������x*)���*3�v��T�D�������E;z�ǚ���q'�0�q� ���O��U��B���K�|}���s�K��?��g����D�mK;0����w.&��87;3�۵k
K�Ǹ�l�i������Ӏ���N���a�m�v7������t����p��Ӎ�V��s�Qy��_^�K�oaH��+W5�ݽ�zϳ�\�.y׮=�0��K�H�D:��	N p��@�'8��_��x1 	y�    IEND�B`�
```

### `src/flows/fno/assets/signals/lemon.png`

```tsx
�PNG

   IHDR   �   �   �>a�   IDATx��	|T����$d�!�KI���bY+(�V�@��JUJ[�b[k��oE�u��j�ʟ�wA�n@%�,*"�YK��L�d���3$d�̼yyo23����{�޼s޽�s�aA�8���LD�!($�(�/F��O�OĻ~%����U�
�)���'@{U`���(F�A�=g����h,�L>��pL �I�OY��� '�@��H�9Ƹ���.��킨f��BYR!��hP���P !���I,��|�c��D$��ۛ�B�#f�z"���8�^V0VӴY<~_ͧ�\e;b�B��mTeH���ـ�-�ܥx��LXJ�k`���:J����><��N��Cj��׹Gp  eٗk���IG�@�c��v�M���(�RW��F�h�Y��W|������
����,���,�v�]z !�ⴲ�?�E|a0��mZ������|NB2�^�������1%�� Q;��_@Z�{��{ &:k�U��'������69��~�+S�C��N&�[��ܟ3�)�(���������D�����+-jq��^i�d��&��A�������~��=o��wX!�q+���d�l�>y��|FZi�Q�{!���
�]>9J��ք�1Lv��k�0�G�Sr�c���oA�A�9�����b,S 9����񷑖�
����߰K�۽��/�P{�v��</�%,���`c����&X�=l��;�[W[9<T�� ��I>K�La�+���{�Z˦��<��3S=�*�0�|��
Q�1U�=��f���b",��o�W�W�"ؑ��QZ�^>c��i
 *���wk,���(:�w��W�5A�o����X>k��)
 Jv�j���4����`���J����Yg�gh�q<ց구��a!rο2�K�Z�CHA��@����Fڤ ����]"X�XS�F�P,�E�r8�g�v[���@:y���l�L�X{�%�KB~��4{�KR0�a�Js��;�?!ݺF��Ѕ�u�� �@���s���²�0JiX<=� �� ��	�k�8�`�b��f[)�Q4A�J��G|�3�# �o��ә�r>:=Y6��j�� lp<�/��,�N� �-��Э �<�<�/#������A�����<W���R g*W=ºVr�+�Qu����j�����Ξ�L�uǍ�c���9�,�f=m�*����A�_����Q��הl��c�2e��h.��ہ�������iOV��g����D�{�^)�|�0�mz�$�����9���@Ɵ{(QCգ��z��<]���g��.�G��;s���[Ν��Τu7���D��|s�N�ꄻx��).��V�{�e��{&q͐K|j��w�p��O��W�Æ��1��P]����E��o�C��cZ��k��K�a"ֽ���|#�4l<�����FY�m�l!��PHLl��I�=�C�oa2�.�^:F�ǮP��Y��~�)�V�$K�=�(�9_s�KX�r���b��˱��ڊ4ߜ�K�J�NZE(*������/���$�U�b�<�o�c��M�ف^���ki��sF���#>"
�x�c8j|��[(�(�M�H�c�]o�(�G��8��_��	>���������w�s���w���c�bb�����V�p�R[��?���BXO�H����c#�(�dKi����8J���+�p��_�. �zt�C�b��J�X��̀�z9��b�q�����
P���v�|;��3���5�ϝ=�Ac�jKmR����������=�ޏP�,�ga
1#��r�+̔�@Q�Q;hG�q������V	�۹�	_R����<|O86�˸���a�f�)�S�.=2�	l��U����m�Ct ��0аT�lP����+,�������	t z6N mP M�T/:pP�@G���"�Be˺A�T��x��Ne�T��"Ti,k� ���_�~U�ݣ��9�o/D��<]�5B�*%N$�U�z���1�&|ؿhW�K���.%,߁#ep��
�	\�$��VBe�L�w��mP�P����K��S�HP���m09���(�v��J����СG��@S����YI��L�?�����r���ZG>�({��!#�K}����++�\�O7}�5d!��`��̌4L�|"�^�3���`5J�:��H�jʷ�\`��-�}��6oź��z�zl۱zЯV��"��I��8S��܅<4��n*����#b��������g�]�C���(]�}�{�׷�B 7��/c��Ё�*��y�=Y�l��qW������-��.���+!!�	����mZj�a�oN|���o��&!ކŷ݄KF���G :ʕ�VYY��������>��>�
c.�*ٕ�ä�������k�f����5���oV|آ�<��:�v�O���"p�Txl3}�$��ל��H����T�i<�6�_��*�@�H�ռ��E#Ў��5������l��es�~��^�X�p�������Ń�߅+&���a-Gߢ��<xt�q�>�8���Z
o�Ϲ�H�#t�aK���������F�]|[�-fk�)��~�s<�?�6+ї��\ �7p�P ݇����{�-ǐs�1rĹ���Am�U!�kä	c�q�k(��ĉ��H�n~�#%HO`�	:�6��?`�=,~֘��):L�8v
�%+ ���_u	_�[Ƚ�:W�����U��N�K�����n��/��~�T���&6B��$GI��]��I�ʧ��4^���-]db~�-(-�%�;w�~+z$��|G���y�W�w���qL� U�	T>���}5�}E���ٟTd%��/{陣��q��)��3ODu��z���e�F����Z+��s��o��x���G�_΀)�_�G
vb}VV�mf͘3� Gz,�W�MhP^��ju��0Ɣ��-J�� |�vEL��h��N/y	���s�8g=MMa?��!��b��y!n��%-�'�zNK�K���NoX��7[���R� ���s@��ߴ�rkE5,c��֯�l�&9.v���òW�`��e�/d�
6�a)=-T�0�򮰰h�t������ t�c��z��g8,eH?XF�����칳heE\�%�Y�
�Y� m:���?\�!z'�E^^�{}��E��s���*��Ce']��̳��3��<olk!]�^&�7M?�66��=p�(��b�+�� C_�����;�~8r���þXarZ���`B�}�*�>XI	����r�K��2r���yt��I�M2#��E��
TR�)��Y� ��Q�A��YĞ���dW��-:��I����ݵ�jc�%�����X� �6�fkвՐ��(C�B�,�m����ְ��hL�G�������q��K��Əްf�wqL��i���}����w�=��̃�&oa)�wF=��a��2����@�7j�u{�_�C��
f���w��$��^��0��,�˒���s�����~'�0�`�E��]�?��r����ː��n��:�D�X�S�8�4LQ\�s�Y�??�{$ �M*.��?�1?�5�Х����h���`5�2w�jc���65&@�6��%{ �s�	E�n�!G�n����)�R�.��@��	�0���M��!�x�H�90��7��~S��Ӓ�����U��9yV!e-e.?7�������fK��i��?��
��EN#o�
z�C�f싚0���.9�Q*��<]�ӑ�-e-Z"�X�nE�-��8}��q;n3��z~�������a������RW�ς�$�\r����(����!�&I@ӗ�D��Bč��4�����+�)������P�hV^��{>˩�r	�t�pL-Bgb�6��u�,���Fn���"%.�7�����!@� Z�#"P�����*��3m�\�JaG�s���Л�4�/�N�ly���%)屸�.  IDAT���yy�
�uU6���wa&,�W�7>pn+"D�hy2�@R}�==<����}o �\�6b�N!�"���1�L�h+en���l�o�S�߳1|��F�v`�8����*��gM����h�aDe� ��.m��+/��r��ӹ��!D������ ����)jPA�-z ���o��0��8�_�@'F�0a˴��%ng�J��N�Nz��ԢP�@(a���n�bR��_���Q~��k5���L����w(&��F ���T�u�_�p�F��mO$�B�*�V@N�����j�,������=������y��_W!��NϠ��ԘG�ؔur�A���O�`�:C
�\�s�x��)ḋ=Hv�E��l�=@G�Z������Dz-4�U(:� ���B/a^r���R'��P�%[_�KetE�9|���=m�%�lQ����7`�b������Ç5�B�ꖆ{Y�:{.��BwS��-d��lu��Pl�Z��v"v����G'�Qt�T�l��������_�/=6����A�e�0�;:�y�l�)�)��>)��$Q#�Y^�JtQ=^F1:�Ջ�L�p��8�G>�jR��<�xγ���]uTOz��]�Q=tU����S�����%[�;r�i�A��£2*�ц%
H��
�.a%�q��p���oK1���p�6�5�b?���T$�X���z��q�5��.�c��D�W ))İ�X�P�0ӭQ��#���)@��碇@/"���1�͒2���Aڴ\C./R�E�eM2D����i���T7�.}�����"_<5����%^Fi�z��wJQ�&7�&N!�x�e?��	"Z��)<�h&|���G��f��)�(f�%"�2���ݓ���\=��CQݟW��~M��B���0mŞL&U#������5m'�D�b��4�]�w�[Čp&�K6�Y��b&�q����K��Q�w�8�x(�Bދ&��,�5���8��6��1�hQ�
����SuN�"͑	D2���=K�CT���R��t鰮Qi+ո�9z<�`ɢmg�Ж2�筂�xO/�^�[- �!���%]����+�/�l�>߰�q+f"�����s7 �D�l{]D�n�V\�a��z\s�:��䳄EX^����x
i3G!1�s ��������p.bF!q�(�\�+��-��nM~��?�'N��~k��,�P��nߘa��4W ���uڇt�d��g��V�������?���.�X�{QB�`��{��ݞ��g�8o!�\=��ޑv�4X�����Wp`�ը-oz�§�{
X�܅�ߝ޳x��ԝ�vٿiD�l�,�b�fЮ�F�u?��]�p����rG�7�1��R�STQ�I.�d\M�/�D;;�C|0�8���T�õ�T�n��|a�EU�Q����e�B�k���8�s)�bE�����#z(��g��&�t������R�zĚ�DͶ��mW�mlm��x��43Z��NSD�Ŕ<w��T�z���n5_-�� Q��@��5������XW�����#�/�űS����k���dh��y�ݧt�v��_볔�&�2��P�ƈ�E�(/�5����������� �g���M]z���OP�l�l�gA� �{~:M�݄���Q����j��NJ�Q'1�3R��ѹ�������4G���yZm�0ET��Q�O8Jᨌ��[�QI�Vx��5��Wc;o4�t�@�S5�����=�Qt��F���/ۈ�   ��2���   IDAT ���Ds��V    IEND�B`�
```

### `src/flows/fno/assets/signals/neeraj.png`

```tsx
�PNG

   IHDR   @   @   �iq�   	pHYs  %  %IR$�  iiCCPDisplay P3  x�u��K�P�O�R�:�2�C��
vqh+E0T�S�~	m|$)RqW)�X�Yp��TpqpDݜ:)�hxޗT�"����8�s�\�P+�(閑LĤ�Ժ�{���S�f���,
��������O�YM�v�O\��.�v�S�]՟ɚ���A�����m�	�%1h)���ǂ�.�;��d���X�
j��I,�;�|��e����ޟ�W���Q�a&�PQ���ӎ?�-rW`P.�,�DI���Сa2qAꐸs�~���mm��mp�/��B8������x n�L5TG���r��	0���(�a��!w{�{��c�v��#�����+�)j�1)O>   tEXtSoftware Figma���c  %vIDATx�{	��gu����/�����g�4�Eh`XZ$��4�0��H±�����$%W���qRTLr��q�")��T%f120b$�4=�4��{zz�޾����^#���M�t�~��������s����7�1q� =����#j��oЪ䴠X�bK��]@X������bda*����s'�p��/L�|hx#�::���H�n�����5�����7ց���o�|o��C�ա[�{�@�JN/�tߤ�����x����:?^?L���Ѵ��(�
Z�mu+4vZuZeQ�ï��x�L݄AcuM�fh�����ijy�� �3J�[�M��i�������D�kv���\�m���#q8��3�*º��Q�^��/�h�@g����X�¶��a���B�<C�]�u�&�"
a�B�g��@zQ�^��д�o��Za�5<ުnhɯ����f_7b�aĲ��]殯��^� �2Kv�sb��@�H$Ԏ'SIX��=;�.ėu:�+V/BOu�"3=�:�ᷖp��I��ǫ���'r��W�_���U+��O�f�4.�Z�!8SB�z���i��������6��|�]]���ܕ+���m�u]�q�D�DI��2M�>	�:����3r�`*�̉W�8�[?s���������7�����dh���"����H&��o�p�J�Rj糙�����et<GwW�2:���}�dR/NK�3*blہI���W�>b�-�йCoka��{�W��Կz����î�ŷ~����s�$��Ҍ���a�[�r�l����&TJU�
���t�/��	�������8L0A7,����[-��`B�*+�̓�4��vxs\���{sx�3G_�M��}c�}�f�v�+��?���E�VAs�0kut�s�V+*�eg��r��Z-����u�=�\;����kp���s�����z����E��PC�V�<_�m&�ka��	��e4m,G��������" �O�ϸc^y��J�R~��=#���ym���zƒ���Frq�������,�J��!IT*E4�5�j5�	�bI]1�p7h���*zz�QZ_C�\�#�th+++*B4^3lp[5h���ju���p�S�x��{~�m���m��_���_���:B]S��W��;�Y>#c~#@�����qM�ӽ���s�}�p�YG�h�<��$Iq/��A�����a��Lu��l��:;;Mu��Z��m�z7�ǂ�E���ޟ������ݯ��������is��M�Ze�����c�}bB��[�ُ��4��psss\p��~���MҾ�c�g�������$	�餃T����ّ��J	��<�r�3-�@�I��ZCpw.����\g(+����'>S�t�~�8�����PPe̒*���ݍ'�2�ٴم��c�q=$�U��ζhxI1<�NZ\�g�a
�}w<�N��I�љMb��&��w��#�����D��P9]c�]]����z��yLͮ0�X���>��.x�qn� biԸ�����G��L�����"318��S�_��z0���df���3�QA��%��q-fj	����{�m�5��L8:w2��"��%ll۔�؎a��v#fǘN:��8z�rt��|:�cjH�Gp=_Q�j_>����y�.���n�hj��N�; ���+|�t����EX�8������c�˅�V�ER��˝M�s��i��7d�������1�������և��l���M�����KTO�9�^�`�0�Ꮁ�iB���o�w�/h�&��x���awSWJ�4|T�5�8�tP�������.F	R�ꠅ�N:���~���|�.n�H�l�3�UN�A���<�K�V/���1��h�U�-.#,�s�"l-�q��U������;ۅ8�Վgx�8�S�ͫXC�v�k�0��_��\;F�lTU�ToP�ԍ��G0ye5�WؤA��>��i������Tꅬ&�'X��=�7}��R��y�G�/DAt4"P����.�U�w�U�D�U��	(�úFOWaWg�����]���G.f�'�CLr�a����Y@`��Y�qV�X�x��5�8)�N�>X�^:�Qg%�z�G�M���=�>��'����	�;����d�+�b*4B(m��Ȗ�EGq�s�_�^�3
�M�F�������ڿ�s�͋~��;�ȸ
�tƺ�\�����Ȅ#�L&��|E��D7�d��oM���ɾ!��JM'�N'b��������z�&b,��LR��C4�,��klT&��艘Sz m6��J(sP��p�G_��|���ݲ ݦU2�"���0��/�b�� ��#��)���t�;�"��ɥ�c�#T,Mc���491�r����в���E��]f_!Q��sj���ӄ�G��1FP��I���:����*�'R�v�	�Rm"i�v�8��e�_#F�D���0�4�xAsB����BNdQ��L��Ij4C�q�X���{�D��y�����Y���F�"K�D@|�W_���*�%P��"�ڽ��@~L�wUD�z)��CA	:)l&�J�cH�I*2�5f�{: �f/����G\�#��O����K�G^�ȯՂHu\��N��~YJ�A�!7��5�HT�m��ަ�	�8}�r��q[���<1h���I��R�� ��)%�Jd�Q���yM��������&��9#,�����ٹ�Û�,��('�D�-�׳��.]B��(%0���o����ڝ?���['����@���!Ԧl�Ϗ�����MA��6!���v.�㊡ -���DĀ���Ij�!�ӌ���iH�8��w:��p�tV�yC;�U491�X_?vF�$����T�0FX��������\�B	��Yr�&�0g��މ�/�%�ӭ�Q�!%�]v�`���u%".\1?1�ƚ�lVz7,?�W�7ቢ�P���i=��ֵv���O���4F�AN#Z,i��(�(�ˈ��dQ�3��;\I%F�N�@��0����pw��5k�
���F�k7ۛ'[F��3D{dLq��C/VKo�G#)3�<���\����"�m���T�`���m���8y���D��W�/A�Da	Yj��.xv/��B�����L#3U�Viq��)�Q �Z\�r��A��g_�5�vm���~�7T��#Os��>g�D��$L�	�4K�6��E�-�o�*t�aĚ��|��҉����-K�\Fb<wO���\P���2�\�J!<^5��i�� ���lb"+��Տ������Ο���o�F�`��Y[��@��M��.N�Ĩ�<����Ev���"
�C����R���,c;aiM̯S`�����S����ˎL�R�'��)�p�L�4þ��0��{I��L#-Y��`�Y��h����́���<!D�� ]S��Bc�#S���VqE��y��ϐ�䡙A������3.c��������q�MO�%r��a������H�82(b�QP�F�'{ܳ�*u��Y)��ܺ���Q�ؕ��v��3Sx�};Q�%q�R>�0�ًx�@j� "��s	�3�	�I4�#��a��U�@�}��!��P�2$��EL�H~f>i)"8�E5�i�'�M��p��e$��{�<F��3g�L֬V��p.��k�E�Cb����Jd%2x��p���%��~��!���<�`�w͵�ss򛇱{�R�6ևd�bjsB1m�B1^h	o,2�����>��~�5�GNS%-`��4H�	����*-T�"��qr|N`�����a�����Q�v;C�<�����A����>��<��D�=�@�����'��Mh�Q�_R]����R,�{w�`��!�8A/��ڂn�D�WW���N�<����ط�p����f�R��J5��q��R�F�}��
��>�,���a�����HG0&D��FTt���u�#�?��9;�v����{����μ�F����v;�����tѩ}�C�p�u�U�1��o�u5���-�$n��s#�-ږ05�$s9��ut(���$��7 ng�ng9���[�:R�$<y.�5[�T/����9���Q�t�D���6.@'^fn�����~�S}OA���|[\õL�C5Gz[��y���gxo��屌�Y�A^Gc��E�$���>��N9��Ƙ
u��"y_��Ne�x`�l	5�N� eftF�:�~����=��)�#\�M��F��A��o�%ڒx$ʙ4vĲ��U��A�� �R1�5iI<�*��x������Y�v�)�����x�T�9���4��Q:˺ώ/G�Z_=�T}�=�W.��;��d���\���;�2�SJMr��ÈԹI�'�F�و��Hھ�Ǐa�u>q}�}I46YA[3�~�I('��"�j��u���o�U˅�S6*��	����+%��*�PJua�B��n�Z���N'v����~�~����m�R�
o�f����XC)C��e+lR3��d�+H�o��S��e���K�(�)�oV��C��� �>���z�FH �a$ '�E�h����вjj��=������Z/���7�J9�K������B�T��ڑ�<Cp���n��,��E�f���T�1��!^T�@A"r��
���������u����Yi��ڂHy�L��;/ev��Et�l#�����2�ܞ ����	��,]���PV#U	�8Zmص�-�7�U�@5K�BؒYU��F�q��8���bX��Z�{dM�b��b沫�� ����f�(�X��2�LU5i���d>9s�'9�g�ps8�ɢJ�6�Wב�ꧪ�E$/.�p�el���{�iҨ@��߷awo�U�aL�{řY��򅭈Ey���6�Q]_�.������|�Z-=�_ �ZOz�~���d�ř�yY�r��ʲk��&:M�F6z¶J����YJ��	�5���&w��G\HeE0�|x'(��ۇh�¡H�~m�󌌾<��V*�T�Cm}���X���O�B��<�︚v��{�\��qt��`� �W����h���0TK���*W3`���Ȱ}/1����<ْXc�f�P5�T��&�xmc���S���� Ŕ(q�3̷8�8���+N'�s4�k|�)�F�L�T�F�q��6"�Q���"\��O�h�l?��J[�͆��;�HX��zۯم+4�oxHr�Q�H����*�o7��\X^���H%�i6T!1"`��i"���٤�Xc�u� �j�%�U�<~�Պ������H���*�2���I�"�IR̗��h��$����cE��j�_F:)��nP'(Z�-K]�<�N�����'gΞgO0�2��ӧq��ݙ,���ǥ�J�y��� k*у�4v��pס��I޳���E�3N,x�c��_boP��l㍦z۶�!\BR��"��H[����#�/j2��ҷG*�b��3t��1��8�6,ޖ��79+Е�!T8t�]TW[jڤJ��gqqn
?;�'N=OgR��@cu�ׁ̒��GW:�$w�ڑ��D[�b��2�b�N�ZD~�W��[��)�e�<��
����)�A����60��q�&}�P�eO��3��F�]��DFu��]���)2QY	x&���S�]��P�)�LI�����O^��6'���}��x�y�i|�ѓ������	P'������s<�I���Du2(��ċ2�q��p
����c��XP]D.O�Ɂ���S�"�s�Em��ds)�F��2���Wf��st˙8��yhJ3T��v��O��N�U���%����̳F��䉃���I]f	��K��JQ��M�%U�\M�͛:Ұ�.�v昽��u�'&b�±9�SL ��|w}����8��لFXg���}l��R*/,��� iq �k���odz��I�&H줋�T_c4XIF�`��Q	6��͜�s�uv�s���0��3x�%�0�`���=|}��q���ή��qj��y^��V�P 11�ۉ���-�#�=��i��(�؆Α��F��@�&VT�M��
+��(�6+����������O<���nk��Y"�M��ٶ�\�(��p������ͯ�޴��諌���!�`�u�m�lC��9 a"u�D�8'B���, ��L��Ë��"���G��3�����H���r�;�E׍�P]�r�?��R?+G	u��UR⎾[�$#!���<��IN����I�"��/|l�ԉ3E���8JQn)��$��%�Gq>נ]�:Ø�~"�q�_���$�������`A��H����/1�8��$��.�q�yE�/ˬ0â��t��s��+���U��8��ݻ(v�f�%|s��V����hqe	j�9)��o�:4��*���e̮���Z2�Z�0���\��m��%|; 8�h	E2H�c�Q�\{�RR�@�<*��h<��(J<<F�3-C3%��V[�&�����+5x�a�$xdw	��L?�M�N܉��P�ydp'|L�رΖ��g�♙�X����7���6u8�ܨ�Y�u�v��w����^�!/X��(�WV�8?����%�s��m�4b��O���?����䜦�#%cC��$���ԟ*�{���F�f[�I��z���ʯC�N��cX����<�Z)EQ[f����S�a��huNk]F/��ݝX|j]l�V֫X)UH������9I����=x��kq�ګ�y�_����0�{n�e�Yel��t�`߳wac%*HҖYf߼��ݏ~���Ȧ9�L���m3����pg�t$�?~���'Qx�b��[�X��R�ġ�.�ʛ�M��騗m���HNjz$�C���"��g�aטB�)F��n"zUG����~H!�`Mg��ƞ�VS�v�߫�(rpB�9�0���?�sFO��/��Z�Ej�"G�د�!��PkԱX)�sk�n�G���-�8#0�2���'/,�O�@��������ҋ�x9�7���v4��F~E� �X��P����)��ퟝa�4B^���ϖ� j���	��`��e��k�㨓KL��7����k|^w��`��L�<u~P�ͳ�k�VJL���:C9���ַ�#K$�d
�D��{�|���A�z3J�ue�d�񼃏��6�:;�g�H�E׌�'~z���J��'Z잚��*��J+�j��N<�'�(��d,Fu6d?���#���!S.�;������a�JQ�tX�J_�a�TQ�T��d��m���Vg���%�x��.����2�"�����:qp�&\�}����
�Ub?��4>��V]�r\GZ��C�����ǎ���SQ�:������5���ȳsvn���U�@Y"C���ӡʟE@��(X��j�9D�%�;T���t�	����
�7قf�:]\#�$K���
���A�W֨V�V,cm�s=���<w�{G{q�e1
$n��Ǔ�������LR9Z$2KN��G�k�*�]�g�3c;p��#GV��ׇ������~=�7A�U2�2��*�RUM ���Hq��20���)�'�}�h%:&���[p
�T�0��v�����t^���K����c,_r R*�`g�z+tas���Nq� �Mg��h�n��u7s��9P�W6���r�1.�ZF�c��HuN���t��l�/<#Ď�n����!�Z$��!җzH2�	>&K���;2H� �|�H-�36��.�����DQ�;�M�X����|#�����ȥ��ZRynқ&{��!BE��%�][VFqĤ�Q��Ǜ��ĶkơˈKFk��v��q"433Ϯ��b��$�,&���/�����ԮCG�K�|��������$;=ٞ�SW�= �!%0�8ٔ�f��h�Z�N�ܵ��l7X�!^=�?�`Jkkj4&C�z�J���B���&i�H�qv��L�m範���c�u7!?�W2�a�WL9b�8%��/\b��P_���'��nXGn��WpL�'�q�}�gpV]�J2s#B��]r��Z�T�(��;�-��ϊ i�CMJ��ԤR�&�2Zj�r���[b��S� ��sA���&�AM��jD��y��wr6�ݜ���g�v��C:��0eR}���i�R�[���[>�y����O�/|����tӸ���h�S��C����A�A���l���)c��:M�Nm�7j7S�I�V�N�o�S��3�l��-���@D�6T.�n�Gg��_C�Z�L��d�jT/�Y�K�-�W�y�@Pm)��6�o�dב�Ɨ��	���v���x�\��|�m�/�j	Ո{r��l�I�"�T�t�@u���e�'��߇�4��#5)�r��u�w��[ו����>H5�X�P͌�K��>j�&��e\���mۮ�'���N����w��ʶ�����·�����z{\����d�b��|T��!*9P!�� �����]B?�S��Y��qz���+Gj�괗 �!�̽&��g�~#�{+���>i�=mГ���ߛd���C�Q+�(L�5]�P<��O�n~9���O��	_��[$�&�R��zm���=sې���s����C�cN�E���S-��G�,]���搆���j$E�rQ��l������Q�#I��S��Ph�݋(�ŨB�H���m+2p�-�������>2s�[c���=�4�ia{�dX���ir������>$k�[+��Oc����7݃A#�έ���U��Bk9i��
�o}?<�:N�:�T&"m�Ғ�`�,,,�G�b�QF�t*JlŴ�s��{>�JLzu���\��zL��a�2��,��՞ʠz"T:����v�9�dR��oދ�x��i�ꇐa����-:c�('�.<O�k)�Vy-��3�^>�����ɋ��C����ر���$��1�1�:��W�������w��]�Gu��O��9��Ht�Y	<��ϡ3��7o?u?\r���|�l��FřrR\ԧ�K�(_I F��E��q���8������I�񡏳tvsAѱ��7�N��Wk�k��d����u�d
ܭk�H(	�>5Z��W��g�g�*���Ǳ��;'�{|o	�!y+���8g�]z6B��C���㼯I:l5���+�����;��riLZ����n�[+�5<^��Ί#X
'����HT<ME�A2q3�r��V��.�b�e��Z��8@@��L��u8Z\ERS>zS�bL5����o�70��}�N9I����r�����������9�{y��<t�=�c;��1��8�V
��ޏ��kO|� s@�s�� ~�$�l�s�U��t������O��}u�ջ��������xc>=�3����(~y��#5�4�0��F�0X���u0�U��E��ec�e���yJkb�Yj�\�\9��?�<�7��Q�
� �    IEND�B`�
```

### `src/flows/fno/assets/signals/zing-mark.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="D2 &#226;&#134;&#146; Zing logo">
<g id="Vector">
<path d="M9.9697 13.4419L8.4863 14.9253H16.0732V17.9663H3.77341V15.3393L7.82028 11.2925L9.9697 13.4419Z" fill="#393939" style="fill:#393939;fill:color(display-p3 0.2235 0.2235 0.2235);fill-opacity:1;"/>
<path d="M16.2265 7.18699L11.0732 12.3384L8.9238 10.1889L10.4082 8.70555H3.77341V5.66648H10.4082L8.9238 4.18308L11.0732 2.03367L16.2265 7.18699Z" fill="#393939" style="fill:#393939;fill:color(display-p3 0.2235 0.2235 0.2235);fill-opacity:1;"/>
</g>
</g>
</svg>
```

### `src/flows/fno/assets/smart-invest.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="mountain_flag_24dp_E3E3E3_FILL0_wght300_GRAD0_opsz24 1">
<path id="Vector 6276" d="M7.71493 13.2857L9.42921 10.2857H14.5721L16.2864 13.7143L14.1435 15L12.0006 14.1428L9.85779 15L7.71493 13.2857Z" fill="#E8E8E8" style="fill:#E8E8E8;fill:color(display-p3 0.9098 0.9098 0.9098);fill-opacity:1;stroke:black;stroke-opacity:1;" stroke-width="0.857143" stroke="black"/>
<path id="Vector 6275" d="M3.85547 20.5714L7.71261 13.7143L9.85547 15L11.9983 14.1428L13.7126 15L16.284 13.2857L19.7126 20.5714H3.85547Z" fill="#E8E8E8" style="fill:#E8E8E8;fill:color(display-p3 0.9098 0.9098 0.9098);fill-opacity:1;stroke:black;stroke-opacity:1;" stroke-width="0.857143" stroke="black"/>
<path id="Vector" d="M8.5936 13.1557L10.0551 14.1384L11.5878 13.3597C11.7083 13.289 11.8439 13.2537 11.9946 13.2537C12.1453 13.2537 12.2808 13.289 12.4013 13.3597L13.9436 14.1384L15.3743 13.1864L14.3648 11.1729C14.3392 11.1217 14.3007 11.0801 14.2493 11.0479C14.198 11.0159 14.1435 10.9999 14.0858 10.9999H9.8416C9.78393 10.9999 9.7311 11.0159 9.6831 11.0479C9.63493 11.0801 9.59801 11.1217 9.57235 11.1729L8.5936 13.1557ZM5.22435 19.9999H18.7493L16.0436 14.5442L14.4821 15.5902C14.3449 15.6838 14.1984 15.7348 14.0426 15.7432C13.8868 15.7515 13.7319 15.7172 13.5781 15.6402L11.9993 14.8462L10.4206 15.6307C10.2668 15.7077 10.1119 15.7394 9.9561 15.7259C9.80026 15.7124 9.65376 15.6588 9.5166 15.5652L7.91485 14.5192L5.22435 19.9999ZM4.25335 21.4999C3.90835 21.4999 3.6481 21.3576 3.4726 21.0729C3.29693 20.7882 3.28601 20.4953 3.43985 20.1942L8.21485 10.5097C8.36868 10.2083 8.59201 9.96474 8.88485 9.7789C9.17785 9.5929 9.49676 9.4999 9.8416 9.4999H11.2493V3.4039C11.2493 3.14607 11.3356 2.93098 11.5081 2.75865C11.6804 2.58615 11.8954 2.4999 12.1531 2.4999H16.8723C17.0365 2.4999 17.1638 2.57107 17.2541 2.7134C17.3444 2.85574 17.3512 3.00382 17.2743 3.15765L16.8108 4.04415C16.7775 4.11465 16.7608 4.18324 16.7608 4.2499C16.7608 4.31657 16.7775 4.38515 16.8108 4.45565L17.2743 5.34215C17.3512 5.49599 17.3444 5.64407 17.2541 5.7864C17.1638 5.92874 17.0365 5.9999 16.8723 5.9999H12.7493V9.4999H14.0666C14.4114 9.4999 14.7262 9.59032 15.0108 9.77115C15.2955 9.95182 15.5198 10.1928 15.6838 10.4942L20.5338 20.1942C20.6877 20.4953 20.6768 20.7882 20.5011 21.0729C20.3256 21.3576 20.0653 21.4999 19.7203 21.4999H4.25335Z" fill="#161616" style="fill:#161616;fill:color(display-p3 0.0863 0.0863 0.0863);fill-opacity:1;"/>
</g>
</svg>
```

### `src/flows/fno/assets/strategies.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="icon">
<path id="vectro" d="M13.3938 2.72266C13.692 2.72267 13.9336 2.9643 13.9336 3.2625C13.9335 3.56068 13.6919 3.80233 13.3938 3.80234H10.2812C10.0788 3.80243 9.90025 3.93516 9.84141 4.12891L8.90234 7.22422L12.1945 7.225C12.4926 7.22512 12.7342 7.46681 12.7344 7.76484C12.7343 8.06294 12.4926 8.30535 12.1945 8.30547L8.59453 8.30469L7.42031 12.1844C7.22345 12.8335 6.62447 13.2773 5.94609 13.2773H2.60625C2.30806 13.2773 2.06648 13.0357 2.06641 12.7375C2.06641 12.4393 2.30802 12.1977 2.60625 12.1977H5.94609C6.14866 12.1976 6.32787 12.0649 6.38672 11.8711L7.46641 8.30391H3.80625C3.50814 8.30379 3.26646 8.06217 3.26641 7.76406C3.26644 7.4659 3.50811 7.2243 3.80625 7.22422H7.77422L8.80781 3.81563C9.00467 3.16653 9.60295 2.72274 10.2812 2.72266H13.3938Z" fill="#161616" fill-opacity="0.6" style="fill:#161616;fill:color(display-p3 0.0863 0.0863 0.0863);fill-opacity:0.6;"/>
</g>
</svg>
```

### `src/flows/fno/assets/trade-calls.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="19.8232" height="19.8213" viewBox="0 0 19.8232 19.8213" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="ai-smart-assistant-square--ai-smart-assistant-square-intelligence-helper">
<path id="Subtract" d="M9.11455 3.48215C8.78711 3.94149 8.60115 4.50039 8.60115 5.08929C8.60115 6.14051 9.19581 7.09465 10.1246 7.56139L10.3143 7.64789L12.0847 8.37612C12.1507 8.40339 12.2061 8.45009 12.2451 8.50865L12.2786 8.57004L13.0068 10.3404C13.4337 11.3771 14.3789 11.5773 15.5001 11.5773C16.0892 11.5773 16.1249 11.5773 16.3392 11.5773V17.7679C16.3392 18.5569 15.6997 19.1964 14.9107 19.1964H2.05353C1.26455 19.1964 0.624959 18.5569 0.624959 17.7679V4.91072C0.624959 4.12175 1.26455 3.48215 2.05353 3.48215H9.11455Z" fill="#E8E8E8" style="fill:#E8E8E8;fill:color(display-p3 0.9098 0.9098 0.9098);fill-opacity:1;"/>
<g id="Vector 6273">
<path id="Vector 6269_3" d="M13.7585 2.55993L14.4872 0.790156C14.5284 0.690243 14.6258 0.625035 14.7338 0.625035C14.8418 0.625035 14.9392 0.690243 14.9804 0.790156L15.7091 2.55993C15.9992 3.26446 16.5587 3.82392 17.2632 4.11402L19.033 4.84276C19.133 4.88389 19.1981 4.98126 19.1981 5.08932C19.1981 5.19738 19.133 5.29475 19.033 5.33588L17.2632 6.06462C16.5587 6.35472 15.9992 6.91418 15.7091 7.61871L14.9804 9.38849C14.9392 9.48839 14.8418 9.55361 14.7338 9.55361C14.6258 9.55361 14.5284 9.48839 14.4872 9.38849L13.7585 7.61871C13.4684 6.91418 12.909 6.35472 12.2044 6.06462L10.4346 5.33588C10.3347 5.29475 10.2695 5.19738 10.2695 5.08932C10.2695 4.98126 10.3347 4.88389 10.4346 4.84276L12.2044 4.11402C12.909 3.82392 13.4684 3.26446 13.7585 2.55993Z" fill="#161616" style="fill:#161616;fill:color(display-p3 0.0863 0.0863 0.0863);fill-opacity:1;"/>
</g>
<g id="Vector 6270">
<path id="Union" d="M8.66113 2.85742C9.0061 2.85767 9.28613 3.1374 9.28613 3.48242C9.28597 3.82731 9.006 4.10718 8.66113 4.10742H2.05371C1.60991 4.10742 1.25 4.46733 1.25 4.91113V13.8389L3.38965 11.6699L3.39062 11.6689C3.63629 11.4233 3.94319 11.3009 4.2998 11.3008C4.65658 11.3008 4.9642 11.4232 5.20996 11.6689L6.52344 12.9951L9.00684 10.5361H8.52246C8.32324 10.5361 8.14801 10.4672 8.00879 10.3281C7.86965 10.189 7.79994 10.0136 7.7998 9.81445C7.7998 9.61521 7.8697 9.44002 8.00879 9.30078C8.14806 9.16151 8.32309 9.0918 8.52246 9.0918H10.7451C10.9443 9.09191 11.1196 9.16162 11.2588 9.30078C11.3977 9.43997 11.4668 9.61533 11.4668 9.81445V12.0361C11.4667 12.2351 11.3976 12.4107 11.2588 12.5498C11.1197 12.6888 10.9442 12.7587 10.7451 12.7588C10.5459 12.7588 10.3697 12.6889 10.2305 12.5498C10.0916 12.4107 10.0226 12.2351 10.0225 12.0361V11.5498L7.43164 14.1406C7.18597 14.3861 6.87901 14.5088 6.52246 14.5088C6.16592 14.5088 5.85896 14.3861 5.61328 14.1406L4.2998 12.8271L1.47363 15.6543C1.4076 15.7203 1.33204 15.7683 1.25 15.8018V17.7686C1.25039 18.212 1.61015 18.5713 2.05371 18.5713H14.9111C15.3545 18.571 15.7135 18.2119 15.7139 17.7686V11.9941C15.7139 11.6492 15.9939 11.3694 16.3389 11.3691C16.684 11.3692 16.9638 11.649 16.9639 11.9941V17.7686C16.9635 18.9022 16.0449 19.821 14.9111 19.8213H2.05371C0.919802 19.8213 0.000391633 18.9024 0 17.7686V4.91113C0 3.77697 0.919556 2.85742 2.05371 2.85742H8.66113ZM5.80176 14.0889C5.80384 14.0906 5.80653 14.092 5.80859 14.0938C5.78203 14.0716 5.75561 14.0476 5.73047 14.0225L5.80176 14.0889ZM14.7334 0C15.0494 0 15.3386 0.167004 15.498 0.432617L15.5586 0.551758L16.2871 2.32227C16.5138 2.8725 16.9507 3.30952 17.501 3.53613L19.2705 4.26465C19.605 4.4022 19.8231 4.72791 19.8232 5.08887C19.8232 5.44999 19.6051 5.77645 19.2705 5.91406L17.501 6.64258C16.9507 6.86921 16.5138 7.30617 16.2871 7.85645L15.5586 9.62598C15.421 9.9601 15.0946 10.1787 14.7334 10.1787C14.3724 10.1785 14.0467 9.95997 13.9092 9.62598L13.1807 7.85645C12.954 7.3062 12.517 6.86924 11.9668 6.64258L10.1963 5.91406C9.86231 5.77644 9.64453 5.45008 9.64453 5.08887C9.6447 4.72784 9.86246 4.40223 10.1963 4.26465L11.9668 3.53613C12.517 3.3095 12.954 2.87247 13.1807 2.32227L13.9092 0.551758L13.9697 0.432617C14.1291 0.167157 14.4175 0.000147311 14.7334 0ZM7.99707 10.0068C7.99903 10.0123 8.0018 10.018 8.00391 10.0234C7.99219 9.99298 7.98269 9.96086 7.97656 9.92773L7.99707 10.0068ZM11.2998 9.81445L11.2939 9.72852C11.2933 9.72404 11.2918 9.71926 11.291 9.71484C11.2961 9.74672 11.2998 9.78016 11.2998 9.81445ZM8.01758 9.57227C8.01514 9.57757 8.01302 9.58349 8.01074 9.58887C8.02339 9.5591 8.03849 9.53006 8.05664 9.50293L8.01758 9.57227ZM11.1406 9.41895L11.0781 9.36426C11.0733 9.36063 11.0675 9.35791 11.0625 9.35449C11.0895 9.37328 11.1163 9.39457 11.1406 9.41895ZM10.9521 9.2959C10.9221 9.28435 10.891 9.27459 10.8584 9.26855C10.8571 9.26832 10.8558 9.26781 10.8545 9.26758C10.8885 9.27382 10.921 9.28401 10.9521 9.2959ZM14.3369 2.79785C13.9834 3.65649 13.301 4.33882 12.4424 4.69238L11.4775 5.08887L12.4424 5.48633C13.301 5.83989 13.9834 6.52222 14.3369 7.38086L14.7334 8.34473L15.1309 7.38086C15.4845 6.52225 16.1667 5.83989 17.0254 5.48633L17.9893 5.08887L17.0254 4.69238C16.1667 4.33882 15.4845 3.65646 15.1309 2.79785L14.7334 1.83301L14.3369 2.79785Z" fill="#161616" style="fill:#161616;fill:color(display-p3 0.0863 0.0863 0.0863);fill-opacity:1;"/>
</g>
</g>
</svg>
```

### `src/flows/fno/assets/us-flag.png`

```tsx
�PNG

   IHDR     �   ����   sRGB ���   DeXIfMM *    �i            �       �      �       �    ��36  @ IDATx�}�����{������{��DQ�Q��ݨ?������b��X�1��`Q(����{��?�;�.{j�&�C���ۙ�y睙w�}�ۿ@�B#���F 4��@hB#���F 4��@hB#���F 4��@hB#���F 4?��~�3�O���*_dd,|�d�DyQ^Ykzw� 6
ش������C�*4�b������|_mX4j*�
O@TL:���,���8��
��$�����lߴ�Σ�^ͅ�>B#p��Q7�Z���W�BCUj���(4QIp�#`��76��4Ԗ��*j|�-ۃ��!�	Nh%4��������v�P����Pp�WTs�@���RB\���el��/��E����P���ը�,B�G�:�=xw���4�8*&0��H��d��:\�޺E�����ܫ���@Y#.�'�!��tOd"=�C]1|u�p�#o�_C�c,������`��xD9	�vA���|}��Jppɩ����%Ȫ�5@��i*.i�8�ښ2�<��w2B�������7���*��Vo}
6�Z�B#��1G�Ի"y{�Zڰ=�O?�=2	��@�Vif�O��ź-_�\�A�L�e�R� 776P�੪y�j_b:_�CC%|���P�wAp�^�{h���Q7IR{_ꫬ��hTI��' �&��p2ȼ���U����M�X�t^���"Q��o��8K��2#r��o�$��	0#��!��� �V6���a}�F��u��	#���s)��_�\����łe���+9�t8������������!�x�'��`����}r���?�����8� F܋�ց[�ػ;.�y�	k�mǤ㇢g�T�8g�_Vh�m+�^�����T�8��aƙ�����$��wQ%�w'\�+,2:�5h��?�8� &"<U��,�Hĉ+���Ǳ���X�^��/?8���!�l6�\Ө�G�x$E����X��֯Ev^>�?}"��x2^}�m��E�&}5�*@��9���h�
k1: :����G�{��uN��i:���G�U m��|'��nW5�<HHnk6e���7�������.jWP����֘��� ۥ!91#w��E�znAbQ�9��%x=����+���7c���pr:a���@
퐹<x�B�G�Uo͌!����K��q�_.��N�@l3�(đ�d�>s/گ����Uӿf����c?�[R��]�6����銭�	ֿ��<�����07���A��ñܘ�")��&�C�yT��?)+oe�'�q��Q��'adl2"�$G��<s�����H2ќ��Ok������g�Xڼ=��I�E**2u%X�)�9��b�ki���m���?�x����&�@I`㿆�:۸��4�]�e�����H�w���B��Q���BV_
������`��f��z�F�4XS�V)�7>M�u���O2ۤ���D7^�Gw�3��7ߛ~n��|#�95zvJA��p\y�'7���q�܋�R��&5!	yŅ+߅��/�g_�Ŷ��������8��PG���d8s�;΁��Kx�2�#jED�#.�� ��ih�3G�T����!Ql�"RJ̺�|Kue��=<��iS�k/�`ڭ]��Kf�3�3b�!����g�ϖ~���0�wl��n-��S�Q�Y�>�M�R"N0�������t|��Rt��ݺd`������s�x	J1�r1�#`�Kr�3��s(2������{��qD.�\-��� ��3�s��P*3衏d�*���Օ��F�E���4����R<1�����Vפ���j�����<Ɉ<f?dږ��¥;�}W�	~��<f�!�˱�S��ڿ^��s���O⬬NE����Ģ{�Yކ
Ժ��~3�����?f��,�]5�,��M-��1Kq20���C�`���ܐ�L#~DPylI@#
�����5a������*ɔ�o���VY�(�b�d�|a�HK��!���;Ϝ�v�)Cz��jx\4��>�֩Q�߱6�a���Lsv�T/r*�s/u+$�
0� ��S�Q)�E^�~lٶ�@�w����j__k��$2��F�z�F�����uCu�i)1�Aq��_���_��$�_��X��u����ؙ��D>~�P�ꪳ�����X��gv���f�{�<ln�cZO�Llbf�.�e����F����=������]�|U�P�!K��D�Hw5��/('�B9����1~�p,�d���xT�Hx=�d��ѭ;~z�Ps�R�F��bź����Yز�y��-���
f�R4��-Z`��!x��9A[�v��Ӧ�7�R�*����?�㥟 ,<�`C��I���MZ,��t2�ڸ�g�\{�T��
z���U��s"wG�MTS.F]�:��T׻� �D�!��B"T��}��G��h%�AUYc#p�u.��U�p����:ً��ψ)�č���44{}š,����ߜB%n4v�4�8�t�}o�p�&'�BBt�Q��<�uN8a�M�"�t.Ͼ0~n����Ĕ��r.8ҹ�S���g���ap��f�=x%6o���2sK�\�Z*����ܟD@g,9.~���U58Jb�xH|j:r���g��|`�����U�;PSUhR5<���������o|����h��ό�ǐ�q�ś&ƄM}�|^zvL�}׎Z�����q�C)��I��h8
�Cw���m�~�*�4q�bc1i�U؛s�>D^�U��X�e���CO�tP���M��*y���at�ڴ����o�\q1N���I
�X��
�M9{:�ԩ$�M\�ڦ�G��P�Є>��U ���(���XXx�'��7g���_�|���EX��g��+�L"����X���[\���&��F���X�����G~s=ƍ)n#"���ً�Wo�GKW�����yڞ�)g���m��N��R��k
�V5Q�P�`n��d�p�QR�nk@vĴL���3���� .�'�e肶kiI�S׶1X�-1���[]�<+�^B�#?����_�w^��U�x N���je��B\}�,�~�����l�F3Ѐ��ycӄ+�@�eu�@[��$y��>?g#N#;7�X��]�"�N��h��f�6��zM��ɯv37�I�r��'���#�U"-�%R"p�E�Y?�^�8�3����1M���;�J�c�\&��3N臸�z�sb7\6s�i".������2元(�Ah=4�2G�[�m��|�	�PZ���!��G"�&�S�\gL����c@�s��/���6����U����\춄Hn��d���?�M�`8��a.�}�q�]{�@w<��\\z�ݦ�&zS]�v4 ���6��E����7��ӎ���?CI%]��\�����b$���$�n��g�AX�a�ѽ�sXp���}�������o�À�m�"ދ��0i����)6
akꏠ�tX�~l��Q�ܘ!�qDG�0S{[N����QY���-��k�����b��/��닰bS��*��q]��r�}i.�� �������z�!���\���.5�N<�;I��Q�7�b2������@>=e�/F���V���⤱4{pۯ��cO���;�O�vx�w��c�njB���q�T����q��'b��g��ʭS�ю)A�	%e4e�����s\DJO���ܯ��yu/�K�ҋ���C�`���T��yߘ�ٮ���_��/~2��l����RM���e<���nzF'��=N�ܽ����'7t�b�
�I��Y���t���ZoR�e%��"��ps���-�����޹���+T	2���dLa�V����յ5�ۻ�}�"�?}F�e,Sk�l�ƭ;Q[͜1���ɻc�>��`!��Y��ʙw�_���;a��]((8pX��P���׫֠��?9{�1aG��a���2n#����؛_O��_��?�i_>��Q_��Gj�X9��kO�q�z�_o-3��~�/p�>�Κ6Ь�C�S8Y�����T�o�@�z,��c̉��\����F,�r����p��Ͷ��W���h:�+���lb���W��8�v�R��O�/#�m�������һX�I������z��]a��o"ڛS����ٗ�s���H�B�ԋW��p�Ȋ/�o����ȗf����ƛ������Ǌ�)&��� �~E�b���.��H ��s�i�Lʉ��:!�b�e���/�W��+3�`c��<iji�*.��c��o/܀�'�nQ>D"�J"���؄��V�W�9�L��Gh#pt(y�&f�&��"��(݅��'�b��X���'�c���.�����$,y���)mA]TX�Y������Ǟ:6����&p��ݐ�Í��vP�r��W\d6?��KX�p�I`^\A'R#p�ݯ�F��v�C���?3O�mƏ���u?/=v>x���	��#��ޘ�9�/Ç_n�շ��H�,`I�TMP�����n�֘�;B��pΰ�<�N0�.є���R�XE�k� �}�!R}#2�����I�-����пW+�n��o|mP�QFj��6V�[3�6��ٹex��w�n��`v>�i���r(Q���_��KL�/h���Ą4�[�c�\�;�4���6<��\���M�S�;���������p��uҥ���my@~�L��Gd�_ܞUj[�Q����b�ƶN���:��-���U��A��,Gz�k�	.ʥт"Q5*9|5�] !�?�?�wH�]��e4gZm��o�����䥅�c�k�a��(��"�5�}�������/Zk2�w�޽��ƫ���m;�+�0�2:.&̇r+^��$*aM����Yh�r��?����P޳Q�T�����?nhW�����k~@�+P����2��KWd>��s�sRw�2�'6��a��L���Fw�qT�6i��֒J�I�����$^J�^�8��2��\����_��L���cq��B��J� ���ttB�"S~�SUJ�_lp�'�)<�%'^,Nm8��Xқ\��o.؈��ۛ�[d��f���Q[EM�Y���_?[@qL��q#zu�o~wzu�^(�oǁj���'x��\�k���שh�� S����OS
�N�%��Y��@C�(��H���eWy�s9�4o�EmmL��CI���)�VDb��Q[�hŲ%!��Ї�����X �_GLt��L�k�ȍHC���)����}ɪJ���A-`�#�JP�Bf�+�f��cTd�L,J�6<@����%P�c�
<��JS�����x��9v�U��8�ݜ�ocђ�<����,?G������!3/�%ڦ;���)�����?GN^9�����F���m`cpp���6�-�f�Pm��%��+]W�v�ض�	�:�~y��a$&�n�C��ؙ��u$����F��f���>���3����|+˹MNi�)�-桾���j�w�����-ۃ;/�gʘ�k�����}��3_�"*�IdE�˙͒K�wc="w"PP����)n�����T��/�ij4-zϙ}
%PԵ<������M֤���䢱��ϢS^�ޝ�k��3�>��6�g�h
m��"�s��ɹqT�h����p���0szW��,����1W��p��HQ���F�?͞�Q�i���c^#�PoҳK:.�`6o���S{!%1ʼe7d�%��
��T
�b��X�b�����.�ѩ���9�v�,����c���J����:#�Ǵ	C1�a��9\Z��b���z����F c��V�Z��/���3i���)�$r�(��؃LM���1�uC+�l� �@~���d�V�@UCc����Z�]۽��n�tNA�.}1�G��g���91Y�m���'N8g����8\��m�*g=�؞�+��+�����;���.<ux&3G�UK�ۺj:��a���h�27�r:Z�'2 /�2�9�bQQ��SŶR�03ӊy(,.7I�
�|s�^�؍c��Nz�r���tl�q���Ī�/b���pЁM^�;�G�W疸��_P�څ`V��=zaP���7ӕ���8p u~�윽ع{�dӑO}�d5Y�TU��`�#�^];�+�+%��;�i���E}ե���Y���;��uwa���t܏W��]�xNy��8%�
&}�+*�y��oo?cG�FIy^}�S�!��r�SrL<{� ��ˌu�x��C�d�v�Øɴ�y0�~�&g��-�'�|��cs�=�D�ˬ�%8c�8���ϫd����d�׫2���Fp�êm�]�t��_44����5�xe��{}yy	�d�&`���O|��LB\*����q��X��uu���/1�/rM��7%!
�ɬ<@W����,m�/ 0�{�JɕU��^������99��	������+�������5<띯���QB��k�0�:����D���m���ej���mhpB%�5���aæݘy�0�	��SFZ6Q�,)�(i0�
�߇��>��-E��x�Źh	ۏ��;\L�vL�N�o�*��M����� ��1�l�Zk��Lvd�("��_���S�\��q1I�o��GV0ӛ��胰�h6QԼ9��6�xR _m-HK�4~Xo����i�K�v����B�&��՛k��p�x��l�{)��Y�O4�־�<\�����]p:��\��䞽9FѬN��h���Z�fx�����?Y����;�G'��F��T3yl7�9,?9��(��x�cӯ�|��\�w1��nO�:�U����$���S��4�>�<y>[��Q�<{��9G3(�������8�K��7=	/����Y��K�V����E9ԩ$G���F|ۇ1HR�Ic���W�G��Ix˓;�ݭ=F�Nd`$K���?x9��	xi�<'�-1J��D�p���£O���'^ym�	rT����z߉���dc��贖_P�Tp��� �%�Mȑ�<e(�S�*����m9�*�b��qYN� `��i{wLŴIC���������S�q{'�)�I���ؾe8ŭO�Ų�3�/.��q�m��(��5N"ɴg`�b�6P��;K�1�od�ٯY�J�PV�An�:��{u�;������+�`Z�����b���CQ���h�>&/?�}����QV�>݅޽�c�J:�<lW_Oq� c���(����� ��0�E_m)���p����SǢG�4DGG����˵L2^CΈ�2��+��;� ����V���2�Ѝ|�^�h�-��H�ɫeIi�s�_|��S��]SN�[?sr�J��1hD`�@`�)|����Ýgb�ɣ��mѶu�čBA1#ӫ�8��q{6v�������Qڥ��a{��~����P.K+]ؙWd{:����j�M��Y[q gGl��ު��T�@��H[_�5�$��YQK�P�~N.˕�q2�1>����T4x�����o݃�#�� @��$\�`������uJ+�0��5�׽5��`���gN�6��uA~i=Ӳc�C�?�L�*�7mZ�JaK������m�$�o�t<��py���un��)f�[�A�6lލ-;�_�	NnC,)L��&x�j������K	��Ly9|PW�+���25��5ؑ]�}
��o]�� Vn*F��
K����Q�kT޳"�U�����K�����k�K��fz��|��&-�ǽ�Zgޛ];P�زY�`������h9�wP=$�k�ak��w�c�լ=Nj��Q<j��h"p�9�o�d�����z
��f�b�~*���4J�d�ۥ��d�o
.j�m�g�SN���j#���^_���A�l�h�Z�Z��M?.�$��&ޯ'9�����j���8��������?����;xH`M�����U�b]W"Ў�[	�e�W�cp�@�����4nr�d��r�p߀E_pc���h� c~*f�x pa-f�B�e��>�˗����E���u��k��z�f��6E���k/�f���W�U�[o�i�#Ήfb���ߡ���LT5�q�شe��{Q*�����ٳM��ɴ4���^�`�u뚃&kL־R�o�xu�@��o���n�����!'���Ӳe�\w�<Z��P���\}
F�i F����{��ņ(�H`B���P�d�ipW1T�9Bz�H�#5%���>�l���Ҳ�cs��q&U$#�=-��T]C�!�P/KY|n� 3uX�J�`��l�zq����q�Koz�Ũ��e;�?�c�4�;���AzR�8t�΂>�q�$���˯�g�|���:��z��ʎ7�t���z��s0�^q��{��&����cN6ڥ��$!>�-Z�"�44.�zQ�v�{[��+�tL�a���y&�����2US�5M�b��h��?��ei��QR3�0<p�iJ��Q݉�}�w?q1�����{3�QW|�L�	Y�(��/�Ƿ>�Nf����H?�Q�ҳ�'��%,<���"L�����i��4�S���U�^3WUQ��BS>2�_�uY;��VZLfz#����M��(��3Wm4�t-�������S�D�.�?�gҤ-����p$E����C�>�ϿZa�Q�C�%Xiˉ����@�^�q��gc��!:���\z�x�2e0Z$�a݆��'q��ftNZ翮-k+���H6]�����8%�W����AK]R|4�ʨ����O�W����Rbk1c����ء�v�mU���u�mƉe��9O��A�ν[wߣ����f0���2�܍�o�*��\�����N�h΋:�I�颟LMn�4LP�����=
�;9�e�?��>y=e�i�u�!�q;T`�	Ia*L���ܳ/��TTbR�u����o���6��nSS�y��[ѵ['���L���=:��?\�^逑�]�u�)`����ϗ}��e��VmUM��;^���]�����
mqi�{d_Rj˻����L��v���_$��ON鎓��h�A�]2+���o���)?o�/S��b�Xf�g�U1�s��U[��,�P��`t`̈�2L6K��Z&EcD��1^��Tr�`}�Kg��v��hj*%�l*����L*Lv��p�oQ$��77�M~�^��~؁�	j�����������~s:�o�H4
>���m޾SN�Wd>��ϻ�(���Y�1��WA�M,Q��A����ǙZH���]Z��
k��MYZQP��g�?����!m��3�B��J�e���M�;�ad�h<{�q�<m�v��[����Ă�� I"�Q�>Z�\4��L�h�4�q�@���$&З����Be#E<��Gu�?��W�|��y�x��y"����&�^9��q�
D�JM�񮜊C�Y�4���~����H������(Pi;��S��5aX[,_�9'��;,g�m�n�8;�YN�����H��Zq���<k�i����6�� ��"	���W,Z���q����_rf 1���b8Y��F��}����Ŝ���܇�&��ʶ�}ʵ#p	��� H���`$���3��\2��S���ZM]YUc����4�����q�0����:L���W-93D��4[��#��K�=����ȹ�"{�&�<c,3�OC����`�჏���y8Xi�Rr�*��v>�X�o.\�����s�[c~_{D��?Q�q6��.jH�:��PwS\�_]~:.�tڥŠ�΅!Æ�4FS�0i�S3���ct/�	�ʬ}H7cu"�l Ib����R�㞶���(�l�څ��>I>){��`��[PgAnF`rX�����هt�Ǒ�� �S&�3c�r��TW���]�q��-�~�x��#;`ͺ����IjӻCΝ�4�W�� ҭLf�v�:���;:�S�;ue>*����a�p,�-�Ķ�)Υ���X.�WG����{�q�ic�;���l���b7(�����y���� M�O�����-e�pU����a��>*z܋2�Hk�,ݼ|�6L�6T�P�SojU2����Ki��Q�L�Ͷ���o|�x�!�+.������S'�q}������&��c��L]Y�4�?��P�H���Z����E�%u�ԙ�-;�^F��d쫃���!<���\�ْ�ql0��Gy}
>_S�W�O�zDFx���_к�d��H!\�n�%+������2���
�y𴈍VJ0Ldbv)z	0�ԑ� ��1��lu0��ѫ4��_:�/];�0����t���!"��I����$�U8Tr)��d�a�^�O�Μ(�ܶ�5>�η�=و�̂g���_0쳘N��~�E�1�V�_J���އ�2��<c�i�>#����D�'���g7���Y���o�S�QE���L#R6m����f�n͸����b��m�
�r�X��˺�.���%P`�eLw1�K�Db��HL�.&�P!t��x'O�����(�3ɡ�R� Bt,��7<�G~T�d�Rx&��1u������D� I�dKV�s�R31u5Ç�j�vh��H:vN�C����ӏc e<�-���!pQ����Ԯ]~yӓ�;�~o�G�p7z��7�u�,��>#<��J���dtMI ���O0o�`�ʲ�:Z$���&��l����M-�Q�j�N2�킢
^c�9�MFO�Y�*��1�㼷x�ٿ�ڿ��kO7
ump�4���֑n��r<�Z�D}ρ�F�a��[#* �@i�4c8�~�q���lj�:t�m����;�RDJ�v�/��u�U�6����!¨��`^���?Z�aÆ2gK��(�!�X�+��
FT[�Ab��_b�ć��U">:���B*���칁�c.�����������h���٘��'萑�ϾZOK���䘧e�/�bXkř���>Bܯ0�[n�9^��x��W�~���2��G�8�|��~1IۍH�e��>�t�늑�:�C$F^u�q>�=E�Hl`b*�ܡY^�O��yض�! Tc˷H
^)z9`��i�m��cB/rU���+&ʝ��`��M�a����0r�T/���B{%S�1.16sVA�=��B?�h�L��m�W.`a�#�E��)�/��(���/L���I%6d���4�̈�d�C�q,"U0TYA$���M��M!��z���
8I�nE ����'_Ҫ�j⋛%IL�������
��u�!�جMQ����W�W�>�/��I��#9!	��n�8�edECK��q��y��8�?��6���w�����r	P� �j	h�ҁ�Ə��&�2&l�	썎F��Q�Z�c�ޅ���ڴ�����i��}��]a���=piV\"@�ҡ&�?�\ح��d��WS(�H���D��n}��d�x7���W�}��MlӸɇ�V�}W$YQH��*�ֿb�.:o2XS�Su�I/�W�����/qL����I#�9���;��7���x$�����Z�x�7�(�6/Q�z�6�u�L����SpUL�XGv���r3Z�c/&
=��ttFLMJ6�C��4~5�{V���'N6���򩏡�&(�F�tUr,�+�����X�q���g_m�7� ���m�䳳�l�'�Q %�ǂۄ1��i�X+<)�e��c��3�O0
�[���)��	
r�`)��M��f�� Ј��U����M�W_z�I8���"�K��ۈ{��Ѐ���J_R�Z��Ӭ�O�=��YJS��k$�vd��=���mNp-Oπ� E3R�d�3#�,u0�-�e����c¨�JZ�;Y��*��t�P����AI�h:M���I��j-HTlr���"���zWQ�����=�Vn��i�1�>�ǿӷd5Ń8&�Aҹ�u��үX�fi�{����Eg��i'�1)>�Wf8kaO<~$s��c�盘�j�=4�T�?�(<@9�g�=��3�r�d:N0>)�)-�����P�;P�wj�5�<ob��3�\�t+��m�D��kW3���H�!�L�v�0�g�rjy�Z��,��!WV�1�C�_��P���&<O%�CL)����`.:c(w���bR��m�X�(�K�m�(��J�~,P��`T*�W_�(�U)���,�*��$�]Dy*����Ǧ���dJ�M�/K�*7�ɂ����S�8�$D�ԋ��O?[�.m�ԟn3V!��ٷ��V̲��x��
�� 0���K'�h敩(eʈ��a���&���zm�8%���yn���Kؼy#^~��w\���ep�N�3-^{�c����kE��5��d,QҞ�^�ս4:�_�	�+�����E19��S����o):x�B	�����<��N�	9. R���{OT���v��-c|�/�2���#]o�:�u�9� �1�JL9Y��Z�&�ކ�'���?N���O2�3RvFP�T6��&���LvQ=n����T�l���y?�5����4����:w��$1Kb��H��헨u3��%XG�St˩�[�d'����m	Շ%��<�ܛp��O�*����W;�ȶ�h)_ K����W��)�bP�8�_?�ެ�oS��.ڻ/od����I)h�Tk��J�vPt�v Љ�s�n��>~�#��D���N󕳀_�|��0Ol=�0�t���nRe��wH��m�h�ٔ�I�;�o�t�K&�	#:�k�4��6��e,Yb��)&�)*����^��wdź��c[�$Sl���qc�3i3`;���DA"Ǩ�#�]{�#�ǫ�����ˈb�Q��$�E��5-���ÇP�R`�
������ㆫ�>�������A=�ܬe�+c�� s���FO7����8a���e5��!=�yk>b�]�*3���d8��â�iMJ�)�ci�wL�]�D�S��P��,�|5���Φ�<��{o~��x^�7c�	-�5�1<��w�����ʃDzA?Y����c^6;��&���ED"i	�ӎ�mb�.E~^6N:a2R��Yd̉�фe('��
�
�qmmd��	d��Xrr��^9d�DF=�	��n�˘46R͢��z&ƍ��ޘK��� U��Z��މ�?��`�R�h�زm��ZI:��D���ޛ���OL�ӟ>�� ���?Y�Wf��bg5xg�F*�h��g~�C�^ ���-P����֝�p�)C�h���Ä[��aݦ}��5^x��kC�ic�pڸ4���I\�����L}̪=&>+2��	��և;ѭ}�r	s��!2�?;} �Y�RTU[��桁�'/&��<�eJ�y%!�o�c]4;��O�Y��dN~���x"8�����CM}8���ƭ}Ks�q1�D��#���uJc��/"�����OY�,ۉA�6������(�Q�~?�p���EEbĐ�H��>&\З�J�����_g��A��1�(�#[��'�SN�g_zÀRSeoyy1�RR�K݈|b�t��yYv�s���2	���(�V��c�Ё�U#-�����'�o��b��#G�#�/ڲ�I�%'�}�mM�co��k�^�웈^��#�3�C	h���m�U���T�pk�'%և�O茸��!��v�f4�Ya �äW1.w����@?⥕3��-���E_���D��ӵx�+PR�t���ׯ7�Ҳ�d>���dN{d^3�)Z1��ѧ��~Av&��X��\�a����{����d��U	��b��J��c���M]�@��XQ���c��+6v�Y>�h&rP�>�x�-lߵ�l7� �Y}��D�JZ�%�J�ۮ��|1[��<�,l��L��K�c��R<K�#}��O���Hn�Q;c��E�R�J%����[��i$"�T�h7������өT��:O���nڱ���O%��w?��X�0�Z��3R>D?�hvLDR��Jz�Z"�lG.��i/8mS3Tq��q�|����}����l|�j�R���b>��,Ř�v�]�p�y+�E����
�Ǹɮ�vR0cMӪ�i�^�>e RSWqF�:1}d~^��l,�䫃��w<+��nЁ�{�#3S�����G(�$'`��x��ذm����y�������'9�F��9��Ǉq#z��+&�]?o.Xe�3Xԇ��k�g�������+ucԠ��󷳰m�q��_������펠�/5L��8�z�S����"w\'S[�kg�3j֣݄��t1NYbRRP��RD�$��b��^�������{����5�`���2��UE�L0^Wn���ܙo�R��]HIM1���;rP��S3�"OD�W�C�|�2���1���EH���bb�L�����,l�|�RT� �dW�{sp���}�~��_��݀���"��9� �]��rvoDX\GS�Q�"�ǿ�å�ߍ�����!���b���`d�� ��ͧ9�~}�98��ަ}��HO�@rrx��)d^�z괤{Z�l=+Ef�ʍ��XRZ�{kEP#�þ�Od��wIp���r��P�5�x_��
�)|�#,AJt9Nٶ����7���Zʥ�;��j�*D��Yw�zٗ�%e^����TnH'c~��G�����|�f�xdeq��v��".>Q�Z<��h�)۷��/��Q,g�u�+EO��(� �Hr�� .��<dZPi���1V��V!�
� F�^9�	�n��L&�`<|�SӭwO&~�	���֠�e�"����j��?r+�l؀'�{����4/�Z��8h����x�7 �m>�����\5���һk��r[	��H*!փ�L�y'q�
'���Zdi���(`~b�@@�ظ���0�z0��c0r��d�]O5���g������[# 2���H����O?F4�A�O��"xt�;#9.�Ő���GC��Ln畗���/ƣϿc���Äǔ�==������E?��� 4e����*~q�E����72��+&�)�3��5?����їD]���A��Gk[��H����3�P%��f.�`Rf�ߥ��7�d��R��π*�=���'���>�4^zu��Q�=w1���ɟҜ�� g;�W�I_�/����/8�wL�����+�t�����o�=g��o����(���e*�����lP[��T�b�N]LMA�L������2�M]�(c��f�(��E���|�u��::gl�'�
�Q>z&��Kq����8-+�qN��J��t�3aTl�'���5yX��Ff�ky�&���J� ��[UQ�R�*	x��>�Զ�[�G!�����#z8��bST\��n�3�]�5>fe�(%P����L��D7�p�9N��ڼ��{����ig��o��FH;�xƓ�:�q����MZ,A7�@SŢ�����0u��8�LR�n];p1��c��r/���u4��*%�,Eɑ��V�����SGE���N�jV7�ݼ��_S��l���C�)(62hpK��keu5*�s���<~�
};�F�YLlJkZ�+0m+ >sF�oC�S(L ���Ɩ���
�V8%d���3��x�<�8��Ȉ�)�(����ϝ�,�Sp�M'��F�1��n��4	@T69C�ѐ������@�����6'O�����T���1�Z�PSRtvp��Wy��L?_8�Rȱ�^2h�	���g��?�m"���,ÙW>��_n0���_ c���hAF�,ٱ��&�\4Y�N)�,��:����e�ȋ75ы�oj�__;����oi�YDh(��o������w��a�u�=�Y�����ؾ����ˁ�u�X@�fq϶��C{��ƌ���Ѭt0��qkf�
Zbp��e0�x�ʟ�FP���גK���z=s���MKfп_cu#n�e�J��l�n��b2�HvR8���?={�%�8��U���_������tF��I�[�*��ǌ��,�ҭS;��09��0�/"����è�d8���d�S��O^�K0u�p���]2��x&�b��h��>���Yc����p� ������Q��Ϗ� tj�8!�c�L�b�W�) R�@i%�Qw��u�q���0�G�V����t/*�&Z���5�1r@k�ao��^vTDN�X���2�g2���cU����>�����gvg�me�{*�^���A�\:��].���:+ȁ2;�ͭ[d^ӿ`
  @ IDATW�Y{�1�>��4+�����3]�5��T��h>��Gę��5�9ظ= ������%�8a�8� ��H�s��&�����yz���L3�������=w)��1o��D�~�Q�璳?�̿�:�E�G0Eé����q�iSXm1���\��|v�-���~�jBV|	�\L7�樸�'� A�ǎ�iSF#!)��oy���7�5�F~��Ns�\�]�Ψq�3۔���ߜ�/�o>X�M����"�d���%�pzs���HFM�c��<��n��󧧴���O�$lٺk7m70��JVc�=��t^�Ä�1�1�w_do�
����Q�]UM Fy�hx�'�S�FUV��:dd^޳sh̯Ӽ?���u�]��Ů��c�ƴ�|����`�q}0�i.�ss8isQ�7ebݜ2�P�d��X�D�6?ȨM\x=�~�lSrUf�����)3�#�Wt��_�^o|Kp�f~�F܀,O%L����x*7=�{1��xR��4�gx��a���R}�͖�s�.�ݝ��O�h\��{�����S��v0����[=K�O�!p�`� ��{��B���t��z6f�/�Nl��$V�]Y঎#g6 �t����"l�ط���A�V�k���ӱ#�];� 9-��(oT��TmA<E�:��aɩ�cf;���J��dɱ)BY�V�;`�:R�y�;����>��wsw�N�w�?T�֎j�[6�)8p�M}	�N�A����Y�n�a���hb�T�V�z�R�6L4ae>	l�@F:�SO���Z�����_�g�Z��o��vf�t��|�*�?8�Z:� hx��.=�w���[�@�y7~���ߜ���x(@8�N���~7�(&Λ�9�ě8�G�x%� 3�nU ̹h[���.�|��w��;����8�hr�W2��j/�m�,��!#|����S�a�Yᡴ
ݱԤU�j)�KJ�1{�n���~ĳP���.��-��L}�g<�E ���F��)�"��7*<^x��B4hۚ5�������WtF�e@&��C$��E�Q<S�S��B��K��+:��|8$:i�5�y�w��l�,nƎ� ��Q cI���Q��I^�V���p2S��x�2�v�>�߶���_�@�:�R��>LhE ZG�^�/��F�bD/'����;��2���T�Zɠ�x����;�b�&��_��	q#�DM��w�����[�ĳ����D������&z�R���x� �(t�^�Y�Sy>w�
��6P�[���;m�Ms=�"��	^�ٸ�[�G��IШd����Q�M��0U�ǥ��! ޱ��z���5[h��᜺M`�J�sǶ�@m��4g��F�nh3l8ӄ�����jr*"}
T��D$�  ������Iݽ<���|�C���c��{���c}4���<�������P�*��J]�	��FMLJj���+��yXL�P҆-ۙ	���@�Cj����H�}��A�	DRd����$%�&��C���u,Zv�^�0Q�؛��6?첩FbR|l<����gx��r_��"����b��΂�%X<R�����4�J4n`&��]�bT���?Fnq���)������	���K��D��M�L�ut���E�F������kW��.���2�H�%������QI0��9�֊��y[� g�,�]4I<.� �H��D�b"��<�:�ND��{��O�n�Ry�\��җml6϶��cq��?��~}yf��-|�Z%N�WV"�P�����4�R���d���8��>;�-Z�nC� s���hb�5N0q&z�Kw"o_�l�z���z\l��,G�8�<2�,�h���
��ݯ�L�����q1U��6��|�8��:R^U u|l#��I���d	 �9!�:�TVL؂��1��ڇ5�;��
��CcA��J�\p����ͻ/�֔%��b��� �+Gq)�Y����:��#���</gNߘ����]�� �w�����i����f���cx��塖��XM,��G����%&�fnI�Յ���"�ef��d`���J�A�-=�ԙ�!�[PȇMV$��Z���|�艳ٓS�e�wcي-X��E{��nź��X��ǟ�N�d���(U��}d�5�^ԇ��rJd�ݐ8�۬s�F�?7X.&�_�����~>��)/�1�ꚕ�A�׷�?�Ď��-]N=��LDL�I�YV�m�#��(�Zz6*��(&>�p?q؃��>A��OM�(��rb����L�d�X��r22M�� ]M���E��I�W/�U��G�mh�Bl|K���9��o�Ds1�`|�gg?A6c��f�A8�>��࿖��aA/���O=i������/Q��j-��*"���� g߾&��Ze֭YK�L.��=:G4��oz��0M��w�C$��)��MQd\+���d9�G�$�Cq~��l��X$�p/g.mM����Wl+�'"HLұ�Ѯ��"SuY�m6)I5'y\�0O�s�����G���'Q���SȔ�L]M��B60� ~h���X��WEѩ�˥�)-D:��4���`|LVSK�ZG��Ew���8��9���V������?�%����h� F���sMY��d��E��:�E���_B������˔Qv63�*+�L'�r��Q��t8p�!���q�b�:�ĔT�R���N[ ��&j�L)5<	�q�&�I۔+&����$����Np1�<E�*)��VT΅��� Z{��H-�"�y���Pܫ����Aĥ0����j�7�Ul���X��ջ�O	X,��v���3�ԩ�׳36l�`��P7â������6Dr9~'S�$�+�D�E�@�x���>�G+�Y.ƶ���v�"G�C��q���F�ǋ���h�/����s89Ey��QOٰ�4e�T��h�.w��nJ�|���(No��[3�|�D#�'��OGK����+��N
� �'�^��R4�:�U^^Ʋ�&є�F��!��?ノ��-��Q�u-�>NZ*%�]1H�p�W牧^�M�q.�"hΒr[�I�&G#�j]�.�N���wI�>;T��B>�n��n&���ےkjKY1G�Ī .�֩�T����'o���z�k�n�l�zA��*�ӓ�'��[�"a�[h-Q�TH+_��B�{1-U���D���QM��J��܊H� ~X�OΊ�ϱ�������ѸޜE���bR}E	J�,��F����f���:V��bЗ�����9V#�h;K�{������7"*�o��"���Ȃ��US�RY��S�<̃L�Ս���)K�
�Up1_�>���v	p�	d<2�J��I���'��d�NX=�_�����Y�4� N��L�9�������b����?NDZJ.��Y̢���bcXƄ s�k/v�~z֕����e F�F���8��}�Ǚ��3b����ISC݌@Y�mi�F
�o\Lt�ţ߲��w���C#ÃF����vKn�x�u=�5+�]	��hc[�C�w��{x9�+�B��%|{�#���P��)Wl-b7�
OP�����]]�+s�f{��4Л����d@��´�Ї�鿽�z���_V1K�=}|D곁f�pY�xM��¹6s�']��ek��M��}I�c�3�[L;�'��3�n2�%��+7*����)�p�DT��L�9S;�bp�=3w��I5�����s�t@xa>"ׯ!(��L/�[T܊KQX���Y�t�~���;�?M�LP��z�3;^�C)�{�ei��A�Eݿ��ĩ(qs���J����J�:<TR{����q��8�<���9ǒ��.|L����SU�
> Lh���9(Y0�����m��;>��&*��9�7]�M %F�=䌐
 Lu='����.�F�(�성��4���#��$j
0��0*�]]� 1 2��� ��C@%9F���Х]2N�
�m���D�wXk�6��N����4i8��ĹPYY���ڡ3��,�x=j	LSG�D�T|�'�d�
�3%,ڗ�8ܣY۰��N��u��xD$&!,�I�%�HdFc0f'?TE2����1s�jx�g����s��2C�R�H�p�#0���م�x�ë4��`�� r��G�`�u�澉Z�i����ޡ���2ǲ_A�87ߜ��M��`�c9�H�����4����b'�Ḙ
�dԏH:�NqQ�Խs14-@��S�Im�dƀ�^K��������3���ڡG{�V"+�Q^�?f��"�>o+V��ȁm�ܫ˰�@~G52�3����� ��oU�ŧ��Ũ�
f�*Y�����H0�T����#��j9|�{(�%#>)��qFtgg��r0Mo�ے&vq3�w#b�S@�� �ZLM��~��Wm�3S�Jl� ㉢2���
�
>��f�\�D>����P���^�u|3����&3G�� ���,���Ũ[2�b,GcNG��.���r1V�`/U��HV�[�� 1��b8-�|���؎��G�R0�ZqQ�'�U�Gtj���jzU���!�@��^�E��,��_o�6��(����S���ݱjȅ��^Y
��'�]���,���ۤN�XRh��JߒM�Q���^�[�EJ��LiA�S��e�M �.7>|4*XY3l�6R��`42?,q�yd�G�5۶³w�s��`� ��ֆQD�\�@F #j��3�ɡ�)��O��b��������K}��i�r2�U4�!%��w���^�X��$M���`p��l)V��~�:}�bR0#��5ITU��@'fs���o�v6|�G�f,Nx�����"ky�l�:=SF�@�V%ض���)t���
Vq��&���� X_�����
n�]r�gْ*h�(�2K���Ť*��R��=�Ի�������KP���{w#�Cq�}'�&:�=�}ӥD��6��޻Lr^�����ӴM���v�8�����3=��b���#��+^��\(�P/·����(g��b�_ä��N�&j�VD,Y�����OQ�s��+� K�w �}�k��7�&�Q�C�&��
�y�u1ҟH��m cYz����"+��^��Z�HlL���9�#�z܊ѪS�e߫FK��xn���S)���>�_S݀�*�H ��h��Xݏt T��B3��o��۲}L��{�ӲF��zwk�	��)P�"��#�0�]L�!�E #ůM4<�
��^J�X�I4�߳ij��[��3������W��#Zg����g�|��#���#>��%�>�����u��ֳ0a��BMq�h�T�E�(V=R�O/ONRz�F��w��J�
yq���F�l�<:|Et�	Ww��}Gx(ۻ��z�T&=��j�������������Z���J�&Y�tp_v�*)�w-�S��u4�Ws��	�Du������g�3`�&+'�о�5"GJg5���C�R%�	�A�W�|`ҧV���]11�R�J[�!��c5�Mj�iK�~82�+>H����ո�QV�,�j��k�#s���p�/Oh`�Gs�:r�_y���[�t�d��l�DR����9�9A����~���-31�DD��Du�jOa���DSh�xğ�Fw�|9�.��d�DN,�G�D��� Fn߅���0"���\d�E�2� ��h�m$&fE�x�1Ǌ�]N�t���V����WG7~�E�_���D�1��4uw�e ������K]�X�h���cN�Bf�+ET	��T�T[��IŎ�D�*x�F���#�L�,w�{ ���GOX��!rw��M�3�����Y�D���ig��K�"<��٧�iA�4���[0�h����p�ퟚ�yO���4���1G��Vt�%������l�y���Wۿ`t����'*'��Y�G'��ɧ40˅�<��e�������<��w�.�-�D��ޒ�y᯾�ğ�SF� c��\��[��m-�R����F0�	߮Lp�%'r�9pi���Wy��(��9��$��h�>�����]��"��(*pr�V1�c�?�x�c�mz�a�\D��Fo�D��]�ޯ<�f��K�O��p�u�t�.��]�9�E弇2r�a=�OB}I8]��3��"����`�9�����o��¢\hW��o��͍(85�vpJ�a���~��`L��&���X��RLC,D�e�������3/1�2��`���G�y7t�}���f�!�����@&�,|���B�ߞA�b'��)'c'���Nۣ�y:�-nۚ�d���T���E� �8�M����^%����D�����/Vߒ}#3��d�E��D3���d2lΕT��^�����A� F�iA�z�*H��}�w�ߐ�p7�\N/#Il����)��/�Y�_=�����Ii��6�T[
�h&q~�n��.�֯E�/�ބ�0��ֽ�@�*���9�B�\s���F䋉��N�~�8�J���7S��*:zI(=G9�pN�����0���)B��ˌ��`T2��\YC%�H�b�T|z��g�)�rq�vRJ٦$�/9�Z�Ǆ��/c�&����,=~�����f���"c��z�R�-�Xt�;��j�]���g�lҒy-�0��19.*^��U��0w-�x���R\l�e����i	qF�ga��*�6�Ö}���sP��ss?�6m�5Ht8�U����q���ۉ�+�Ak��32�0�:�)����� $�k����t��ˬ��70�{�jWK3������u���5gE����<�\�h]ܺ=I������G��v3�PYTE@ �$Szhl�)9LEO9	Um;��@.�?���� E�-�0J
]G�0�-�4>�"�H�͔�u�Z��5x/��8q��5Ƀ'�1����~5ࢥ���{q�p �9�(�:x~�e�Ӓ��\�ޏ@�N<��z
�_0ClkA��q5�4NTY�X	��;�Y8%s�&@�G�C��Z��g����bL�_����Q/�i��X����N2��m�:��x>�	(�Tj�Ah}�4����>*�+K��NE/0T�� �����]�G�^�pr@L^u���� ƌ��qD���oΔY�F�X�gQ�,E�:1�$Tg�C���/c�A�dR6ou5$g#.Ƭ�!�D��I�I#�!IcI� EY24x}>�z��]��AF�,�8|Uc�E�Hl�o�8��(m3������#G��sr��s$� cF��2MTq>�[�<����7�,+�g�4u�.��1f~��
z�e���7kV.CF1-FL×EL�NNF������P,g�Č��mRM���S�`��q(�+C�}�" ����=�w2��������k(�E�s߻Ǟ'���F���e#g&v�N"�Yj���`)�w0�h�b�V݉5���ve���2�Ѹ_G.F�IV\Һ66�s�v��0�qq�n61��J#=T�*8O�3� ��,�8G;�Xg_�F�Is�M�XE��7�߀
�ɮ�9zl|P|0����&��V�9�8d�I��O�7��M�M���G��ɱN>5�8���iE�'p�}����.]��~o��gIg����oɓH$$7�7�m;$O8�'��:ەT1������d�TP_��;7nē�y!�1���~1�Q�֫���`^ö�>�C-�����<��J��h���F�H�l����B����^B	,�YZ���$�,YZ���.Xj��PRq�ۉ;v܋d[�$�O�H��w�����H�<���w���~�=�)��R%��0	mȜ����<�Ɂ!���>����+$pq�K(և�C����y�(����v��E՝����&��M��s��8��lAq���T{��Z�|YL#�،D6Z:5���"&H���K�J�b$�������j9tʁ�)1~�y��=�\hI��G��w�B�Z۶��
[NÜb��AKU-�$@�=�/4>�d��e�!_&E  �[�v:j��p:�$�s�c!������$�0��?�:|�q��hN�ytr,�4�#�&Β���/��mDM�2�J�Ug[�%�i���|X����%=��1��k!Qo��M�%	0Q�~�#���l�'s���a�h�6�:�G���aT�� 0@��t���U9�vq��q]��笄Q��C "aAY��	F�-FQ��,�^%�����H֮��l��}J��|�YG����������6նd��)�y8�\����f�1m�\0z�<U&��]��!�o�_� �GVH�?���W��6����Li���o8fϺ��X��F_��9�&o��%2�?���8�#��]]U��J��1DR[7Kޖ=k������"�j�]���0F�ni[�C�:��ps���B�2
M��x���"Jqu��V: �1S���F�m�7s�fH-��B��:N�pW�ȳc.�m�F0�'��[�á� �s �lj@!_��~���zPZ"=lp���C��\�A��p���ؑ	2�}�D�x�5��Wƍn�1�vd�.S#�K�g�$h$!�� �k�(h%�*�{��j�šx]�����#I����Ź�>$:��=%�����3�_�d��25���;ģ�>����u�Ő�11�8�#>pY��{�o�N O׮��Lv�N	!4��t&��Z��
�n��C-F&[Y�]G�(�G���C�
��3�6�|#0��bξ,�@��
A��Fa'S�	�BCq �����ܙ�i=h ����&�m�m@� h))�C
du�?���f���7K��n3 öIb�DmPF��� CS�Ytl�� e�����֔���|t<�æ7{�vxb�󶤬����M�����k,M�Yc�O-�Ր�ےM�%��I�5����"F�C^�lgK���Jw�[��F��'�)�p�_m�2bx�7��O8�`n��,&]�.(=w�`�B�Ⱥ!��+kvt��f搀	��B<�J����B��m��8O)�8G���9�|�0��A�~R�w!��>�P	��������A�>|�$?��6.��(����WA*@��%Rw��R��l��N�j6۴�w$�t�x�� )������8�m߻��h��_��1�& ��"�w���I�;��2��OI��כq�W�ݏt�77���% 缗����>�Ɏ|@��H�m��G�3x��	�� �Y՜W��0�����x����q=�J2�<$�O������K&���M���N���1 ck0�������B
��VZ�X�|7��˥x�)�g�a݇������z�<��)����C�HE)dP<eC�1���hXL�^x�.v�� #�.ى��	��׽Mf}���2d���0
.%���I�M��Nn�3����AF�q:R��1
8/[�d����$�4H���$}�/�r��~�"���A-&M��W�+��O�~}����R���7�ZO� @���_����@mC� 2��^�&)=�=��T�_�L��[�ѕ�F<[3�^�(��D��v9��@Y`3���xL�E�%��M��hn�xז��HF���;w���/I�ݿ���=�\z̑LWcxS�(�(t�2�L�>H�d�3�!��o���lG����צdS��)��TX�P���G%O:�tےƈ�j��)��.�=h4�\�)�u�{[J��xdw�`�A�ۍ�yAoB����C�����u��=�|�x��CW~!���C�ψ�Xq��R�u1��sϭ���%�W?#������o��Fbe����t��WQ�5 ���B�`(:
K��D��T,�nΌ�~���#�c07L�Z^��-E�^6&bY��L�!�aLǊe/�jPbɫq��/w^B�e�cT(;� lL���c^@�.s�"jE��5�0�8y�1�0��W�� <o�jǓ`�7L�)�]�B��>�&G���ϓ����TB"��`&�dVw�\/�!�C��R�@����-��1v�qD��m��2A@�IM�)���}�`�"�Il�z�)���1�ٳ�_:/m�>�ٚ���#p�u �8��/Ұ2f� �$k�ب	����i�?6o���v�?���h�c0���_�7m���g�^��4����4��(@����w�����;�j0��o;RCRLF��V� �4[��~��3�\�َΫ�� S����h�_�/��:3lE���ۗިWB���mF.cM���Hz�B�^�V [�˂�e�;!���!��̺ٶ�I��J-��B+�f�C�.�f��΀	��P�4E���F����R������?J��9�0������PJ���f�I�(#և+�y%3�k���� �
Ps����fM�A�m�N\�{�����[��z`�����K���<.�����|
�CQ���egI��WK��gQA6�S�&�)�F��f���%�qL3f�m{!�����������뵿��� j��]�^#JF��H1mn�����K#��f&.eB>�OyVBr�t�t�t�؛���&��u��.�e����S��ʉ}{%m���i�݅Q�q <�©S̓��(n�<�*��[P9���L:��W<*��8B����`Ջ(���%'�
�U
�1���s4.Y�=�����qzLl���rS����oI�+�3L�%��%&5�K�I��O�@���y���לc�/l��S%�=I^�]呿�^$�SF
06�(��<�yt0C^���&̓F��� 4�<��=�J	����N�4��:BH� &��!���f� ����d�DT,皁�(�i���Ϋ��N$)*��Y�/�.�S��B�_��M���[��$ @qx{�ycX��(�V �0��8# ������'��ϛ�b�$<��#Hu�7�?%-Lc	�%���¶S���*�f$ Fx^��`����:& �h�ϱ,5��o]*����� 8b)}��&���c)����K�2��-E�kAl�,!dݖ���~��q�<&_E �M:���߲��!�Vyxb�܄Hۖ�޹��;^�5��^�t�;F\w���<���P)g\�/�&��Jcy
M���^:a�B��{� c���JԶ߀L������%���F���!��,[�S��P�"Ҹ��u�26���A�:� 6��g����/2������VH�׾+ŗ�N���fw�bJ)N�݆��(�� V%~���ާs��`�l^|^�ehM�����u�r�'"1Ajt���vߝ?��?���2�Js`�\��;�AF�"������\�J�M�� �fI�]h��΢bw��Z��7�6Î�OS[�dPZ%>�h��-��\����\�\�� ��R\��I��oa��/��Eg�[��\����u�X�4�9H*y�A�	�YJN:�`Ȁd8|+7N�e�yͻ����u�ϟ��}s�.S4,v_Q��¸�0
�u"96��J�1��P� �w�A�%�Kˏ~%O�y���I^�az��G�u*������� Cj�d��4� c�a8_G`����S_s��#[BG)T���~,�w��bl{���2�jձ������݌���m[����'�7u
Ã\q�@!�w�3���:)W(�P�×.Ƈ`zS������9�����M�G
2����a�;�(u��s����h*�p�Wt�O��R�@7�p�*`�I	���H��?ӏ6��#�^�{^�1�{��8�:B;���Z���<���l1A��" ���0����'�q9{���C�m�o�WW�G��h�0���#���6Q̼^�̭ﲞg��ݿ�z��2�!4:*�0���������~�m�
�2	2^�o5�z�1Z��%L�	hp̃��D�P��3Ҕb43�|�X|�\�tK�$�0����E$�8or��zē�@���Q"pγ���!=������0<�ΰ�]���H	�*�:�l��C��������_Y.S��6i��f(�1`BQ������b'4���$��T"������ �>m�|�����,"3.�T杶T�,� ��/�(P�w�1����v��KZ-�tk��W�}&^[���e��Lo����d��tC�S�@�)J���Z2�,�0�`G(B���4�ZF���h!��2C���`	�b�a��d�cYZ�øC��!E�V�z)�����?�)�k�'���sF@�C
ݥ�L���ЅJ��P,vM�*<�e��p�E�^?cD����u�r3�F��Ø��dT�Fɧ
r����"*rȠ�r��z���r�t�X}6^-�3�����پ%И���M_�t�M0����i .`�K)��Mmb]܀C����� �c�W�3�%�vHZUru��8�,՝��c������u(��W�K�9R	e��R��C�	иʍk��\#���ts��s.�"}�����,jF��WFr���w��L����>�|�K˩>'@�͇�y cR��/b7Ȍ<�B�L�%�'q��@g������q��J�p
�����
�5���_t�Iq$l"Y�a��C�"߯�G�9�?I�	#�`9D6e�a+;���2��9v$�Q`#9�낌���p_r�Ð͏��
�ܧ �&7x$0�"�-�7oK񆵆�c�v)Fg�ؗ�H�1�����;%	��=�_v=�dwm�JD�F@=E����J��0��!`q�e�QX���������yw�C`*a�n=br��Y%��*����i5+�̌�`j_��^�\���"'�j@� E�9#�o��M3�u���ғ�ǡ�d`I��>����?Ӱ���9w�t�"~�~'���F��&�7��
.�;Fb����O��Z�6�2|�rhl7��a8��&#t�<�P�
�%�sP��v���ݏӁ4��b���uAƫ�P�1x�Sj1<N���L�	$\��'���F�&dd�vW�i�$�[r � R;X�ڼ�KQ�������C;�;tU<w<�R�����?��4��.Ȭu�~)"��n�:s��FX?�s������;���N��%�E�̴4�zB����ƽ�u=��n�QT�\	b�:�|TZ�zB"�;��/Z�x�"�f�d�PP/��q��5],�3�{���?��:�\����1��Y��b"e|��<�|X�/�T2���q�UJP�"�?�<�=|;���	��`�e��><���@GH�!%$�!�������93|�d��v����y��2#��:��o���y�7���<�P�׋kT
M�S�2�Q0߆4�fx��` Cp���`��j1J��t�����l�wm�.���3C$^�~�Ol�@���<$ؿ����[J�CȾ���s�A��)�e�$p"0�3�Ҁ?��9W�/��J�9W��	)~�I��� � ���v�6��D?�R>�B���>i	��� �І��ϔ�����=0�������\�2�Uh�?:mA޳�E��R���N$�9o"�a�)`�G5�y�HzJ���������M����[��_h-4���Dр-s.��T|4۸����Q����c�����0�*��3߼Q���X�tq^><c5䢁��w^�1��v��
�h�M"X-�C �z���=1��P���/	�(����g���;L���|����w`�a�
Y �<0b�U������4�3ΒZ��[8�`@z�J�������?�/۝�B�T���J�z2�+n��_�8��g���>�{
��$��:� �<��0�,;W���w� �X�b���&%�h���k�n���u�f<���8y�y���͐e�4�O���� �6?�A� ��hG1��Y��2�pX���	O)4�mGM��Q�eRgV��N!u��f*O-U� UH,q^aRH�Ir�ӳ�6T�{��Tq Yr��lQ��0��X�2���;L���ϜF��0
.܉�v�
�T\��"���� �0�W�b��G� L�H�WK�?-��M����RO�h��5c�l6h06��3�:�rй*-�9r6]q�0��ܦ���H��1>=�c���t���/�o��d��L�a�0&��b�3(����M���KƢ����Dܭ��gHX�G�R&61-��Q���^�髮5\��ҌO�ah4��͐�q�/���&�g�7(��d�g��@�}����BBmA4u��4�ś7 @mzM�γL�F\�`����~VZ����6�
������`�^���R5��d�@�LE�.����A�g����(�F�@�,�0��a��<����7(b I�H� � �so�̍��k�:�}��{"�Qm��d� ��Ge���[;ܟ���	�Q��=_|A�?�H�h����5u�a��� ��ڋ�q��@FU~�0��qF!�f͕��	N�.u��&�q䕿&w�f��*�|J�U��$H�'�(���7T��~�M	�����g��ŵhj����1����;_7���R���^��6�L���q�������g�\������_��h1�x@�l뗇`2���
d������`�6��P�Edt�.�f���G��o�(ӣ�8^�a��X���ٯ�.��k�c(�p���py0�A��j�(���� !e��&1��Y%�7�Ƹ ��(�O��,�A������ҍ�`C��H*}������y�����eK!�a���W���H�N�9ДN�M�h�0bb�F8�p��4
�(�K)0z,�G��&�j0�S�����Y��+��>G�A*.�����=���k��;4ّ��\҈�I=|�Lؽe@���.y����O�C���W���j�u�Hr����ܛ���Z�jl��;?(��,7�u�
U��}�;��B-'!�y�o�W�o�]{��z��Nm!,%B�"��4��p��a�e�Pԙ��}|�^#��Bq!���0
Mngq��������z��мs��a>7�j{�W5�~T�l �F(��M"�ة<��|�6Ԣ�!¸���䍳{�m��}��!q?�N��N0��II��wI�?�ʌc��>��r�!P,��g��}��=�Q�?��Q�Z��WI�����s�����AMU\�_�G0z��nU���-�6�('���gN�1\�p�	�f16���f��p�M��n��j0�0�:���|��1��J�����h���1X��]0$���1�I`dt��=���/m�.�#c:�W>zyH�@Pq8`�0�z�!��N��p"��m�zy��/P)�a���#O�I����e)Z��������!}��>"�����6�ӣ0��䔰��u/JA���aB2Z/b^8��|˕f/5��y=Lf����8Ga�$��%��Sڠ�u�*	�����3��6���8Ԥ2��G:�6�N����I��[^�6�u�	�l���^�9)�Q2���J��� v�t�4��sR��g��H��?�����(7��Q��b�N��8leU��e{��#Ј�� ��ȹ{�$G��p��}�2���2�2��AN��0��C�Uѳ�H����>S�H`4���Ѥù���1T�؁���6T��e�_1��o~�L���=0p� /��2;ɡ@8�9$^�Ln��.3����%��)$���:(J�i�U�k���¶r��Rj���^�/��$���;��ˤ�z�Ⱥ���09=�i(�1�r1��dSc>��i����D���s/�I ����wH9�b�}���)
�N䏅�)���n.����S�h¥&�a�ێ��Ӧ�GA�Y"��3�y�=���LqE�0����)����#�$��r��a�z�;1�]�<���{L
�a
k*W��7���zI_|�Į���f�ƿ�W��e%˻��`�3D����C`�-T�Uk�7(�k �-��/�p���Iz.�>�E��LTu&�J���������H.E�24BB�|z���g�y2ܱӂ�  ,�IDAT-����&J��?+�{�q5)�ڋ���_�5C�Q�3�3��U /-¨��V�� y2��J�`��66OA��ly=%9a�1dk�<C6>x�t<��̺�r�n�>�^��d F��)Dv�����|��nó��+zJI��ؠ��џ1-pT���H& �#�1.Xg�-��C��^�wm�$8bZ`���Rv�E��!�z��q�./���Ck�npJ��6)��;ȳ�7$���$��}hh�c��'���u�S�ݎ�`Rg6�e��N�"��R���,4	
�*L`����1�ɏSS�n�͎9��Ι'!x�#��������@�.��'%�ֿ.��`�H��K0���\��3m>�g���C�It�3u��F��_I.���p�us6�?-��i�2�}��>;�h�k��핲�}Z����Mƈ;����/n��j��KX�pj�"C0V�E��~M� �Ȇ�I���Jz.�\�P�I�y$���[v0�o� [!�)���bT{Q�yk�|��?�{��ѽ��D�^;$�t �U��n��-m��"*j�/��(�3(O���F7�S'��MD�Y�? 9|C��!�Ϛ#!����C�V&�k�YJ�d��P�>��o�D)3m�O�d�S���$�C{�@~��%~�3���گ�aL#���iY�v��L�PoU��Ke���-��]���r��ZY�����4/���?r��2L9& �k[�hjn1l�A����� C����l�hÃ��puL�)��gJT��x��՘�G��%���m���e� �߳�`aw�B�h����e6�n�� ՃR	��8@�����ap���zM]�}�Z�e,��·3�K�t�6�� ��H<^s�� �NN�ޠ�x��@JO��h�j����h��s�$m���0Q��	��)h�C"�[B�h�]�M� �0�L�W-����Kd��޹�yb>� ʗ��7^$=������c�g�ŝ`_Ǵ��/[�[BA1��+�))Qb�4���P�GF�2�����#,�l�d�ABycɻ[�7-��>8��`�N�7���.]b�����zP!�ɺe��`�Ű�q_��5����v�o��h�:S�����=�z!C�)���FkC>G�w�%�{�`�����v5�E̓� ����������D-�� A��:�xT�W>,E gㇼ�$�W�����is��i0F�G�LDL}�KRԸ�������	��sdʿ|J�#�F���|����埒e|���e��c
0�������F�/T�<������^�a
�v��q�5U���P�֣� ���i[B�ɻY��2���Y�x�20m��Hp�2�����J��J8�ً)yy���6?ج�6U�Q�]�X�]A��:����'�����6.Sx���u�0\_H��A����$��AQ� ld�SN3��������}�]o��'��R!ES�	��#���&r�D��F'�jB�}y��o���޷]�M����Ѝ�tͦV��@>��Zf��=/<�s�\%l�?�}�4�	�u\4�
h2�C�`M� ���G�I��H��`(
2���l�L�4CYP(�w
*0�&�0~�}3;�o�j�cIZ��U;ʷ�}��X�v�4C�{Ө��[{0a洒}k�`��B C���<,6�(�p;�Q<W!�!���y��U-������ c �N�Z_�)��" y���cr�;n笴�n��YSެ�Y�L()�s�˄!�>�d|�v�s��/�"7��0�^�6�@>�^R�`�����}��Ш|����[����;�5����Uc5^|FnB�Bt�V�R�N����[�f���WtE���Lx�Lx?�p;��l�A�Ď̩Y�q?s�v;�ݛ9m��6<*Ș�+�2q�������n+]Wh���mZ�x��&��b�8�����0bYz�*���[7}�	�k0֗�?���>R;^yQ�j^�ͭ���-�qU�]�����v q:�a0n��ˣg_,�������V\S{\��َ����2�d��6�Jz���T�%�)��;
$�ik`��E;�vB��iàp]�`��.Rx�t���k�@c�]���P�bk.��//Ș��.�p�����n:�,��q^��(�d�D�1�w�9�Ɓ/���OZ*�O|��0;�Q<��7�C; �׌j�E�j��U�uiy�M�2�j����Լn�l}� �K�y���5k�������ڠ��!��0?�����/z�����m��g��V$��@��B;à��R��QA
�=�P�u�n(k���_3oi2�^�� �y.q^�lk�h^O�����:e�_�͙ҡ;.E�Ԉ�8L�f=������Y�:42��${�Th��<1y����]Q+E��Y���t�G.;'�*�����\��P��,�o������:ᐌ�SJ�.�G�e��V�\�?!%��d�W& pR�/� �e��If}�K&7������/�<�f������sS�h�N<����3�Z�L-�2�p���`��:�H�?����~u��Zm&A׫DzK
;g֥�B��9;�_>y�7s{����"O����yvjj�|���s�`������Sp����Rt�� C.]�X����+�Z�9�Ւ۽-?D�^�_̐$P6�P�3<���?��!	�B���ߏ��(�P�Y��Ji?��) X
�:f�ܗECh�2.�an)�Mnv�W{qTf��A����z:�8ꑼû,g������h�2u���Ρ�`���u{�6!@G��s�F_\8|���m�κ#�@.ٲ���}����4��j����>�߃��^o���˼�;�Rs�a4���82��TuHt�5 �V!�a�r�J��W��~1t���$\����� W�b�'�p���P�!/��?닅Q�ѵOJ��U�r�!3�����uG�f�~-YT �\HBf�Le�_���kn����Z��^������116l�������^�` �m�Զ��MGCL;:�����h��w���ϗ�W}P~��f�°��A�a��~�?��s�^�����%��A���kyNU\�π� ��8��,�0�֦�d>R�_�*�Y3�E5�MNС���c!h"�^& 6��
>����^2��i3,�{܎���T�����%R�qf�3��??��-/{W�������Z�/#n��_#>��9 ovN���r�<�3�!�]��P��C;�{	�Nu�S��]B�O@��#�ذuk��k:���weǯ�4�k˺��j��R0T�Q�@N��������d�SE ���k�0 J��m��a.�]�;��)�0���p����d��A�����1Ўk��/��E���d��S7�LY��e������P1�W�H���O���{	����FE�5.[������l h��O�C��j��1Gb�Q �yT� �IZÿ5}.�DC}.��6tj�6$��ي�z�s�\�������B�!��Y0_ �YȘ&d:+���L�o���?+�n�o���gL+�Hf��ݻ$������P�~CkJ�Lwj��6�42�˄�3kH7G*$��{ehZ��e�`�[
��0 7|e�T6�2�0+{k�D��w���b��+=?��`��F��,[}�q�A�j93�	<
0f��j��y��m޷��`·^����s�1o��f\�ʁ} 7P@�ހ������w���Q��69\{l����3�4ԭZ��8x ��v��'ɾ�
�-T����	�&HM98a��(�0i(�:�(Mӻi�$��)e�A� ��7)�R����C�Iaj����������j06�Хμ��O���l^g�LL_!݈����-0&l�ɹ.�i��@���BP�)h@~� Ç��C{L�{���$)��� P^�!��C/�;��m@� 4c�E�l	�B�=��Z�Z����1�/5C�h0b���"���Y�%6u��SU]���E3��A�ܳS�Z��s��ގO�*S��
�=ۙ��]Ύ� ������2'ϋ�3��lw}����'%�|/}�(e&�pX��B-���Ru����+Ш����6���ؑ��m[��#�"��2�DG���dL �Țd����ܔ#��H��)���q9�m����ީ�%]$�Bls���1�0���v��B;
�M�2MR.uF����y�і�l�:Y�s�Y$?o�u��=���g�+���p9{��Ab�j%g3(`_��S��
A�nr&͒��("?�� ��n�Ig�%�P����S��	��"�5��d�ـ/��\�niݽ�m�L}�Ac���v?�\�Y�j��}d��ء!fP;�<1Ѕ�J� �ʡ�K9YݘO#��
��bd,��W*�-�>�@�t�̙ 0W]+{@F�T
0ZhN5N��a�$Gj����C:���g���v{S��6��HQx�b��;�L)=g��YH��&�r�L��qzKf�D��^%�l��5�0������	�W�u�򚥧#9�x٬�����g�xQ��B	yj�5���"$�2�95i�� ӹ�01�V��O!�zGI)�g�	�{���}��J:Cm�=U$���fT��@�:I�n��������`���Al#�p<U�L���I���U'KWs�d6��2�cD��i��P��c\F,�0g�[%Y�+�uE�M�0�I�R���+������H��o�������-���e��@6��Y�J�X�hmk��7��`�OL �f"⍪s=r�R�ZP�����qͻ�;�J
�"q�4�С��P������}��_(۾^'��#��TG��qZS%�{&=��A:��'�Em�nݕ��X0��˙�m�����ύ����I\�K-�o�ȩ���u�Y���I�C�Ϡ��`��%	�!Ę��)Yh,d맖�O)j;s)6({J@�ɨ]h0�h�h14���o�uO<-A�{t��O��7!�!"�j�Q)��Q�8w)���*08vjEn �#��
B��� �Ƶ��"�N4��6N`]m&�s��+܁��랓������ 1��W��7Ctٟ��'gx��{��-@/�울쟻X��|T���D:2:�J �n6�0N���1�J�VĖ��K�����0���^=&���<�0(��3�m��4�d"����1���5�f�r�Ղ蛤a�q�oy�4�}�[�?`"�M�e���� @�P�"��t麩���w�;�D���U�x��7�����|�C�|S�ޙ��}����z\���)3�E�N��BM�nh�&M�/����d�\��{��Ҳcl��ZgHԈ�Q��t	r���Év�i��{ݳ������>V@H�R���a.^�dH�w���{��R�m����.��+��dW�`.R��d����	C�Y_��T3 ��/#k�G�^'��릖�f A�]�����bPCN���ez)��݅"c�`T8\J�:#	��T`t5��)&�`�,��R{)L-�o.�)hq�����2g�Tb?
#x)�34��KeGH>��`vp��|0{��O?%�g�]���ڞ��`R�r��c4��s3�	���u�e��SzOY*����}�n�!�}�46,ڷ��� jO��<nq_�$�<%{����n�"�_�vf:A��g�^h��V�}"#+#jS&�vh�g�X��`y�Ed2?'U�<.5_@V2�
�тam���I�Ԑ@a<;�li4�6�x�r��Ǩٰ�P����V�h���+z�Ϩ��4Bv�&S[�?���JO�W�a�/X$�λP*�O��cɛa؜� I�4���u9B�Pn����.d���7����0Z��/��6N�f�EM�a�C�N�[��s�\�EuY|���-��# Ck |�*M�c�P�-�%�lz�}c��p�C�`0� c��ND�H���QK�Pca.�kq�������Q�`�La+±v�c>= �(Mr���'L1u��;�ÿ֦&Y��ӆF�eF%��l۰^��I�c� ��x>�&ŀ(4��O��|��O��ƴ��_~C�F'�Z��8�ԏ����%�Pb�C�	;�I
E�"��"[A/�zM�1Ґk�t�
���w�t���hJ;�P��b�`l���s2�Y�Ll�^v�T|ޱ�(�hz ���yH%�/�*�l2�N�Ѫlk6m��2r�(��9IV�cV5�a���r"� ����Ka�0*�!���9��zl�_	�ܴ~�b*	�J����elI+h��2���5u�|+<K.-Na��K:�|ٙ��Uꖡ�ZӊI�%��Y�w���)����=��a.��ْ��X*ވkB�]1�+[`K*���x������"25YdlZ���jos\�5���2�V�ʝ���y��Um�MF#����yh�D@YIQ�1�%W��e���Z��3�C�RQ� `��`H3�p����&DF�qM���p�Vb��Sz㌅��'Mʦi�!�9��2��`]'�a�>�)��wdþ}�t��^�c5�Ѥ,���~����J�uJ"G+{�O�`����>��>�b�w�E��ˣ2ok#�|/�p���Ul�Q�	,�u!�N4	% �����0��K�e? %���>�Q���b�X�<�<HC(�֣
�����dC���5��rdH3H�b8`��fnn��!-�V5�m��Y�����ҋX�Ø�/`���ekYU������,��=wI��_H�_B�n�A�}��yF��[+��:t�ז����]�^hgQF���d���BM������c�5�S�Z�8���\&_p���m3�X{9����%M8dǶi�}��7�I�����e���6�3��s�`$���6�4s�,y�UR�L�@Ħ�T��5��y/}�h���M�����ֹ�/�O�F�-@��]�����o���8 �Pc��
*4�R8$��C@���-�bs眺L��]R��v$Vj��9�X�>�aA���:D1��p�3��+^^���u&�A&������_�'����bYf_v��k�Fp�-��b��`u[X5������n��~h�Ѷ���r��߭P0ÒH�CV1E5�o]V-G��O@���)︙�e�9���3Δ�&�������v�6˰��Y���æj�V�y�	���Db�֛!�N ����x���A��8 _�鯑8m�&O�Rd�Gܺ�z�궵)^�J��m2~��i����S�QF�;�B9��Q���*���X��ՈV��U�C��F%  ���ǧϐ"��L]�P��X�Ah?#3�(��s����p;5��M���)˻v����NR�cC^�Yщ��]����O�5�d�R�̘!�G-	ґ�{a��������_/s�,9�0zRjZ�o�1� P���uk'�cS���ҭQM(u�������1��,p��@<t�t�$���ٌ�9K!�Ph�!5f!��G���ZCw��
�Oב����H���(�� 0S��˼g����a�)�6��Ms�/�tJ��g'^2%����-y��P���_3�Z���%9v ��Û�n��8���T��&N�*Eu�T�ס����p�r�~<N���T{�<�%��ìƗ�� �ρW8��&Ά��C<hX�]s���3�ʍ�]^w(��L����i�1���KN+����_s��;jKs'���M@�J�������}� �҉���K�H����C�p�n�� _!wV�!5!ͨ�,f4��8p����?�)]MCl��wI�U����H�]��Np�� C��x�d4	��1�Pk�����[$=����F�/�����7J���K�����YΪ��7=�h��Sh�t�BS�g��ed0�&1�L� ^�����6 ͩx�<)�P�3���sD��ۻ*����7��!�}�/���5-��hb[���U@����,r�L��>v3���s����� �m�1�|爐\Ѳ�b߲��w��w$�z=��W��m���@���D�ܡ#��1d��كx��I�6T$3L˩߰^��E�B�OL|�Ϯ���*-�^��k�k0���&��yw�Ĉb�π�����C���-M~�2-�|��a5�X��m@1#�R���?�@F�q�n^{��{����S&�I�έi��)S�5�8`��Hb��\x������W��Ӹs�w���1%QW�k�&邫;��Y���D�x�M]`�,�aQ4m� C�_�2� �ZdL����|S���drn��2
�"0��ۻ���s�g0-��qtfj1vg��"1����F\!�w���(�Ps�z�L�4.J���:�0}���� J�0}!�)���okENW�D@���o���Pe�탌i*��̡��sL%P�6�
 �8JhB#�q�+�@�>'��A��`�!�MOP-�C5���N5�w5M������m��s�Nz)�x�.s�˹9T���i��J���sٞ-��d��dQC��&�W> ���������8�����ɼ��il:�׺��>:��Slt�*�p9���?Q���D�JJ!-F�XtM��G���-���ϙ�$�|8���%ky`J��Em&.МԍN�	�%�����~8�gWI��?I�m�����o >d��>�1T���bk����u�Ll;�n00����{`����c��7��i̵
]w���P&�?�KWIT���%3�w�dQD�ƪ���x��5),.F�uI� ���a�_�ɧ��>6�o�~���[��'Gpy�������j��>�6��K���)�-p���(4�R�ل�U�7iXU;��ˌ��� ��{&N��	��s� �p_�2��K���,1���3��GmF�1�bT����~Q�h1��ܯ��J���4���U���K���)E�6J-�(����j�!�&:��~؈�6��� 8�K�A�=������J�iV�Q`�)O�RI���0c=��>=��p-�x�&7���2�klF;����:&��Ki%4���� /;��5g���͗��qE�y���0C<�v5�d�1;z��o�"����}mL޴���O���TЁ.E%��>���6��zKۻ����/D#w5=@=[t�k��7�5�H��{zJ�X�	5Ho���	��L0�X�r�[���E�r�N���޿rl��'b�K�R`�����*{�;©�K���'��ȁMpTp�V�F�zNI`N��[S	̲u��9n�)y�`h@�U5�[z�������y$����PA�>j	w6�A��3�J�a8���	bse�w�!Mϭ6�cu�� 3��n{��`)q��dHu��8����׹x��1��ݑ-���'`\�7\�'y�[��Ꭴ��領x�S���/]��o�1ۀo����	D
JF݅z�x\u�)f��
J:θ�N�L0��5�I�6[G��_it����͡%�	�����#�	����I��P;�o�)KO���/��EZA>�P{Q1����:W1q?*��-�9����d�5nu�q�NQ���J#�zfun鎃�Nf���/`F�:��(�P���uNA���Aw����DRNA��,g��m�a���*�p�eҰ���i^��_����o�N�!���X�Q<D�\���I����!�5Z6� 3Z��1z��4���b�+b5I��	2m�hHd@�l�`� 2�I���C��u���]#��yR��}V���E�8|-�E�R���ͭZL
�!�2	04;$F���r=��d���p�������7�j-fT�ܡ�ٟ�-��6�c̋2�՞�T.��� ȧ�
 ���d~?�SM�����;%��&�7��d%��0Ɛ'搀�P��5��8��C��+�x�4c~�|���Sb���sbp`���--���̡G��;A[���Z��t���a+�+/�Z��)aD�Y�q�Jf���G��L�$U�����u����S7�jD�
@�'P����P_C���BI�\��1q:i�G�l�*}Ⱥ<�iJ=���O�J��7�?ӗ���N��X��'�=�9}��UWK��gIKwg?M�}��j̧����D�̼[É�IͲ6�ht;�̾�^��4�������8�n�������[g��fD�y;�\� �P�������-�Nh(i��Ρ��V���XM�Ϫ�&C���(���(q?�����i��li����Q��V���M~�-ЀhZuIjq�������I��gR�4Mf4<�����Pp1�s������������'[�[�H�;����x����V\��>�`y~T{у��p�lk�䏾#{n�'4��V����� �Wc\
C�o��O�غ`rn&R=K~\J<0i(I�#��fTn+"n{+�$y�妎6K��C�v���l(��.�v�~5���*���M���)���aT/�r��z��Tk@�����zY���Q�/G͍��-f̷��es�
�6�B �IV��U.ۃ%��4Yf�s��-������X%QV��@�W�.+���Rڇ�
��$�]������zI�՝�[Z����]�zTEe�Rƽ\�Q��1!2TQ)�IS���ֽ�Q���_���9*n����o����cM�-J�2�4���b�ڡ�(mC_u��VVHx�L�4e���5��Tف�� ��S ����@�n�uu�Q�=����+̫��<)3�M��,yAE˦��QQ������ό� �0���,��t`�� �f���)JA�P[0Q�:�R�r�rPp��&��Y�-��m����}�3�h|��?�˨n�����jѹ��Lmf��1,
*���xi���6��u.�p�����2)Ѕ�_B�Uߋ�ڗQ��l�<��$F�xSt�P�BNj��-��
J�`*CrG�|�C:�$@+�b^Ow�0��V���Y'���٭���-0�Z@+#h���%���}1�
�o��Ј{*��ɬ�yT��2�IN�`(K��^w�����LL�A�� r�������3�5'�����`����}�J��p�����aR�ᑶ��I���	 ɑoۺ��۞E�s�7�9���u����B_���?v[�q�n�B� n�>
*\Vͅ�$�p皦љ�����}�~[�{���m�[\Υu(t�
F֥�bp��n�j(��~�-ව�~�-ව�~�-ව�~�-ව�~�-ව�~�-ව�~�-ව�~�-ව�~�-ව�~�����'Q�    IEND�B`�
```

### `src/flows/fno/assets/us-glow-2.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="216" height="133.222" viewBox="0 0 216 133.222" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="glow" filter="url(#filter0_f_0_59)">
<ellipse cx="108" cy="66.6111" rx="60" ry="18.6111" fill="#256FEF" style="fill:#256FEF;fill:color(display-p3 0.1451 0.4353 0.9373);fill-opacity:1;"/>
</g>
<defs>
<filter id="filter0_f_0_59" x="0" y="0" width="216" height="133.222" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
<feFlood flood-opacity="0" result="BackgroundImageFix"/>
<feBlend mode="normal" in="SourceGraphic" in2="BackgroundImageFix" result="shape"/>
<feGaussianBlur stdDeviation="24" result="effect1_foregroundBlur_0_59"/>
</filter>
</defs>
</svg>
```

### `src/flows/fno/assets/us-glow.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="216" height="216" viewBox="0 0 216 216" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="glow" filter="url(#filter0_f_0_105)">
<circle cx="108" cy="108" r="60" fill="#256FEF" style="fill:#256FEF;fill:color(display-p3 0.1451 0.4353 0.9373);fill-opacity:1;"/>
</g>
<defs>
<filter id="filter0_f_0_105" x="0" y="0" width="216" height="216" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
<feFlood flood-opacity="0" result="BackgroundImageFix"/>
<feBlend mode="normal" in="SourceGraphic" in2="BackgroundImageFix" result="shape"/>
<feGaussianBlur stdDeviation="24" result="effect1_foregroundBlur_0_105"/>
</filter>
</defs>
</svg>
```

### `src/flows/fno/assets/watchlist.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="19.8223" height="19.8213" viewBox="0 0 19.8223 19.8213" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="task-list-edit--task-list-edit-work">
<path id="Subtract" d="M16.3392 6.93546C15.7591 6.98869 15.213 7.24336 14.7981 7.65912L8.08379 14.3877C7.70114 14.7711 7.45342 15.2685 7.37786 15.805L6.94929 18.8478C6.9329 18.9641 6.92485 19.0805 6.92483 19.1964H2.05353C1.67465 19.1964 1.31129 19.0458 1.04338 18.778C0.775469 18.5101 0.624959 18.1467 0.624959 17.7678V2.05353C0.624959 1.67465 0.775469 1.31129 1.04338 1.04338C1.31129 0.775469 1.67465 0.624959 2.05353 0.624959H11.3392L16.3392 5.62496V6.93546Z" fill-rule="evenodd" clip-rule="evenodd" fill="#E8E8E8" style="fill:#E8E8E8;fill:color(display-p3 0.9098 0.9098 0.9098);fill-opacity:1;"/>
<path id="Vector" d="M19.1972 12.0534L12.4686 18.7819L9.42578 19.1962L9.85435 16.1534L16.5686 9.4248L19.1972 12.0534Z" fill="#161616" style="fill:#161616;fill:color(display-p3 0.0863 0.0863 0.0863);fill-opacity:1;"/>
<g id="Union">
<path d="M11.3389 0C11.5045 1.07367e-05 11.6641 0.0655475 11.7812 0.182617L16.7812 5.18262C16.8984 5.29982 16.9639 5.45926 16.9639 5.625V6.33887C16.9638 6.68401 16.684 6.96385 16.3389 6.96387C15.9939 6.96364 15.7139 6.68389 15.7139 6.33887V5.88379L11.0801 1.25H2.05371C1.84059 1.25 1.63605 1.33465 1.48535 1.48535C1.33465 1.63605 1.25 1.84059 1.25 2.05371V17.7676C1.25001 17.9807 1.33474 18.1853 1.48535 18.3359C1.63611 18.4866 1.84067 18.5713 2.05371 18.5713H6.33887C6.68398 18.5713 6.96379 18.8512 6.96387 19.1963C6.96385 19.5414 6.68401 19.8213 6.33887 19.8213H2.05371C1.50902 19.8213 0.986615 19.6047 0.601562 19.2197C0.216455 18.8346 1.07878e-05 18.3121 0 17.7676V2.05371C0 1.50906 0.216446 0.986681 0.601562 0.601562C0.986681 0.216446 1.50906 0 2.05371 0H11.3389Z" fill="#161616" style="fill:#161616;fill:color(display-p3 0.0863 0.0863 0.0863);fill-opacity:1;"/>
<path d="M16.5684 8.7998C16.7341 8.79973 16.8935 8.86523 17.0107 8.98242L19.6387 11.6113C19.7559 11.7285 19.8223 11.888 19.8223 12.0537C19.8222 12.2194 19.7558 12.378 19.6387 12.4951L12.9102 19.2236C12.8135 19.3202 12.6881 19.3829 12.5527 19.4014L9.50977 19.8154C9.31588 19.8417 9.12047 19.7754 8.98242 19.6367C8.84467 19.4981 8.77949 19.3029 8.80664 19.1094L9.23535 16.0664L9.25781 15.9678C9.28769 15.8718 9.34038 15.7838 9.41211 15.7119L16.126 8.9834C16.2431 8.86598 16.4025 8.79989 16.5684 8.7998Z" fill-rule="evenodd" clip-rule="evenodd" fill="#161616" style="fill:#161616;fill:color(display-p3 0.0863 0.0863 0.0863);fill-opacity:1;"/>
<path d="M6.90234 9.38965C7.10293 9.10883 7.49355 9.04367 7.77441 9.24414C8.05529 9.44477 8.12053 9.83533 7.91992 10.1162L5.58984 13.3779C5.48306 13.5274 5.31586 13.6225 5.13281 13.6377C4.94993 13.6528 4.76948 13.5867 4.63965 13.457L3.24121 12.0586C2.99748 11.8146 2.99743 11.4188 3.24121 11.1748C3.48529 10.9307 3.8819 10.9307 4.12598 11.1748L5.00195 12.0508L6.90234 9.38965Z" fill="#161616" style="fill:#161616;fill:color(display-p3 0.0863 0.0863 0.0863);fill-opacity:1;"/>
<path d="M6.90234 3.58594C7.10294 3.30529 7.49361 3.2401 7.77441 3.44043C8.05523 3.64102 8.12039 4.03163 7.91992 4.3125L5.58984 7.57422C5.48306 7.72365 5.31585 7.81883 5.13281 7.83398C4.94993 7.84905 4.76948 7.78299 4.63965 7.65332L3.24121 6.25488C2.99761 6.01084 2.99747 5.61505 3.24121 5.37109C3.48526 5.12718 3.88193 5.12718 4.12598 5.37109L5.00195 6.24707L6.90234 3.58594Z" fill="#161616" style="fill:#161616;fill:color(display-p3 0.0863 0.0863 0.0863);fill-opacity:1;"/>
</g>
</g>
</svg>
```

### `src/flows/fno/assets/zing.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="36.6667" height="20" viewBox="0 0 36.6667 20" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="D2 &#226;&#134;&#146; Zing logo">
<g id="Vector">
<path d="M4.89843 7.79386L6.65944 9.55487L10.8824 5.33407L6.65944 1.11111L4.89843 2.87212L6.11427 4.08795H0.677636V6.57803H6.11427L4.89843 7.79386Z" fill="url(#paint0_linear_0_304)"/>
<path d="M30.3744 5.56579C31.5771 5.56579 32.473 6.02232 33.0333 6.76859H33.068V5.73669H35.5556V14.4379C35.5556 17.0794 33.6756 18.7217 30.8654 18.7217C28.2932 18.7217 26.6514 17.2826 26.448 15.2685V15.2663H29.0891C29.2254 16.1641 29.8509 16.7572 30.9348 16.7572C32.17 16.7572 33.068 15.961 33.068 14.5225V13.1678H33.0333C32.3908 13.8947 31.3739 14.2002 30.2404 14.2002C27.7525 14.2002 26.2446 12.439 26.2446 9.9511C26.2447 7.46332 27.9709 5.56582 30.3744 5.56579ZM31.0021 7.69904C29.7171 7.69904 28.7843 8.62948 28.7842 9.98365C28.7843 11.3379 29.6303 12.2856 30.9348 12.2856C32.2393 12.2856 33.2042 11.3205 33.2042 9.94893L33.2021 9.9511C33.202 8.63164 32.2869 7.69917 31.0021 7.69904Z" fill-rule="evenodd" clip-rule="evenodd" fill="url(#paint1_linear_0_304)"/>
<path d="M23.9442 15.5647C24.5757 15.5648 24.9955 16.0084 24.987 16.7588H23.4722C23.5177 17.053 23.6929 17.215 23.9654 17.2151C24.1644 17.2151 24.3163 17.1223 24.4374 16.9297L24.885 17.207C24.6925 17.4924 24.4134 17.6719 23.9399 17.6719V17.6697C23.2844 17.6697 22.8733 17.2695 22.8733 16.6313C22.8734 15.9933 23.3126 15.5647 23.9442 15.5647ZM23.9507 15.9846C23.7064 15.9846 23.5481 16.1099 23.4853 16.3541H24.3745C24.3462 16.123 24.1755 15.9847 23.9507 15.9846Z" fill-rule="evenodd" clip-rule="evenodd" fill="url(#paint2_linear_0_304)"/>
<path d="M21.8631 17.6269H21.2636V17.3914H21.2549C21.097 17.5752 20.8568 17.6681 20.5952 17.6681C19.9916 17.6681 19.6088 17.2484 19.6088 16.6123L19.611 16.6145C19.6111 16.0154 20.0306 15.5631 20.5756 15.5631C20.8567 15.5631 21.097 15.6691 21.2549 15.8593H21.2636V14.2458H21.8631V17.6269ZM20.753 16.0649C20.4395 16.065 20.2188 16.3053 20.2187 16.6145C20.2187 16.9455 20.4264 17.1684 20.7444 17.1684C21.0775 17.1684 21.2896 16.952 21.2896 16.6102H21.2918C21.2917 16.2923 21.0667 16.0649 20.753 16.0649Z" fill-rule="evenodd" clip-rule="evenodd" fill="url(#paint3_linear_0_304)"/>
<path d="M17.3465 15.5625C17.619 15.5626 17.8807 15.6771 18.0149 15.8588H18.0192V15.6011H18.6231V17.6263H18.0192V17.3903H18.0149C17.8634 17.5699 17.619 17.667 17.3421 17.667C16.8006 17.667 16.4227 17.2946 16.3775 16.7312L16.3726 16.6178C16.3729 16.0144 16.7928 15.5625 17.3465 15.5625ZM17.5174 16.0644C17.2059 16.0644 16.9831 16.2896 16.983 16.614C16.9831 16.9383 17.1907 17.1674 17.5 17.1674C17.8331 17.1674 18.0538 16.9362 18.0539 16.6053H18.0561C18.056 16.2744 17.8288 16.0644 17.5174 16.0644Z" fill-rule="evenodd" clip-rule="evenodd" fill="url(#paint4_linear_0_304)"/>
<path d="M15.4921 15.5647C15.5461 15.5647 15.5812 15.5691 15.6136 15.5777V16.2049L15.6006 16.2092C15.5271 16.1595 15.4489 16.136 15.3603 16.136C15.1116 16.1361 14.9128 16.3112 14.9127 16.5597V17.6307H14.3132V15.6059L14.3153 15.6038H14.9018V15.9304H14.9148C15.0489 15.7142 15.3104 15.5649 15.4921 15.5647Z" fill="url(#paint5_linear_0_304)"/>
<path d="M12.9915 15.6054H13.3919V16.0986H12.9915V17.6301H12.3926V16.0986H12.1392V15.6054H12.3926V15.0146H12.9915V15.6054Z" fill="url(#paint6_linear_0_304)"/>
<path d="M5.75522 10.4616L4.5394 11.6774H10.7568V14.1699H0.677636V12.0171L3.99415 8.7011L5.75522 10.4616Z" fill="url(#paint7_linear_0_304)"/>
<path d="M14.6468 14.1682H12.1588V5.73724H14.6468V14.1682Z" fill="url(#paint8_linear_0_304)"/>
<path d="M21.8425 5.56796C23.7223 5.56801 24.9229 6.70225 24.923 8.51501V14.1525H22.4349V9.27619C22.4348 8.17523 21.8594 7.59976 20.8773 7.59976C19.8953 7.59984 19.201 8.29451 19.2009 9.37819V14.1525H16.7128V5.73724H19.2009V6.78595H19.2356C19.8781 5.99005 20.7934 5.56796 21.8425 5.56796Z" fill="url(#paint9_linear_0_304)"/>
<path d="M13.4033 1.3503C14.1953 1.35042 14.8372 1.99221 14.8373 2.78422C14.8373 3.57631 14.1954 4.21856 13.4033 4.21868C12.6112 4.21868 11.9689 3.57638 11.9689 2.78422C11.969 1.99214 12.6112 1.3503 13.4033 1.3503Z" fill="url(#paint10_linear_0_304)"/>
</g>
</g>
<defs>
<linearGradient id="paint0_linear_0_304" x1="5.9078" y1="6.2375" x2="6.73041" y2="11.9135" gradientUnits="userSpaceOnUse">
<stop stop-color="#F6BC2F" style="stop-color:#F6BC2F;stop-color:color(display-p3 0.9647 0.7373 0.1843);stop-opacity:1;"/>
<stop offset="1" stop-color="#D79900" style="stop-color:#D79900;stop-color:color(display-p3 0.8431 0.6000 0.0000);stop-opacity:1;"/>
</linearGradient>
<linearGradient id="paint1_linear_0_304" x1="5.9078" y1="6.2375" x2="6.73041" y2="11.9135" gradientUnits="userSpaceOnUse">
<stop stop-color="#F6BC2F" style="stop-color:#F6BC2F;stop-color:color(display-p3 0.9647 0.7373 0.1843);stop-opacity:1;"/>
<stop offset="1" stop-color="#D79900" style="stop-color:#D79900;stop-color:color(display-p3 0.8431 0.6000 0.0000);stop-opacity:1;"/>
</linearGradient>
<linearGradient id="paint2_linear_0_304" x1="5.9078" y1="6.2375" x2="6.73041" y2="11.9135" gradientUnits="userSpaceOnUse">
<stop stop-color="#F6BC2F" style="stop-color:#F6BC2F;stop-color:color(display-p3 0.9647 0.7373 0.1843);stop-opacity:1;"/>
<stop offset="1" stop-color="#D79900" style="stop-color:#D79900;stop-color:color(display-p3 0.8431 0.6000 0.0000);stop-opacity:1;"/>
</linearGradient>
<linearGradient id="paint3_linear_0_304" x1="5.9078" y1="6.2375" x2="6.73041" y2="11.9135" gradientUnits="userSpaceOnUse">
<stop stop-color="#F6BC2F" style="stop-color:#F6BC2F;stop-color:color(display-p3 0.9647 0.7373 0.1843);stop-opacity:1;"/>
<stop offset="1" stop-color="#D79900" style="stop-color:#D79900;stop-color:color(display-p3 0.8431 0.6000 0.0000);stop-opacity:1;"/>
</linearGradient>
<linearGradient id="paint4_linear_0_304" x1="5.9078" y1="6.2375" x2="6.73041" y2="11.9135" gradientUnits="userSpaceOnUse">
<stop stop-color="#F6BC2F" style="stop-color:#F6BC2F;stop-color:color(display-p3 0.9647 0.7373 0.1843);stop-opacity:1;"/>
<stop offset="1" stop-color="#D79900" style="stop-color:#D79900;stop-color:color(display-p3 0.8431 0.6000 0.0000);stop-opacity:1;"/>
</linearGradient>
<linearGradient id="paint5_linear_0_304" x1="5.9078" y1="6.2375" x2="6.73041" y2="11.9135" gradientUnits="userSpaceOnUse">
<stop stop-color="#F6BC2F" style="stop-color:#F6BC2F;stop-color:color(display-p3 0.9647 0.7373 0.1843);stop-opacity:1;"/>
<stop offset="1" stop-color="#D79900" style="stop-color:#D79900;stop-color:color(display-p3 0.8431 0.6000 0.0000);stop-opacity:1;"/>
</linearGradient>
<linearGradient id="paint6_linear_0_304" x1="5.9078" y1="6.2375" x2="6.73041" y2="11.9135" gradientUnits="userSpaceOnUse">
<stop stop-color="#F6BC2F" style="stop-color:#F6BC2F;stop-color:color(display-p3 0.9647 0.7373 0.1843);stop-opacity:1;"/>
<stop offset="1" stop-color="#D79900" style="stop-color:#D79900;stop-color:color(display-p3 0.8431 0.6000 0.0000);stop-opacity:1;"/>
</linearGradient>
<linearGradient id="paint7_linear_0_304" x1="5.9078" y1="6.2375" x2="6.73041" y2="11.9135" gradientUnits="userSpaceOnUse">
<stop stop-color="#F6BC2F" style="stop-color:#F6BC2F;stop-color:color(display-p3 0.9647 0.7373 0.1843);stop-opacity:1;"/>
<stop offset="1" stop-color="#D79900" style="stop-color:#D79900;stop-color:color(display-p3 0.8431 0.6000 0.0000);stop-opacity:1;"/>
</linearGradient>
<linearGradient id="paint8_linear_0_304" x1="5.9078" y1="6.2375" x2="6.73041" y2="11.9135" gradientUnits="userSpaceOnUse">
<stop stop-color="#F6BC2F" style="stop-color:#F6BC2F;stop-color:color(display-p3 0.9647 0.7373 0.1843);stop-opacity:1;"/>
<stop offset="1" stop-color="#D79900" style="stop-color:#D79900;stop-color:color(display-p3 0.8431 0.6000 0.0000);stop-opacity:1;"/>
</linearGradient>
<linearGradient id="paint9_linear_0_304" x1="5.9078" y1="6.2375" x2="6.73041" y2="11.9135" gradientUnits="userSpaceOnUse">
<stop stop-color="#F6BC2F" style="stop-color:#F6BC2F;stop-color:color(display-p3 0.9647 0.7373 0.1843);stop-opacity:1;"/>
<stop offset="1" stop-color="#D79900" style="stop-color:#D79900;stop-color:color(display-p3 0.8431 0.6000 0.0000);stop-opacity:1;"/>
</linearGradient>
<linearGradient id="paint10_linear_0_304" x1="5.9078" y1="6.2375" x2="6.73041" y2="11.9135" gradientUnits="userSpaceOnUse">
<stop stop-color="#F6BC2F" style="stop-color:#F6BC2F;stop-color:color(display-p3 0.9647 0.7373 0.1843);stop-opacity:1;"/>
<stop offset="1" stop-color="#D79900" style="stop-color:#D79900;stop-color:color(display-p3 0.8431 0.6000 0.0000);stop-opacity:1;"/>
</linearGradient>
</defs>
</svg>
```

### `src/flows/fno/commodities/archive/DayPickerByWeek.tsx`

```tsx
/**
 * ARCHIVED 2026-11-24 — not in the app. The Commodity calendar page (fno-38) in Expiring This Week version 4: the days
 * as week sections (Monday to Sunday), each titled with its range ("November 23 – 29"), with that week's day picker
 * (no week pills) and the selected day's cards; a 2 line edge to edge between weeks (`.weekSection`,
 * `--app-week-divider`). The page went back to the day list (dates on the left, one card per contract or event).
 * To bring it back: in ExpiryTimeline's CalendarBody, when `useFlowOption('fno', 'expiringVersion', 'v4') === 'v4'`,
 * return `<div className={styles.calendar}><DayPickerByWeek days={days} showKind={tab === 'all'} eventDetails … /></div>`,
 * and add 'fno-38' back to the option's floatOn (fno/index.tsx).
 */
import { SectionHeader } from '@l3/components/SectionHeader'
import { Stack } from '@l3/components/Stack'
import { t } from '../../copy'
import { dayFrom } from '../components/CalendarDay'
import { DayPicker, byWeek, todayInWeek } from '../components/ExpiringDayPicker'
import styles from '../components/Commodities.module.css'

/** A week's title: its Monday to Sunday, month spelled out — "November 23 – 29", "November 30 – December 6". */
function weekTitle(week: number) {
  const monday = dayFrom(week * 7 - todayInWeek())
  const sunday = dayFrom(week * 7 - todayInWeek() + 6)
  const month = (date: Date) => date.toLocaleDateString('en-IN', { month: 'long' })
  const to = month(sunday) === month(monday) ? `${sunday.getDate()}` : `${month(sunday)} ${sunday.getDate()}`
  return t('expiring.weekRange', { from: `${month(monday)} ${monday.getDate()}`, to })
}

/**
 * The calendar page in version 4 (fno-38): the days split into week sections (Monday to Sunday). Each section has the
 * week as its title ("November 23 – 29"), that week's days as a row of date cards (no week pills — the title says which
 * week), and the card for the selected day under it; each week picks its own day (its first, to start). A 2 line runs
 * edge to edge between two weeks, 24 above and below it.
 */
export function DayPickerByWeek({ days, ...rest }: Omit<Parameters<typeof DayPicker>[0], 'weekPills'>) {
  return <Stack gap="24">
    {byWeek(days).map((w) => <section key={w.week} className={styles.weekSection} aria-label={weekTitle(w.week)}>
      <Stack gap="12">
        <SectionHeader title={weekTitle(w.week)} />
        <DayPicker days={w.days} weekPills={false} {...rest} />
      </Stack>
    </section>)}
  </Stack>
}
```

### `src/flows/fno/commodities/archive/expiryPreviewSamples.ts`

```ts
/**
 * ARCHIVED 2026-11-24 — not in the app. The prototype setting "Calendar days" (F&O, Commodities) let the home's
 * Expiring This Week show sample weeks instead of the real MCX calendar: 3 today, 2 today · 1 tomorrow, 1 a day. Only
 * the real data is shown now. Nothing imports this file.
 * To bring it back: import `expiryPreviewSamples` in ExpiringCalendar / ExpiringCalendarCard, read
 * `useFlowOption('fno', 'expiringDays', 'real')` and pass `expiryPreviewSamples[sample]` to `expiryPreview(3, …)`, and
 * add the option to fno/index.tsx: { id: 'expiringDays', group: 'Commodities', label: 'Calendar days', values: [real
 * "Real week", calendar "3 today", split "2 today · 1 tomorrow", spread "1 a day"], default: 'real', floatOn:
 * ['fno-08', 'fno-09', 'fno-10', 'fno-38'] }.
 */
import { contracts, expiryCalendar, expiryCalendarAll, type ExpiryDay } from '../data'

/**
 * Prototype: how the home's short calendar (Expiring This Week v2 / v3) looks when the week splits differently — the
 * setting “Calendar days”. Sample weeks: the first two days hold only option / future contracts, an event comes on the
 * third day only. `calendar` = 3 today (all contracts); `split` = 2 today + 1 tomorrow; `spread` = 1 a day, so the
 * third row is the event. The calendar page (fno-38) keeps the real calendar.
 */
export type ExpiryPreviewSample = 'real' | 'calendar' | 'split' | 'spread'
const crudeStock = expiryCalendar.event.flatMap((d) => d.entries).find((e) => e.name === 'EIA crude oil inventories')!
export const expiryPreviewSamples: Record<ExpiryPreviewSample, ExpiryDay[]> = {
  real: expiryCalendarAll, // the real MCX calendar (default)
  calendar: [
    { inDays: 0, entries: [...contracts('option', ['Gold Mini', 'Crude Oil Mini']), ...contracts('future', ['Natural Gas'])] },
    { inDays: 1, entries: contracts('option', ['Natural Gas']) },
    { inDays: 2, entries: [crudeStock] },
  ],
  split: [
    { inDays: 0, entries: [...contracts('option', ['Gold Mini']), ...contracts('future', ['Crude Oil Mini'])] },
    { inDays: 1, entries: [...contracts('option', ['Natural Gas']), ...contracts('future', ['Natural Gas Mini'])] },
    { inDays: 2, entries: [crudeStock] },
  ],
  spread: [
    { inDays: 0, entries: contracts('option', ['Gold Mini']) },
    { inDays: 1, entries: contracts('future', ['Natural Gas Mini']) },
    { inDays: 2, entries: [crudeStock] },
  ],
}
```

### `src/flows/fno/commodities/assets/crude-oil.png`

```tsx
�PNG

   IHDR   �   �   �>a�  ciCCPkCGColorSpaceDisplayP3  (�}��K�PƿV��u2�C��
�8�DqU�ꔾ����G�"7�����
�n�::8�������y/��"z��~|��8 9npn��;�[\�+��-%��� �񜮯J��?��>��N�Y�������1����]H�����%����qK���r��g�X �&VXͨ�������`�r���l��9�X�<p�0Є�?�����]r7�R��|�ɑ"'���p�0�XC�R�w��w�O���'`�#�����p6G'k���<02\�����G��V��S`���P϶W�j���<0�(��$�:�-!>���S�p�|�b��[   cICP n��   8eXIfMM *    �i            �       ��       �    kF&M  YiTXtXML:com.adobe.xmp     <x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="XMP Core 6.0.0">
   <rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
      <rdf:Description rdf:about=""
            xmlns:xmp="http://ns.adobe.com/xap/1.0/">
         <xmp:CreatorTool>Figma</xmp:CreatorTool>
      </rdf:Description>
   </rdf:RDF>
</x:xmpmeta>
�\�  #IDATx�{�U�y����)7E>����Ԃ�btƙ�j�N�δ��?�d2�m��M�h����N�2�v��mJ��6MM���V��zC��E.��o�����9|h�9�нf���˻�^�}�����^�|YV���*T�,PY��@e���*T�,PY��@e���*T�,PY��@e���*T�,PY�l�@�,�@��Y�*P�;`���C��W�x@�
t:�2�����o�~�&*S�����G!�۷�1�~��Nb���z������9rd�u��V��[rt,n���sw���w{��������G�f8��9眓�)D�T�$�(�="�V�a�گ>|��={��ܸq�f�b��Y:� <��M[�n}�����b6z���������7r�D!FB�FWD8�e�M� b=#B�h���k���b?gC�c	p�=�\y饗.]�l�P������ٱc�z"y�uD��'��	�J� ��"�~�UX�{�lق�x7)�:� �}�;��'7�x�Z�m۶%`-���FRDO���2P��A�������� ���{�}����Z�����<�X�z��ǎ����ۇ_y���kvfr�	�f$�; <�QR��L{	��	x�D� ������;v�ӫ����Tv'��ӧ��z�P'M����.��W����l���fb6y����u���g�)yʊ����ߟ�{���x�L���y�l߾}	|�Z�1@-��C�5j��#G~Nd��y�7Fu���;��ę�%��iӾt�%�L>|xv�Wd�#Ȗ,Y�]xᅙ�� �n�> t3B�	.����k��D�L3;��O3@$�!�3$�	�%�ڃ\�=ɬ�.��7F�1U�m��x��ا�u$fΜ9\;�Gƌsk����^x!{��׳�'f��iV�7v��&�/����A�]��ӧg�ND�H<D� �q]�6�\C�G}ذaƏ?U��uy��u�;w����Mv$�/˸���2#k<   �0aB�<��3�"@<�E�IC$A��a����MX���ͩ?�9PO�O�!���@��2����L���5�i�~���V�P��t$��ꪇ4ۧk�՘���Ǖ�,l޼9-���ݝ@c��F�D0	 Ǹq�2+��x@�;O�� 0��y�@ �@�1�45�UVW]"�U��5拴���]O&K:� S�N.���f�0fl��X 	�z�x@�z����_NB�9c3g�LH³����+�d+W��6lؐ��T��Z��˵�+�O<�<��|]��kߨ�+"�.���J�G ��g�l0<���C �kg�� o� 厁vx@Tf.��x\=�:��|��7S9@(�Х���|	��
y]�6�D�4�&��7�p�d���5kִ��R�@���d�뙭�-lmxV{f�,x{�q��yڰ�8�;�|��3���3�O�1L:���cy�4,*���di�x&k�x�dm�~e���j�Q�Z:D��Q���X �؄|�% I�Pt �%��>Fܻ%'����]����� )�k@�?�a`�b�G4�;�D�a� h|���3g��[n�e�E�Z�����7��f͚5[ �P��]  ����	l|�H�᪙���e��pʔ)iɬծ=���ˌPH�k�e�1�I<�D�H�A�A��%I�ܲ~O���������( ࿠s�3#��v�2������cF3�!d`�� !��� �@D���e���������6���;��?�|�I��$t��rۏj��d�����" ��� ��<i"`p���C,�  �EO���d��|O}F���׍cq9��]u=}�G�����eGC�_�8A��_�`�1����[���*?��e�)�
��&�@9�GЩ��� �&$�XH�2�Q/{2��uq�x�|tc����k"���s}�fR���7p�p��u���L��!��?'�����I��I|�cG��rID��`C^4�~�[:� �e��hQ!�u�1h�@�I����Y�D���Ҳ�C��c�}QF��n��2X��y�� �B�K��LN�هD�9ܲ����~�;�	�;@��=z&yB�_��l�q9�#ݺ�W�-��C�ZJO�Gy�Þ�:]<���΁4�FL��� @6Дx�#��G� �!��h G���7!���c1�J��L�&���������f����Ó�?�LX$�'�w��ɣ�<��G4Ȕɻ�io�L���� ��9�i)�.��آt�6�
�c����e�ie8u����gx-m��b �X\1`:D`�\��r�3���H @7��51У/���HB�����i�5�j�/u�Vɓ�l�?�utO�����>�Y��~i�2(ր $� ���M$e.70�:��[����<"���͛���'�� ��|饗��z�@V� b���t#�݇	ἥ�D�4:˙�:06��}�y���Z)KO ��M�>`�N��q�~*���v����6(�ˑ>HG�]giP��4���c���tԉit����3/��V�KO ��ۺ��yyR{����n�MD x	P��.� ����}E���q�F$h~,W�:^M������A�-�Sj��o?������5�!/^�8݋C {o�|ۅ� ����I��@�s�e3�O�[|Tk"�>=_x�t�>κR@��2�U ��}0�p��tt�ð��H�r��c������y�[�z_�t 1��u)���U�V��V�R@�q��@Iv����BHz]���{.���0�D )�-�lH`"AE���M1M��B#��6�<��o)�{G�]�#֗� ��s�j��S4�P��4O?�t�bŊ�Tc����s�K���'�F�	�;]��͛�1��$	����GE�V�K�:xƌ���z
80�q����|��p��ܞ�x��c��L�$�|ˢ�&�<��i�^F���|ڃ]L��e��s(�ո�z8�����5{Gg�j�d�]3� �!��9�����s��!ҁ�����# D ��7薀�(�o�����k����iC�>��ۗD��Q����i��{�����f�f-@�6	0(��] �x[ǻ{�@���@��$�L!KHC ��7!m�-M����f��u=c��
�p�]�.YJtww���}=��:��� �hcy�1�P}BY@�uxy0��4ހ��@*H�%"�>d�\����������\_�ky��������)�)����$G� �� �i\��÷}9��R�.z�K@�Y���7`C{{�S�����e�9��+Yۨcf_Q�a��.YJh��M�)� \&�|f*�  Lt��=�M@dI�@��^{-��v\�)XNh�g�;�G�`��|m��eH�#�q),�x�hw(#���M��Y
���-==S�3� ��L�9���1۬#XD�����k <d�- � ������]��5�����Ĵ����Y�'�[�5m���~�v�/i]���-`�``�w���	.s�:�t@�2��]�� <Dpf>K�=  �C{��=�91̞�}pm��@�����2�o>U^��jk(݉ ͺ�a8`ؐ��R�4�& ��
��Ǽ�('M[f0�>�ź��jX P�e� 0�Y&�l�,�]/C��Vy��"��H�� �+d�Obl�A�`	X$�`L� ���e�39�#җw�xf5" ��C�\��/��bD�@��#�O	5�؏����_��%���k7�"�����f��M �O��<``d�L���G�=��?�c�'�'����'P��w�}8:oi=���>��m����~������TЌ�V�����amH�#PF$D��9ݨ�2���\��@�gY�5�=6�	ɵ����2�_���v�"�f�l��]6(Ĉ��:��q]��h�So\��(sI;\	����]����������4ue	e" ���)��s�q)'x�K������L�[�κ&����G'_�2������В�{�q�|ip�]w�կ� c"#��r�P^1m�]^�s����}��(wp��EI=Q��p�R�ow�Ĵj�(�Ν{�~�e� �c�-��5H��ַ��P�t����>���Td1�.��Dn˩�8�F�{���{�\�h>X�$�'3Pi��"x��.w�8�r�w�Q���k;��Xc��ԉ ���Z�}?_�Ld�=�v��8���/n�z~������yC�$Ak�v_֍�Fe�Q,��d<1�:�iO���K?9��ue�m' ��Κ�QK?����4�z׹̒��h���wy3i}$с�6
9�;���?.��c,,S����٭z�������6��51�Dg����cۨ�}M�V�ct�%���V��Y��M�� �-�'���g�<����N��@4Y
#�Ŵ��-֑w<h��6��h�?��)-�������N �/x?�;{�İ^�D�3�u�Ժ��u�9m�f��X#��|^��?��_�ݿ?W�	p�}�q�w:y?ϋd�=2�)��<�" �ܠAw����؏�]���$�e���j�/�pK[O�6���N �����X��oȤ��%ͫZ~��7u���1Xř�rK�8�Sc�,�m�(㌏�y��Z�N����%J�� zp�bf=�c�Qg<����"�H0�����D�t��9���dҽtD���k�w�z���N dV>[2~���K�.�6��d��J��9��&�@A�(3p1]�mc��Y��T�E28�r,�1������o]�0:�����}] ���LǱ8��q-�s�6�!R���f��r��k��H�z�A����`�$����ߗG[w&���i+��܇d�>���s �g�p,I������A
<Dh|L�]����z{�p��NG )�G��^kYެ��?�n+��y��w<� �4g� ��	8��Q-�Aܤ"�"� hb�r�"��|����6	�v�{���_����<]l_�|[	�[����~��p@f�s���Ưur\�C"�dA@�ip���L�׋`;urp�@c��lm��eM�� �g�- �!��[�4�1�I��H��sK@�f/� "�Y$� 	$����gY��;���
�[���L�G��)�>i��B��?U�S7����i�����|G���ɨ����� xȀpt�<I���x��>� [z�G>FHa@�!�iʬO�ƱI�����B�����j�n�a)���,gsș~<wx�<4b�觉<C���%� ���X�t]�� ��u]�oc}��m!������#�O��������l\Kt �� $0!�+� 	� �<;���(A�׈d�g��a\���e��k����̷�Jq��co&O~�f?�r��ϵ���#�p�\c�^�F.^��Xbt�d��2� p�ľ�>��,����6|}���	�[J�Av��c@:㐬+�	��6�_-�����@/~�k�� ���V	���00�G��G ��X� ��/�w{�	��`oi���K���k ��E )s̯�n�t��4�OJ����� ��3�j��?�{~�)�tpJ9�& `��,�H=uDH�m$u����:�hÃ&$^��
t�S��@0_�6�H�}N�]�b�+t�|��@F�E;�>2�n�0,FƠH���O�#��:n�x �׼���x�ܤ �>����!|=��uȼ������e�uRh)d�n�z��]c<B�1]�#orDR��,u�g��xH � I9:D{_/���2>_��0j�DK�wh�i�����(�;l����L �d�YI�c�s���=�ɳ�'�E�(w?��m�%U\g��]����G�CK	�Y�����8�5�-���@�h.'O= 8��� Y�6��"��\ǵ�C�C1�>��~^�>f�����4��� zX�f�m�jܛ�x6ٰ���w>�f@b��܏����2@�ֱ���6�QW������u�&[J ���i~��XF������ #�t�7�:� @� J�E��O���X�i�?	ԋ�Z>+��G�	6h<����ؤ�X�y�9o�8���5�1!����٧��E��x���Ȗ@�<���Mr���Q����W �N���(��1�a�����)�!^3��B���U��t�	���f�f�^qK _c=fg�S<�sh`�S�����g�)�(��o�e�-]f�.!�Nz�q��<�OSE��i��H�D����v��x4�3|��'����=�~N��D�7�Q����uq�5j���`G���P�6`�|볺�*#��ӻ~Z�"?��l�AҠ�t>�kt�lTN����w>���}@.�:��*>��1I����� �J�O_�K���&_8?��6�o� �<dK 1(��֋�:�f�d��znG_@��5��F�Y?�P�v`$���(�׌!"L�]BD�9KK�@��-c�t�'m}���ty��K4�Q�ӥ  ��nz���'���E�d�q��x���|&Y� Gi�h4"���U�P(ݏ>��[�4�@�Re��w�Z�0'�����v ��@�h��ҠSn�-i�Y%�1�>��O_O� �F�NL�� ��io�r�ڵ��Z�b�����8�IPi�3H��`Б&�_$ˏơd1_�����3��t�J �����B_����
-#�X�1��8����	H#	���	��E:&�������g?8&�GE�7�~'��N �������Ϭ���E�(.����)ph#�0�pb��P��r�E��g~� ��O5�G�.�W��gj�>1]Ք�L��G�e�mZ"�h��	�9t�B�6j#Y�]E�J�\@�˃.Jf;�<ms]~��^]�_Kn�3^� ~:y��$ܨ'�w�����/(��: ��<aj&��7�v�QZ��)}Tu_���wr�� @�Q�k�FK��� ΐ��8R.0`>D�K��E�@�ɯ�_W�R��O��f�F��y���,^"\�8I��%c��+2�V �Q�'���(}@�;7)�\�Y�}�b��7v~6��v��!Z&�	�A"�9�c��;vP�n����'����z��*T�,PY��@e���*T�,PY��@e���*T�,PY��@e���*T�,PY��@e���*T�,PY��@9,���sS��    IEND�B`�
```

### `src/flows/fno/commodities/assets/gold-default.png`

```tsx
�PNG

   IHDR   `   `   �w8  ciCCPkCGColorSpaceDisplayP3  (�}��K�PƿV��u2�C��
�8�DqU�ꔾ����G�"7�����
�n�::8�������y/��"z��~|��8 9npn��;�[\�+��-%��� �񜮯J��?��>��N�Y�������1����]H�����%����qK���r��g�X �&VXͨ�������`�r���l��9�X�<p�0Є�?�����]r7�R��|�ɑ"'���p�0�XC�R�w��w�O���'`�#�����p6G'k���<02\�����G��V��S`���P϶W�j���<0�(��$�:�-!>���S�p�|�b��[   cICP n��   8eXIfMM *    �i            �       `�       `    ��}t  YiTXtXML:com.adobe.xmp     <x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="XMP Core 6.0.0">
   <rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
      <rdf:Description rdf:about=""
            xmlns:xmp="http://ns.adobe.com/xap/1.0/">
         <xmp:CreatorTool>Figma</xmp:CreatorTool>
      </rdf:Description>
   </rdf:RDF>
</x:xmpmeta>
�\�  .ZIDATx���W���u�A��eٖ,K�	d��6ql������k����̞e���{v��x&l�#㄃�le�rK��V�V�^��W��q�e�Asu��{oݺu���n����������Q+_���S7?�䌟���SۂW��D�M�hMd�_�jK�_Y���k�ϯ���*)�+��?2R��m�OV>������ٞ�ڟ���_����=;��-*���&5���Q���|���"�[p���[h���}��4�ػs�}��=�� =QAϵ�Dv@��?m8cqޗ��+[��6l����e|�@�N�,/J��"�)�g۴��l��t�����};��ܣ���`�O��	�{n�K��nwϛg7���m�FF�|���NH�*�#(�룬��f�|��O�m�c������E��5���[#�1]'�P��u6w�i��N�;j�����lxX�� �O����3&� ��<)𪮸$���lu��`������g�n���ٟu?r��v�D��	ါϴ�kϷ�.�gwΛmo��3��΀�y�@��6ў	�L>����A��-O�u3l��δTI�uwtno۳��[�5<p��홖oݧ���uo��?��N���fڥ,%=����XE�sa(i�.'d YW ?��3Bu��b��V���2�:w�U�<�F�m�v�b��߾�+�+%��l�2뭡��[|�T�R]�}���
�:3KK~,72�#�#̈́�K6О���u�Hk��*Ծ2u�\�����z�P{���[�7?��<��ہ����7�w}�j��gf��gk�l&?4���X�"�Y���X�Iӊ�(�Q��j���!�a��<G��)�l�Iˬ�z�u�6ٻ�g{6m���/�ڐ#S��A����I�q�4�����a�j 0<��X�  #�c	��_�Dvl��w�����1�x�v�;�`y׬(�4dy�����Gz�7=�R��|�w��W�v�7�d�O�p��>�ƾTSm*)�B6YN7 ��x�*Ϛ�;�B��Y@��q � :B9�)�M[ؾ�$:Bw�U����ج�n���?ˆ�k��u������R�D�����E���7��I�R[a��*��WUڌ�-7C��G�,���9嘨c���->ewb�(����ܬ#`B��3��"�C�fFIy���Yh���5[��;�v�l�u?����D4������2��3�Q����
;gT�>@��'x��	��\@���
,N��Y��"��}�'!�R3���!�ԓ�b��u.ʜ��mʜ�V5���j�Ӵ���5������?��:��5]����O��i5vWy�}���
��M>��`� �Fʱ#"�)i�� H@�>c���z�NR.w��B����#��Q6A����SefgŴV3�l�/�������}�����5�E�WKa��m�{���6���>WQi���Yj�"O�� �OY2>@B9�����I2��[r(�F?��^��d>2:�����@���T�1\��L-������Xa�B��>Ա��W:=}k�]�=�1SN7���w���
n9�n�/�/��R�="�h�.£\=��R)� ��q	 wN�gа���� S�:b���K�� �z�����낯v��G=�*�Y�f�Vq��ֶeu��G��?y�^s��19iX����);��ܾZ�g7��z����2h�TUf�I��Tu!�*'�5�Œ3@�Q��@�;@	�:%:C�K�	�ȃ��1����b��/	�]w"��)R72<fM����jg�.k������>�M��n���^���j�ϵ;ug�=k��F
�x<�q��䠌ђ�5_e�s�hyZz��|6$y���^�1� = �2u�� ��?���Dw�yQY=�*]	�iv��1�b��g�ڸ�֭�^ܤǐ���Jk�Mw�̞����^��n�w�;�������2��|��n ���*��8_2��N!�%��j�}Ʌ.�8��4Q�}��aOR���y_N�׿�C|-�^'f�Cu8�C=z���oX'���f�[��kY���$�7d=��\��b�h?�1���S��s/?���SS����p_�!��b2�1�/�q3�Q�x24��H.�����A��-ҁ(�<)�~U0'!7M��-�x�GT��~_7�Q‐��=�֦����-C�>E�n,�՚]yY�-<��~���ʍ����: L����런��Uw���\EQ�+�jy#>N��0}��  �0��g��L_'�i !�$�80�%yt�lB,��]?:Ћb�t^�S����2>��Sg�56
��f��`Zr��-\d��u�Uή�uM�u�h����=�ƴ;�2�\�p���U����|�����l�՞t�͜6j�y��s��K� L�0��0��<��
rPUp��4fO�q�DrL"��8u!��*}�^䘉^vA�� ^�������6m4ۺ��^����Į���6u��6޳������>��CM��Ƿ��W�cr�;O��F����]���笲��Ԝk����=�<�>e��X�Xv`��D;�y���^�&e?v�G;@|s���D2�gy|H&�����!�q�OFBў"6�N�xؾWѾFKN�~-9r���f׿w��w�VXQb�-����o�Cz�]Pd}����G7L�nR���3��Wd벚�<;�w�voj���g�����.��Yٌy�V[�m�^EI�AgΔ�A%�~� �����#�%KIs)��}� �	E{"di{�`&d�!K�У<�d6k�]�AN8�@Q�Ņ��[�����-o챎m�Y�����l��#����m����[��Z���H�����r�ɖ���˯�c��'ٖU;m��l��_�Ⳟ�yg]l����o?Ϧ��[�ص�Z���#�GmT����`�ِ�x>`��#�`�h����ϑE��}.��N�B7���S�|�@
[2���]:�p�٩��u��+�5��v��^�\=���_eM���d91X^�@:(�&��ی��\M�U4l����![t�B[���{�l��۷s������˛��J�\h3O��i��V�?`c�Ze���#Yxx �7s ���q�a��������'�rp���'Ō$��	�Y�%--f/���/���Sv�-�l������z��k7ZCÈ���ņ�����>̀_�5͛W�I���V72n�Ѵ*m��=�{m���*ͳ�-�9����׶o�#��V>�U��:WYqݙz�[k5��f�Ng��Ȇ�� H*� x����"�m��U��l��BΏ����Iwȡ��r��|����i�Y��?��vN��{n���o|���Xd��u�Jk�?�#��i/�sA���?���<��8���6�����zV�� ҫ�����z�ﳩS����셳����vo���V��f����+�=�j�J���ˆ��lH�ǈ]�(7�D$�̄��-49�dT��4���,�%9<'�1�J�R֦�z��~Q/�.</e��z�͹�:�ɳ�����ͻl��ak�{l��NE��%���5C�5���z�-�+Ӥ3��.���A�]S�$�o,}:	t��69b�[p�e6mv��{ض�;`]��[�5ZI�K՞oe3�T9��d��{-��́D�lt`�q�r"��ƁV2D/�0:|�P=*z;����(�!�-��z�p@N ꯾��.��22t�쬷�]O؎u���qܺ�䠃w#
$�g�!�Kd8A�Xψ}�h��x��6M��RX�� G��s�gm���ΖC6ܺ[�hgقη�)����m~q���U��L8��]e�s��Q�VY.K��l|T����;���YH�L���^ǌ�W��Б��}Be���M��ɥ���6�^T��l����<�������JmJmxߣv`s�կ��Z�y�Ag,�\��;n�~)�P23 _���]w3��Xmg��.�Jy�Q�k��$��Ay�p눵�6t�Q�4�c�^|����hl�]Z/��ڨ�Zuq��My���:ͦ�.���.Ռ �����J���(�����.,����!�y��#�-V8���YcS�^X=n-�im���(�������i���֥�o�Ю�V����RI��Y��D{v��V�J���u�}�n<�=��w��RND��m���u��1J��H;��gc]m�i:1]p�U������v`G��[����V˫^��<+�>ݦL�W8���?���Q�2`�}�*!��J�/��0T
%|��_YS�%"�6m��ZNz��ͮ�i�-��
�/�����ֺ}�5l���bcf�b͇ԝ��ر�)�C��U���������[���wwh�0���Ė�1�� iDF�uY{�Ku��ŋl���弔��~�Z�l��)9�GN8��kϳ���6´
���[ޘ��0}�C_�������K��(P"@h_R�o��2RG[�֯����R�+�Qb��x�U�r��{Y���M��f�Tiy`.��@˦8j��G ��P����`�}l�q,A|�f@�}J�JY��:t@�3`@�T�s�R ����~�mi���>�;�T��L�6>4�{s[j���<oee�W{�q�q�UVXj��Ɔ�}s���:�@��[(���90J��N-�TQ��[�m��a;�'�O�F��v��-�r�����r˳�c˰�Z��i0@]�p c�}��.ߌY�-��v�p\���V����+�38]1��ր/0E����Ŭ��k*Z��>���d��N�}�9��Ku�鷦�����z+�h��r���,���Ӭ�jH����/M�^]}�җ��a���L�+us���@�V=�mk��<�/�(ߖ��v�^r�Nd������.ܸ{�:��@�A�Ǻ� ]/����~� �^��h��3��<Q?��J{T�W�I�WʠR��)#ayT�'Pvc�Y7�.�ɂ}��虝�h��{��K}�^d'�7b{׭���v��-�������uq��V,����ڌ���޸�:w�w����E��2;�������Ҫ�ֲ눭]�k:�ټY�^r���P˳vd�;�o�:�M8_�Y� }(e\��X�B��d��4!�v)9�P�����Z��Bx���<��G�:"���#*���:�I7N|�s�HV���;�y�:㬷�f.����#�c�AkkXce�M�>����J+�z�UΨ�ѵO�C��ɛ 3�>���M�=E V��u�l��?^^tn�]s�96���dL��l���^��v�J��? ���-e �z�����<���+�x}`�A�E;-�Cze�'�N�W:�:��K����>%��F�� �a�;@� �%)�k '2[0��<�s�`j��+���u晩�'�Y_{�5m8d��h��Y�{g��r��.��ZECq��{���ᆪV߁��Qg����Um��aLw�f�\[gg^�^+�}���b������G��E6�\���eG@�'���!�ӏx LE ��7_���u�fှ������4�K�&S���z�u	ؤ_��'�X~h���4�1�r����_L���d3�,�3nx��<d{W��͏���F�s�YV>o����XY��g�֒��F�;4�SVT:E@ۦmÆ!��ca�T-�n�U�~��9��!;�Po͍f��zn��[�1kÒ�+�W6S��.ڱ3#|	]���q��ĝ�&�
�D����un��U���Cx� Q�%� 1��ž��j�
���A��lƂ=6���l���	j�5���^x�y�6k����s�\�ñ9��#V<�]�����m��!���אּe�_��?[�]�4��Z��׉ڟ�H��/��{4'vb?v{`)e|0d�\�u�GeFU���x �>:T����n����>0@�#��6/h\��,Ao�p���7�_�ط���ZWX� �������[m�=�]�Q�x�杶�\�^+�s�:��ԽFϤ�ٺ���nZ�.�e�՞~��Ȟ'���M�Ԙ��Ti��HP���v�؍�����T��DvR�u�ڑ�Y����4���g��fB�t�=��}#���b�b,@sÄ�ܙ� �\^�(c<z�-z�ƁP
�C�-�lh��-[ݼ:���";ﶳ�{�=��jMO~O�a�����ִf�m����"{��o�3�l�{�l}��7���O�b9�u] �|���;ӵ��m�Gf:��f.ʪ`L��Ty��<�t�*P�j���&u�o�脙 �n�@r U�e'"����B�3�ў:��z_ { ���Y���d2��uz�f�El��WY���l��k|�!۸~�mn�E�g����97Xz�
���S۷kПnv�q��ʬ��ɛ+@�YǸT��ǩ���I�'����AK� "�{��SCz21���;Z�N�Y'>�0�t�1B��`��4�W?�� %ﺐ�<��a4�uJɣ����q`g����6�w��̹�N���=Td��KNz�+�jw]gk�����E�H��G��s�)�*a\؈��1>r"l@;X��6�Sf<��d�^�ҙ��Ҥ3��VHI�\?��7QK� �Ð!e�`k���e�~DU�(w��}CV}a�;�6bqG=~d̆�=b3��N?�̗}G�T/T�ZV)�m;���~=��׬��Щ4Nd4v�lȈ{���ڏ��{d�����3�|�B�,ˏN#���\	 I����%FtN�aPD�b8��K&����ĝF!�<� ׫���8�n~�҇��s.�g��wْ����u��m�^%�d���3��;tTv	T��{�����i��w��'��|��'���9�~及�d�-=Ñ�~�IT��H9:'��G��Y׽Y��0w��ʚ
�	Z�<�hH\�AR>�<:h��%O���q�^VHNǙ�~���s��u ��g���r�v1���)��� �GJ}�x�#ߍ��G}Y�ջ�<����ߧI0� ]���P��=c@��"*T�˔��HRnV ��Rճ��i7��L��,w������z_��{�;>>�[ ��Q����ހ���G�v �=���,}8����Ot�$�{?j�"}�Nx�(�������]�OD�:�?3��%�#=Jq@�y��ME# :�B�h���l��s��e!х�e`��2�v��)k�xZ/q�<�cs�e
��S�>_��qVR9�)�+=��I(fr؂M���(�Yx��n��4e_�&u�XJ�LˎdD�tD�2C!ep�!�I�f~�:�0r}�3�Ȼ�dGGBl�>`1L�7̀q! �D[���%���qRe����L|5��������z�S�
�Qv���ّV_'�I0< �����; J#���<�� � �����Ȼi�a� |�H��E����1�$D���X`�M�7R� l�:gHr ���ם 6��A�����̒ e��Rv���}E*)�>=:v�H���p �$N`��0����KU�- p�4m�M>2|�B�qm�L.���q>� �.�,���F�*�1�!_~���U�mrd�:$G^�\����(4�������4�h�Ay�+��� ���d;h���$� ���|��N䜒Ax�nL�&ᓠ�"u�s�ľ�G�/���u�g�B}R����s~�QF�Kc��<���q6���&u�~Z�'�2?C���nl�)5��]�<�SE��Yƃ���` ��q�	h�	�#r��6��e��
=��L�'d�u�r��mK�e(��)�.�SN"�ӝ����9]�/w���ؤ��)OF�y�摪4�S�P��x����p�q�����v*#�h���M?{7Lu���]$�A �}����a�f��}ҍ݀����BY�)�9��N��'�̰Y�" X�r�����f���(4�z�I(��O=�	�x>���+Ũ č�u�61�.H��<%������=��
�hڏi�u�|P�"WD�.>���1�R��?չ�3]�3C�+i�~�(�:)�\��&�I�w�B/�
����+&���D&������AR� 2b C=�^�Dꐡ^Y'xN�	S��g�J�|�ê�$E7`�,��&���<3�I~�L#���:�#G?�i���#�;�7b5R�1hT�,�^0")b��=�V,��)8&��''~� ��U��9_o����D��X6X� 
�7�Ͷ�)��6��|!�6%)P��j�R���s�r�tЖ�H7}�F4|�޹R�F���ߤVفN��D�6>8�Ĥ=K�� ���6f���<.E耫��XٍWe8-t�l�$e���}��Y������>�۩�Ε\8�t�����j�k���|J��jӜ���:�L�#��/�,�#|v��m 9��pܜ�5�\ȹ#�� @� *���.� D)�py.WC]"�(e�iw̔]P	���Z-���&u -R2���Pt��I�߀	���8r0��/PQ���.�|�N�	y<��c�����$~�ţ��=��<t��T F�6�feT��Q|�-�P��\!��fB:&hZ�b���3x��#R���%��[�h��L���C�a���G<1�AUJ�o�TǠ=�5�#3*��l i@SB�8�" �Ԟ: $��')y.�q�D�<�QG�؃2D�mZ�,��&u��o`��Q���j��:�p HA�W[�7L<f��%���~��Ֆ~�q���h�dO���d�F�1��ER�S�0:\���r�QށV�IWY��l��I�hCcuyD��A�&�I�?C�q�910�`:���a6�S��iHel��Hۤ�����sՖ'��TP���n�SGY��߹�;qEI�؆Nʾ<�U�Tc[6�U�	�!�	�(�l���'3�yt��)7�M1����&u��a���֙P �w'H?��r1��X<�T�Ȋ�� ��>+Tt�>h˦�N[e�   �2�Io��/��!瀠Oe�!xX�EY����D.���"�կ�ԇ>��)~��SG �0�J�ܣ��t ��1���գFF��Qe��4F�Pv�����:N�x)���S��J]��� |����1<o/!�g#�+ԇ�ΧO.�Od�!T��/�	]2�:��ݑOR%�B�;u�AF�ğ�:��R�����D���'���I|u`!����(�G��XJ��ʫ>�P��L�Ѵ����$�M�%�~��#����E��r*f�������a�/�G����m�)�T�/��:�� k�S^�=��R�X��tFbHR'`gЬ��H �D����� ���`%�Lf	�W����T�<�c�\�MV'���C=W�9��Sv�e�����L<�1�W�/�f��(d�����~S�Wm��ͷ0�θ�y�,r�r�;"dD`�2�uG�A �^���:w@�31�!�!꣍7���$��8q�(a����QP��!2����Ix�!�S�%G��#O�oz�1|��s�J���`����v��c锁�D^L��B���f��-D;(fE�s���'�p'P��$E���-�/��ڤ��Gm�I{��+fBn��ٙ�P�D��Ccv�ov؃��1~����Z���]s��>�Ǥ|q��J�wP�}���yʺL�|�	hq��"e�>�w�%��)M��3�� �� JbN��vI�(�m�';U���#��U��oUu�Q�ﭰ�lx�?���@翪�ճ
쏴�ޡ�4lf6` ���ԀH��2@��hp�L	 G9dHy� u�Nry꤇ �܈�$O{N)�O��"�w{�� �}���R�t�'�=�@�`\���M����N�G��S�CR{��������~�޾�{�+�/�ӾV�i��?� b9�G @	�rR�`�#���A>X��v�ِ&�Y��З��mNuH�^�.�8/q4ˍO%��+���?6��9?�=���!�v�.{"1�5%���N?z���S�]`���ٗ�{�z����4Tv渖� �9>�@�r�	aXB;���Ʃ��! �I��y���ʶ~�1���Km�ч�%���G��3�<}�B3g�u�3;���F}���ڵ��E{�z�n�/F}|�^�ڨ?��ץx{� TlʤD3�10��,8�Hw���2��E|����6�Y�#@'�?�@���V;_r��:�����D��;_m����̮}j�}�%i:x���8��Y�~�����+w�i:������ �h�ʹ`�s ^�2� >p�!Q�Q��R��.3���^��8�p'��9�*SG��~�c�3Ovs����<���m��y�踖�W2���_����η�����ܦ_�-��zia�|�n����8 �˼	�8����E=:2��T��CF�@���C� �.�� �F�(cy**�I�r��-�"ڼ���6^nԃ���{��Gt�pk�[۲_��狾�bЀ� ��=�|լ:/ї���� ��Ǭ��|�.R�A�w��6�i7���j��l���o����9 ��}+��]�vU[����k��d�8B#�h&�%�ye2w��P�(���I��\0��Q�y҃|��4i�u���w,=�f�W6��m�l���[��cy�C��Jo�0�G���{����_�R7p�U���W�)�[]  "� ?����s ����Prk9 +ɂ�p��E
��h���خ_����*x?����]e{Xe_���PW44g�%�d"��`� &�m�SY._8Ͻ�>�q�8*f���(Hړ��gA2c4C�Cv�_���_���~S�Mu@����۪�S�&��'��Z��jY���FH� "�Sf N�L��S�Kf9�ޝ$ �[w���K
�".�p���c�UMw���+�U�5�G����^h���-�~�l����w��ݖ�т��Q8�#���;f��C`�>>sN���`�ؓO����Ԣ��+�zL!'�( v�M���,���}��5�"��lzKf@� �e����U���;�A�hK���W/} J� ��'�3Q���z�ssځ�{DD�t����H]���Ń���h-��-�x�c��*۸d�}p`�n�s�V�?�[�<��w��
X_����
<��S�o�R�;�*�<����Z�{�Ck�k��!Z�}��	� r����K��*U���h��n�?qU=���RE:���a�B?���&��/��f�Qf����)Yھ�W�7�t�='ѷ�^�;��cD�>ez�a��K�a���;�9ӭdV��g6i�٬�c�7%E�4	t ��fc���qkַ����idjO�Ϸl>��k�>�q��l�t{N?�4K/�N�2��_��(3�9}�Z�Gl���#�J=�=�s3�o��R�"�o~h�=y,���2'��-��i��aO�ڻl�~/b�/9Z@��l��qkԣ����}��Bq�F����U؟?�r�o(Dof�L�7����냗�l=}�K-E�W�Z?��� ���Њ�Z�v����������m�o��G/��uC�Y����<C� ���˱��p*G|�����xvN���u@��3l�P��dS�����婆��?^������? �z"���5�=e$|    IEND�B`�
```

### `src/flows/fno/commodities/assets/gold-guinea.png`

```tsx
�PNG

   IHDR   `   `   �w8  ciCCPkCGColorSpaceDisplayP3  (�}��K�PƿV��u2�C��
�8�DqU�ꔾ����G�"7�����
�n�::8�������y/��"z��~|��8 9npn��;�[\�+��-%��� �񜮯J��?��>��N�Y�������1����]H�����%����qK���r��g�X �&VXͨ�������`�r���l��9�X�<p�0Є�?�����]r7�R��|�ɑ"'���p�0�XC�R�w��w�O���'`�#�����p6G'k���<02\�����G��V��S`���P϶W�j���<0�(��$�:�-!>���S�p�|�b��[   cICP n��   8eXIfMM *    �i            �       `�       `    ��}t  YiTXtXML:com.adobe.xmp     <x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="XMP Core 6.0.0">
   <rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
      <rdf:Description rdf:about=""
            xmlns:xmp="http://ns.adobe.com/xap/1.0/">
         <xmp:CreatorTool>Figma</xmp:CreatorTool>
      </rdf:Description>
   </rdf:RDF>
</x:xmpmeta>
�\�  >IDATx�	�\Wy�WKWW��"��ݲe[�7���a38$l�mrrI<	�����fH9$3���xÖ%˖���ޒZ������k�7���.�s&��Ar�k�~�޻��[�w�{2{5���������{E��7:p�^������ϩx���/"z����o����4g2�V��͡P���2Z]V�W�?_�t8�O���r9?���T>���s�x<9��&'#e���luϹ���/|��ةS��E��ϝ ��ws�=�qy*Z��԰��2wU�[��+��\}$���ɰ��n�)�|�|��|��9~�|��%���[м`0�k�9�~:������N�M�I?7�><��p�Gv���	�s!�������m�K����n��xׄ�?3VQ����,��\*	�A@���|�3�Y>��<��ȣ�t�S�<��X0�@8l\j�PU�E'���S�Һ�FF����:O��#Gf~���`��߿����U����:��Ħ�B�����2s 	7=�������u>n~�@=�AВ _��.7����(�2pEj-R���@�T�˟L�r���~��?y�̧����(�,8����4T�W[�S���z=���" 'uug��f���_��� 7v�AQ�v��� @s"�~s���𬐏s� "���;G��
�,PZc^y���V=9��o<��C{?�5#�+�^Q<��G�^���#eၷF��~��A�[�=+� ��:G�ΰy��],��@�g�v�����,6��d�8��%�g%h�hY��˲VX0\	���Fd��M��48���W��o5��4�<��*j�u��Py���9��'o;�O�\�LzEp����i[�����ԯ���.�L�t#��4���8=�^_��L�XD�$mt�lv��y���@[-�%�[g��Ĭ�ܬ�Ҭ����K�VU��-op��3����tb�湷 	R��\<t����*�K*�� �-����<v� �e%�C_�;r�׽��r��BٮM��Y�2	�� ���h
�ÃAA�0���̓j"��驠M��l~��yi���r �PMaAH �8p��CjF�-�p�>����U[���"�M�D-9;h��~�$�Q[�6��TP��Sݒ���Z+m\�}�ة����=��zt��k�rT����V6���DI��݁��K�	�U`4��B�3ٜ��'P'�6=���a����T���k9W��Up�C �P"�/�pr4 �t��.<�I��&u�k�`%HJ8Ze���6S&`s���9'M�V@� gڢڰW�Ԑ���}?��|v٭�W�ˑ.F�|��h�O�n��.X��c����x?P�.Λ������Ȩ%�΍�±u��Z�y�g!N�
�!T�0����+aǱ��`9p���Y4������j	��$�@d�y�VʄQs�6?9`���������@��Ԫ��8�E[~o�M{wq��N���Jc�뾊����Ϭ�C~ PE�# SB�9�� ηD2��1�Ɂq���[�R��ڀ�ʐX4�F�\�d#�)/HF6������T,���$�Ҽ����@D�"�Ԓ��Ը$"q8�!���~��"�,���?��)dU���*��y9�W�U4T|r~��t�'&��#�y�����/�O4���5�� �V
'7X�Y���E���A��Ycּ#W[��W��r7��	$�p��C/�Yo�d%5Wx��T�Xi��?m��n��(H��An&�b� ��T�b��ui(E��T~���Z:~�rsݎ�e�EX�)w�]Z3߼���N?���;?�G����OL�D������UĘJi�s��u�J�F8?_g�=)�?1jMuy[�1dM��-mb`J�`u(� {��0�峒�qr�%V��M�\��ϑ}Q�b�����}�z9uоS?@�p�T�Ȫg"�;2ݧI����Tet���2�E�zL�4Q���TeD��%�D�Қ?h~r诼O��/?!�/?M���7G#�_Ύ=����ډfAyh���6�h���O�T���^�ۆ��o+J{�d���g`�\n
��� fRsv�=�M�e=�Z}��<���w��W���[XES�M���h�UW����^*�l@U5п^��/ԏh\E)r��1�eQ���T"h���p�����u�������L6l�̍޵5�����/I�f/��D������|&3��9hQ߂�I����X,f��j{nwa�Y�tm�6nm����� �y�aV\��D���"�,Z��Yi5`�,=?f�	���ɰm[8q��$�y����@$G²��p�6߸ު��l($B��:K��Ȍ�Z%���bX�$Dpj)8j���լڈ��g��h�� �T�T��M��k"�g��l�^�s|��C����\���7E+�+77��U�y�+�|)H'�A�c'��\K6ډCH�ږ�"�i{��C��:��8��&�HZ�ɖZE�N+oق* ��G/��a����іm{����}�~b��pmK/@�)dSbVV�d�l�����<� mi+��m�����I�S��C���&�^s�h4n3]��Bv��v�Gy���Y�@��Ǻg�EKK>��PK�%���Q�%�������Ͼ=3q��9 5_܋hS�B�P��?�g��q�>�ک �<�.�8N*��p�+���i�K6㕀�T�~b���Ԩys,��`��{-�-m�'NY��.�m����OY6>l�٤��r=y���a�H����#�n���"�8N7�����*��4��!�Mb�շ]Ž硺<<�|/��9r(��uE�=��B�K&@����a�?f�OT�٬���kAgggP%� ���t���m�� �6j�-�Y�q���c'�w�����3g�vt�Y�O��y��A�C��U^���<g�n�T:`���ȣ��!���Ow�����`�Q�s?OlIse���/y�irϩ�W�����f���U��x��OZ�����M���*�$����z�c3�Tr�C��"�^���Rݲe��ّə�"�����C�n�	h�!@��=�V��Q`hY��nT�)\E8�<d+8K�ځ�vYc�1,Kyu^R��C��?85�-3u�]jg������:�?7j}=�6��ڎ��Jyb!�^��d�B̸��w�����,���-������"D
���bō6SR�:%2��jB���?5�P�$�J|�'��.� _�H����َr�V��n��)�������I{�۪!�4B�2xQ��zp����XP��;۬�����&o�ۃp�Ԥ�źȓ��kKD)�r�t���Д-[�F6��o��%���V��<�:�J�B�@4��D������p�V��PG��9]rL�1�YD6�5���<KL�Y%�Qf���;,��:��H����:�w����o��Z4]ʯZ�*�ssV���(����r��2�0d5�ki�u�w��Z�>&Q��{M�IL[�(e��_���"胚rˌ
�;˨�+����	���`��A20ֵHH=K9#�ֺj������]��[������J�ͼg�ƙuO ��*e��r��ֲ
�ya�`�L	���5&%<U�!t��5Tf�*��`�L�'��i���\"tUiep+O*�t�D �*��e��Ĵ�g��&�C ����P�֭c���Tz/��'�H��X���ouV�x�[`��!x��v�I�c`C&nk7�
��\��t����O�x�������Zz67�n���66<��c`�p��*[��̥/lee
y ��0r���Y˜!k�gF������0��mp��=�zK����VS+LD�P>��cS��r3�/>�ie2�7�2i�:i�G�� -�r��-�v[��_ѡ�<#�y	��YW�c�&����@��M����4�>�'�{
@ �p��Ӈ�
��}���J�Vofr����,>6jݱ���Dp�-Y[F~"RėN��+�ɑ�
u��x6��Oؙ�f7l�X���F.���C�5�S�[�	��`��D�߼l�����S�k��
����k�-�K�7z�$���v-ј8�Ϊ�����Y�R�B�в쀘���Yo�sv��j���b��6
�N����#�W.��Fk!.]F�a����ÜM�����yGUE0�Ӏ\�Yf8k���VְD<��,���j<��[��3G�%i���-��)}����� kb�#"P�"�� �[��"�nZ\ sI�dG�ln��bۇ��k&�hZ� �� �2���	ĂP�Au��0���K�A�~��3��f�-���D�oOgƭ��,�����۷��,�(��Qp�2�K����6Ȭ���Vc;�klvb��%x��� �,3O\ t#��&�O�IYy#q�;#�>�Q�YӜ�ő�I�"P��dN�8[�V��َ���F�PC:���,)��8KM���ɆY@"�~@[�t<�&�hE�d�n%B΁���V�,�9��+�Jp�:��y������f㱐��ޝ���L`���B!�S/H����aTf��.�ֶr���a1j��Ԩ��o�K�Z�������"���d��Yޜ���)���x.v=��N?��\R��r,����_���#��a@]�}uO�"�#ZOHϧB@E����x�K#�t�,�:-a�>��p=��c\�)|�@����U�bA����/r�zIhy��S���qXVnA�,��>���5
1Bw�9y̞~|��\��^s�2+����!x_�+jy�nYi鉓VZ�$���Ntڊ+oD�m$P�hx-u1���1�>}���uW�p���8r�tƭ�� �uD�Y�5�;���6P���g:������ �ԶxZ� ��cST�PB �4 ���(J'�V͒��`�r���q�:�A��چI&ڰl5`+�p��{얀�:N�'w���7�����t��#GqA����(,�������
�^�f='�XU�jkjی��1a&��
!7y5J�<X��T2�kGNƭ�H��7�OƢ��q�R bI�+��Q����T#y]f�	}�K곾������%$��x�ߩ8��"ZG-4&p�x8�1���!S��C��Q\Bސ�4�5h��lZ��3�6�w��V��2C}���?$��f�w�����I��w[�|2�aT��̫a��yf�4���[Z-5w��<i}.�Q5/RN�z+�^c���-T�� a�w��k���ԭ$"(� ����5%61�F�e��f\�rAE����Ͱ� ςy��.�wQ*�-����ɵVg���
dՏ�V�����M�B(����^7^�:)n�N�aa�  g8"pr����SOřD�m��QL%-?
5��(��;��1��WB����<��.�a^�c�p[�D[�,�~�C�HIڪ��/�|$���PT��u���tS��[i����&$���`<�*���6����ٷ�0�K"��P��ڳ�^�,���3X��Z�au�u������Z�%D����6<����:�߬�.��B|g����fsqf��G��3�n���%�"����!|1�n�h7�y�I�ɝ�s�;<'��2v��"k+ֆ�[<��J�c?��p��)bFq�h������f�υ�9+�C�jj}�_�̎�b�i����
�?��cH�z���UK����{	�A�-�% ��O��;�-m�V�k��RO��"���ܲ%m����Ul��q�;1UWTF��F밫Ws ���q���72Ў{�G��b��8���(�Lq�%�7l����ٴ��n;�N>>"Ä*�\�7��h/��Z���V�����!�9�;�a�:��yS���x4���P�i��50�{�v�~-�Q;� 	��X׶|f-B��,�0^#LHGaW��	�oi5`�Xc}��'&]/\��T��	�5���A;r(h�o����I���렳��޺լo���T�Z��jX\�|�ŔSq��M 9���;�_�:h�L`Г��.�^(��9j5�� &�0G��g�X�:8��������G\���Ņ�a�
"�+�n���6�޷�����Q^y4G����)Z��z�췁�b?K����E�ԛn���Y{g:�W��%l���e�t	$Á���iqE��tS�o��I�� ���Œ	8�0 �Q��h����W"��H��A�]j�ӑ�\b�u�z�,O�>aӳ�]蘱�i��-k0�s�}�-��=�0[XXv,�3�����͌�Yo�R��efK �&��Vy:N��L��h�j��l�M����*���y�vlO`� ��(�ꤘ�C�pJ˺klj��Ο���X�`a�5<z�Γ����.���>̈���gmɪV��Zf��2�4�B��q1Z�ԇ0��Y�={ޞz(i���V�ٱ�x
L����<v��9輥,@�A�	�XY��� ��!�d6�&v.[jk
���<���Z�x>Lx���fg \a��E�8^׍��He����"����f�Jk�r�=����?x��#���C:E$�'%Asƪ��l~6k�X���a�PE��/�W]�h���gy���4��p�u��@���iZ���_R�(�!]�����;�̀�k�YA��T�������
�#���� '�g��-�K��@�؍��Hy�F�֯2��/��$�m��jg��
";OJ�����}��s�l��<&q��>8�nw��rNE�gpU@e�CYC���V��t�x>k}�� ��e`���=i��biQ	 T�a�Y�&�Y|�=?>e��m�M퇻�L�`:���7�*q���oī�u�N�c�+m��!̬M��dO�x�M�[eTV�&.����c�>�� y&�2�����R۶8]��U*Gz�EO�k�V�mT[��kX���v��y;w�m�ʤ�zw���u]�+"��������U؋)7���b��3�"��d�(� ���a_�L�� �{Q/�~���?n��,N����#� Հɮɗ:��:<��n;���ն^a뮹ٚ��9c��Ag;4�VDR�SY���eԚ�*^/0���*I�.NWL��TN.�S3B�$���c"�U�˛�[�o�gػ�q�[�l�^wu ������D�MO��4D�>SU缾AV��<3kL����A�,n���iQ,�dK��F\AI3��s3�����Xl`7�T�l�#h1�(aa���I"�e�֌����h�J[��Zk�p-�=� 6��ȋpD���Q�: "P�R$�{"�~;�E5���p�p���њf��/a�`��m߮.�=��-o���v�� d�r�=��O]�s�[޺�JkP����G�ĳ��5\q�$Pa3�R7M������]�es�Ni��u�Ӊ#'1hq�q�/�����O����W�Z�$(��$Թ��Nkn���x��?�a�Su�&�l٪��z�� n�0.$k�lKV*%�
aX�WvGu�[��%�Ū�H5!�j�T���4X�]�u��bQ�%�{l�r��h��z���R5b%O�$@X�ba����{��Z;�B���SJR�'tQ[Zik��[�/�%@eUmlR)V� ���tJ2���e{��wv��s�-3�(�x�8o6
0��ICQ"���ؾ8=i�ۅt��*+Ŋ��VZcC�#xG��
g3����^�+��s䈤��
���b�kb�f:s63z��\�V^�bf�o��d{d
���/�:(���-��	�Wb�j�C��ι]��V[��ǚ�c9��h��@m�ӈ�v�(j�ýU��SC�YzN^��L:U����T̞��7�;�hm�������-�bhY͢wr/E�U\��i���*ty4eA&�����~#�܅}/��9 E��J�����!�%�RuB@��j��c!�׼�Ŧ��"휀��xWDK�m2�Dep⼅�T����!I����9ܘ��f�HU�s�$�9w��e֪�z�G&�(c�}D���������� �����?�O�vG���cp3-8cFc2F/��h{Ǚ����h�m��NG�Zrt7v��m~X%�xKi�2�������l�e���� �b=S�ٵ�v�hbŖ����D�i�NeY3��ŧ��n��Y��}:WZ���jZ�vw�W���?z��cO��\퀗��8DHBI[�k����w.�wQ���v&�+V��Ա�ϋpnQ>��Ľ
`�!�z"��aK����#ΰ��{-�OXtl7K���硇癴L�N��R\n��r�� o�N����IHa�L5K]�Cc�Z/�0!&#����}���R1�ϝJ����0NAiYR�N*���d���$/����\�ZEK苈��k��Ɋ�k%���KH�`���r���֍��ف�i�T�g�	�Ӊj!��$N��I����#6=x�Vo�͚W���<C��[���3�����^P��Z`K���,���N[Nm�1���).`�t[DT?��yC��g��� 0��vìW�/Z��n�(\���4:>����u��Τm^G~XZm��
|Ͱ%by���	�����A�~,��}�㢉�O��(�Η6Mdm��2;�L�V.�3�A묞)��F���3�����
D���[mݖ׳>�����'X�t�u�8�1ϫ�Ȳ��R4�rIgjKg�ж�V��Vq��s�MIP����
|�R�yk�E��Ey^I�9;�GU��'����L!u%I�tcT;�g���,
;X~_�6bkV�w��TYI��X<-J �^�#c���V���2�li3�f� �f�E=^�:�8B����s��|�ښ����NW���b'�)��ΛǦ�d�	��#��AS�c�S��,+:ϋ �$�/��H 7��R,�ЎvC�e�R��g�/�K��TL���d�M��R�1�O���#f欭���0�&|�"��T�Ԭ��{�2�ϩ3�lʶ���&�-LlIVhѴ(o'aЬ������}�����%;<��B��8O�Q�q�Q�ah�I��%u�&O�f��kk6[Ų60�����mۭoBxe���x��+�vT	����$n��f9��B/��M�F�(�N�]\v��egꜽ ��6M�'��=���(�˫m꿒�F�ͅ24y7x�����{rG͕����3;�A`��è&͘M��7u\�
߾�]����K���7@f�V�].N� �!ݨ��T���R�"�J����!^x�{H�Ӡ�Z�΋wm��cSV ��L����B��
��VaJ�gp���*��!�>g�h�	u0�Zp� '���N�h���K����"����Aߋ*O&Kc�*<Ү(k�vޜ���>(Ċ-RBm��E	�а��&�؄�{_�ݶ��bF`�6q�B�"��:/�F��Y^xq�-�l!��J�A�aܼ�v�8������3sy���fw��[ǹi�˖/!B��C Gݒ@��ڥ��c��A��&Y,=k��(;�@�,&Q(\�U)J��{���yQ���x��)�E��s	�] ���!�.u?/�gQ b�����G�;wmz{��ݟ�[X=juX�I���x.wU�r�����~	<���l��R�����r&�6CH��	�RA�~����s�,��\�j)qs��_�h�"!)X�Km:u�}1�>��{:�0jO^��<J2ʚ�>�4������o{���9vKP���
�ɥ���x�OcӦ��Ε���0�"u��>�޵�<���q��a�x�W`tI�vHՀ����_g���d�:I��s5�t����H�Ȭ8���P$�JjDaqx�}A��;ޯ��"���������@�ѡq�����MY�8�í��W�Xg���E���8�K�8���/��fCj?"c#�t�T�~�vź�}���H$jO(��B�b���H�Ѡ����蹤�M�<���}��ʑϕ���p����pq��:�l�Dɀ�cp��W]/N�x��E�S|F.��(q~{c�m������/U[��Y;~� 1�Q)�$��KHT�j{\��47���
�p=��3��9n��wڪ���,.݉3�:őmq��T�(?]�Y��D�"��(<V.�E	�/V��qn
$G� i�!"(9)�L�p��x���bHU�Y��ڢ�����l�����o��7�zl��c�y������*2^P=;7V�s�$Oe�6���2�p�=�7���:�(�=oW�g�w�����������7o7\kv��$�,`�z\��.]k'�@`.#��YjK�����ѵ�.�-.VNDW��3��(����t�Vy)'����L���9T��;J���j	~�՗�m�Z,��+gW�{�`�*�0���*,�%�@�7����N�����N���É4�9��$C�v����g?p����ig;̮���*�F� ��8��v,�w�
���/ptU��\������s�O�[� f%��#V�&�$ٍ���#w���ꓷ��l?�ϱ�у�x�oGЎ<=d�'��䈯��s�.Ơus��c�@l�(��K~��K�K�hD΀	"� ��4��>��[|{���fw�3i���������/rn`V�Rb3��&1��:��4�jC�	@�/���#�(����O�:tA��K"�\N�8a_�/ɪ����:�� v�5b:KZ���e��wTYeS��ƄM������ȄN-S����5�6��>\h���E	p��vu{�v�q���5�G�a4�
8Շ $`=�����a�m�������w�������!��=o��fWn�__�@WP�P]R5Q��[�wэ�����T�KU��8PH��By�C7�.eeT�L2�G;�rs����f}�1�a{�	���ڌ���(�R��#5�zܙ{n!D�L^���>�eƱ}����o�q+o�4�b�q<:/�s@��4}qR3��u��2��	;\mw���v��Cv��E���}ON��#��*��A�xФI��4HZ��"��*�hE@D<�A$5*���	$q�ڐGė�lQܪ��y�dg�ݺ�o.L����{A*͆�k�"��9���A���~��b��z���G�v�k�#�K��&��xb>b29t0Ş�R{���EQ%j�u����� ᖀ҅&=,P�ii�Ɠ���x�����{��7����N;���;r�z�^8�|�ח�����@9�B�9�+�K��}���z�y��>�#��	:c�������n��Pm��jF�a��-�c`�cBA�����c�r�R�@���QW;�G��8y&��5lv�=�7�o���.�% �#�O�|ַ�Rܶ���?s+VꜸKp+P�'�ŁJR�e���0�WyQ��[V��cj���7��&��Ww��w�e��-v�oG���cl�8կI�X�C	�ym̩!�"�9")�� �ĝ
K�<�~�2pRBD�vS��y��/oD"� >����L�x�]:�T��-��	�!�p�9��.d�rQlUע��z2���s���kn-e�4�0۸@8��Q����(uV�������4���&����r;�^bO�8i��
{�}�m���q���ؠM��S�Ib�q��pf��6XJp��M�k�r��6�^��TXk����g�n�N�J���I��!�:PU���p�k�I;}Wy�9w� g�?I���z�d��P�����x��O���w��Q����� p/W�\�R��T.7�� 0�<'�^d4]X�3���H2�k�p� �G�q�p���R����G�����.���-xQӸ���jB��z۽�������f9��$�I�.�A>�[k�F*N�R*���}(
�g��q�ΪVg�#��n2�s0��n���D�O1v�#�Z���(�Բx�0�@�+�"u �>u�F=h��kߎ��ێ����kf(�����T}qP�ED�KV�\I}iÖ�(%�����X���|Ӂ��������"=*b�a��\��>RhK*�%β����F&
FW�Ϻ�m�M��&���̋!��t- �y�ټ�w�$����u��{��.ȻR�"�.�����B�
�E �wz�]�VΏ��~[�C��H��)��`
������f�X�A���{��5��T��rX@K���5ծi�V�5h�1' ŹM*GFZ �P̆�]G|1�#*�ݼ���A�"w���Z�uq~�>��o=WRM�T��ϝ5���ǘ?�(�E<��)�)r ��,�%�~hsxAh ��dyZ�;�w�>�[�vͶr���´]�F�� tAR97�b0/r+���'.�Ҟpω=�D$]��V9E)ݼ�k1���\�b�h���SցL}�_t��T������Y �P���$_�^�\O�l��c����j���/���/IM[7��&��hU�B�8��t��� ������w�u��\�����zxQ���F|k�u�H~�X �8P�9b�[��@E�wP��X�V�K���@dv�T�B;΀�R�R0������	,C�	Β0��%a�Ю!^*���Pg�`ؐ'�+�P"2'�Kj������c�UY4�ܢ��ʺ���I��������lM���� K��}���<�:^�
zx)�
(�[$� q�	w�Iݓ*A��p��A����O@P��ӱ�~�@�EG �T����Վ�^�	�Ҥ����������Y<J � ����#�x?"}��Q��&�/�Z�������DQ�}�@��pd?Pe���~n���KyY!`��Ō�΋=�~���B���u�MU����-���͆��H z]K:��c��QV��U�j[D��DN�s�ؔ��#�r{P7';�C�9}�sfo|#�@;�������^��h�o�=W�m�T�x��6��;���pc�� -�h�J/#�w`з����lox�V{�Gg���3�,l��?�,�a�#��*R�/��"PX�x�Vg��!ݫ<V���ө1~�N��M^���va� r�E=M*UI��'�	]Ro�+o3{�{P?�������+��ԅ��f��&�����%%1�%��7�8��Z��>*��F\(���4����q��˯��w_o���N�[�7�\3g^�w9ׅ��efzE }RR�)}��z?lӪ�_/ה��|@�G�h���$�*����z��
��$F�A�-p|��{��!� 1�\NxZ}V��H��;�@}q�|}(~�L�>u��ᥥK&���~�u3�;K-^����	|uL�}�����H�����)�W��/�7���l���XNپ��$:�^UQ;�nWo*�2�J�[�l��m�*�-��: #��R����h�&IB�3'&�}&�.&��O����j���m���3����<ҠY��^�<@v�<@�s��� �c�a>�{�u�R]��������f��9_��VԂπ<�!��� �['%�~�y �����d�>��{����m���N�X��Z�_~�xL�Ń*J��7��Ӧ'_m���'��l��kQ@�I?OBT�(9 Ri	:�.s��� T=u�J����טw�M��`����1�)���Q��U$Vm�M�D�G��ҷ��ԍ��\�_N���;��	+|n�o���jܽl�MO���[$�z�q8������Zਰ���h�U� d��y�;y�ώ�Y__���������$K�d�B��D�{Z�['�g8��� ��<I�!|�@2Z�۲ެ�������;	�:|b��$����a���7��(u�CTiO?}�pR�,D���;˚쏾���oER�_��%Œ������m!�e��������]h�f��@�߳�6��8h7�����|������#�?��_��O�U{=݃֍�d�##l�#�F��3�B!@_�W��ԋ��w\�}6`��|�3��Ĩ��LĲ�X}��A��+���ꔼ��0������;�Ҏ��˒����[S�빊:�=��+��r�?>�M�������8�(���Q��ɣ@G�'�Y�bq��Q��$D�5��L�Ǟ~��}��u�xm����m�*l��!h>K#�yd_�_���Փ|
�7Q|�!Ŧp9��4�>��,��ҫ��}�1���$�!�rT@o��[׿Q#թy�Ʊ@L�G\/WV̤3�k�@�h�	���|�Z<�L�Z���6�;��o��o�\P>�{✢�&DT�}?II�5�rߤjd��)�4��̹v���΃��y��w̼_y��������ͪ������ٺ$�c��/�[Rc�>�͚!� nŵԧ$4O�-��T���3�>��'�o�w�y>y$�)~~�>a��<�DPl�/v���n��]�d�|A���W/Мa�w��;��Z��z�@�r����}�� �6���	�5djV_�����b<��ZR��z�<�ݖ�y�hw��F�7���3޴�I��tѠ����"$g�s�sI��{��T���?���?�K"�O���ǒ���}��ƼU�_�B�I�l��w��Z��8�� p�svtF�QJ�Ie	<'I �h�������%[�P�,����>�����&��o�Nj�.m��n�@R�}M�\���s���k��|��._��g��A>.����}�F4z��T�FLr���'i(A�m��H�C�N�D�Wh�+��ʗ�\���vX�[�#.�qx�6��J���J�4Z�)��l��?���ϻεۧ��1C�.O��˗>��P�|�-�C�ˇ��of�V�ɐf���,!D���BQz�"�q���� ��q���ǋ���X(�$y� Az1�ʫ!���We�n���UV�D<Tb/o�<�7j_����4���J�b�>�={����Я��w�bf�<�əS Hg;}+ �-���#/@�v@Ke9`��k�t�Ʃp�Iy!t��@-���K�))�K%T��2�2�؟f�����ǽrJ�˟^��{�X��G�}�=���v�0��V�g�f�N��]/�!�+q�vpv��N�sűE %n1Dy�."��3�\Ya�C�%q"�#4g1��򞝋���
�?�͏�陣+�W&�b(v�K�M��{�=y���O5��[�w��l`ɱL�ʸ*�-"U��"���8�.r��:��5Ԣ�˿P@e�Ay&Е���q��^�it�3|{�������]z4�5�S�y�	P��?�p������_��,o�m�M�:�Q���'6�p@<������@bLǝ��3�\�h"���@I� �="�V~=q���j#�ئY��<��䃐O=L��=�����c���%���Ч��	�k��qp�n��l=��%`_�:
��#���"�R�y3WD��b|��ˏ�	�-��h��r�o{�#�p�Yl;{����w�8	U��Ks�¤͛��Fv'��
��Mx1k0��؆�����7.����嵩2&jA�N��G�h�c9q���	��Q�v?R����7⤿8�� �,�! U��柍�Ώr�`;(��5�:�(S��R8[�.o<����]|g��ޫ�^E�U^E�����p�	#��    IEND�B`�
```

### `src/flows/fno/commodities/assets/gold-mini.png`

```tsx
�PNG

   IHDR   `   `   �w8  ciCCPkCGColorSpaceDisplayP3  (�}��K�PƿV��u2�C��
�8�DqU�ꔾ����G�"7�����
�n�::8�������y/��"z��~|��8 9npn��;�[\�+��-%��� �񜮯J��?��>��N�Y�������1����]H�����%����qK���r��g�X �&VXͨ�������`�r���l��9�X�<p�0Є�?�����]r7�R��|�ɑ"'���p�0�XC�R�w��w�O���'`�#�����p6G'k���<02\�����G��V��S`���P϶W�j���<0�(��$�:�-!>���S�p�|�b��[   cICP n��   8eXIfMM *    �i            �       `�       `    ��}t  YiTXtXML:com.adobe.xmp     <x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="XMP Core 6.0.0">
   <rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
      <rdf:Description rdf:about=""
            xmlns:xmp="http://ns.adobe.com/xap/1.0/">
         <xmp:CreatorTool>Figma</xmp:CreatorTool>
      </rdf:Description>
   </rdf:RDF>
</x:xmpmeta>
�\�  *TIDATx�}	��U��w�yLU�*�Te�HH!2dR�Dl^�.��v�_7��v���'*OE�D#�y2��J*����R�<������?7�2��|uμ����g���o̆Yf�E`�Yf�E��G|KB��D��K.�M�9e��{�䕭��{�Ўm@��*�ߌ
7d�B?����?�ǧͅ?.0��ѻ��Pï��ߡ���F��M
�+ټr�o�Ζ�s{��>	)ј�x1�	9����VSu��'��|�q4�_�W�P�GN�kﹷ�@�`��6:�I� *&iV 6%���5���;�j�}_�e�">�
��hssY�]�%�C�c���_�j�	�	�*$5{12Vb`0��\��|UQ�on�/�F���X���򮊚;Z���|���������P��Q^ʈR�Y�v|�2r�<o��c'[��v7�W�j۟�[���wS	H�8�����QQ��������	t�-������$�%��WY\J���`05��M���>��Q�n(���P(��)8������k�6�� yhI	*7Kg�f��#��EW�61�aeh�D��At����������P��J
����](|'�Q@(�)�����5�k�5���M�@M��^�K6��u@y����S�fPTt,gO
|щ$/�T(����y��������wBd���*NK�=4x{����o���ȵ �O�;��,��X���r�~��W�R��a�d�J��Bhl����:9.!uަ�;�?��Ӱ��|��4Zd��B5�f�&��Sw]_� -��
0>nq50)����@�N3A���*������=!�~�O��KdE4&��1>��-����	�h����l�tyCS�C�{�.�F��݆|��Ղ* ���m&|�,�-ϴ˻2Sۅ�c}�%�Ow�������/��W�Ĺe~8��4X���*?���@�]��ƇGO 	�Y��Z�
|��%��3W�<;�0��;E(=V����8è����,C���q�'!c~4d�����S�83$��.�T^|^SEݯ�ʗ`b�P�В[�f{z�R���4kw KA�f;�Q�f���XkI��C *�u�|z��碫� �|	ǝ�1�A�Tj;�yQ~��/�y�����
]�g|������}��L�O޷l���U@��Y� ��rh���&\��f��Itn�||�Q�bY��� ��}	k�;�k� 
��bx��-��0�/��Y�6S�}������G}a�]��ՙ>ߔ�+P�g�j̪	�Y2�-�)7��ج���"Ey������A��0z+�q�����S��ơݕ�&Vg�����3�萍�>�x��9x�7��no�lI���B����;�6�����)��Ŗ����F`�r�Spd�.&�̏��"Ͼ���lBzP���vQq�#���C���86��6̝)�(�{B�+�%��V�������@,w:V �������t�c {
��+��ژ������vL�8ϲ@l
��?�ޚ�(z�U�:g��(ϫ�&5󘠁�ǚ�Qah+�$�4V?���{����M	��u�V���0���!��z%�Y��*(-$�GV��~����6�Lm-�����̀���W���yX�y&G;Q���S���	��%0fFLB>��(���7��謴Pm�Κ=%74w�⼫��%��F��<�f��P;l����nIRI!�tN1���S\.�E�>�>�)'��ۃC�6c�V>A�y Ɣg��>�%M��n�|;2g��D��s�����Sw�P� b�������-EhG�2\k�>L�wB�W��[+�)�+W[4�N��h�;�牝Xz�zL��|OB�km\?�R�f����&&�4'�gB"������5ֵ�[�_�(�`�7;0l�e.B@
�j'w`�0�f�����)M@�����f��<Z-Yi�Rt��@��8����5�i�1hP#��r�&���}]:>ΪG]�ۍ5���N_�R��hɫ��|�r� ����'���E�ڰL�Y��ࣴ=^���MTb�����]��l!V���`'�
[m|�A��b�i�g���K��kW��	����YuLAc�+a�|�����-e��N��F��@�Mp�n�"��j�/e9p�t���qu�c��X
�N����Ϣ�v;�_8����p'�Z�k�h���ueZ��z�M	J���e_����9��1�á��0X~慭�-T�/���m3ͧ������  L`��jf� W����ޞuR��	G����/���r�p�F����T�vu��DOJ���j�-���*W0z�G�G��\�q^����KR�l�/ZqI���;�[3CϽ,1+�&Xd񥀲Z+��f�̛_W��P`��K�nGվ�t��\�ުm��֝*��R�vk�x�s`�BDC��'�MFa�S9��c��~G�V����?�+�L��������* �xm)e��@`{m
a��v�=�L���b�"�}�_��gK���S19Ј��&[p��42����*�2c��8j;I���ɼCm�%�c
h��ת��ok<��w����f�M���q�,%��MrF�g_�9���̑e���H]�|��k�W��;�u���47��|�����[?Ʋzs=�4����_/ͤ��ë��;�qo�������xm�[n��c��o��m�����u������rD�Y5�,f�� T���Sx��~l�vM�[;��)D@���}UO�������t�Mh9�l�ù:����g �S�� �5p��v�rVr���O;{q�'o�+�c~��޽�^���v5�k[u�?���[ �a��V/����6��)�Y+w/��R���w�G��.��������Y�X���=��7���q���BKz��\ёU�Nc[P��y�_>'yI���n�wo����Ì)�y낄���慨���IId��I@	f��<3�h2v�!n���v)L@+�fԂ���sg�@}��^p���c��X͗)S��|����1H2r���|�[��sÄ/�#KzO����y�?�6�ٌD3�����Ӈ�}w��R�ٶ�^�'x�
j@y�:�#p͒����R���(�g^���b�V��0
�eZmq��۹�>�E�=[Ƌ�oGkES����/#�����оޔ ka;թ��6����%Ƣt�<�&�ɪ�ӱPlٷ"s|8pgy^�%�����]>A��δ܍��L1tIr4�V�)Ƌ��ܕ��L�Ci�!����}5�	��EX��x�y�m��N�N}̅QZ��k\bo���7f�����_�t����)_�#ǂ�_�K1�~:�qAg��]%��?��:b�;K�fݷ:R��vo.��|��¦ɘe��RO�K�6;��
�gy�oC�E��l����m� ��ܝs}�q5�D^�3k�f�N�>����I|���$��#�m+���U���w��՝9�Dbrd	���@�#�e�ف�r�%�k+��Na��-x����g0P�,�^.Ɗ�6��������RIƔ&��S�����d���;_� Z�����o�E��;�Ƿ��7�����rg�����p�)�L@R�ׇ,�^�Hh,7� ��kF�9�ewAj��4E������2�}����z�+�:>��wV4���"��^�����:�:�5#�x3]׈�9x��@�t�7Pn1�����4�ʓ�5Uw?P��q��Ș]�Ф$p��ɯ��������������Hi6����	�2t�>�}/V`�y�yMٍ�ʎp;����lL�ɿ+-���W,��1�2�S��W����F3������?�����@V�|�-=nS}y�C��ׯ�ݬ�A��13�$UݿgeJ+8˧P�1�Ug�Ό�._��e�m�B�r;x�P�[�
�9g��}h-�0��.��V,'������S��c�y(m ����Ѽ���X��~ܱ.=�_X!f2x���$�����P�m���!rl�����Ւ�m	I�E��Y��䣴��v�l��,V�|�Y�GW4m�8�r�����<���*��z�\�Q�ڙ#g��2��L�����yf�[<¥V����bD$T�q�"����@��g"H�7���_�X9t՞��1Q����Z��x�)-W"Pe���$��d�&ۨ�)���,>�j�܎�4~���<ᾊ|~����5����@kx�$a/�d���JOrWc����O!p���D�nZ<y�S���=->���$����m%<�c =��^��ڒ�_V�mɎ��o��<S)i�)���͍x�T&a����j��iC�iS���(�pb�0P��������i�h,h���� �4��r�1�����rQsҀg����D�N�`wElc.��σ�y�L���i��ؔ$|;wI�)+s&������v�������ǯh�j�uM~y�,߹u��KP������"[D)�Y��KQ�3v��K�@�o�C�$��,�2��_ž��p��Ѿ���5E����z�%W����}Df��ΎD�S=A��[�G^S9�	��֥� �s�>�tK���muǵ���ei�.;{q��~jm�ۻ��
(y4������W�������H�e�����):�����,rئ ��/ �0����m,�K��	�{���]X���T�*_�� m`t�m�sL� ��,_�@��L��O�~�Hغ3�@�CK�N?��[*�6�,Qw�n�҇c�8SҐ������qѺ��O�,y|�[�h�u�k��f��S���7c�SB�A�����b,T.����,�>5dY�ʝ����s_��D�,�ϯ߇܁�� >n�/7�ݍ��f��V�)I��+b:�ng���?p�>�ʘK��|�|`y�,��l0�ɿEr�ۥΐԹшO����8!���_�<'��W�LmǾJNF��7�^W�|_NI��vr��N8��8��po�	,`cJ���wJΥ�Y)I@�R����:�5{�Δ :qI�6`�C;��x6oV�p`[{���Y��u����3��gZ�"R�N����NA�"�~A_��
�7��vu-��!�w�$�Ob��9���e����ܹ���.:~��)'�.}�<Q�q`����Ƶs��G[I�!�O���8_�?�X	\
i;2'�۵�y������:�(���%�����+���Xu�̙3�����|��襈^��)M �2�˒{�yM���x̠�xd;��s�ߴ�f��_��V�H����r�6�uk�^.�1���)wVDߗ�;����HL�_v޲�C�)���@��|�9�xi"�1k��,?�?թC���t-i�5�1�9`n���Rȏ�u�<-m d��3�e�2��|��c�u?v>�lX��,?�<]�1.w3F��H6�8�\��$��Z����h�eT#����������XFW���/b�~�n��)���*6c�k|?作�PjP�$-���2�ƪN�ښ� �&�x��}$ʇs$d�JGjg2��U���K����3�~�'вw�$���e�!%��U��P��dQdZe�@�<��bZJ���&���d��/`��y�=���ټ�Ƕ-M�CMZV��2��J��������,6���E�|� ��^���_� ��8����ذ�~���.�O�4gHZ7�7^�r�Ҹ�t�q��q	��fA�L�9�c����(C�����1����ʕW��������HG�8	[�����֝z ��~��$t�BG�Ə���}�U�-��l�.a��(/�U����Y��k0�V�]����"�+O6�G�aw« ��x� ̈́�Aڒ]�L��@eإ,��=@��������Y"�(�8���v�EǼ
���޵���l	D���\����CL
&}�ģU��Œ��Wu=5p?k�Q�׆��Grw	J���`�w����n,۴��kAOɋ�M����r1�^��`�	#`e�n�a�S����*U�8�{<�p�]�xᾧ�I�ȉ���j0�)���Lh�"](�'���Yy7�b��M	;ya��XJ�/�_�!��(-%�Q�z��f��$��ȿ�W���n-��~���s��I��K� 7*��
�hm"e^>z��z��w���ߤH=��=F����ϙEM=�ѶKV�/D���Q��{�J$��5`�0�;�;{j�D�	����j::��Dޖ�1m�����yc������Ղ^#j�r�a��j�N�2 쫢[�X��O-�]�!���CwUA(�����A;9��2/:��r=���m�~IIM�8����3��P
�:*�ۼ=mAħ-��f����ny�;�	,]�ud��=F�u~d��#�88�����B�2����hn�@WM�ʑ��4$���B���o�H�_���QJ�)NA�c}����X%�^�ɱ�y�$/\���R��+�R`�����_��g�4d��۱�3��b�����<��4���a���5aaZ�}����C�Ĵ�Ph�5���o��V/������������Vx~k:�C�-h.y-U5�F�Z����2�D]y/ǜ� g#E^�I��7�}�}��tN	�	&K�h�B(a�`��;��0�Y��� �p_��b�/I�Q��Yܖ�I�uF�_���@���?܍��E��4	/m)ǥ���Y�v@���"�b,�w��')C?��Ee��5��+TZ���YO�V��vz�Q�K}��N�B�ebjr�O�7qe�n�w�Y���$� ���U?ZJw���x�S��Z����^�¡��>d{O�H�S�����ѻ��p��8�/_$����ˊ̢��i�x��k��wR�-FҪ�r���W�{H܀��%!_�����������c2؃�'�EL�"�L��G��P�$P63��X�F�O���S�X�R����,�����$�A��_��k�x�����A���R�_�B��]��'������4��O^�I�z�JPVX���8d-Y�v�8�����I�����m !Oݹ��?��!�<x,Q u�	�b��c^�������7<��k����b�/8}�^@�c̗��"�f�螴��(~�nDs/��n^�U��h�\�[pő�+!H��d��U�2�˯k�4�?�Dq]g�f����F|�W=Z�ہ{�
�����)N��C�٧����F�v�&Ƃ>ы�8�I=���ݵh�n�P0�Wapp eTD����ݔ��?nL�/^C�)�psϩ��p�h�s��P_Y�܁$<+XowCI���MtK��X�t/�l\���?ß��`��%��0Ez�E���ŪS���^FO���4�Ϭ-��N^6"���@��x�4��j��?�KA�f��ۉ]Vͱtb�}���hk�E�/�M�ӯg���߈��F*���O`���m�~O 1s!}�$J�բ�}�x�N����A�+�q�l�֮Ŭ=*�{$�r����E��ղ,� k������PY�K8��80�с��}H�Z���H�ŎG�@Y���l���Ye��+�N��vtkR�� ]A��k ��q������b���_����t(��qT���Oyͬں1Zv;V򄖔����2�d��@���.��u�Z<��d��o��o��Ф�<ǟ��e�;*� yT'�y�<q~�T��n������r�i���kL[+f�g�MiMg�8��FyY^� ph� ���N��/�j�n	�r�6�W���"�I3o�y��ī�,�b.���_0�8���Ѭ�tXe; 1*��~�qU����zFՆ���w��21w������(-����_���.�(D#/���'㔕�Hpk&I��Ż�OZ�_����p���"n��X��Y1�,N�d�oV����[D��4/W�wO#.�E�3��Ŷ�pо@H`G	�EUqF�|�Uf�_5y�ޗ��^���R��ė�U;���������P��S�o��U�Y���Tl	�|S�_�A_����Ќ)�a��)sZ^2�:��ܽeq�X��#`|{M�хq��e�c���6xVoh>֖�3�Ti^ �Q�9s��$7Lc��I�Eq���t ���� F�C��������y7�/fXJ� ��{i+:�P���Rd@��vPz�gy�8��x{Bw}%�Ɠ�[Vv����}��hg�N�g.�1eN�\c4��s�.���<�����Ί4���0�0v'R��Odl��A����.�V���l��HD{cѲ-�� c�i�@�jLtX4'	�����
O>�w�����j�&�:{�}"��6�0�z�@G��M�u���o�s;6$���o�ȋf��2�~�U{�K}�h��_W i�$�;�X]�U�s�2���p"&�����f���A��Ot�'}��
����qjc
 -sAУQ0�#)2'���7�u������΀O��%~J�Q��X�ţD�D��x�<|�6�b���៥R)v�c}���{�����=>�IM���ql���hY��X
���U��`?>?D��yDH�m 	䥕7���Hf��*��/2�x<�d�-g	��Û����Q�0���q�^&���[�߁�¥���Z�b��+�}H�e�vuhS,�]�o�����G��X��nR&h�����8�A���ڱ@m\,C���N��>���@ю��;����M�����$AӀ� #�h�|��*��P������|l���*���j'�L��1�����w/�w�[���Jt���\�Le�4��:D���Y�x�XZ��\�&�o����D�q�Gb=`'�+S���B4���|�]�h��p`�뇛�G�W~�Zqy� v���8@��nX�:'�$� P<<0��d_�3M+��L���@�	3%?����D����|�V�I�&�0�q��a���D��#P*��(�V�<�G}-HV�2��b��v�c2�[�1cY{?
��'�)�pА5���x:�.n����#��~iU�E 'C�ge�)A�zF�!$&Lٷ7�w;!�y$'�8�J�
���6'w��pӕ�?� nq���'�V��	��<�sh_-���3-tIhu��(E��JL��'+�N���K^a!��^��$�<���������o� 5��������5M���q1,�zl�s Y�sAJR;I4F'5e�'<�,��FA�܎G֨�Ѳ��ؒ,��?���e����~>�ul�}� +�C~��7)_Ai��
]"���'Y�T뀷Y��b��(N|ɥqT�7���|��~�=kzP�7�� ��!>�Շ���Y����4�FEL�c�	7��⑞�I��:��0����My���Y���$�z���H����Q������ɫ��!Ȧ*Y MW���Ǒ"`{�e �BA��#%::��B7��ҩkmǿ�7��<y�E�Ȱ�[�?�����#��k#�(1k㑓0fd�YB����u]eݔ\�Y��R�N�Z ���⤄��_���P���{M��v��O����ε,�&k�Z�+g�f��{��QQ�ŵc���7l@�b�����5�d�x��܉�W��kwl�cE���~��o/��{���?��:<?77��}� S*u���8���(ZȄ���g���,Ќ��Fή�.�6*�gG��g��O|���CA��O�� ���xlR }�!��v$��Y�����z��v�W���.���[x+|�}����7
�vl��}���G3���w'p��(N���Ӣb�e1���og�w��}m�ͫ)����%��/B�����vl\�~�5�w�";�I>M	���we�O>=�zh�Іc����`�� �u�10��N���7��E�^؈�p�7���{�"������v|�'�g����J81�Ð>)q[c����ԪzYOz
&��]��x��9��~�����R�v�?a)ק�Y�m�H���m��X3[���-�N��۞����+�훍�yL��h�K��9���{����T�\��bڏ�h.q|k�c�F���,*�g��~Z�#|oۑ2O'?c��t�����1��,=AnH���#N�p*J��?�*�����M��UeZ�Zڱ���~� ���!d�t]�i^gT��勺�Ů5���<w�Y˅/J��=`jz<����F(�
���c�%��/��j�MK��cЗ��SC���9���h�\N;;e�|	�OO�!���R�։����n~n�Z��ï��ۛeg���v]��a�(������$ƒ&QU9���¾�.W4��C���n�--�����N�E5���/qÉ����ͷz!��E7����n�4���r��"�Rϯ[f�Oͼw<�x.r���x3zwq�-@+�Oh�����Ex�g��~3��/dn]�g������~���R�bo������Y��}��wE�����f^G_��P&��R�B�Gͮ����\�/Óp9?Q?��m4ק��xd[�m��k�fǟE`�Yf�E`�Yf�E`�Yf�E`�Yf�E`�cA��f$8&��6    IEND�B`�
```

### `src/flows/fno/commodities/assets/gold-petal.png`

```tsx
�PNG

   IHDR   `   `   �w8  ciCCPkCGColorSpaceDisplayP3  (�}��K�PƿV��u2�C��
�8�DqU�ꔾ����G�"7�����
�n�::8�������y/��"z��~|��8 9npn��;�[\�+��-%��� �񜮯J��?��>��N�Y�������1����]H�����%����qK���r��g�X �&VXͨ�������`�r���l��9�X�<p�0Є�?�����]r7�R��|�ɑ"'���p�0�XC�R�w��w�O���'`�#�����p6G'k���<02\�����G��V��S`���P϶W�j���<0�(��$�:�-!>���S�p�|�b��[   cICP n��   8eXIfMM *    �i            �       `�       `    ��}t  YiTXtXML:com.adobe.xmp     <x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="XMP Core 6.0.0">
   <rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
      <rdf:Description rdf:about=""
            xmlns:xmp="http://ns.adobe.com/xap/1.0/">
         <xmp:CreatorTool>Figma</xmp:CreatorTool>
      </rdf:Description>
   </rdf:RDF>
</x:xmpmeta>
�\�  'UIDATx�	�eYu�׹ÛǪ�j���kl�ih�q��"�`�@�l� 14�&�J9Nl'���8rp"�1 �b�-'6M a���������U�y���|�z��(R��^(�U�{ϰ���Z�_k��ϭ���&7���Mn"p���D�&7������G�C/��ܳmǡ�����E�Ѩ-]��r���?������'b��o?p���ū���zEs�m/ر�Ec�c�je�������G.^8��_=�����%>�ַ���,�|��c�����:o���zx�{��K�U��KS�Y\�Zώ��r[�x�����&f�O,�o��#1y�
�B ���qwW3������ۢܵ��zW�O��v'ZK3�E�n�[�����?�P{����/~�s ~�o���(�ƍب�M:}Sg�u��Z<�Ռ�%ʑ��K�@ �c�":e�M_���V{�h��N�z���������7��KU�7Ҿ~#5�m�Wo��K��Ok�x��]ͮh߲-���F�a�P����ۢѳ5�ň�ًqe�g�D�?ێ�ɨ]�������{z��{����}�z�3n��7���;cO����o�G�k��0���#6���cϊ�ێ淢�>�'bia1�q����Б�TF����M������pC��~�q{_'~m�p�ĎQkԢ�ځEl۳/z6�ѿ;P}�>KS����), b���̹�+av���x�]�b`d����'O��?����n$u����������������6����W����k��{8�!���¹h-�	�A� |q,�jg���>/Dq��Ų{xc__o��C�c��_�r��?��xAm)~m�H�覱(�\��D�o���;�7݅��B,o���`6:�P�K�wN�����8w1����������+���Qn|�=�B�K�::/���g� w�زsst�~�V�Aep[KW"&QyA��^r��I��\�l�xf�Vv�;#۷����!��\w|��q��B�RO����OF1o"��֏ý�7|?@�lg��ekY�ۄ���`���1^�n��&���̥�TqGlm�薁x�^7�ﻮ��{cWk!~q�7^:�95�63�F(~��z�n��j~��ľ��]p�;�6V O����~���n�0jl�S8��)�;ch��������}A<uc��	&����a ^�g��0�D��߲���n���@�z|�t�s碽8K��	A�v�#,gǍ��S�S_c��qhWY+�r��S��zL�}q|�����-��57�8�a0~���O�DAYl��s;�o�������_�_��q&�7�����
�hIE����5HM0T<��B�}��7<Z6�k=��x�w]_藟~�-�#Gbd��������E"�'� |���]��r ���"z�A���kK� �Ӛ���9����j���EF��c��&7�h�h_��{7"�V������F��>������W��|���K����߶�`�	�G`���[#���ÛvFc��|.������|�Ks�8� :P�2肬���-���Dz�[�
�y��8��c����Z٨T񺃛�Ǹ��%���� j#�Z+ޱes��%�_H8�ش9bd|$zV4��IԐ���)���)���	����'�pJ*2���K+�K��ňo�����(Ʒt�X�H����#��!_3|�g⮥�x/�����E��cQ;�c+���dc#z�wA;�~Ӑ�XR�lv�3�Eb}4�tp� ��fw�|@^B �����C�~��<�p}��G:]���׻{	hg��$T��!��+���k"�O���Z����=x[�!4,��2@#�����O�M�oJ94��ȧ� p��b+gB�T�WS��.2T㘠@
�Aet���� ;��QL�'����*�u�w^��W] 9=����f��w8����x��QL�e?,3����$e�"4)y���-,�=agg�bF>����2�ÄX����#�ru="G�&h|� ;Ƶ%m��ԕ���}���y��T������xyO�ܺ��ٶ�7�>�)Α�o ���n�p�oӲ����-ׄ[��� �IR�g�x@��1>�R Ҍ���HA��h�!4�U�K��o�Οc��\yl_љ��ۆ���{׵OS\U��?��]����;��z�@9=U�SG�!��~����A�Y��X�j@V��δ�r��N�>x.����g&]����ea�e����ԣ?P@ާ��/��&�)&g�l��Ƕ�{����]�r��o	9��V4������Fq����E�� }�F ݽ�htD<5���_.ٴ <m�5t���������ɷ?Z�N���}7��Y�H]������<^��$M��[~�9���j�P�_)W�AL~���oٰ������S3q�$=0�߀�Uݽ�Q']�0��6l�%j�%���(̀�S�P ؙ/U	���������{�@�b�-7i�q������ }��}�:��_A�*~�*���.���h��݇;eY/�?Δ!xJj��������U�t��Z�����/-�g$�N��Q�NF9�*��~ ���/��(��������h�B�ɟŨ]��3^��4�/|�mq�U����] ��T�����E[w�:c��j�?Σ�h���[/�7��k�:<��L�����^ _"�6�.հB�i�W����5�
E�~K^�p��
 �O!�v8nڂ�� L��<�4�|��-��g�/�r���� ⡸yS_ѷ���rfr�8q�c����.��9 �� ��\�,��u�fH9\fc ���t�}��|:�k�����s������MO-��~�����s�	!���u��9��QiUֵ�����8�;��.G{jg���y��n�" )H�ov����C�DQ�+���f�o�2�?�7N� Mt�j��V�cS���c/����ˀ<qe��Q��u�0�'��c�����@O����Ƌ��j�u��F���{��������/N��,xvz������]��R����D����%��:��8�I��V��� 	�[����r�ZC�R�5�>�-��i��s���4t��ڶ��+�/�k�&��b��}��xϧ�[����u�������;w+{�ǋs'&R���W�u�F-��ĥ�e����$�_r������ �R�����d[j��wS�j���ǹ��UI�#��R�Q�#h�Q{w3� ��e�������x�����׿>0��/�&��z<o�+^52�,��?�W��2���y�`�
��FZ4S�:[S͋���Z������)�E�/t�'5���UܞcYl���V��W��S��_���S��7���5b�N�@[���_@P�9P���/Y���^퇎D�g��-[l�����±SqQ�s:�6�̢@1;��h�x2�D%�.�(�$�d%\)��I1|O��K/�������|f�8�"�LMtq��9�ƨ�Ğ�m�q�@�n����]�3!��,�;?�L^6f�Ф���^�������fsî�Ȋ�3'�S���R�#RSR�2|��\&sf�@�����}�R�EZP��\��4�
��{R�
�+0?+�LI�\c;�Q�j��3h�μo�;v7��!��%�-N����e7T�sS�8�*�u+k��#Q(�Gi�C㽝F��b��ɸ���4�����  
�V�Ǒf.�XC�(��?�f����f�tW���*xϫ�B� �k=�qm��_A8�f��{�گ/�6�M.jp�-��֮��v&�����(���'LF7���|`}vk���֏����e?�r1.?��͚�>����g�]�_�o �n�[��TTBA�������f��@	�*mw�hG-�*,
F���LQx��dY��{�>Ƚ�f6c�C����|Ԉ�������8�%�8X@<qO�w�|�J�kޭ�"���u8���E����܅ch?�M�S�0w����W4��@e��o:W���|똆�`	�RR{�U$���� 
��I7j==R`��*.�
�����ǹ�g舉�	wYmQ���{;�����{�(��gs �K�^�����<��$���C�?ԬŶ�Mc��Y�]9�d�`�:[�V!�O�c6�NΧ4w R��:.AY:(Q�R�Q���+�I��j�/���`dd�����G��½�T8
K���(.�Bj{�"Tt��FchO�o�Ca3T$E=Œ$r���g��5�5	��O�Ρ�x���<�Y�<��/���si�t^*2����覃�z������\Y��J������ET�-y^0}N���B�2*-Wֶ����R �K���(.�[`��in����r�������f�<c�=�	r�k/4a��T���z�P��ށ�̅�b�;U���a�2b߀�:�i4o p�
��	Z��� x�h3�?Z����Y�-K��W0
��j�B���]��ֱG��
���ר��x���V� ����C[wľ}�+�� �8�0�����La�Z ��4�Ytx�g��,j���Ź4gt�������\j~�k�zȎvCGZoa�Vj� s$�-�"u�jvZ
;�T ҎT��k�hG������ �<�|�_���z�F���Ē��'��t�����3��I*���(�-,2x!5��جU���B�Øc�k����*'/������v\ln�&��ن`�	'�+��d`M6h��84X�N�^`��3?;��y��"���J(���e �s
�I��$���\K"��o�L�獣�F��س���&���8)c�q��?6RÚʪ0Ј:�[m�b����l1�$%P� �Q��ha���R����D��O� $-t�X�s�u�vܯ�vj���Gh5_�M�X��Y�T�t��=.����ZF�<�RhwPv�}�i��t{�4�E���ؾ�7����Z�Ϟ�)�w�qG>dh��
/K�~n�9��,fY]�D���A3�F@
��k�ݬrn�����^9��CA���g-´� Ѩ�j���$�H'�9lZ����9_Y���g��ZWE=��~O+X�W��f��Csg9Ax5�3�7o�];"ƙJ��K�:�ul��<��U��}�p���!��+˯
) �w3������ ��\�bh=��@0ר�Z�ʌ�13q� �i+�s����t�ȹ����!h�/����W�*_U	�gg����=�9�2�Y���^����`R���&��H�O�(� 8Bv�|����j� ���P�&��k�	=�i�*J����Pp�c�Y?�{��bA�%�Ky�(eyc�k��S��"\�Ui���+$zЅ�V>��s����9�a�Lrp��b3�N�@�`��|V�f�W�����t��ٴ�&3m��c���Z�`�V@;��.����Nr}��X�}�H��!�Z�:�
j%�M�y�y�=���v�d�����+Ѝ������!
2D}s���Q�Be(�$,��jn����q�D�H@ǋ��d��ՕU�|L�Mo�\Ab��ς������&�R��~;9��$<=�2�����
 +�^�/�˴���)3���9)��
���V�,��=��>�3?�l�֤ �-�Y�0��<�<N�mt���`���^��9���j0�^2k� �6�8 h���.�ٞ*���_T^E1P��kE/4� ����j���}�Q�Ҕ�g��Gi�϶#�{�x�~�{��g��Z���+ �S��YDH9����v�+�Fz�A��q
�a"�����Z he��+d��RM�W��ў�3䪝���S�F ���L�E :i^�(x��X��#�\���������,R���*�3sP<N��� $����nڐV��QORuim�����#��ptl Cz*&.���
�8X/��X��`!.�6� ���L�$v��*��eN��V��s����4!�d��;����N�Yqӑ��u�rb�d�'DI�$�Qi��$�k}
��r2��Q����P�F�H�*�u�L:f�0�y-ܚ@i�x��X�_��FW���\�*�����2M���Ɉ[�S�fs�0)�@���7�j�#Oj����X@71޵��3�&r �<}���&\۩U����uoTQNFC\�4�����ye�_M�0�tՆJ��he����|1��Q�����{��;���׉�fb6���e�Lf	����:�шHK���~�9�&�]*?茽�LdA8Rk������x^+3�0�n-A-Oǫ xvFET��j���'�+�H�dk��y�%��.SD�Ap���<���8��CA0�Z�u��/���w���BsVWX5>K[��#L���t�ѤM��b,m
F��$q5�M�I���=Fo���b�6�9.(yGL�8���:����n�ɢK��@��A?Z�	,'�����S����c��<�׸xK�g0�(yIķ����S
^��&;���j��N�^���β��A-�a�4b��F�hT�!�(QUN9���S"K��B$�����w2+�
�C�(%@
�cr��\v2���f ��H@���ɢ�f�,cu3� :��
��3�ZqV��3Z��GI�].S,�a����iL����H��\uY� X:��?���o���~:l"��E���[�U��&�z/���%�\^�J�_5*�PJ6ԫ���6��+;����4]��-��u�
���	�����f�O�\T�Tx��$Ug䨚��2����i��}����!e�d<yt*�<�s8�����v�,c�EVU�<�+�EW�ex����Np�E R� �,�̄Knh[��̜3mυXv���i�+$��SJT[ޯ��9j�i�x]���.�͕D�R����A��	�c0�w+ y�з���:"�u�*F0 ���>�>��z�Xy���DZ���̪˪�Y��=:y�Ϊ��qN����h��X���gϠ�l,;�$�c,��Z���.T��l.��1����0�@��D|ٯ@�ڢT�3S�l��}�~	s�� }E ��ᦎ&���\郖�Qf�,]��1{�x�sq�A�
`�[�����@��)HD����s���Նj�K�{	���z���Ǹ�dt����o��r�4�!�2.�|#�&v9�`sJ!HC�H��������ZCS�&iP_j0�*���x4�w���P�&��*��bQ�SA\a���(��"�zo�_DX�G�#Y	W���I ���1�ŗД���a��7�j���좣TR;i��b:��'q���0G~%3�"�t�5\�^8��l�^a�	v��L�ARr3���}����Q�^ �@�~�Q�̾��Z�`���uu��%�w&�cª`�[y�J��M����c����ʚ�Y-��x ���v=���b� ��H%�=�bh�h�X��[���U��Z�gh�;�c�/���
B���*u��9)CAX��P��jw�Eu�6G���ܙ����D?3����9�S�9���Q���س�~P���T�&���q��ʚ0s!����}]��nl�S�_�G!�(��@ �~b���C�O2 :���m�o�L-��	�um�_тZot�P��}\}��>��<})�_Vvr1]mx��=����)��	�2.�e@?z<��0�5�����	��*v��7�||�?��f�������x-���iX�a}���U��j�����K%o���+%��U@j�Q�S��Ҫ�F���TR���Z���s��x�VaK��/:��!�ͅ9�s<���%V�Yz�U�3q�T�߉��c M ��Y�A�K���SB'/1K�4�X}��Q���t��5 ������,?�z gܰ:e�B�tn ��G��+��i g�t�jpF}�g�5
+�dP@����d�T X�B�F|�NCb5�X�ď�0�N��:W��gyY�G�x�Q��7��7��q.�\*�%��8��sW�����]����Z˺��_����">�x%��@��I�%j��@��sBE�
���,L^�0�X�G�7����<�I=����HK�d��J6KJRxrw��h1�b�C_r-?�֟>�,0��mi�d��19��S���,Q�s���|�l�g��o;pY{Y،������0T�o ��� �>��gv΢�4<�HЃ ��.��U�)0@��!#��TN�%���@�FK�KM|�V����wW�9`���F�d}Z��Ti|KF%���8Ϋ�Z��3���3Ca�O�Q�S�{2:/�O1@9��� Щ~�p�}�́���� T�ݛ���k�#�����L�{_�֤����p���	�[�,%I�b��.t�Z+Ӻ���y�r�X	'��lJ�®/�{s��w�p�ηB}�`��xL?go�F��A�6�� ʳ�Y�����
��I��)���9Q��)$7>�
��*��%).��H9����7��~�+
�g��C��&�|p�"��t���|��q?�[����U_"�z�-1�ڿ�/�˝w������(�v����k���)��.�ؕP�G��~��Y`aI%��K9UԔ�# �k}*��ku��}X��c	��������Nd�n��u����M��zA<���{>&�@d �B��=-�<�l.c� ��������b��,P:�J�l�ٺs�͍ґ��ޢv�*�JZC

D�S���b�OB�>�q�7׌��/����j ������!"Z���d?���@"� `.�U.�M���
C�V�A��9�J�\Y� ;�(�j��Ko�ҧm崥AϬ*Z� *��~7^�.Y#�ѱ"�)����/�}ԛ��?<��o<��<;��ˎ������~:���T������#NW)V��� @4�.�� K5��+����{�>���}#!���Μ�c�Ǣ��	DJX���̪��}����+���3�����H,����:��㟻��()��!&��	��瀌��v�Nr^�b��{�UAXYВ�����y{�`�GG�����q��j���}-������g?���s��j�
�VKG�8|v_<�H�0<�5;0h��V��XU���w����r��^���-�&+'����=�y׎�e�	��5��I3VA�Yr��,�ar=�+������]����@�~����>���#�en�&�[H��i�7՜��F-U{M�uSx�� �}�����>�W�K;՚O��I#7<p����u��#���F��g�O���]T�kZ����Y�7�ށO8�3%*	�
��\�S��GAU{ͬ�O �NU
1�L�X��l��h�9�����}��W����`����~�_{��O3�z�@���ct�x���NF��~l��L���؍@
s9����R�W,ᙚ.�'���p� �r�����,��
ǳ �O�Ƿ��g�����`��3���u@տ�-�_y$���P_p��|�o��l�X�Ά2C'o�e� ����{�M�$�KW|^�}_E�� m[����/,���翽>�M��.�U Ukğ~;��L_	o��~6B�sِ�H
B��0���6��~�����ב����,�	OcI���g�:���Α#�Ë�-�zOn�����~'�/d��n@>@7A��_����.���W0�Y�x�s�\�`O ��w��<��8�|�s��s���~��_��.�-8�=h�^��=຅σPH��E��Y��,b�61C�.bE������c����O��n�rC���:��h|�t�p�S�DB5ި�>�ۮ�i�u�K��e$������&7���Mn"p���D������b1q��6�    IEND�B`�
```

### `src/flows/fno/commodities/assets/gold-ten.png`

```tsx
�PNG

   IHDR   `   `   �w8  ciCCPkCGColorSpaceDisplayP3  (�}��K�PƿV��u2�C��
�8�DqU�ꔾ����G�"7�����
�n�::8�������y/��"z��~|��8 9npn��;�[\�+��-%��� �񜮯J��?��>��N�Y�������1����]H�����%����qK���r��g�X �&VXͨ�������`�r���l��9�X�<p�0Є�?�����]r7�R��|�ɑ"'���p�0�XC�R�w��w�O���'`�#�����p6G'k���<02\�����G��V��S`���P϶W�j���<0�(��$�:�-!>���S�p�|�b��[   cICP n��   8eXIfMM *    �i            �       `�       `    ��}t  YiTXtXML:com.adobe.xmp     <x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="XMP Core 6.0.0">
   <rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
      <rdf:Description rdf:about=""
            xmlns:xmp="http://ns.adobe.com/xap/1.0/">
         <xmp:CreatorTool>Figma</xmp:CreatorTool>
      </rdf:Description>
   </rdf:RDF>
</x:xmpmeta>
�\�  . IDATx�	���U��}�ݷξhV�b�$k-�4�%Y���`!c��*RHU*5!aI%�JƆ;l�H ؈�Jٖ0�v;��fy�{3o���ν�4I����g���u�>��?�O/_ߋ��.!p	�K\B�����%.!�#Py�K|�+?Mq�u�ë���-l�5q��ol���dk�d�hu�����h�L�[�Z��斈��j��F8�������Rmj�T��jS[��T�u��*s�B���R���5U��45��W�ZZ�+�����n��^͙M��
��G�aμ%�mm���e���M�Q	��J��V�l�M�Wk��Zm��Q�&�kSM-��ZsԢ�F�+���
y�*���@6M�VЪT�W���+͕�昚��SƓ�MM�M������Zuˡm�~�?|i��/9&g���{"���T̛7/>����Z|�[Ee,b�8��F��1E8A~���}�`"��\k4AZ3Bg�2L9p������q�'!��~g:����9sc����mO��ԋ����$��kZ������V����l����l��E{����1��q@�{]3 ��Ĕ!@�� IG�T����5�&�+��k)Hd� �5��-ȍPz�HL�z�t_�v�n�6O�56q������'(Ӌ�^Wl�M��b��T<Tm�FUF�z��R�����O� ����](��_���y��\ׁ���^����C�W�g5�J�I� k���S��,���Gcւy�i��ᗦN_qo<���Y��*�#���t�ae���E�������z�G�G{5�/�K���XV0ӈf|�^�S�p	��`���z�$�Ԛ4Y��f�i�rO�i�R��Xq�[���w�%�g�3�l���~���\�$�86�ÒԚ���E(]��e��Ɯ���
`��Gerp 6�U��^ �����I��"�/�8��NqE�JO�P>�)��J���<2����8���Ю�����ػ�m|I�3�^7����1�_��bz����I��� Y]���"�^6?f���2&�GOͶ���k�2N( �Ҕ0԰�SS#�h����b�A��nWq@��Wfá:�5Q0�k������14x:��>���]C�~�7��Rgʩ6���Gbz�s�Qm��>-�i�}t�s�x����1<��I��hi���[ź���=wН���`Ήa�`L��c��b�|l�B[�1���8�#��/���xBz��O�gb|����O�[&��5�-�΋��X���=��on��L���:7�MwЖ3���J�-(�~���+c��?�_x4,]
p���]1:2c�L���@��WLM6��s?�dG��@ɑ`cL41��a��/e�X>�ET�_qS'��O���ޓQ��������_l����mf
3�.�	���ceg{|e����oG�4PP�����O�@�!:�N��_B�>3���:����(s�MB絖+� �ȧ�OߠSX�/��)0�;�.D�X-�����ι�p����e΄��=`���Is�VC�[5�4�6�|ƙ�+��j������5+�{�K��Z�b��N/P��4&|�5J���5%�9���qc�s�Kz^�2�Q�(Bt��*��U���uv!l�?�%�����F���{7�s훫<�@��v���/���/ō4�+���1~V��jf}Wưw��G����M���-��c�̶�'���m*�;H1�jϐ�^mh]Zہ�5!�	��
Fi����^���e]H�5�*����"����Ǟp�;W�5�����,d���q=Dۛ�g��+�\ �-u�ǖ3�ekWc���T��l�0X��ŷ7G�����͵AH'�IQ"�&�� �YH彦��Ɣq U�/���b���LO�4��`���;~�,�/�ص?b�#N2Yؽ�g��^���~��݌��.� �>/�F�>�Uk[G��Q9�ѸΎJ����qx�Shy-��9'�hpws�䇪�����T̈�X�q����	u:n�y,_�~��R.�<	�v�)�"�z_u�i���o���_��;?�kg=����̻������@��bWr���ƺ	�R��\y�z"���!LJS��xꥈ�n����0[BlC4j�ZLU�WW��Mo�w��k�t���>��e��^F
�и�߸6Z��u���Y�̡W16��1�f��E�S/�Ѽc��Oſ���<�T���ܸρ����������MO�<_C'��a6D��r���Z���z�$8j�����9��fE�R˹W(�ܣn�l=�j�.f� � �~VzT
�L�-d&�O/�b��ط��rzh�G6��[�Ir!n������h?ˀ�)���D�]�Aсq�7ĩ!V��ǘ���Sc����w�;+Nc��hf�`
PM_�/t����Q(Ӡ7��r���@��Q�=T��hi�ڿs/+w�S#��o����T��弃���x�6�t�[��&PDj�
vͮ�eW��>�͍��3��beS��Nu9em W@2@C5���X"�+�� �g(�x.J^C�Wd���x�p���^p���,�O��Bq����������Q|��c��S�V�u\i��b�l��k6��2A�������xaG���}'��]G����}���������v"�Lf:$n��@/]IK��t�4�H3F��GeP���8���W�o�>���ͤ *�:�۫�SS��{�[T^g�;�"��'v?<�8|(v�EÖw��ŧ�b���p{B�0��l�>`��P��N"n���β3K�Gz/�é�.t��,K�f0��i�n�N�~���Z�H��͘ ��b=���O{o��j����˯�3�����<=G3��Ŧ�w�����dD� a�O5j��j��HM$T�u�������.�K9$�^�e@w"1�U23W�Ǐ��О�7�~�{��s.��Q�s��2��{��-��Rѥ��ڟ�V�1�͖�e7��]_�V����M�ʪ���1#��W��4a .R��'��7������0�H\:�{����-v����|3�>�W�8���x�c'HG��M}�G��~�6�a~���]��rC�m�PI������8}�������Ў���s����T?^�[���yV�<2��Y�V0tb%���x¼�����}�Г�{Iy��)���(c�I��HK�gF\�c(mc�3;{�S�cG'��S����Wm���c.�}��ԧ5~��0D5Ak�A�d����h~t.�*Fz�2BWc�DO�׮�:'r�Y�L�i� �_Sz� dZ���zA�x��t�K�y�t�t�\Z͌N��5���I�Ky^�~pJꌨ�5K3���P;���<6�~�]:����`���r�e �j�i����+׿;�l��G��}10��l�w�uV�̵�f���a� �� ͆[�`D�=���|�)�b�r"�P�崉J��OA�G>)pB�tC��p�����74wAT�=�~��D�Muʳ�� ��/�l*�q4uTS��F�m����K�uq�o?����ƶ���:7���@N%X)0xL��'(�M�m3N/ �&
Z��rSzu�
x
�������%B�e�m!��"�\E#���^�t[�{�������!��Y� �	?B%��Т��( ^[q���{y�����pQ۹%���[�7u� �~��FXs]́�H�ѥɀ��
(�S�$�ǰ�˫�3o�B"ײ䡗��f&��#���&C/��v`��I�c�0��������?���7��u�����s�Ů����-�v�
����Qم+VES���v����8�3�wF�x�N��#x&k#ɓ�lc � fψ/��'XЧ3�8�<4#�?E�Kz���Ac^]T֍t�<�	K3  �Z&Fk��ţ��-�}Ȭ��,~�[  �c����v�C�B�������{�{�s��y<f�'Y�w����7����ᬩ�s�-���d��^�P�'�`k?
8���җkm����J�+&��"��y�oZ���m�mt��2���L��֡8���g��u�:�sw���X���89��X��4Ƚi�\���jj�)��;���S���n�uN�������myi�=�nn#xӀ��a�$�ea�<H�|��P��P�A��s�9������=ua�V��Y[
���X�4:ye	���Iʠ݃C���҉+���^�������UxH�S~�� ���QI���\2�lA���>�b{۱)w����n�f*�I���l?�Ϙ���ܙI�<y��m�#��_�,���|��}h���H���IG�+���r�|u]q|dYfb���t�(��f���v�Ӯ�3N�vW�^?�������]q����_58g�����T�G���Y��><��veڕ ^~��qz��ɾ�N�Ʒ��#N��<j�����(��4T`IJ�
�l��N��=H!�g�hI�{�D������k,Ҍ�%�� ��>Y�t��j����3L�8
x�|#�m�S�Y�g��>�b���a����W��^�`�����M��?���_�	�Y��0�T�dX�����f��ؠ�K#Z��p[�������=z$��9mq�J��O����4!�BԾbβ�SX'3�=�y�" u���:�nQ{Jb�U�9&����c�D�O�g��-�Zn{����t�מ���	�e�FW�.��L���q�r��fF�sKo��8��g���ՙ�5~�I +��}�s�u"��z%2�":�x�572���<䓮��Z<�-�ow�5��lZOm"�]j)�q��q����"��8���zh~\��A�<��<���GO;,Y�׮�7^�K �c-����C�u�PfQ������^����������[����(���� ��YT�c<K�t��Άj���=�-.��-qb��<x�Gc�~4lMW,�Y�`��_���6��9k�x���Y�y��t)O:�Rxb� �S6��E�8�I�'�h�<�s�]�b�[/�vzg3��#�7���@K(���[Zᗕl�e]U.n���z� 8M���sE{��WN�����𽺳ܳr�^L�; �i����h� l蚛��'O3`�G��c��؋�sW�Ѓ��t9�ڥu6B��Ayt-�&a��:�	8��:��抓e+�\��{/�_v-�3���fa
�㱯�-���pܐ���!�]���$%��"�1�4Y
�����|�,J�"X��%��0�C��޼la���Uپ����bn��~(;P�<\e�`����s����NV�_��t?�������c^�i�11=�P����~�k&l�����h�8�b�Ra�~���D�Q.Q9�
��/���������=�����L�ꇼRp��8 O����T(��x�Pt
A!+�,�P�1!�m���!T�_�پi�ulx�_a���+�������tɷX^�z�T�o��Ͱ_u���ľm��9�rf^�yOSܱa	��i'�*.���S��9���	�ǟ�`��w�r�sc�P,Zm-��u0w����)�'���l�cG�GT��H�м ��2� ji�aٻ=)!��Df۽'_6����κ<�w�H]�G�����ɛߴa�>��J��^���O�b�f~�6���zw��	^VF-Z� 欸)�w�-�$�:p4��f1�jA,���pN��m�6F`���'5��p|��8݆���5��8��+���-�=ӽ�9�����5�����@���a�����E�U"���g��KM�nɝҼ�6sa�y��3��sY�.��͙���Ow�4��UX|gH1��8��.���b�J�����{���7�-z����[�D��h�{3!m�y�l�1��7��@��P������>:���s��!.��	�T��w���e%�Ga����/�V�M�.��@�'ao�Ij�,4i,��yLw�inW�.]�uL�����zEG�Ww�n^�"�v�4�baj��߆:[X�v)��=����1�Ö�wb6���f������[`深gx�$��e�*�r��뾵yj�{��\c�f��\�`^F�89�������G�]�W��ո3�
!�u1�&禎�h��k�ӕ��K���:�`��.kWq|==�xW�S��~�ʮ!�WN|�}���$6�gXh�a���������ݿ��*�ls����8��`�Of*�;�������v\kCS��/�Ɯ]��N��Z�hN�铘�^^L�6/�k] �ᚆfR�-.N�eK'��0������H2ȴ���6V9-�ĂEm1�֮ZÃ�R������ (���y��,�VDl��ȾA0H�����D�«�Į?�`U5���fh6�:;:�����]7��^���iC����c8�?'�M`�A"�}�����Ɂ�
��S��i�0�:�t��|ց�D�i
���@+O�4�αD��<u$*DiHN!yo�pL����Ǧ���
�9l�T�#f{%g�Wu����>��>	 ܾ���wp>f%�z�Ӽշ���lT9�<pxo�����_�[���!+�7���@$�4,���a#�bg�^����ը��4�zן'@�Ndr@E��S�K I��M�z�4�sm�I2.�6��｡��ېi�n��a�w��',�I��|��U�+���G����o��g_�����Y-~}�[�8��
4-�A��8�ң�9w�z���,|�jgQ�����~*h7u /�{ﵡ��	8uL�hT�fzN�{� Zf`
���7�F�4�.m4хV��K�a<	�9���*�fU;�u!:�H�O
�!��G"���.Llg�ŴE��K���%�^��zE��cbh<�~�/&���%:�g��
��%���佮����Ϲt/�͵W���6Q���oC��6L�O�xoÊ�2ܦ���PS�r���t6�+�ءS�]hɄ�41�W���r�����!T ��͘t�o�[��*���@Iw�pǽ;�+r����8P�z�_��]�x�%�t��>$<��W�_q������s��=�/;���� h�TJ��Ѹ�VވF�R�l8�"eZ�{�q�i��M!IC�s�X�N��;:�Sϕ�ʐc�2���4����|L4��NT�B�t�W�f��L3����cb�.�0m,J��L��X�Z��v�~,ј/ eǷ�6�6?�3⯾�9�?�w���Ѩb�Ls�w��Tn���n'�4�vؘRadD�A6F��Τ���ƛM�^�4#n�	�/��� ��X'@iʈO!�����'Y(�u��x���褐�^�Tz���4���6��M�������̻~)��\���"�;W�Kh�&l5TVO�����#ݼ�^c����t(++w*W�'�/�K"7�#3Ҳ�3���+`'M�~�<��K�s]�t���aR�Ng(/����Q`���BsDXS�F����=����������o��;��鬆���״���;+|�뱟�vM�0�M+5�u�a�^6�Ʈ�hj���������V^_4�ym��
�!��k�3�AW��J��Gf�3��8y���,�`�\�e;�[/�#�x���f>ߤ����� _]��*��ey	0�
���,�eg9����龭��k���#>��_8��n�� ,���a�Cp�5�O=_o�/bО�|P�ZH��L'���'�����-(�t#�<�4�'�v����fY�.�|�ՂN�[�<�� 6��U!i&5�;v#$̖6�U(�e�g	��i^��S@���ٱD
ۿ��H�&���V��򷺇�O_�~�+{�Y�͇���U���I��%�>��d�sRM��:�J��E͂4V6g<��r0�Z�żܟ�+L��n?��^���m����e9`����X��,e'�b����:�a���g]yF�~��:/"�F��-.����Hh��_����d��<����z|���na���FVOgq�G��6(�%�S?����g�L*$`�ׅP4:Z�b��E��Z�L�ْX��2��֙��3�Di�1��S�j$�}����e�Lɺ�]�15l��R0
�i��<���)��G7�s#N�Y�)=�6��9���x�E˗�3t�?���ݯ�9k�'O�6��@�vZ9.�o��F����C|��8#����J���65S������*�q-m�tk����jw˳`Cg=��@�erd28��C�X�(�!�{�r{�J4ψ{�k��E����3���e�I�gd= e��H����qD�5����gg���� ���ϳz8mS��;ix��Y�" +��3V�����۠��ԓ�k��݈S(j��Ӷ;��xr�U 
D�,�-ǀ9������nb2OU�Y�������9�����Mϲ�G~��� �B �P�m��
���G��y��÷y���m�Ξ���شuC�9�Q+��T.A�r��7�܅�bz�U��zO�Oz"��S������L�?4�L��:�˱�Ϻ�@`���W�5;���5�P��uМ���4Vب��늽�{��-L�y��,H�0�Ne�yM=�6]���)֭s߮��[|����s�~y�� 6Ү���s�� �,M�����e/�u��>�x����e`�_v]}6�
�F�-3���@��=teO�K�׭D���C#��6���I��(��s��#J�����.ǉa�7y��VҪ�M���zʴ.�%ZƎ3����T��+�7�ˆs���ѥ%�_���u��1k��ۊ���ᠡV;���c'0�'ǅ4�Jo���r]4�{���Y��𖬀���Չ�,L0j�N~:�F���5%t�UV��옣�|�����
��ǎ���Կ���a�G9��+��������T������i.��F���lTN�w�q� {�v(��զ�#;�]od��	J9MY�0C� ꬤ;�=L1���{�su�k��z�
!�SC+P�n*����
�k}
�PZA���k|N μ�8�xl�ڛ��������'�OƟ�)����`1����T�Q+�3�6`�Q @�x��=�����yR��u ������35����N�:�ʭn˶\Cp��#�8� ��)[�Ag&�fY��gZ ֍=��g�儴m�.z��8�Y�O�����q?�- z�i
�=e�85q/6_��<�=��F/Z\_�����ks��OPҌ�Pg���� 3�x��X��{�u��ײi��0�W���$?��v�<������'k�Ǫ�R�۝� ,���>������X�0�����K��;�U���(�^F�r� k�hi�L��W����r�^�,�t]�묐8���3�!^^��5��zX7�����&&�GX9/�1fd��ূQ���	���1Jk~��+���>@/pf��4΋��)��G	i�,u 
D��ih�s/Xe�P�<��n����P�O�)˔��!I�O򕟌�#M:�ס�/=�e��Yݣ���o�� wA���x{��Ʂ'��	��
���u��2ϐ
��)y�"�4��m���u��Q��@��&���O�/�3��x�V\
��xX����Ǽ�QZ�����}8*<�>=�s��o�wA���'�< �ؠ�us,�~���Gu��^x?#7�/��g�u� kDZ����4���ڒFD�m�!	M��t���[L��ϸ�E=�W�����!j��~����l�p�����x�cW�P[-6P�u�F�@8�|�^g3ug4�g�s#�EZ�T����f���+".��&��I�\xQ�1�|�3�_LS!/1�ij��+��R�-�E�w$N��O>���U�ra��,�ѧs���L8�,��uĩ'���O�#<?����~4����H�@g���0���g|0i�.�W�&��*Aݗ2�:�9"�ԋ�k������{y�կ�7
�)ff�6���<K��]i�2�lΗ��P�slܔ�6�S47��D�O�h����� J����/�fZ��4����%�
��,���1߀������D �c����L���.�͘ ��q���ah�Rsl�B�fе�>5�q]��잊��f`�I!q�^-�smDd	uڤ'���#o�������4�+>剗�
�b˺�B �~�-l?=������)G3�ئ�_aGi���me�����̜�#Ҧ:&�O$�	�U�3�$�Х�* ���'��O��,C7�Թ��[�^�.e�Q^~��5,�Em3ʓ��9��O���3�(z�ܟ={����hQ��k�х�Y���8l)(w(����~��$�0�.�G�����y�B1��"��*��?�>��zűH�� ���KV����y�l�?�����~롛QȐ���	=�d5�.���� õAuQ�^ΒE�☖�/��� �+���Q��A����t��O1cF��F�tɗ��b��r�It������zO`g��w(>���<� �s�aF�W��CX�?`��o!$j���[�8���Q5̯�Ea��{�O�ht�h�'�7{��:�i�Ȩ']�5�����ƭ�q�a�f���)63faz�{?_�?���,�5~h�̻���^4�n�]U�B�-�+h���Ƨ\>`��]�	yv�*�	!l��%��� ̚dq���>�_��ωy��8�^e�3��M�oXW�R����8E�䃭�yL����ObO)g&Ct`�ݓ���]Wį���~�XCS+n��Ղ|��ʠ�jE�4�i�<�"@��v��n#���YD)\M�@��٣���t1���]�E��"��U0}*��`[�S�;�F!\(��KO��SsQ�M�h��+�CL��V[��B�o^˲�J4��R�)�	�1L�'�r
m�g�5�v�h���=�8ptgN�f50���ע��9���|�	_�V��C\�}v�#y*Tǀ<ŁPx����x�����Y�f��Ƕ]Tw�Aǎ���_l�'nX�	���`��K�i�Z>@��g��05��5���W�f�j�y���!`�Z���5�ߝeԜ�f^��t������7$��S��U��I�'y�Y�b��1��'��_��	��⸋. ����kt8>����0�\͇S�����Qy#��E�끥�!楻��9\wq�n����ځ9��3>���������͌��E�F���$f%��L9p�yR�^�B����Q��qҏ�R�^��t�/�fc����b�� J�1I���_���#�vzA�d���Q��k��lI%��!�K�`#���c��I4m�=�ޢs������hF���/`�k|�`�6��L���������M�I�fRp�����{���:���U ���u�H�!�2ߚ��p���5+��j�j�6?AlMG�v���"NA��\-V�	�ni���E�G�َT���v�W��~kg�||S`���p�� J��{],�;�z����]�-�1�S̞\����/� ��;� ���G��]\���Jetcںy'���5���C_~�pi����3�
?�!�bF>��?�O�p��OM������f��g�ǰH���c ����΋���2-�z��� JC�},92]��S1'F���D�K�/�����%.!p	�K�3C��Ɲ�Ud`�h    IEND�B`�
```

### `src/flows/fno/commodities/assets/gold.png`

```tsx
�PNG

   IHDR   @   @   �iq�   	pHYs  %  %IR$�  iiCCPDisplay P3  x�u��K�P�O�R�:�2�C��
vqh+E0T�S�~	m|$)RqW)�X�Yp��TpqpDݜ:)�hxޗT�"����8�s�\�P+�(閑LĤ�Ժ�{���S�f���,
��������O�YM�v�O\��.�v�S�]՟ɚ���A�����m�	�%1h)���ǂ�.�;��d���X�
j��I,�;�|��e����ޟ�W���Q�a&�PQ���ӎ?�-rW`P.�,�DI���Сa2qAꐸs�~���mm��mp�/��B8������x n�L5TG���r��	0���(�a��!w{�{��c�v��#�����+�)j�1)O>   tEXtSoftware Figma���c  �IDATx�[i�\�u���{Ϣ�5�l�f������*��؎	q0$�D�!@��@UJN*.�m�)#H������Ih!!��ьF3�;/={O�������kYBh$��[��_��~��|���\�ƥ�2�uP7n��/q(��	�cǼ)��9\�hgc�[�������� �}���x��z����+N��\ӕ�?1���qt��7�G&���p�x�J�m�o�UIL(�B�Н�J���<S�e��f��}��M6/_�8.��� 8�q�4=���YYu��AQ5�x6!�^UB�I@�\t�SMo�"����~d,�x���w����+ \{MY����w�w�P2^!�5�n�ϙ�n�M��I1�-��xAkg���[:��\�=�������}m���iN(n/��Dhџw��:�.���w��bT_�94lNT�oZho���_�*����ɟ-��:�9Td>��� �@�}v�1�Y��b���J��9� &����1_���9щW�Y�c|) �27Xw���5�;�5��y����>I��<��{~��04/T��Q��C��^�ܓ�U8�� вs�U�~616�q���n+�9�����24�>Tn4݄}��0�н32�P�eJ�Z�:�\y�r;�:����>\���_Z+~f������[�.�L4�I��3��߱j��Ϙ��>�|>y�5;�F�♨ٳ�0��\\��/�G����0T�����^�TKE�ό𸢋̮�$�)�Z����6��{]��F3������(��mGk���&Ɛ3�7`��������s��+�cBq������MƩ������p.�Kء{�ӗ�di>��"28;��0�p��$+�E/��;��08�jW��r]�+Na�Ld�x��v�+⚪�3�@�C�ꝅ�c��lGNi6�?iF$b)cӴ�7hb�M��H��:������[X�#��$���2֙�̃Y�0���,T�4Ĵ��ܺ�9h:�J1O�δ���� C��3p�d�|� w�X�P��~w}�22J�%NzٙT�D�w����A�,���]
�+KxJ)*>܊��h>܈X$��'�b�bH��p��T|o2��T�@�eU۫_h�-v��eVRYIN�����H��@c�詥�k�ھ��f�ġF�	4&�L������e|���L��ǲ�� ���w.s�`*��ľ�7ͽ��(,yI:�cZ�>!l��T�y��o>%�T�bƂ\�Ե1z�pa1o�9)I�2��rz�� #M��s��1���Y�<������p:%,夀�����e��e���BGh ]�_�L�3�7�F��|tV���Z�r�rd4�ߴ��40��ARΌ����\m8o �e�U�Q�N©L�1A�붞�1�J#%d�Sm�ˤ���(�������dI�+ꐈY�+(�����b>�a����_���jǤC������~�����C��.��r	��6��g�����Pt�8R��so!bj!jw���+栯����?U���٠X9 ��#N�,{�OƞI� ְ�j����my�G<DG���v�;�vcC��f%�-g��xW����E���q����r�o��g�%���H~,�<���A�w-�'|8���93`�*hWd��eUy˿M�E�,�x�-)�@��.�=7�%4��)��o�i���.G���(��M�o�F�$��v�t�Qx�p��0��hMO��ea����)���]]����ֵF$b�;��I�K\�I��OA)u��c��jwlF��訬���T-����cB,Ɓo���F�s|. O<��9�^<�q�.Rw��b�uI�Dq���k��2�O�:F{_!z)�ʷ N�k�9�\��A�1�g��c��E31�g݄��	����V)f���I�)�7�-vXrb��eb����!���,m_�e
.��@}3��\'�O�)3�;���� ͇�X��3�%W�b׮ɇ�gpp#�"��7ګ�E�Sd�F�ƫv<ꢣ+�.i�nyT�9R
`�����md�t�׷�RǦ���s�#^A{�鵶(����	��J��N50������$��@��%�ݵ�o�����](���pgR6ׄgeB�2X��mAY�+��<j�w�pA6z�6������.T�9/���Y�<�&P�L�#k
��O�@j�y=0���5��Ɵ`��sc�i��FN��mխWi:�����Y���JP8�E#�)�[R��q�l_H3\���m�6�=U�G-�2��Y��������*�,c3i�$+Ƞל�I�q�)>/��-�[U���(�:�m/���)x���]�pΖ�}u��	��,�]���e0d�:+����i'<�]?%<��8�އ��$���3�$gگ2��`���t��KƦ������ ��}^�,zN*1bz�ZBg'NW��;��m?�����S��R����^3c�e<�I�Ұj���#Iʺ�r�!��ɝ[E�;F{��q�}�^�?��q�{��7L��C C��5�����i��R`v��N�w��6~
�)9Nx�X�Y�ʝ25=#�Ίw�)�|-�Ѧ]H� ��n�c�W^5;48�dL�Gf���>�M�S��I-,���!��Wj!�rmނ��٨�ۍ?�ބ�i��X��U�P��<��v`�����tL�H����E,�tN��t��\��H������W�p���3�?}}��''�� �U?m:ڜ�9m
2���"���&G4H�W�	�CdwE��>��U�J#��\����FάlT���Ȉ�`��=L�z`�6KiI=�?y5�0K##7� ��\;Xy%0��<L����`�r�����v�d8e*��f�cyUCT�.�>������%�ۏ���~2l���O�18�\���ą��߀x$��c��R1�QA7Y�����X��N��Δ\��7���oa�l�ӎ�11JI�#�'B�u�k2�H�n���0�Н��j	��m�i/�L)�	�w�L�U�"�4+��6���jtv��`|�1}d�u'�E��G�Mg�0uwE0�����Ĵ+��P�1L�ZHOFl�	�~�2eJM����IM����/#�$�(�C�5a!a�������H�^ކ�6jgR�s)���8��Fd��`�Zk8�gB�,(l�A��xɤ���M�P[%��3��R
�Giu �8�t|�azoZ�)F%h�^���,Z:��K1�z�ܥ���9j-ZX���p�N��u;*��0}A��ct$��.aݗ�JC��X"��}�۬����䨉:�M�i��K�8�V~��ں��e!���t��:��m#H͟���.Zc4s���ӊQF��;-�}3J��MH&e>iv����N�s��s�'f��k�"��QSW�����q�m{SJ�p���b>jeua$���A+ޣ���� ��-�JY=D���P:{\Iu�Jj�U���8c]$��	g�Z�z�POM�`4�����=M����ǬE�ZZ�}�{gb@.1�ڠ+2�\�ɶ4E���

f�b�eK)1�hs"W�/7�t���g�9k.�wWc�;'�l�*ml"q��+�2
7tY�5&@�eu� {���}� �f�(����(�fd���J́N��H4����&e"A��DU'"a�?OZC��� f�LU`���}����u�Ĵ��^���� ��L�i��]MԬVv�����G-i�[B�ꆨ��+F��?�@e����+���W��̀{����MQ��J�"��IS�s�#�k�ij��@�5:����2�����}�g������4 �{����y�"j1��rjsCz�%<��.(�J�sJ��su$SG������$�E��|$n��2�l���{�������`a Ο�`�j�����a�/L��5��a�'Ը�+RL�IuI�R�>��-����O��@4����w\T������ ��,���ڪ���Q*i���4�sԴ���,<�dȮыϏ6ZϿC^�G��
��c
�Ɇ�&�g���)���!���z�ɍf�3��b�K9߄�^��K;QL�ǁ��X0��TF��V�M���b��*a�d�%*��'���w4.�Y�y�K��Q2I�SM� E���#x$���o�e�_IZƱ�3 ��Z�s(�K���Qc�7lƩ���Ά=C��G��gc���$ �ZZBx���*Q��]�0Nݓc�ˀ��G��w�NC�%�D��f^�����kף��!��9��[n%uM0��4E��� �'?g1��s�:"a���&�����R&`2	=�m`�i �ބ�_�
?�	�4�F�v8jy��ǰu��D1fX��]��2 �S'wm���&CBi8ۏ���D��\�}�'���#�����,,�N���2W<��VL�h��2E҅��[xB���wڡJW�-׬�Ɩ.\=�����.7$��g��F\���	�����f�&�;=8����O��a�i@SP�Mt��d�E�Re�V��CT��0X��/a�$;J&b"�@�� 9ۀ�<����&C�nBԔ�h܎k�|�4mf�HF���g-l�^/�E���ڧ�����U���oq��/�
��^�C�N.���(��/���p�4>a$��c&�=��{q���.�g����4>
w��P�Gct#�KZ�ζ]zh
-șc��e�����8-����Kߞ*�]x,Ň��=�=Fцc�'���0�r�
Y�u��*�c��{���׷�)y����eZ&Q7깵؜���i�s+eyEa�A'��Ԝ�m��<�*۹�u�k�T�=����	>��z4�x��_$c�.�ĺX��O��Ix�0:Ħ�a�����|&����}O�y�M��.��|2�E?._c!��54&GN�~�1҇�;�8?[��F+�~�ț�a��A^5��"��4L�6���Vوe?�?�M�žs��ի���)lhn�$����8�|(�9�\����!��G���_�����������#!l"��L6�	]�G�gfL�s�N���G;�R_��_܋c�v�@�G^B'm�Uӌ�٩&F�*)���`5XM��a��1�n���D�S7)�%x�׬b�:K���-�"�xqv'7=�6\�x�[�����T*j�!?�m�/�?9����X5�D}����a��x�	��X;ighҡv� �q�J�O�c.y�ئ����n��Z�г��S�oӦ3w|/�K�Ҹ4.�K�Ҹ4�6� '�n,äq�    IEND�B`�
```

### `src/flows/fno/commodities/assets/natural-gas.png`

```tsx
�PNG

   IHDR   �   �   �>a�  ciCCPkCGColorSpaceDisplayP3  (�}��K�PƿV��u2�C��
�8�DqU�ꔾ����G�"7�����
�n�::8�������y/��"z��~|��8 9npn��;�[\�+��-%��� �񜮯J��?��>��N�Y�������1����]H�����%����qK���r��g�X �&VXͨ�������`�r���l��9�X�<p�0Є�?�����]r7�R��|�ɑ"'���p�0�XC�R�w��w�O���'`�#�����p6G'k���<02\�����G��V��S`���P϶W�j���<0�(��$�:�-!>���S�p�|�b��[   cICP n��   8eXIfMM *    �i            �       ��       �    kF&M  YiTXtXML:com.adobe.xmp     <x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="XMP Core 6.0.0">
   <rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
      <rdf:Description rdf:about=""
            xmlns:xmp="http://ns.adobe.com/xap/1.0/">
         <xmp:CreatorTool>Figma</xmp:CreatorTool>
      </rdf:Description>
   </rdf:RDF>
</x:xmpmeta>
�\�  'YIDATx�	�%u}�u��ݷ���i�YE�Md:G�3����=F=br|'�F9F�$*�	$�G�FD�������]�ֽU��֣93#B��^Wu׻[�{���������,�"
D�(Q �@D��"
D�(Q �@D��"
D�(Q �@D��"
D�(Q �@D��"
D�(Q`�P�Y$����[��~�۾�w_s�)���}�o���^��G� ���$�G'~p\o�mo8{���X����ş���?{�sRk��yR�y�XD�5[席�k՚Ŗ�����B����������֭�E�S_�O9� ��,�9N&�Θ��\��
=el�/����=��r�	�Q% �j�8�Z�L����c��U��s,=:���7n�q�O�}��<��:���o�?��0�ٴ�ܜ��ͤ�V��~�C_��ڛ� �x��~�Q% N�sJƗ�ͼ�9�X,fN`O����c����W�ޟ� �-�����S�*&c�	i���ϬR1wb¼f�:m��V�ⱸ��,79����.]�}ޟp�@ҳu�vg8A�[�7��� +�n�֬լQ�ZCn�-�������~����?���yoH��d2�0��Z<�l.k�B�
���x-��[*��A'�_b���|�u����<��F `��b~���,��Ms̿���b�})1?�$.�[:���N���{��9)��_<*�ƫ�Z�qۯoכ�d�q������;���7�jioY��6�����M���>��s8���`u��Ɏ�dK׬1'�s��2߂����� ��~��#;�6���/��b�� ����L�����-Yn��댎��.�k�N`�-�װ�D6��|�z��_��C�R���^ r��og;5�V�=�,��	k�N�f�'�3t��� ��o@\`��'m �6��~r�u+0����� �<2���*�H�ڶ�U6p���oŠ�p�@��k����w�4?p"��O����Ϯ�����.jpj���ؙA�ik^�9~EЯkn�n�����c #��Q,
��b�r~�8�����ƍ϶h��?���l��8��_�t���>Ƽ��[m\��P�����?-|~f���%��}C�LA�Ả[��(�k㢊� �Z�������=���,8�ߪ;wZh+��~^�x��p	-����G��b!�D| �J[�zA��+voܸt�؀E) ���gߐlC�Q���8�
˖Zs�v�LN�W���0ܓ��8�𾘭L@��q<����D��0?KA�^��Ϸ,�:�� ���߾.�y�r&g��>���Zc�������`f�v�������W(�*�?���.��Gp&w��/[������-:���ǜS�ي�y����c�Y��6�?�}�O���O�^�\F�C���i��1GH@bOml��/}u��g�Yb1��#��_��{����=6eǝ~��s9ko�b��1��{hy@@��d	H���x<�u0��� �K6��
J�}Dn �@<��\���ع�b���#߽Po���g�9'��_*s���m��ך�أVݷ�Z�|B�bT��02�H��m���V?��B:<�X:������du��8B�}�H r���Ean��WVe�o'덞����� |j0��aҽ&~^��|�/3��0S�������T���,B�*> XlsL� ��@��ة���ȏPZZ�2��%�G�ܘ/4�o�-86E���o��䔵�m��G�'<�a��6ͮH_ ���"�
A<V��&��PXa�'ˀ tp��#��ĩ���w������:�mFFFb����9�E�\�N��B��sָ�^��̂���2T
��h�|�~<V�/&c�% 2m�c��ѣ���� e�)��,٬N{��g��	���ON�,�?Z �.?]r�+�����կ�����?��yd ��	ڈ��\�q�;��i`��e|��R�,��!xr�C=���7� � 4��xρM��0kNi�ʎ���~r݆�[`�'^�����.C�j��P����|v�6w�.�&g�E�֖O�H����O�&����U�~x,�W�ߖ�ct<a>BZ��GӴ�Kp�A�hj�0K��󩷽��s�ֽ��ZH$]�1�m�\sr����5�Y�{�%o1���֎�V=|��|j��U���U�V��%>�)A�-Ɗ�	��"H`-TN��4]�Ֆ{ ��@�*/(�����%��m2\R�'���o��ϮyՑC��������l'�fα������/�����ۭyh����߯������t.��I�xNy~��`�|m�b�P@^	_SA��8B��2�u�$X��<*���ŢU+u�۹sx��G��q%\p1@Ο�b.�Xߦ��n��V2w㝔j�[#�GZs���a��B�RA1r��K�w���1@ ���=����;���@Y���C\ xB��k������e�0Y45M�I�y�m���ȯ�w�������/~7���ׄ�+�-�%g�m�;M����z�V��y?�P����[�V�7t��]nA�]�Ǫ�p�m�+>��u�ך�~�0G�Q��Y��M�a��l�L��#��Ɏ���.�d_��.��`�f|k�U�&����\x��>�§���66���̇��.S/?A���K�e�C\����Sb M��s���,�d� Y	�|�:�P��X����e�9+9ܽ�
��L�;pp聿���a�����D�|?ߩ]��������O��͟�Ԛ��	�Oe��Ч���*���S?U����s��P�U@  �r�� ��f�e���Fj
��	����}M��l���9�A*s�
&B(�G@�m~�=~��]?Y� ശ�v�m���,ߒ��w�)�޼�&����U�dÓD���G������6�,��!����Y�y&�����i���:X��@"����4B������l���lf���'�����1�o�gw��.�t� ��Ypڭ?S��_}�yf�c�>��D���Y�&�2�-7��]S)�`~�7Tk��6c�ԅ;L�m*^��j�P. ��`<*�PZ�Mc�cCA �azhnӣ6��`�\�T�WC����>���o���{�>�����v�;W�u��n&{�w�c.��Z��< 7?R�SE�%\��,K��>S���~<��9����!�Dp�v?�b��u��7�+���V�e�Pه��rX�~��:M<T���;�|��+��� �_uUO��~���h[�*�����>>0�2c��3�:�B�|��|^�]�[��U1��APASg�u�r��D2��z�H`KHp`���4!�*5]�`��Sk���MRs�s�#t�2)��AHbvm}�rZ�G�έ�-@���Eyw���g��Do�:?d��I�$����k�F�hi}X�	5x^k�r���.����KFPGBA̰���23~�|& �0	� �܊�b�D�D�@h�Q�RC��g�ST�����`�ľ����/���n�F�Z@�H������K_s:�}����oN3�%�܂a��1��	���{�l��4�]�������a�'���o�}n�vLOٚ�+��Qqi��B	R(LpXnA. �-��$�1������i���a��N("r���L�&{�l���.]v�k����ih��i�ЪU�EKm�.si�����N����F����0@`�����%4x�����f��]�����l2��Y�Y�w��UA.����t��
�P iq  �	@��-������������H(y�����}���,��A��^�Z�14q��f�Z�w���Q�n��h\��
�T��%h���0F�k\r�&��a�
?�tg^��d&����N�i�U����
y��Ttr���H�R�O�o��?Έ�4^k	��>G�����AQ��7�G�,�q1����o���_��l�v���H�[��y�7y�/z׬�;L7�8�^Ŧ��mbb
���C�>���0Z���a �_�q��k h�4q�Ϭ����f<���N�R��=s�9�%KpI�J��@!��Oŉ�
�E�;�"*h鳸������YC��ғ8�o��/W�/�J���X��O��V�P�up��>܁�|C��	�W��|>�f��14���i��T�9F�O�*�	��3���G�~�� O��V�b��H:��i,��1^�E��S��h��w(c5��da1�r@�YnS�@�vx���>�.u�֕��[g$'ݢ�WdI74�c�_8��$Z���*�6&	�dn�ʭ 0��9V�`��0����鳁���a��]9N{���?Z2d_Gk���e�,q+�����dS�p(�|����J�#�H	e�D�Ydļ:9u��m��t���'��_�A��nAK�a�+��[�U�45pj��m(�Gݑ��TL�ҷY@�*��O��F�6��$?�����{A߭����E��c�����O�h���0Yw}�v5���$%X �/ܰ�Ct��V�>���V�ZW�v% �z���8ZT$��z��jZ��Ì�=f�}i�l��a�|��v��)-s203<��S,[3�����L��Ѱ�4��R�qy��	��̇1�4�ϑ+��i:(,7�8$ɕ��}I���G�b��ih�Վܽw9�{�l�kN���Ko�{~{X��aa� �M�����q[htX�Cи0gG�C�q���aa�~�TO��,G�`~��ÍKz���d����n'�sYN���g�s��.�s_��L~�����
t����1Le�
J�X�>1�u�`�Y�33d�J"�#��(�^":�V�$G����+]t%��T�h�<R6���C�`.��5U�J}�f�ُ�y�J�ي�9��RNfe��+T��"��ʸJ�0�)Ɔ��^����d�6�q�s�> k��K0�n�����W�O��XZ듟+��xv+�J_f@�P�h?�7vXL�`��GL��w���9�7�5�^}�Ov=�������8���M(�w�ne������w��B������h�Xi��=9�OA)� {!���?�n?��:��u�(~2��)/n	 ��U+�$�mM'>`"��O�h�<�̧Ր���F��σ$wlE����޿��{���g��gy��Q��S(��vW���K�@��s�*��4�JI,�vs��v���ZuT��  B)	4bt��uY̽����\���n��a.���t�v5٥����������i֦���}�Ep�rA����˝z�g�_��s���X�Ih�\��
߄M�WP�s�^��r.�
z���'[�/�	 z ���F))6�g�
�	p�T*A�Pwm]' ��\�Jgsy4Qk���H�ɝY�v�ԪV��U�}Y��1���v��4�@6eŁ���ll���u���ݳRh�&�ˤ����zj0��y�I���A ��#\\K$�W���	�g �7HQ��1�k5�D:k=KW|�x��:-���\� f,�80>ia�6i:'�i�v"��b��!p���ǮXa�Tj�C�߾+<����;���E"D/�HƘ*����R�j��ܖ6-^�Ú�a[V*[/�D�n�$���'�f�I
3�"�~u)���R�|���c�>�)���u� 䲛 �9 r-2 �_�\��r�`f
s����-4���"O�0�{ʸ+�;5z�s���~tM2�OF�;�;�j"U�wd��S��;����\��vSd*��[?A.H:�LB
�q,A�����- ��c��^�R�r���s?���u.��k�) ���ک����&�@����; 1{�@�|�_�9v W�1��V���0�3�??�eݢ�zkWjo��na����mt�N��ÉԆ�>x�GN8�5w��O��haa
|n�o�V�0����ф������$�j\��0��'���g��ҕ��Ģ���7j�>	b���!F��y����{7Eo��D�x���7p��U�����>)K�\1�
Y���#�����vֽs~����ɞ���'z˽��=��+���%��TO��G�������ku���,]����;�W����s/���[����&U�~=��"r��zTS��/�[����w�|���G�/���ʕ�<�m�o�~�C�_��/>��O<����FF.j���D
aT�(E7Q/��î��I�Z	<ҹ��(>Q>���2���u�3���p�#�q��;��S���:e�"V`~��=�V���@���u�����X<�f;��G>�n_���);�����U*M�D��t���4�z ��U�T��(���돖���q*��m�s>���ꫧ��;^�׺��\y�������w��yD]�-��L��1�&���y�/�H�R��N$���3Z�R�۬Vs��z3���׹?�;д�K��2E�4P�(��W/�0�%��%n'���K=�����V �r��d���~���Je�e�RL㯓�6"�V�,1��G ԕ�	⁙=����������A	�O��B��s��kT�i�P�5��	V��V�Xn��ƒC�?8�k_���b�K�ܮ ��z��;�έi{� �(��  �@+��l	�.���ͯQ�p��n4� �/�F��ۖ���=��`���ƚ�
 �r���$mc�A(;���r�_��zK��N�7�� �����Oy��Dg��qi�iXy`�z!tILn,�%��AS�F=�zp�oA��Z�S%�	����ľ�|a&�����%;(���b!��W!+Y5���GF����]- b���|�v2�	0�Q�DWP�NP(d(	�?O!H���������U/��|B�}�P�� (�N6ff(Ecu�8
�����"S����+��$3w�/���r���z�o_����X�4���?� /�-,� h�Rr-g��|�)�U�5w��J��]~��|�ޞ!>�s�? #A����_$��q�|��X�^��j����7x��GFhb��mA�H؜���Y��ޚ56
<,̿����t�r��4���w'��׿ް�����c}�T����Sl�%�j4���D�h� � =+��UK��`_�Ugf2���ܑ�w��o~�޹`�u��7�<���|w?��=��1����O�-PFH�3�/��Sc�{��%��}��甒��q+'�u��0��Y�����|p�p��H,�C0��&w5�����}���r�o���r������7�vڭ,�{���3Y#�V  ��Y���sԳ7�k�t������M�~���6��?����!�S/y�=~ӷmǮ��H�²�����ҨV�=�xr���=���]/��"o#jZ���~����蟞�Ζ_}�1�`>�F�����M�"����:v�}K�t�?b�S,_�=7��4�$	���塷'k���w�ٜk�շ9ӳ�%�5�}���;7�����d�G�T���_k�!��S��ᖩ�g:�
U� �t_����O������J~b|����ي%��:@c3v�ѱ���\�Ug�i���1�B��A�v��(τ��F��at�_�H�Ⱃ�{�՞x���_m���,�	��i`0(=�d^�溓��/��ɋ����|���p�m���gf�����d�$��~8�e�	��OO�6?�@j��Gm�6���K�"eZ�FYSh�(˷�_{�Mb�5X�Ei�HM&*ڔA����;�U�o�����j~mW�w�`���ԓ��\b+W�0�����Id�)��v�s�- ���Z�����+ǟ�	���]) 7n��LM]J@��N��Zwnn9cZ���H�Ԭ��bB4�f��}�m���w�zP��V,�A����x�(���n](j�+��C�
��r3O��e�`��\t�ܶ�vl�b{y��iw����z����^ni�C�+F�O�E�	3���z����<����Y��;]tQ��d��}w�	��n�q����^1��P�o� K��·�8�^^@'/?x��l�i���g������0Ku����:��w�ΤQ_X��|&�!z�
O>��my��q;��ʿ5>k��PY��NY���h4MS����6����h,P!� ����Iz	�d�>��O���rpfz����^8]��B#�J�������~*qm��e�f�E�+��Z�����R��%���N����4:�q��>�i�Jz���K���	�&j��*$g�=Ύ%��UG��������G�Yȡݬ��ș3H���rY4��a�8��p!)�a	0+� �t��9�Dֺj	ٮ��e�ʵ��m׽�qǭ����\�����չ���*�Dt�
h�b���%�Ba���kH��j�\���ʖ��׊����b<��e�͋��,���@ѩ��
A��v�S��9���^��z/��Z9,���`y
�e,Eyh��L+�k.W�}63�J>�u�������X:l�	�3�kw8�Q(��(-F����-��rpLѠ��].A�֥a3B
��C�$eZ1-<�"Hڨu���1P�F�&�P�z��@�In��|���i ���@�ejM7Y���gR'P�=:��V����}�H���u.�����e��iY�f.��<�����ϢQy�l����+����&�lC�+�V\�Q�(�-w�Ҳ0�¡���ɦ��a<!8Ws��ǚ�D���*}�3���o�%�X�Ci_+^�f��\��!�M��Z�$\9��Rk��K���{r I1J��`��#t��u@��©�{`���D�@��_�h]�	ؓ���nh���ˡ�А���
.$<n��{ܒ��kh�X�%M�ε�,e�߰�1B���x���&�8$&l��_De��k��J��a
Z�"Me0&�D��d>��~��G�j�:H
s>�?
�4��h]��*㿵s��\�1����Ö1.
4��L[ͧ�+\A̅�n��R��*�bTJn�n�����5]6{�E��X?�o���>8bA��ԙ��H�
���-��Q��&����d�jqIb�	@l�����ὙtfU�ʴJ4�7?��5����0�>
�<:�<�����O�5=������v}�Ƽ�Z*mk�P�%|�
��1M_�vejH��"�����wCJ����S�+!�=�N��N'��u�&:t�vқ߼��/��;���N�w�ǂ�i����y��*�t���ys�}�h�48kf84�h'lC�y	��fJ���`�ފ�s�ܟ2Y�������+�ޯ�q�� �eꓚM��T���ʁF6��=Ss{��O���z��^{�N}U7m׮�~|��=���k�Ι�f��D�?>�I��eS��]��t�7.<-0M�0�y�� joָV ~_���WP'�����^i�F���P(|T( (Z<�l��iF@���$������`�O��V\+��N{ަ[�x��=���Awn]- �D2����}��Ԛ\o��Y�aU*�2��$���g���^��*rM��}�l l�g��XO'Nw/��tX�f���r���]�|�i�%�x"H��U��(�k �ē�I"�1�s���`��C���-cOM~{���/�w?�����y�[ߚ:�<�ϧ{��T�A?c�<�<v���}�\��=����NR�?�5�ڀM�X���dw��h����G��=�I���BtTD��"
D�(Q �@D��"
D�(Q �@D��"
D�(Q �@D��"
D�(Q �@D��"
D�(Q �@D��"
D�(Q�7O���0�8�3W�    IEND�B`�
```

### `src/flows/fno/commodities/assets/silver.png`

```tsx
�PNG

   IHDR   �   �   �>a�   sRGB ���   xeXIfMM *           >       F(       �i       N      ,     ,    �       �       ��       �    �@k   	pHYs  .#  .#x�?v  &�IDATx�{�eW}��~��=�޹����93�k cb��&�Md7�!J@��Dn%D�J�J��J�?�)Q��:�RPU���Tr�R��`��̐�<���y��w?��Zk�s���{�t��{��o��[��o��c�}ƹ�544444444444444444444444444444444444444444444444444444444444444444444444��H^t�#C~�ޡ����X�ʍi���?��W������_*����nN�gUz������]U����)���-�$���$I��GKW>�����;���ci�����.����A}p�:V8w2M�۫�z�s�K]�n�^j�2��,+/�@Q!�4qW����EQM(p�r�,�}��+�G�~b8i�����e���t\���ܝDl����z4��AG8��Vj���A�(�LP܋L�"�Q���L/�RdP�_N+7���.�p&���{��c#O���G��w/��)7��x��C�_<='2�ŨC�.Nқo/}���F�f��գ�(/d�6�&� �
/��K"2d�҂�d�*7�U��@�Rn	Გ�Ȧygq��x���ҡG67.���w��gb}�����7����O�ݾ��ﻩ��O�Uv{�L_
�/�S0L�Nt� |o�N4}�Ilݣ競�(���:l���g@��ۓ����!�4k�����΂kw�U�ꈧ�,v\1Xw���z�\y���������^|�~�����c��c�����~y4�:n-�)����x�?���Ԭ��d��� �Na?�{����0=O�]D��!BҬ�Vϵ:}���v%��C7����%7X��v6W�pK��?U5u��pzn0�_�ޏ����c�)���s���_�̻ߕ���I���t�.��K��*K7���b��2l��p����ЕŘ��T���}����4��sq���z�dL��l/�܄�G�]3�e9vz���7@�C	{{�ɘ���2�:�	&�H���*wc�U��q�/�R����C�������?�t��rLh��.%�����;��\J�K�.��R��qT�b�,�t2 p&�R
$(�kB7�L$`sQ14fh��M�^؋���˲�:�hӍ�.#����V�h{����Gcz��9������M?x�|=R�V�I�`~�K�{>�����w.�)s��7�\��l�!���Xtg9����`n�K(Ċ�L)]���K�e��/F3�@`�R�
��sAS����K�.ʅo���ѝ�M%��n��h'�l/l	��=���L�^�QǢ�RE,B���kF}��D4=ܧۋF�i��,� �%��cz2�A�n�IV�[J�j#�����ޒk/� D��dw��-ϔBCE:�G�+�~���(=wLO�Yu;���\6s��b�2�G4&=��л%tuk�\
úyu�Xk|L����dR���}U q���O������r�i��R83����Ȇ�2� ?�g9W�e�0	����8tx�X���#�P�zwɘ����WM�c�=t0��6�6�O�����'�|t~-xIߛ� r�y�5�OܤH.�����蟝�/!�(,@9��b'����B���?Kkgs5|M���e!R��¥O�$�`�&��B`%:޼����n���n����d�[=�%7�ѫ���9GЬ0��Kd�Da[&X/M����v����T8�MPJ�m͢趒��d�s��׾8�k���������#����jz��aś	�j��L	0c��A�6c�+#_
�f9��v�n~��^��Z�;�ȟ����	[����mb���{���>nB�UюO��ĭ0|��طz��,K%�ҦQ�>�y���~���b�s��G����Nƣ�[Yu=�>�y ��!jq��zJW����O7��0>k�`Z0v�b��X%0�x�G=~�@1�*�hZ0�Ug�R ��9E1�����G,�������Ѡ�����X:3��Ye{�WЎ[��j��d�5��+A�_I�
a�K-��fY��LO��|�&na��&�,��5?���3�^رn_�TB�p��4�PBVn�Q΄�3����u�~�/��{�������nX_�[YR�
���Bv���-,lK3��d�?+ka�hH�,ݯ�ex�˰��%����CM�A����\�t���x�����!�"!=z��h��J��~��ꄯ}o��� eZ}  R8B���--��]���d�}�¦H$p+kD��5��@s	�O3�^?�r�G\��	�,T?q/8�׹aJb�>?Љ"��Ǡ�>��J�*~��p�� ��w�z{R�o���k3 ��XB1 �@L�Ľh$X�X϶�L�*g�*KPuqirgJPHxʠ%�H}��`"VB�)Ɋi%��R��4T�,mt�6��}�y�b��
�=�q��zF���}S�*�7�JN�HD=S������4s>n4!nDʙ�|ᐥ<�SS �� � r�֞��O�Z�λ��|6e�(�[�[j $�T������?:����|�c?~`Z��5	��T@@���L�>L�^B�)��фMP��A�*K\�/�Úx�� Va(��]�R~�j�S�X@~̥�+��%��pT��Ȭ��D�����W�{��E���ϴ�ꄖ~^�&:��ѕ���*�l��@g�j~HSU
���̴h�n6�(��sʫ���bINux�����O�F1Մ�+&?ę��7��_{����/tx���_�����_�\9@�rތ+) �^M<�F���`�l(LB��:��ꁞ%��a�@� �����o,��X(
���y�>��L����(L���w�+(d�ς�=��G�=W���^�T�M&S�bN�Hxa �K��]^n>�p���1,�@l���Pb7`�ǈ�j�5��c�HS��g�'� �R�1��**g4��8i�g��N�ɴz�o���xq�7n�����%��8	C`D����~�dX�	��E,��6�6��H�^�����=
ZM���*�� V�����BHWR]�"r�������dB�I^��b�������NqtA利�������o��j����ci������h�>X���7<�.�Cզ:|�P5���!�+ �8oT��-1ܔjN�G=��.2�&l#��粚�7W�\ŠG���h��)�*OJ��e�o������_]����=U����w����!8��&\B/o(�X)!��2��B7ˠޫ�B8]`Fa(ж1�ʒI	K5��y�Ҷ��������TotR�(�]��<K��Tˌ=�.�F7"�k���Ί��+\�U�\�J��q������t�C�Td���T��Γ���G�7��LҊ�\�I,{H�F��敯ِ�����X�ҼBH�ߔF=��"@/�,���Y)�����Ȓ|Y�����9�D(�'3~���p)����
��]'�V5,�Ѹ�nO�L׫��Wɟ�;�g�r��^�O.���w/�j͞�'?~��������8<����l�a�v�RƐ:̂Y��������ڔ@ʣ?�����?|mg�y9v�6lN�������	G���K�.O�J�e��D*��e���˧.�Q+-\7E��9Y4�.����&�R�.������?��W~��o�uL>M�G���=�@�����X�:��i1x[2-~&�L�-6C��Kf9k%�I_Q�&G�������BH���i��~�0�K��l ��u���xW�2�|��/p��G�Gߗ��M5L�Q�N?c i�m��k-N
���monu�r7;n�Xv�֊������V�n�z�4i��v��n�g�<{���/���CB���9������_��_�<����th)�_W�Ս��<�$�8A�f�>�W;��BU�9'�� �mn���7ٸ���Z��$+˥[Z�\g��{Um7�`-�#�B�����B���>�S�kx9r�	28H}���C�� M�k7؋��x��t�Y��9K��N'��.� �����=3r���s��3�Yt]�5�:��~�-�R��>s�n�c�y��owZI���C��T���2Iw8�|�}����X6?:]|�o��G����kV��z ����.c��h�}j2��k���Xf��'ڮa��6�Y����"\���c7L��p���G��ޙ�;����''7��Ύ;~�t7���c�"�Aյ��@���)�X"l}�iJ ˡ<��C7�ȑ��)��G��	��({�,�+L�2H��ؤ�q�U�\�Q����[�0t�>;r_?S��W*���r�ܺ�[Dq;n�#h�(�9��1����8��Ł�$mqL��>0��i^�H�� ����*Nݘ�Oq��n��P1���M����Yp���� ��{I���O�v�>�°"n�_o�y��X�=f����������,a �=}�_rzw��������k:v�ϻ����S��p���PG�o�n�G8����^ϕ 9a�5Ūh�Q�&���Љb���d���y�+nk}�zv0 e����+׌��Z&�m�u�_�+�ncu�67+�3�J�����^�u�����M�0�+��r3�q����aLx��ZeH�����|~1�S^L-t�eJ_�",�V[k���s���O���j���=)���ox�B?�/)g���]O��t鴮���l?����v���H�W7�R9�t��EB�Ý��\q��n����]~�{�K��O݀ё��S�����m�=�s����,�Q�.���Sǁ#S����"=��)��o��M\�з���Ό��x�n�Ҷ�ra�\����a��U0E�a�2y'q+�u�����-���[osG�ǎ�]��&�|�D7��� P�R���-ԓ�0��R�<�L�(���<֕.'��A�w���/^��i����M`Pу�Zbder�/���	VZ\�ym���E�7u�V��-]w�-_�ykX$���[���̐2B�EKff߃�	���yΪK�]�m�a�-�;�|�'�@�
��x���36����k���-w�/v��#�ve⶷�X"��9���{$�H�Ő�f�����d��Ԇ�c�۾d�#蛄�Ջ�q	T�Q.�6 ���1	Xq����qe�&�
���p��^r~�Z�x�
�鏼�6��1$����"��fb,3���[�A��QI� ��𶮷r#�MV:G�%EI�0F���3����-��n�f"�̌?g"ɘ|�뺇1��N����ķ��S�nsu�6��n{k�.�W��(X8A�:Qb��dE���&��*yr�N�ͳP�]�x���	_�O=]��, �U�K��(hUI\���Ek�32)�������W������k�)�kV W��n�nq��������- ag�%y�"��^�sz���i�c��X���~���I\�ϼ�|��ż�Y��b���"���	�s��ɟ�'�gHHJx�^�P��[�=���/~�x�0	�st��ՕK�ɸ�_Ѓ�9�3,I�$��GS 1 e���E�N�XXzs��2�/�B��bޤ��,=B��,���8�-HoZ*�������]�|�7�3�8��:Ј)��/AG-����C�.�-n�0X�0���'c��z'�@��O�?��{�Lr�:1�Ƀ�s3�����qޤd�j�����
����;L�/3�0o#�ؗSLq�.˳�}��@U�l��z>B�"O�pE���z	_���n�YU>�'�<=w�.�'RF����F��j�5)@�����������C����AA�S$Y|�Hf�7�!U���ղC�_�ޔO��D��z��`׭FS�R�g�S�&�$Hq�'G<�B���&b��&�,E/`�`�Zh䢧�_��N�)��H�0���J���ټ�V;� 	wv	 o��au�F���ȃ�V��C�	Q������v�K����?�bW�M���,1_r�&@�H7q��P���,B�&�=59����N�q�>��~��I"�����aƞ�&[��u��;� $.��Jd���sL`��RU��h���ui�y[��z����_~P��%�U'�W;,,�����.rv�|����b����Z�T���z1a/��S+t7k�UлO���c���	�̿��\Y��$��f���>�R���͒�KÀL�� ))�̱G��g�\a""?��-�.m��b�/v������wH�;s�����6-;��VX.M��H%xP���(�^bً,�+����r~�G{L�T��\�V��-5ެ�"A�uQ��v�&K�{>q����rWm����`3)6@DB4�r{�'~�I�q5���Pe�4�<)��h�\�v�E���W:��3�Yf�U�u;�5
�JMb%���"�z(�������?)�����u�pǝ9�\`���\���l3��k��(����ˇH9���a�O��c�E �@Ũc`NV!X���Q�F}�,��X�y���l<��#$�qH~^�U)��ӧ18��]��z��d�y��0+F���o�pAq�) Z���7�s%��	
��AX��1YK�:P"���\@��^=�z��i���@� ��<#��^�R6)���W��X:����m��g���6���;/�/0%`/�+�a ���<0fXɛ��X��eC�£1!�ʇ*<���	�v�uGa�	�Jh��ww��~b�!f��M,Y�����	Ba��-4A~L���JS��ŕ'+`y%
�2�$��%�0��K�؜�~������ �t��s�E��Z��+g��a�����؀�sVy���?�D>�T�%sR�#k ����E�^P��z�l�@}�j
jBW%^�5>�bpY�����kI���Rt4$%V�~��z�u���*P�/0w&�ؕ��[s?�)r-3to�D�����X�A�b��Q%]��7a�N=B`f]�.��z�����,uբ�zk���گ~�s��SH)�2kD�)LBm[�GQ�Ņ�[������ �����6��t�B��VpN\�S%��ȒY,�(qџיJ�	ݣ�YL��EG���
)U���al�ۡ�w��sz��$���������_x�%.���X͞1��~���y+��X���AR -�L��v7�� z�&����UФPq���d��Ö�2��̌^��`���a��9&\if��/��cl���@�|@���𹺺�(�,����Ӑ%�= ��  ij_t
�uUH��(��y�N��u! �'�N�>y�����Y��m67ݏ��m�kqe�RQ �������\@A��;h-N	�Etb��� ���[q��oK�A�6㇢��J��%[�i$s�L��Y}�!%p�n���"��3	�;�6<X�Q�~����7��W��$b�h�����uQ���H��:q(�V�0��¿q�X(pjqQD�x�[��v��X9Ȁ��I�ڝ�{�N?o�q{����n#�g�Q��]�<ߘ]�{b_��u��|L���l @��y�&h� zè�fbmn W2�!�vE�Sδ05,輀�����^�h��g����uG[��A�Mi�d���PW@�m�@KC���,�ߵT۴	$�B����C��3�A���W��l��\�(&/7�_��>G�y)�����Ƽ�D���6m|�&'k l�/p��I�e�J�2F�����}\J@ ?���I��U�d��?/x{�Ns���|.�L)�?�)���τ�Ձ/e0�@�
x��n�E/tT�?t���2��q࣭�	e�&�~��󑯞M�6��c��sW��IT��3"a L�T_�\t�`�mg�'���?�N(<�{^
P�F���
���W3��L*���Ê�d�{ᲀ3RO�4_F�Vf� ����@K?�+s���-��=��_�L�W:ż�e�@��>�}cNp
�2������}ߕ� ��R�)�P�3Y�¤���$(QN>�<q*i�oC��z�{�kW.�P��S�l�M���!�
p��󲚾S��Tn�?�KO��~�+��f6ʲ�2c0�-Ku�y�/�ӵD�)!9�~3�HQo%`S���R&���7��.���Q	��B� ���\�r�aρ�g~��-,p��d�[�7�CG�r����2����5�!E�;��Y�N����"�0�����4�w��y~c��
���� �������2�� �.%�L��6�{��bxΏ���E(�EZ	��g\5��Hp/(!�L�*XB��<�1����!��U�@Ҕ��69o;��O[�߹EN!u0��_`�_�����̺~�**��=sϕ���ߢ`�Mг����&̥����[�r���,A��>��[}�3�i�s�b�Όo��T�8	& Y�"ó4�+�s��Xө�5�&D#�,@����CpH�謾PE���j�o��#xYP�{Rߋ�B#���-'r���/й�KL�P ��m���Ca~�XO��m�D�}�eD��<-�jTT`B���,���	���J����U>q��7������2�v��;�ࡺH�I���!"�@�5�[X�GH�փ��>M���2z��K�?i�Ϥ�C�3Dgϧ�a.b� 
,�S��6��j���:W`ix�'�-�d��&��C�}�X����Nʉ2iρ��@�?q�$� ��!F��RS����U���WR�F@޳D������]0�̎���n��������Vx�ӂ3K@ܷ ��VI)�f�ĺ|���$�ǱZ�څK��������=������_Tg�'z�;��qQ���a��=��N�l(���b�6���k���2�M��9��ae֧�i������sv֯�q:p[W.���9 ܘ6�,��س���ĊH�%"�-���s��L጖|��Q�Ln%�1�x�۳*�ʑ���J���V�<�Ѵռ�\L�>�V��(}ɹ�u�6.s�\�p��в����*�Z:�2c\aTE�Q]�?)��z���#8�9�]N���%wy��z+�W�9J�Z5,u��2?`��xV�7Ϡ�b�v8�N�a���\(���Q��a{k4��(���Y�u�Y \����7�
v���e��� �=J��:HXG2���vƓ��hZfV�r*kok-��^wYQ벤P�nzB���HӋ�� >:$�h!��	���]K�$��*��@��M�&w�!��.2	\c�EE�v�>���5�tX����v;[�[�fʓ.��e���o���Z:����R���aa�أ��!ƙB��*+ٚB���4ܸS�@�T
sl��-�""	d ί��n������'�O�gt�s:�#E>�_���d{4M:�2�f��=�?I[�2�'�4�'���:�� �Ov�|���g9����y�2i%-���|@#�/�,�>?�/����s&��׶����gh�}g�[)���4k4��x������S,�,��F̈́Y�7K�I� ��A
�)_+���+M;`�oV�t�+�x��<Pw��������G'-���2u�٤�*�����ȍF<��P�)�؜ȗ�:��?�ȇ/��L��3���i9��mx�h�*�Jq&�U���Pʍ���M��vVM�Y��N�������OzP��j"�� �HS�5o:�    IEND�B`�
```

### `src/flows/fno/commodities/components/CalendarDay.tsx`

```tsx
import { Avatar } from '@l3/components/Avatar'
import { Button } from '@l3/components/Button'
import { Card } from '@l3/components/Card'
import { Grid } from '@l3/components/Grid'
import { Icon } from '@l3/components/Icon'
import { MaskIcon } from '@l3/components/MaskIcon'
import { Stack } from '@l3/components/Stack'
import { msArrowDownward, msArrowUpward, msEvent, msLink } from '@l3/icons/material'
import { Tag } from '@l3/components/Tag'
import { t } from '../../copy'
import type { ExpiryDay, ExpiryEntry } from '../data'
import scalper from '../../assets/scalppro.svg'
import styles from './Commodities.module.css'

/** The day `inDays` from today. */
export function dayFrom(inDays: number) {
  const date = new Date()
  date.setDate(date.getDate() + inDays)
  return date
}

/**
 * One day of the Commodity calendar: on the left the grey date block (weekday over the date, today ringed), on the
 * right one card with that day's entries split by hairlines (home v2), or one card per entry, 8 apart (`separate`, the calendar page). Used by the calendar page (fno-38) and the home's
 * Expiring This Week, version 2.
 * - A contract row: art, name (and its kind when `showKind`), option chain (options only) and ScalpPro icon buttons;
 *   the row opens the asset page.
 * - An event row: event icon, name (two lines), time; no buttons. Under it one tag per commodity it moves
 *   (an L3 Tag with an up / down arrow and the commodity; tap → asset page); with `eventDetails` also previous / forecast / actual above
 *   (the calendar page — the home keeps events to one line). No country, impact tag or why line. Not tappable.
 * `sticky` keeps the date block under the calendar page's month header while the day is in view.
 */
export function CalendarDay({ day, showKind, eventDetails = true, sticky = true, separate = false, onAsset, onOptionChain, onScalper }: {
  day: ExpiryDay
  /** One card per contract or event (8 apart) instead of one card for the day — the calendar page. */
  separate?: boolean
  showKind: boolean
  eventDetails?: boolean
  sticky?: boolean
  onAsset: () => void
  onOptionChain: () => void
  onScalper: () => void
}) {
  return <Stack direction="horizontal" gap="12" align="start">
    <CalendarDate inDays={day.inDays} className={styles.calendarDate} sticky={sticky} />
    {separate
      ? <Stack gap="08" className={styles.calendarCards}>
        {day.entries.map((c) => <Card key={c.id} padding="none" className={styles.calendarCard}>
          <CalendarEntry entry={c} showKind={showKind} eventDetails={eventDetails} onAsset={onAsset} onOptionChain={onOptionChain} onScalper={onScalper} />
        </Card>)}
      </Stack>
      : <Card padding="none" className={styles.calendarCard}>
        {day.entries.map((c) => <CalendarEntry key={c.id} entry={c} showKind={showKind} eventDetails={eventDetails} onAsset={onAsset} onOptionChain={onOptionChain} onScalper={onScalper} />)}
      </Card>}
  </Stack>
}

/** The date block: weekday over the date (today inverted on the calendar page — dark fill, light text — not marked on the home). The page / v2 draw it as a grey block; v3 as the card's left column. */
export function CalendarDate({ inDays, className, sticky = false }: { inDays: number; className: string; sticky?: boolean }) {
  const date = dayFrom(inDays)
  return <Stack gap="00" align="center" className={className} data-static={!sticky || undefined} data-today={inDays === 0 || undefined}>
    <span className={styles.calendarWeekday}>{date.toLocaleDateString('en-IN', { weekday: 'short' })}</span>
    <span className={styles.calendarDay}>{date.getDate()}</span>
  </Stack>
}

/** One calendar row — a contract (art, name, kind, option chain + ScalpPro, tap → asset page) or an event (see CalendarDay). */
export function CalendarEntry({ entry: c, showKind, eventDetails = true, onAsset, onOptionChain, onScalper }: {
  entry: ExpiryEntry
  showKind: boolean
  eventDetails?: boolean
  onAsset: () => void
  onOptionChain: () => void
  onScalper: () => void
}) {
    if (c.event) {
      // An event: everything upfront — there's no event page, so the row isn't tappable and has no buttons; each asset it moves is.
      const e = c.event
      const stats = ([['previous', e.previous], ['forecast', e.forecast], ['actual', e.actual]] as const)
      return <Stack gap="08" className={styles.calendarRow}>
        <Stack direction="horizontal" gap="12" align="center">
          <Avatar icon={<Icon icon={msEvent} size={14} />} size={24} className={styles.calendarAvatar} />
          <Stack gap="00" className={styles.calendarText}>
            <p className={styles.calendarName} data-wrap>{c.name}</p>
            <span className={styles.calendarExchange}>
              {[showKind ? t('expiryAll.kind.event') : null, e.time].filter(Boolean).join(' · ')}
            </span>
          </Stack>
        </Stack>
        <Stack gap="08" className={styles.calendarEventBody}>
          {eventDetails && e.previous && <Grid columns={3} gap="08">
            {stats.map(([key, value]) => <Stack key={key} gap="00">
              <span className={styles.calendarExchange}>{t(`expiryAll.${key}`)}</span>
              <span className={styles.calendarStat}>{value ?? t('expiryAll.due')}</span>
            </Stack>)}
          </Grid>}
          {/* What it moves, one tag per commodity (arrow = bullish / bearish); tap → its asset page.
              One row that scrolls sideways when they don't fit. */}
          <Stack direction="horizontal" gap="08" className={styles.calendarMoves}>
            {e.moves.map((m) => {
              const label = t(m.trend === 'up' ? 'expiryAll.bullishFor' : 'expiryAll.bearishFor', { name: m.name })
              // A small L3 Tag: up / down arrow (profit / loss colour) and the commodity; tappable.
              return <Tag key={m.name} variant="tertiary" size="sm" color={m.trend === 'up' ? 'profit' : 'loss'}
                iconLeft={<Icon icon={m.trend === 'up' ? msArrowUpward : msArrowDownward} />}
                role="button" tabIndex={0} aria-label={label} className={styles.calendarMoveTag}
                onClick={onAsset} onKeyDown={(ev) => { if (ev.key === 'Enter' || ev.key === ' ') { ev.preventDefault(); onAsset() } }}>{m.name}</Tag>
            })}
          </Stack>
        </Stack>
      </Stack>
    }
    return <Stack direction="horizontal" gap="12" align="center" className={styles.calendarRow}
      data-tappable onClick={onAsset}>
      <Avatar src={c.image} initials={c.initials} size={24} className={styles.calendarAvatar} />
      <Stack gap="00" className={styles.calendarText}>
        <p className={styles.calendarName}>{c.name}</p>
        {/* When kinds are mixed, say which each row is. */}
        {showKind && <span className={styles.calendarExchange}>{t(`expiryAll.kind.${c.kind}`)}</span>}
      </Stack>
      {/* Option chain: options only — futures have no chain. */}
      <RowActions name={c.name} chain={c.kind === 'option'} onOptionChain={onOptionChain} onScalper={onScalper} />
    </Stack>
}

/** The row's two icon buttons: option chain (when `chain`) and ScalpPro. They stop the tap so the row doesn't open too. */
function RowActions({ name, chain, onOptionChain, onScalper }: { name: string; chain: boolean; onOptionChain: () => void; onScalper: () => void }) {
  return <Stack direction="horizontal" gap="08" align="center">
    {chain && <Button variant="tertiary" size="sm" raised="none" aria-label={t('expiryAll.chain', { name })} iconLeft={<Icon icon={msLink} size={16} />} onClick={(ev) => { ev.stopPropagation(); onOptionChain() }} />}
    <Button variant="tertiary" size="sm" raised="none" aria-label={t('expiryAll.scalper', { name })} iconLeft={<span className={styles.calendarIcon}><MaskIcon src={scalper} /></span>} onClick={(ev) => { ev.stopPropagation(); onScalper() }} />
  </Stack>
}
```

### `src/flows/fno/commodities/components/Commodities.module.css`

```css
/* Commodities tab, contract picker and Lot summary — flow-only pieces on L3 tokens. */
/* Commodity shortcut (Figma 6754:63662): a 52 white circle, light outline, 32 art (no glow: L3 buttons have no drop shadow) — overrides the L3 Tertiary
   button's size, shape and icon slot on purpose (same exception as the F&O ribbon tabs). */
.shortcut.shortcut { width: var(--app-size-commodity-shortcut); height: var(--app-size-commodity-shortcut); min-width: var(--app-size-commodity-shortcut); padding: 0; --btn-radius: var(--l3-radius-full); --btn-surface: var(--l3-surface-primary); --btn-border: var(--l3-border-light); }
.shortcut.shortcut > span { width: var(--l3-size-32); height: var(--l3-size-32); }
.shortcutArt { display: block; width: var(--l3-size-32); height: var(--l3-size-32); object-fit: contain; }
.change { font: var(--l3-text-label-10); }
.meta { font: var(--l3-text-label-12); color: var(--l3-content-tertiary); white-space: nowrap; }
.pillDivider { flex: none; align-self: stretch; width: 1px; background: var(--l3-border-light); }

/* Contract picker */
.chipArt { display: block; width: var(--l3-size-16); height: var(--l3-size-16); object-fit: contain; }
.rowArt { display: block; width: var(--l3-size-20); height: var(--l3-size-20); object-fit: contain; }
.groupLabel { font: var(--l3-text-heading-12); }
.group { overflow: hidden; border: 1px solid var(--l3-border-light); border-radius: var(--l3-radius-12); }
.chips { padding: var(--l3-spacing-16); }
/* The chips row already brings 16 above the list. */
.pickerBody { padding: 0 var(--l3-spacing-16) var(--l3-spacing-16); }
.pickerBody.equity { padding-top: var(--l3-spacing-16); }

/* Lot summary */
.tabArt { display: block; width: var(--l3-size-16); height: var(--l3-size-16); object-fit: contain; }
.lotBody { padding-block: var(--l3-spacing-24) var(--l3-spacing-32); }
/* ILLIQUID tag on a card: its own tap target (explains illiquid) inside the card's button. */
.tagTap { position: relative; display: inline-flex; cursor: pointer; }
.tagTap::before { content: ''; position: absolute; inset: calc(-1 * var(--l3-spacing-12)) calc(-1 * var(--l3-spacing-04)); }

/* Expiring This Week: a sideways rail of contract cards, each with its expiry tag sitting on the card's top edge.
   The rail runs to the screen edges (cards snap to the 16 inset); the top padding makes room for the tag. */
.expiryRail { display: flex; gap: var(--l3-spacing-12); overflow-x: auto; scroll-snap-type: x mandatory; scroll-padding-inline: var(--l3-spacing-16); margin-inline: calc(-1 * var(--l3-spacing-16)); padding: 0 var(--l3-spacing-16) var(--l3-spacing-04); scrollbar-width: none; }
.expiryRail::-webkit-scrollbar { display: none; }
.expiryItem { position: relative; flex: none; width: calc(100% - var(--l3-spacing-32)); scroll-snap-align: start; }
.expiryItem:only-child { width: 100%; }
.expiryArt { display: block; width: var(--l3-size-32); height: var(--l3-size-32); object-fit: contain; }
.expiryLogo { display: inline-flex; flex: none; align-items: center; justify-content: center; width: var(--l3-size-48); height: var(--l3-size-48); border-radius: var(--l3-radius-full); background: var(--l3-surface-secondary); }
.expirySymbol { font: var(--l3-text-heading-16); white-space: nowrap; }
.expiryRule { height: 1px; background: var(--l3-border-light); }
.expiryLabel { font: var(--l3-text-description-12); color: var(--l3-content-secondary); white-space: nowrap; }
.expiryValue { font: var(--l3-text-heading-14); white-space: nowrap; }
/* The action footer sits 16 under the details, like the card's other parts (L3's footer gives 12: the body's bottom
   padding; local 4 on top — L3 gap, Card has no footer spacing prop). */
.expiryCard[data-footer] > :last-child { padding-top: var(--l3-spacing-04); }
/* Hover greys the whole card (details + buttons), not only the tap body as L3's footer card does — L3 gap. */
@media (hover: hover) {
  .expiryCard[data-footer][data-interactive]:hover {
    background-image: linear-gradient(var(--l3-state-layer-dark-hover), var(--l3-state-layer-dark-hover));
  }
  .expiryCard[data-footer][data-interactive] > :first-child:hover { background-image: none; }
}
.expiryActionIcon { display: inline-flex; width: var(--l3-size-20); height: var(--l3-size-20); }

/* ---- Expiry calendar (fno-38) -----------------------------------------------------------------------------------
 * L3 has no calendar / timeline list (Steps is a progress list) — L3 gap. Left (48): one surface-secondary date block,
 * the weekday over the date (today adds a border-dark ring); beside it one static card per day, its rows split by
 * hairlines, each row 12 from every side with its content centred. */
.calendar { display: flex; flex-direction: column; gap: var(--l3-spacing-16); padding: var(--l3-spacing-12) var(--l3-spacing-16) 0; } /* 12 + the month header's 12 = 24 above the first title */
/* Sticky month header: covers what scrolls under it (screen background), 12 above and below the title (12 above when stuck at the top). */
.calendarMonthHead { position: sticky; top: 0; z-index: 1; padding-block: var(--l3-spacing-12); background: var(--l3-surface-default); }
/* The month title at 20 (heading-20, the user's call 24 Nov), 12 below it: L3 Section header's title is heading-14 with no size option — L3 gap. */
.calendarMonthHead h2 { font: var(--l3-text-heading-20); }
.calendarMonth { display: flex; flex-direction: column; gap: var(--l3-spacing-08); }
/* A 2 line between two months, edge to edge, 24 above (16 gap + 08) and 24 below to the title (12 + the header's 12). */
.calendarMonth + .calendarMonth {
  margin: var(--l3-spacing-08) calc(-1 * var(--l3-spacing-16)) 0;
  padding: var(--l3-spacing-12) var(--l3-spacing-16) 0;
  border-top: var(--app-week-divider) solid var(--l3-border-light);
}
.calendarDate {
  position: sticky; top: calc(var(--calendar-head) + var(--l3-spacing-08)); /* under the month header, while its day is in view */
  box-sizing: border-box; flex: none; width: var(--l3-spacing-48); padding: var(--l3-spacing-08) var(--l3-spacing-04);
  border-radius: var(--l3-radius-12); background: var(--l3-surface-secondary);
}
.calendarDate[data-static] { position: static; } /* the home's Expiring This Week v2: no month header to stick under */
/* Today on the calendar page: the date block inverted (dark fill, light text). The home's short calendar (data-static)
   doesn't mark today. */
.calendarDate[data-today]:not([data-static]) { background: var(--l3-surface-inverted); }
.calendarDate[data-today]:not([data-static]) .calendarWeekday,
.calendarDate[data-today]:not([data-static]) .calendarDay { color: var(--l3-content-inverted); }
.calendarWeekday { font: var(--l3-text-description-12); color: var(--l3-content-secondary); }
.calendarDay { font: var(--l3-text-label-16); color: var(--l3-content-primary); }
.calendarCards { flex: 1; min-width: 0; } /* the calendar page: one card per entry */
.calendarCard.calendarCard { flex: 1; min-width: 0; gap: 0; } /* rows touch: L3 Card's 08 row gap would open a strip between them — the hairline is the only split */
/* L3 Card draws its border as an inset shadow, which a row's hover / press fill would paint over: redraw the same
   border on top of the rows so it stays visible. */
.calendarCard.calendarCard { position: relative; }
.calendarCard::after { content: ''; position: absolute; inset: 0; border-radius: inherit; box-shadow: inset 0 0 0 1px var(--l3-border-light); pointer-events: none; } /* 1px: Figma stroke weight */
.calendarCard > * + * { box-shadow: inset 0 1px 0 var(--l3-border-light); } /* 1px hairline between rows */
.calendarRow { padding: var(--l3-spacing-12); }
.calendarRow[data-tappable] { cursor: pointer; touch-action: manipulation; -webkit-tap-highlight-color: transparent; } /* the same 12 from every side of the card */
/* Each contract row is the tap target: hover and press turn it surface-secondary (the card clips it to its corners). */
.calendarRow[data-tappable]:active { background: var(--l3-surface-secondary); }
@media (hover: hover) { .calendarRow[data-tappable]:hover { background: var(--l3-surface-secondary); } }
.calendarText { flex: 1; min-width: 0; }
.calendarName { flex: 1; min-width: 0; margin: 0; font: var(--l3-text-label-14); color: var(--l3-content-primary); overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
/* An event's name is long ("EIA crude oil inventories"): it wraps to two lines, then ellipsis. */
.calendarName[data-wrap] { white-space: normal; display: -webkit-box; -webkit-box-orient: vertical; -webkit-line-clamp: 2; }
.calendarStat { font: var(--l3-text-label-14); color: var(--l3-content-primary); }
.calendarWhy { margin: 0; font: var(--l3-text-description-12); color: var(--l3-content-secondary); }
/* An event's details line up with its name: past the 24 icon and the 12 gap. */
/* An event's commodities: one row of tags that scrolls sideways (no scrollbar). */
.calendarMoves { overflow-x: auto; scrollbar-width: none; overscroll-behavior-x: contain; }
.calendarMoves::-webkit-scrollbar { display: none; }
/* Under the Previous / Forecast / Actual readings: 10 above the tags (the body's 8 + 2), not tight under the numbers. */
.calendarMoves:not(:first-child) { margin-block-start: var(--l3-spacing-02); }
/* Each commodity as an L3 Tag (arrow + name); it's tappable, so it doesn't shrink and shows a pointer. */
.calendarMoveTag { flex: none; cursor: pointer; -webkit-tap-highlight-color: transparent; }
.calendarEventBody { padding-inline-start: calc(var(--l3-size-24) + var(--l3-spacing-12)); }
.calendarExchange { font: var(--l3-text-description-12); color: var(--l3-content-secondary); }
.calendarIcon { display: inline-flex; width: var(--l3-size-16); height: var(--l3-size-16); }

/* Commodity icon without L3 Avatar's 1px edge (the art has its own shape). L3 gap: Avatar has no borderless option. */
.calendarAvatar::after { box-shadow: none; }
.calendarAvatar.calendarAvatar > span { color: var(--l3-content-primary); } /* the event icon in content-primary (user, 2026-11-24): L3 Avatar draws icons in a faded secondary */
/* Expiring This Week, version 2 (home): the first days of the calendar, 12 between days. */
.expiryCalendarPreview { display: flex; flex-direction: column; gap: var(--l3-spacing-16); } /* 16 between two days */
/* Expiring This Week, version 3 (home): the same days in ONE card. Each day is a band: the date as the card's grey
   left column (full height of the day, attached edge to edge), the day's rows beside it; hairlines between days
   (full width, across the date column too) and between rows (rows only). Every date has the same weight (no today marker). */
.calendarJoined.calendarJoined { position: relative; gap: 0; overflow: hidden; }
.calendarJoined::after { content: ''; position: absolute; inset: 0; border-radius: inherit; box-shadow: inset 0 0 0 1px var(--l3-border-light); pointer-events: none; } /* 1px card edge over the fills */
.calendarJoinedDay { display: flex; align-items: stretch; }
.calendarJoinedDay + .calendarJoinedDay { border-top: 1px solid var(--l3-border-light); } /* 1px between days: a border, so it also crosses the grey date column */
.calendarJoinedDate.calendarJoinedDate { flex: none; box-sizing: border-box; width: var(--l3-spacing-48); justify-content: center; padding: var(--l3-spacing-08) var(--l3-spacing-04); background: var(--l3-surface-secondary); }
.calendarJoinedRows { flex: 1; min-width: 0; display: flex; flex-direction: column; }
.calendarJoinedRows > * + * { box-shadow: inset 0 1px 0 var(--l3-border-light); } /* 1px between rows of a day */

/* fno-38: the body slides with the tabs. The track holds the current tab's body with the tabs next door just off-screen
   either side (clip, not hidden, so the sticky month / date blocks still stick to the page's scroll). */
.calendarViewport { overflow-x: clip; min-height: 100%; }
.calendarTrack { position: relative; min-height: 100%; }
.calendarPanel[data-side='before'], .calendarPanel[data-side='after'] { position: absolute; inset-block-start: 0; inline-size: 100%; }
.calendarPanel[data-side='before'] { inset-inline-start: -100%; }
.calendarPanel[data-side='after'] { inset-inline-start: 100%; }
/* Expiring This Week, version 4 (home): the week's days as a row of date cards (48 wide, the calendar's date block
   size), 08 apart, scrolling sideways; the selected one border-dark on surface-secondary, the others border-light. L3 has no
   date strip / day chip — L3 gap. Under it the selected day's card (.calendarCard). */
/* Full bleed: the row runs to the screen edges (out through the section's 16 inset), the first and last day still 16 in. */
.dayPicker { display: flex; gap: var(--l3-spacing-10); margin-inline: calc(-1 * var(--l3-spacing-16)); padding-inline: var(--l3-spacing-16); overflow-x: auto; scrollbar-width: none; overscroll-behavior-x: contain; }
.dayPicker::-webkit-scrollbar { display: none; }
/* Fades at the ends of the day row, only on a side with more to scroll to (ExpiringDayPicker sets data-more-before /
   data-more-after as it scrolls): the cards melt out instead of being cut. A mask, so it works on any background; black
   here is mask opacity, not a colour. */
.dayPicker { --fade-before: 0px; --fade-after: 0px; mask-image: linear-gradient(to right, transparent, black var(--fade-before), black calc(100% - var(--fade-after)), transparent); }
.dayPicker[data-more-before] { --fade-before: var(--l3-spacing-24); }
.dayPicker[data-more-after] { --fade-after: var(--l3-spacing-24); }
.dayPickerDay { position: relative; overflow: hidden; flex: none; display: flex; flex-direction: column; align-items: center; width: var(--l3-spacing-48); padding: var(--l3-spacing-08) 0; border: 1px solid var(--l3-border-light); border-radius: var(--l3-radius-12); background: var(--l3-surface-primary); cursor: pointer; font: inherit; color: inherit; -webkit-tap-highlight-color: transparent; }
.dayPickerDay[aria-selected='true'] { border-color: var(--l3-border-dark); background: var(--l3-surface-secondary); } /* selected: dark border, grey fill */
@media (hover: hover) { .dayPickerDay[aria-selected='false']:hover { background: var(--l3-surface-secondary); } }
.dayPickerDay:focus-visible { outline: 2px solid var(--l3-border-dark); outline-offset: 2px; }
.expiringViewAll.expiringViewAll { flex: none; } /* View all keeps its full label; the SectionHeader (width 100%) gives way */
/* V4: the pill that opens each later week ("NEXT WEEK", "7 DEC"), after the reference's month pill: grey
   (surface-secondary), fully rounded, as tall as the date cards, the text turned 90° (bottom to top), 8 upper
   case (Description 10 at L3's local 8 size), content-primary — a thin pill. */
.dayPickerWeek { flex: none; margin-left: var(--l3-spacing-08); /* 8 more before a new week (18 from the last day) */ display: flex; align-items: center; justify-content: center; padding: 0 var(--l3-spacing-04); border-radius: var(--l3-radius-full); background: var(--l3-surface-secondary); writing-mode: vertical-rl; transform: rotate(180deg); white-space: nowrap; text-transform: uppercase; font: var(--l3-text-description-10); font-size: var(--l3-font-size-local-08); line-height: 1; letter-spacing: 0.04em; color: var(--l3-content-primary); }
/* Commodity calendar V4 (fno-38): week sections split by a 2 line (border-light) running edge to edge — out through the
   page's 16 inset — with 24 on either side of it (the Stack's 24 above, this 24 below): 48 between two weeks. */
/* archived (archive/DayPickerByWeek.tsx) */ .weekSection + .weekSection { margin-inline: calc(-1 * var(--l3-spacing-16)); padding: var(--l3-spacing-24) var(--l3-spacing-16) 0; border-top: var(--app-week-divider) solid var(--l3-border-light); }
```

### `src/flows/fno/commodities/components/CommoditiesFeed.tsx`

```tsx
import { Stack } from '@l3/components/Stack'
import { ContractSection, type Choose } from '../../components/ContractSection'
import { Watchlists } from '../../components/Discovery'
import { TradingChart } from '../../components/TradingChart'
import type { Contract, Watchlist } from '../../data'
import { t } from '../../copy'
import { smartFutures, type Commodity, type ExpiringContract } from '../data'
import { CommodityHeatmap } from './CommodityHeatmap'
import { CommodityShortcuts } from './CommodityShortcuts'
import { ExpiringCalendar } from './ExpiringCalendar'
import { ExpiringCalendarCard } from './ExpiringCalendarCard'
import { ExpiringDayPicker } from './ExpiringDayPicker'
import { ExpiringThisWeek } from './ExpiringThisWeek'
import { useFlowOption } from '../../../../shared/prototype'
import { PopularCommodities } from './PopularCommodities'
import parts from '../../components/HomeParts.module.css'

type Props = {
  /** The contract the chart shows ("Gold"); its selector opens the contract picker. */
  instrument: string
  lists: Watchlist[]
  onCommodity: (commodity: Commodity) => void
  onAsset: () => void
  onPicker: () => void
  onChoose: Choose
  onContract: (contract: Contract) => void
  onDestination: (name: string) => void
  onAddWatchlist: () => void
  onChain: () => void
  onScalper: () => void
  /** Expiring This Week's View all → the Upcoming expiries timeline. */
  onExpiries: () => void
  /** An Expiring card's trend read-out → the trend info sheet. */
  onTrendInfo: (contract: ExpiringContract) => void
}

/** The Commodities tab of F&O home (Figma 6754:63637), under the shared header, P&L, indices and product tabs. */
export function CommoditiesFeed({ instrument, lists, onCommodity, onAsset, onPicker, onChoose, onContract, onDestination, onAddWatchlist, onChain, onScalper, onExpiries, onTrendInfo }: Props) {
  // Prototype setting “Expiring This Week”: Version 1 = the card rail, Version 2 = the short calendar,
  // Version 3 = that calendar in one card (dates attached as its left column). Version 4 = a row of day
  // cards, the selected day's entries below.
  const expiringVersion = useFlowOption('fno', 'expiringVersion', 'v4')
  return <Stack gap="32" className={parts.feed}>
    <CommodityShortcuts onOpen={onCommodity} />
    {expiringVersion === 'v4'
      ? <ExpiringDayPicker onAsset={onAsset} onOptionChain={onChain} onScalper={onScalper} onViewAll={onExpiries} />
      : expiringVersion === 'v3'
      ? <ExpiringCalendarCard onAsset={onAsset} onOptionChain={onChain} onScalper={onScalper} onViewAll={onExpiries} />
      : expiringVersion === 'v2'
      ? <ExpiringCalendar onAsset={onAsset} onOptionChain={onChain} onScalper={onScalper} onViewAll={onExpiries} />
      : <ExpiringThisWeek onAsset={onAsset} onContract={onContract} onScalper={onScalper} onViewAll={onExpiries} onTrendInfo={onTrendInfo} />}
    <TradingChart instrument={instrument} onInstrument={onPicker} onChoose={onChoose} onDestination={onDestination} onChain={onChain} onScalper={onScalper} />
    <div className={parts.divider} />
    <div data-fno="watchlists"><Watchlists lists={lists} onAdd={onAddWatchlist} onOpen={onDestination} /></div>
    <div data-fno="options"><PopularCommodities onChoose={onChoose} onContract={onContract} onViewAll={() => onDestination(t('commodities.popular'))} /></div>
    <div data-fno="heatmap"><CommodityHeatmap onOpen={onDestination} onViewAll={() => onDestination(t('heatmap.title'))} /></div>
    <div data-fno="futures"><ContractSection kind="futures" contracts={smartFutures} onChoose={onChoose} onContract={onContract} onViewAll={() => onDestination(t('futures.title'))} /></div>
  </Stack>
}
```

### `src/flows/fno/commodities/components/CommodityHeatmap.tsx`

```tsx
import { useState } from 'react'
import { Card } from '@l3/components/Card'
import { SectionHeader } from '@l3/components/SectionHeader'
import { Tabs } from '@l3/components/Tabs'
import { t } from '../../copy'
import { heatmapGroups } from '../data'
import parts from '../../components/HomeParts.module.css'

type Group = keyof typeof heatmapGroups

/** Futures Heatmap on the Commodities tab: Bullion / Energy / Metals pills (no Stock ⇕ Index switch) over the 3-column tiles. */
export function CommodityHeatmap({ onOpen, onViewAll }: { onOpen: (name: string) => void; onViewAll: () => void }) {
  const [group, setGroup] = useState<Group>('bullion')
  return <section className={parts.heatmapSection} aria-label={t('heatmap.title')}>
    <div className={parts.inset}><SectionHeader title={t('heatmap.title')} action={{ type: 'view-all', label: t('viewAll'), onClick: onViewAll }} /></div>
    <div className={parts.heatmapRow}><Tabs appearance="pill" size="sm" aria-label={t('heatmap.title')} value={group} onChange={setGroup} items={(['bullion', 'energy', 'metals'] as const).map((value) => ({ value, label: t(`heatmap.${value}`) }))} /></div>
    <div className={parts.heatmap}>{heatmapGroups[group].map((cell) => <Card variant="flat" key={cell.id} className={[parts.heatCell, cell.tone === 'up' ? parts.heatUp : parts.heatDown].join(' ')} onClick={() => onOpen(cell.name)}>
      <span className={parts.heatName}>{cell.name}</span><span><strong>{cell.change.toFixed(2)}%</strong><span className={parts.heatPrice}>{cell.price}</span></span>
    </Card>)}</div>
  </section>
}
```

### `src/flows/fno/commodities/components/CommodityShortcuts.tsx`

```tsx
import { Button } from '@l3/components/Button'
import { Grid } from '@l3/components/Grid'
import { Inset } from '@l3/components/Inset'
import { Stack } from '@l3/components/Stack'
import { t } from '../../copy'
import { commodities, type Commodity } from '../data'
import parts from '../../components/HomeParts.module.css'
import styles from './Commodities.module.css'

/** Gold · Silver · Crude Oil · Natural Gas, four across: artwork in a round Tertiary button, the name and the day's change
 *  under it. Its own 16-gutter 4-column Grid (24 Nov: the shared .shortcuts class lost its row when Equity moved to ShortcutCircles). */
export function CommodityShortcuts({ onOpen }: { onOpen: (commodity: Commodity) => void }) {
  return <div className={parts.shortcuts}><Inset paddingInline="16" paddingBlock="00"><Grid columns={4} gap="08" role="list" aria-label={t('commodities.shortcuts')}>{commodities.map((commodity) => <Stack key={commodity.id} gap="08" align="center" role="listitem">
    <Button variant="tertiary" size="lg" className={styles.shortcut} aria-label={commodity.name} iconLeft={<img className={styles.shortcutArt} src={commodity.image} alt="" />} onClick={() => onOpen(commodity)} />
    <Stack gap="04" align="center">
      <span className={parts.secondaryLabel}>{commodity.name}</span>
      <span className={[styles.change, commodity.change < 0 ? parts.down : parts.up].join(' ')}>{commodity.change > 0 ? '+' : ''}{commodity.change.toFixed(2)}%</span>
    </Stack>
  </Stack>)}</Grid></Inset></div>
}
```

### `src/flows/fno/commodities/components/ExpiringCalendar.tsx`

```tsx
import { ExpiringHeader } from './ExpiringHeader'
import { t } from '../../copy'
import { expiryCalendarAll, expiryPreview } from '../data'
import { CalendarDay } from './CalendarDay'
import parts from '../../components/HomeParts.module.css'
import styles from './Commodities.module.css'

/**
 * Expiring This Week, version 2 — the Commodities home section as a short calendar instead of the card rail: the
 * calendar's first 3 entries (`expiryPreview`), on their days (the grey date block on the left, one card per contract or event, 8 apart), so
 * it's three rows on one day or spread over two or three days. Events first within a day and on one line (time ·
 * country, impact); contracts as on the calendar page (option chain + ScalpPro, row → asset page). View all → the
 * Commodity calendar (fno-38) with everything. Prototype setting "Expiring This Week" picks Version 1 (cards) or 2.
 */
export function ExpiringCalendar({ onAsset, onOptionChain, onScalper, onViewAll }: { onAsset: () => void; onOptionChain: () => void; onScalper: () => void; onViewAll: () => void }) {
  return <section className={parts.contractSection} aria-label={t('expiring.title')}>
    <ExpiringHeader onViewAll={onViewAll} />
    <div className={styles.expiryCalendarPreview}>
      {expiryPreview(3, expiryCalendarAll).map((day) => <CalendarDay key={day.inDays} day={day} showKind sticky={false} eventDetails={false} separate onAsset={onAsset} onOptionChain={onOptionChain} onScalper={onScalper} />)}
    </div>
  </section>
}
```

### `src/flows/fno/commodities/components/ExpiringCalendarCard.tsx`

```tsx
import { Card } from '@l3/components/Card'
import { ExpiringHeader } from './ExpiringHeader'
import { t } from '../../copy'
import { expiryCalendarAll, expiryPreview } from '../data'
import { CalendarDate, CalendarEntry } from './CalendarDay'
import parts from '../../components/HomeParts.module.css'
import styles from './Commodities.module.css'

/**
 * Expiring This Week, version 3 — the version 2 short calendar (the calendar's first 3 entries on their days, events
 * first and on one line) in ONE card: each day is a band with the date as the card's grey left column, attached edge
 * to edge and as tall as the day's rows, and the rows beside it; hairlines between days and between rows. Rows act as
 * on the calendar page (option chain + ScalpPro, row → asset page). View all → the Commodity calendar (fno-38).
 */
export function ExpiringCalendarCard({ onAsset, onOptionChain, onScalper, onViewAll }: { onAsset: () => void; onOptionChain: () => void; onScalper: () => void; onViewAll: () => void }) {
  return <section className={parts.contractSection} aria-label={t('expiring.title')}>
    <ExpiringHeader onViewAll={onViewAll} />
    <Card padding="none" className={styles.calendarJoined}>
      {expiryPreview(3, expiryCalendarAll).map((day) => <div key={day.inDays} className={styles.calendarJoinedDay}>
        <CalendarDate inDays={day.inDays} className={styles.calendarJoinedDate} />
        <div className={styles.calendarJoinedRows}>
          {day.entries.map((c) => <CalendarEntry key={c.id} entry={c} showKind eventDetails={false} onAsset={onAsset} onOptionChain={onOptionChain} onScalper={onScalper} />)}
        </div>
      </div>)}
    </Card>
  </section>
}
```

### `src/flows/fno/commodities/components/ExpiringDayPicker.tsx`

```tsx
import { Fragment, useEffect, useRef, useState } from 'react'
import { Card } from '@l3/components/Card'
import { Stack } from '@l3/components/Stack'
import { ExpiringHeader } from './ExpiringHeader'
import { t } from '../../copy'
import { expiryCalendarAll, type ExpiryDay } from '../data'
import { CalendarEntry, dayFrom } from './CalendarDay'
import parts from '../../components/HomeParts.module.css'
import styles from './Commodities.module.css'

/** How far ahead the home's day row reaches: about a month. */
const DAYS_AHEAD = 31

/** Today's place in its calendar week (weeks run Monday to Sunday): Mon 0 … Sun 6. */
export const todayInWeek = () => (new Date().getDay() + 6) % 7

/** Days grouped by calendar week (0 = this week, 1 = next week …), in order. */
export function byWeek(days: ExpiryDay[]): { week: number; days: ExpiryDay[] }[] {
  const weeks: { week: number; days: ExpiryDay[] }[] = []
  for (const day of days) {
    const week = Math.floor((day.inDays + todayInWeek()) / 7)
    const last = weeks[weeks.length - 1]
    if (last?.week === week) last.days.push(day)
    else weeks.push({ week, days: [day] })
  }
  return weeks
}

/** The pill before a week: "Next week", then that week's Monday ("7 Dec") — short, so the turned text fits the row. */
function weekLabel(week: number) {
  if (week === 1) return t('expiring.nextWeek')
  return dayFrom(week * 7 - todayInWeek()).toLocaleDateString('en-IN', { day: 'numeric', month: 'short' })
}

/**
 * The day picker (Expiring This Week version 4, the default): the given days (only days that
 * have something, so every card leads somewhere) as a row of small date cards, scrolling sideways. Weeks run Monday to
 * Sunday; each week after this one starts with a thin grey pill, its text turned 90° (bottom to top, upper case, 8):
 * "NEXT WEEK", then the week's Monday ("7 DEC"). The selected day has a dark border on grey; the first day is selected
 * first (no count tag — removed 24 Nov). Under the row, that day's contracts and events, one card each (8 apart).
 */
export function DayPicker({ days, weekPills = true, showKind, eventDetails, onAsset, onOptionChain, onScalper }: {
  days: ExpiryDay[]
  /** The "NEXT WEEK" / "7 DEC" pills between weeks — off when the days are one week already (the calendar page's week sections). */
  weekPills?: boolean
  /** Tag each row with its kind (Options / Futures / Event) — when the days mix kinds. */
  showKind: boolean
  /** Events show their figures (previous / forecast / actual) — on the calendar page, not on the home. */
  eventDetails: boolean
  onAsset: () => void
  onOptionChain: () => void
  onScalper: () => void
}) {
  const [selected, setSelected] = useState(days[0]?.inDays ?? 0)
  const day = days.find((d) => d.inDays === selected) ?? days[0]
  // The row's ends fade on a side with more to scroll to (data-more-before / -after → the CSS mask), checked on scroll and resize.
  const row = useRef<HTMLDivElement>(null)
  const updateFades = () => {
    const el = row.current
    if (!el) return
    el.toggleAttribute('data-more-before', el.scrollLeft > 1)
    el.toggleAttribute('data-more-after', el.scrollLeft + el.clientWidth < el.scrollWidth - 1)
  }
  useEffect(() => {
    updateFades()
    const observer = new ResizeObserver(updateFades)
    if (row.current) observer.observe(row.current)
    return () => observer.disconnect()
  }, [days])
  return <>
    <div ref={row} onScroll={updateFades} role="tablist" aria-label={t('expiring.days')} className={styles.dayPicker}>
      {byWeek(days).map((w) => <Fragment key={w.week}>
        {weekPills && w.week > 0 && <span className={styles.dayPickerWeek} aria-hidden>{weekLabel(w.week)}</span>}
        {w.days.map((d) => {
          const date = dayFrom(d.inDays)
          const active = d.inDays === day?.inDays
          return <button key={d.inDays} type="button" role="tab" aria-selected={active} className={styles.dayPickerDay}
            aria-label={date.toLocaleDateString('en-IN', { weekday: 'long', day: 'numeric', month: 'long' })}
            onClick={() => setSelected(d.inDays)}>
            <span className={styles.calendarWeekday}>{date.toLocaleDateString('en-IN', { weekday: 'short' })}</span>
            <span className={styles.calendarDay}>{date.getDate()}</span>
          </button>
        })}
      </Fragment>)}
    </div>
    {day && <Stack gap="08">
      {day.entries.map((c) => <Card key={c.id} padding="none" className={styles.calendarCard}>
        <CalendarEntry entry={c} showKind={showKind} eventDetails={eventDetails} onAsset={onAsset} onOptionChain={onOptionChain} onScalper={onScalper} />
      </Card>)}
    </Stack>}
  </>
}

/**
 * Expiring This Week, version 4 — the day picker over the next month (contracts with option chain + ScalpPro, events
 * on one line). View all → the Commodity calendar (fno-38), the day list (one card per contract or event).
 */
export function ExpiringDayPicker({ onAsset, onOptionChain, onScalper, onViewAll }: { onAsset: () => void; onOptionChain: () => void; onScalper: () => void; onViewAll: () => void }) {
  return <section className={parts.contractSection} aria-label={t('expiring.title')}>
    <ExpiringHeader onViewAll={onViewAll} />
    <DayPicker days={expiryCalendarAll.filter((d) => d.inDays < DAYS_AHEAD)} showKind eventDetails={false} onAsset={onAsset} onOptionChain={onOptionChain} onScalper={onScalper} />
  </section>
}
```

### `src/flows/fno/commodities/components/ExpiringHeader.tsx`

```tsx
import { Button } from '@l3/components/Button'
import { Icon } from '@l3/components/Icon'
import { SectionHeader } from '@l3/components/SectionHeader'
import { Stack } from '@l3/components/Stack'
import { msCalendarMonth } from '@l3/icons/material'
import { t } from '../../copy'
import styles from './Commodities.module.css'

/**
 * Expiring This Week's header (all four versions): the L3 SectionHeader title, and View all as a Ghost Small button with
 * a calendar icon BEFORE the label (it opens the Commodity calendar, fno-38). L3's SectionHeader `view-all` action only
 * takes a chevron after the label, so the button sits beside the header instead — L3 gap.
 */
export function ExpiringHeader({ onViewAll }: { onViewAll: () => void }) {
  return <Stack direction="horizontal" gap="08" align="center" justify="between">
    <SectionHeader title={t('expiring.title')} />
    <Button variant="ghost" size="sm" className={styles.expiringViewAll} onClick={onViewAll} iconLeft={<Icon icon={msCalendarMonth} />}>{t('viewAll')}</Button>
  </Stack>
}
```

### `src/flows/fno/commodities/components/ExpiringThisWeek.tsx`

```tsx
import { Button } from '@l3/components/Button'
import { Card } from '@l3/components/Card'
import { MaskIcon } from '@l3/components/MaskIcon'
import { PriceChange } from '@l3/components/PriceChange'
import { ExpiringHeader } from './ExpiringHeader'
import { Stack } from '@l3/components/Stack'
import { inr } from '../../../../shared/data/format'
import { useFlowOption } from '../../../../shared/prototype'
import type { Contract } from '../../data'
import { t } from '../../copy'
import { expiringThisWeek, type ExpiringContract } from '../data'
import scalper from '../../assets/scalppro.svg'
import { TrendBadge } from '../../components/TrendBadge'
import { trendLabel, trendSince } from '../sheets/TrendInfoSheet'
import parts from '../../components/HomeParts.module.css'
import styles from './Commodities.module.css'

/** The commodity art on the left of each card — hidden for now (kept, not deleted). */
const SHOW_ART = false

/** The expiry line's day: Today, Tomorrow, then the weekday ("Thu"). */
function expiryDay(days: number) {
  if (days === 0) return t('expiring.today')
  if (days === 1) return t('expiring.tomorrow')
  const date = new Date()
  date.setDate(date.getDate() + days)
  return date.toLocaleDateString('en-IN', { weekday: 'short' })
}

/** The card as a contract, for the contract sheet (Buy). */
const asContract = (c: ExpiringContract): Contract => c.kind !== 'future'
  ? { id: c.id, name: `${c.symbol} ${c.option}`, description: c.description, price: c.price, change: c.priceChange, volume: 0, side: c.option.includes(' PE') ? 'put' : 'call' }
  : { id: c.id, name: c.symbol, description: c.description, price: c.price, change: c.priceChange, volume: 0 }

/** The card's variant: the expiry line under the symbol and the left column's label (the option, or LTP for a future). */
const expiryLine = (c: ExpiringContract) =>
  c.kind === 'option' ? t('expiring.tag', { day: expiryDay(c.expiresInDays) })
  : c.kind === 'event' ? t('expiring.eventTag', { event: c.event, day: expiryDay(c.eventInDays), time: c.eventTime })
  : t('expiring.futTag', { date: c.expiryDate })
const priceLabel = (c: ExpiringContract) => c.kind === 'future' ? t('expiring.ltp') : c.option

/**
 * Expiring This Week — the Commodities tab's section between the commodity shortcuts and the chart: a sideways rail
 * of contracts whose options expire this week. Each card: the commodity with when its options expire (plain text,
 * "OPT Expiry Today" / "FUT Expiry 3 Dec"), the trend since when it started, the option's premium or the future's LTP
 * (left) and the margin per lot
 * (right), each a label over its value, then
 * View all opens the Upcoming expiries timeline (fno-38). The trend read-out (top right, with its i) opens the trend info sheet. ScalpPro and Buy in the card's action footer (no fill); the three parts sit 16 apart. A tap on the card opens the contract's asset page.
 */
export function ExpiringThisWeek({ onAsset, onContract, onScalper, onViewAll, onTrendInfo }: { onAsset: () => void; onContract: (contract: Contract) => void; onScalper: () => void; /** The trend read-out (Strong Uptrend / Bullish …, the whole top right) → the trend info sheet. */ onTrendInfo: (contract: ExpiringContract) => void; /** View all → the Upcoming expiries timeline (fno-38). */ onViewAll: () => void }) {
  // Prototype setting “Expiring card buttons”: off hides the whole ScalpPro + Buy footer.
  const showButtons = useFlowOption('fno', 'expiringButtons', 'on') === 'on'
  return <section className={parts.contractSection} aria-label={t('expiring.title')}>
    <ExpiringHeader onViewAll={onViewAll} />
    <div className={styles.expiryRail}>
      {expiringThisWeek.map((c) => <div key={c.id} className={styles.expiryItem}>
        <Card
          className={styles.expiryCard}
          onClick={onAsset}
          aria-label={`${c.symbol} ${priceLabel(c)}`}
          footer={showButtons ? <>
            <Button variant="secondary" size="md" fullWidth iconLeft={<span className={styles.expiryActionIcon}><MaskIcon src={scalper} /></span>} onClick={onScalper}>{t('chart.scalper')}</Button>
            <Button variant="primary" size="md" fullWidth onClick={() => onContract(asContract(c))}>{t('expiring.buy')}</Button>
          </> : undefined}
        >
          <Stack gap="16">
            <Stack direction="horizontal" gap="12" align="center">
              {SHOW_ART && <span className={styles.expiryLogo}><img className={styles.expiryArt} src={c.image} alt="" /></span>}
              <Stack gap="04" className={parts.grow}>
                <p className={styles.expirySymbol}>{c.symbol}</p>
                <p className={parts.description}>{expiryLine(c)}</p>
              </Stack>
              <TrendBadge trend={c.trend} label={trendLabel(c)} since={trendSince(c)} largeSince info={t('expiring.sinceInfo')} onInfo={() => onTrendInfo(c)} />
            </Stack>
            <div className={styles.expiryRule} />
            <Stack direction="horizontal" gap="12" justify="between">
              <Stack gap="04"><span className={styles.expiryLabel}>{priceLabel(c)}</span><Stack direction="horizontal" gap="08" align="center"><span className={styles.expiryValue}>{inr(c.price)}</span><PriceChange value={c.priceChange} unit="percent" size="md" /></Stack></Stack>
              <Stack gap="04" align="end"><span className={styles.expiryLabel}>{t('expiring.margin')}</span><span className={styles.expiryValue}>{inr(c.margin)}</span></Stack>
            </Stack>
          </Stack>
        </Card>
      </div>)}
    </div>
  </section>
}
```

### `src/flows/fno/commodities/components/PopularCommodities.tsx`

```tsx
import { useState } from 'react'
import { Button } from '@l3/components/Button'
import { Card } from '@l3/components/Card'
import { Icon } from '@l3/components/Icon'
import { PriceChange } from '@l3/components/PriceChange'
import { SectionHeader } from '@l3/components/SectionHeader'
import { Select } from '@l3/components/Select'
import { Stack } from '@l3/components/Stack'
import { Tab, Tabs } from '@l3/components/Tabs'
import { lmSwitchArrowVertical } from '@l3/icons/lemonnade'
import { msFilterList } from '@l3/icons/material'
import { inr } from '../../../../shared/data/format'
import type { Choose } from '../../components/ContractSection'
import { t } from '../../copy'
import { popularFutures, popularOptions, type CommodityContract } from '../data'
import parts from '../../components/HomeParts.module.css'
import styles from './Commodities.module.css'

/**
 * Popular commodities: Options ⇕ Futures switch, category pills, Filter + sort, contract cards. A future's card shows
 * price and change on one line with its margin per lot under it.
 */
export function PopularCommodities({ onChoose, onContract, onViewAll }: { onChoose: Choose; onContract: (contract: CommodityContract) => void; onViewAll: () => void }) {
  const [futures, setFutures] = useState(false)
  const [category, setCategory] = useState('top')
  const [volume, setVolume] = useState(false)
  const [filter, setFilter] = useState(t('filter.all'))
  const categories = (['top', 'gainers', 'losers', 'advanced'] as const).map((value) => ({ value, label: t(`commodities.${value}`) }))
  const source = futures ? popularFutures : popularOptions
  const filterChoices = [t('filter.all'), t('filter.gainers'), t('filter.losers')]
  const matching = source.filter((c) => filter === t('filter.gainers') ? c.change > 0 : filter === t('filter.losers') ? c.change < 0 : true)
  const offset = categories.findIndex((c) => c.value === category)
  const ordered = category === 'top' ? matching : [...matching.slice(offset), ...matching.slice(0, offset)]
  const rows = volume ? [...ordered].sort((a, b) => b.volume - a.volume) : ordered
  return <section className={parts.contractSection} aria-label={t('commodities.popular')}>
    <SectionHeader title={t('commodities.popular')} action={{ type: 'view-all', label: t('viewAll'), onClick: onViewAll }} />
    <Stack direction="horizontal" gap="08" align="center" className={parts.filterRow}>
      <Tab appearance="pill" size="sm" emphasis="secondary" action iconRight={<Icon icon={lmSwitchArrowVertical} size={12} />} onClick={() => setFutures(!futures)} aria-label={t('commodities.segment')}>{t(futures ? 'commodities.futures' : 'commodities.options')}</Tab>
      <span className={styles.pillDivider} aria-hidden />
      <Tabs aria-label={t('commodities.popular')} appearance="pill" size="sm" items={categories} value={category} onChange={setCategory} />
    </Stack>
    <Stack direction="horizontal" align="center" justify="between">
      <Button variant="ghost" size="sm" iconLeft={<Icon icon={msFilterList} size={12} />} onClick={() => onChoose(t('filter'), filterChoices, filter, setFilter)}>{filter === t('filter.all') ? t('filter') : filter}</Button>
      <Select size="sm" aria-label={t('sort.label')} onClick={() => setVolume(!volume)}>{t(volume ? 'sort.volume' : 'sort.price')}</Select>
    </Stack>
    <Stack gap="12">{rows.map((contract) => <Card key={contract.id} onClick={() => onContract(contract)}>
      <Stack direction="horizontal" gap="08" justify="between" align="center">
        <Stack gap="04" className={parts.grow}><p className={parts.heading}>{contract.name}</p><p className={parts.description}>{contract.description}</p></Stack>
        {contract.margin
          ? <Stack gap="04" align="end"><Stack direction="horizontal" gap="04" align="center"><p className={parts.heading}>{volume ? contract.volume.toLocaleString('en-IN') : inr(contract.price, 2)}</p><PriceChange value={contract.change} unit="percent" size="md" /></Stack><p className={styles.meta}>{t('commodities.margin', { margin: contract.margin })}</p></Stack>
          : <Stack gap="04" align="end"><p className={parts.heading}>{volume ? contract.volume.toLocaleString('en-IN') : inr(contract.price, 2)}</p><PriceChange value={contract.change} unit="percent" size="sm" /></Stack>}
      </Stack>
    </Card>)}</Stack>
  </section>
}
```

### `src/flows/fno/commodities/data.ts`

```ts
import type { Contract } from '../data'
import gold from './assets/gold.png'
import silver from './assets/silver.png'
import crudeOil from './assets/crude-oil.png'
import naturalGas from './assets/natural-gas.png'
import goldMini from './assets/gold-mini.png'
import goldDefault from './assets/gold-default.png'
import goldGuinea from './assets/gold-guinea.png'
import goldPetal from './assets/gold-petal.png'
import goldTen from './assets/gold-ten.png'

/** Snapshot examples from Figma 6754:63073 (F&O Home → Commodities); these are not live quotes. */

/** The four commodity shortcuts under the product tabs. `change` is the day's percent change. */
export type Commodity = { id: string; name: string; change: number; image: string }
export const commodities: Commodity[] = [
  { id: 'gold', name: 'Gold', change: -5.17, image: gold },
  { id: 'silver', name: 'Silver', change: 1.58, image: silver },
  { id: 'crude', name: 'Crude Oil', change: 4.12, image: crudeOil },
  { id: 'gas', name: 'Natural Gas', change: 2.43, image: naturalGas },
]

/** Popular commodities. Options shows the Figma frame's rows as drawn (one future among the calls); `margin` is the margin per lot. */
export type CommodityContract = Contract & { margin?: string }
export const popularOptions: CommodityContract[] = [
  { id: 'pop-0', name: 'GOLD 19400 CE', description: 'Call | 14 Jan 26', price: 417, change: 0.1, volume: 23843233, side: 'call' },
  { id: 'pop-1', name: 'GOLD FUT', description: 'Future | 14 Jan 26', price: 417, change: 0.1, volume: 21102400, margin: '1,65,450.23' },
  { id: 'pop-2', name: 'GOLD 19400 CE', description: 'Call | 14 Jan 26', price: 417, change: 0.1, volume: 19640000, side: 'call' },
  { id: 'pop-3', name: 'GOLD 19400 CE', description: 'Call | 14 Jan 26', price: 417, change: 0.1, volume: 17220500, side: 'call' },
]
export const popularFutures: CommodityContract[] = ['GOLD FUT', 'SILVER FUT', 'CRUDEOIL FUT', 'NATURALGAS FUT'].map((name, i) => ({ id: `popf-${i}`, name, description: 'Future | 14 Jan 26', price: 417, change: 0.1, volume: 21102400 - i * 1800000, margin: '1,65,450.23' }))

/** Smart Futures on the Commodities tab. */
export const smartFutures: Contract[] = Array.from({ length: 4 }, (_, i) => ({ id: `cfut-${i}`, name: 'GOLD 19400 CE', description: 'Call | 14 Jan 26', price: 417, change: 0.1, volume: 15400 + i * 1900, side: 'call' }))

/** Futures Heatmap tiles per group. Up / down colour follows each tile's tone, as in the frame. */
export type HeatTile = { id: string; name: string; change: number; price: string; tone: 'up' | 'down' }
const tile = (name: string, i: number): HeatTile => ({ id: `${name}-${i}`, name, change: -0.27, price: '2,817.40', tone: i % 2 ? 'up' : 'down' })
export const heatmapGroups: Record<'bullion' | 'energy' | 'metals', HeatTile[]> = {
  bullion: ['GOLD MINI', 'GOLD MICRO', 'GOLD', 'SILVER MINI', 'ZINC', 'SILVER MICRO', 'SILVER', 'ZINC MACRO', 'ZINC LARGE'].map(tile),
  energy: ['CRUDEOIL', 'CRUDEOIL MINI', 'NATURALGAS', 'NATGAS MINI', 'CRUDEOIL', 'NATURALGAS'].map(tile),
  metals: ['COPPER', 'ALUMINIUM', 'ZINC', 'LEAD', 'NICKEL', 'ALUMINI'].map(tile),
}

/** The contract picker ("Choose options contract"): Equity indices, and Commodities grouped by commodity. */
export type PickerContract = { id: string; name: string; price: string; change: number; image?: string; tag?: string }
export const equityContracts: PickerContract[] = ['NIFTY 50', 'BSE Sensex', 'Nifty Bank', 'Nifty Financial Services', 'Nifty Midcap Select', 'BSE BANKEX', 'Nifty Next 50', 'BSE Sensex 50'].map((name) => ({ id: name, name, price: '₹1,42,557.00', change: -0.68 }))
export type CommodityGroup = { id: string; name: string; image?: string; contracts: PickerContract[] }
const contract = (name: string, image?: string, tag?: string): PickerContract => ({ id: name, name, price: '₹1,42,557.00', change: 0.68, image, tag })
export const commodityGroups: CommodityGroup[] = [
  { id: 'gold', name: 'Gold', image: gold, contracts: [contract('Gold Mini', goldMini, 'Lowest Margin'), contract('Gold', goldDefault), contract('Gold Guinea', goldGuinea), contract('Gold Petal', goldPetal), contract('Gold Ten', goldTen)] },
  { id: 'silver', name: 'Silver', image: silver, contracts: ['SILVER', 'SILVER100', 'SILVERM', 'SILVERMIC'].map((n) => contract(n, silver)) },
  { id: 'crude', name: 'Crude Oil', image: crudeOil, contracts: ['CRUDEOIL', 'CRUDEOILM'].map((n) => contract(n, crudeOil)) },
  { id: 'gas', name: 'Natural Gas', image: naturalGas, contracts: ['NATURALGAS', 'NATGASMINI'].map((n) => contract(n, naturalGas)) },
  { id: 'copper', name: 'Copper', contracts: [contract('COPPER')] },
  { id: 'aluminium', name: 'Aluminium', contracts: [contract('ALUMINIUM'), contract('ALUMINI')] },
  { id: 'zinc', name: 'Zinc', contracts: [contract('ZINC'), contract('ZINCMINI')] },
]

/** Lot summary (Gold Summary): one tab per gold lot, its futures and its option contracts. */
export const goldLots = [
  { id: 'gold', name: 'Gold', image: goldDefault },
  { id: 'mini', name: 'Gold Mini', image: goldMini },
  { id: 'guinea', name: 'Gold Guinea', image: goldGuinea },
  { id: 'ten', name: 'Gold Ten', image: goldTen },
  { id: 'petal', name: 'Gold Petal', image: goldPetal },
]
export const lotFutures: Contract[] = [
  { id: 'lf-0', name: 'Gold', description: 'Fut | 5 Oct', price: 417, change: 0.1, volume: 0 },
  { id: 'lf-1', name: 'Gold', description: 'Fut | 5 Dec', price: 417, change: 0.1, volume: 0 },
]
export type LotOption = Contract & { marginPerLot: number; /** Too few trades: Buy / Sell are blocked (commodities only). */ illiquid?: boolean }
export const lotOptions: LotOption[] = [
  ...Array.from({ length: 5 }, (_, i): LotOption => ({ id: `lo-${i}`, name: 'GOLD 19400 CE', description: 'Call | 5 Oct 26', price: 417, change: 0.1, volume: 23843233, marginPerLot: 23345, side: 'call' })),
  // A far out-of-the-money strike nobody trades: illiquid.
  { id: 'lo-5', name: 'GOLD 24000 CE', description: 'Call | 5 Oct 26', price: 3, change: -25, volume: 4, marginPerLot: 300, side: 'call', illiquid: true },
]
export const expiryMonths = ['October', 'November', 'December']
export type LotSort = 'price' | 'volume' | 'margin'

/**
 * A commodity contract's asset page (Figma 6754:61613, Gold MINI 5 OCT Fut). Prices in ₹. `illiquid` (commodities
 * only): the page shows the ILLIQUID tag and Buy / Sell are disabled.
 */
export type AssetPage = {
  name: string
  /** Expiry + type, e.g. "5 OCT Fut". */
  contract: string
  image?: string
  price: number
  change: number
  illiquid?: boolean
  daysToExpiry: number
  margin: string
  leverage: string
  priceUnit: string
  notice: string
  futures: { id: string; name: string; date: string; price: number; change: number }[]
  low: number
  high: number
  prevClose: number
  open: number
  upperCircuit: number
  lowerCircuit: number
  tickSize: string
  unit: string
  lotSize: number
  minLot: number
  lastQty: number
  lastTime: string
  expiryDate: string
  lastTradingDate: string
  bids: { price: string; qty: number }[]
  asks: { price: string; qty: number }[]
  bidTotal: number
  askTotal: number
}
export const goldMiniAsset: AssetPage = {
  name: 'Gold MINI', contract: '5 OCT Fut', image: gold, price: 159000, change: -0.22,
  daysToExpiry: 41, margin: '10.84% / 10.84%', leverage: '9.22X / 9.22X', priceUnit: 'Per 10 gram', notice: 'Tender margin period starts 30 Sept',
  futures: [
    { id: 'dec', name: 'Gold 5 DEC Fut', date: '05 Dec 2026', price: 153580, change: 2.16 },
    { id: 'feb', name: 'GOLD 5 FEB FUT', date: '05 Feb 2027', price: 156580, change: -0.12 },
  ],
  low: 157000, high: 160000, prevClose: 158000, open: 157000, upperCircuit: 162000, lowerCircuit: 152000, tickSize: '0.05', unit: '10 grams',
  lotSize: 100, minLot: 1, lastQty: 1, lastTime: '2026-10-29 12:16:42', expiryDate: '2026-10-05', lastTradingDate: '2026-10-05',
  bids: [{ price: '1,58,000', qty: 1 }, { price: '1,57,000', qty: 2 }, { price: '1,56,000', qty: 3 }, { price: '1,55,000', qty: 3 }, { price: '1,54,500', qty: 900 }],
  asks: [{ price: '1,59,000', qty: 1 }, { price: '1,60,000', qty: 2 }, { price: '1,61,000', qty: 3 }, { price: '1,62,000', qty: 4 }, { price: '1,62,500', qty: 15007 }],
  bidTotal: 11003, askTotal: 36367,
}
/** The same page for an illiquid commodity contract (Gold Petal, far month): few trades, wide spread. */
export const illiquidAsset: AssetPage = {
  ...goldMiniAsset, name: 'Gold PETAL', contract: '5 FEB Fut', image: goldPetal, price: 15880, change: 0, illiquid: true,
  low: 15880, high: 15880, prevClose: 15880, open: 15880, lastQty: 1, lastTime: '2026-10-27 15:02:11',
  bids: [{ price: '15,420', qty: 1 }], asks: [{ price: '16,390', qty: 1 }], bidTotal: 1, askTotal: 1,
}

/** Gold MINI intraday 5-minute candles for the asset page chart (illustrative). */
const assetCloses = [159600, 159420, 159510, 159380, 159450, 159300, 159200, 158400, 157900, 157600, 157750, 157500, 157400, 157650, 157900, 157800, 157700, 158000, 157600, 157300, 157900, 158300, 158100, 158200, 157900, 157700, 157600, 157500]
export const assetCandles = assetCloses.map((close, i) => {
  const open = i ? assetCloses[i - 1] : close + 120
  return { open, close, high: Math.max(open, close) + 90 + (i % 3) * 40, low: Math.min(open, close) - 80 - (i % 4) * 30, volume: 20 + ((i * 37) % 60) }
})

/**
 * Expiring This Week (F&O home → Commodities, between the shortcuts and the chart): commodity contracts expiring soon.
 * One card, two variants (`kind`):
 * - `option`: the ATM option (`option`, e.g. "132000 CE ATM") with its premium; the expiry line is "OPT Expiry <day>",
 *   the day from `expiresInDays` (0 = Today, 1 = Tomorrow, then the weekday).
 * - `future`: the future's last traded price (LTP); the expiry line is "FUT Expiry <expiryDate>" ("3 Dec").
 * `price` / `priceChange` are the option's premium or the future's LTP with the day change (%); `margin` is the margin
 * per lot (₹); `trend` / `since` feed the trend read-out.
 * - `event`: a market event on the contract's commodity today (the EIA natural gas storage report): the line under the
 *   symbol is the event and its time ("NG storage · Today 9:00 PM"), the trend read-out is the outlook ("Bullish" over
 *   "Smaller build"), then the ATM option like an
 *   `option` card (the readings are on the calendar's Events tab). Data from the user's reference card (2026-11-17).
 */
type ExpiringBase = {
  id: string; symbol: string; /** The Commodity it belongs to. */ commodity: Commodity['id']; image: string; description: string
  trend: 'up' | 'down'; since: string; price: number; priceChange: number; margin: number
  /** What's behind the trend, in two short lines — the trend info sheet's bullets (Dash's read-out). */
  trendNotes: string[]
}
export type ExpiringContract =
  | (ExpiringBase & { kind: 'option'; option: string; expiresInDays: number })
  | (ExpiringBase & { kind: 'future'; expiryDate: string; /** YYYY-MM-DD, to drop the card once it's past. */ expiresOn: string })
  | (ExpiringBase & {
      kind: 'event'; option: string
      /** The event's short name and when it's out (IST). */
      event: string; eventInDays: number; eventTime: string
      /** The outlook ahead of it ("Bullish") and why, in a few words ("Smaller build"). */
      outlook: string; reason: string
    })
/** Days from today to the next `weekday` (0 = Sunday … 4 = Thursday); 0 when it's today. */
const nextWeekday = (weekday: number) => (weekday - new Date().getDay() + 7) % 7
/**
 * The cards carry the REAL MCX dates of this week (see mcxExpiries below: AlgoTest / MCX, Nov 2026) — gold, Gold Mini
 * and silver options on 27 Nov (their futures 4 Dec), Natural Gas futures today (24 Nov), Silver Mini futures 30 Nov,
 * and the weekly EIA natural gas storage report on Thursday. Prices, margins and trends are samples. Crude oil and
 * natural gas OPTIONS aren't here: theirs expire 16 and 23 Dec, not this week. Cards whose date has passed drop off.
 */
export const expiringThisWeek: ExpiringContract[] = ([
  { kind: 'option', id: 'exp-goldm', symbol: 'GOLDM', commodity: 'gold', image: gold, description: 'Fut | 4 Dec 26', expiresInDays: daysUntil('2026-11-27'), trend: 'up', since: '3:25 PM', option: '132000 CE ATM', price: 118, priceChange: 14.56, margin: 1180, trendNotes: ['EMA(9) on the 15m candles has stayed above EMA(21) since 3:25 PM, and every dip has been bought', 'Momentum is with buyers. Trailing a stop under the last swing low works better than chasing'] },
  // Second for testing the futures variant: Natural Gas futures expire today.
  { kind: 'future', id: 'exp-naturalgas-fut', symbol: 'NATURALGAS', commodity: 'gas', image: naturalGas, description: 'Fut | 24 Nov 26', expiryDate: '24 Nov', expiresOn: '2026-11-24', trend: 'down', since: '10:05 AM', price: 318.6, priceChange: -1.82, margin: 119480, trendNotes: ['Price slipped under EMA(9) on the 15m candles at 10:05 AM and has not reclaimed it', 'Each rally is fading below the average. Selective entries beat chasing the move lower'] },
  // Third: the events card — the EIA natural gas storage report, out every Thursday at 9:00 PM IST.
  { kind: 'event', id: 'exp-natgasmini-event', symbol: 'NATGASMINI', commodity: 'gas', image: naturalGas, description: 'Fut | 28 Dec 26', event: 'NG storage', eventInDays: nextWeekday(4), eventTime: '9:00 PM', trend: 'up', since: '', outlook: 'Bullish', reason: 'Smaller build', option: '305 CE ATM', price: 7.4, priceChange: 4.2, margin: 1850, trendNotes: ['EIA storage is expected at +38 Bcf this week against +56 Bcf last week, a smaller build than usual', 'A smaller build means tighter supply. Prices can move sharply in the minutes after the 9:00 PM release'] },
  { kind: 'option', id: 'exp-silver', symbol: 'SILVER', commodity: 'silver', image: silver, description: 'Fut | 4 Dec 26', expiresInDays: daysUntil('2026-11-27'), trend: 'down', since: '1:10 PM', option: '158000 PE ATM', price: 642.5, priceChange: 8.2, margin: 19275, trendNotes: ['EMA(9) on the 15m candles crossed below EMA(21) at 1:10 PM, and lower highs keep forming', 'Sellers are in control. Bounces into the moving averages have been sold so far'] },
  { kind: 'future', id: 'exp-silverm-fut', symbol: 'SILVERM', commodity: 'silver', image: silver, description: 'Fut | 30 Nov 26', expiryDate: '30 Nov', expiresOn: '2026-11-30', trend: 'up', since: '11:40 AM', price: 157820, priceChange: 0.86, margin: 78910, trendNotes: ['EMA(9) on the 15m candles turned up at 11:40 AM and price has stayed above it since', 'Buyers are stepping in on every dip. A close back under the average would weaken the trend'] },
] satisfies (ExpiringContract & { expiresOn?: string })[]).filter((c) =>
  c.kind === 'option' ? c.expiresInDays >= 0 : c.kind === 'future' ? daysUntil(c.expiresOn) >= 0 : true)

/**
 * Expiry calendar (fno-38, View all on Expiring This Week): the days commodity contracts expire, plus the market events
 * that move them. Each day holds everything on it (one day can have several). Just the name — no prices. Options rows
 * have ScalpPro and option-chain buttons, futures rows only ScalpPro, events none. Real MCX dates (mcxExpiries); `inDays` = days from today
 * (0 = today), so the dates always lead from today. The All tab merges the three by day.
 */
export type ExpiryKind = 'option' | 'future' | 'event'
export type ExpiryEntry = {
  id: string
  kind: ExpiryKind
  name: string
  /** Events: everything shows on the card (there's no event page). */
  event?: ExpiryEvent
  /** The commodity's art, shown as a 24 avatar before the name. Base metals have no art yet: `initials` instead. */
  image?: string
  /** Chemical symbol for metals without art (Zn, Cu, Al, Pb). */
  initials?: string
}
/**
 * A market event that moves commodity prices — the fields every economic calendar shows (Investing.com, Zerodha
 * Markets calendar, broker commodity dailies): when (IST), where, how much it usually moves prices, the last reading,
 * what's expected and, once out, what came in. Plus which MCX commodities it moves and one line on how.
 */
export type ExpiryEvent = {
  /** Release time in IST ("9:00 PM"). */
  time: string
  /** Who releases it: "US", "China", "OPEC+". */
  country: string
  impact: 'high' | 'medium' | 'low'
  /** The last reading, the consensus forecast and (once released) the actual, with units. None for meetings with no number (OPEC+). */
  previous?: string
  forecast?: string
  actual?: string
  /** The MCX commodities it moves and which way it's expected to push each (up = bullish, down = bearish). One entry per
   *  commodity, never its contract sizes: Gold and Gold Mini move together, so it's just "Gold" (likewise Crude Oil,
   *  Natural Gas, Silver). */
  moves: { name: string; trend: 'up' | 'down' }[]
  /** How it usually moves them, in one line. */
  why: string
}
export type ExpiryDay = { inDays: number; entries: ExpiryEntry[] }
const expiryArt: Record<string, Pick<ExpiryEntry, 'image' | 'initials'>> = {
  'Gold': { image: gold }, 'Gold Mini': { image: goldMini }, 'Gold Guinea': { image: goldGuinea }, 'Gold Petal': { image: goldPetal },
  'Silver': { image: silver }, 'Silver Mini': { image: silver }, 'Silver Micro': { image: silver },
  'Crude Oil': { image: crudeOil }, 'Crude Oil Mini': { image: crudeOil },
  'Natural Gas': { image: naturalGas }, 'Natural Gas Mini': { image: naturalGas },
  'Zinc': { initials: 'Zn' }, 'Copper': { initials: 'Cu' }, 'Aluminium': { initials: 'Al' }, 'Lead': { initials: 'Pb' },
}
/** Contracts by name (exported for the archived sample weeks, commodities/archive). */
export const contracts = (kind: 'option' | 'future', names: string[]): ExpiryEntry[] =>
  names.map((name) => ({ id: `${kind}-${name}`, kind, name, ...expiryArt[name] }))
const event = (name: string, details: ExpiryEvent): ExpiryEntry => ({ id: `event-${name}`, kind: 'event', name, event: details })
/**
 * Real MCX dates (Nov 2026 – Mar 2027), from AlgoTest's "MCX Expiry Dates for November and December 2026" (published
 * 2026-11-09, itself from MCX's contract launch calendar), cross-checked with Zerodha's bulletins and Dhan's 2026
 * schedules. Rules: crude oil and natural gas options expire 2 business days before their futures; gold, Gold Mini and
 * silver options in the last week of the month before the futures; Gold Petal and Gold Ten have no options; copper
 * futures expire on the last calendar day of the month. December option dates for gold, Gold Mini, silver, Silver Mini
 * and copper weren't published yet, so they aren't here. Several contracts DO share a day (e.g. 27 Nov: gold, Gold
 * Mini and silver options) — that's how MCX schedules them. MCX can move a date by circular; refresh before a release.
 */
const mcxExpiries: { date: string; kind: 'option' | 'future'; names: string[] }[] = [
  { date: '2026-11-24', kind: 'future', names: ['Natural Gas', 'Natural Gas Mini'] },
  { date: '2026-11-27', kind: 'option', names: ['Gold', 'Gold Mini', 'Silver'] },
  { date: '2026-11-30', kind: 'future', names: ['Silver Mini', 'Copper', 'Gold Petal'] },
  { date: '2026-12-04', kind: 'future', names: ['Gold', 'Gold Mini', 'Silver'] },
  { date: '2026-12-16', kind: 'option', names: ['Crude Oil', 'Crude Oil Mini'] },
  { date: '2026-12-18', kind: 'future', names: ['Crude Oil', 'Crude Oil Mini'] },
  { date: '2026-12-23', kind: 'option', names: ['Natural Gas', 'Natural Gas Mini'] },
  { date: '2026-12-28', kind: 'future', names: ['Natural Gas', 'Natural Gas Mini'] },
  { date: '2026-12-31', kind: 'future', names: ['Copper', 'Gold Petal'] },
  { date: '2027-01-05', kind: 'future', names: ['Gold Mini'] },
  { date: '2027-02-05', kind: 'future', names: ['Gold'] },
  { date: '2027-02-26', kind: 'future', names: ['Silver Mini'] },
  { date: '2027-03-05', kind: 'future', names: ['Silver'] },
]
/** Days from today (0 = today) to a YYYY-MM-DD date, in local time. */
function daysUntil(iso: string) {
  const [y, m, d] = iso.split('-').map(Number)
  const today = new Date(); today.setHours(0, 0, 0, 0)
  return Math.round((new Date(y, m - 1, d).getTime() - today.getTime()) / 86400000)
}
/** Group dated entries into calendar days from today on (past dates dropped). */
function byDate(items: { inDays: number; entries: ExpiryEntry[] }[]): ExpiryDay[] {
  const days = new Map<number, ExpiryEntry[]>()
  for (const item of items) if (item.inDays >= 0) days.set(item.inDays, [...(days.get(item.inDays) ?? []), ...item.entries])
  return [...days].sort((a, b) => a[0] - b[0]).map(([inDays, entries]) => ({ inDays, entries }))
}
/** The EIA weekly reports (US, 10:30 AM ET = 9:00 PM IST in winter): crude oil inventories on Wednesdays, natural gas
 *  storage on Thursdays, for the next 5 weeks. Readings are samples, not live. US holiday shifts (e.g. Thanksgiving)
 *  aren't modelled. */
function weekly(weekday: number, entry: ExpiryEntry): { inDays: number; entries: ExpiryEntry[] }[] {
  const first = (weekday - new Date().getDay() + 7) % 7
  return Array.from({ length: 5 }, (_, week) => ({ inDays: first + week * 7, entries: [entry] }))
}
export const expiryCalendar: Record<ExpiryKind, ExpiryDay[]> = {
  option: byDate(mcxExpiries.filter((e) => e.kind === 'option').map((e) => ({ inDays: daysUntil(e.date), entries: contracts('option', e.names) }))),
  future: byDate(mcxExpiries.filter((e) => e.kind === 'future').map((e) => ({ inDays: daysUntil(e.date), entries: contracts('future', e.names) }))),
  event: byDate([
    ...weekly(3, event('EIA crude oil inventories', { time: '9:00 PM', country: 'US', impact: 'high', previous: '−3.4M bbl', forecast: '−1.8M bbl', moves: [{ name: 'Crude Oil', trend: 'down' }, { name: 'Natural Gas', trend: 'down' }, { name: 'Gold', trend: 'up' }], why: 'Falling stocks usually lift crude; a surprise build pulls it down.' })),
    ...weekly(4, event('EIA natural gas storage', { time: '9:00 PM', country: 'US', impact: 'high', previous: '+56 Bcf', forecast: '+38 Bcf', moves: [{ name: 'Natural Gas', trend: 'up' }, { name: 'Crude Oil', trend: 'up' }], why: 'A smaller injection than expected usually lifts natural gas.' })),
  ]),
}
/** All tab: every kind on each day — options, then futures, then events. */
export const expiryCalendarAll: ExpiryDay[] = (() => {
  const byDay = new Map<number, ExpiryEntry[]>()
  for (const kind of ['option', 'future', 'event'] as const)
    for (const day of expiryCalendar[kind]) byDay.set(day.inDays, [...(byDay.get(day.inDays) ?? []), ...day.entries])
  return [...byDay].sort((a, b) => a[0] - b[0]).map(([inDays, entries]) => ({ inDays, entries }))
})()

/**
 * Expiring This Week, version 2 (home): the calendar's first `count` entries (3), keeping them on their days — three on
 * one day, or spread over two or three days. Events come first within a day: they're timed, so they matter most today.
 * Everything else is on the calendar page (View all).
 */
export function expiryPreview(count = 3, source: ExpiryDay[] = expiryCalendarAll): ExpiryDay[] {
  const days: ExpiryDay[] = []
  let left = count
  for (const day of source) {
    if (left === 0) break
    const ordered = [...day.entries].sort((a, b) => Number(b.kind === 'event') - Number(a.kind === 'event'))
    const entries = ordered.slice(0, left)
    days.push({ inDays: day.inDays, entries })
    left -= entries.length
  }
  return days
}
```

### `src/flows/fno/commodities/screens/AssetPage.module.css`

```css
/* No line under the Actionbar until the page scrolls (then L3's elevated state brings line + shadow). */
.bar:not([data-elevated]) { box-shadow: none; }

/* Commodity asset page (Figma 6754:61613) — flow-only layout on L3 tokens. Panels are the design's grey info boxes. */
.page { padding-block: var(--l3-spacing-08) var(--l3-spacing-32); }
.inset { padding-inline: var(--l3-spacing-16); }
.grow { flex: 1; min-width: 0; }
.head { display: flex; align-items: center; gap: var(--l3-spacing-12); padding-inline: var(--l3-spacing-16); }
.name { margin: 0; font: var(--l3-text-heading-16); }
.contract { font: var(--l3-text-label-14); color: var(--l3-content-tertiary); white-space: nowrap; }
.price { font: var(--l3-text-heading-24); white-space: nowrap; }
.art { flex: none; width: var(--l3-size-48); height: var(--l3-size-48); object-fit: contain; }
.chart { display: flex; flex-direction: column; height: var(--app-size-asset-chart); }
.chart > * { flex: 1; min-height: 0; }

/* Chart tools: icon over label, five across. */
.tools { display: grid; grid-template-columns: repeat(5, 1fr); padding-inline: var(--l3-spacing-08); }
.tool { display: flex; flex-direction: column; align-items: center; gap: var(--l3-spacing-04); min-height: var(--l3-size-48); padding: var(--l3-spacing-04) 0; border: 0; background: none; color: var(--l3-content-primary); font: var(--l3-text-label-10); cursor: pointer; }
.tool span:last-child { color: var(--l3-content-secondary); }
.interval { font: var(--l3-text-heading-14); line-height: var(--l3-size-20); }

/* Option chain · ScalpPro (Figma 6754:62688): two equal Secondary buttons, 40 tall, light outline. ScalpPro is disabled for an illiquid contract. */
.chartActions { display: grid; grid-template-columns: 1fr 1fr; gap: var(--l3-spacing-12); padding-inline: var(--l3-spacing-16); }
.chartAction.chartAction:not(:disabled) { --btn-border: var(--l3-border-light); }
/* Disabled ScalpPro (illiquid): an invisible tap layer over it opens the illiquid tooltip (same as the option chain's). */
.scalpWrap { position: relative; display: grid; }
.scalpTip.scalpTip { position: absolute; inset: 0; display: block; }
.scalpTap { display: block; width: 100%; height: 100%; padding: 0; border: 0; background: none; cursor: pointer; }
.tip { display: inline-flex; align-items: center; gap: var(--l3-spacing-12); white-space: nowrap; }
.tipText { display: flex; flex-direction: column; gap: var(--l3-spacing-02); text-align: left; }
.tipTitle { font: var(--l3-text-label-12); color: var(--l3-content-inverted); }
.tipSub { font: var(--l3-text-description-12); color: var(--l3-content-inverted-secondary); }
.tipInfo { position: relative; margin-right: calc(-1 * var(--l3-spacing-04)); display: inline-grid; place-items: center; width: var(--l3-size-16); height: var(--l3-size-16); padding: 0; border: 0; background: none; color: inherit; cursor: pointer; }
.tipInfo::before { content: ''; position: absolute; inset: calc(-1 * var(--l3-spacing-08)); }
.scalpTip [role='tooltip'][data-ready] { animation: asset-tip-in var(--l3-motion-duration-medium) var(--l3-motion-easing-decelerate) both; transform-origin: var(--tt-arrow) 100%; }
@keyframes asset-tip-in { from { opacity: 0; scale: 0.9; translate: 0 var(--l3-spacing-04); } }
@media (prefers-reduced-motion: reduce) { .scalpTip [role='tooltip'][data-ready] { animation: none; } }
.scalpIcon { display: inline-flex; width: var(--l3-size-20); height: var(--l3-size-20); }

.section { display: flex; flex-direction: column; gap: var(--l3-spacing-16); padding-inline: var(--l3-spacing-16); }
.sectionRail { display: flex; flex-direction: column; gap: var(--l3-spacing-16); }
.panel { display: flex; flex-direction: column; gap: var(--l3-spacing-12); padding: var(--l3-spacing-16) var(--l3-spacing-12); border-radius: var(--l3-radius-16); background: var(--l3-surface-secondary); }
/* Contract Info rows: dashed separators, as in Figma. */
.dashed > * + * { border-top: 1px dashed var(--l3-border-light); padding-top: var(--l3-spacing-12); }
.notice { display: flex; align-items: center; justify-content: space-between; gap: var(--l3-spacing-08); padding: var(--l3-spacing-10) var(--l3-spacing-12); border: 0; border-radius: var(--l3-radius-08); background: var(--l3-surface-primary); color: var(--l3-content-primary); font: var(--l3-text-label-12); text-align: left; cursor: pointer; }
.notice svg, .notice :last-child { color: var(--l3-content-secondary); }

.futureTop { display: flex; flex-direction: column; gap: var(--l3-spacing-04); padding: var(--l3-spacing-12); border-bottom: 1px solid var(--l3-border-light); }
.futureBottom { display: flex; justify-content: space-between; align-items: center; gap: var(--l3-spacing-08); padding: var(--l3-spacing-12); }
.futureName { font: var(--l3-text-label-12); white-space: nowrap; }

.statValue { font: var(--l3-text-heading-12); white-space: nowrap; }
.statLabel { font: var(--l3-text-label-12); color: var(--l3-content-tertiary); white-space: nowrap; }
.grid { display: grid; grid-template-columns: 1fr 1fr; gap: var(--l3-spacing-16) var(--l3-spacing-12); }

/* 24H range: purple → blue bar with a bolt at the last traded price. */
.range { position: relative; height: var(--l3-size-08); margin-block: var(--l3-spacing-06); border-radius: var(--l3-radius-full); background: linear-gradient(90deg, var(--l3-surface-accent-purple-default), var(--l3-surface-accent-discover-default)); }
.marker { position: absolute; top: 50%; translate: -50% -50%; display: inline-flex; color: var(--l3-content-accent-discover-default); }
.ltp { display: flex; align-items: center; gap: var(--l3-spacing-04); font: var(--l3-text-label-12); color: var(--l3-content-tertiary); }
.ltp strong { font: var(--l3-text-heading-12); color: var(--l3-content-primary); }

/* Market depth: bids | asks, a divider between, totals under a rule. */
.depth { display: grid; grid-template-columns: 1fr 1fr; gap: 0; padding: var(--l3-spacing-12) 0; }
.depthSide { width: 100%; border-collapse: collapse; font: var(--l3-text-heading-12); }
.depthSide + .depthSide { border-left: 1px solid var(--l3-border-light); }
.depthSide th { font: var(--l3-text-label-12); color: var(--l3-content-secondary); text-align: left; padding: 0 var(--l3-spacing-12) var(--l3-spacing-08); }
.depthSide td { padding: var(--l3-spacing-08) var(--l3-spacing-12); }
.depthSide th:last-child, .depthSide td:last-child { text-align: right; }
.depthSide tfoot td { border-top: 1px solid var(--l3-border-light); padding-top: var(--l3-spacing-16); font: var(--l3-text-label-12); }
.up { color: var(--l3-content-accent-indicator-up-default); }
.down { color: var(--l3-content-accent-indicator-down-default); }

/* The note + ⓘ: a light-error toast strip, one tap target (opens “What does illiquidity mean?”). */
.illiquidNote { display: flex; align-items: center; justify-content: center; gap: var(--l3-spacing-04); width: 100%; min-height: var(--l3-size-40); padding: var(--l3-spacing-08) var(--l3-spacing-12); border: 0; border-radius: var(--l3-radius-08); background: var(--l3-surface-accent-error-light); font: var(--l3-text-label-12); color: var(--l3-content-accent-error-default); cursor: pointer; }
.pair { display: grid; grid-template-columns: 1fr 1fr; gap: var(--l3-spacing-12); }

/* ILLIQUID tag: tapping it explains illiquid (48 touch area around the small tag). */
.tagButton { position: relative; display: inline-flex; padding: 0; border: 0; background: none; cursor: pointer; }
.tagButton::before { content: ''; position: absolute; inset: calc(-1 * var(--l3-spacing-16)) calc(-1 * var(--l3-spacing-04)); }
```

### `src/flows/fno/commodities/screens/AssetPage.tsx`

```tsx
import { useEffect, useRef, useState } from 'react'
import { Tooltip } from '@l3/components/Tooltip'
import { Actionbar } from '@l3/components/Actionbar'
import { Button } from '@l3/components/Button'
import { ButtonGroup } from '@l3/components/ButtonGroup'
import { Card } from '@l3/components/Card'
import { Icon } from '@l3/components/Icon'
import { MaskIcon } from '@l3/components/MaskIcon'
import { KeyValueList, KeyValueRow } from '@l3/components/KeyValueList'
import { PriceChange } from '@l3/components/PriceChange'
import { SectionHeader } from '@l3/components/SectionHeader'
import { Stack } from '@l3/components/Stack'
import { Tag } from '@l3/components/Tag'
import { msArrowRange, msBoltFill, msDraw, msFunction, msInfo, msLink, msSettings, msStar, msStarFill, msBlock } from '@l3/icons/material'
import { inr } from '../../../../shared/data/format'
import { Rail } from '../../../../shared/ui/Rail'
import { Screen } from '../../../../shared/ui/Screen'
import { TradingPane } from '../../components/TradingPane'
import { DetailSheet } from '../../sheets/HomeSheets'
import { IlliquidSheet } from '../../sheets/IlliquidSheet'
import { t } from '../../copy'
import { assetCandles, type AssetPage as Asset } from '../data'
import scalppro from '../../assets/scalppro.svg'
import styles from './AssetPage.module.css'
import { TopBarAction } from '../../../../shared/ui/TopBarAction'
import flat from '../../flatCards.module.css'

type Props = { asset: Asset; onBack: () => void; onChain: () => void; /** ScalpPro (Scalper) — disabled for an illiquid contract. */ onScalper: () => void; /** Buy / Sell open the commodity order pad. */ onOrder: (side: 'buy' | 'sell') => void }

/**
 * A commodity contract's asset page (Figma 6754:61613): name + contract and price with the commodity art; the chart and
 * its tools; Option chain; Contract Info; the other futures; Performance (24H range + key prices); Trading details;
 * Market Depth; Buy / Sell docked. An illiquid contract (commodities only) shows the ILLIQUID tag and greyed-out Buy /
 * Sell, whatever screen it was opened from.
 */
export function AssetPage({ asset, onBack, onChain, onScalper, onOrder }: Props) {
  const [saved, setSaved] = useState(false)
  const [detail, setDetail] = useState<string | null>(null)
  const [explain, setExplain] = useState(false)
  // Illiquid: ScalpPro is disabled; a tap on it shows the illiquid tooltip (tap only — no hover / focus), gone after 5 s.
  const [scalpTip, setScalpTip] = useState(false)
  const scalpWasOpen = useRef(false)
  useEffect(() => {
    if (!scalpTip) return
    const timer = window.setTimeout(() => setScalpTip(false), 5000)
    return () => window.clearTimeout(timer)
  }, [scalpTip])
  // The Actionbar's bottom line shows only once the page has scrolled under it.
  const pageRef = useRef<HTMLDivElement>(null)
  const [scrolled, setScrolled] = useState(false)
  useEffect(() => {
    const body = pageRef.current?.parentElement
    if (!body) return
    const onScroll = () => setScrolled(body.scrollTop > 0)
    onScroll()
    body.addEventListener('scroll', onScroll, { passive: true })
    return () => body.removeEventListener('scroll', onScroll)
  }, [])
  // The sample candles are Gold MINI's; scale them to this contract's price.
  const scale = asset.price / assetCandles[assetCandles.length - 1].close
  const candles = assetCandles.map((c) => ({ ...c, open: c.open * scale, close: c.close * scale, high: c.high * scale, low: c.low * scale }))
  const position = ((asset.price - asset.low) / Math.max(1, asset.high - asset.low)) * 100
  const tools = [
    { key: 'range', icon: msArrowRange, value: t('asset.range') },
    { key: 'interval', icon: null, value: t('asset.interval') },
    { key: 'indicators', icon: msFunction, value: t('asset.indicators') },
    { key: 'drawings', icon: msDraw, value: t('asset.drawings') },
    { key: 'settings', icon: msSettings, value: t('asset.settings') },
  ]
  const stat = (value: string, label: string) => <Stack gap="04"><p className={styles.statValue}>{value}</p><p className={styles.statLabel}>{label}</p></Stack>
  // The illiquid note sits inside the button dock, right above Buy / Sell.
  const dock = <ButtonGroup aria-label={`${asset.name} ${asset.contract}`} direction={asset.illiquid ? 'vertical' : 'horizontal'}>
    {asset.illiquid && <button type="button" className={styles.illiquidNote} onClick={() => setExplain(true)}>{t('asset.illiquidNote')}<Icon icon={msInfo} size={16} /></button>}
    {asset.illiquid
      ? <div className={styles.pair}><Button variant="buy" disabled>{t('asset.buy')}</Button><Button variant="sell" disabled>{t('asset.sell')}</Button></div>
      : <><Button variant="buy" onClick={() => onOrder('buy')}>{t('asset.buy')}</Button><Button variant="sell" onClick={() => onOrder('sell')}>{t('asset.sell')}</Button></>}
  </ButtonGroup>

  return <Screen className={flat.flatCards}
    top={<Actionbar className={styles.bar} elevated={scrolled} onBack={onBack} backLabel={t('asset.back')} actions={<TopBarAction icon={saved ? msStarFill : msStar} label={t('asset.watchlist')} pressed={saved} onClick={() => setSaved(!saved)} />} />}
    bottom={dock}
    sheet={explain ? <IlliquidSheet contract={`${asset.name} ${asset.contract}`} onClose={() => setExplain(false)} /> : detail ? <DetailSheet title={detail} onClose={() => setDetail(null)} /> : undefined}>
    <Stack ref={pageRef} gap="32" className={styles.page}>
      <Stack gap="16">
        <div className={styles.head}>
          <Stack gap="04" className={styles.grow}>
            <Stack direction="horizontal" gap="08" align="center"><h1 className={styles.name}>{asset.name}</h1><span className={styles.contract}>{asset.contract}</span>{asset.illiquid && <button type="button" className={styles.tagButton} aria-label={t('illiquid.open')} onClick={() => setExplain(true)}><Tag color="error" variant="secondary" size="sm" iconLeft={<Icon icon={msBlock} size={12} />}>{t('asset.illiquid')}</Tag></button>}</Stack>
            <Stack direction="horizontal" gap="04" align="center"><p className={styles.price}>{inr(asset.price, 2)}</p><PriceChange value={asset.change} unit="percent" size="sm" /></Stack>
          </Stack>
          {asset.image && <img className={styles.art} src={asset.image} alt="" />}
        </div>
        <div className={styles.chart}><TradingPane candles={candles} start="09:15" minutes={15} label={t('asset.chart', { name: asset.name, contract: asset.contract })} /></div>
        <div className={styles.tools} role="toolbar" aria-label={t('asset.tools')}>{tools.map((tool) => <button key={tool.key} type="button" className={styles.tool} onClick={() => setDetail(tool.value)}>
          {tool.icon ? <Icon icon={tool.icon} size={20} /> : <span className={styles.interval}>{t('asset.intervalValue')}</span>}<span>{tool.value}</span>
        </button>)}</div>
        <div className={styles.chartActions}>
          <Button variant="secondary" size="md" fullWidth className={styles.chartAction} iconLeft={<Icon icon={msLink} size={20} />} onClick={onChain}>{t('asset.chain')}</Button>
          <div className={styles.scalpWrap}>
            <Button variant="secondary" size="md" fullWidth className={styles.chartAction} disabled={asset.illiquid} iconLeft={<span className={styles.scalpIcon}><MaskIcon src={scalppro} /></span>} onClick={onScalper}>{t('chart.scalper')}</Button>
            {asset.illiquid && <Tooltip className={styles.scalpTip} placement="top" open={scalpTip} onOpenChange={(open) => { if (!open) setScalpTip(false) }}
              content={<span className={styles.tip}><span className={styles.tipText}><span className={styles.tipTitle}>{t('chain.illiquid')}</span><span className={styles.tipSub}>{t('chain.illiquidSub')}</span></span><button type="button" className={styles.tipInfo} aria-label={t('chain.illiquidMore')} onClick={() => { setScalpTip(false); setExplain(true) }}><Icon icon={msInfo} size={16} /></button></span>}>
              <button type="button" className={styles.scalpTap} aria-label={`${t('chart.scalper')}: ${t('chain.illiquid')}, ${t('chain.illiquidSub')}`} aria-expanded={scalpTip}
                onPointerDown={() => { scalpWasOpen.current = scalpTip }} onClick={() => setScalpTip(!scalpWasOpen.current)} />
            </Tooltip>}
          </div>
        </div>
      </Stack>

      <section className={styles.section} aria-label={t('asset.info')}>
        <SectionHeader title={t('asset.info')} />
        <div className={styles.panel}>
          <KeyValueList aria-label={t('asset.info')} className={styles.dashed}>
            <KeyValueRow label={t('asset.daysToExpiry')} value={t('asset.days', { count: asset.daysToExpiry })} />
            <KeyValueRow label={t('asset.margin')} value={asset.margin} />
            <KeyValueRow label={t('asset.leverage')} value={asset.leverage} />
            <KeyValueRow label={t('asset.priceUnit')} value={asset.priceUnit} />
          </KeyValueList>
          <button type="button" className={styles.notice} onClick={() => setDetail(asset.notice)}><span>{asset.notice}</span><Icon icon={msInfo} size={16} /></button>
        </div>
      </section>

      <section className={styles.sectionRail} aria-label={t('asset.futures', { name: asset.name.toUpperCase() })}>
        <div className={styles.inset}><SectionHeader title={t('asset.futures', { name: asset.name.toUpperCase() })} /></div>
        <Rail label={t('asset.futures', { name: asset.name.toUpperCase() })} visible={1.9}>{asset.futures.map((f) => <Card key={f.id} surface="secondary" padding="none" onClick={() => setDetail(f.name)}>
          <div className={styles.futureTop}><p className={styles.futureName}>{f.name}</p><p className={styles.statLabel}>{f.date}</p></div>
          <div className={styles.futureBottom}><p className={styles.statValue}>{inr(f.price, 2)}</p><PriceChange value={f.change} unit="percent" size="sm" /></div>
        </Card>)}</Rail>
      </section>

      <section className={styles.section} aria-label={t('asset.performance')}>
        <SectionHeader title={t('asset.performance')} />
        <div className={styles.panel}>
          <Stack direction="horizontal" justify="between"><Stack gap="04"><p className={styles.statLabel}>{t('asset.low')}</p><p className={styles.statValue}>{inr(asset.low, 2)}</p></Stack><Stack gap="04" align="end"><p className={styles.statLabel}>{t('asset.high')}</p><p className={styles.statValue}>{inr(asset.high, 2)}</p></Stack></Stack>
          <div className={styles.range}><span className={styles.marker} style={{ left: `${position}%` }}><Icon icon={msBoltFill} size={20} /></span></div>
          <p className={styles.ltp}><Icon icon={msBoltFill} size={12} /> {t('asset.ltp')} <strong>{inr(asset.price, 2)}</strong></p>
        </div>
        <div className={[styles.panel, styles.grid].join(' ')}>
          {stat(inr(asset.prevClose, 2), t('asset.prevClose'))}{stat(inr(asset.open, 2), t('asset.open'))}
          {stat(inr(asset.upperCircuit, 2), t('asset.upperCircuit'))}{stat(inr(asset.lowerCircuit, 2), t('asset.lowerCircuit'))}
          {stat(asset.tickSize, t('asset.tickSize'))}{stat(asset.unit, t('asset.unit'))}
        </div>
      </section>

      <section className={styles.section} aria-label={t('asset.trading')}>
        <SectionHeader title={t('asset.trading')} />
        <div className={[styles.panel, styles.grid].join(' ')}>
          {stat(String(asset.lotSize), t('asset.lotSize'))}{stat(String(asset.minLot), t('asset.minLot'))}
          {stat(String(asset.lastQty), t('asset.lastQty'))}{stat(asset.lastTime, t('asset.lastTime'))}
          {stat(asset.expiryDate, t('asset.expiry'))}{stat(asset.lastTradingDate, t('asset.lastTradingDate'))}
        </div>
      </section>

      <section className={styles.section} aria-label={t('asset.depth')}>
        <SectionHeader title={t('asset.depth')} />
        <div className={[styles.panel, styles.depth].join(' ')}>
          {([['bid', asset.bids, asset.bidTotal, styles.up], ['ask', asset.asks, asset.askTotal, styles.down]] as const).map(([side, rows, total, tone]) => <table key={side} className={styles.depthSide}>
            <thead><tr><th>{t(side === 'bid' ? 'asset.bid' : 'asset.ask')}</th><th>{t('asset.qty')}</th></tr></thead>
            <tbody>{rows.map((r, i) => <tr key={i}><td>{r.price}</td><td className={tone}>{r.qty.toLocaleString('en-IN')}</td></tr>)}</tbody>
            <tfoot><tr><td>{t('asset.total')}</td><td>{total.toLocaleString('en-IN')}</td></tr></tfoot>
          </table>)}
        </div>
      </section>
    </Stack>
  </Screen>
}
```

### `src/flows/fno/commodities/screens/ExpiryTimeline.tsx`

```tsx
import { useLayoutEffect, useRef, useState, type CSSProperties } from 'react'
import { Actionbar } from '@l3/components/Actionbar'
import { Icon } from '@l3/components/Icon'
import { SectionHeader } from '@l3/components/SectionHeader'
import { Stack } from '@l3/components/Stack'
import { Tabs } from '@l3/components/Tabs'
import { msApps, msCandlestickChart, msEvent, msTrendingUp } from '@l3/icons/material'
import { Screen } from '../../../../shared/ui/Screen'
import { neighbour, useSwipeBetween } from '../../../../shared/ui/useSwipeBetween'
import { t } from '../../copy'
import { expiryCalendar, expiryCalendarAll, type ExpiryKind } from '../data'
import { CalendarDay, dayFrom } from '../components/CalendarDay'
import styles from '../components/Commodities.module.css'
import flat from '../../flatCards.module.css'

type Tab = 'all' | ExpiryKind
const TABS: Tab[] = ['all', 'option', 'future', 'event']
const TAB_ICONS: Record<Tab, string> = { all: msApps, option: msCandlestickChart, future: msTrendingUp, event: msEvent }

const monthOf = (date: Date) => date.toLocaleDateString('en-IN', { month: 'short', year: 'numeric' })

/**
 * fno-38 · Expiry calendar — View all on Expiring This Week (Commodities). All / Options / Futures / Events (flat tabs with icons, sticky, in the
 * Actionbar's bottom slot). The days run from today under a month section header (L3 SectionHeader, content-primary: "Nov 2026", repeated when the month turns):
 * on the left one grey block (surface-secondary) holding the weekday over the date (today inverted on the calendar page — dark fill, light text — not marked on the home), on the right one card with that day's contracts — one day can hold
 * several, split by hairlines. Scrolling, the month header sticks at the top until the next month's pushes it out, and
 * each day's date block sticks under it for as long as that day's card is in view. A row is only the contract's name with two flat (no shadow) icon
 * buttons, centred vertically, the row 12 in from every side: options get option chain (→ option chain page) then ScalpPro (→ Scalper);
 * Changing tab slides the body with it (tap: the new tab's body slides in from its side; swipe left / right on the body drags it
 * to the next / previous tab, rubber-band at the ends — shared useSwipeBetween).
 * futures ScalpPro only; events show everything upfront (time IST, previous / forecast / actual, one arrow tag per commodity it moves → asset page), no buttons. All tags each row with its kind. Cards are flat (border, no shadow).
 */
export function ExpiryTimeline({ onBack, onAsset, onOptionChain, onScalper }: { onBack: () => void; onAsset: () => void; onOptionChain: () => void; onScalper: () => void }) {
  const [tab, setTab] = useState<Tab>('all')
  // The tab being tapped, so the tabs answer at once while the body is still sliding.
  const [tapped, setTapped] = useState<Tab | null>(null)
  // The body slides with the tabs (the shared useSwipeBetween, like Market's tabs and the stocks theme page): the tab
  // next door's body sits just off-screen on either side, so a swipe drags it into view and a tap slides it across.
  const body = useRef<HTMLDivElement>(null)
  const comingFrom = useRef<1 | -1 | 0>(0)
  const swipe = useSwipeBetween({
    page: tab,
    canGo: (direction) => neighbour(TABS, tab, direction) !== null,
    onSwitch: (direction) => { const next = neighbour(TABS, tab, direction); if (next) { setTab(next); setTapped(null) } },
    slides: () => (body.current ? [body.current] : []),
    fades: () => [],
  })
  // A tap on a tab. Next door: the same slide as a swipe. Further away: it slides straight in from its side.
  const pick = (next: Tab) => {
    const step = TABS.indexOf(next) - TABS.indexOf(tab)
    if (!step || next === tapped) return
    setTapped(next)
    if (Math.abs(step) === 1) return swipe.go(step as 1 | -1, () => { setTab(next); setTapped(null) })
    comingFrom.current = step > 0 ? 1 : -1
    setTab(next)
    setTapped(null)
  }
  useLayoutEffect(() => {
    const from = comingFrom.current
    comingFrom.current = 0
    const el = body.current
    if (!from || !el || matchMedia('(prefers-reduced-motion: reduce)').matches) return
    el.animate([{ translate: `${from * el.offsetWidth}px 0` }, { translate: '0 0' }], { duration: 280, easing: 'cubic-bezier(0.2, 0, 0, 1)' })
  }, [tab])
  const props = { onAsset, onOptionChain, onScalper }
  return <Screen className={flat.flatCards} top={<Actionbar title={t('expiryAll.title')} onBack={onBack} backLabel={t('lot.back')}
    bottom={<Tabs aria-label={t('expiryAll.filter')} value={tapped ?? tab} onChange={(v) => pick(v as Tab)}
      items={TABS.map((value) => ({ value, label: t(`expiryAll.tab.${value}`), iconLeft: <Icon icon={TAB_ICONS[value]} size={16} /> }))} />} />}>
    <div className={styles.calendarViewport}>
      <div ref={(el) => { body.current = el; swipe.bind(el) }} className={styles.calendarTrack}>
        {/* Keyed by tab: the body that slides in stays the same once it becomes the current one. */}
        {[neighbour(TABS, tab, -1), tab, neighbour(TABS, tab, 1)].map((panelTab, at) => panelTab && (
          <div key={panelTab} className={styles.calendarPanel} data-side={['before', 'current', 'after'][at]} inert={at !== 1} aria-hidden={at !== 1 || undefined}>
            <CalendarBody tab={panelTab} {...props} />
          </div>
        ))}
      </div>
    </div>
  </Screen>
}

/** One tab's days, grouped by month. */
function CalendarBody({ tab, onAsset, onOptionChain, onScalper }: { tab: Tab; onAsset: () => void; onOptionChain: () => void; onScalper: () => void }) {
  const days = tab === 'all' ? expiryCalendarAll : expiryCalendar[tab]
  // The days grouped by month ("Nov 2026", "Dec 2026"), in order.
  const months: { month: string; days: typeof days }[] = []
  for (const day of days) {
    const month = monthOf(dayFrom(day.inDays))
    if (months.at(-1)?.month === month) months.at(-1)!.days.push(day)
    else months.push({ month, days: [day] })
  }
  // The sticky date blocks stop just under the sticky month header: measure its height once it's drawn.
  const headRef = useRef<HTMLDivElement>(null)
  const [headHeight, setHeadHeight] = useState(0)
  useLayoutEffect(() => { setHeadHeight(headRef.current?.offsetHeight ?? 0) }, [tab])
  return <div className={styles.calendar} style={{ '--calendar-head': `${headHeight}px` } as CSSProperties}>
    {months.map((m, mi) => <section key={m.month} className={styles.calendarMonth} aria-label={m.month}>
      {/* Sticky: the month stays at the top until the next month's header pushes it out. */}
      <div ref={mi === 0 ? headRef : undefined} className={styles.calendarMonthHead}><SectionHeader title={m.month} /></div>
      {/* 32 between two days (no line). */}
      <Stack gap="32">
        {m.days.map((day) => <CalendarDay key={day.inDays} day={day} showKind={tab === 'all'} separate onAsset={onAsset} onOptionChain={onOptionChain} onScalper={onScalper} />)}
      </Stack>
    </section>)}
  </div>
}
```

### `src/flows/fno/commodities/screens/LotSummary.tsx`

```tsx
import { useState } from 'react'
import { Actionbar } from '@l3/components/Actionbar'
import { Button } from '@l3/components/Button'
import { Card } from '@l3/components/Card'
import { EmptyState } from '@l3/components/EmptyState'
import { Icon } from '@l3/components/Icon'
import { PriceChange } from '@l3/components/PriceChange'
import { SectionHeader } from '@l3/components/SectionHeader'
import { Select } from '@l3/components/Select'
import { Stack } from '@l3/components/Stack'
import { Tab, Tabs } from '@l3/components/Tabs'
import { msFilterList, msKeyboardArrowDown, msBlock } from '@l3/icons/material'
import { inr } from '../../../../shared/data/format'
import { Screen } from '../../../../shared/ui/Screen'
import { ChoiceSheet, DetailSheet } from '../../sheets/HomeSheets'
import { ContractSheet } from '../sheets/ContractSheet'
import { IlliquidSheet } from '../../sheets/IlliquidSheet'
import { Tag } from '@l3/components/Tag'
import type { Contract } from '../../data'
import { t } from '../../copy'
import { expiryMonths, goldLots, lotFutures, lotOptions, type LotOption, type LotSort } from '../data'
import parts from '../../components/HomeParts.module.css'
import styles from '../components/Commodities.module.css'
import flat from '../../flatCards.module.css'

type Modal = { kind: 'detail'; title: string; contract?: Contract } | { kind: 'contract'; contract: Contract & { illiquid?: boolean } } | { kind: 'illiquid'; contract: string } | { kind: 'choice'; title: string; values: string[]; value: string; onPick: (v: string) => void }

/**
 * Gold Summary (Figma 6754:65113 by price, 6754:65288 by volume, 6754:65444 margin per lot): the lot tabs sit in the
 * Actionbar's bottom slot; Futures, then Options with expiry month, category pills, Filter and the sort choice.
 */
type Props = {
  sort?: LotSort
  /** Open with the Buy / Sell sheet up on this option (fno-23 a liquid one, fno-24 the illiquid one). */
  initialSheet?: string
  onBack: () => void
  onChain: () => void
  /** The sheet's contract name › opens the asset page (illiquid = the ILLIQUID page). */
  onAsset: (illiquid: boolean) => void
  /** The Buy / Sell sheet's buttons open the commodity order pad. */
  onOrder: (side: 'buy' | 'sell') => void
}

export function LotSummary({ sort: initialSort = 'price', initialSheet, onBack, onChain, onAsset, onOrder }: Props) {
  const [lot, setLot] = useState(goldLots[0].id)
  const [month, setMonth] = useState(expiryMonths[0])
  const [category, setCategory] = useState('top')
  const [sort, setSort] = useState<LotSort>(initialSort)
  const [filter, setFilter] = useState(t('filter.all'))
  const [modal, setModal] = useState<Modal | null>(() => { const c = lotOptions.find((o) => o.id === initialSheet); return c ? { kind: 'contract', contract: c } : null })
  const close = () => setModal(null)
  const choose = (title: string, values: string[], value: string, onPick: (v: string) => void) => setModal({ kind: 'choice', title, values, value, onPick })
  const sorts: LotSort[] = ['price', 'volume', 'margin']
  const sortLabel = (s: LotSort) => t(`sort.${s}`)
  const value = (option: LotOption) => sort === 'volume' ? option.volume.toLocaleString('en-IN') : sort === 'margin' ? inr(option.marginPerLot, 0) : inr(option.price, 2)
  // A card opens the Buy / Sell sheet (live app); an illiquid contract's sheet has Buy / Sell greyed out.
  const open = (contract: Contract & { illiquid?: boolean }) => setModal({ kind: 'contract', contract })
  const options = lotOptions.filter((o) => filter === t('filter.puts') ? o.side === 'put' : true)
  const lotName = goldLots.find((l) => l.id === lot)!.name
  const sheet = modal?.kind === 'illiquid' ? <IlliquidSheet contract={modal.contract} onClose={close} /> : modal?.kind === 'contract' ? <ContractSheet contract={modal.contract} onClose={close} onIlliquid={() => setModal({ kind: 'illiquid', contract: modal.contract.name })} onAsset={() => { close(); onAsset(!!modal.contract.illiquid) }} onBuy={() => { close(); onOrder('buy') }} onSell={() => { close(); onOrder('sell') }} /> : modal?.kind === 'detail' ? <DetailSheet title={modal.title} contract={modal.contract} onClose={close} /> : modal?.kind === 'choice' ? <ChoiceSheet {...modal} onClose={close} /> : undefined
  return <Screen className={flat.flatCards} sheet={sheet} top={<Actionbar title={t('lot.title', { name: goldLots[0].name })} onBack={onBack} backLabel={t('lot.back')}
    bottom={<Tabs aria-label={t('lot.lots')} value={lot} onChange={setLot} width="hug" items={goldLots.map((l) => ({ value: l.id, label: l.name, iconLeft: <img className={styles.tabArt} src={l.image} alt="" /> }))} />} />}>
    <Stack gap="32" className={styles.lotBody}>
      <section className={parts.contractSection} aria-label={t('lot.futures')}>
        <SectionHeader title={t('lot.futures')} action={{ type: 'view-all', label: t('viewAll'), onClick: () => setModal({ kind: 'detail', title: `${lotName} ${t('lot.futures')}` }) }} />
        <Stack gap="12">{lotFutures.map((future) => <Card key={future.id} onClick={() => open(future)}>
          <Stack direction="horizontal" gap="08" justify="between" align="center"><Stack gap="04" className={parts.grow}><p className={parts.heading}>{future.name}</p><p className={parts.description}>{future.description}</p></Stack><Stack gap="04" align="end"><p className={parts.heading}>{inr(future.price, 2)}</p><PriceChange value={future.change} unit="percent" size="sm" /></Stack></Stack>
        </Card>)}</Stack>
      </section>
      <section className={parts.contractSection} aria-label={t('lot.options')}>
        <SectionHeader title={t('lot.options')} action={{ type: 'view-all', label: t('lot.chain'), onClick: onChain }} />
        <Stack direction="horizontal" gap="08" align="center" className={parts.filterRow}>
          <Tab appearance="pill" size="sm" emphasis="secondary" action iconRight={<Icon icon={msKeyboardArrowDown} size={16} />} aria-label={t('lot.expiry')} onClick={() => choose(t('lot.expiry'), expiryMonths, month, setMonth)}>{month}</Tab>
          <span className={styles.pillDivider} aria-hidden />
          <Tabs aria-label={t('lot.options')} appearance="pill" size="sm" value={category} onChange={setCategory} items={[{ value: 'top', label: t('commodities.top') }, { value: 'active', label: t('lot.active') }, { value: 'oi', label: t('lot.oi') }, { value: 'gainers', label: t('lot.gainers') }]} />
        </Stack>
        <Stack direction="horizontal" align="center" justify="between">
          <Button variant="ghost" size="sm" iconLeft={<Icon icon={msFilterList} size={12} />} onClick={() => choose(t('filter'), [t('filter.all'), t('filter.calls'), t('filter.puts')], filter, setFilter)}>{filter === t('filter.all') ? t('filter') : filter}</Button>
          <Select size="sm" aria-label={t('sort.label')} onClick={() => choose(t('sort.title'), sorts.map(sortLabel), sortLabel(sort), (label) => setSort(sorts.find((s) => sortLabel(s) === label)!))}>{sortLabel(sort)}</Select>
        </Stack>
        <Stack gap="12">{options.length === 0 && <EmptyState title={t('empty')} description={t('empty.description')} />}{options.map((option) => <Card key={option.id} onClick={() => open(option)}>
          <Stack direction="horizontal" gap="08" justify="between" align="center"><Stack gap="04" className={parts.grow}><Stack direction="horizontal" gap="08" align="center"><p className={parts.heading}>{option.name}</p>{/* The card is a button, so the tag is a tappable span inside it (stops the card's own tap). */}{option.illiquid && <span className={styles.tagTap} onClick={(e) => { e.stopPropagation(); setModal({ kind: 'illiquid', contract: option.name }) }}><Tag color="error" variant="secondary" size="sm" iconLeft={<Icon icon={msBlock} size={12} />}>{t('asset.illiquid')}</Tag></span>}</Stack><p className={parts.description}>{option.description}</p></Stack>
            {sort === 'price' ? <Stack gap="04" align="end"><p className={parts.heading}>{value(option)}</p><PriceChange value={option.change} unit="percent" size="sm" /></Stack> : <p className={parts.heading}>{value(option)}</p>}</Stack>
        </Card>)}</Stack>
      </section>
    </Stack>
  </Screen>
}
```

### `src/flows/fno/commodities/sheets/ContractPickerSheet.tsx`

```tsx
import { useId, useState } from 'react'
import { BottomSheetHeader } from '@l3/components/BottomSheet'
import { Radio } from '@l3/components/Checkbox'
import { ListCell } from '@l3/components/ListCell'
import { Stack } from '@l3/components/Stack'
import { Tag } from '@l3/components/Tag'
import { Tabs } from '@l3/components/Tabs'
import { Sheet } from '../../../../shared/ui/Sheet'
import { t } from '../../copy'
import { commodityGroups, equityContracts, type PickerContract } from '../data'
import parts from '../../components/HomeParts.module.css'
import styles from '../components/Commodities.module.css'

type Segment = 'equity' | 'commodities'

/**
 * "Choose options contract" (Figma 6754:65111 Commodities, 6754:65054 Equity): Equity / Commodities tabs in the header's
 * bottom slot (Commodities also gets a row of commodity chips under them), then the contracts as radio rows. Picking
 * one selects it and closes the sheet.
 */
export function ContractPickerSheet({ segment: initialSegment = 'commodities', value, onPick, onClose }: { segment?: Segment; value: string; onPick: (name: string) => void; onClose: () => void }) {
  const id = useId()
  const [segment, setSegment] = useState<Segment>(initialSegment)
  const [commodity, setCommodity] = useState('all')
  const commodityCount = commodityGroups.length
  const tabs = <Tabs aria-label={t('picker.title')} value={segment} onChange={setSegment} items={[{ value: 'equity', label: t('picker.equity', { count: equityContracts.length }) }, { value: 'commodities', label: t('picker.commodities', { count: commodityCount }) }]} />
  const chips = <div className={styles.chips}><Tabs aria-label={t('picker.filter')} appearance="pill" size="sm" value={commodity} onChange={setCommodity} items={[{ value: 'all', label: t('picker.all') }, ...commodityGroups.map((g) => ({ value: g.id, label: g.name, iconLeft: g.image ? <img className={styles.chipArt} src={g.image} alt="" /> : undefined }))]} /></div>
  const row = (c: PickerContract) => <ListCell key={c.id} as="label" size="sm" selected={c.name === value}
    iconLeft={c.image ? <img className={styles.rowArt} src={c.image} alt="" /> : undefined}
    label={c.name}
    description={<span className={parts.label}>{c.price} <span className={c.change < 0 ? parts.down : parts.up}>{c.change > 0 ? '+' : ''}{c.change.toFixed(2)}%</span></span>}
    trailing={<Stack direction="horizontal" gap="08" align="center">{c.tag && <Tag color="discover" variant="secondary" size="sm">{c.tag}</Tag>}<Radio name={id} checked={c.name === value} onChange={() => { onPick(c.name); onClose() }} /></Stack>} />
  const groups = commodityGroups.filter((g) => commodity === 'all' || g.id === commodity)
  return <Sheet labelledBy={id} onClose={onClose} header={<BottomSheetHeader heading={t('picker.title')} headingId={id} bottom={<>{tabs}{segment === 'commodities' && chips}</>} />}>
    <div className={[styles.pickerBody, segment === 'equity' && styles.equity].filter(Boolean).join(' ')}>
      {segment === 'equity'
        ? <div className={styles.group}>{equityContracts.map(row)}</div>
        : <Stack gap="24">{groups.map((g) => <Stack key={g.id} gap="12"><p className={styles.groupLabel}>{g.name}</p><div className={styles.group}>{g.contracts.map(row)}</div></Stack>)}</Stack>}
    </div>
  </Sheet>
}
```

### `src/flows/fno/commodities/sheets/ContractSheet.module.css`

```css
/* Buy / Sell contract sheet (live app reference, 2026-10-29) on L3 tokens. */
.body { display: flex; flex-direction: column; gap: var(--l3-spacing-12); }
.row { display: flex; align-items: center; justify-content: space-between; gap: var(--l3-spacing-12); }
.name { display: inline-flex; align-items: center; gap: var(--l3-spacing-04); min-height: var(--l3-size-48); margin-block: calc(-1 * var(--l3-spacing-12)); padding: 0; border: 0; background: none; color: var(--l3-content-primary); font: var(--l3-text-heading-18); text-align: left; cursor: pointer; }
.price { font: var(--l3-text-heading-18); white-space: nowrap; }
.expiry { display: inline-flex; align-items: center; gap: var(--l3-spacing-08); font: var(--l3-text-heading-16); }
/* The note + ⓘ: a light-error toast strip, one tap target (opens “What does illiquidity mean?”). */
.note { display: flex; align-items: center; justify-content: center; gap: var(--l3-spacing-04); width: 100%; min-height: var(--l3-size-40); padding: var(--l3-spacing-08) var(--l3-spacing-12); border: 0; border-radius: var(--l3-radius-08); background: var(--l3-surface-accent-error-light); font: var(--l3-text-label-12); color: var(--l3-content-accent-error-default); cursor: pointer; }
/* Buy / Sell side by side under the note (the dock is vertical then; same 12 gap as a horizontal dock). */
.pair { display: grid; grid-template-columns: 1fr 1fr; gap: var(--l3-spacing-12); }
.tagButton { position: relative; display: inline-flex; padding: 0; border: 0; background: none; cursor: pointer; }
.tagButton::before { content: ''; position: absolute; inset: calc(-1 * var(--l3-spacing-16)) calc(-1 * var(--l3-spacing-04)); }
```

### `src/flows/fno/commodities/sheets/ContractSheet.tsx`

```tsx
import { useId } from 'react'
import { Button } from '@l3/components/Button'
import { ButtonGroup } from '@l3/components/ButtonGroup'
import { Icon } from '@l3/components/Icon'
import { PriceChange } from '@l3/components/PriceChange'
import { Tag } from '@l3/components/Tag'
import { msChevronRight, msInfo, msBlock } from '@l3/icons/material'
import { inr } from '../../../../shared/data/format'
import { Sheet } from '../../../../shared/ui/Sheet'
import { t } from '../../copy'
import type { Contract } from '../../data'
import styles from './ContractSheet.module.css'

type Props = { contract: Contract & { illiquid?: boolean }; onAsset: () => void; /** The ILLIQUID tag explains illiquid. */ onIlliquid: () => void; onBuy: () => void; onSell: () => void; onClose: () => void }

/**
 * Buy / Sell sheet from a contract card (live app, Gold Summary): name › (asset page) · price, expiry + type · change,
 * Buy (brand) / Sell (secondary). Illiquid (commodities, product rule): ILLIQUID tag and Buy / Sell greyed out — the
 * user can only open the asset page or tap outside to close. Same sheet from any entry point.
 */
export function ContractSheet({ contract, onAsset, onIlliquid, onBuy, onSell, onClose }: Props) {
  const id = useId()
  return <Sheet labelledBy={id} onClose={onClose}
    // The illiquid note sits inside the button dock, right above Buy / Sell.
    footer={<ButtonGroup aria-label={t('contractSheet.label', { name: contract.name })} direction={contract.illiquid ? 'vertical' : 'horizontal'}>
      {contract.illiquid && <button type="button" className={styles.note} onClick={onIlliquid}>{t('asset.illiquidNote')}<Icon icon={msInfo} size={16} /></button>}
      {contract.illiquid
        ? <div className={styles.pair}><Button variant="buy" disabled onClick={onBuy}>{t('asset.buy')}</Button><Button variant="sell" disabled onClick={onSell}>{t('asset.sell')}</Button></div>
        : <><Button variant="buy" onClick={onBuy}>{t('asset.buy')}</Button><Button variant="sell" onClick={onSell}>{t('asset.sell')}</Button></>}
    </ButtonGroup>}>
    <div className={styles.body}>
      <div className={styles.row}>
        <button type="button" className={styles.name} id={id} onClick={onAsset} aria-label={t('contractSheet.open', { name: contract.name })}>
          {contract.name}<Icon icon={msChevronRight} size={20} />
        </button>
        <span className={styles.price}>{inr(contract.price, 2)}</span>
      </div>
      <div className={styles.row}>
        <span className={styles.expiry}>{contract.description.replace('|', '·')}{contract.illiquid && <button type="button" className={styles.tagButton} aria-label={t('illiquid.open')} onClick={onIlliquid}><Tag color="error" variant="secondary" size="sm" iconLeft={<Icon icon={msBlock} size={12} />}>{t('asset.illiquid')}</Tag></button>}</span>
        <PriceChange value={contract.change} unit="percent" size="md" />
      </div>
    </div>
  </Sheet>
}
```

### `src/flows/fno/commodities/sheets/TrendInfoSheet.module.css`

```css
/* Trend info sheet (live app reference, 2026-11-17) on L3 tokens. */
/* The trend row: a hairline under it, 16 to the bullets (the Stack's gap). */
.summary { padding-bottom: var(--l3-spacing-16); border-bottom: 1px solid var(--l3-border-light); }
.symbol { font: var(--l3-text-heading-16); color: var(--l3-content-primary); white-space: nowrap; }
.notes { display: flex; flex-direction: column; gap: var(--l3-spacing-12); margin: 0; padding-left: var(--l3-spacing-20); font: var(--l3-text-description-14); color: var(--l3-content-primary); }
/* The disclaimer: a grey note (surface-secondary, radius 12), warning icon + title over the line. */
.disclaimer { padding: var(--l3-spacing-12) var(--l3-spacing-16); border-radius: var(--l3-radius-12); background: var(--l3-surface-secondary); }
.disclaimerTitle { font: var(--l3-text-label-12); color: var(--l3-content-primary); }
.disclaimerText { margin: 0; font: var(--l3-text-description-12); color: var(--l3-content-secondary); }
/* "Analyzed by Dash": a dashed rule above, the Dash orb at 24 next to the line. */
.byDash { padding-top: var(--l3-spacing-16); border-top: 1px dashed var(--l3-border-light); font: var(--l3-text-label-14); color: var(--l3-content-secondary); }
.byDash [data-size] { --orb-box: var(--l3-size-24); }
```

### `src/flows/fno/commodities/sheets/TrendInfoSheet.tsx`

```tsx
import { Button } from '@l3/components/Button'
import { ButtonGroup } from '@l3/components/ButtonGroup'
import { Icon } from '@l3/components/Icon'
import { PriceChange } from '@l3/components/PriceChange'
import { Stack } from '@l3/components/Stack'
import { msWarning } from '@l3/icons/material'
import { Sheet } from '../../../../shared/ui/Sheet'
import { DashOrb } from '../../../../shared/ui/dash/DashOrb'
import { t } from '../../copy'
import { TrendBadge } from '../../components/TrendBadge'
import type { ExpiringContract } from '../data'
import styles from './TrendInfoSheet.module.css'

/** The trend read-out's label and second line, as on the card: the outlook for an event card, else Strong Up / Downtrend. */
export const trendLabel = (c: ExpiringContract) => c.kind === 'event' ? c.outlook : t(c.trend === 'up' ? 'expiring.up' : 'expiring.down')
export const trendSince = (c: ExpiringContract) => c.kind === 'event' ? c.reason : t('expiring.since', { time: c.since })

/**
 * Why this trend — from the trend read-out on an Expiring This Week card (Strong Uptrend / Downtrend, or an event's
 * Bullish). Live app reference (phone screenshot, 2026-11-17): the trend (arrow, then label over since, left-aligned) on the left and the
 * contract with its day change on the right, a hairline, Dash's two bullets on what's behind it, the grey disclaimer,
 * a dashed rule, "Analyzed by Dash", then Okay. No sheet header: the trend row is the top (the dialog is named by
 * aria-label). Opens through the shared Sheet, so it stays inside the screen (the phone frame on desktop).
 */
export function TrendInfoSheet({ contract, onClose }: { contract: ExpiringContract; onClose: () => void }) {
  const label = trendLabel(contract)
  return (
    <Sheet
      onClose={onClose}
      label={t('trendInfo.label', { trend: label, symbol: contract.symbol })}
      footer={<ButtonGroup aria-label={t('trendInfo.label', { trend: label, symbol: contract.symbol })}><Button size="lg" onClick={onClose}>{t('trendInfo.okay')}</Button></ButtonGroup>}
    >
      <Stack gap="16">
        <Stack direction="horizontal" gap="12" align="center" justify="between" className={styles.summary}>
          <TrendBadge trend={contract.trend} label={label} since={trendSince(contract)} largeSince iconStart />
          <Stack gap="04" align="end">
            <span className={styles.symbol}>{contract.symbol}</span>
            <PriceChange value={contract.priceChange} unit="percent" size="md" />
          </Stack>
        </Stack>
        <ul className={styles.notes}>{contract.trendNotes.map((note) => <li key={note}>{note}</li>)}</ul>
        <Stack gap="08" className={styles.disclaimer}>
          <Stack direction="horizontal" gap="04" align="center" className={styles.disclaimerTitle}><Icon icon={msWarning} size={16} /><span>{t('trendInfo.disclaimerTitle')}</span></Stack>
          <p className={styles.disclaimerText}>{t('trendInfo.disclaimer')}</p>
        </Stack>
        <Stack direction="horizontal" gap="08" align="center" justify="center" className={styles.byDash}>
          <DashOrb size="sm" halo={false} />
          <span>{t('trendInfo.byDash')}</span>
        </Stack>
      </Stack>
    </Sheet>
  )
}
```

### `src/flows/fno/components/AutoTpSlIcon.module.css`

```css
/*
 * Auto TP/SL mark — Figma motion (get_motion_context, 11783:10106 / 10114 / 10122), 1.198 s, boomerang (alternate):
 * candle: opacity 0 → 1 and scaleY 0.15 → 1 by 0.2922, ease-out, then holds;
 * tp: opacity holds 0 until 0.2504, then 0 → 1 by 0.4591 ease-out; x holds 5 until 0.2504, then 5 → 0 by 0.4591 on
 *     cubic-bezier(0.2, 0, 0.2, 1.3) (overshoots a little);
 * sl: the same between 0.3756 and 0.5843.
 * Opacity and x have different easings, so each is its own animation.
 */
.icon {
  display: block;
  flex: none;
}

.candle line {
  stroke: var(--l3-content-primary);
  stroke-width: 1.5;
  stroke-linecap: round;
}

.candle rect {
  fill: var(--l3-content-primary);
}

.candle {
  transform-box: fill-box;
  transform-origin: 50% 100%;
  animation: candle var(--app-auto-tpsl-loop) linear infinite alternate both;
}

.tp {
  fill: var(--l3-surface-accent-indicator-up-default);
  animation:
    tpFade var(--app-auto-tpsl-loop) linear infinite alternate both,
    tpSlide var(--app-auto-tpsl-loop) linear infinite alternate both;
}

.sl {
  fill: var(--l3-surface-accent-indicator-down-default);
  animation:
    slFade var(--app-auto-tpsl-loop) linear infinite alternate both,
    slSlide var(--app-auto-tpsl-loop) linear infinite alternate both;
}

@keyframes candle {
  0% {
    opacity: 0;
    scale: 1 0.15;
    animation-timing-function: ease-out;
  }
  29.22%,
  100% {
    opacity: 1;
    scale: 1 1;
  }
}

@keyframes tpFade {
  0%,
  25.04% {
    opacity: 0;
    animation-timing-function: ease-out;
  }
  45.91%,
  100% {
    opacity: 1;
  }
}

@keyframes tpSlide {
  0%,
  25.04% {
    translate: 5px 0;
    animation-timing-function: var(--app-auto-tpsl-ease);
  }
  45.91%,
  100% {
    translate: 0 0;
  }
}

@keyframes slFade {
  0%,
  37.56% {
    opacity: 0;
    animation-timing-function: ease-out;
  }
  58.43%,
  100% {
    opacity: 1;
  }
}

@keyframes slSlide {
  0%,
  37.56% {
    translate: 5px 0;
    animation-timing-function: var(--app-auto-tpsl-ease);
  }
  58.43%,
  100% {
    translate: 0 0;
  }
}

@media (prefers-reduced-motion: reduce) {
  .candle,
  .tp,
  .sl {
    animation: none;
  }
}
```

### `src/flows/fno/components/AutoTpSlIcon.tsx`

```tsx
import styles from './AutoTpSlIcon.module.css'

/**
 * The Auto TP/SL mark in chart Settings (Figma 11756:79819 / 79827 / 79835), animated as in Figma: the candle grows up
 * from its base, then the TP bar (green, above) and the SL bar (red, below) slide in from the right; 1.198 s, played
 * forward then back, on a loop. Drawn in SVG on L3 tokens (Figma's export can't be downloaded here).
 */
export function AutoTpSlIcon() {
  return (
    <svg className={styles.icon} viewBox="0 0 24 24" width="24" height="24" aria-hidden="true">
      <g className={styles.candle}>
        <line x1="9" y1="5" x2="9" y2="19" />
        <rect x="6.5" y="8" width="5" height="8" rx="1" />
      </g>
      <rect className={styles.tp} x="14" y="5" width="8" height="3" rx="1.5" />
      <rect className={styles.sl} x="14" y="16" width="8" height="3" rx="1.5" />
    </svg>
  )
}
```

### `src/flows/fno/components/BreakevenExplainer.module.css`

```css
/*
 * How breakeven works · the example (copied from the designer's recording). L3 tokens; the orange and the profit fade
 * are local tokens (src/local-tokens.css: the recording's orange isn't in L3). Positions come from BreakevenExplainer:
 * each callout gets its anchor as --x / --y and places itself around it.
 */
.stage {
  position: relative;
  overflow: hidden;
  background: var(--l3-surface-primary);
  cursor: pointer; /* a tap plays it again */
  -webkit-tap-highlight-color: transparent;
}

.chart {
  position: absolute;
  inset: 0;
  display: block;
}

/* ---- Price axis: ₹101–₹103 grey on dashed gridlines; ₹100 (the buy) bold on a solid line. ---- */
.gridline,
.baseline {
  stroke: var(--l3-border-light);
  stroke-width: 1;
}

.gridline {
  stroke-dasharray: 4 3;
}

.axisLabel,
.axisEntry,
.zoneLabel,
.chip,
.bought,
.sold,
.ltp {
  position: absolute;
  left: var(--x);
  top: var(--y);
  white-space: nowrap;
}

.axisLabel,
.axisEntry,
.zoneLabel {
  transform: translateY(-50%);
}

.axisLabel {
  color: var(--l3-content-tertiary);
  font: var(--l3-text-description-12);
}

.axisEntry {
  color: var(--l3-content-primary);
  font: var(--l3-text-label-12);
}

/* V2: what the buy cost (₹0 → ₹100), L3's light blue. */
/* ---- Zones: orange charges (₹100 → B/E), a green fade for the net profit (B/E → ₹102). ---- */
.chargesZone {
  fill: var(--app-be-charges-zone);
}

.profitTop {
  stop-color: var(--app-be-profit-top);
}

.profitMid,
.profitBottom {
  stop-color: var(--l3-surface-accent-success-light);
}

.profitBottom {
  stop-opacity: 0.4;
}

.zoneLabel {
  font: var(--l3-text-label-12);
}

.zoneLabel[data-zone='charges'] {
  isolation: isolate;
  display: inline-flex;
  gap: var(--l3-spacing-04);
  color: var(--app-be-orange-text);
}

/* "Order charges" is the tag the charge tags stack into (the same white pill, behind its text), under the zone. */
.zoneLabel[data-zone='charges']::before {
  content: '';
  position: absolute;
  inset: calc(-1 * var(--l3-spacing-02) - 1px) calc(-1 * var(--l3-spacing-06) - 1px);
  z-index: -1;
  border: 1px solid var(--l3-border-light);
  border-radius: var(--l3-radius-06);
  background: var(--l3-surface-primary);
  box-shadow: var(--l3-shadow-elevation-low);
}

.zoneLabel[data-zone='profit'] {
  color: var(--l3-content-accent-success-default);
}

/* ---- The breakeven line and its chip (white, a B/E tag then the price), the chip's right edge on the plot's. ---- */
.breakevenLine {
  stroke: var(--app-be-orange);
  stroke-width: 1.25;
  stroke-dasharray: 4 3;
}

.chip {
  /* The chart's "Breakeven" tag (PositionOverlay, Figma 11756:79332), text only: warning-light fill and 1px edge,
     radius 4, Label/10 warning text, 16 tall (Figma 2 / 4 / 2 / 6 with the border inside). L3 theme tokens, so dark
     mode follows. */
  display: inline-flex;
  align-items: center;
  padding: calc(var(--l3-spacing-02) - 1px) calc(var(--l3-spacing-04) - 1px) calc(var(--l3-spacing-02) - 1px) calc(var(--l3-spacing-06) - 1px);
  border: 1px solid var(--l3-border-accent-warning-light);
  border-radius: var(--l3-radius-04);
  background: var(--l3-surface-accent-warning-light);
  color: var(--l3-content-accent-warning-default);
  font: var(--l3-text-label-10);
  transform: translate(-100%, -50%);
  transform-origin: right center;
}

/* ---- The price line, the buy dot, the ringed crossing marker, the green sell dot and their pulses. ---- */
.priceLine {
  fill: none;
  stroke: var(--l3-content-primary);
  stroke-width: 1.75;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.buyDot {
  fill: var(--l3-content-primary);
}

.crossingRing {
  fill: var(--app-be-charges-zone);
  stroke: var(--app-be-orange);
  stroke-width: 1.25;
}

.crossingPulse {
  fill: var(--app-be-orange);
}

.sellRing,
.sellRingDrawing {
  fill: var(--l3-surface-accent-success-light);
  stroke-width: 1.25;
}

.sellRing {
  stroke: var(--l3-border-accent-success-light);
}

.sellRingDrawing {
  stroke: var(--l3-border-accent-success-default);
}

.sellDot,
.sellPulse {
  fill: var(--l3-surface-accent-success-default);
}

/* ---- Callouts: white pills with a light edge and a soft shadow. ---- */
.bought,
.sold,
.ltp {
  border: 1px solid var(--l3-border-light);
  border-radius: var(--l3-radius-08);
  background: var(--l3-surface-primary);
  box-shadow: var(--l3-shadow-elevation-low);
}

/* "Bought at ₹100": under the buy dot, a notch on top pointing at it. */
.bought {
  padding: var(--l3-spacing-04) var(--l3-spacing-08);
  color: var(--l3-content-primary);
  font: var(--l3-text-label-12);
}

.bought::before,
.sold::after {
  content: '';
  position: absolute;
  width: var(--l3-spacing-08);
  height: var(--l3-spacing-08);
  background: var(--l3-surface-primary);
  rotate: 45deg;
}

.bought::before {
  top: calc(var(--l3-spacing-04) * -1 - 1px);
  left: var(--l3-spacing-16);
  border-top: 1px solid var(--l3-border-light);
  border-left: 1px solid var(--l3-border-light);
}

/* "Sold at ₹102": left of the sell dot, green edge and text, a tail pointing right at the dot. */
.sold {
  display: inline-flex;
  align-items: center;
  gap: var(--l3-spacing-06);
  padding: var(--l3-spacing-04) var(--l3-spacing-08) var(--l3-spacing-04) var(--l3-spacing-06);
  border-color: var(--l3-border-accent-success-light);
  box-shadow: none;
  color: var(--l3-content-accent-success-default);
  font: var(--l3-text-label-12);
  transform: translate(-100%, -50%);
}

.sold::after {
  top: calc(50% - var(--l3-spacing-04));
  right: calc(var(--l3-spacing-04) * -1 - 1px);
  border-top: 1px solid var(--l3-border-accent-success-light);
  border-right: 1px solid var(--l3-border-accent-success-light);
}

/* V2: the sell sits on a thin strip next to the B/E chip, so "Sold" goes above the dot (its right edge 10 past it), no tail. */
/* LTP: rides the line's head, centred above it — the last price the line passed. */
.ltp {
  display: flex;
  flex-direction: column;
  padding: var(--l3-spacing-02) var(--l3-spacing-08);
  transform: translate(-50%, -100%);
  transform-origin: center bottom;
}

.ltpName {
  color: var(--l3-content-secondary);
  font: var(--l3-text-description-10);
}

.ltpValue {
  color: var(--l3-content-primary);
  font: var(--l3-text-label-14);
}

/*
 * The intro the loop ends on (the stage cuts to surface/secondary): Figma's reveal (the video on 11802:369, 1.23 s,
 * measured frame by frame) —
 * - the mark: opacity 0 → 1 from 30 ms over 250 ms (linear); scale 0.55 → 1 from 100 ms over 400 ms on L3's pop easing;
 * - INTRODUCING, Breakeven Line, the one-liner: from 300 / 470 / 670 ms, each 400 ms (L3 long): opacity 0 → 1 linear,
 *   8 up → 0 ease-out.
 */
.intro {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: var(--l3-spacing-24) var(--l3-spacing-16);
  background: var(--l3-surface-secondary);
  text-align: center;
}

.introIcon {
  margin-bottom: var(--l3-spacing-16);
  animation:
    fadeIn var(--app-be-icon-fade) linear var(--app-be-icon-fade-delay) both,
    popIn var(--l3-motion-duration-ai-pop) var(--l3-motion-easing-ai-pop) var(--app-be-icon-pop-delay) both;
}

.overline,
.introTitle,
.introText {
  animation:
    fadeIn var(--l3-motion-duration-long) linear var(--app-be-rise-delay) both,
    riseIn var(--l3-motion-duration-long) ease-out var(--app-be-rise-delay) both;
}

.overline { --app-be-rise-delay: var(--app-be-overline-delay); }
.introTitle { --app-be-rise-delay: var(--app-be-title-delay); }
.introText { --app-be-rise-delay: var(--app-be-tagline-delay); }

@keyframes fadeIn {
  from {
    opacity: 0;
  }
}

@keyframes popIn {
  from {
    scale: 0.55;
  }
}

@keyframes riseIn {
  from {
    translate: 0 var(--l3-spacing-08);
  }
}

/* INTRODUCING: 12 bold, tracking 0.96 (Figma) — L3 has no overline style: heading-12 + local tracking. */
.overline {
  margin: 0;
  color: var(--l3-content-tertiary);
  font: var(--l3-text-heading-12);
  letter-spacing: var(--app-overline-tracking);
  text-transform: uppercase;
}

.introTitle {
  margin: var(--l3-spacing-04) 0 var(--l3-spacing-08);
  color: var(--l3-content-primary);
  font: var(--l3-text-heading-24);
}

.introText {
  margin: 0;
  max-width: calc(var(--l3-size-128) * 1.75);
  color: var(--l3-content-secondary);
  font: var(--l3-text-label-12);
}

/*
 * Zoomed in, the charges (designer's brief, 2026-11-03): a tag per band — white like the B/E chip, the name then the
 * rate — joined to its band by an orange leader and dot.
 */
.chargeTag {
  position: absolute;
  left: var(--x);
  top: var(--y);
  display: inline-flex;
  align-items: center;
  gap: var(--l3-spacing-04);
  padding: var(--l3-spacing-02) var(--l3-spacing-06);
  border: 1px solid var(--l3-border-light);
  border-radius: var(--l3-radius-06);
  background: var(--l3-surface-primary);
  box-shadow: var(--l3-shadow-elevation-low);
  color: var(--l3-content-primary);
  font: var(--l3-text-label-12);
  white-space: nowrap;
  transform: translateY(-50%);
}

/* Brokerage's tag is the small one (designer's call: Lemonn's brokerage is a small part of the charges). */
.chargeTag[data-size='small'] {
  gap: var(--l3-spacing-02);
  padding: 1px var(--l3-spacing-04);
  font: var(--l3-text-label-10);
}

.chargeRate {
  color: var(--l3-content-secondary);
}

.leader line {
  stroke: var(--app-be-orange);
  stroke-width: 1;
}

.leader circle {
  fill: var(--app-be-orange);
}
```

### `src/flows/fno/components/BreakevenExplainer.tsx`

```tsx
import { useEffect, useId, useLayoutEffect, useRef, useState, type CSSProperties } from 'react'
import { Icon } from '@l3/components/Icon'
import { msCheckCircleFill } from '@l3/icons/material'
import { inr } from '../../../shared/data/format'
import { t } from '../copy'
import { breakevenCharges, breakevenExample, exampleChargesTotal } from '../data'
import { BreakevenIcon } from './BreakevenIcon'
import styles from './BreakevenExplainer.module.css'

/**
 * The example in How breakeven works — copied from the designer's recording of the explainer (measured frame by frame),
 * plus the charges breakdown (designer's brief, 2026-11-03). A 15 s loop on a white stage:
 * 1. the price axis (₹100–₹103) and its dashed gridlines fade in; the buy dot pops in at ₹100 with "Bought at ₹100";
 * 2. the chart zooms in 2× on ₹100 → ₹100.30 (the charges are thin at the normal scale): ₹102–₹103 move up out
 *    of view and the charges zone fills one charge at a time, each a band as tall as its share of the charges, with a
 *    tag (name · ₹ on the ₹100 buy). Top down: STT, transaction, stamp duty, SEBI, and brokerage last at
 *    the bottom. They come in top down, so brokerage comes in last (₹0.02, a thin band, its tag the small one);
 * 3. it zooms back out: the bands close into one orange charges zone and the tags slide down under it, stacking into one
 *    tag that reads "Order charges" and stays under the zone; the breakeven line draws across its top at ₹100.30
 *    and its "Breakeven" tag comes in (the chart's tag: text only, no price);
 * 3. an LTP bubble rides the price line as it draws up to ₹102 (showing the last price it passed); where it crosses the
 *    breakeven line a ringed marker pulses;
 * 4. at ₹102 the bubble goes, a green dot pulses, "Sold at ₹102" slides in and the green net-profit zone grows from the
 *    breakeven line up to the sell price, labelled "Net Profit"; it holds;
 * 5. it holds on the finished chart, then plays again, on loop.
 * Every play OPENS with the intro (19 Nov, Anshul_Risk_Meter: "it should come every time") — the Breakeven mark,
 * INTRODUCING, Breakeven Line, the one-liner — for 2.5 s, fading into the chart: on open, on each loop and on a tap,
 * which (after the first play) starts it again from the intro.
 * `still` (reduced motion) shows the finished chart and no intro.
 */
export function BreakevenExplainer({ still = false }: { still?: boolean }) {
  const stageRef = useRef<HTMLDivElement>(null)
  const width = useWidth(stageRef, FIGMA_WIDTH)
  const [run, setRun] = useState(0)
  // Runs on: the loop (LOOP) brings the intro in at INTRO_AT and starts the chart again.
  const elapsed = useElapsed(!still, Infinity, run)
  const loop = Math.floor(elapsed / LOOP)
  const inLoop = elapsed % LOOP
  // The chart's own clock starts once the intro has had its time.
  const time = still ? PLAYED : Math.max(0, inLoop - INTRO_HOLD)
  const replay = () => { if (!still && elapsed >= EXPLAINER_LENGTH) setRun(run + 1) }

  return (
    <div
      ref={stageRef}
      className={styles.stage}
      style={{ height: HEIGHT }}
      role="button"
      tabIndex={0}
      aria-label={`${t('breakeven.chartLabel')} ${t('breakeven.replay')}`}
      onClick={replay}
      onKeyDown={(e) => { if (e.key === 'Enter' || e.key === ' ') { e.preventDefault(); replay() } }}
    >
      <ExampleChart time={time} width={width} />
      {!still && inLoop < INTRO_HOLD && <Intro key={loop} fade={1 - ramp(inLoop, [INTRO_HOLD - INTRO_OUT, INTRO_OUT])} />}
    </div>
  )
}

/**
 * Where each part comes in: [start, duration] in ms (t = 0 is the chart starting on a blank stage). From the B/E line
 * on, it's the recording's timing moved 3 s later for the charges breakdown. */
const SHOT = {
  axis: [150, 250],
  buyDot: [400, 200],
  bought: [650, 150],
  zoomIn: [1000, 500],
  chargeFill: [1550, 300], // the top band and its tag first; each one below CHARGE_STEP later, brokerage last
  zoomOut: [4100, 600],
  leadersOut: [4100, 150],
  zoneMerge: [4100, 600], // the bands close into one zone
  tagsMerge: [4100, 450], // the top tag first; each one below TAG_MERGE_STEP later
  tagsOut: [4600, 150], // the stacked tags cross-fade into the one "Order charges" tag under the zone
  chargesLabel: [4600, 150],
  breakevenLine: [4750, 450],
  breakevenChip: [5200, 200],
  ltpIn: [5550, 150],
  priceLine: [5800, 2150],
  crossingPulse: [120, 400], // after the line reaches the crossing
  ltpOut: [8000, 150],
  sellDot: [8000, 200],
  sellPulse: [8200, 500],
  sold: [8250, 150],
  profitZone: [8450, 550],
  profitLabel: [9150, 150],
} satisfies Record<string, [number, number]>

const CHARGE_STEP = 350
const TAG_MERGE_STEP = 30
/** The intro opens every play: its reveal (~1.1 s) and a hold, then it fades (INTRO_OUT) into the chart. */
const INTRO_HOLD = 2500
const INTRO_OUT = 300
/** How long the chart takes to finish (ms), its Net Profit label in. */
const PLAYED = SHOT.profitLabel[0] + SHOT.profitLabel[1]
/** From open until the chart has finished once (the sheet's button unlocks then; a tap can replay after it). */
export const EXPLAINER_LENGTH = INTRO_HOLD + PLAYED
/** One play: the intro, the chart, then 2.2 s on the finished chart before the next play's intro. */
const LOOP = EXPLAINER_LENGTH + 2200
/** The LTP value cross-fades for this long when the line passes a turn. */
const LTP_SWAP = 100

/** The plot, in px (measured at the card's 326 width in Figma; it stretches with the card). */
const FIGMA_WIDTH = 326
const HEIGHT = 286
const PLOT_LEFT = 53.5
const PLOT_RIGHT_INSET = 12.5
const AXIS_X = 12.5
const ZONE_LABEL_INSET = 8.5
/**
 * "Order charges" is a tag in the charge tags' column, 6 under the zone (its middle 17 under ₹100): the zone, ₹0.25
 * tall, is too thin to hold it. A tag's text starts 7 in (its 6 padding and 1 edge).
 */
const CHARGES_LABEL_DROP = 17
const TAG_TEXT_INSET = 7
/** Callouts around their dots: "Bought" hangs 12.5 below with its notch 20 in; "Sold" ends 10 left; LTP sits 8.5 above. */
const BOUGHT_GAP = 12.5
const BOUGHT_NOTCH_X = 20
const SOLD_GAP = 10
const LTP_GAP = 8.5
/** ₹100 sits at 209 and every rupee is 53 higher; zoomed in, 2× that (the charges zone twice its final height). */
const BASELINE = 209
const RUPEE = 53
const ZOOM = 2
const ZOOMED_RUPEE = RUPEE * ZOOM
const priceY = (price: number, perRupee: number) => BASELINE - (price - breakevenExample.entry) * perRupee
/**
 * Zoomed in, each charge is a band of the zone, as tall as its share of the charges (at least 2, so SEBI's ~0.1% still
 * shows; the rest shrink to make room), 1 apart. Their tags sit in a column 140 from the plot's right, at least 24
 * apart and 10 from the top, each joined by a leader to a dot 20 left of it at its band's middle.
 */
const MIN_BAND = 2
const BAND_GAP = 1
const TAG_COLUMN = 140
const TAG_SPACING = 24
const TAG_TOP = 10
const LEADER = 20
const BANDS = chargeBands()

function ExampleChart({ time, width }: { time: number; width: number }) {
  const gradientId = useId()
  const { entry, breakeven, exit, axis, path } = breakevenExample
  const zoomIn = ramp(time, SHOT.zoomIn, easeInOut)
  const zoomOut = ramp(time, SHOT.zoomOut, easeInOut)
  const perRupee = RUPEE + (ZOOMED_RUPEE - RUPEE) * zoomIn * (1 - zoomOut)
  const y = (price: number) => priceY(price, perRupee)
  const plotRight = width - PLOT_RIGHT_INSET
  const points = path.map((p) => ({ x: PLOT_LEFT + p.at * (plotRight - PLOT_LEFT), y: y(p.price), price: p.price }))
  const start = points[0]
  const end = points[points.length - 1]
  const crossing = points.find((p) => p.price === breakeven) ?? points[0]

  // The price line draws at a steady pace across the plot; its head is where the LTP bubble rides.
  const drawn = ramp(time, SHOT.priceLine)
  const headX = start.x + drawn * (end.x - start.x)
  const passed = points.filter((p) => p.x <= headX)
  const next = points[passed.length]
  const last = passed[passed.length - 1] ?? start
  const head = next ? { x: headX, y: last.y + ((headX - last.x) / (next.x - last.x)) * (next.y - last.y) } : end
  const crossedAt = SHOT.priceLine[0] + ((crossing.x - start.x) / (end.x - start.x)) * SHOT.priceLine[1]
  const lastTurnAt = SHOT.priceLine[0] + ((last.x - start.x) / (end.x - start.x)) * SHOT.priceLine[1]

  const axisIn = ramp(time, SHOT.axis)
  const profitZone = ramp(time, SHOT.profitZone, easeOut) * (y(breakeven) - y(exit))
  const ltp = ramp(time, SHOT.ltpIn, easeOut) * (1 - ramp(time, SHOT.ltpOut))
  const sellIn = ramp(time, SHOT.sellDot, easeOutBack)
  const chargeIn = (order: number) => SHOT.chargeFill[0] + (BANDS.length - 1 - order) * CHARGE_STEP
  const bandFill = (order: number) => ramp(time, [chargeIn(order), SHOT.chargeFill[1]], easeOut)
  const leadersShown = 1 - ramp(time, SHOT.leadersOut)
  const tagsShown = 1 - ramp(time, SHOT.tagsOut)
  const tagX = plotRight - TAG_COLUMN
  const labelX = tagX + TAG_TEXT_INSET
  const labelY = y(entry) + CHARGES_LABEL_DROP
  const tagMerge = (order: number) =>
    ramp(time, [SHOT.tagsMerge[0] + (BANDS.length - 1 - order) * TAG_MERGE_STEP, SHOT.tagsMerge[1]], easeInOut)

  return (
    <>
      <svg className={styles.chart} width={width} height={HEIGHT} viewBox={`0 0 ${width} ${HEIGHT}`} aria-hidden>
        <defs>
          <linearGradient id={gradientId} x1="0" y1="0" x2="0" y2="1">
            <stop offset="0" className={styles.profitTop} />
            <stop offset="0.6" className={styles.profitMid} />
            <stop offset="1" className={styles.profitBottom} />
          </linearGradient>
        </defs>
        <g opacity={axisIn}>
          {axis.map((price) => (
            <line key={price} className={price === entry ? styles.baseline : styles.gridline} x1={PLOT_LEFT} x2={plotRight} y1={y(price)} y2={y(price)} />
          ))}
        </g>
        {/* The charges zone: the bands fill up one by one; zooming out, the whole zone fades in over them and closes the gaps. */}
        {BANDS.map((band, order) => {
          const top = y(band.from + (band.to - band.from) * bandFill(order))
          const height = Math.max(0, y(band.from) - top - BAND_GAP)
          return height > 0 && <rect key={band.charge.id} className={styles.chargesZone} x={PLOT_LEFT} width={plotRight - PLOT_LEFT} y={top} height={height} />
        })}
        <rect className={styles.chargesZone} x={PLOT_LEFT} width={plotRight - PLOT_LEFT} y={y(breakeven)} height={y(entry) - y(breakeven)} opacity={ramp(time, SHOT.zoneMerge, easeInOut)} />
        {leadersShown > 0 &&
          BANDS.map((band, order) => {
            const shown = ramp(time, [chargeIn(order), SHOT.chargeFill[1]]) * leadersShown
            const middle = y((band.from + band.to) / 2)
            return (
              shown > 0 && (
                <g key={band.charge.id} className={styles.leader} opacity={shown}>
                  <line x1={tagX - LEADER} y1={middle} x2={tagX} y2={band.tagY} />
                  <circle cx={tagX - LEADER} cy={middle} r={2} />
                </g>
              )
            )
          })}
        <rect fill={`url(#${gradientId})`} x={PLOT_LEFT} width={plotRight - PLOT_LEFT} y={y(breakeven) - profitZone} height={profitZone} />
        <line
          className={styles.breakevenLine}
          x1={PLOT_LEFT}
          x2={PLOT_LEFT + ramp(time, SHOT.breakevenLine, easeInOut) * (plotRight - PLOT_LEFT)}
          y1={y(breakeven)}
          y2={y(breakeven)}
        />
        {drawn > 0 && <polyline className={styles.priceLine} points={[...passed, head].map((p) => `${p.x},${p.y}`).join(' ')} />}
        <circle className={styles.buyDot} cx={start.x} cy={start.y} r={4.5 * ramp(time, SHOT.buyDot, easeOutBack)} />
        {time >= crossedAt && (
          <g>
            <Pulse cx={crossing.x} cy={crossing.y} time={time - crossedAt} shot={SHOT.crossingPulse} className={styles.crossingPulse} />
            <circle className={styles.crossingRing} cx={crossing.x} cy={crossing.y} r={7.5} />
            <circle className={styles.buyDot} cx={crossing.x} cy={crossing.y} r={4} />
          </g>
        )}
        {drawn >= 1 && (
          <g>
            <Pulse cx={end.x} cy={end.y} time={time} shot={SHOT.sellPulse} className={styles.sellPulse} />
            <circle className={sellIn > 0 ? styles.sellRing : styles.sellRingDrawing} cx={end.x} cy={end.y} r={7.5} />
            <circle className={styles.sellDot} cx={end.x} cy={end.y} r={4.5 * sellIn} />
          </g>
        )}
      </svg>

      {axis.map((price) => (
        <span key={price} className={price === entry ? styles.axisEntry : styles.axisLabel} style={at(AXIS_X, y(price), axisIn)}>
          {inr(price, 0)}
        </span>
      ))}

      <span className={styles.chip} style={{ ...at(plotRight, y(breakeven), ramp(time, SHOT.breakevenChip, easeOut)), scale: `${0.9 + 0.1 * ramp(time, SHOT.breakevenChip, easeOut)}` }}>
        {/* Just "Breakeven", the chart's own tag (Figma 11756:79332), no price (19 Nov, user). */}
        {t('breakeven.chip')}
      </span>

      <span
        className={styles.zoneLabel}
        style={at(labelX, labelY, ramp(time, SHOT.chargesLabel))}
        data-zone="charges"
      >
        {t('breakeven.charges')}
        <span className={styles.chargeRate}>{t('breakeven.chargesTotal', { amount: chargeInr(exampleChargesTotal) })}</span>
      </span>
      <span className={styles.zoneLabel} style={at(PLOT_LEFT + ZONE_LABEL_INSET, y(exit) + 32.5, ramp(time, SHOT.profitLabel))} data-zone="profit">
        {t('breakeven.netProfit')}
      </span>

      {/* Zooming out, the tags slide into the zone and stack where its "Order charges" label comes in. */}
      {tagsShown > 0 &&
        BANDS.map((band, order) => {
          const shown = ramp(time, [chargeIn(order), SHOT.chargeFill[1]], easeOut)
          const merge = tagMerge(order)
          const tagY = band.tagY + (labelY - band.tagY) * merge
          return (
            shown > 0 && (
              <span key={band.charge.id} className={styles.chargeTag} data-size={band.charge.id === 'brokerage' ? 'small' : undefined} style={{ ...rise(at(tagX, tagY), shown, 0, 4), opacity: shown * tagsShown }}>
                {t(`breakeven.charge.${band.charge.id}`)}
                <span className={styles.chargeRate}>{chargeInr(band.charge.amount)}</span>
              </span>
            )
          )
        })}

      <span className={styles.bought} style={rise(at(start.x - BOUGHT_NOTCH_X, start.y + BOUGHT_GAP), ramp(time, SHOT.bought, easeOut), 0, 4)}>
        {t('breakeven.bought', { price: inr(entry, 0) })}
      </span>
      <span className={styles.sold} style={rise(at(end.x - SOLD_GAP, end.y), ramp(time, SHOT.sold, easeOut), 6, 0)}>
        <Icon icon={msCheckCircleFill} size={16} />
        {t('breakeven.sold', { price: inr(exit, 0) })}
      </span>

      {ltp > 0 && (
        <span className={styles.ltp} style={{ ...at(head.x, head.y - LTP_GAP, ltp), scale: `${0.9 + 0.1 * ltp}` }}>
          <span className={styles.ltpName}>{t('breakeven.ltp')}</span>
          <span key={last.price} className={styles.ltpValue} style={{ opacity: last === start ? 1 : ramp(time, [lastTurnAt, LTP_SWAP]) }}>
            {inr(last.price)}
          </span>
        </span>
      )}
    </>
  )
}

/**
 * The charges as bands of the zone, bottom to top (in rupees, so they follow the zoom), and where each tag sits when
 * zoomed in: at its band's middle, pushed up to stay TAG_SPACING apart, then back down to stay under TAG_TOP.
 */
function chargeBands() {
  const { entry, breakeven } = breakevenExample
  const zone = breakeven - entry
  const total = breakevenCharges.reduce((sum, charge) => sum + charge.amount, 0)
  const heights = breakevenCharges.map((charge) => Math.max((charge.amount / total) * zone, MIN_BAND / ZOOMED_RUPEE))
  const fit = zone / heights.reduce((sum, height) => sum + height, 0)
  let from = entry
  const bands = breakevenCharges.map((charge, order) => {
    const band = { charge, from, to: from + heights[order] * fit, tagY: 0 }
    from = band.to
    return band
  })
  bands.forEach((band, order) => {
    const middle = priceY((band.from + band.to) / 2, ZOOMED_RUPEE)
    band.tagY = order === 0 ? middle : Math.min(middle, bands[order - 1].tagY - TAG_SPACING)
  })
  for (let order = bands.length - 1; order >= 0; order--) {
    const above = bands[order + 1]
    bands[order].tagY = Math.max(bands[order].tagY, above ? above.tagY + TAG_SPACING : TAG_TOP)
  }
  return bands
}

/** A charge in ₹: paise to 2 places (₹0.15); the tiny ones to their first digit (₹0.003, ₹0.0002). */
export function chargeInr(amount: number) {
  return `₹${amount >= 0.01 ? amount.toFixed(2) : Number(amount.toPrecision(1))}`
}

/** A ring that grows from the marker (7.5 → 14) and fades. */
function Pulse({ cx, cy, time, shot, className }: { cx: number; cy: number; time: number; shot: [number, number]; className: string }) {
  const p = ramp(time, shot, easeOut)
  if (p <= 0 || p >= 1) return null
  return <circle className={className} cx={cx} cy={cy} r={7.5 + 6.5 * p} opacity={0.4 * (1 - p)} />
}

/** The intro every play opens with: Figma's reveal (its timings are CSS animations, so it plays each time it mounts). */
function Intro({ fade = 1 }: { fade?: number }) {
  return (
    <div className={styles.intro} style={{ opacity: fade }}>
      <BreakevenIcon variant="tile" className={styles.introIcon} />
      <p className={styles.overline}>{t('breakeven.introducing')}</p>
      <p className={styles.introTitle}>{t('breakeven.lineName')}</p>
      <p className={styles.introText}>{t('breakeven.tagline')}</p>
    </div>
  )
}

/** A callout anchored at (x, y) on the stage; each callout's CSS places itself around that point. */
function at(x: number, y: number, opacity = 1): CSSProperties {
  return { '--x': `${x}px`, '--y': `${y}px`, opacity } as CSSProperties
}

/** Comes in by `progress`, moving from (dx, dy) px away to its place. */
function rise(style: CSSProperties, progress: number, dx: number, dy: number): CSSProperties {
  return { ...style, opacity: progress, translate: `${dx * (1 - progress)}px ${dy * (1 - progress)}px` }
}

/** 0 → 1 over [start, duration], eased. */
function ramp(time: number, [start, duration]: [number, number], ease = linear) {
  return ease(Math.min(1, Math.max(0, (time - start) / duration)))
}
const linear = (x: number) => x
const easeOut = (x: number) => 1 - (1 - x) ** 3
const easeInOut = (x: number) => (x < 0.5 ? 4 * x ** 3 : 1 - (-2 * x + 2) ** 3 / 2)
const easeOutBack = (x: number) => 1 + 2.70158 * (x - 1) ** 3 + 1.70158 * (x - 1) ** 2

/** Milliseconds since the play started, every frame, stopping at `until`; a new `run` plays it again from 0. */
function useElapsed(playing: boolean, until: number, run: number) {
  const [elapsed, setElapsed] = useState(0)
  useEffect(() => {
    if (!playing) return
    let frame = 0
    let start: number | undefined
    setElapsed(0)
    const tick = (now: number) => {
      start ??= now
      const passed = Math.min(now - start, until)
      setElapsed(passed)
      if (passed < until) frame = requestAnimationFrame(tick)
    }
    frame = requestAnimationFrame(tick)
    return () => cancelAnimationFrame(frame)
  }, [playing, until, run])
  return elapsed
}

/** The element's width, kept current. */
function useWidth(ref: React.RefObject<HTMLElement | null>, fallback: number) {
  const [width, setWidth] = useState(fallback)
  useLayoutEffect(() => {
    const element = ref.current
    if (!element) return
    const observer = new ResizeObserver(() => setWidth(element.clientWidth))
    observer.observe(element)
    setWidth(element.clientWidth)
    return () => observer.disconnect()
  }, [ref])
  return width
}
```

### `src/flows/fno/components/BreakevenIcon.module.css`

```css
/* Breakeven marks (How breakeven works). L3 colour tokens only. */

/* 48 tile (Figma 11989:36412): radius 12, 12 padding around the 24 arrow, a dark gradient — surface/quaternary far above
   the tile fading into surface/inverted, so only a soft lift shows at the top. The SAME in light and dark mode (19 Nov,
   user): L3's fixed base neutrals (charcoal-200 / -900 = the light theme's quaternary / inverted), not the theme tokens,
   which flip in dark mode. */
.tile {
  display: grid;
  place-items: center;
  width: var(--l3-size-48);
  height: var(--l3-size-48);
  box-sizing: border-box;
  padding: var(--l3-spacing-12);
  border-radius: var(--l3-radius-12);
  background: linear-gradient(
    to bottom,
    color-mix(in srgb, var(--l3-base-neutral-charcoal-200) 20%, var(--l3-base-neutral-charcoal-900)) 0%,
    var(--l3-base-neutral-charcoal-900) 100%
  );
}

.tile img { display: block; }

.small {
  display: block;
  flex: none;
}

.smallDashed {
  stroke: var(--l3-border-accent-warning-default);
  stroke-width: 1.5;
  stroke-dasharray: 2.5 2;
}

.chip {
  fill: var(--l3-surface-accent-warning-light);
  stroke: var(--l3-border-accent-warning-default);
  stroke-width: 1;
}

.small[data-variant='up'] .smallDashed {
  stroke: var(--l3-content-tertiary);
}

.smallArrow {
  fill: none;
  stroke: var(--l3-content-accent-success-default);
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;
}
```

### `src/flows/fno/components/BreakevenIcon.tsx`

```tsx
import tileArrow from '../assets/breakeven-tile-arrow.svg'
import styles from './BreakevenIcon.module.css'

type BreakevenIconProps = {
  /**
   * tile: the 48 "Breakeven" mark (Figma 11989:36412) — a dark tile, Figma's own 24 arrow (lime gradient) in the middle;
   * line: 20, the yellow breakeven line with its chip (11783:12573); up: 20, a green arrow over the line (11783:12586).
   */
  variant: 'tile' | 'line' | 'up'
  className?: string
}

/**
 * The breakeven marks of How breakeven works. The tile uses Figma's exported arrow (assets/breakeven-tile-arrow.svg,
 * 19 Nov) and keeps the same colours in light and dark mode; the 20 marks are drawn to match in SVG on L3 colour tokens
 * (an L3 gap: no breakeven icon in the icon set).
 */
export function BreakevenIcon({ variant, className }: BreakevenIconProps) {
  if (variant === 'tile') {
    return (
      <span className={`${styles.tile} ${className ?? ''}`} aria-hidden="true">
        <img src={tileArrow} width="24" height="24" alt="" />
      </span>
    )
  }
  return (
    <svg className={`${styles.small} ${className ?? ''}`} data-variant={variant} viewBox="0 0 20 20" width="20" height="20" aria-hidden="true">
      <line className={styles.smallDashed} x1="1" y1="12" x2="19" y2="12" />
      {variant === 'line' ? (
        <rect className={styles.chip} x="11" y="8.5" width="8" height="7" rx="1.5" />
      ) : (
        <path className={styles.smallArrow} d="M10 17V4M6 8l4-4 4 4" />
      )}
    </svg>
  )
}
```

### `src/flows/fno/components/ContractSection.tsx`

```tsx
import { useState } from 'react'
import { Button } from '@l3/components/Button'
import { Card } from '@l3/components/Card'
import { EmptyState } from '@l3/components/EmptyState'
import { Icon } from '@l3/components/Icon'
import { PriceChange } from '@l3/components/PriceChange'
import { SectionHeader } from '@l3/components/SectionHeader'
import { Select } from '@l3/components/Select'
import { Stack } from '@l3/components/Stack'
import { Tab, Tabs } from '@l3/components/Tabs'
import { lmSwitchArrowVertical } from '@l3/icons/lemonnade'
import { msFilterList } from '@l3/icons/material'
import { inr } from '../../../shared/data/format'
import { futures, options, stockOptions, type Contract } from '../data'
import { t } from '../copy'
import styles from './HomeParts.module.css'

export type Choose = (title: string, values: string[], value: string, onPick: (value: string) => void) => void

/** `contracts` replaces the Equity sample (the Commodities tab passes its own Smart Futures). */
export function ContractSection({ kind, contracts, onChoose, onContract, onViewAll }: { kind: 'options' | 'futures'; contracts?: Contract[]; onChoose: Choose; onContract: (contract: Contract) => void; onViewAll: () => void }) {
  const [category, setCategory] = useState(kind === 'options' ? 'top' : 'long')
  const [stock, setStock] = useState(false)
  const [volume, setVolume] = useState(false)
  const [filter, setFilter] = useState(t('filter.all'))
  const categories = kind === 'options' ? [
    { value: 'top', label: t('options.top') }, { value: 'active', label: t('options.active') }, { value: 'oi', label: t('options.oi') }, { value: 'advanced', label: t('options.advanced') },
  ] : [
    { value: 'long', label: t('futures.long') }, { value: 'covering', label: t('futures.covering') }, { value: 'short', label: t('futures.short') }, { value: 'unwind', label: t('futures.unwind') },
  ]
  const keys = categories.map((c) => c.value)
  const source = contracts ?? (kind === 'futures' ? futures : stock ? stockOptions : options)
  const filterChoices = kind === 'options' ? [t('filter.all'), t('filter.calls'), t('filter.puts')] : [t('filter.all'), t('filter.gainers'), t('filter.losers')]
  const matching = source.filter((c) => filter === t('filter.puts') ? c.side === 'put' : filter === t('filter.calls') ? c.side === 'call' : filter === t('filter.gainers') ? c.change > 0 : filter === t('filter.losers') ? c.change < 0 : true)
  // Categories select distinct orderings of this small snapshot; volume sort is descending.
  const offset = keys.indexOf(category)
  const ordered = [...matching.slice(offset), ...matching.slice(0, offset)]
  const rows = volume ? ordered.sort((a, b) => b.volume - a.volume) : ordered
  return <section className={styles.contractSection} aria-label={t(`${kind}.title`)}>
    <SectionHeader title={t(`${kind}.title`)} action={{ type: 'view-all', label: t('viewAll'), onClick: onViewAll }} />
    <Stack direction="horizontal" gap="08" align="center" className={styles.filterRow}>
      {kind === 'options' && <Tab appearance="pill" size="sm" action iconRight={<Icon icon={lmSwitchArrowVertical} size={12} />} onClick={() => setStock(!stock)} aria-label={t('scope.label')}>{t(stock ? 'scope.stock' : 'scope.index')}</Tab>}
      <Tabs aria-label={t(`${kind}.title`)} appearance="pill" size="sm" items={categories} value={category} onChange={setCategory} />
    </Stack>
    <Stack direction="horizontal" align="center" justify="between">
      <Button variant="ghost" size="sm" iconLeft={<Icon icon={msFilterList} size={12} />} onClick={() => onChoose(t('filter'), filterChoices, filter, setFilter)}>{filter === t('filter.all') ? t('filter') : filter}</Button>
      <Select size="sm" aria-label={t('sort.label')} onClick={() => setVolume(!volume)}>{t(volume ? 'sort.volume' : 'sort.price')}</Select>
    </Stack>
    <Stack gap="12">{rows.map((contract) => <Card key={contract.id} onClick={() => onContract(contract)}>
      <Stack direction="horizontal" gap="08" justify="between" align="center"><Stack gap="04" className={styles.grow}><p className={styles.heading}>{contract.name}</p><p className={styles.description}>{contract.description}</p></Stack><Stack gap="04" align="end"><p className={styles.heading}>{volume ? contract.volume.toLocaleString('en-IN') : inr(contract.price, 2)}</p><PriceChange value={contract.change} unit="percent" size="sm" /></Stack></Stack>
    </Card>)}{rows.length === 0 && <EmptyState title={t('empty')} description={t('empty.description')} />}</Stack>
  </section>
}
```

### `src/flows/fno/components/Discovery.tsx`

```tsx
import { Avatar } from '@l3/components/Avatar'
import { Button } from '@l3/components/Button'
import { Card } from '@l3/components/Card'
import { Icon } from '@l3/components/Icon'
import { SectionHeader } from '@l3/components/SectionHeader'
import { Stack } from '@l3/components/Stack'
import { msAdd, msChevronRight } from '@l3/icons/material'
import { Rail } from '../../../shared/ui/Rail'
import { ShortcutCircles } from '../../../shared/ui/ShortcutCircles'
import analysisIcon from '../assets/shortcuts/analysis.svg'
import ipoIcon from '../assets/shortcuts/ipo.svg'
import watchlistIcon from '../assets/shortcuts/watchlist.svg'
import referralIcon from '../assets/shortcuts/referral.svg'
import { t } from '../copy'
import type { Watchlist } from '../data'
import styles from './HomeParts.module.css'

/** F&O Home's shortcuts, Figma 6754:62886 (24 Nov, the user's call: "copy this exact design"): Analysis · IPO ·
 *  Watchlist · Referral, each a 40 disc with Figma's two-tone green Streamline icon (assets/shortcuts) and its name under it.
 *  Drawn with the shared ShortcutCircles. */
export function Shortcuts({ onWatchlist, onDestination }: { onWatchlist: () => void; onDestination: (label: string) => void }) {
  const art = (src: string) => <img src={src} alt="" />
  const items = [
    { id: 'analysis', label: t('shortcut.analysis'), icon: art(analysisIcon) },
    { id: 'ipo', label: t('shortcut.ipo'), icon: art(ipoIcon) },
    { id: 'watchlist', label: t('shortcut.watchlist'), icon: art(watchlistIcon) },
    { id: 'referral', label: t('shortcut.referral'), icon: art(referralIcon) },
  ]
  return (
    <div className={styles.shortcuts}>
      <ShortcutCircles items={items} tone="in" label={t('shortcut.label')} onOpen={(id) => (id === 'watchlist' ? onWatchlist() : onDestination(items.find((i) => i.id === id)!.label))} />
    </div>
  )
}

export function Watchlists({ lists, onAdd, onOpen }: { lists: Watchlist[]; onAdd: () => void; onOpen: (name: string) => void }) {
  return <section className={styles.watchlists} aria-label={t('shortcut.watchlist')}>
    <Stack direction="horizontal" align="center" justify="between" className={styles.inset}><SectionHeader title={t('watchlists.title', { count: lists.length })} /><Button variant="ghost" size="sm" iconLeft={<Icon icon={msAdd} size={12} />} onClick={onAdd}>{t('watchlists.add')}</Button></Stack>
    <Rail label={t('shortcut.watchlist')} visible={1.4}>{lists.map((list) => <Card key={list.id} onClick={() => onOpen(list.name)}>
      <Stack direction="horizontal" gap="12" align="center"><Avatar initials={list.name[0]} size={40} /><Stack gap="04" className={styles.grow}><p className={styles.heading}>{list.name}</p><p className={styles.description}>{t('watchlists.count', { count: list.count })}</p></Stack><Icon icon={msChevronRight} size={20} /></Stack>
    </Card>)}</Rail>
  </section>
}
```

### `src/flows/fno/components/FnoNav.tsx`

```tsx
import { BottomNavbar } from '@l3/components/BottomNavbar'
import { NavIcon } from '@l3/components/BottomNavbar/NavIcon'
import { FloatingNav, FloatingNavIcon, useBottomNavVariant, useColourNavIcons, useFloatingNav } from '../../../shared/ui/FloatingNav'
import { t } from '../copy'

export function FnoNav({ onHome, onDestination, onChain, onScalper }: { onHome: () => void; onDestination: (label: string) => void; onChain: () => void; onScalper: () => void }) {
  const items = [
    { value: 'fno', label: t('title'), name: 'fno' },
    { value: 'chain', label: t('nav.chain'), name: 'fnoOptionChain' },
    { value: 'positions', label: t('nav.positions'), name: 'fnoPositions' },
    { value: 'scalper', label: t('nav.scalper'), name: 'fnoScalper' },
  ] as const
  const variant = useBottomNavVariant()
  // V2: the chosen F&O icon in black and white, like the main nav's; V3 keeps L3's coloured one (23 Nov, user)
  const colourNav = useColourNavIcons()
  const floating = useFloatingNav() && !colourNav
  return <FloatingNav><BottomNavbar aria-label="F&O" variant={variant} home={{ label: t('nav.home'), onClick: onHome }} value="fno" onChange={(v) => { const item = items.find((i) => i.value === v); if (v === 'scalper') onScalper(); else if (v === 'chain') onChain(); else if (item && v !== 'fno') onDestination(item.label) }} items={items.map(({ value, label, name }) => ({ value, label, icon: <NavIcon name={name} />, selectedIcon: floating && name === 'fno' ? <FloatingNavIcon name="fno" selected /> : <NavIcon name={name} selected /> }))} /></FloatingNav>
}
```

### `src/flows/fno/components/Header.module.css`

```css
.bar { display: flex; align-items: center; gap: var(--l3-spacing-12); height: var(--app-topbar-height); padding-inline: var(--l3-spacing-16); background: var(--l3-surface-secondary); transition: background-color var(--l3-motion-duration-short) var(--l3-motion-easing-standard); }
.bar[data-scrolled] { background: var(--l3-surface-primary); }
.bar > :is(.profile, .search, .wallet) { display: inline-flex; flex: none; align-items: center; justify-content: center; height: var(--app-stocks-topbar-control); padding: 0; border: 0; color: var(--l3-content-primary); cursor: pointer; -webkit-tap-highlight-color: transparent; transition: transform var(--l3-motion-duration-short) var(--l3-motion-easing-standard); }
.bar > :is(.profile, .search, .wallet):active { transform: scale(var(--l3-motion-scale-press-default)); }
.bar > :is(.profile, .search, .wallet):focus-visible { outline: 2px solid var(--l3-content-primary); outline-offset: 2px; }
.bar .profile { width: var(--app-stocks-topbar-avatar); height: var(--app-stocks-topbar-avatar); border-radius: var(--l3-radius-full); background: var(--l3-surface-accent-indigo-light); box-shadow: inset 0 0 0 1px var(--l3-border-accent-indigo-default); /* 1px ring: the user's profile keeps it (18 Nov) */ color: var(--l3-content-accent-indigo-default); font: var(--l3-text-label-14); }
.bar .search { flex: 1; min-width: 0; justify-content: flex-start; gap: var(--l3-spacing-08); padding-inline: var(--l3-spacing-12); border-radius: var(--l3-radius-full); background: var(--l3-surface-default); box-shadow: inset 0 0 0 1px var(--l3-border-light); }
.placeholder { overflow: hidden; color: var(--l3-content-secondary); font: var(--l3-text-label-14); text-overflow: ellipsis; white-space: nowrap; }
.wallet { width: var(--app-stocks-topbar-control); border-radius: var(--l3-radius-full); background: var(--l3-surface-default); box-shadow: inset 0 0 0 1px var(--l3-border-light); }
```

### `src/flows/fno/components/Header.tsx`

```tsx
import { Icon } from '@l3/components/Icon'
import { msAccountBalanceWallet, msSearch } from '@l3/icons/material'
import { DashEntry } from '../../../shared/ui/dash/DashEntry'
import { t } from '../copy'
import styles from './Header.module.css'
import { TopBarAction } from '../../../shared/ui/TopBarAction'

type HeaderProps = {
  initials: string
  scrolled?: boolean
  onProfile: () => void
  onSearch: () => void
  onWallet: () => void
  onDash: () => void
}

/** F&O's local instance of the Stocks home header: profile, search, DASH and wallet. */
export function Header({ initials, scrolled = false, onProfile, onSearch, onWallet, onDash }: HeaderProps) {
  return <header className={styles.bar} data-scrolled={scrolled || undefined}>
    <button type="button" className={styles.profile} aria-label={t('top.profile')} onClick={onProfile}>{initials}</button>
    <button type="button" className={styles.search} onClick={onSearch}>
      <Icon icon={msSearch} size={20} /><span className={styles.placeholder}>{t('top.search')}</span>
    </button>
    <DashEntry label={t('top.dash')} ariaLabel={t('top.dash')} onClick={onDash} />
    <TopBarAction icon={msAccountBalanceWallet} label={t('top.wallet')} onClick={onWallet} />
  </header>
}
```

### `src/flows/fno/components/Heatmap.tsx`

```tsx
import { useState } from 'react'
import { Icon } from '@l3/components/Icon'
import { Card } from '@l3/components/Card'
import { SectionHeader } from '@l3/components/SectionHeader'
import { Stack } from '@l3/components/Stack'
import { Tab, Tabs } from '@l3/components/Tabs'
import { lmSwitchArrowVertical } from '@l3/icons/lemonnade'
import { heatmap } from '../data'
import { t } from '../copy'
import styles from './HomeParts.module.css'

export function Heatmap({ onOpen, onViewAll }: { onOpen: (name: string) => void; onViewAll: () => void }) {
  const [category, setCategory] = useState('auto')
  const [stock, setStock] = useState(true)
  const cells = category === 'auto' ? heatmap : heatmap.slice(category === 'financial' ? 0 : 3, category === 'financial' ? 6 : 9)
  return <section className={styles.heatmapSection} aria-label={t('heatmap.title')}>
    <div className={styles.inset}><SectionHeader title={t('heatmap.title')} action={{ type: 'view-all', label: t('viewAll'), onClick: onViewAll }} /></div>
    <Stack direction="horizontal" gap="08" className={styles.heatmapRow}>
      <Tab appearance="pill" size="sm" action iconRight={<Icon icon={lmSwitchArrowVertical} size={12} />} aria-label={t('scope.label')} onClick={() => setStock(!stock)}>{t(stock ? 'scope.stock' : 'scope.index')}</Tab>
      <Tabs appearance="pill" size="sm" aria-label={t('heatmap.title')} value={category} onChange={setCategory} items={(['auto', 'financial', 'fmcg'] as const).map((value) => ({ value, label: t(`heatmap.${value}`) }))} />
    </Stack>
    <div className={styles.heatmap}>{cells.map((cell, i) => <Card variant="flat" key={cell.id} className={[styles.heatCell, cell.tone === 'up' ? styles.heatUp : styles.heatDown].join(' ')} onClick={() => onOpen(stock ? cell.name : ['NIFTY 50', 'BANK NIFTY', 'SENSEX'][i % 3])}>
      <span className={styles.heatName}>{stock ? cell.name : ['NIFTY 50', 'BANK NIFTY', 'SENSEX'][i % 3]}</span><span><strong>{cell.change.toFixed(2)}%</strong><span className={styles.heatPrice}>{cell.price}</span></span>
    </Card>)}</div>
  </section>
}
```

### `src/flows/fno/components/HomeParts.module.css`

```css
/* F&O home composition and custom heatmap. */
.overview { padding: 0 0 var(--l3-spacing-24); background: var(--l3-surface-secondary); }
.inset { padding-inline: var(--l3-spacing-16); }
.amount { font: var(--l3-text-heading-24); white-space: nowrap; }
.indices { display: flex; gap: var(--l3-spacing-16); overflow: hidden; }
/* Zing signals card (Figma "Logo Container"): flush with the screen's left edge, open on the left, rounded on the right,
   a zing-honey outline and a honey → white wash from the top. Overrides L3 Card's border, radius and padding on purpose. */
.zing.zing { flex: none; width: max-content; display: flex; flex-direction: column; align-items: flex-start; justify-content: center; gap: var(--l3-spacing-06); padding: var(--l3-spacing-10) var(--l3-spacing-08) var(--l3-spacing-12); border: 1px solid var(--l3-border-accent-zing-default); border-left: 0; border-radius: 0 var(--l3-radius-12) var(--l3-radius-12) 0; background: linear-gradient(179deg, var(--l3-surface-accent-zing-light) 1%, var(--l3-surface-primary) 50%); box-shadow: var(--l3-shadow-elevation-low); }
.zing img { display: block; }
.indexRail { display: flex; min-width: 0; flex: 1; gap: var(--l3-spacing-12); overflow-x: auto; padding-right: var(--l3-spacing-16); scrollbar-width: none; }
.indexCard { flex: none; width: max-content; }
.label, .secondaryLabel, .up, .down { font: var(--l3-text-label-12); white-space: nowrap; }
.secondaryLabel { color: var(--l3-content-secondary); }
.up { color: var(--l3-content-accent-indicator-up-default); }
.down { color: var(--l3-content-accent-indicator-down-default); }
.caption { font: var(--l3-text-description-10); color: var(--l3-content-secondary); }
.heading { font: var(--l3-text-heading-14); overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
.description { font: var(--l3-text-description-12); color: var(--l3-content-secondary); white-space: nowrap; }
.grow { flex: 1; min-width: 0; }
.feed { padding-block: var(--l3-spacing-24) 0; } /* page end: the body's --app-body-end */
.ribbonIcon { display: inline-flex; width: var(--l3-size-16); height: var(--l3-size-16); }
/* The shortcuts row (shared ShortcutCircles brings its own 16 at the sides): 8 above it, as before. */
.shortcuts { padding-top: var(--l3-spacing-08); }
.actionIcon { display: inline-flex; align-items: center; justify-content: center; width: var(--l3-size-20); height: var(--l3-size-20); }
.shortcutLarge { display: inline-flex; align-items: center; justify-content: center; width: var(--l3-size-24); height: var(--l3-size-24); }
.asset { display: block; flex: none; }
:global([data-mode='dark']) .asset { filter: invert(1); }
.chartSection { display: flex; flex-direction: column; gap: var(--l3-spacing-16); padding-inline: var(--l3-spacing-16); }
.trendIcon { display: inline-flex; width: var(--l3-size-20); height: var(--l3-size-20); color: var(--l3-content-accent-indicator-down-default); }
.trendIcon[data-trend='up'] { color: var(--l3-content-accent-indicator-up-default); transform: scaleY(-1); }
.chart { width: 100%; display: block; }
.divider { border-top: 1px solid var(--l3-border-light); }
.watchlists, .heatmapSection { display: flex; flex-direction: column; gap: var(--l3-spacing-16); }
.contractSection { display: flex; flex-direction: column; gap: var(--l3-spacing-16); padding-inline: var(--l3-spacing-16); }
.filterRow { overflow: hidden; }
.filterRow > :first-child { flex: none; }
.filterRow > [role='tablist'] { min-width: 0; }
.heatmapRow { padding-inline: var(--l3-spacing-16); overflow: hidden; }
.heatmapRow > :first-child { flex: none; }
.heatmapRow > [role='tablist'] { min-width: 0; }
.heatmap { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 1px; }
.heatCell { display: flex; flex-direction: column; justify-content: space-between; gap: var(--l3-spacing-24); min-width: 0; aspect-ratio: 1; padding: var(--l3-spacing-16) var(--l3-spacing-12); border: 0; color: var(--l3-content-inverted); text-align: center; cursor: pointer; }
.heatCell.heatCell.heatUp { background: var(--l3-surface-accent-indicator-up-default); }
.heatCell.heatCell.heatDown { background: var(--l3-surface-accent-indicator-down-default); }
.heatName { font: var(--l3-text-heading-12); }
.heatCell strong { display: block; font: var(--l3-text-heading-16); }
.heatPrice { display: block; margin-top: var(--l3-spacing-04); font: var(--l3-text-label-14); opacity: var(--l3-opacity-60, 0.6); }

/*
 * F&O product tabs — the approved exception to L3 Ribbon (Figma 6754:63641): grey row on surface/secondary with a green
 * baseline; Label/12; the selected tab has a success-green outline and a green-50 → white wash from the top.
 */
.productTabs.productTabs { background: var(--l3-surface-secondary); box-shadow: inset 0 -1px 0 var(--app-fno-tabs-baseline); }
.productTabs.productTabs [role='tab'] { --tab-font: var(--l3-text-label-12); }
.productTabs.productTabs [role='tab'][aria-selected='true'] { --tab-border: var(--l3-border-accent-success-default); --tab-surface: var(--l3-surface-default); background-image: linear-gradient(180deg, var(--l3-surface-accent-success-light) 3%, var(--l3-surface-default)); }

/* A product tab switch: only the content under the tabs slides in, from the chosen tab's side. */
/* The product tabs stay put under the top bar once the page scrolls past them (they sit mid-page, so not in the
   Actionbar's bottom slot). */
.stickyTabs { position: sticky; top: 0; z-index: 2; }
/* Once stuck, the row (what the inactive tabs sit on) takes the scrolled top bar's colour (Header .bar[data-scrolled]);
   the active tab keeps its own gradient. */
.stickyTabs .productTabs.productTabs { transition: background-color var(--l3-motion-duration-short) var(--l3-motion-easing-standard); }
.stickyTabs[data-stuck] .productTabs.productTabs { background-color: var(--l3-surface-primary); }
.productContent { overflow-x: clip; }
.productContent[data-slide='from-end'] > * { animation: fno-in-from-end var(--l3-motion-duration-long) var(--l3-motion-easing-standard) both; }
.productContent[data-slide='from-start'] > * { animation: fno-in-from-start var(--l3-motion-duration-long) var(--l3-motion-easing-standard) both; }
@keyframes fno-in-from-end { from { transform: translateX(100%); } to { transform: none; } }
@keyframes fno-in-from-start { from { transform: translateX(-100%); } to { transform: none; } }
@media (prefers-reduced-motion: reduce) { .productContent > * { animation: none !important; } }
/* The trend read-out as one tap target (opens the trend info sheet): label, since, i and arrow, with the hit area
   grown 12 around it (top right of the Expiring card) so it's easy to hit. */
.trendButton { position: relative; display: inline-flex; align-items: center; gap: var(--l3-spacing-04); cursor: pointer; border-radius: var(--l3-radius-08); }
.trendButton::before { content: ''; position: absolute; inset: calc(-1 * var(--l3-spacing-12)); }
.trendButton:focus-visible { outline: var(--l3-spacing-02) solid var(--l3-border-dark); outline-offset: var(--l3-spacing-04); }
```

### `src/flows/fno/components/Overview.tsx`

```tsx
import { useState } from 'react'
import { Button } from '@l3/components/Button'
import { Card } from '@l3/components/Card'
import { Icon } from '@l3/components/Icon'
import { PriceChange } from '@l3/components/PriceChange'
import { Select } from '@l3/components/Select'
import { Stack } from '@l3/components/Stack'
import { Tag } from '@l3/components/Tag'
import { msArrowForward } from '@l3/icons/material'
import zing from '../assets/zing.svg'
import { indices } from '../data'
import { t } from '../copy'
import styles from './HomeParts.module.css'

export function Overview({ onDestination }: { onDestination: (name: string) => void }) {
  const [day, setDay] = useState(false)
  return <Stack gap="24" className={styles.overview}>
    <Stack direction="horizontal" align="center" justify="between" className={styles.inset}>
      <Stack gap="08">
        <Select size="sm" onClick={() => setDay(!day)}>{t(day ? 'pnl.day' : 'pnl.total')}</Select>
        <Stack direction="horizontal" gap="08" align="center"><p className={styles.amount}>{day ? '₹520.75' : '₹1,500.25'}</p><PriceChange value={day ? 4.2 : 12.4} unit="percent" size="md" decimals={1} /></Stack>
      </Stack>
      <Button variant="tertiary" size="sm" aria-label={t('pnl.open')} iconLeft={<Icon icon={msArrowForward} size={20} />} onClick={() => onDestination(t('nav.positions'))} />
    </Stack>
    <div className={styles.indices}>
      <Card onClick={() => onDestination(t('signals'))} className={styles.zing}><img src={zing} alt="Zing" /><Tag color="zing" variant="secondary" size="sm">{t('signals')}</Tag></Card>
      <div className={styles.indexRail}>
        {indices.map((index) => <Card key={index.name} onClick={() => onDestination(index.name)} className={styles.indexCard}>
          <Stack direction="horizontal" gap="04" align="center" justify="between"><p className={styles.secondaryLabel}>{index.name}</p><Tag color="discover" variant="secondary" size="sm">{index.expiry}</Tag></Stack>
          <Stack direction="horizontal" gap="04" align="center"><span className={styles.label}>{index.price}</span><PriceChange value={index.change} unit="number" size="sm" /><span className={styles.up}>({index.percent})</span></Stack>
        </Card>)}
      </div>
    </div>
  </Stack>
}
```

### `src/flows/fno/components/PositionOverlay.module.css`

```css
/*
 * A position on the option chart (Figma "Scalper screen · C · Boxed chip", 11756:78739). Laid over the plot; only the
 * pills, buttons and the breakeven chip take taps, so the chart under them still scrolls / zooms.
 */
.overlay {
  position: absolute;
  top: 0;
  left: 0;
  pointer-events: none;
}

/* Dashed lines across the plot. 1px hairlines. */
.line {
  position: absolute;
  left: 0;
  height: 0;
  border-top: 1px dashed var(--l3-border-dark);
}

.line[data-kind='tp'] {
  border-top-color: var(--l3-border-dark);
}

.line[data-kind='entry'] {
  border-top-color: var(--l3-content-primary);
}

.line[data-kind='sl'] {
  border-top-color: var(--l3-border-accent-indicator-down-light);
}

/* Breakeven: a solid 1px warning-light line (Figma 11756:79330, #FFDF88 in light); the theme token follows dark mode. */
.line[data-kind='be'] {
  border-top-color: var(--l3-border-accent-warning-light);
  border-top-style: solid;
}

/* The entry price on the axis: inverted, as tall as the last price's tag. */
.axisTag {
  position: absolute;
  display: flex;
  align-items: center;
  height: var(--l3-size-16);
  padding-left: var(--l3-spacing-02);
  border-radius: var(--l3-radius-02);
  background: var(--l3-surface-inverted);
  color: var(--l3-content-inverted);
  font: var(--l3-text-label-12);
  translate: 0 -50%;
}

/* A row of pills centred on its line: TP and SL from 64 in (past the entry row's Exit), the entry row from 12. */
.row {
  position: absolute;
  left: var(--l3-spacing-64);
  display: flex;
  align-items: center;
  gap: var(--l3-spacing-08);
  translate: 0 -50%;
}

.row[data-kind='entry'] {
  left: var(--l3-spacing-12);
}

.pill {
  display: flex;
  align-items: center;
  gap: var(--l3-spacing-04);
  height: var(--l3-size-24);
  padding-inline: var(--l3-spacing-02) var(--l3-spacing-04);
  border: 1px solid var(--l3-border-light);
  border-radius: var(--l3-radius-04);
  background: var(--l3-surface-primary);
  box-shadow: var(--l3-shadow-elevation-low);
  pointer-events: auto;
}

.row[data-kind='entry'] .pill {
  padding-left: var(--l3-spacing-04);
}

.pnl {
  font: var(--l3-text-label-12);
  white-space: nowrap;
}

.pnl[data-tone='up'] {
  color: var(--l3-content-accent-indicator-up-default);
}

.pnl[data-tone='down'] {
  color: var(--l3-content-accent-indicator-down-default);
}

.pnl[data-tone='flat'] {
  color: var(--l3-content-secondary);
}

/* The drag handle and ✕: bare 16 icons; the handle is the pill's grip (vertical drag, no page scroll). */
.handle,
.close {
  display: grid;
  place-items: center;
  padding: 0;
  border: 0;
  background: none;
  color: var(--l3-content-primary);
  cursor: pointer;
}

.handle {
  touch-action: none;
  cursor: ns-resize;
}

.handle:focus-visible,
.close:focus-visible,
.breakeven:focus-visible {
  outline: 2px solid var(--l3-border-accent-discover-default);
  outline-offset: 1px;
}

/* Exit / Add Trail / Add TP: L3 Secondary Small, 24 tall here to sit on the 24 pills (Figma). */
.exit.exit {
  --btn-height: var(--l3-size-24);
  --btn-padding-block: 0;
  --btn-padding-inline: var(--l3-spacing-08);
  --btn-radius: var(--l3-radius-04);
  --btn-font: var(--l3-text-label-12);
  --btn-icon-size: var(--l3-icon-size-14);
  pointer-events: auto;
}

/* "B/E 105.55 ⓘ" — Figma 11756:79332: warning-light box, edged top / bottom / left only, flush to the price axis,
   left corners rounded 4, padding 2 4 2 6, Label/10 in warning, a 12 ⓘ, gap 2. */
.breakeven {
  position: absolute;
  display: flex;
  align-items: center;
  gap: var(--l3-spacing-02);
  /* Figma 2 / 4 / 2 / 6 with the 1px border drawn inside (16 tall in all): each side's padding less the border. */
  padding: calc(var(--l3-spacing-02) - 1px) calc(var(--l3-spacing-04) - 1px) calc(var(--l3-spacing-02) - 1px) calc(var(--l3-spacing-06) - 1px);
  border: 1px solid var(--l3-border-accent-warning-light);
  border-radius: var(--l3-radius-04);
  background: var(--l3-surface-accent-warning-light);
  color: var(--l3-content-accent-warning-default);
  font: var(--l3-text-label-10);
  white-space: nowrap;
  translate: 0 -50%;
  cursor: pointer;
  pointer-events: auto;
}

/* The tag's info icon: 12, Figma's own glyph, in the tag's text colour. */
.breakevenInfo {
  display: block;
  flex: none;
  width: var(--l3-size-12);
  height: var(--l3-size-12);
}
```

### `src/flows/fno/components/PositionOverlay.tsx`

```tsx
import { useRef, type KeyboardEvent, type PointerEvent } from 'react'
import { Button } from '@l3/components/Button'
import { Icon } from '@l3/components/Icon'
import { MaskIcon } from '@l3/components/MaskIcon'
import { Tag } from '@l3/components/Tag'
import { msAdd, msCheck, msClose, msDragIndicator } from '@l3/icons/material'
import infoOutline from '../assets/breakeven-info.svg'
import { t } from '../copy'
import { OPTION_TICK, SCALPER_TP_SL_GAP, type ScalperPosition } from '../data'
import type { PaneScale } from './TradingPane'
import styles from './PositionOverlay.module.css'

type PositionOverlayProps = {
  scale: PaneScale
  position: ScalperPosition
  /** The option's last traded price: the entry row's live P&L, and the side TP / SL must stay on. */
  last: number
  /** The breakeven price, or null when the Breakeven line is off (Settings → View on chart). */
  breakeven: number | null
  onChange: (position: ScalperPosition) => void
  /** Exit (or the entry pill's ✕): sell the whole position at market. */
  onExit: () => void
  /** The ⓘ on the breakeven chip: How breakeven works. */
  onBreakevenInfo: () => void
}

/** The pills can't come closer than this to the entry row (px), so they never overlap it. */
const MIN_GAP = 30
/** …nor closer than this to the plot's top or bottom edge (px). */
const EDGE = 12

/**
 * A position on the option chart (Scalper "C · Boxed chip"): dashed lines across the plot at the take-profit, the
 * entry and the stop-loss, each with its pill at the left —
 * - TP: drag handle · green "TP Qty:65" · the P&L if it fills · ✕ (removes the TP);
 * - entry: Exit · blue "+65" (the quantity) · the live P&L · ✕ (exits too); "Add TP" / "Add SL" when one is removed;
 * - SL: drag handle · red "SL Qty:65" · the P&L if it fills · ✕ · Add Trail (the stop-loss follows the price up).
 * Drag a handle (or focus it and use ↑ / ↓) to move TP or SL: they stay on their side of the price and clear of the
 * entry row, in ₹0.05 steps. The breakeven line (solid, warning-light, Figma 11756:79330) runs to the price axis with a
 * boxed "Breakeven ⓘ" tag on it, 8 left of the axis (Figma 11756:79332); tapping it opens How breakeven works.
 */
export function PositionOverlay({ scale, position, last, breakeven, onChange, onExit, onBreakevenInfo }: PositionOverlayProps) {
  const { y, price, plotW, plotH, axis } = scale
  const { entry, quantity, takeProfit, stopLoss, trailing } = position
  const root = useRef<HTMLDivElement>(null)

  /** Keep a dragged price on its side of the market, clear of the entry row and inside the plot, on the tick. */
  const clampTp = (p: number) => tick(Math.min(Math.max(p, last + OPTION_TICK, price(y(entry) - MIN_GAP)), price(EDGE)))
  const clampSl = (p: number) => tick(Math.max(Math.min(p, last - OPTION_TICK, price(y(entry) + MIN_GAP)), price(plotH - EDGE)))
  const move = (kind: 'tp' | 'sl', p: number) =>
    onChange(kind === 'tp' ? { ...position, takeProfit: clampTp(p) } : { ...position, stopLoss: clampSl(p) })

  const drag = (kind: 'tp' | 'sl') => ({
    onPointerDown: (e: PointerEvent<HTMLButtonElement>) => {
      e.currentTarget.setPointerCapture(e.pointerId)
      e.preventDefault()
    },
    onPointerMove: (e: PointerEvent<HTMLButtonElement>) => {
      if (!e.currentTarget.hasPointerCapture(e.pointerId) || !root.current) return
      move(kind, price(e.clientY - root.current.getBoundingClientRect().top))
    },
    onKeyDown: (e: KeyboardEvent<HTMLButtonElement>) => {
      const step = e.key === 'ArrowUp' ? OPTION_TICK : e.key === 'ArrowDown' ? -OPTION_TICK : 0
      if (!step) return
      e.preventDefault()
      move(kind, (kind === 'tp' ? takeProfit : stopLoss)! + step * (e.shiftKey ? 20 : 1))
    },
  })

  const pnl = (exit: number) => (exit - entry) * quantity
  const live = pnl(last)

  return (
    <div ref={root} className={styles.overlay} style={{ width: plotW + axis, height: plotH }}>
      {/* Lines first, so every pill sits above every line. */}
      {takeProfit !== null && <span className={styles.line} data-kind="tp" style={{ top: y(takeProfit), width: plotW }} aria-hidden="true" />}
      <span className={styles.line} data-kind="entry" style={{ top: y(entry), width: plotW }} aria-hidden="true" />
      {stopLoss !== null && <span className={styles.line} data-kind="sl" style={{ top: y(stopLoss), width: plotW }} aria-hidden="true" />}
      {breakeven !== null && <span className={styles.line} data-kind="be" style={{ top: y(breakeven), width: plotW }} aria-hidden="true" />}

      {/* The entry price on the axis (the last price keeps its own green / red tag). */}
      <span className={styles.axisTag} style={{ top: y(entry), left: plotW + 1, width: axis }} aria-hidden="true">{entry.toFixed(2)}</span>

      {takeProfit !== null && (
        <div className={styles.row} style={{ top: y(takeProfit) }}>
          <div className={styles.pill}>
            <button type="button" className={styles.handle} aria-label={t('position.moveTp', { price: takeProfit.toFixed(2) })} {...drag('tp')}>
              <Icon icon={msDragIndicator} size={16} />
            </button>
            <Tag variant="primary" color="profit" size="sm">{t('position.tp', { quantity })}</Tag>
            <span className={styles.pnl} data-tone={tone(pnl(takeProfit))}>{rupees(pnl(takeProfit))}</span>
            <button type="button" className={styles.close} aria-label={t('position.removeTp')} onClick={() => onChange({ ...position, takeProfit: null })}>
              <Icon icon={msClose} size={16} />
            </button>
          </div>
        </div>
      )}

      <div className={styles.row} data-kind="entry" style={{ top: y(entry) }}>
        <Button variant="secondary" size="sm" onClick={onExit} className={styles.exit}>{t('position.exit')}</Button>
        <div className={styles.pill}>
          <Tag variant="primary" color="discover" size="sm">{`+${quantity}`}</Tag>
          <span className={styles.pnl} data-tone={tone(live)} aria-label={t('position.livePnl', { amount: rupees(live) })}>{rupees(live)}</span>
          <button type="button" className={styles.close} aria-label={t('position.close')} onClick={onExit}>
            <Icon icon={msClose} size={16} />
          </button>
        </div>
        {takeProfit === null && (
          <Button variant="secondary" size="sm" iconLeft={<Icon icon={msAdd} />} className={styles.exit} onClick={() => onChange({ ...position, takeProfit: clampTp(Math.max(last, entry) + SCALPER_TP_SL_GAP) })}>
            {t('position.addTp')}
          </Button>
        )}
        {stopLoss === null && (
          <Button variant="secondary" size="sm" iconLeft={<Icon icon={msAdd} />} className={styles.exit} onClick={() => onChange({ ...position, stopLoss: clampSl(Math.min(last, entry) - SCALPER_TP_SL_GAP), trailing: false })}>
            {t('position.addSl')}
          </Button>
        )}
      </div>

      {stopLoss !== null && (
        <div className={styles.row} style={{ top: y(stopLoss) }}>
          <div className={styles.pill}>
            <button type="button" className={styles.handle} aria-label={t('position.moveSl', { price: stopLoss.toFixed(2) })} {...drag('sl')}>
              <Icon icon={msDragIndicator} size={16} />
            </button>
            <Tag variant="primary" color="loss" size="sm">{t('position.sl', { quantity })}</Tag>
            <span className={styles.pnl} data-tone={tone(pnl(stopLoss))}>{rupees(pnl(stopLoss))}</span>
            <button type="button" className={styles.close} aria-label={t('position.removeSl')} onClick={() => onChange({ ...position, stopLoss: null, trailing: false })}>
              <Icon icon={msClose} size={16} />
            </button>
          </div>
          <Button
            variant="secondary"
            size="sm"
            iconLeft={trailing ? <Icon icon={msCheck} /> : undefined}
            aria-pressed={trailing}
            onClick={() => onChange({ ...position, trailing: !trailing })}
            className={styles.exit}
          >
            {trailing ? t('position.trailing') : t('position.addTrail')}
          </Button>
        </div>
      )}

      {breakeven !== null && (
        <button type="button" className={styles.breakeven} style={{ top: y(breakeven), right: `calc(${axis}px + var(--l3-spacing-08))` }} onClick={onBreakevenInfo} aria-label={t('breakeven.chipLabel', { price: breakeven.toFixed(2) })}>
          {t('breakeven.chip')}
          {/* Figma's info_outline (12), tinted with the tag's text colour so it follows light / dark. */}
          <span className={styles.breakevenInfo}><MaskIcon src={infoOutline} /></span>
        </button>
      )}
    </div>
  )
}

/** Round to the option tick (₹0.05), clear of float noise. */
const tick = (p: number) => Math.round(Math.round(p / OPTION_TICK) * OPTION_TICK * 100) / 100

const tone = (v: number) => (v > 0 ? 'up' : v < 0 ? 'down' : 'flat')

/** "+₹766", "-₹468", "₹0" — whole rupees, Indian grouping, as on the live app's position pills. */
export const rupees = (v: number) => {
  const r = Math.round(v)
  return `${r > 0 ? '+' : r < 0 ? '-' : ''}₹${Math.abs(r).toLocaleString('en-IN')}`
}
```

### `src/flows/fno/components/TradingChart.tsx`

```tsx
import { useState } from 'react'
import { Button } from '@l3/components/Button'
import { Chart } from '@l3/components/Chart'
import { Select } from '@l3/components/Select'
import { Stack } from '@l3/components/Stack'
import { Tabs } from '@l3/components/Tabs'
import { MaskIcon } from '@l3/components/MaskIcon'
import { chartSeries } from '../data'
import { t } from '../copy'
import chain from '../assets/option-chain.svg'
import scalper from '../assets/scalppro.svg'
import { TrendBadge } from './TrendBadge'
import styles from './HomeParts.module.css'

/** `instrument` + `onInstrument`: the Commodities tab shows its own instrument and opens the contract picker instead of the index sheet. */
export function TradingChart({ instrument, onInstrument, onChoose, onDestination, onChain, onScalper }: { instrument?: string; onInstrument?: () => void; onChain: () => void; onChoose: (title: string, values: string[], value: string, onPick: (v: string) => void) => void; onDestination: (name: string) => void; onScalper: () => void }) {
  const [chosenIndex, setIndex] = useState('NIFTY 50')
  const index = instrument ?? chosenIndex
  const [metric, setMetric] = useState('price')
  const items = (['price', 'oi', 'change', 'pcr', 'advance'] as const).map((value) => ({ value, label: t(`chart.${value}`) }))
  return <section className={styles.chartSection} aria-label={t('chart.label', { index, metric })}>
    <Stack direction="horizontal" justify="between" align="center">
      <Stack direction="horizontal" gap="08" align="center"><Select size="lg" aria-label={t('chart.index')} onClick={onInstrument ?? (() => onChoose(t('chart.index'), ['NIFTY 50', 'BANK NIFTY', 'SENSEX'], index, setIndex))}>{index}</Select><span className={styles.down}>5.17%</span></Stack>
      <TrendBadge trend="down" label={t('chart.trend')} since={t('chart.since')} />
    </Stack>
    <Tabs aria-label="Chart metric" appearance="pill" size="sm" items={items} value={metric} onChange={setMetric} />
    <Chart data={chartSeries(metric, index)} label={t('chart.label', { index, metric: items.find((i) => i.value === metric)!.label })} type={metric === 'price' ? 'candle' : 'line'} showLastPrice={false} showVolume={metric === 'price'} className={styles.chart} />
    <Stack direction="horizontal" gap="12"><Button variant="secondary" size="md" fullWidth iconLeft={<span className={styles.actionIcon}><img className={styles.asset} src={chain} alt="" /></span>} onClick={onChain}>{t('chart.chain')}</Button><Button variant="primary" size="md" fullWidth iconLeft={<span className={styles.actionIcon}><MaskIcon src={scalper} /></span>} onClick={onScalper}>{t('chart.scalper')}</Button></Stack>
  </section>
}
```

### `src/flows/fno/components/TradingPane.module.css`

```css
/* Trading chart pane (Scalper). SVG geometry is in CSS px (TradingPane.tsx); colours and type are L3 tokens. */
.pane {
  position: relative;
  min-height: 0;
  flex: 1;
}

.svg {
  position: absolute;
  inset: 0;
  overflow: visible;
}

.axisLine {
  stroke: var(--l3-border-intense);
  stroke-width: 1;
}

.tick,
.time {
  fill: var(--l3-content-secondary);
  font: var(--l3-text-label-12);
}

/* Candles: up green, down red (L3 indicator colours); 1px wicks. */
.up {
  fill: var(--l3-content-accent-indicator-up-default);
  stroke: var(--l3-content-accent-indicator-up-default);
}

.down {
  fill: var(--l3-content-accent-indicator-down-default);
  stroke: var(--l3-content-accent-indicator-down-default);
}

.up line,
.down line {
  stroke-width: 1;
}

.up rect,
.down rect {
  stroke: none;
}

/* Last price: a dashed line in the up colour to the axis, and the green tag with white text. */
.lastLine {
  stroke: var(--l3-content-accent-indicator-up-default);
  stroke-width: 1.5;
  stroke-dasharray: 4 3;
}

.lastTag {
  fill: var(--l3-surface-accent-indicator-up-default);
}

[data-tone='down'] > .lastLine {
  stroke: var(--l3-content-accent-indicator-down-default);
}

[data-tone='down'] > .lastTag {
  fill: var(--l3-surface-accent-indicator-down-default);
}

.lastText {
  fill: var(--l3-static-white);
  font: var(--l3-text-label-12);
}

/* Session high / low: the value in primary text, a dot and a line in secondary. */
.marker line {
  stroke: var(--l3-content-secondary);
  stroke-width: 1;
}

.marker circle {
  fill: var(--l3-content-secondary);
}

.marker text {
  fill: var(--l3-content-primary);
  font: var(--l3-text-label-12);
}

/* An applied indicator's two lines. */
.fast,
.slow {
  fill: none;
  stroke-width: 1.5;
  stroke-linejoin: round;
}

.fast {
  stroke: var(--l3-content-accent-us-stock-default);
}

.slow {
  stroke: var(--l3-content-accent-zing-default);
}

/* Zoom in at the top of the plot, zoom out at the bottom, against the price axis. */
.zoom {
  position: absolute;
  top: 0;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding-block: var(--l3-spacing-04) var(--l3-spacing-08);
  box-sizing: border-box;
  pointer-events: none;
}

.zoomButton.zoomButton {
  --btn-content: var(--l3-content-secondary);
  pointer-events: auto;
}

/* "5m ▾" in the corner under the price axis. */
.timeframe.timeframe {
  position: absolute;
  right: 0;
  bottom: 0;
  justify-content: center;
  font: var(--l3-text-label-14);
}
```

### `src/flows/fno/components/TradingPane.tsx`

```tsx
import { useLayoutEffect, useRef, useState, type ReactNode } from 'react'
import { Button } from '@l3/components/Button'
import type { ChartCandle } from '@l3/components/Chart'
import { Icon } from '@l3/components/Icon'
import { msArrowDropDown, msZoomIn, msZoomOut } from '@l3/icons/material'
import { t } from '../copy'
import styles from './TradingPane.module.css'

/** A line drawn over the candles (an applied indicator), one value per candle. */
export type PaneLine = { values: number[]; tone: 'fast' | 'slow' }

export type TradingPaneProps = {
  candles: ChartCandle[]
  /** The first candle's time ("11:30") and the candle length in minutes: the time axis is worked out from them. */
  start: string
  minutes: number
  /** Accessible name, e.g. "NIFTY 50, today, 5-minute candles". */
  label: string
  lines?: PaneLine[]
  /** Prices the scale must show besides the candles (an open position's TP / SL), so their lines stay on the chart. */
  include?: number[]
  /** Things laid over the plot at prices (a position's lines and pills, the breakeven line), placed with `scale`. */
  overlay?: (scale: PaneScale) => ReactNode
  /** Empty candle slots after the last candle (room for the price to run into). Default 3. */
  room?: number
}

/** The pane's price ↔ pixel scale, for an overlay: `y(price)` from the pane's top, `price(y)` back. */
export type PaneScale = { y: (price: number) => number; price: (y: number) => number; plotW: number; plotH: number; axis: number }

// Geometry in CSS px, measured on the live app's screenshot (392 wide).
const AXIS = 50 // the price axis on the right, past its separator line
const TIME = 30 // the time axis under the plot
const PAD_TOP = 26 // the session high sits this far under the top
const PAD_BOTTOM = 34 // …and the low this far above the time axis
const EMPTY_SLOTS = 3 // room after the last candle
const MAX_BODY = 4 // candles never get wider than this, however few there are (Figma: thin candles)
const TIME_EVERY = 10 // a time label every 10 candles (50 minutes)
const MARKER = 18 // the high / low marker's line length

/**
 * A trading chart pane (Scalper): candles, a price axis on the right with the last price tagged, the session's high
 * and low marked with their values, zoom in / out, a time axis under it and the candle length (5m) in the corner.
 * Drawn at the pane's real size (it fills its parent), so the text never stretches. Colours are L3 tokens.
 * L3's Chart is a fixed 360 × 200 picture without high / low markers, zoom or a timeframe — listed as an L3 gap.
 */
export function TradingPane({ candles, start, minutes, label, lines = [], include = [], overlay, room = EMPTY_SLOTS }: TradingPaneProps) {
  const box = useRef<HTMLDivElement>(null)
  const [size, setSize] = useState({ w: 0, h: 0 })
  useLayoutEffect(() => {
    const el = box.current
    if (!el) return
    const measure = () => setSize({ w: el.clientWidth, h: el.clientHeight })
    measure()
    const ro = new ResizeObserver(measure)
    ro.observe(el)
    return () => ro.disconnect()
  }, [])

  const plotW = Math.max(0, size.w - AXIS)
  const plotH = Math.max(0, size.h - TIME)
  const highs = candles.map((c) => c.high)
  const lows = candles.map((c) => c.low)
  const candleHi = Math.max(...highs)
  const candleLo = Math.min(...lows)
  const hi = Math.max(candleHi, ...include)
  const lo = Math.min(candleLo, ...include)
  const slot = plotW / (candles.length + room)
  const bodyW = Math.min(slot * 0.6, MAX_BODY)
  const x = (i: number) => slot * (i + 0.5)
  const y = (v: number) => PAD_TOP + ((hi - v) / (hi - lo || 1)) * (plotH - PAD_TOP - PAD_BOTTOM)
  const span = plotH - PAD_TOP - PAD_BOTTOM
  const price = (py: number) => hi - ((py - PAD_TOP) / (span || 1)) * (hi - lo)
  const last = candles[candles.length - 1]
  const ticks = niceTicks(lo, hi).filter((v) => y(v) > 8 && y(v) < plotH - 8 && Math.abs(y(v) - y(last.close)) > 14)
  const hiIndex = highs.indexOf(candleHi)
  const loIndex = lows.indexOf(candleLo)
  const fmt = (v: number) => v.toFixed(2)
  const times = candles.map((_, i) => i).filter((i) => (i + 1) % TIME_EVERY === 0 || i === candles.length - 1)

  return (
    <div className={styles.pane} ref={box}>
      {size.w > 0 && (
        <svg className={styles.svg} width={size.w} height={size.h} role="img" aria-label={label}>
          {/* separators: the price axis and the time axis */}
          <line className={styles.axisLine} x1={plotW + 0.5} y1={0} x2={plotW + 0.5} y2={plotH} />
          <line className={styles.axisLine} x1={0} y1={plotH + 0.5} x2={size.w} y2={plotH + 0.5} />

          {ticks.map((v) => (
            <text key={v} className={styles.tick} x={plotW + 4} y={y(v)} dominantBaseline="central">{Math.round(v * 100) / 100}</text>
          ))}

          {candles.map((c, i) => {
            const up = c.close >= c.open
            const top = y(Math.max(c.open, c.close))
            const body = Math.max(1, y(Math.min(c.open, c.close)) - top)
            return (
              <g key={i} className={up ? styles.up : styles.down}>
                <line x1={x(i)} x2={x(i)} y1={y(c.high)} y2={y(c.low)} />
                <rect x={x(i) - bodyW / 2} y={top} width={bodyW} height={body} rx={0.5} />
              </g>
            )
          })}

          {lines.map((l) => (
            <path key={l.tone} className={styles[l.tone]} d={l.values.map((v, i) => `${i ? 'L' : 'M'}${x(i).toFixed(1)},${y(v).toFixed(1)}`).join('')} />
          ))}

          {/* last price: a dashed line to the axis, then the tag — green while the candle is up, red while it's down */}
          <g data-tone={last.close >= last.open ? 'up' : 'down'}>
            <line className={styles.lastLine} x1={x(candles.length - 1) + slot * 0.5} y1={y(last.close)} x2={plotW} y2={y(last.close)} />
            <rect className={styles.lastTag} x={plotW + 1} y={y(last.close) - 8} width={AXIS} height={16} rx={2} />
            <text className={styles.lastText} x={plotW + 3} y={y(last.close)} dominantBaseline="central">{fmt(last.close)}</text>
          </g>

          <Marker x={x(hiIndex)} y={y(candleHi)} value={fmt(candleHi)} towardRight={hiIndex < candles.length / 2} />
          <Marker x={x(loIndex)} y={y(candleLo)} value={fmt(candleLo)} towardRight={loIndex < candles.length / 2} />

          {times.map((i) => (
            <g key={i}>
              <line className={styles.axisLine} x1={x(i)} x2={x(i)} y1={plotH} y2={plotH + 5} />
              <text className={styles.time} x={x(i)} y={plotH + 18} textAnchor="middle" dominantBaseline="central">{clock(start, minutes * i)}</text>
            </g>
          ))}
        </svg>
      )}
      {size.w > 0 && overlay?.({ y, price, plotW, plotH, axis: AXIS })}
      <div className={styles.zoom} style={{ right: AXIS + 2, height: plotH }}>
        <Button variant="ghost" size="sm" iconLeft={<Icon icon={msZoomIn} />} aria-label={t('scalper.zoomIn')} className={styles.zoomButton} />
        <Button variant="ghost" size="sm" iconLeft={<Icon icon={msZoomOut} />} aria-label={t('scalper.zoomOut')} className={styles.zoomButton} />
      </div>
      <Button
        variant="ghost"
        size="sm"
        iconRight={<Icon icon={msArrowDropDown} />}
        aria-label={t('scalper.timeframeLabel')}
        className={styles.timeframe}
        style={{ width: AXIS, height: TIME }}
      >
        {t('scalper.timeframe')}
      </Button>
    </div>
  )
}

/** The session's high / low: its value, a dot and a short line to the candle (to the right when the candle is on the left). */
function Marker({ x, y, value, towardRight }: { x: number; y: number; value: string; towardRight: boolean }) {
  const end = towardRight ? x + MARKER : x - MARKER
  return (
    <g className={styles.marker}>
      <line x1={x} y1={y} x2={end} y2={y} />
      <circle cx={end} cy={y} r={1.5} />
      <text x={towardRight ? end + 5 : end - 5} y={y} textAnchor={towardRight ? 'start' : 'end'} dominantBaseline="central">{value}</text>
    </g>
  )
}

/** Round price-axis steps (1, 2, 5 × 10ⁿ) for about six labels. */
function niceTicks(lo: number, hi: number) {
  const raw = (hi - lo) / 6
  const pow = 10 ** Math.floor(Math.log10(raw))
  const step = [1, 2, 4, 5, 10].map((m) => m * pow).find((s) => s >= raw) ?? raw
  const first = Math.ceil(lo / step) * step
  return Array.from({ length: Math.floor((hi - first) / step) + 1 }, (_, k) => first + k * step)
}

/** "11:30" + 45 minutes → "12:15". */
function clock(start: string, add: number) {
  const [h, m] = start.split(':').map(Number)
  const total = h * 60 + m + add
  return `${Math.floor(total / 60)}:${String(total % 60).padStart(2, '0')}`
}
```

### `src/flows/fno/components/TrendBadge.tsx`

```tsx
import type { KeyboardEvent, MouseEvent } from 'react'
import { Icon } from '@l3/components/Icon'
import { MaskIcon } from '@l3/components/MaskIcon'
import { Stack } from '@l3/components/Stack'
import { msInfo } from '@l3/icons/material'
import downtrend from '../assets/downtrend.svg'
import styles from './HomeParts.module.css'

/**
 * The trend read-out: "Strong Uptrend / Downtrend" in up / down colour over "Since <time>" (caption 10 in the chart; `largeSince` = description 12, the Expiring cards), with the double
 * arrow on the right. One component for the chart's header and the Expiring This Week cards, so they stay identical.
 * The up arrow is the down artwork turned over. `info` (the Expiring cards) adds the info (i) icon after "Since", in
 * content-secondary like the line. With `onInfo` the whole read-out (label, since, i, arrow) is one tap target that
 * opens the trend info sheet — it sits inside a tappable card, so the tap stops there and doesn't open the card too.
 */
export function TrendBadge({ trend, label, since, largeSince = false, info, onInfo, iconStart = false }: {
  trend: 'up' | 'down'; label: string; since: string; largeSince?: boolean
  /** The arrow on the left and the text left-aligned (the trend info sheet's top row); default arrow right, text right-aligned. */
  iconStart?: boolean
  /** Label of the info icon after "Since"; none = no icon. */
  info?: string
  /** Opens the trend info sheet; makes the whole read-out tappable. */
  onInfo?: () => void
}) {
  const sinceClass = largeSince ? styles.description : styles.caption
  const arrow = <span className={styles.trendIcon} data-trend={trend}><MaskIcon src={downtrend} /></span>
  const content = <>
    {iconStart && arrow}
    <Stack gap="04" align={iconStart ? 'start' : 'end'}><span className={trend === 'up' ? styles.up : styles.down}>{label}</span>{info
      ? <Stack direction="horizontal" gap="04" align="center" className={sinceClass}><span>{since}</span><Icon icon={msInfo} size={12} /></Stack>
      : <span className={sinceClass}>{since}</span>}</Stack>
    {!iconStart && arrow}
  </>
  if (!onInfo) return <Stack direction="horizontal" gap={iconStart ? '08' : '04'} align="center">{content}</Stack>
  // A span with the button role: the card's body is already a <button>, and a button can't hold another one.
  const open = (event: MouseEvent | KeyboardEvent) => { event.stopPropagation(); event.preventDefault(); onInfo() }
  return <span
    role="button"
    tabIndex={0}
    aria-label={`${label}, ${since}. ${info ?? ''}`}
    className={styles.trendButton}
    onClick={open}
    onKeyDown={(event) => { if (event.key === 'Enter' || event.key === ' ') open(event) }}
  >{content}</span>
}
```

### `src/flows/fno/components/UsBanner.module.css`

```css
/* US MARKETS banner (teammate's design 9001:3). No L3 banner component: a card-like button from L3 tokens. */
.wrap { padding-inline: var(--l3-spacing-16); }
.banner { position: relative; display: flex; align-items: center; justify-content: space-between; gap: var(--l3-spacing-08); width: 100%; padding: var(--l3-spacing-12); border: 0; border-radius: var(--l3-radius-12); box-shadow: inset 0 0 0 1px var(--l3-border-accent-discover-light); background: var(--l3-base-hue-blue-900); color: inherit; text-align: left; cursor: pointer; overflow: hidden; -webkit-tap-highlight-color: transparent; }
.glow, .glow2 { position: absolute; pointer-events: none; }
.glow { top: calc(50% - 76px); left: -106px; width: 216px; }
.glow2 { top: calc(50% - 14px); left: -46px; width: 216px; transform: rotate(11.73deg); }
/* Flag picture: static still of the animated US flag, tilted, bleeding off the left edge. */
.flagWrap { position: absolute; top: -15px; left: -54px; display: flex; align-items: center; justify-content: center; width: 151px; height: 106px; pointer-events: none; }
.flag { width: 138px; height: 79px; object-fit: cover; transform: rotate(12deg); }
.copy { position: relative; display: flex; flex: 1; flex-direction: column; gap: var(--l3-spacing-02); min-width: 0; padding-left: 58px; white-space: nowrap; }
.kicker { display: flex; align-items: center; gap: var(--l3-spacing-04); font: var(--l3-text-heading-10); letter-spacing: var(--l3-letter-spacing-ai-caps); color: var(--l3-base-hue-blue-400); }
.live { display: inline-flex; align-items: center; gap: var(--l3-spacing-04); margin-left: var(--l3-spacing-04); color: var(--l3-content-accent-indicator-up-default); }
.dot { width: 6px; height: 6px; border-radius: var(--l3-radius-full); background: currentColor; animation: us-pulse 1.6s ease-in-out infinite; }
.headline { font: var(--l3-text-heading-14); color: var(--l3-base-neutral-charcoal-50); }
.sub { margin-top: var(--l3-spacing-02); font: var(--l3-text-description-10); color: var(--l3-base-neutral-charcoal-400); }
.arrow { position: relative; display: flex; flex: none; align-items: center; justify-content: center; width: var(--l3-size-32); height: var(--l3-size-32); border: 1px solid color-mix(in srgb, var(--l3-static-white) 12%, transparent); border-radius: var(--l3-radius-16); background: color-mix(in srgb, var(--l3-static-white) 10%, transparent); color: var(--l3-static-white); }
@keyframes us-pulse { 50% { opacity: 0.35; } }
@media (prefers-reduced-motion: reduce) { .dot { animation: none; } }
```

### `src/flows/fno/components/UsBanner.tsx`

```tsx
import { Icon } from '@l3/components/Icon'
import { msChevronRight } from '@l3/icons/material'
import { t } from '../copy'
import flag from '../assets/us-flag.png'
import glow from '../assets/us-glow.svg'
import glow2 from '../assets/us-glow-2.svg'
import styles from './UsBanner.module.css'

/** "US MARKETS · LIVE" flag banner under the F&O quick actions (Equity tab). The whole card is one tap target → US Stocks. */
export function UsBanner({ onOpen }: { onOpen: () => void }) {
  return <div className={styles.wrap}>
    <button type="button" className={styles.banner} onClick={onOpen}>
      <img src={glow} alt="" aria-hidden="true" className={styles.glow} />
      <img src={glow2} alt="" aria-hidden="true" className={styles.glow2} />
      <span className={styles.flagWrap}><img src={flag} alt="" className={styles.flag} /></span>
      <span className={styles.copy}>
        <span className={styles.kicker}>{t('us.eyebrow')}<span className={styles.live}><span className={styles.dot} aria-hidden="true" />{t('us.live')}</span></span>
        <span className={styles.headline}>{t('us.headline')}</span>
        <span className={styles.sub}>{t('us.sub')}</span>
      </span>
      <span className={styles.arrow} aria-hidden="true"><Icon icon={msChevronRight} size={24} /></span>
    </button>
  </div>
}
```

### `src/flows/fno/components/useLiveInstrument.ts`

```ts
import { useEffect, useState } from 'react'
import type { ChartCandle } from '@l3/components/Chart'
import type { ScalperInstrument } from '../data'

type LiveOptions = {
  /** The price step (₹0.05 for NIFTY and its options). */
  tick: number
  /** A new price every this many ms. */
  everyMs?: number
  /** A new candle starts after this many prices (prototype: ~15 s, so the chart visibly moves; the axis keeps 5m). */
  pricesPerCandle?: number
}

/**
 * Makes a Scalper chart feel live (prototype): every second the last candle's close takes a small step, stretching its
 * high / low; every `pricesPerCandle` steps a new candle opens at that close and the oldest drops off, so the window
 * keeps its length and its time axis moves on. The steps lean back toward the sample price, so the chart stays around
 * the design's numbers (and an open position's TP / SL stay on their sides). The header's price, change and % follow.
 * In the real app this is the market feed.
 */
export function useLiveInstrument(base: ScalperInstrument, { tick, everyMs = 1000, pricesPerCandle = 15 }: LiveOptions): ScalperInstrument {
  const [state, setState] = useState(() => ({ candles: base.candles, opened: 0, steps: 0 }))

  useEffect(() => {
    const typicalRange = base.candles.reduce((sum, c) => sum + c.high - c.low, 0) / base.candles.length
    const id = window.setInterval(() => {
      setState(({ candles, opened, steps }) => {
        const last = candles[candles.length - 1]
        const pull = (base.price - last.close) * 0.08
        const close = snap(last.close + pull + (Math.random() - 0.5) * typicalRange * 0.12, tick)
        const updated: ChartCandle = { ...last, close, high: Math.max(last.high, close), low: Math.min(last.low, close) }
        if ((steps + 1) % pricesPerCandle === 0) {
          const next: ChartCandle = { open: close, high: close, low: close, close }
          return { candles: [...candles.slice(1, -1), updated, next], opened: opened + 1, steps: steps + 1 }
        }
        return { candles: [...candles.slice(0, -1), updated], opened, steps: steps + 1 }
      })
    }, everyMs)
    return () => window.clearInterval(id)
  }, [base, tick, everyMs, pricesPerCandle])

  const price = state.candles[state.candles.length - 1].close
  const previousClose = base.price - base.change
  const change = Math.round((price - previousClose) * 100) / 100
  return {
    ...base,
    candles: state.candles,
    start: addMinutes(base.start, state.opened * base.minutes),
    price,
    change,
    percent: (change / previousClose) * 100,
  }
}

const snap = (p: number, tick: number) => Math.round(Math.round(p / tick) * tick * 100) / 100

function addMinutes(start: string, add: number) {
  const [h, m] = start.split(':').map(Number)
  const total = h * 60 + m + add
  return `${Math.floor(total / 60)}:${String(total % 60).padStart(2, '0')}`
}
```

### `src/flows/fno/copy.json`

```json
{
  "top.search": "Search stocks",
  "top.profile": "Profile and settings",
  "top.wallet": "Wallet",
  "top.dash": "DASH",
  "title": "F&O",
  "nav.home": "Home",
  "nav.chain": "Option Chain",
  "nav.positions": "Positions",
  "nav.scalper": "Scalper",
  "pnl.total": "Total P&L",
  "pnl.day": "Day P&L",
  "pnl.open": "View positions",
  "signals": "2 Signals",
  "equity": "Equity",
  "commodities": "Commodities",
  "strategies": "Strategies",
  "us.eyebrow": "US MARKETS •",
  "us.live": "LIVE",
  "us.headline": "Live now · till 2:30 AM IST",
  "us.sub": "Buy Apple, NVIDIA & more",
  "shortcut.label": "Shortcuts",
  "shortcut.calls": "Trade Calls",
  "shortcut.analysis": "Analysis",
  "shortcut.ipo": "IPO",
  "shortcut.watchlist": "Watchlist",
  "shortcut.invest": "Smart Invest",
  "shortcut.referral": "Referral",
  "chart.index": "Choose index",
  "chart.trend": "Strong Downtrend",
  "chart.since": "Since 12:46 PM",
  "chart.price": "Price",
  "chart.oi": "OI",
  "chart.change": "Change in OI",
  "chart.pcr": "PCR",
  "chart.advance": "Advanced declined",
  "chart.label": "{index} · {metric}",
  "chart.chain": "Option chain",
  "chart.scalper": "ScalpPro",
  "watchlists.title": "Watchlist ({count})",
  "watchlists.add": "Add watchlist",
  "watchlists.count": "{count} stocks",
  "watchlists.create": "Create watchlist",
  "watchlists.name": "Watchlist name",
  "watchlists.created": "Watchlist created",
  "options.title": "Smart Options",
  "options.top": "Top traded",
  "options.active": "Most active",
  "options.oi": "OI gainers",
  "options.advanced": "Advanced",
  "heatmap.title": "Futures Heatmap",
  "heatmap.auto": "Auto",
  "heatmap.financial": "Financial services",
  "heatmap.fmcg": "FMCG",
  "futures.title": "Smart Futures",
  "futures.long": "Long Build",
  "futures.covering": "Short Covering",
  "futures.short": "Short Buildup",
  "futures.unwind": "Long Windup",
  "scope.index": "Index",
  "scope.stock": "Stock",
  "scope.label": "Instrument type",
  "filter": "Filter",
  "filter.all": "All contracts",
  "filter.calls": "Calls",
  "filter.puts": "Puts",
  "filter.gainers": "Gainers",
  "filter.losers": "Losers",
  "sort.price": "By Price",
  "sort.volume": "By Volume",
  "sort.label": "Sort contracts",
  "viewAll": "View all",
  "close": "Okay",
  "cancel": "Cancel",
  "prototype.description": "This destination is not included in the current prototype. This screen uses sample market data.",
  "contract.price": "Price",
  "contract.volume": "Volume",
  "contract.change": "Change",
  "empty": "No contracts match",
  "empty.description": "Choose another filter to see contracts.",
  "scalper.back": "Back to F&O",
  "scalper.strategies": "Strategies",
  "scalper.all": "All",
  "scalper.addStrategies": "Add more strategies",
  "scalper.tools": "Scalper tools",
  "scalper.positions": "Positions",
  "scalper.orders": "Orders",
  "scalper.chain": "Option chain",
  "scalper.active": "Active",
  "scalper.activeCount": "{count} active",
  "scalper.pickInstrument": "Change instrument",
  "scalper.pickSegment": "Change segment",
  "scalper.link": "Link both charts",
  "scalper.chartType": "Chart type",
  "scalper.chartTools": "Chart tools",
  "scalper.zoomIn": "Zoom in",
  "scalper.zoomOut": "Zoom out",
  "scalper.timeframe": "5m",
  "scalper.timeframeLabel": "Candle length",
  "scalper.chartLabel": "{name}, today, 5-minute candles",
  "scalper.resize": "Resize the charts",
  "scalper.orderType": "Order type",
  "scalper.market": "Market",
  "scalper.limit": "Limit/Trigger",
  "scalper.buy": "Buy at Mkt",
  "scalper.sell": "Sell at Mkt",
  "scalper.quantity": "Quantity",
  "scalper.lots": "{count} lot",
  "scalper.required": "Req: {amount}",
  "scalper.funds": "Funds: {amount}",
  "tools.range": "Range",
  "tools.zing": "Zing",
  "tools.indicators": "Indicators",
  "tools.drawings": "Drawings",
  "tools.templates": "Templates",
  "tools.settings": "Settings",
  "tools.new": "NEW",
  "tools.search": "Search {section}",
  "tools.yours": "Your indicators",
  "tools.create": "Create",
  "tools.none": "No indicators created yet.",
  "tools.byDash": "Made with DASH Ai",
  "tools.longPressHint": "Long press for more options",
  "tools.showOnChart": "Show on chart",
  "tools.isOnChart": "It’s on this chart",
  "tools.notOnChart": "Not on this chart",
  "tools.openInDash": "Open in DASH",
  "tools.detailsDone": "Done",
  "tools.lemonn": "Lemonn indicators",
  "tools.favourite": "Add {name} to favourites",
  "tools.soon": "Pick Indicators to add one to the chart.",
  "tools.guideTip": "Indicators you created with DASH",
  "tools.indicatorsCount": "Indicators ({count})",
  "tools.clearAll": "Remove all indicators from the chart",
  "tools.onChart": "on the chart",
  "tools.onChartList": "{count} indicators on the chart",
  "tools.add": "Add {name} to the chart",
  "tools.remove": "Remove {name} from the chart",
  "tools.searchPlaceholder": "Search indicators",
  "tools.closeSearch": "Close search",
  "tools.noResults": "No indicators match “{query}”.",
  "scalper.indicatorCount": "{count} indicators on the chart",
  "scalper.refresh": "Reset the chart",
  "tools.createLabel": "Create an indicator with DASH",
  "commodities.popular": "Popular commodities",
  "commodities.options": "Options",
  "commodities.futures": "Futures",
  "commodities.segment": "Contract type",
  "commodities.top": "Top traded",
  "commodities.gainers": "Top gainers",
  "commodities.losers": "Top Losers",
  "commodities.advanced": "Advanced declined",
  "commodities.margin": "Margin / lot : {margin}",
  "commodities.shortcuts": "Commodities",
  "heatmap.bullion": "Bullion",
  "heatmap.energy": "Energy",
  "heatmap.metals": "Metals",
  "picker.title": "Choose options contract",
  "picker.equity": "Equity ({count})",
  "picker.commodities": "Commodities ({count})",
  "picker.all": "All",
  "picker.filter": "Commodity",
  "lot.title": "{name} Summary",
  "lot.back": "Back to F&O",
  "lot.lots": "Gold lots",
  "lot.futures": "Futures",
  "lot.options": "Options",
  "lot.chain": "View option chain",
  "lot.expiry": "Expiry month",
  "lot.active": "Most active",
  "lot.oi": "OI gainers",
  "lot.gainers": "Top gainers",
  "sort.margin": "Margin per lot",
  "sort.title": "Sort by",
  "strategies.segment": "Strategies for",
  "strategies.zing": "Zing Trades",
  "strategies.explore": "Explore",
  "strategies.builtWith": "Built with DASH Ai",
  "strategies.todayReturns": "Today’s Returns",
  "strategies.lastWeek": "Last week",
  "strategies.avgTrades": "Avg. trades",
  "strategies.perDay": "{count} per day",
  "strategies.winRate": "Win rate",
  "strategies.favourite": "Save {name}",
  "strategies.learn": "Learn in 30 Secs",
  "strategies.apply": "Apply",
  "strategies.dayWin": "{day}: profit",
  "strategies.dayLoss": "{day}: loss",
  "strategies.dayFlat": "{day}: no trade",
  "strategies.smartInvest": "Smart Invest",
  "strategies.by": "By {name}",
  "strategies.minDeposit": "Min. deposit",
  "strategies.pnl7": "7 Days P&L",
  "strategies.pnl30": "30 Days P&L",
  "strategies.showPnl": "Show or hide P&L",
  "strategies.aum": "AUM",
  "strategies.slots": "Slots left",
  "strategies.charges": "Monthly charges",
  "strategies.invest": "Invest now",
  "strategies.prebuilt": "Pre-build Strategies",
  "strategies.underlying": "Underlying",
  "strategies.bullish": "Bullish",
  "strategies.bearish": "Bearish",
  "strategies.neutral": "Neutral",
  "strategies.volatile": "Volatile",
  "strategies.pop": "Probability of profit",
  "strategies.funds": "Funds Req: {amount}",
  "strategies.maxProfit": "Max Profit:",
  "strategies.maxLoss": "Max Loss:",
  "strategies.unlimited": "Unlimited",
  "strategies.payoff": "Payoff: loss below the breakeven, profit above it",
  "strategies.quick": "Quick Trade",
  "strategies.beginner": "Beginner friendly",
  "strategies.which": "Which way will",
  "strategies.move": "move?",
  "strategies.up": "Up • Bullish",
  "strategies.down": "Down • Bearish",
  "strategies.pickUnderlying": "Choose underlying",
  "chain.title": "Option chain",
  "chain.back": "Back to F&O",
  "chain.tabs": "Option chain and strategies",
  "chain.addStrategies": "Add more strategies",
  "chain.underlying": "Choose underlying",
  "chain.expiry": "Expiry:",
  "chain.expiryTitle": "Choose expiry",
  "chain.signals": "Zing signals: {count}",
  "chain.greeks": "Greeks",
  "chain.basket": "Basket orders",
  "chain.pcr": "PCR:",
  "chain.maxPain": "Max Pain:",
  "chain.atmIv": "ATM IV:",
  "chain.call": "Call",
  "chain.put": "Put",
  "chain.metric.ltp": "LTP",
  "chain.metric.oi": "OI",
  "chain.metric.oiChange": "OI Chg",
  "chain.metric.iv": "IV",
  "chain.metricTitle": "Show in the price columns",
  "chain.range.0": "All",
  "chain.range.5": "±5",
  "chain.range.10": "±10",
  "chain.rangeTitle": "Strikes to show",
  "chain.rangeOption.0": "All strikes",
  "chain.rangeOption.5": "5 strikes around the spot",
  "chain.rangeOption.10": "10 strikes around the spot",
  "chain.tag.support": "OI Support",
  "chain.tag.resistance": "OI Resistance",
  "chain.tag.maxPain": "Max Pain",
  "chain.spot": "Spot price",
  "chain.select": "{action} {strike} {side} at {price}",
  "chain.buyBadge": "B",
  "chain.sellBadge": "S",
  "chain.contract": "{strike} {side}",
  "chain.orderOptions": "Set Limit",
  "chain.tpsl": "TP/SL",
  "chain.balance": "Balance :",
  "chain.req": "Req :",
  "chain.quantity": "Quantity",
  "chain.lots": "{count} lots",
  "chain.lot": "1 lot",
  "chain.buy": "Buy",
  "chain.sell": "Sell",
  "chain.placed": "{action} order placed · {contract}",
  "chain.oiLegend": "Call OI {call} · Put OI {put}",
  "chain.illiquid": "ILLIQUID contract",
  "chain.illiquidIcon": "ILLIQUID",
  "chain.illiquidMore": "Why can’t I trade this?",
  "chain.illiquidLabel": "{strike} {side}, illiquid: can’t be traded",
  "asset.back": "Back",
  "asset.watchlist": "Add to watchlist",
  "asset.illiquid": "ILLIQUID",
  "asset.chart": "{name} {contract}, today, 5-minute candles",
  "asset.tools": "Chart tools",
  "asset.range": "Range",
  "asset.interval": "Interval",
  "asset.intervalValue": "5m",
  "asset.indicators": "Indicators",
  "asset.drawings": "Drawings",
  "asset.settings": "Settings",
  "asset.chain": "Option chain",
  "asset.info": "Contract Info",
  "asset.daysToExpiry": "Days to Expiry",
  "asset.days": "{count} Days",
  "asset.margin": "Margin (Buy/Sell)",
  "asset.leverage": "Leverage (Buy/Sell)",
  "asset.priceUnit": "Price unit",
  "asset.futures": "{name} Futures",
  "asset.performance": "Performance",
  "asset.low": "24H Low",
  "asset.high": "24H High",
  "asset.ltp": "Last Traded Price :",
  "asset.prevClose": "Prev. Close",
  "asset.open": "Open",
  "asset.upperCircuit": "Upper Circuit",
  "asset.lowerCircuit": "Lower Circuit",
  "asset.tickSize": "Tick Size",
  "asset.unit": "Price Unit",
  "asset.trading": "Trading details",
  "asset.lotSize": "Lot Size",
  "asset.minLot": "Minimum Lot",
  "asset.lastQty": "Last Traded Qty",
  "asset.lastTime": "Last Traded Time",
  "asset.expiry": "Original Expiry date",
  "asset.lastTradingDate": "Last Trading Date",
  "asset.depth": "Market Depth",
  "asset.bid": "Bid Price",
  "asset.ask": "Ask Price",
  "asset.qty": "Quantity",
  "asset.total": "Total",
  "asset.buy": "Buy",
  "asset.sell": "Sell",
  "asset.illiquidNote": "Trading is not allowed as this contract is ILLIQUID",
  "contractSheet.label": "{name}: buy or sell",
  "contractSheet.open": "Open {name}",
  "contractSheet.expiry": "{date}",
  "illiquid.title": "What does illiquidity mean?",
  "illiquid.forContract": "{contract} is ILLIQUID right now",
  "illiquid.general": "Some contracts barely trade",
  "illiquid.point1": "Very few people are buying or selling it",
  "illiquid.point2": "Buy and sell prices are far apart, which increases chances of slippage",
  "illiquid.point3": "To protect you, Lemonn doesn’t allow orders in it",
  "illiquid.ok": "Got it",
  "illiquid.open": "What does illiquidity mean?",
  "chain.illiquidSub": "Can’t be traded",
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
  "position.tp": "TP Qty:{quantity}",
  "position.sl": "SL Qty:{quantity}",
  "position.moveTp": "Take-profit at ₹{price}. Drag or use the arrow keys to move it",
  "position.moveSl": "Stop-loss at ₹{price}. Drag or use the arrow keys to move it",
  "position.removeTp": "Remove take-profit",
  "position.removeSl": "Remove stop-loss",
  "position.exit": "Exit",
  "position.close": "Exit position",
  "position.livePnl": "P&L {amount}",
  "position.addTp": "TP",
  "position.addSl": "SL",
  "position.addTrail": "Add Trail",
  "position.trailing": "Trailing",
  "breakeven.chip": "Breakeven",
  "breakeven.chipLabel": "Breakeven ₹{price}. How breakeven works",
  "breakeven.title": "How breakeven works",
  "breakeven.titleV2": "What is breakeven line?",
  "breakeven.descriptionV2": "The price your trade must sell above to cover what you paid plus all order charges. Sell above it and you make a profit.",
  "breakeven.understand": "I understand",
  "breakeven.playing": "Example playing",
  "breakeven.exampleLabel": "Example",
  "breakeven.example": "Example:",
  "breakeven.exampleTrade": "Bought 1 lot at {price}",
  "breakeven.introducing": "Introducing",
  "breakeven.lineName": "Breakeven Line",
  "breakeven.tagline": "Sell above this line and your Net P&L stays positive",
  "breakeven.replay": "Tap to play it again.",
  "breakeven.chartLabelV2": "Example chart: bought at ₹100, the order charges stack up on it (STT ₹0.15, transaction ₹0.07, stamp duty and SEBI under a paisa, brokerage ₹0.02) into the breakeven line at ₹100.25 — a sliver of the ₹100; sold 12% higher at ₹112 for a net profit",
  "breakeven.chartLabel": "Example chart: bought at ₹100, the order charges stack up (STT ₹0.15, transaction ₹0.07, stamp duty and SEBI under a paisa, brokerage ₹0.02, plus GST) into the breakeven line at ₹100.30; sold at ₹102 above it for a net profit",
  "breakeven.bought": "Bought at {price}",
  "breakeven.sold": "Sold at {price}",
  "breakeven.ltp": "LTP",
  "breakeven.netProfit": "Net Profit",
  "breakeven.charges": "Order charges",
  "breakeven.chargesTotal": "≈{amount}",
  "breakeven.charge.brokerage": "Brokerage",
  "breakeven.charge.stt": "STT",
  "breakeven.charge.transaction": "Transaction",
  "breakeven.charge.sebi": "SEBI",
  "breakeven.charge.stamp": "Stamp duty",
  "breakeven.beTag": "B/E",
  "breakeven.tableLabel": "Breakeven for the example",
  "breakeven.tableBought": "Bought at",
  "breakeven.tableCharges": "Order charges (incl. GST)",
  "breakeven.tableShow": "Show the charges breakdown",
  "breakeven.tableHide": "Hide the charges breakdown",
  "breakeven.charge.gst": "GST (18%)",
  "breakeven.tableBreakeven": "Breakeven price",
  "breakeven.info1": "See your **Breakeven price** live on your ScalpPro",
  "breakeven.info2": "For a positive P&L after charges, always **sell above your breakeven line**",
  "settings.title": "Chart settings",
  "settings.autoTpSl": "Auto TP/SL",
  "settings.applied": "Applied",
  "settings.chartType": "Chart type",
  "settings.type.candles": "Candles",
  "settings.type.heikinAshi": "Heikin Ashi",
  "settings.type.line": "Line",
  "settings.stopLoss": "Stop Loss Preference",
  "settings.sl.market": "At Market Price",
  "settings.sl.limit": "At Limit Price",
  "settings.view": "View on chart",
  "settings.breakeven": "Breakeven line",
  "settings.new": "New",
  "settings.executions": "Buy/Sell executions",
  "settings.sync": "Sync Charts",
  "settings.cancel": "Cancel",
  "settings.apply": "Apply",
  "expiring.title": "Expiring This Week",
  "expiring.days": "Days with expiries",
  "expiring.nextWeek": "Next week",
  "expiring.weekRange": "{from} – {to}",
  "expiring.tag": "OPT Expiry {day}",
  "expiring.today": "Today",
  "expiring.tomorrow": "Tomorrow",
  "expiring.up": "Strong Uptrend",
  "expiring.down": "Strong Downtrend",
  "expiring.since": "Since {time}",
  "expiring.futTag": "FUT Expiry {date}",
  "expiring.ltp": "LTP",
  "expiring.sinceInfo": "About the trend",
  "expiring.margin": "Margin Per Lot",
  "expiring.buy": "Buy",
  "expiring.eventTag": "{event} · {day} {time}",
  "trendInfo.label": "{trend} on {symbol}",
  "trendInfo.disclaimerTitle": "Disclaimer:",
  "trendInfo.disclaimer": "Dash AI provides descriptive market data visualisation only and does not issue trading signals or investment advice.",
  "trendInfo.byDash": "Analyzed by Dash",
  "trendInfo.okay": "Okay",
  "expiryAll.title": "Commodity Calendar",
  "expiryAll.filter": "Contract type",
  "expiryAll.tab.all": "All",
  "expiryAll.tab.option": "Options",
  "expiryAll.tab.future": "Futures",
  "expiryAll.tab.event": "Events",
  "expiryAll.kind.option": "Options",
  "expiryAll.kind.future": "Futures",
  "expiryAll.kind.event": "Event",
  "expiryAll.impact.high": "High impact",
  "expiryAll.impact.medium": "Medium impact",
  "expiryAll.impact.low": "Low impact",
  "expiryAll.previous": "Previous",
  "expiryAll.forecast": "Forecast",
  "expiryAll.actual": "Actual",
  "expiryAll.due": "Due",
  "expiryAll.bullishFor": "Bullish for {name}",
  "expiryAll.bearishFor": "Bearish for {name}",
  "expiryAll.scalper": "Open {name} in ScalpPro",
  "expiryAll.chain": "Open the {name} option chain",
  "signals.title": "Zing signals",
  "signals.allTitle": "All Signals",
  "signals.strip.people": "{count} people",
  "signals.strip.traded": "have traded on {name} today",
  "signals.strip.trending": "Trending on MCX",
  "signals.strip.tradedShort": "{count} traded today",
  "signals.strip.moveIs": "{name} is",
  "signals.strip.today": "today",
  "signals.strip.open": "MCX is open till 11:30 PM",
  "signals.strip.live": "Live",
  "signals.strip.name.gold": "gold",
  "signals.strip.name.silver": "silver",
  "signals.strip.name.crude": "crude oil",
  "signals.strip.name.gas": "natural gas",
  "signals.strip.title.gold": "Gold",
  "signals.strip.title.silver": "Silver",
  "signals.strip.title.crude": "Crude oil",
  "signals.strip.title.gas": "Natural gas",
  "signals.filter": "Filter signals",
  "signals.filterOn": "A filter is saved",
  "signals.chips": "Signal filters",
  "signals.yours": "Your filter ({count})",
  "signals.all": "All Signals ({count})",
  "signals.win50": "Win rate ≥ 50% ({count})",
  "signals.nifty": "Nifty",
  "signals.sensex": "Sensex",
  "signals.savedTip": "Filter applied & saved for quick access",
  "signals.active": "Active signals ({count})",
  "signals.totalPnl": "Total P&L",
  "signals.plus": "+{amount}",
  "signals.pnl": "P&L",
  "signals.winRate": "Win rate",
  "signals.percent": "{value}%",
  "signals.rr": "RR",
  "signals.view": "View",
  "signals.viewLabel": "View {name}",
  "signals.none": "No signals here right now",
  "signals.noneHint": "New signals show up as the strategies fire. Try another filter.",
  "signals.filterTitle": "Filter signals",
  "signals.picked": "Picked filters",
  "signals.remove": "Remove {label}",
  "signals.cancel": "Cancel",
  "signals.apply": "Apply",
  "signals.clearAll": "Clear All",
  "signals.allIndices": "All Indices",
  "signals.section.indices": "Indices",
  "signals.section.winRate": "Win rate",
  "signals.section.direction": "Call/Put",
  "signals.section.strategies": "Strategies",
  "signals.market.nifty": "NIFTY 50",
  "signals.market.sensex": "SENSEX",
  "signals.market.banknifty": "BANKNIFTY",
  "signals.market.stocks": "F&O Stocks",
  "signals.market.commodity": "Commodity",
  "signals.win.all": "All",
  "signals.win.50": "Win rate ≥ 50%",
  "signals.win.30": "Win rate ≥ 30%",
  "signals.dir.all": "All",
  "signals.dir.call": "Call",
  "signals.dir.put": "Put",
  "signals.pill.nifty": "Nifty 50",
  "signals.pill.sensex": "SENSEX",
  "signals.pill.banknifty": "Bank Nifty",
  "signals.pill.stocks": "F&O Stocks",
  "signals.pill.commodity": "Commodity",
  "signals.segments": "Signal segments",
  "signals.segment.all": "All",
  "signals.segment.index": "Index",
  "signals.segment.stocks": "Stocks",
  "signals.segment.commodity": "Commodities",
  "signals.commodity.gold": "Gold",
  "signals.commodity.silver": "Silver",
  "signals.commodity.crude": "Crude Oil",
  "signals.commodity.gas": "Natural Gas",
  "signals.mcx": "MCX · {name}",
  "signals.win25": "Win rate ≥ 25% ({count})",
  "signals.banknifty": "Bank Nifty"
}
```

### `src/flows/fno/copy.ts`

```ts
import { makeCopy } from '../../shared/copy'
import copy from './copy.json'

export const t = makeCopy('fno', copy)
```

### `src/flows/fno/data.ts`

```ts
import type { ChartCandle } from '@l3/components/Chart'

/** Snapshot examples from Figma 11569:41100; these are not live quotes. */
export const indices = [
  { name: 'NIFTY 50', expiry: 'Expires Tue', price: '51,663.15', change: 252.89, percent: '0.05%' },
  { name: 'SENSEX', expiry: 'Expires 25 Aug', price: '51,663.15', change: 252.89, percent: '0.05%' },
  { name: 'GOLD MINI', expiry: 'Expires 25 Aug', price: '51,663.15', change: 252.89, percent: '0.05%' },
]

export type Contract = { id: string; name: string; description: string; price: number; change: number; volume: number; side?: 'call' | 'put' }
export const options: Contract[] = Array.from({ length: 4 }, (_, i) => ({ id: `option-${i}`, name: 'NIFTY 19400 CE', description: 'Call | 14 Jan 26', price: 417, change: 0.1, volume: 12400 + i * 1200, side: 'call' }))
export const futures: Contract[] = ['POWERINDIA', 'PYTM', 'MCX', 'TITAN'].map((name, i) => ({ id: `future-${i}`, name, description: 'Fut | 14 Jan 26', price: 417, change: 0.1, volume: 18600 + i * 2300 }))
export const stockOptions: Contract[] = futures.map((c) => ({ ...c, id: `${c.id}-call`, name: `${c.name} 400 CE`, description: 'Call | 14 Jan 26', side: 'call' }))
export type Watchlist = { id: string; name: string; count: number }
export const watchlists: Watchlist[] = [
  { id: 'special', name: 'Special 25', count: 5 },
  { id: 'banking', name: 'Banking watchlist', count: 4 },
  { id: 'favourites', name: 'Favourites', count: 6 },
]
/** The source deliberately repeats JSWSTEEL; up/down colour follows each tile's surface. */
export const heatmap = Array.from({ length: 9 }, (_, i) => ({ id: `heat-${i}`, name: 'JSWSTEEL', change: -0.27, price: '2,817.40', tone: (i % 3 === 1 ? 'up' : 'down') as 'up' | 'down' }))

const closes = [24980,24970,24994,24982,25000,24988,24976,24991,24997,24989,25002,25020,25012,25028,25035,25026,25050,25066,25054,25075,25088,25110,25130,25118,25142,25132,25155,25140,25162,25150,25133,25144,25124,25116,25100,25090,25103,25084,25110,25120]
export const priceCandles: ChartCandle[] = closes.map((close, i) => {
  const open = i ? closes[i - 1] : close - 12
  return { open, close, high: Math.max(open, close) + 11, low: Math.min(open, close) - 10, volume: 24 + (i * 37) % 75 }
})
/** Other metric series are illustrative prototype states, not analytics. */
export function chartSeries(metric: string, index: string): ChartCandle[] {
  const factor = index === 'SENSEX' ? 3 : index === 'BANK NIFTY' ? 2 : 1
  return priceCandles.map((c, i) => {
    const base = metric === 'price' ? c.close * factor : metric === 'pcr' ? 0.7 + i / 100 : metric === 'oi' ? 12000 + i * 80 : 100 + Math.sin(i / 5) * 40
    const delta = metric === 'price' ? (c.close - c.open) * factor : base * 0.01
    return { open: base - delta, close: base, high: base + Math.abs(delta) + (metric === 'price' ? 10 : base * 0.01), low: base - Math.abs(delta) - (metric === 'price' ? 10 : base * 0.01), volume: c.volume }
  })
}

/**
 * Scalper: two linked intraday panes (5-minute candles, 11:30 → 15:25) traced from the live app's screenshot —
 * NIFTY 50 spot and the NIFTY 27 OCT 22750 call. Illustrative prototype data, not live quotes. Each candle opens at
 * the previous close; the wick sizes vary a little so the panes read like a real session. The session's high and low
 * are pinned to the screenshot's markers (22,753.20 / 22,541.55 and 123.25 / 52.35).
 */
export type ScalperInstrument = {
  /** The contract's name, e.g. "NIFTY 50". */
  name: string
  /** What the first pane shows (Spot / Futures); the option pane has none. */
  segment?: string
  /** Call / Put, for an option. */
  side?: string
  price: number
  change: number
  percent: number
  candles: ChartCandle[]
  /** The first candle's time and the candle length, for the time axis. */
  start: string
  minutes: number
}

const spotCloses = [22556, 22545, 22562, 22584, 22596, 22606, 22598, 22589, 22576, 22593, 22608, 22622, 22634, 22617, 22598, 22582, 22574, 22590, 22606, 22620, 22652, 22641, 22655, 22646, 22662, 22653, 22646, 22658, 22650, 22704, 22690, 22673, 22668, 22684, 22679, 22694, 22706, 22712, 22691, 22708, 22714, 22719, 22716, 22723, 22725, 22721, 22728, 22753.2]
const optionCloses = [56, 61, 59, 66, 64, 58, 61, 66, 59, 67, 73, 69, 62, 58, 55, 59, 63, 68, 74, 70, 79, 83, 78, 86, 82, 90, 84, 79, 121, 111, 96, 91, 95, 92, 102, 99, 104, 96, 88, 100, 103, 101, 104, 106, 104, 107, 106, 108.2]

function sessionCandles(closes: number[], wick: number, pins: { high: [number, number]; low: [number, number] }): ChartCandle[] {
  return closes.map((close, i) => {
    const open = i ? closes[i - 1] : close + wick
    const reach = wick * (1 + ((i * 7) % 5) / 4)
    const last = i === closes.length - 1
    let high = last ? Math.max(open, close) : Math.max(open, close) + reach
    let low = Math.min(open, close) - reach
    // The session's high and low are the screenshot's: no other wick goes past them.
    high = i === pins.high[0] ? pins.high[1] : Math.min(high, pins.high[1] - wick / 2)
    low = i === pins.low[0] ? pins.low[1] : Math.max(low, pins.low[1] + wick / 2)
    return { open, close, high, low }
  })
}

export const scalperSpot: ScalperInstrument = {
  name: 'NIFTY 50', segment: 'Spot', price: 22753.2, change: 153.2, percent: 0.68,
  candles: sessionCandles(spotCloses, 6, { high: [47, 22753.2], low: [1, 22541.55] }),
  start: '11:30', minutes: 5,
}

export const scalperOption: ScalperInstrument = {
  name: 'NIFTY 27OCT 22750', side: 'Call', price: 108.2, change: 41.75, percent: 62.83,
  candles: sessionCandles(optionCloses, 2, { high: [28, 123.25], low: [14, 52.35] }),
  start: '11:40', minutes: 5,
}

/** The Lemonn indicators in the chart-tools sheet (the live app's list, alphabetical). */
export const lemonnIndicators = ['5 EMA Sell - Power Of Stocks', '5/20 EMA by AbhishekX Trades', 'ADX', 'ALMA', 'ASP by TradersPath Academy', 'ATR', 'Bollinger Band Width', 'Bollinger Bands', 'CPR', 'DEMA', 'EMA', 'Ichimoku Cloud', 'MACD', 'Nifty 5-Star Indicator by Dr. Gokul Chhabra', 'Opening Range Breakout (ORB)', 'RSI', 'Supertrend', 'VWAP']

/**
 * A position on the Scalper's option chart: bought `quantity` units at `entry` (the average price). Take-profit and
 * stop-loss are exit prices (null = not set). `trailing`: the stop-loss follows the price up (Add Trail).
 */
export type ScalperPosition = {
  entry: number
  quantity: number
  takeProfit: number | null
  stopLoss: number | null
  trailing: boolean
}

/** The sample open position (fno-35): 1 lot bought at ₹104.60 a little earlier, TP and SL set. */
export const scalperPosition: ScalperPosition = { entry: 104.6, quantity: 65, takeProfit: 115.2, stopLoss: 96.4, trailing: false }

/** A new order's TP and SL start this far from the entry (₹ per unit); the user drags them from there. */
export const SCALPER_TP_SL_GAP = 10

/**
 * Round-trip charges for buying and later selling `quantity` options at `entry` (NSE options, Lemonn's flat brokerage).
 * The sell side is priced at the entry too — at breakeven the sell price is only a few paise higher, so the difference
 * is far below a paisa per unit.
 */
export const optionCharges = {
  brokeragePerOrder: 20, // ₹ per executed order: one to buy, one to sell
  stt: 0.001, // 0.1% of the sell premium
  exchange: 0.0003503, // NSE transaction charge, 0.03503% of premium turnover (buy + sell)
  sebi: 10 / 1e7, // ₹10 per crore of turnover
  stamp: 0.00003, // 0.003% of the buy premium
  gst: 0.18, // 18% on brokerage + exchange + SEBI charges
}

/** Total ₹ charges for a round trip (buy and sell) of `quantity` units at `entry`. */
export function roundTripCharges(entry: number, quantity: number) {
  const c = optionCharges
  const buy = entry * quantity
  const turnover = buy * 2
  const brokerage = c.brokeragePerOrder * 2
  const exchange = turnover * c.exchange
  const sebi = turnover * c.sebi
  return brokerage + exchange + sebi + buy * c.stt + buy * c.stamp + (brokerage + exchange + sebi) * c.gst
}

/**
 * Breakeven: the sell price at which the Net P&L (after every charge) is zero — the entry plus the charges spread over
 * every unit, rounded up to the option tick (₹0.05) so selling at it never ends in a loss.
 */
export function breakevenPrice(entry: number, quantity: number) {
  const exact = entry + roundTripCharges(entry, quantity) / quantity
  return Math.round(Math.ceil(exact / OPTION_TICK - 1e-9) * OPTION_TICK * 100) / 100
}

/** Options trade in steps of ₹0.05. */
export const OPTION_TICK = 0.05

/**
 * What the example pays, in ₹ on its ₹100 buy (the rate card, as a % of ₹100 — one unit, so a % reads straight as ₹):
 * brokerage 0.01% each way (₹0.02), STT 0.15% on the sell (₹0.15), NSE transaction 0.03553% each way (₹0.07), SEBI
 * 0.0001% each way (₹0.0002), stamp 0.003% on the buy (₹0.003). GST isn't a band of its own: it's charged on the
 * charges, not the trade. Bottom to top, in the order they stack up: brokerage last at the bottom, then the rest
smallest to biggest, so STT sits on top under the breakeven line and brokerage stays clear of it.
 */
export type ExampleChargeId = 'brokerage' | 'stt' | 'transaction' | 'sebi' | 'stamp'
export type ExampleCharge = { id: ExampleChargeId; amount: number }

const EXAMPLE_ENTRY = 100
const ofEntry = (percent: number) => (percent / 100) * EXAMPLE_ENTRY

export const breakevenCharges: ExampleCharge[] = [
  { id: 'brokerage', amount: 2 * ofEntry(0.01) },
  { id: 'sebi', amount: 2 * ofEntry(0.0001) },
  { id: 'stamp', amount: ofEntry(0.003) },
  { id: 'transaction', amount: 2 * ofEntry(0.03553) },
  { id: 'stt', amount: ofEntry(0.15) },
]

/** GST, 18% on brokerage + transaction + SEBI (not a band of the chart: it's charged on the charges). */
export const exampleGst = optionCharges.gst * breakevenCharges.filter((c) => c.id === 'brokerage' || c.id === 'transaction' || c.id === 'sebi').reduce((sum, charge) => sum + charge.amount, 0)
/** Everything the example pays, GST included (≈₹0.26). */
export const exampleChargesTotal = breakevenCharges.reduce((sum, charge) => sum + charge.amount, 0) + exampleGst
/** ₹100 + the charges with GST (₹0.26), up to the next tick: ₹100.30. */
const exampleBreakeven = Math.round(Math.ceil((EXAMPLE_ENTRY + exampleChargesTotal) / OPTION_TICK - 1e-9) * OPTION_TICK * 100) / 100

/**
 * How breakeven works — the example trade its explainer plays (the recorded Figma explainer): 1 lot bought at ₹100,
 * breakeven ₹100.30 after charges (GST included), sold at ₹102. `path` is the price line: where each turn sits across the plot (0 = its
 * left edge, 1 = its right) and the price there; it crosses the breakeven line at its 3rd point.
 */
export const breakevenExample = {
  entry: EXAMPLE_ENTRY,
  breakeven: exampleBreakeven,
  exit: 102,
  axis: [103, 102, 101, 100],
  path: [
    { at: 0.029, price: EXAMPLE_ENTRY },
    { at: 0.239, price: 100.1 },
    { at: 0.407, price: exampleBreakeven },
    { at: 0.608, price: 101.1 },
    { at: 0.86, price: 102 },
  ],
}

/** The chart's display settings (chart-tools sheet → Settings). */
export type ChartType = 'candles' | 'heikinAshi' | 'line'
export type StopLossPreference = 'market' | 'limit'
export type ChartSettings = {
  chartType: ChartType
  stopLoss: StopLossPreference
  breakevenLine: boolean
  executions: boolean
  syncCharts: boolean
}
export const defaultChartSettings: ChartSettings = { chartType: 'candles', stopLoss: 'market', breakevenLine: true, executions: true, syncCharts: false }

/*
 * Zing signals (Scalper → the Active chip, top right): live trade signals from Zing strategies. Snapshot sample from
 * Figma 6900:23853 (file 9r61YQp7QQZAQovDyz8hLF, "Enrich signal filter"); not live data.
 */
/** Where a signal trades — the filter sheet's Indices group and the quick chips. */
export type SignalMarket = 'nifty' | 'sensex' | 'banknifty' | 'stocks' | 'commodity'
/** The strategy's picture: a person, the Lemonn mascot, or a brand logo (assets/signals). */
export type SignalAvatar = 'neeraj' | 'lemon' | 'booming'
export type ZingSignal = {
  id: string
  strategy: string
  avatar: SignalAvatar
  market: SignalMarket
  /** The tag under the name: the underlying (NIFTY, SILVER 100). */
  underlying: string
  /** Back-tested win rate in percent. A strategy without one shows its P&L instead. */
  winRate?: number
  /** Today's P&L on this signal, ₹ (shown when there's no win rate). */
  pnl?: number
  side: 'Buy' | 'Sell'
  option: 'call' | 'put'
  /** The contract, as the card's first figure reads it ("Call 23950"). */
  contract: string
  /** Risk : reward, as written ("1.4", "1:2"). */
  rr: string
  /** The rule that fired, label then value ("EMA 9 >" "EMA 21", "Price ≥" "EMA 9", "PCR" "1.55"). */
  rule: [string, string]
  /** The rule's label is greyed (a name before a number, like PCR) or reads with its value (a comparison). */
  ruleMuted?: boolean
  /** A commodity signal: which commodity (its logo, from commodities/assets). */
  commodity?: SignalCommodity
  /** A commodity signal's nudge strip (setting "Commodity nudge strip"): how many traded it today, and today's move. */
  nudge?: { traders: string; move: string }
}
/** The MCX commodities a signal can be on (the Commodities home's shortcuts). */
export type SignalCommodity = 'gold' | 'silver' | 'crude' | 'gas'
/** How a signal's market reads as a segment: index options, F&O stock options, or MCX commodities. */
export type SignalSegment = 'index' | 'stocks' | 'commodity'
export const segmentOf = (signal: ZingSignal): SignalSegment => (signal.market === 'commodity' ? 'commodity' : signal.market === 'stocks' ? 'stocks' : 'index')
export const zingSignals: ZingSignal[] = [
  // Newest first, as the live feed: index, commodity (MCX) and F&O stock signals come in mixed.
  { id: 'scalping-pulse', strategy: 'Scalping Pulse by Neeraj', avatar: 'neeraj', market: 'nifty', underlying: 'NIFTY', winRate: 72, side: 'Buy', option: 'call', contract: 'Call 23950', rr: '1.4', rule: ['EMA 9 >', 'EMA 21'] },
  { id: 'gold-breakout', strategy: 'Gold Breakout Pro', avatar: 'lemon', market: 'commodity', commodity: 'gold', underlying: 'GOLD', winRate: 64, side: 'Buy', option: 'call', contract: 'Call 72000', rr: '1.5', rule: ['Price ≥', 'VWAP'], nudge: { traders: '2.1K+', move: '+1.2%' } },
  { id: 'prime-ema', strategy: 'Prime scalper EMA', avatar: 'lemon', market: 'nifty', underlying: 'NIFTY', pnl: 367.3, side: 'Buy', option: 'put', contract: 'Put 23950', rr: '1:2', rule: ['Price ≥', 'EMA 9'] },
  { id: 'booming-bulls', strategy: 'Booming Bulls Put SuperTrend', avatar: 'booming', market: 'sensex', underlying: 'SENSEX', winRate: 34, side: 'Buy', option: 'call', contract: 'Call 23950', rr: '1.3', rule: ['PCR', '1.55'], ruleMuted: true },
  { id: 'crude-reversal', strategy: 'Crude Reversal', avatar: 'booming', market: 'commodity', commodity: 'crude', underlying: 'CRUDEOIL', winRate: 58, side: 'Buy', option: 'put', contract: 'Put 6200', rr: '1:2', rule: ['RSI', '28'], ruleMuted: true, nudge: { traders: '1.4K+', move: '−2.4%' } },
  { id: 'reliance-orb', strategy: 'Opening Range Breakout', avatar: 'neeraj', market: 'stocks', underlying: 'RELIANCE', winRate: 61, side: 'Buy', option: 'call', contract: 'Call 2960', rr: '1.3', rule: ['Price ≥', 'ORB high'] },
  { id: 'bank-trend', strategy: 'Bank Nifty Trend Rider', avatar: 'booming', market: 'banknifty', underlying: 'BANKNIFTY', winRate: 52, side: 'Buy', option: 'call', contract: 'Call 51500', rr: '1.4', rule: ['ADX', '31'], ruleMuted: true },
  { id: 'gas-squeeze', strategy: 'NatGas Squeeze', avatar: 'lemon', market: 'commodity', commodity: 'gas', underlying: 'NATURALGAS', winRate: 47, side: 'Buy', option: 'put', contract: 'Put 280', rr: '1:2', rule: ['Price <', 'VWAP'], nudge: { traders: '860+', move: '+3.1%' } },
  { id: 'inside-candle', strategy: 'Inside Candle', avatar: 'lemon', market: 'nifty', underlying: 'NIFTY', winRate: 56, side: 'Buy', option: 'call', contract: 'Call 23950', rr: '1.2', rule: ['EMA 9 >', 'EMA 21'] },
]
/** Total P&L across today's signals (Figma's figure). */
export const signalsTotalPnl = 13367

/** The filter sheet's choices. Indices and Strategies pick several (none = all); Win rate and Call/Put pick one. */
export type SignalFilter = { markets: SignalMarket[]; winRate: 'all' | '50' | '30'; direction: 'all' | 'call' | 'put'; strategies: string[] }
export const noSignalFilter: SignalFilter = { markets: [], winRate: 'all', direction: 'all', strategies: [] }
export const signalMarkets: SignalMarket[] = ['nifty', 'sensex', 'banknifty', 'stocks', 'commodity']

export function matchesFilter(signal: ZingSignal, filter: SignalFilter) {
  if (filter.markets.length && !filter.markets.includes(signal.market)) return false
  if (filter.winRate !== 'all' && (signal.winRate ?? 0) < Number(filter.winRate)) return false
  if (filter.direction !== 'all' && signal.option !== filter.direction) return false
  if (filter.strategies.length && !filter.strategies.includes(signal.id)) return false
  return true
}
/** How many choices narrow the list (0 = no filter). */
export function filterCount(filter: SignalFilter) {
  return filter.markets.length + filter.strategies.length + (filter.winRate === 'all' ? 0 : 1) + (filter.direction === 'all' ? 0 : 1)
}

/** The filter the Figma frames pick (Nifty 50 + Sensex, two strategies): the prototype's "Your filter" screens. */
export const sampleSignalFilter: SignalFilter = { markets: ['nifty', 'sensex'], winRate: 'all', direction: 'all', strategies: ['booming-bulls', 'inside-candle'] }
```

### `src/flows/fno/flatCards.module.css`

```css
/*
 * F&O: no shadow on any card. L3 gives clickable cards (Card, card ListCells) elevation-soft; in this flow they keep
 * only their 1px border. Put on every F&O screen's root (Screen className), so its sheets are covered too. Repeated
 * class: above L3's own (selected) card rules.
 */
.flatCards.flatCards [data-interactive][data-padding] { box-shadow: var(--card-border); }
.flatCards.flatCards [data-interactive][data-variant='card'] { box-shadow: inset 0 0 0 1px var(--l3-border-light); } /* 1px hairline */
.flatCards.flatCards [data-interactive][data-variant='card'][data-selected] { box-shadow: inset 0 0 0 1px var(--l3-border-dark); } /* 1px hairline */
```

### `src/flows/fno/index.tsx`

```tsx
import type { Flow, Go } from '../types'
import { Home, type HomePart, type Product } from './screens/Home'
import { LotSummary } from './commodities/screens/LotSummary'
import { AssetPage } from './commodities/screens/AssetPage'
import { ExpiryTimeline } from './commodities/screens/ExpiryTimeline'
import { goldMiniAsset, illiquidAsset } from './commodities/data'
import { OptionChain } from './option-chain/screens/OptionChain'
import { OrderPad } from './order-pad/screens/OrderPad'
import type { Segment } from './strategies/data'
import { noSignalFilter, sampleSignalFilter, scalperPosition } from './data'
import { Scalper } from './screens/Scalper'
import { SplashScreen } from '../../shared/ui/Splash'
import { markMove } from '../../shared/prototype'

/**
 * Each product tab is its own screen, all in group 'home': one page in different states, so a tab switch keeps the
 * header and the product tabs in place and only the content under the tabs slides (Home animates it).
 */
/**
 * ScalpPro (home cards, Expiry calendar …) always opens the Scalper as a new page, in from the right — even from screens
 * listed after it, which app order alone would read as back. Its back returns to that page (`backOr`).
 */
/** The Zing signals sheet screens whose list the "Commodity signals" version changes (not the filter screens). */
const SIGNALS_SHEET_SCREENS = ['fno-39', 'fno-45', 'fno-46', 'fno-47']
const openScalper = (go: Go) => { markMove('fno-05', 'forward'); go('fno-05') }
/** Back to wherever the asset page was opened from (option chain, Gold Summary, Search…); `fallback` when opened directly. */
const backOr = (go: Go, fallback: string) => { if (window.history.length > 1) window.history.back(); else go(fallback) }

const tabScreen = (product: Product, segment?: Segment) => product === 'equity' ? 'fno-01' : product === 'commodities' ? 'fno-08' : segment === 'commodities' ? 'fno-16' : 'fno-15'
type HomeOptions = { scrollTo?: HomePart; product?: Product; segment?: Segment; picker?: 'equity' | 'commodities' }
const home = (go: Go, scrollTo?: HomePart, options: HomeOptions = {}) => <Home scrollTo={scrollTo} product={options.product} segment={options.segment} picker={options.picker} onProduct={(product, segment) => go(tabScreen(product, segment))} onCommodity={() => go('fno-12')} onAsset={() => go('fno-21')} onExpiries={() => go('fno-38')} onHome={() => go('stocks-01')} onSearch={() => go('search-25')} onProfile={() => go('profile-01')} onWallet={() => go('deposit-01')} onDash={() => go('dash-02')} onUsStocks={() => go('stocks-09')} onOptions={() => go('search-26')} onFutures={() => go('search-27')} onChain={() => go('fno-17')} onScalper={() => openScalper(go)} />

export const fno: Flow = {
  id: 'fno', title: 'F&O',
  description: 'Equity F&O home: P&L, indices, chart metrics, watchlists, Smart Options, Futures Heatmap and Smart Futures.',
  figmaFile: 'nLs24dTJdPz9A5pu3AWMbe',
  options: [
    // The breakeven sheet (fno-36): Version 2 (default) = What is breakeven line? + the charges table,
    // no info lines; Version 1 = the sheet as it first shipped (How breakeven works, two info lines, no table).
    // Commodity nudge strip (Figma 6946:42446, 24 Nov): a strip that peeks out over a commodity signal's card with a
    // reason to look (how many traded it today); it slides out from behind the card, then a shimmer runs across it.
    // The only Zing signals setting (24 Nov: the Commodity signals versions are gone — segment tabs + the logo tag stay).
    // A floating S0 … S4 bubble on the signals sheet screens flips it.
    {
      id: 'commodityStrip',
      group: 'Zing signals',
      label: 'Commodity nudge strip',
      picker: 'dropdown',
      values: [{ value: 'off', label: 'Off' }, { value: 's1', label: '1 · Gold glow (Figma)' }, { value: 's2', label: '2 · Colour per commodity' }, { value: 's3', label: '3 · Dark ticker' }, { value: 's4', label: '4 · Rotating facts' }],
      default: 's1',
      floatOn: SIGNALS_SHEET_SCREENS,
      quickSwitch: {
        on: SIGNALS_SHEET_SCREENS,
        // On the chart, above the sheet (it's 75% of the screen; the default spot lands on its tabs).
        spot: { side: 'left', y: 0.14 },
        values: [
          { value: 'off', label: 'Nudge strip off', short: 'S0' },
          { value: 's1', label: 'Nudge strip 1 · Gold glow (Figma)', short: 'S1' },
          { value: 's2', label: 'Nudge strip 2 · Colour per commodity', short: 'S2' },
          { value: 's3', label: 'Nudge strip 3 · Dark ticker', short: 'S3' },
          { value: 's4', label: 'Nudge strip 4 · Rotating facts', short: 'S4' },
        ],
      },
    },
    { id: 'breakevenSheet', group: 'Scalper', label: 'Breakeven sheet', values: [{ value: 'v1', label: 'Version 1' }, { value: 'v2', label: 'Version 2' }], default: 'v2', floatOn: ['fno-36'] },
    // Expiring This Week (Commodities, fno-08): Version 1 = the sideways card rail; Version 2 = a short calendar (the
    // calendar's first 3 entries on their days, View all → fno-38); Version 3 = that calendar in one card.
    { id: 'expiringVersion', group: 'Commodities', label: 'Expiring This Week', values: [{ value: 'v1', label: 'Version 1' }, { value: 'v2', label: 'Version 2' }, { value: 'v3', label: 'Version 3' }, { value: 'v4', label: 'Version 4' }], default: 'v4', floatOn: ['fno-08', 'fno-09', 'fno-10'] },
    // Expiring This Week v2 / v3: which sample week the short calendar shows, to see how the days split — 3 today,
    // 2 today + 1 tomorrow, or 1 a day. Contracts only on the first two days; the event comes on day 3.
    // “Calendar days” (sample weeks) archived 2026-11-24 — real data only (commodities/archive/expiryPreviewSamples.ts).
    // Expiring This Week (Commodities, fno-08): show or hide the cards' ScalpPro + Buy footer (the whole grey strip).
    { id: 'expiringButtons', group: 'Commodities', label: 'Expiring card buttons', picker: 'toggle', values: [{ value: 'off', label: 'Hidden' }, { value: 'on', label: 'Shown' }], default: 'on', floatOn: ['fno-08', 'fno-09', 'fno-10'],
      // Phone app mode: a floating one-tap switch on the Commodities home, so it flips without opening the settings sheet.
      quickSwitch: { on: ['fno-08', 'fno-09', 'fno-10'], values: [{ value: 'on', label: 'Shown', short: 'BTN ON' }, { value: 'off', label: 'Hidden', short: 'BTN OFF' }] } },
  ],
  // The F&O tab's parts, as the preview lists them (like the tab's own pages). Positions isn't built yet.
  sections: [
    { id: 'home', title: 'Home' },
    { id: 'chain', title: 'Option chain' },
    { id: 'scalper', title: 'Scalper' },
    { id: 'asset', title: 'Contracts & asset page' },
    { id: 'order', title: 'Order pad' },
  ],
  screens: [
    { id: 'fno-34', section: 'home', name: 'Splash', figma: '', badge: 'new', tab: true, note: 'The launch splash: the Lemonn logo centred for 2 s, then it fades into Equity home (a tap skips ahead). Hidden at launch for now (src/shared/ui/Splash: SPLASH_SCREENS is empty), so the app opens straight on the home; this page still plays it.', render: (go) => <SplashScreen onDone={() => go('fno-01')} home={home(go)} /> },
    { id: 'fno-01', section: 'home', group: 'home', name: 'Equity home', badge: 'changed', badgeNote: 'New US Markets · Live banner under the shortcuts; opens US Stocks', figma: '11569:41100', tab: true, note: 'From the main F&O tab. Home returns to Stocks; DASH, Search, Profile and Wallet open their existing flows. Selectors, chart metrics, filters, sorting and watchlist creation work locally. Destinations outside this frame open an explanatory sheet.', render: (go) => home(go) },
    { id: 'fno-02', section: 'home', group: 'home', name: 'Home · watchlists & Smart Options', figma: '11569:41100', tab: true, note: 'The same long screen, scrolled to watchlists.', render: (go) => home(go, 'watchlists') },
    { id: 'fno-03', section: 'home', group: 'home', name: 'Home · Futures Heatmap', figma: '11569:41100', tab: true, render: (go) => home(go, 'heatmap') },
    { id: 'fno-04', section: 'home', group: 'home', name: 'Home · Smart Futures', figma: '11569:41100', tab: true, render: (go) => home(go, 'futures') },
    { id: 'fno-05', section: 'scalper', name: 'Scalper', figma: '', note: 'From ScalpPro on F&O home, the Expiring cards, the Expiry calendar or the Scalper bottom-nav tab — always a new page in from the right; back returns to the page it was opened from. The chart-tools sheet groups personal DASH AI indicators separately from Lemon indicators.', render: (go) => <Scalper onBack={() => backOr(go, 'fno-01')} onCreateIndicator={() => go('dash-20')} /> },
    { id: 'fno-06', section: 'scalper', group: 'scalper', name: 'Scalper · DASH indicator', figma: '', note: 'From DASH AI’s View indicator. Opens the chart-tools sheet directly on Indicators, the saved DASH AI indicator under Your indicators with a focus guide. Tap rows to add / remove indicators (several at once); search filters the list.', render: (go) => <Scalper onBack={() => backOr(go, 'fno-01')} createdIndicator="Supertrend (10, 3) with EMA 20" onCreateIndicator={() => go('dash-20')} /> },
    { id: 'fno-07', section: 'scalper', group: 'scalper', name: 'Scalper · indicator applied', figma: '', note: 'With the saved DASH AI indicator on the chart: “1 ▾” at the chart’s top-left and illustrative EMA 9 / 21 lines on the NIFTY 50 candles.', render: (go) => <Scalper onBack={() => backOr(go, 'fno-01')} createdIndicator="Supertrend (10, 3) with EMA 20" openIndicators={false} initialIndicator="Supertrend (10, 3) with EMA 20" onCreateIndicator={() => go('dash-20')} /> },
    { id: 'fno-35', section: 'scalper', group: 'scalper', name: 'Break Even · position + breakeven line', figma: '11756:78739', badge: 'new', note: 'Version C (Boxed chip): an open position on the option chart — TP pill (drag ⠿ to move, ✕ removes), entry row (Exit · +65 · live P&L), SL pill (+ Add Trail), and the solid warning-light breakeven line with a boxed “Breakeven ⓘ” tag on it, 8 left of the price axis (Figma’s “B/E 105.55”: spelled out, no price — designer’s call; the label still reads the price) (tap → How breakeven works). Breakeven = entry + round-trip charges per unit (data.ts breakevenPrice). Buy at Mkt on fno-05 opens a position the same way; the first buy also opens How breakeven works. Exit buttons are 24 tall to sit on the pills (Figma), not Large.', render: (go) => <Scalper onBack={() => backOr(go, 'fno-01')} onCreateIndicator={() => go('dash-20')} initialPosition={scalperPosition} /> },
    { id: 'fno-36', section: 'scalper', group: 'scalper', name: 'Break Even · How breakeven works (sheet)', figma: '11783:5569', badge: 'new', note: 'Two versions (setting “Breakeven sheet”, floating card beside the phone): Version 2 (default) — heading “What is breakeven line?” (no description; “price” → “line”, 19 Nov), the charges table, no info lines; Version 1 — “How breakeven works” with the two info lines, no table. Opens on the first buy and from the B/E chip’s ⓘ (and Settings → Breakeven line ⓘ). The example card loops (a tap replays it): every play opens with the “Introducing Breakeven Line” intro (2.5 s), then a 9.3 s chart copied from the designer’s recording: on a white chart the buy at ₹100; the chart zooms in 2× and the orange charges zone fills one band per charge from the F&O options rate card, in ₹ on the ₹100 buy (top down: STT ₹0.15, transaction ₹0.07, stamp duty, SEBI, then brokerage ₹0.02 last at the bottom with a smaller tag; they come in top down — no GST band: it’s charged on the charges; heights by cost), then zooms back out to one thin zone, the tags sliding down under it and stacking into one “Order charges ≈₹0.26” tag (GST included); the dashed B/E line at ₹100.30 draws along its top with the chart’s “Breakeven” tag (text only, no price), an LTP bubble rides the price line up through B/E (a ringed marker pulses) to “Sold at ₹102”, the green Net Profit zone fills; it holds, then plays again from the intro. “I understand” is locked until the chart has played once (intro + chart, 11.8 s), a loader line filling along its top edge, then turns primary (Figma’s button variants). Reduced motion: the finished chart, button ready. Under the example, the same trade as a calculation table (a card on the secondary surface, no heading, compact L3 key-value rows, one line each, no lines inside): Bought at ₹100.00 · Order charges (incl. GST) ≈₹0.26 — tap the row to open the breakdown (closed by default: STT, transaction, brokerage, stamp duty, SEBI, GST 18%) — and Breakeven price ₹100.30 in bold (L3 total row). Labels are L3’s 12 styles (the recording’s are ~11). The zoomed-in charges aren’t in Figma or the recording (designer’s brief). A V2 (starts zoomed in on a blue ₹0 → ₹100 fill, zooms out true to scale, sold 12% up at ₹112) is archived in fno/archive/BreakevenExplainerV2.tsx.', render: (go) => <Scalper onBack={() => backOr(go, 'fno-01')} onCreateIndicator={() => go('dash-20')} initialPosition={scalperPosition} initialSheet="breakeven" /> },
    { id: 'fno-37', section: 'scalper', group: 'scalper', name: 'Break Even · chart settings (breakeven line)', figma: '11754:69563', badge: 'new', note: 'The chart-tools sheet on Settings: Auto TP/SL (animated mark, Applied), Chart type (Candles / Heikin Ashi / Line), Stop Loss Preference (radio), View on chart (Breakeven line ⓘ New, Buy/Sell executions, Sync Charts). Changes are a draft: Apply keeps them (unticking Breakeven line hides the B/E line and chip), Cancel or closing drops them. Figma’s rail (Bolt, Indicators, Drawings, Settings) is the live app’s six groups here.', render: (go) => <Scalper onBack={() => backOr(go, 'fno-01')} onCreateIndicator={() => go('dash-20')} initialPosition={scalperPosition} initialSheet="settings" openIndicators={false} /> },
    { id: 'fno-39', section: 'scalper', group: 'signals', name: 'Zing signals · All signals', figma: '6900:23855', badge: 'new', note: 'From the Active chip at the tool row’s right end (Zing). Figma: file 9r61YQp7QQZAQovDyz8hLF (Enrich signal filter), old Lemonn design system, rebuilt in L3. Top row: filter button | All Signals (4) · Win rate ≥ 50% · Commodity · Nifty · Sensex (L3 pill tabs, Small; counts are worked out from the signals). Active signals (n) with Total P&L, then a card per signal: avatar, strategy, market + win rate tags (or a P&L tag), View; under a line Buy Call 23950 • RR • the rule. A chip with no signals shows the L3 empty state. Filter → fno-40.', render: (go) => <Scalper onBack={() => backOr(go, 'fno-01')} onCreateIndicator={() => go('dash-20')} initialSheet="signals" initialSignals={{}} /> },
    { id: 'fno-40', section: 'scalper', group: 'signals', name: 'Zing signals · Filter · Indices', figma: '6900:26203', badge: 'new', note: 'The filter takes the signals sheet over in place, in the Scalper’s Settings sheet look: L3 Side nav Indices · Win rate · Call/Put · Strategies, the white panel with its Heading/16 title row and Clear All, card rows with a checkbox (Indices, Strategies) or radio (Win rate, Call/Put; the chosen one tinted blue), the picks as pills over Cancel / Apply (primary). Cancel or a scrim tap brings the signals back; Apply saves them as Your filter (→ fno-45).', render: (go) => <Scalper onBack={() => backOr(go, 'fno-01')} onCreateIndicator={() => go('dash-20')} initialSheet="signals" initialSignals={{ filter: 'indices' }} /> },
    { id: 'fno-41', section: 'scalper', group: 'signals', name: 'Zing signals · Filter · Indices picked', figma: '6900:29666', badge: 'new', note: 'NIFTY 50 and SENSEX ticked (All Indices unticks itself; untick both and it’s back). The side tab shows how many it picked (Figma: a red 1 — L3 Side nav’s corner flag, in blue). The picks sit as chips over Cancel / Apply; ✕ takes one off.', render: (go) => <Scalper onBack={() => backOr(go, 'fno-01')} onCreateIndicator={() => go('dash-20')} initialSheet="signals" initialSignals={{ filter: 'indices', draft: { ...noSignalFilter, markets: ['nifty', 'sensex'] } }} /> },
    { id: 'fno-42', section: 'scalper', group: 'signals', name: 'Zing signals · Filter · Win rate', figma: '6900:27042', badge: 'new', note: 'Win rate: All · ≥ 50% · ≥ 30% (pick one).', render: (go) => <Scalper onBack={() => backOr(go, 'fno-01')} onCreateIndicator={() => go('dash-20')} initialSheet="signals" initialSignals={{ filter: 'winRate', draft: { ...noSignalFilter, markets: ['nifty', 'sensex'] } }} /> },
    { id: 'fno-43', section: 'scalper', group: 'signals', name: 'Zing signals · Filter · Call/Put', figma: '6900:27889', badge: 'new', note: 'Call/Put: All · Call · Put (pick one).', render: (go) => <Scalper onBack={() => backOr(go, 'fno-01')} onCreateIndicator={() => go('dash-20')} initialSheet="signals" initialSignals={{ filter: 'direction', draft: { ...noSignalFilter, markets: ['nifty', 'sensex'] } }} /> },
    { id: 'fno-44', section: 'scalper', group: 'signals', name: 'Zing signals · Filter · Strategies', figma: '6900:28736', badge: 'new', note: 'Strategies: one row per Zing strategy with its picture (L3 Avatar 24), pick several. A long name is cut at 140 in its chip (Figma dev note).', render: (go) => <Scalper onBack={() => backOr(go, 'fno-01')} onCreateIndicator={() => go('dash-20')} initialSheet="signals" initialSignals={{ filter: 'strategies', draft: { ...noSignalFilter, markets: ['nifty', 'sensex'], strategies: ['booming-bulls'] } }} /> },
    { id: 'fno-45', section: 'scalper', group: 'signals', name: 'Zing signals · Your filter saved (tip)', figma: '6900:30528', badge: 'new', note: 'Right after Apply: Your filter (n) comes in first, selected, with ✕ to remove it; the filter button gets a red dot; a blue tooltip “Filter applied & saved for quick access” with ✕ points at it once (Figma’s colour on the L3 tooltip). Figma keeps All Signals selected; here the saved filter is, so the list shows what it picked.', render: (go) => <Scalper onBack={() => backOr(go, 'fno-01')} onCreateIndicator={() => go('dash-20')} initialSheet="signals" initialSignals={{ saved: sampleSignalFilter, savedTip: true }} /> },
    { id: 'fno-46', section: 'scalper', group: 'signals', name: 'Zing signals · Your filter saved', figma: '6900:24637', badge: 'new', note: 'The same without the tip: next time the sheet opens, Your filter is one tap away.', render: (go) => <Scalper onBack={() => backOr(go, 'fno-01')} onCreateIndicator={() => go('dash-20')} initialSheet="signals" initialSignals={{ saved: sampleSignalFilter }} /> },
    { id: 'fno-47', section: 'scalper', group: 'signals', name: 'Zing signals · All Signals (plain)', figma: '6900:25420', badge: 'new', note: 'Figma’s plain look: an “All Signals” header and every signal. Figma’s ← back is left out: L3 gives the first sheet over a screen no back button.', render: (go) => <Scalper onBack={() => backOr(go, 'fno-01')} onCreateIndicator={() => go('dash-20')} initialSheet="signals" initialSignals={{ plain: true }} /> },
    { id: 'fno-08', section: 'home', group: 'home', name: 'Commodities home', figma: '6754:63637', tab: true, note: 'The Commodities product tab. Gold / Silver / Crude Oil / Natural Gas shortcuts open the Lot summary (Gold Summary). The chart’s instrument selector (“Gold”) opens the contract picker. Popular commodities: Options ⇕ Futures switch; Futures Heatmap: Bullion / Energy / Metals.', render: (go) => home(go, undefined, { product: 'commodities' }) },
    { id: 'fno-09', section: 'home', group: 'home', name: 'Commodities · heatmap & Smart Futures', figma: '6754:63637', tab: true, note: 'The same long screen, scrolled to the Futures Heatmap.', render: (go) => home(go, 'heatmap', { product: 'commodities' }) },
    { id: 'fno-10', section: 'home', group: 'home', name: 'Contract picker · Commodities', figma: '6754:65111', tab: true, note: 'From the chart’s “Gold ⇕”. Equity / Commodities tabs in the sheet header’s bottom slot, commodity chips (All, Gold, Silver …) under them; contracts grouped by commodity as radio rows (Gold Mini tagged “Lowest Margin”). Picking one updates the chart and closes the sheet.', render: (go) => home(go, undefined, { product: 'commodities', picker: 'commodities' }) },
    { id: 'fno-11', section: 'home', group: 'home', name: 'Contract picker · Equity', figma: '6754:65054', tab: true, note: 'The same sheet on its Equity tab: the 8 index contracts.', render: (go) => home(go, undefined, { product: 'commodities', picker: 'equity' }) },
    { id: 'fno-38', section: 'home', name: 'Commodity calendar (View all)', figma: '', badge: 'new', note: 'From View all on Expiring This Week (fno-08). All / Options / Futures / Events (flat tabs with icons, sticky; All merges them by day). Options rows: option chain (→ fno-17, back returns here) + ScalpPro; futures: ScalpPro only; events: no buttons. Days from today under a month section header (SectionHeader, content-primary): weekday over the date in one grey block (surface-secondary; today inverted (surface-inverted)), beside it one card with that day’s contracts — one day can hold several. A row is only the name with flat ScalpPro (→ fno-05) and open-contract (→ asset page fno-21) icon buttons. Back → Commodities home. Layout after the user’s reference (Expiry Calendar screenshot, 2026-11-17; no Figma frame yet).', render: (go) => <ExpiryTimeline onBack={() => go('fno-08')} onAsset={() => go('fno-21')} onOptionChain={() => { markMove('fno-17', 'forward'); go('fno-17') }} onScalper={() => openScalper(go)} /> },
    { id: 'fno-12', section: 'asset', group: 'lot', name: 'Gold Summary · by price', figma: '6754:65113', note: 'From a commodity shortcut on fno-08. Gold lot tabs (Gold, Gold Mini, Gold Guinea, Gold Ten, Gold Petal) in the Actionbar’s bottom slot; Futures (View all) and Options (View option chain, expiry month, category pills, Filter, sort). The sort opens a sheet: By Price · By Volume · Margin per lot.', render: (go) => <LotSummary onBack={() => go('fno-08')} onChain={() => go('fno-17')} onAsset={(illiquid) => go(illiquid ? 'fno-22' : 'fno-21')} onOrder={(side) => go(side === 'buy' ? 'fno-25' : 'fno-29')} /> },
    { id: 'fno-13', section: 'asset', group: 'lot', name: 'Gold Summary · by volume', figma: '6754:65288', note: 'Sorted by volume: each option shows its traded volume, no change.', render: (go) => <LotSummary sort="volume" onBack={() => go('fno-08')} onChain={() => go('fno-17')} onAsset={(illiquid) => go(illiquid ? 'fno-22' : 'fno-21')} onOrder={(side) => go(side === 'buy' ? 'fno-25' : 'fno-29')} /> },
    { id: 'fno-14', section: 'asset', group: 'lot', name: 'Gold Summary · margin per lot', figma: '6754:65444', note: 'Sorted by margin per lot: each option shows the margin for one lot, no change.', render: (go) => <LotSummary sort="margin" onBack={() => go('fno-08')} onChain={() => go('fno-17')} onAsset={(illiquid) => go(illiquid ? 'fno-22' : 'fno-21')} onOrder={(side) => go(side === 'buy' ? 'fno-25' : 'fno-29')} /> },
    { id: 'fno-15', section: 'home', group: 'home', name: 'Strategies · Equity', figma: '6754:64178', tab: true, note: 'The Strategies product tab with Equity selected in the pill group: shortcuts, Zing Trades, Smart Invest, Pre-build Strategies (Nifty 50 ⇕, Bullish / Bearish / Neutral / Volatile), Quick Trade. Card footer buttons stay Small (32) as in Figma.', render: (go) => home(go, undefined, { product: 'strategies', segment: 'equity' }) },
    { id: 'fno-16', section: 'home', group: 'home', name: 'Strategies · Commodities', figma: '6754:64607', tab: true, note: 'The same tab with Commodities selected: commodity Smart Invest baskets, GOLD as the underlying.', render: (go) => home(go, undefined, { product: 'strategies', segment: 'commodities' }) },
    { id: 'fno-17', section: 'chain', group: 'chain', name: 'Option chain', figma: '11630:16785', note: 'From Option chain on the F&O chart (any product tab), the Expiry calendar’s option-chain button or the Option Chain bottom-nav tab; Back → the page it was opened from (F&O home when opened directly). Opens scrolled to the spot pill. BankNifty ▾ and Expiry ▾ open sheets; Σ shows delta instead of the day change; the basket and Zing tile open the explanatory sheet. Column heads: Call / Put metric (LTP, OI, OI Chg, IV) and the strike range (All, ±5, ±10). Tap a price to Buy, tap it again to Sell, a third time to clear.', render: (go) => <OptionChain onBack={() => backOr(go, 'fno-01')} onAsset={() => go('fno-21')} /> },
    { id: 'fno-18', section: 'chain', group: 'chain', name: 'Option chain · Buy selected', figma: '11630:16184', note: 'A put price tapped once: B badge, green wash, the order dock with the contract, Balance / Req, quantity in lots and Buy (brand). Buy places a sample order (toast) and clears the selection.', render: (go) => <OptionChain initialSelection={{ strike: 25400, side: 'put', action: 'buy', ltp: 160.54 }} onBack={() => backOr(go, 'fno-01')} onAsset={() => go('fno-21')} /> },
    { id: 'fno-19', section: 'chain', group: 'chain', name: 'Option chain · Sell selected', figma: '11695:26269', note: 'The same put tapped again: S badge, red wash, Sell (secondary) in the dock; Req becomes the margin per lot.', render: (go) => <OptionChain initialSelection={{ strike: 25400, side: 'put', action: 'sell', ltp: 160.54 }} onBack={() => backOr(go, 'fno-01')} onAsset={() => go('fno-21')} /> },
    { id: 'fno-20', section: 'chain', group: 'chain', name: 'Option chain · illiquid contract', figma: '', note: 'Illiquid contracts (deep in-the-money calls, far out-of-the-money puts) carry a block icon beside the price, like Groww. Unlike Groww, a tap never selects them: a tooltip opens just above — “ILLIQUID contract” / “Can’t be traded” ⓘ; tapping away closes it, ⓘ opens a sheet with why it’s blocked, its traded lots and buy–sell gap, and a tip. Opens on the 25,700 put with the tooltip up.', render: (go) => <OptionChain initialIlliquid={{ strike: 25700, side: 'put' }} onBack={() => backOr(go, 'fno-01')} onAsset={() => go('fno-21')} /> },
    { id: 'fno-21', section: 'asset', group: 'asset', name: 'Asset page · Gold MINI', figma: '6754:61613', note: 'A commodity contract page. Entry (one of several): the contract name in the option chain order dock (“25,400 Put ›”). Back returns where it came from; Option chain → fno-17; Buy / Sell open the sample sheet. Equity contracts get their own (similar) page later.', render: (go) => <AssetPage asset={goldMiniAsset} onBack={() => backOr(go, 'fno-18')} onChain={() => go('fno-17')} onScalper={() => openScalper(go)} onOrder={(side) => go(side === 'buy' ? 'fno-25' : 'fno-29')} /> },
    { id: 'fno-22', section: 'asset', group: 'asset', name: 'Asset page · illiquid', figma: '6754:61613', note: 'Product rule (commodities only): an illiquid contract’s page shows the ILLIQUID tag next to its name and Buy / Sell greyed out, with “Trading is not allowed as this contract is illiquid” above them — whatever screen it was opened from.', render: (go) => <AssetPage asset={illiquidAsset} onBack={() => backOr(go, 'fno-17')} onChain={() => go('fno-17')} onScalper={() => openScalper(go)} onOrder={(side) => go(side === 'buy' ? 'fno-25' : 'fno-29')} /> },
    { id: 'fno-23', section: 'asset', group: 'lot', name: 'Gold Summary · Buy / Sell sheet', figma: '', note: 'Tapping any futures or option card opens the Buy / Sell sheet (live app, 2026-10-29): name › (asset page fno-21) · price, expiry · change, Buy (brand) / Sell (secondary).', render: (go) => <LotSummary initialSheet="lo-0" onBack={() => go('fno-08')} onChain={() => go('fno-17')} onAsset={(illiquid) => go(illiquid ? 'fno-22' : 'fno-21')} onOrder={(side) => go(side === 'buy' ? 'fno-25' : 'fno-29')} /> },
    { id: 'fno-24', section: 'asset', group: 'lot', name: 'Gold Summary · illiquid sheet', figma: '', note: 'Product rule (commodities): an illiquid contract carries the ILLIQUID tag on its card (edge case — illiquid contracts shouldn’t be listed, but the state is built) and in the sheet; Buy / Sell are greyed out with “Trading is not allowed as this contract is illiquid”. Only the name › (asset page fno-22) or tapping outside works.', render: (go) => <LotSummary initialSheet="lo-5" onBack={() => go('fno-08')} onChain={() => go('fno-17')} onAsset={(illiquid) => go(illiquid ? 'fno-22' : 'fno-21')} onOrder={(side) => go(side === 'buy' ? 'fno-25' : 'fno-29')} /> },
    { id: 'fno-25', section: 'order', group: 'order', name: 'Order pad · Buy · Market', figma: '8671:18433', note: 'Commodity option chain order pad (other order pads differ a little). From Buy on the commodity asset page or the Gold Summary Buy / Sell sheet. Delivery / Intraday tabs, Market / Limit / SL pills, Quantity (⇕ lots) in steps of one lot, Set TPSL, Avail. · Req, Buy. Placing shows a sample toast; no order is sent.', render: (go) => <OrderPad side="buy" onBack={() => backOr(go, 'fno-21')} /> },
    { id: 'fno-26', section: 'order', group: 'order', name: 'Order pad · Buy · Limit', figma: '8671:18433', note: 'Limit adds the validity (Day ⇕ → Day / IOC) and a limit price row with a % stepper from the market price.', render: (go) => <OrderPad side="buy" type="limit" onBack={() => backOr(go, 'fno-21')} /> },
    { id: 'fno-27', section: 'order', group: 'order', name: 'Order pad · Buy · SL', figma: '8671:18433', note: 'SL adds a trigger price row above the limit row.', render: (go) => <OrderPad side="buy" type="sl" onBack={() => backOr(go, 'fno-21')} /> },
    { id: 'fno-28', section: 'order', group: 'order', name: 'Order pad · Buy · Intraday', figma: '8671:18433', note: 'Intraday: “This position will auto close by 11:30 PM” above the dock.', render: (go) => <OrderPad side="buy" product="intraday" onBack={() => backOr(go, 'fno-21')} /> },
    { id: 'fno-29', section: 'order', group: 'order', name: 'Order pad · Sell · Market', figma: '8671:18433', note: 'Sell adds Margin · Leverage (grey strip) above the quantity; the action is Sell (red).', render: (go) => <OrderPad side="sell" onBack={() => backOr(go, 'fno-21')} /> },
    { id: 'fno-30', section: 'order', group: 'order', name: 'Order pad · Sell · SL', figma: '8671:18433', render: (go) => <OrderPad side="sell" type="sl" onBack={() => backOr(go, 'fno-21')} /> },
    { id: 'fno-31', section: 'order', group: 'order', name: 'Order pad · Sell · Intraday', figma: '8671:18433', render: (go) => <OrderPad side="sell" product="intraday" onBack={() => backOr(go, 'fno-21')} /> },
    { id: 'fno-32', section: 'order', group: 'order', name: 'Order pad · Buy · ILLIQUID (edge case)', figma: '8671:18433 + product rule', note: 'Should never be reached — every entry point blocks illiquid contracts — but if one slips through: ILLIQUID tag in the header (tap → “What does illiquidity mean?”), the blocked note in the dock (tap → same sheet) and Buy disabled. Inputs stay usable.', render: (go) => <OrderPad side="buy" illiquid onBack={() => backOr(go, 'fno-21')} /> },
    { id: 'fno-33', section: 'order', group: 'order', name: 'Order pad · Sell · ILLIQUID (edge case)', figma: '8671:18433 + product rule', note: 'The same edge case on the Sell side: Sell disabled.', render: (go) => <OrderPad side="sell" illiquid onBack={() => backOr(go, 'fno-21')} /> },
  ],
}
```

### `src/flows/fno/option-chain/components/OrderDock.module.css`

```css
/* Option chain order dock (Figma 11630:16715) on L3 tokens. */
.dock { background: var(--l3-surface-primary); box-shadow: var(--l3-shadow-elevation-high); }
.header { display: flex; align-items: center; gap: var(--l3-spacing-04); height: var(--app-size-chain-dock-header); padding-inline: var(--l3-spacing-16) var(--l3-spacing-08); border-bottom: 1px solid var(--l3-border-light); }
/* A wash of the action's colour from the left edge (Figma: green-50 → white by 30%). */
.header[data-action='buy'] { background: linear-gradient(90deg, var(--l3-surface-accent-indicator-up-light), var(--l3-surface-primary) 30%); }
.header[data-action='sell'] { background: linear-gradient(90deg, var(--l3-surface-accent-indicator-down-light), var(--l3-surface-primary) 30%); }
.badge { display: inline-grid; place-items: center; flex: none; min-width: var(--l3-size-16); height: var(--l3-size-16); padding-inline: var(--l3-spacing-04); border-radius: var(--l3-radius-04); font: var(--l3-text-heading-10); color: var(--l3-content-inverted); }
.badge[data-action='buy'] { background: var(--l3-surface-accent-indicator-up-default); }
.badge[data-action='sell'] { background: var(--l3-surface-accent-indicator-down-default); }
.contract.contract { font: var(--l3-text-heading-14); margin-right: auto; }
.options.options { font: var(--l3-text-label-12); }
.bullet { color: var(--l3-content-tertiary); }
.body { display: flex; flex-direction: column; gap: var(--l3-spacing-16); padding: var(--l3-spacing-12) var(--l3-spacing-16) var(--l3-spacing-16); }
.funds { display: flex; justify-content: space-between; font: var(--l3-text-label-12); }
.funds strong { font: var(--l3-text-heading-12); }
.muted { color: var(--l3-content-tertiary); }
.underline { text-decoration: underline; }
.actions { display: grid; grid-template-columns: 1fr 1fr; gap: var(--l3-spacing-16); align-items: center; }
/* The quantity sits in a 48-tall bordered box (Figma 11630:16746): − and + at the ends (28 circles), value + lots between. */
.stepperBox { display: flex; align-items: center; height: var(--l3-size-48); padding: var(--l3-spacing-06) var(--l3-spacing-08); border: 1px solid var(--l3-border-light); border-radius: var(--l3-radius-12); }
.stepperBox > * { flex: 1; justify-content: space-between; }
.stepperBox button { width: var(--l3-size-28); height: var(--l3-size-28); }
```

### `src/flows/fno/option-chain/components/OrderDock.tsx`

```tsx
import { useState } from 'react'
import { Button } from '@l3/components/Button'
import { Icon } from '@l3/components/Icon'
import { Stepper } from '@l3/components/Stepper'
import { msChevronRight } from '@l3/icons/material'
import { inr } from '../../../../shared/data/format'
import { t } from '../../copy'
import { balance, sellMarginPerLot, type Action, type Side } from '../data'
import styles from './OrderDock.module.css'

/** The contract picked in the chain and whether it's a buy or a sell. */
export type Selection = { strike: number; side: Side; action: Action; ltp: number }

type Props = { selection: Selection; lotSize: number; onContract: () => void; onOptions: () => void; onPlace: (action: Action) => void }

/**
 * Order dock (Figma 11630:16715): B / S badge + contract (opens its details) · Set Limit • TP/SL; Balance and the funds
 * this order needs (buy = premium × quantity, sell = margin per lot); quantity in lots (L3 Stepper) and Buy (brand) or
 * Sell (secondary). The header carries a wash of the action's colour from the left.
 */
export function OrderDock({ selection, lotSize, onContract, onOptions, onPlace }: Props) {
  const [quantity, setQuantity] = useState(lotSize)
  const lots = quantity / lotSize
  const required = selection.action === 'buy' ? selection.ltp * quantity : sellMarginPerLot * lots
  const contract = t('chain.contract', { strike: selection.strike.toLocaleString('en-IN'), side: t(`chain.${selection.side}`) })
  return <div className={styles.dock} data-surface="primary">
    <div className={styles.header} data-action={selection.action}>
      <span className={styles.badge} data-action={selection.action} aria-hidden>{t(selection.action === 'buy' ? 'chain.buyBadge' : 'chain.sellBadge')}</span>
      <Button variant="ghost" size="sm" iconRight={<Icon icon={msChevronRight} size={16} />} onClick={onContract} className={styles.contract}>{contract}</Button>
      <Button variant="ghost" size="sm" iconRight={<Icon icon={msChevronRight} size={16} />} onClick={onOptions} className={styles.options}>{t('chain.orderOptions')} <span className={styles.bullet} aria-hidden>•</span> {t('chain.tpsl')}</Button>
    </div>
    <div className={styles.body}>
      <div className={styles.funds}>
        <span><span className={styles.muted}>{t('chain.balance')}</span> <strong>{inr(balance, 0)}</strong></span>
        <span><span className={[styles.muted, styles.underline].join(' ')}>{t('chain.req')}</span> <strong>{inr(required, 0)}</strong></span>
      </div>
      <div className={styles.actions}>
        <div className={styles.stepperBox}><Stepper label={t('chain.quantity')} value={quantity} onChange={setQuantity} min={lotSize} step={lotSize} size="lg" fullWidth sublabel={lots === 1 ? t('chain.lot') : t('chain.lots', { count: lots })} /></div>
        <Button variant={selection.action === 'buy' ? 'brand' : 'secondary'} size="lg" fullWidth onClick={() => onPlace(selection.action)}>{t(selection.action === 'buy' ? 'chain.buy' : 'chain.sell')}</Button>
      </div>
    </div>
  </div>
}
```

### `src/flows/fno/option-chain/data.ts`

```ts
/**
 * Option chain sample (Figma 11695:26269). Illustrative prototype data, not live quotes: strikes 100 apart around the
 * spot, call premiums falling and put premiums rising with the strike, open interest peaking near the support /
 * resistance strikes.
 */

export type Side = 'call' | 'put'
export type Action = 'buy' | 'sell'
/** What the LTP columns show (the column header switch). */
export type Metric = 'ltp' | 'oi' | 'oiChange' | 'iv'

export type OptionQuote = {
  /** Last traded price, ₹. */
  ltp: number
  /** Day change, percent. */
  change: number
  /** Open interest, contracts. */
  oi: number
  /** Change in open interest today, percent. */
  oiChange: number
  /** Implied volatility, percent. */
  iv: number
  /**
   * Too few trades to deal in safely — the app blocks orders in it (Groww shows a ⃠ icon and lets you pick it; Lemonn
   * shows the icon and a tooltip instead of selecting it). Deep in-the-money calls and far out-of-the-money puts here.
   */
  illiquid?: boolean
  /** Lots traded today. */
  volume: number
  /** Gap between the best buy and sell price, as a percent of the price. */
  spread: number
}
export type StrikeRow = { strike: number; call: OptionQuote; put: OptionQuote }

export type Underlying = { id: string; name: string; spot: number; change: number; lotSize: number; maxPain: number; pcr: number; atmIv: number }
export const underlyings: Underlying[] = [
  { id: 'banknifty', name: 'BankNifty', spot: 25300.4, change: 5.56, lotSize: 35, maxPain: 25400, pcr: 0.68, atmIv: 26.1 },
  { id: 'nifty', name: 'Nifty 50', spot: 25300.4, change: 0.42, lotSize: 75, maxPain: 25300, pcr: 0.92, atmIv: 12.4 },
  { id: 'finnifty', name: 'FinNifty', spot: 25300.4, change: -0.31, lotSize: 65, maxPain: 25200, pcr: 1.08, atmIv: 14.8 },
  { id: 'sensex', name: 'Sensex', spot: 25300.4, change: 0.35, lotSize: 20, maxPain: 25400, pcr: 0.81, atmIv: 13.2 },
]
export const expiries = ['09 Oct', '16 Oct', '23 Oct', '30 Oct', '27 Nov']
/** The strike-range choice (column header "All"): every strike, or N strikes either side of the spot. */
export const ranges = [0, 5, 10] as const
export type Range = (typeof ranges)[number]

/** Call OI peaks at the resistance strike above the spot; put OI at the support strike below it (lakh contracts). */
const callOi = [8, 9, 11, 14, 18, 26, 31, 35, 58, 24, 19, 12, 9]
const putOi = [14, 21, 28, 33, 54, 38, 22, 16, 11, 8, 6, 5, 4]

export function chainFor(underlying: Underlying): StrikeRow[] {
  return Array.from({ length: 13 }, (_, i) => {
    const strike = 24700 + i * 100
    const callIntrinsic = Math.max(underlying.spot - strike, 0)
    const putIntrinsic = Math.max(strike - underlying.spot, 0)
    const time = 160 * Math.exp(-Math.abs(strike - underlying.spot) / 420)
    return {
      strike,
      call: { ltp: round(callIntrinsic + time), change: round(19 - i * 2.6), oi: callOi[i] * 100000, oiChange: round(4 + (i % 4) * 3.1), iv: round(underlying.atmIv + Math.abs(i - 6) * 0.6), illiquid: i < 3, volume: i < 3 ? 4 + i * 3 : 1800 + i * 240, spread: i < 3 ? round(9.4 - i * 1.7) : round(0.4 + Math.abs(i - 6) * 0.08) },
      put: { ltp: round(putIntrinsic + time * 0.9), change: round(-45.68 + i * 4.2), oi: putOi[i] * 100000, oiChange: round(-2 + (i % 3) * 2.4), iv: round(underlying.atmIv + Math.abs(i - 6) * 0.7), illiquid: i > 9, volume: i > 9 ? 3 + (12 - i) * 4 : 2100 - i * 90, spread: i > 9 ? round(7.8 + (i - 10) * 1.9) : round(0.5 + Math.abs(i - 6) * 0.09) },
    }
  })
}

const round = (n: number) => Math.round(n * 100) / 100

/** Funds shown in the order panel (sample account). */
export const balance = 10000
/** Margin to sell one lot (sample) — selling an option blocks margin, buying pays the premium. */
export const sellMarginPerLot = 1250
```

### `src/flows/fno/option-chain/screens/OptionChain.module.css`

```css
/* Option chain (Figma 11695:26269) — flow-only layout on L3 tokens. */

/* ---- Top: back · ribbon "Option chain" · Add more strategies; selectors; stats; column heads ---- */
.top { flex: none; background: var(--l3-surface-secondary); }
/* The ribbon's baseline runs the full width under the header; the selected tab's fill covers it under itself. */
.header { display: flex; align-items: flex-end; height: var(--l3-size-48); padding-left: var(--l3-spacing-06); box-shadow: inset 0 -1px 0 var(--l3-border-intense); }
.back.back { align-self: center; margin-top: var(--l3-spacing-04); }
.ribbon.ribbon { flex: none; padding-inline: var(--l3-spacing-12) var(--l3-spacing-16); background: transparent; box-shadow: none; }
/* Figma: the selected tab is white with a light outline, no flares, so it opens into the white selector row. */
.ribbon.ribbon [role='tab'][aria-selected='true'] { --tab-surface: var(--l3-surface-default); --tab-border: var(--l3-border-light); --tab-font: var(--l3-text-label-12); }
.ribbon.ribbon [role='tab'][aria-selected='true']::before { display: none; }
.addStrategies { display: inline-flex; align-items: center; gap: var(--l3-spacing-06); align-self: center; margin-top: var(--l3-spacing-04); padding: 0; border: 0; background: none; color: var(--l3-content-secondary); font: var(--l3-text-label-12); cursor: pointer; }
.addRing { display: grid; place-items: center; width: var(--l3-size-16); height: var(--l3-size-16); border-radius: var(--l3-radius-full); box-shadow: inset 0 0 0 1px var(--l3-border-dark); color: var(--l3-content-primary); }

.selectors { display: flex; align-items: center; gap: var(--l3-spacing-12); height: var(--l3-size-48); padding-left: var(--l3-spacing-12); background: var(--l3-surface-default); border-bottom: 1px dashed var(--l3-border-light); }
.vDivider { flex: none; align-self: center; width: 1px; height: var(--l3-size-20); background: var(--l3-border-light); }
.muted { color: var(--l3-content-tertiary); }
/* Zing signals: honey tile at the right edge, open on the right, with the signal count. */
.zing { position: relative; display: grid; place-items: center; margin-left: auto; width: var(--l3-spacing-36); height: var(--l3-size-32); padding: 0; border: 1px solid var(--l3-border-accent-zing-default); border-right: 0; border-radius: var(--l3-radius-08) 0 0 var(--l3-radius-08); background: var(--l3-surface-accent-zing-light); color: var(--l3-content-accent-zing-default); cursor: pointer; }
.zingCount { position: absolute; top: calc(-1 * var(--l3-spacing-04)); right: var(--l3-spacing-04); }

.stats { display: flex; align-items: center; gap: var(--l3-spacing-12); height: var(--l3-size-40); padding-inline: var(--l3-spacing-12); background: var(--l3-surface-default); border-bottom: 1px solid var(--l3-border-intense); overflow-x: auto; scrollbar-width: none; white-space: nowrap; }
/* Σ and basket (Figma 28 × 28, radius 9 → L3 08, border #dbdbdb = border/intense). */
.statButton.statButton { flex: none; width: var(--l3-size-28); height: var(--l3-size-28); min-width: var(--l3-size-28); min-height: var(--l3-size-28); padding: 0; --btn-radius: var(--l3-radius-08); --btn-border: var(--l3-border-intense); --btn-surface: var(--l3-surface-primary); }
.statOn.statOn { --btn-surface: var(--l3-surface-inverted); --btn-content: var(--l3-content-inverted); }
.stat { flex: none; font: var(--l3-text-label-10); }
.stat strong { font: var(--l3-text-heading-10); }
.dot { flex: none; width: var(--l3-size-04); height: var(--l3-size-04); border-radius: var(--l3-radius-full); background: var(--l3-content-disabled); }

.columns, .row { display: grid; grid-template-columns: 1fr var(--app-size-chain-strike) 1fr; }
.columns { height: var(--l3-size-40); background: var(--l3-surface-default); border-bottom: 1px solid var(--l3-border-light); }
.columnHead { padding: 0 var(--l3-spacing-16); border: 0; background: none; color: var(--l3-content-secondary); font: var(--l3-text-label-12); text-align: left; cursor: pointer; }
.strikeHead { text-align: center; background: var(--l3-surface-secondary); }
.putHead { text-align: right; }

/* ---- Rows ---- */
.row { position: relative; height: var(--app-size-chain-row); border-bottom: 1px solid var(--l3-border-light); }
.strike { background: var(--l3-surface-secondary); display: flex; flex-direction: column; align-items: center; justify-content: center; gap: var(--l3-spacing-02); }
.strikeValue { font: var(--l3-text-heading-12); }

.cell { position: relative; display: flex; align-items: center; gap: var(--l3-spacing-08); padding: 0 var(--l3-spacing-16); border: 0; background: none; color: var(--l3-content-primary); text-align: left; cursor: pointer; }
.cell[data-side='put'] { justify-content: flex-end; text-align: right; }
.cell[data-side='call'] { flex-direction: row-reverse; justify-content: flex-end; }
.values { display: flex; flex-direction: column; gap: var(--l3-spacing-02); }
.ltp { font: var(--l3-text-label-12); }
.sub { font: var(--l3-text-label-10); }
.up { color: var(--l3-content-accent-indicator-up-default); }
.down { color: var(--l3-content-accent-indicator-down-default); }
.subNeutral { color: var(--l3-content-tertiary); }

/* Selected: a B / S badge on the strike side and a wash of the action's colour from the outer edge. */
.badge { position: absolute; top: 50%; translate: 0 -50%; display: grid; place-items: center; min-width: var(--l3-size-16); height: var(--l3-size-16); border-radius: var(--l3-radius-04); font: var(--l3-text-heading-10); color: var(--l3-content-inverted); }
.cell[data-side='put'] .badge { left: 0; }
.cell[data-side='call'] .badge { right: 0; }
.badge[data-action='buy'] { background: var(--l3-surface-accent-indicator-up-default); }
.badge[data-action='sell'] { background: var(--l3-surface-accent-indicator-down-default); }
.cell[data-side='put'][data-selected='buy'] { background: linear-gradient(90deg, transparent, var(--l3-surface-accent-indicator-up-light)); }
.cell[data-side='put'][data-selected='sell'] { background: linear-gradient(90deg, transparent, var(--l3-surface-accent-indicator-down-light)); }
.cell[data-side='call'][data-selected='buy'] { background: linear-gradient(270deg, transparent, var(--l3-surface-accent-indicator-up-light)); }
.cell[data-side='call'][data-selected='sell'] { background: linear-gradient(270deg, transparent, var(--l3-surface-accent-indicator-down-light)); }

/* OI bars on the row's bottom edge: call OI (red) runs left from the middle, put OI (green) right. */
.oi { position: absolute; left: 0; right: 0; bottom: -1px; height: 2px; pointer-events: none; }
.oiCall, .oiPut { position: absolute; bottom: 0; height: 100%; }
/* Each bar fades out toward the middle (Figma). */
.oiCall { right: 50%; background: linear-gradient(90deg, var(--l3-surface-accent-indicator-down-default) 60%, transparent); }
.oiPut { left: 50%; background: linear-gradient(90deg, transparent, var(--l3-surface-accent-indicator-up-default) 40%); }

/* Spot: a thin band between the two strikes the price falls between, with the price pill in the middle. */
.spotRow { position: relative; display: grid; place-items: center; height: var(--l3-size-32); border-bottom: 1px solid var(--l3-border-light); background: var(--l3-surface-default); }
.spot { padding: var(--l3-spacing-06) var(--l3-spacing-12); border-radius: var(--l3-radius-08); background: var(--l3-surface-inverted); color: var(--l3-content-inverted); font: var(--l3-text-label-12); white-space: nowrap; box-shadow: var(--l3-shadow-elevation-high); }
.spotUp { color: var(--l3-content-accent-indicator-up-default); }
.spotDown { color: var(--l3-content-accent-indicator-down-default); }

/* Illiquid contracts: a block icon beside the price (strike side); a tap shows the tooltip above instead of selecting. */
.illiquidCell { position: relative; display: grid; }
/* An invisible box over the ⃠ icon: the tooltip's anchor, so its arrow points at the icon. */
.tipTarget { position: absolute; display: block; pointer-events: none; }
.tipTarget > * { display: block; width: 100%; height: 100%; pointer-events: auto; }
.tipDot { display: block; width: 100%; height: 100%; }
.blocked { display: inline-flex; vertical-align: -2px; margin-inline: var(--l3-spacing-04); color: var(--l3-content-tertiary); }
.cell[data-illiquid] .ltp { color: var(--l3-content-secondary); }
.tip { display: inline-flex; align-items: center; gap: var(--l3-spacing-12); white-space: nowrap; }
/* Two lines: the label, then a secondary line under it. */
.tipText { display: flex; flex-direction: column; gap: var(--l3-spacing-02); }
.tipTitle { font: var(--l3-text-label-12); color: var(--l3-content-inverted); }
.tipSub { font: var(--l3-text-description-12); color: var(--l3-content-inverted-secondary); }
.tipInfo { position: relative; margin-right: calc(-1 * var(--l3-spacing-04)); display: inline-grid; place-items: center; width: var(--l3-size-16); height: var(--l3-size-16); padding: 0; border: 0; background: none; color: inherit; cursor: pointer; }
/* The icon sits 8 from the bubble edge (like L3 Tooltip ✕: it steps out of the text's 4 inline padding); its touch area stays larger than the 16 icon. */
.tipInfo::before { content: ''; position: absolute; inset: calc(-1 * var(--l3-spacing-08)); }

/* The illiquid tooltip grows out of its arrow (at the icon): fade + scale + a 4 px slide away from the icon, once placed. */
.tipTarget [role='tooltip'][data-ready] { animation: chain-tip-in var(--l3-motion-duration-medium) var(--l3-motion-easing-decelerate) both; }
.tipTarget [role='tooltip'][data-side='top'] { transform-origin: var(--tt-arrow) 100%; --tip-from: var(--l3-spacing-04); }
.tipTarget [role='tooltip'][data-side='bottom'] { transform-origin: var(--tt-arrow) 0; --tip-from: calc(-1 * var(--l3-spacing-04)); }
@keyframes chain-tip-in { from { opacity: 0; scale: 0.9; translate: 0 var(--tip-from); } }
@media (prefers-reduced-motion: reduce) { .tipTarget [role='tooltip'][data-ready] { animation: none; } }
```

### `src/flows/fno/option-chain/screens/OptionChain.tsx`

```tsx
import { Fragment, useEffect, useLayoutEffect, useMemo, useRef, useState, type CSSProperties, type ReactNode } from 'react'
import { Aerobar } from '@l3/components/Aerobar'
import { Badge } from '@l3/components/Badge'
import { Button } from '@l3/components/Button'
import { Icon } from '@l3/components/Icon'
import { Select } from '@l3/components/Select'
import { Tabs } from '@l3/components/Tabs'
import { Tag } from '@l3/components/Tag'
import { Tooltip } from '@l3/components/Tooltip'
import { msAdd, msArrowBack, msBlock, msBoltFill, msFunctions, msInfo, msShoppingBasket } from '@l3/icons/material'
import { Screen } from '../../../../shared/ui/Screen'
import { ChoiceSheet, DetailSheet } from '../../sheets/HomeSheets'
import { t } from '../../copy'
import { chainFor, expiries, ranges, underlyings, type Action, type Metric, type OptionQuote, type Range, type Side } from '../data'
import { OrderDock, type Selection } from '../components/OrderDock'
import { IlliquidSheet } from '../../sheets/IlliquidSheet'
import styles from './OptionChain.module.css'
import flat from '../../flatCards.module.css'

type Modal = { kind: 'choice'; title: string; values: string[]; value: string; onPick: (v: string) => void } | { kind: 'detail'; title: string } | { kind: 'illiquid'; contract: string; quote: OptionQuote }

type Props = {
  /** Open with a contract already selected (fno-18 Buy, fno-19 Sell). */
  initialSelection?: Selection
  /** Open with the illiquid tooltip up on this contract (fno-20). */
  initialIlliquid?: { strike: number; side: Side }
  onBack: () => void
  /** The contract name in the order dock opens its asset page. */
  onAsset: () => void
}

/** How long the illiquid tooltip stays up. */
const TIP_MS = 5000
const metrics: Metric[] = ['ltp', 'oi', 'oiChange', 'iv']
const lakh = (n: number) => `${(n / 100000).toFixed(1)}L`

/**
 * Option chain (Figma 11695:26269 — 11630:16785 default, 11630:16184 Buy; Sell is the same frame with S). Strikes run
 * low → high down the page, calls left, puts right; the spot pill sits between the two strikes it falls between and the
 * chain opens scrolled to it. A price tap selects that contract to Buy, a second tap on it switches to Sell, a third
 * clears it; the order dock rises while a contract is selected.
 */
export function OptionChain({ initialSelection, initialIlliquid, onBack, onAsset }: Props) {
  const [underlyingId, setUnderlyingId] = useState(underlyings[0].id)
  const [expiry, setExpiry] = useState(expiries[0])
  const [metric, setMetric] = useState<Metric>('ltp')
  const [range, setRange] = useState<Range>(0)
  const [greeks, setGreeks] = useState(false)
  const [selection, setSelection] = useState<Selection | null>(initialSelection ?? null)
  // The illiquid contract whose tooltip is up ("25,700 put"); an illiquid tap shows it instead of selecting.
  const [tip, setTip] = useState<string | null>(initialIlliquid ? `${initialIlliquid.strike}-${initialIlliquid.side}` : null)
  // The tooltip goes away by itself after 5 s (or when another contract is tapped).
  useEffect(() => {
    if (!tip) return
    const timer = window.setTimeout(() => setTip(null), TIP_MS)
    return () => window.clearTimeout(timer)
  }, [tip])
  const [modal, setModal] = useState<Modal | null>(null)
  const [placed, setPlaced] = useState<string | null>(null)
  const underlying = underlyings.find((u) => u.id === underlyingId)!
  const allRows = useMemo(() => chainFor(underlying), [underlying])
  const spotIndex = allRows.findIndex((row) => row.strike > underlying.spot)
  const rows = range === 0 ? allRows : allRows.slice(Math.max(0, spotIndex - range), spotIndex + range)
  const maxOi = Math.max(...allRows.flatMap((r) => [r.call.oi, r.put.oi]))
  const below = allRows.filter((r) => r.strike < underlying.spot)
  const above = allRows.filter((r) => r.strike > underlying.spot)
  const support = below.reduce((a, b) => (b.put.oi > a.put.oi ? b : a)).strike
  const resistance = above.reduce((a, b) => (b.call.oi > a.call.oi ? b : a)).strike

  // Open at the money: the spot pill in the middle of the list.
  const spotRef = useRef<HTMLDivElement>(null)
  useLayoutEffect(() => {
    const spot = spotRef.current
    const body = spot?.closest('[data-chain]')?.parentElement
    if (spot && body) body.scrollTop += spot.getBoundingClientRect().top - body.getBoundingClientRect().top - body.clientHeight / 2
  }, [underlyingId, range])

  const choose = (title: string, values: string[], value: string, onPick: (v: string) => void) => setModal({ kind: 'choice', title, values, value, onPick })
  const tap = (strike: number, side: Side, quote: OptionQuote) => { setTip(null); setSelection((current) => {
    const same = current?.strike === strike && current.side === side
    if (!same) return { strike, side, action: 'buy', ltp: quote.ltp }
    return current.action === 'buy' ? { ...current, action: 'sell' } : null
  }) }
  const value = (quote: OptionQuote) => metric === 'ltp' ? quote.ltp.toFixed(2) : metric === 'oi' ? lakh(quote.oi) : metric === 'oiChange' ? `${quote.oiChange}%` : quote.iv.toFixed(2)
  const sub = (quote: OptionQuote, side: Side, strike: number) => {
    if (greeks) {
      const delta = side === 'call' ? Math.max(0.02, Math.min(0.98, 0.5 + (underlying.spot - strike) / 1200)) : -Math.max(0.02, Math.min(0.98, 0.5 - (underlying.spot - strike) / 1200))
      return { text: `Δ ${delta.toFixed(2)}`, tone: styles.subNeutral }
    }
    return { text: `${quote.change}%`, tone: quote.change < 0 ? styles.down : styles.up }
  }
  const tagFor = (strike: number) => strike === support ? <Tag color="profit" variant="primary" size="sm">{t('chain.tag.support')}</Tag> : strike === resistance ? <Tag color="loss" variant="primary" size="sm">{t('chain.tag.resistance')}</Tag> : strike === underlying.maxPain ? <Tag color="discover" variant="primary" size="sm">{t('chain.tag.maxPain')}</Tag> : null

  const cell = (strike: number, side: Side, quote: OptionQuote) => {
    const selected = selection?.strike === strike && selection.side === side ? selection.action : undefined
    const s = sub(quote, side, strike)
    const contract = t('chain.contract', { strike: strike.toLocaleString('en-IN'), side: t(`chain.${side}`) })
    // Illiquid: the block icon sits beside the price on the strike side; the price never selects.
    const blocked = quote.illiquid ? <span className={styles.blocked} data-blocked aria-hidden><Icon icon={msBlock} size={14} /></span> : null
    const price = <span className={styles.ltp}>{side === 'put' && blocked}{value(quote)}{side === 'call' && blocked}</span>
    const content = <span className={styles.values}>{price}<span className={[styles.sub, s.tone].join(' ')}>{s.text}</span></span>
    if (quote.illiquid) {
      const key = `${strike}-${side}`
      return <IlliquidCell open={tip === key} onToggle={(open) => setTip(open ? key : null)}
        label={t('chain.illiquidLabel', { strike: strike.toLocaleString('en-IN'), side: t(`chain.${side}`) })} side={side}
        onMore={() => { setTip(null); setModal({ kind: 'illiquid', contract, quote }) }}>{content}</IlliquidCell>
    }
    return <button type="button" className={styles.cell} data-side={side} data-selected={selected} aria-pressed={!!selected}
      aria-label={t('chain.select', { action: t(selected === 'buy' ? 'chain.sell' : 'chain.buy'), strike: strike.toLocaleString('en-IN'), side: t(`chain.${side}`), price: quote.ltp.toFixed(2) })}
      onClick={() => tap(strike, side, quote)}>
      {selected && <span className={styles.badge} data-action={selected} aria-hidden>{t(selected === 'buy' ? 'chain.buyBadge' : 'chain.sellBadge')}</span>}
      {content}
    </button>
  }

  const sheet = modal?.kind === 'choice' ? <ChoiceSheet {...modal} onClose={() => setModal(null)} /> : modal?.kind === 'detail' ? <DetailSheet title={modal.title} onClose={() => setModal(null)} /> : modal?.kind === 'illiquid' ? <IlliquidSheet contract={modal.contract} onClose={() => setModal(null)} /> : undefined
  const top = <div className={styles.top}>
    <div className={styles.header}>
      <Button variant="ghost" size="sm" iconLeft={<Icon icon={msArrowBack} />} aria-label={t('chain.back')} onClick={onBack} className={styles.back} />
      <Tabs aria-label={t('chain.tabs')} appearance="ribbon" size="sm" value="chain" onChange={() => {}} items={[{ value: 'chain', label: t('chain.title') }]} className={styles.ribbon} />
      <button type="button" className={styles.addStrategies} onClick={() => setModal({ kind: 'detail', title: t('chain.addStrategies') })}>
        {t('chain.addStrategies')}<span className={styles.addRing} aria-hidden><Icon icon={msAdd} size={12} /></span>
      </button>
    </div>
    <div className={styles.selectors}>
      <Select size="sm" icon="chevron" aria-label={t('chain.underlying')} onClick={() => choose(t('chain.underlying'), underlyings.map((u) => u.name), underlying.name, (name) => { setUnderlyingId(underlyings.find((u) => u.name === name)!.id); setSelection(null) })}>{underlying.name}</Select>
      <span className={styles.vDivider} aria-hidden />
      <Select size="sm" icon="chevron" aria-label={t('chain.expiryTitle')} onClick={() => choose(t('chain.expiryTitle'), expiries, expiry, (e) => { setExpiry(e); setSelection(null) })}><span className={styles.muted}>{t('chain.expiry')}</span> {expiry}</Select>
      <button type="button" className={styles.zing} aria-label={t('chain.signals', { count: 2 })} onClick={() => setModal({ kind: 'detail', title: t('signals') })}>
        <Icon icon={msBoltFill} size={20} /><Badge count={2} size="sm" className={styles.zingCount} />
      </button>
    </div>
    <div className={styles.stats}>
      <Button variant="secondary" size="sm" aria-label={t('chain.greeks')} aria-pressed={greeks} iconLeft={<Icon icon={msFunctions} size={16} />} onClick={() => setGreeks(!greeks)} className={[styles.statButton, greeks && styles.statOn].filter(Boolean).join(' ')} />
      <Button variant="secondary" size="sm" aria-label={t('chain.basket')} iconLeft={<Icon icon={msShoppingBasket} size={16} />} onClick={() => setModal({ kind: 'detail', title: t('chain.basket') })} className={styles.statButton} />
      <span className={styles.vDivider} aria-hidden />
      <span className={styles.stat}><span className={styles.muted}>{t('chain.pcr')}</span> <strong>{underlying.pcr}</strong></span><span className={styles.dot} aria-hidden />
      <span className={styles.stat}><span className={styles.muted}>{t('chain.maxPain')}</span> <strong>{underlying.maxPain.toLocaleString('en-IN')}</strong></span><span className={styles.dot} aria-hidden />
      <span className={styles.stat}><span className={styles.muted}>{t('chain.atmIv')}</span> <strong>{underlying.atmIv.toFixed(2)}</strong></span>
    </div>
    <div className={styles.columns}>
      <button type="button" className={styles.columnHead} onClick={() => choose(t('chain.metricTitle'), metrics.map((m) => t(`chain.metric.${m}`)), t(`chain.metric.${metric}`), (label) => setMetric(metrics.find((m) => t(`chain.metric.${m}`) === label)!))}>{t('chain.call')} {t(`chain.metric.${metric}`)}</button>
      <button type="button" className={[styles.columnHead, styles.strikeHead].join(' ')} onClick={() => choose(t('chain.rangeTitle'), ranges.map((r) => t(`chain.rangeOption.${r}`)), t(`chain.rangeOption.${range}`), (label) => setRange(ranges.find((r) => t(`chain.rangeOption.${r}`) === label)!))}>{t(`chain.range.${range}`)}</button>
      <button type="button" className={[styles.columnHead, styles.putHead].join(' ')} onClick={() => choose(t('chain.metricTitle'), metrics.map((m) => t(`chain.metric.${m}`)), t(`chain.metric.${metric}`), (label) => setMetric(metrics.find((m) => t(`chain.metric.${m}`) === label)!))}>{t('chain.put')} {t(`chain.metric.${metric}`)}</button>
    </div>
  </div>

  return <Screen className={flat.flatCards} top={top} sheet={sheet}
    bottom={selection ? <OrderDock key={`${selection.strike}-${selection.side}`} selection={selection} lotSize={underlying.lotSize} onContract={onAsset} onOptions={() => setModal({ kind: 'detail', title: `${t('chain.orderOptions')} · ${t('chain.tpsl')}` })} onPlace={(action: Action) => { setPlaced(t('chain.placed', { action: t(action === 'buy' ? 'chain.buy' : 'chain.sell'), contract: t('chain.contract', { strike: selection.strike.toLocaleString('en-IN'), side: t(`chain.${selection.side}`) }) })); setSelection(null) }} /> : undefined}
    toast={placed ? <Aerobar floating type="success" heading={placed} onDismiss={() => setPlaced(null)} /> : undefined}>
    <div className={styles.chain} data-chain role="list" aria-label={t('chain.title')}>
      {rows.map((row, i) => {
        const spotHere = rows[i - 1] && rows[i - 1].strike < underlying.spot && row.strike > underlying.spot
        const tag = tagFor(row.strike)
        return <Fragment key={row.strike}>
          {spotHere && <div ref={spotRef} className={styles.spotRow} role="listitem" aria-label={t('chain.spot')}><span className={styles.spot}>{underlying.spot.toFixed(2)} <span className={underlying.change < 0 ? styles.spotDown : styles.spotUp}>{underlying.change > 0 ? '+' : ''}{underlying.change}%</span></span></div>}
          <div className={styles.row} role="listitem" data-itm={row.strike < underlying.spot ? 'call' : 'put'}>
            {cell(row.strike, 'call', row.call)}
            <div className={styles.strike}><span className={styles.strikeValue}>{row.strike}</span>{tag}</div>
            {cell(row.strike, 'put', row.put)}
            <span className={styles.oi} aria-label={t('chain.oiLegend', { call: lakh(row.call.oi), put: lakh(row.put.oi) })}>
              <span className={styles.oiCall} style={{ width: `${(row.call.oi / maxOi) * 50}%` }} />
              <span className={styles.oiPut} style={{ width: `${(row.put.oi / maxOi) * 50}%` }} />
            </span>
          </div>
        </Fragment>
      })}
    </div>
  </Screen>
}

/**
 * An illiquid price cell: the whole cell is the tap target, but the tooltip points at the ⃠ icon so the icon reads as
 * “illiquid”. The L3 Tooltip anchors on an invisible box laid over the icon (outside the cell's button, so the ⓘ button
 * in the tooltip isn't nested in another button). Mobile: it opens only on a tap — never hover or focus — and closes on
 * a second tap, tap-away, after 5 s, or when another contract is tapped (the screen's timer).
 */
function IlliquidCell({ open, onToggle, onMore, label, side, children }: { open: boolean; onToggle: (open: boolean) => void; onMore: () => void; label: string; side: Side; children: ReactNode }) {
  const wrap = useRef<HTMLDivElement>(null)
  const wasOpen = useRef(false)
  const [target, setTarget] = useState<CSSProperties | null>(null)
  // Measure the icon first, then mount the tooltip on the box over it — the L3 Tooltip places itself when it opens,
  // so its anchor must already sit on the icon (it then flips above / below to fit and aims its arrow at the icon).
  useLayoutEffect(() => {
    const icon = wrap.current?.querySelector('[data-blocked]')
    if (!open) { setTarget(null); return }
    if (!icon || !wrap.current) return
    const w = wrap.current.getBoundingClientRect(), r = icon.getBoundingClientRect()
    setTarget({ left: r.left - w.left, top: r.top - w.top, width: r.width, height: r.height })
  }, [open])
  return <div ref={wrap} className={styles.illiquidCell}>
    <button type="button" className={styles.cell} data-side={side} data-illiquid="" aria-label={label} aria-expanded={open}
      onPointerDown={() => { wasOpen.current = open }} onClick={() => onToggle(!wasOpen.current)}>{children}</button>
    {open && target && <span className={styles.tipTarget} style={target}>
      <Tooltip placement="top" open onOpenChange={(next) => { if (!next) onToggle(false) }}
        content={<span className={styles.tip}><span className={styles.tipText}><span className={styles.tipTitle}>{t('chain.illiquid')}</span><span className={styles.tipSub}>{t('chain.illiquidSub')}</span></span><button type="button" className={styles.tipInfo} aria-label={t('chain.illiquidMore')} onClick={onMore}><Icon icon={msInfo} size={16} /></button></span>}>
        <span className={styles.tipDot} />
      </Tooltip>
    </span>}
  </div>
}
```

### `src/flows/fno/order-pad/data.ts`

```ts
/**
 * Commodity options order pad (Figma 8671:18433). Sample contract and account values, not live data. Prices in ₹.
 */
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
/** Selling (writing) shows the margin and leverage the exchange asks for. */
export const sellMargin = { margin: '7.00%', leverage: '14.3X' }
export const funds = { available: 1105002, required: 1075060 }
/** Intraday positions are squared off automatically at this time (MCX evening session). */
export const intradayCloseTime = '11:30 PM'
export const validities = ['Day', 'IOC']
```

### `src/flows/fno/order-pad/screens/OrderPad.module.css`

```css
/* Commodity options order pad (Figma 8671:18433) on L3 tokens. */
.contract { display: flex; flex-direction: column; align-items: flex-start; gap: var(--l3-spacing-02); padding: 0; border: 0; background: none; color: var(--l3-content-primary); text-align: left; cursor: pointer; }
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

.tpsl { display: inline-flex; align-items: center; gap: var(--l3-spacing-04); min-height: var(--l3-size-32); padding: 0; border: 0; background: none; color: var(--l3-content-primary); font: var(--l3-text-label-12); cursor: pointer; }

/* Dock: optional auto-close note (intraday), then Avail. · Req and the action. */
.dock { background: var(--l3-surface-primary); }
.autoClose { margin: 0; padding: var(--l3-spacing-12) var(--l3-spacing-16); font: var(--l3-text-label-12); color: var(--l3-content-tertiary); text-align: center; }
.dockBody { display: flex; flex-direction: column; gap: var(--l3-spacing-12); padding: var(--l3-spacing-12) var(--l3-spacing-16) var(--l3-spacing-16); border-top: 1px solid var(--l3-border-light); }
.funds { display: flex; justify-content: space-between; font: var(--l3-text-label-12); }
.req { padding: 0; border: 0; background: none; color: var(--l3-content-accent-discover-default); font: var(--l3-text-label-12); text-decoration: underline; cursor: pointer; }

/* ILLIQUID edge case: tag in the header (tap → explainer), the blocked note above the disabled action. */
.headEnd { display: inline-flex; align-items: center; gap: var(--l3-spacing-08); }
.tagButton { position: relative; display: inline-flex; padding: 0; border: 0; background: none; cursor: pointer; }
.tagButton::before { content: ''; position: absolute; inset: calc(-1 * var(--l3-spacing-16)) calc(-1 * var(--l3-spacing-04)); }
.illiquidNote { display: flex; align-items: center; justify-content: center; gap: var(--l3-spacing-04); width: 100%; min-height: var(--l3-size-40); padding: var(--l3-spacing-08) var(--l3-spacing-12); border: 0; border-radius: var(--l3-radius-08); background: var(--l3-surface-accent-error-light); font: var(--l3-text-label-12); color: var(--l3-content-accent-error-default); cursor: pointer; }
```

### `src/flows/fno/order-pad/screens/OrderPad.tsx`

```tsx
import { useState } from 'react'
import { Actionbar } from '@l3/components/Actionbar'
import { Aerobar } from '@l3/components/Aerobar'
import { Button } from '@l3/components/Button'
import { Icon } from '@l3/components/Icon'
import { PriceChange } from '@l3/components/PriceChange'
import { Select } from '@l3/components/Select'
import { Stack } from '@l3/components/Stack'
import { Stepper } from '@l3/components/Stepper'
import { Tabs } from '@l3/components/Tabs'
import { Tag } from '@l3/components/Tag'
import { lmSwitchArrowVertical } from '@l3/icons/lemonnade'
import { msAddCircleFill, msBlock, msInfo } from '@l3/icons/material'
import { inr } from '../../../../shared/data/format'
import { Screen } from '../../../../shared/ui/Screen'
import { ChoiceSheet, DetailSheet } from '../../sheets/HomeSheets'
import { IlliquidSheet } from '../../sheets/IlliquidSheet'
import { t } from '../../copy'
import { funds, intradayCloseTime, orderContract, sellMargin, validities, type OrderProduct, type OrderSide, type OrderType } from '../data'
import styles from './OrderPad.module.css'
import flat from '../../flatCards.module.css'

type Props = {
  side: OrderSide
  product?: OrderProduct
  type?: OrderType
  /**
   * Edge case: an ILLIQUID contract should never reach the order pad (every entry point blocks it), but if one does,
   * the pad shows the ILLIQUID tag, the blocked note in the dock and a disabled Buy / Sell.
   */
  illiquid?: boolean
  onBack: () => void
}

type Modal = { kind: 'choice'; title: string; values: string[]; value: string; onPick: (v: string) => void } | { kind: 'detail'; title: string } | { kind: 'illiquid' }

/**
 * Commodity options order pad (Figma 8671:18433) — commodity option chain only; other order pads differ a little.
 * Actionbar: back · contract ⇕ (name, expiry, price + change) · exchange, Delivery / Intraday tabs in its bottom slot.
 * Body: Market / Limit / SL pills (+ validity “Day ⇕” for Limit / SL); Sell shows Margin · Leverage; Quantity (⇕ lots,
 * lot hint, stepper of one lot); Limit adds a limit price row, SL a trigger price row and a limit row (each with a %
 * stepper from the market price); Set TPSL. Intraday: the auto-close note above the dock. Dock: Avail. · Req, then
 * Buy (brand) or Sell (sell).
 */
export function OrderPad({ side, product: initialProduct = 'delivery', type: initialType = 'market', illiquid = false, onBack }: Props) {
  const c = orderContract
  const [product, setProduct] = useState<OrderProduct>(initialProduct)
  const [type, setType] = useState<OrderType>(initialType)
  const [validity, setValidity] = useState(validities[0])
  const [lots, setLots] = useState(false)
  const [quantity, setQuantity] = useState(c.lotSize)
  const [limitPct, setLimitPct] = useState(20.3)
  const [triggerPct, setTriggerPct] = useState(20.3)
  const [modal, setModal] = useState<Modal | null>(null)
  const [placed, setPlaced] = useState(false)
  const buy = side === 'buy'
  const priceAt = (pct: number) => inr(Math.round(c.ltp * (buy ? 1 - pct / 1000 : 1 + pct / 1000)), 0)
  const priceRow = (label: string, pct: number, setPct: (n: number) => void) => <div className={styles.field}>
    <span className={styles.fieldLabel}>{label}</span>
    <span className={styles.fieldValue}>{priceAt(pct)}</span>
    <Stepper size="sm" className={styles.stepper} label={t('order.offset')} value={pct} onChange={setPct} min={0} step={0.1} format={(n) => `${n.toFixed(1)}%`} />
  </div>

  const sheet = modal?.kind === 'illiquid' ? <IlliquidSheet contract={`${c.name} ${c.contract}`} onClose={() => setModal(null)} /> : modal?.kind === 'choice' ? <ChoiceSheet {...modal} onClose={() => setModal(null)} /> : modal?.kind === 'detail' ? <DetailSheet title={modal.title} onClose={() => setModal(null)} /> : undefined
  const top = <Actionbar onBack={onBack} backLabel={t('order.back')}
    title={<button type="button" className={styles.contract} aria-label={t('order.switch')} onClick={() => setModal({ kind: 'detail', title: t('order.switch') })}>
      <span className={styles.contractName}>{c.name}<Icon icon={lmSwitchArrowVertical} size={16} /><span className={styles.expiry}>{c.contract}</span></span>
      <span className={styles.contractPrice}>{inr(c.ltp, 2)}<PriceChange value={c.change} unit="percent" size="sm" /></span>
    </button>}
    actions={<span className={styles.headEnd}>{illiquid && <button type="button" className={styles.tagButton} aria-label={t('illiquid.open')} onClick={() => setModal({ kind: 'illiquid' })}><Tag color="error" variant="secondary" size="sm" iconLeft={<Icon icon={msBlock} size={12} />}>{t('asset.illiquid')}</Tag></button>}<span className={styles.exchange}>{c.exchange}</span></span>}
    bottom={<Tabs aria-label={t('order.product')} value={product} onChange={setProduct} items={[{ value: 'delivery', label: t('order.delivery') }, { value: 'intraday', label: t('order.intraday') }]} />} />

  const dock = <div className={styles.dock} data-surface="primary">
    {product === 'intraday' && <p className={styles.autoClose}>{t('order.autoClose', { time: intradayCloseTime })}</p>}
    <div className={styles.dockBody}>
      <div className={styles.funds}>
        <span><span className={styles.muted}>{t('order.available')}</span> <strong>{inr(funds.available, 0)}</strong></span>
        <span><button type="button" className={styles.req} onClick={() => setModal({ kind: 'detail', title: t('order.required') })}>{t('order.required')}</button> <strong>{inr(funds.required, 0)}</strong></span>
      </div>
      {illiquid && <button type="button" className={styles.illiquidNote} onClick={() => setModal({ kind: 'illiquid' })}>{t('asset.illiquidNote')}<Icon icon={msInfo} size={16} /></button>}
      <Button variant={buy ? 'brand' : 'sell'} size="lg" fullWidth disabled={illiquid} onClick={() => setPlaced(true)}>{t(buy ? 'order.buy' : 'order.sell')}</Button>
    </div>
  </div>

  return <Screen className={flat.flatCards} top={top} bottom={dock} sheet={sheet}
    toast={placed ? <Aerobar floating type="success" heading={t('order.placed', { side: t(buy ? 'order.buy' : 'order.sell'), name: c.name, contract: c.contract })} onDismiss={() => setPlaced(false)} /> : undefined}>
    <Stack gap="16" className={styles.body}>
      <Stack direction="horizontal" align="center" justify="between">
        <Tabs aria-label={t('order.type')} appearance="pill" size="sm" value={type} onChange={setType} items={(['market', 'limit', 'sl'] as const).map((value) => ({ value, label: t(`order.${value}`) }))} />
        {type !== 'market' && <Select size="sm" aria-label={t('order.validity')} className={styles.validity} onClick={() => setModal({ kind: 'choice', title: t('order.validity'), values: validities, value: validity, onPick: setValidity })}>{validity}</Select>}
      </Stack>
      {!buy && <div className={styles.margin}><span><span className={styles.muted}>{t('order.margin')}</span> <strong>{sellMargin.margin}</strong></span><span><span className={styles.muted}>{t('order.leverage')}</span> <strong>{sellMargin.leverage}</strong></span></div>}
      <div className={styles.field}>
        <button type="button" className={styles.unit} aria-label={t('order.unitSwitch')} onClick={() => setLots(!lots)}>{t(lots ? 'order.lots' : 'order.quantity')}<Icon icon={lmSwitchArrowVertical} size={12} /></button>
        <span className={styles.hint}>{t('order.lotHint', { lot: c.lotSize })}</span>
        <Stepper size="sm" className={styles.stepper} label={t(lots ? 'order.lots' : 'order.quantity')} value={lots ? quantity / c.lotSize : quantity} onChange={(n) => setQuantity(lots ? n * c.lotSize : n)} min={lots ? 1 : c.lotSize} step={lots ? 1 : c.lotSize} />
      </div>
      {type === 'sl' && priceRow(t('order.trigger'), triggerPct, setTriggerPct)}
      {type !== 'market' && priceRow(t('order.limitPrice'), limitPct, setLimitPct)}
      <Stack direction="horizontal" justify="end">
        <button type="button" className={styles.tpsl} onClick={() => setModal({ kind: 'detail', title: t('order.tpsl') })}>{t('order.tpsl')}<Icon icon={msAddCircleFill} size={16} /></button>
      </Stack>
    </Stack>
  </Screen>
}
```

### `src/flows/fno/screens/Home.tsx`

```tsx
import { useEffect, useLayoutEffect, useRef, useState } from 'react'
import { Aerobar } from '@l3/components/Aerobar'
import { MaskIcon } from '@l3/components/MaskIcon'
import { Stack } from '@l3/components/Stack'
import { Tabs } from '@l3/components/Tabs'
import { Screen } from '../../../shared/ui/Screen'
import { user } from '../../../shared/data/user'
import { ContractSection, type Choose } from '../components/ContractSection'
import { Shortcuts, Watchlists } from '../components/Discovery'
import { FnoNav } from '../components/FnoNav'
import { Header } from '../components/Header'
import { Heatmap } from '../components/Heatmap'
import { UsBanner } from '../components/UsBanner'
import { Overview } from '../components/Overview'
import { TradingChart } from '../components/TradingChart'
import { ChoiceSheet, CreateWatchlistSheet, DetailSheet } from '../sheets/HomeSheets'
import { CommoditiesFeed } from '../commodities/components/CommoditiesFeed'
import { ContractPickerSheet } from '../commodities/sheets/ContractPickerSheet'
import type { Commodity, ExpiringContract } from '../commodities/data'
import { TrendInfoSheet } from '../commodities/sheets/TrendInfoSheet'
import { StrategiesFeed } from '../strategies/components/StrategiesFeed'
import type { Segment } from '../strategies/data'
import { watchlists, type Contract } from '../data'
import { t } from '../copy'
import equity from '../assets/equity.svg'
import commodities from '../assets/commodities.svg'
import strategies from '../assets/strategies.svg'
import styles from '../components/HomeParts.module.css'
import flat from '../flatCards.module.css'

export type HomePart = 'top' | 'watchlists' | 'options' | 'heatmap' | 'futures'
/** The product tab: Equity (fno-01…04), Commodities (fno-08…11), Strategies (fno-15, 16). */
export type Product = 'equity' | 'commodities' | 'strategies'
type Props = {
  product?: Product
  /** Strategies tab: Equity or Commodities strategies. */
  segment?: Segment
  /** Commodities tab: open with the contract picker up, on this tab of it. */
  picker?: 'equity' | 'commodities'
  onProduct: (product: Product, segment?: Segment) => void
  onCommodity: (commodity: Commodity) => void
  /** A contract card (Expiring This Week) → that contract's asset page. */
  onAsset: () => void
  /** Expiring This Week's View all → the Upcoming expiries timeline (fno-38). */
  onExpiries: () => void
  scrollTo?: HomePart; onHome: () => void; onSearch: () => void; onProfile: () => void; onWallet: () => void; onDash: () => void; onUsStocks?: () => void; onOptions: () => void; onFutures: () => void; onChain: () => void; onScalper: () => void }
type Modal = { kind: 'detail'; title: string; contract?: Contract } | { kind: 'create' } | { kind: 'choice'; title: string; values: string[]; value: string; onPick: (v: string) => void } | { kind: 'picker'; segment: 'equity' | 'commodities' } | { kind: 'trend'; contract: ExpiringContract }

/** fno-01 … 04 · one scrollable Equity home, with board frames for the lower sections. */
export function Home({ product = 'equity', segment = 'equity', picker, onProduct, onCommodity, onAsset, onExpiries, scrollTo = 'top', onHome, onSearch, onProfile, onWallet, onDash, onUsStocks, onOptions, onFutures, onChain, onScalper }: Props) {
  const root = useRef<HTMLDivElement>(null)
  const [modal, setModal] = useState<Modal | null>(picker ? { kind: 'picker', segment: picker } : null)
  const [instrument, setInstrument] = useState('Gold')
  const [lists, setLists] = useState(watchlists)
  const [created, setCreated] = useState(false)
  const [scrolled, setScrolled] = useState(false)
  // The product tabs are stuck under the top bar: their row takes the scrolled top bar's colour.
  const [tabsStuck, setTabsStuck] = useState(false)
  useEffect(() => {
    const body = root.current?.parentElement
    if (!body) return
    const tabs = root.current?.querySelector('[data-fno="tabs"]')
    const onScroll = () => {
      setScrolled(body.scrollTop > 0)
      setTabsStuck(!!tabs && body.scrollTop > 0 && tabs.getBoundingClientRect().top <= body.getBoundingClientRect().top + 1)
    }
    onScroll()
    body.addEventListener('scroll', onScroll, { passive: true })
    return () => body.removeEventListener('scroll', onScroll)
  }, [])
  const close = () => setModal(null)
  const open = (title: string) => setModal({ kind: 'detail', title })
  const choose: Choose = (title, values, value, onPick) => setModal({ kind: 'choice', title, values, value, onPick })
  const scroll = (part: HomePart) => {
    const body = root.current?.parentElement
    const target = root.current?.querySelector(`[data-fno="${part}"]`)
    if (body && target) body.scrollTo({ top: body.scrollTop + target.getBoundingClientRect().top - body.getBoundingClientRect().top, behavior: 'smooth' })
  }
  // A product tab switch slides only the content under the tabs, toward the chosen tab's side. If the page was
  // scrolled past the tabs (they stick under the top bar), it stops with the new content's start right under them.
  const order: Product[] = ['equity', 'commodities', 'strategies']
  const shownProduct = useRef(product)
  const [slide, setSlide] = useState<'from-end' | 'from-start' | null>(null)
  if (shownProduct.current !== product) {
    setSlide(order.indexOf(product) > order.indexOf(shownProduct.current) ? 'from-end' : 'from-start')
    shownProduct.current = product
  }
  useLayoutEffect(() => {
    const body = root.current?.parentElement
    const tabs = root.current?.querySelector('[data-fno="tabs"]')
    const content = root.current?.querySelector('[data-fno="content"]')
    if (!slide || !body || !tabs || !content) return
    // The tabs stick under the top bar, so measure the new content against their bottom edge.
    const offset = content.getBoundingClientRect().top - tabs.getBoundingClientRect().bottom
    if (offset < 0) body.scrollTop += offset
  }, [product])
  useEffect(() => { if (picker) setModal({ kind: 'picker', segment: picker }) }, [picker])
  useLayoutEffect(() => {
    const body = root.current?.parentElement
    const target = root.current?.querySelector(`[data-fno="${scrollTo}"]`)
    if (body && target && scrollTo !== 'top') body.scrollTop += target.getBoundingClientRect().top - body.getBoundingClientRect().top
  }, [scrollTo])
  const sheet = modal?.kind === 'detail' ? <DetailSheet title={modal.title} contract={modal.contract} onClose={close} /> : modal?.kind === 'choice' ? <ChoiceSheet {...modal} onClose={close} /> : modal?.kind === 'picker' ? <ContractPickerSheet segment={modal.segment} value={instrument} onPick={setInstrument} onClose={close} /> : modal?.kind === 'trend' ? <TrendInfoSheet contract={modal.contract} onClose={close} /> : modal?.kind === 'create' ? <CreateWatchlistSheet onClose={close} onCreate={(name) => { setLists((ls) => [...ls, { id: `custom-${ls.length}`, name, count: 0 }]); close(); setCreated(true) }} /> : undefined
  return <Screen className={flat.flatCards} top={<Header scrolled={scrolled} initials={user.name.split(' ').map((name) => name[0]).join('')} onSearch={onSearch} onProfile={onProfile} onWallet={onWallet} onDash={onDash} />} bottom={<FnoNav onHome={onHome} onDestination={open} onChain={onChain} onScalper={onScalper} />} sheet={sheet} toast={created ? <Aerobar floating type="success" heading={t('watchlists.created')} onDismiss={() => setCreated(false)} /> : undefined}>
    <Stack ref={root}>
      <div data-fno="top"><Overview onDestination={open} /></div>
      <div data-fno="tabs" className={styles.stickyTabs} data-stuck={tabsStuck || undefined}><Tabs aria-label="F&O products" appearance="ribbon" size="md" className={styles.productTabs} value={product} onChange={(v) => onProduct(v)} items={[{ value: 'equity', label: t('equity'), iconLeft: <span className={styles.ribbonIcon}><MaskIcon src={equity} /></span> }, { value: 'commodities', label: t('commodities'), iconLeft: <span className={styles.ribbonIcon}><MaskIcon src={commodities} /></span> }, { value: 'strategies', label: t('strategies'), iconLeft: <span className={styles.ribbonIcon}><MaskIcon src={strategies} /></span> }]} /></div>
      <div key={product} data-fno="content" className={styles.productContent} data-slide={slide ?? undefined}>
      {product === 'equity' && <Stack gap="32" className={styles.feed}>
        <Shortcuts onWatchlist={() => scroll('watchlists')} onDestination={open} />
        {onUsStocks && <UsBanner onOpen={onUsStocks} />}
        <TradingChart onChoose={choose} onDestination={open} onChain={onChain} onScalper={onScalper} />
        <div className={styles.divider} />
        <div data-fno="watchlists"><Watchlists lists={lists} onAdd={() => setModal({ kind: 'create' })} onOpen={open} /></div>
        <div data-fno="options"><ContractSection kind="options" onChoose={choose} onContract={(contract) => setModal({ kind: 'detail', title: contract.name, contract })} onViewAll={onOptions} /></div>
        <div data-fno="heatmap"><Heatmap onOpen={open} onViewAll={() => open(t('heatmap.title'))} /></div>
        <div data-fno="futures"><ContractSection kind="futures" onChoose={choose} onContract={(contract) => setModal({ kind: 'detail', title: contract.name, contract })} onViewAll={onFutures} /></div>
      </Stack>}
      {product === 'commodities' && <CommoditiesFeed instrument={instrument} lists={lists} onCommodity={onCommodity} onAsset={onAsset} onPicker={() => setModal({ kind: 'picker', segment: 'commodities' })} onChoose={choose} onContract={(contract) => setModal({ kind: 'detail', title: contract.name, contract })} onDestination={open} onAddWatchlist={() => setModal({ kind: 'create' })} onChain={onChain} onScalper={onScalper} onExpiries={onExpiries} onTrendInfo={(contract) => setModal({ kind: 'trend', contract })} />}
      {product === 'strategies' && <StrategiesFeed segment={segment} onSegment={(next) => onProduct('strategies', next)} onChoose={choose} onDestination={open} onWatchlist={() => open(t('shortcut.watchlist'))} />}
      </div>
    </Stack>
  </Screen>
}
```

### `src/flows/fno/screens/Scalper.module.css`

```css
/*
 * Scalper — measured on the live app's screenshot (392 wide, dark). Every colour is an L3 token: the page is
 * surface/default, the panels surface/primary; Active and its count use the Zing accent, the chart-type button the
 * US-stock blue (the live app's blue tint), Buy the brand lime.
 */

/* Chrome around the charts (header band, the band between the charts, the order dock): surface/secondary in light (the
   live app's grey separators), surface/default (black) in dark. */
.screen {
  --scalper-chrome: var(--l3-surface-default);
}

:global(html[data-mode='light']) .screen {
  --scalper-chrome: var(--l3-surface-secondary);
}

/* ---- Top: header (back · strategy tabs · add) and the tool row ---- */
.top {
  flex: none;
  background: var(--scalper-chrome);
}

.header {
  display: flex;
  align-items: flex-end;
  height: var(--l3-size-48);
  padding-left: var(--l3-spacing-06);
}

.back.back {
  align-self: center;
  margin-top: var(--l3-spacing-08);
}

/* L3 ribbon tabs: the selected tab takes the tool row's surface and a light edge, so it runs into the row below. */
.strategies.strategies {
  flex: none;
  padding-inline: var(--l3-spacing-16) var(--l3-spacing-20);
  background: transparent;
  box-shadow: none;
}

.strategies.strategies [role='tab'][aria-selected='true'] { /* beats L3's ribbon selector (0,3,0) */
  --tab-surface: var(--l3-surface-primary);
  --tab-border: var(--tab-surface); /* no outline (designer's call, 2026-11-03): sides and flares in the fill colour */
}

.addStrategies {
  display: inline-flex;
  align-items: center;
  gap: var(--l3-spacing-08);
  align-self: center;
  margin-top: var(--l3-spacing-08);
  padding: 0;
  border: 0;
  background: none;
  color: var(--l3-content-secondary);
  font: var(--l3-text-label-14);
  cursor: pointer;
}

.addRing {
  display: grid;
  place-items: center;
  width: var(--l3-size-24);
  height: var(--l3-size-24);
  border-radius: var(--l3-radius-full);
  background: var(--l3-surface-accent-zing-light);
  box-shadow: inset 0 0 0 1px var(--l3-border-accent-zing-default); /* 1px: Figma stroke weight has no variable */
  color: var(--l3-content-primary);
}

/* Tool row: 36 tall on surface/primary, a dashed line under it; scrolls sideways (Active runs off the edge). */
.tools {
  display: flex;
  align-items: center;
  height: var(--l3-spacing-36);
  padding-left: var(--l3-spacing-20);
  overflow-x: auto;
  background: var(--l3-surface-primary);
  border-bottom: 1px dashed var(--l3-border-intense);
}

.tool.tool {
  flex: none;
  --btn-content: var(--l3-content-primary);
  font: var(--l3-text-label-14);
}

.divider {
  flex: none;
  width: 1px;
  height: var(--l3-size-20);
  margin-inline: var(--l3-spacing-16);
  background: var(--l3-border-light);
}

/* Active strategies: Zing tint, rounded on the left, running off the right edge; the count sits on the icon. */
.active {
  display: inline-flex;
  flex: none;
  align-items: center;
  gap: var(--l3-spacing-08);
  height: var(--l3-size-32);
  margin-left: var(--l3-spacing-16);
  padding: 0 var(--l3-spacing-24) 0 var(--l3-spacing-12);
  border: 1px solid var(--l3-border-accent-zing-light);
  border-right: 0;
  border-radius: var(--l3-radius-08) 0 0 var(--l3-radius-08);
  background: var(--l3-surface-accent-zing-light);
  color: var(--l3-content-accent-zing-default);
  font: var(--l3-text-label-14);
  cursor: pointer;
}

.activeIcon {
  position: relative;
  display: grid;
  place-items: center;
}

.count {
  position: absolute;
  top: calc(-1 * var(--l3-spacing-08));
  right: calc(-1 * var(--l3-spacing-08));
  display: grid;
  place-items: center;
  min-width: var(--l3-size-16);
  height: var(--l3-size-16);
  border-radius: var(--l3-radius-full);
  background: var(--l3-surface-accent-zing-default);
  color: var(--l3-static-black);
  font: var(--l3-text-heading-10);
}

/* ---- Chart panels ---- */
.panel {
  display: flex;
  flex: 1;
  flex-direction: column;
  min-height: 0;
  background: var(--l3-surface-primary);
}

.panelHead {
  display: flex;
  flex: none;
  align-items: flex-start;
  justify-content: space-between;
  gap: var(--l3-spacing-12);
  padding: var(--l3-spacing-12) var(--l3-spacing-16) var(--l3-spacing-04);
}

.instrument {
  display: flex;
  flex-direction: column;
  min-width: 0;
}

.nameRow,
.priceRow {
  display: flex;
  align-items: center;
  gap: var(--l3-spacing-06);
  height: var(--l3-size-20);
}

.picker {
  display: inline-flex;
  align-items: center;
  gap: var(--l3-spacing-02);
  padding: 0;
  border: 0;
  background: none;
  color: var(--l3-content-secondary);
  cursor: pointer;
}

.name {
  color: var(--l3-content-primary);
  font: var(--l3-text-heading-14);
  text-decoration: underline;
  text-decoration-thickness: 1px;
  text-underline-offset: var(--l3-spacing-04);
}

.segment {
  margin-left: var(--l3-spacing-04);
  color: var(--l3-content-primary);
  font: var(--l3-text-label-14);
}

.link.link {
  --btn-content: var(--l3-content-primary);
  margin-left: var(--l3-spacing-04);
}

.price {
  color: var(--l3-content-primary);
  font: var(--l3-text-label-14);
}

.up {
  display: inline-flex;
  align-items: center;
  color: var(--l3-content-accent-indicator-up-default);
  font: var(--l3-text-label-14);
}


/* The pane's tools button: 32 (L3 Small) on surface/secondary. */

.paneButton.paneButton {
  --btn-surface: var(--l3-surface-secondary);
  --btn-content: var(--l3-content-primary);
  --btn-border: var(--l3-border-intense);
  margin-top: var(--l3-spacing-04);
}

/* The chart fills the panel; "N ▾" (indicators on it) sits at its top-left, the reset button at its bottom centre. */
.chart {
  position: relative;
  display: flex;
  flex: 1;
  min-height: 0;
}

.indicatorCount.indicatorCount {
  position: absolute;
  top: var(--l3-spacing-04);
  left: var(--l3-spacing-16);
  --btn-content: var(--l3-content-primary);
  font: var(--l3-text-label-14);
}

.refresh.refresh {
  position: absolute;
  bottom: var(--l3-spacing-40);
  left: 50%;
  --btn-content: var(--l3-content-accent-discover-default);
  --btn-radius: var(--l3-radius-full);
  transform: translateX(-50%);
}

/* Between the panes: a 16 band on the page colour with a drag handle. */
.split {
  display: grid;
  flex: none;
  place-items: center;
  height: var(--l3-size-16);
  background: var(--scalper-chrome);
}

.handle {
  width: var(--l3-size-40);
  height: var(--l3-size-04);
  padding: 0;
  border: 0;
  border-radius: var(--l3-radius-full);
  background: var(--l3-content-secondary);
  cursor: row-resize;
}

/* ---- Order dock ---- */
.dock {
  display: flex;
  flex: none;
  flex-direction: column;
  align-items: center;
  gap: var(--l3-spacing-04);
  padding: var(--l3-spacing-12) var(--l3-spacing-04) var(--l3-spacing-08);
  background: var(--scalper-chrome);
}

.orderType.orderType {
  background: transparent;
  box-shadow: inset 0 0 0 1px var(--l3-border-intense); /* 1px: Figma stroke weight has no variable */
}

.order {
  display: grid;
  grid-template-columns: minmax(0, 1fr) auto minmax(0, 1fr);
  align-items: start;
  gap: var(--l3-spacing-08);
  width: 100%;
}

.side,
.qty {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--l3-spacing-04);
}

.buy.buy,
.sell.sell {
  --btn-radius: var(--l3-radius-16);
}

.req {
  color: var(--l3-content-secondary);
  font: var(--l3-text-label-12);
}

.funds {
  color: var(--l3-content-secondary);
  font: var(--l3-text-label-10);
}

/* The chart-tools sheet brings its own layout: no content padding (L3 2.4: that includes its 16 top and 24 bottom
   spaces) — edge to edge. No top hairline either (L3 draws one above every sheet; over the dimmed screen it read as a
   stray line) — the sheet keeps its shadow. */
/* Raised so it beats L3's no-dock rule (.surface[data-placement] > .content:last-child adds 24 + the safe area). */
.sheet.sheet.sheet [data-sheet-content]:last-child,
.sheet [data-sheet-content] {
  padding: 0;
}

.sheet.sheet.sheet {
  box-shadow: var(--l3-shadow-elevation-high);
}

/* An open position (fno-35): the option pane takes 3 parts of the height to the spot pane's 2, so the TP, entry and
   SL pills clear each other (Figma C). */
.panel[data-tall] {
  flex: 1.5;
}
```

### `src/flows/fno/screens/Scalper.tsx`

```tsx
import { useMemo, useState } from 'react'
import { Button } from '@l3/components/Button'
import { ButtonGroup } from '@l3/components/ButtonGroup'
import type { ChartCandle } from '@l3/components/Chart'
import { Icon } from '@l3/components/Icon'
import { Stack } from '@l3/components/Stack'
import { Stepper } from '@l3/components/Stepper'
import { Tabs } from '@l3/components/Tabs'
import { msAdd, msArrowBack, msJoin, msLink, msMonitoring, msPlaylistAdd, msReceiptLong, msKeyboardArrowDown, msRefresh, msSwapHoriz, msUnfoldMore } from '@l3/icons/material'
import { Screen } from '../../../shared/ui/Screen'
import { Sheet } from '../../../shared/ui/Sheet'
import { PositionOverlay } from '../components/PositionOverlay'
import { TradingPane, type PaneLine, type TradingPaneProps } from '../components/TradingPane'
import { useLiveInstrument } from '../components/useLiveInstrument'
import { t } from '../copy'
import { breakevenPrice, defaultChartSettings, OPTION_TICK, SCALPER_TP_SL_GAP, scalperOption, scalperSpot, type ChartSettings, type ScalperInstrument, type ScalperPosition } from '../data'
import { BreakevenSheet } from '../sheets/BreakevenSheet'
import { ChartToolsSheet, type ToolsSection } from '../sheets/ChartToolsSheet'
import { SignalsSheet, type SignalsSheetState } from '../sheets/SignalsSheet'
import styles from './Scalper.module.css'
import flat from '../flatCards.module.css'

type ScalperProps = {
  onBack: () => void
  /** An indicator made with DASH AI: listed under Your indicators. */
  createdIndicator?: string
  /** Open with the chart-tools sheet up on Indicators. Default: open when a DASH indicator is passed (View indicator). */
  openIndicators?: boolean
  /** An indicator already applied to the NIFTY 50 pane. */
  initialIndicator?: string
  onCreateIndicator?: () => void
  onApplyIndicator?: (name: string) => void
  /** An open position on the option chart (TP / SL pills, the breakeven line). Default: none — Buy opens one. */
  initialPosition?: ScalperPosition
  /** Open with How breakeven works up, the chart-tools sheet on Settings, or Zing signals (the Active chip). */
  initialSheet?: 'breakeven' | 'settings' | 'signals'
  /** Zing signals: the state it opens in (filter sheet up, a saved filter …). */
  initialSignals?: SignalsSheetState
}

const LOT = 65

/**
 * Scalper (ScalpPro on F&O home) — the live app's trading workspace, rebuilt in L3:
 * - top: back · the strategy tabs (L3 ribbon: "All") · Add more strategies; under it the tool row (Positions · Orders ·
 *   Option chain · the Active strategies chip with its count);
 * - two linked chart panes: NIFTY 50 spot above, the option contract below, a handle between them;
 * - the order dock: Market / Limit-Trigger, Buy at Mkt · quantity in lots · Sell at Mkt, the margin each needs.
 * The spot pane's "add" button opens the chart-tools sheet (indicators). Prices are sample data.
 */
export function Scalper({ onBack, createdIndicator, openIndicators, initialIndicator, onCreateIndicator, onApplyIndicator, initialPosition, initialSheet, initialSignals }: ScalperProps) {
  /** Zing signals, from the Active chip at the tool row's right end. */
  const [signalsOpen, setSignalsOpen] = useState(initialSheet === 'signals')
  const [sheetOpen, setSheetOpen] = useState(initialSheet === 'settings' || (openIndicators ?? Boolean(createdIndicator)))
  const [toolsSection, setToolsSection] = useState<ToolsSection>(initialSheet === 'settings' ? 'settings' : 'indicators')
  /** The chart's settings, and the copy being edited in the sheet's Settings (Apply keeps it, Cancel drops it). */
  const [settings, setSettings] = useState<ChartSettings>(defaultChartSettings)
  const [draft, setDraft] = useState<ChartSettings>(defaultChartSettings)
  const [position, setPosition] = useState<ScalperPosition | null>(initialPosition ?? null)
  /** The option chart's scale takes in the TP / SL as they were set when the position opened (not while one is being
   * dragged — the scale would run away with it; dragging stays inside the chart). */
  const [scaleFor, setScaleFor] = useState<number[]>(() => tpSl(initialPosition))
  const [breakevenOpen, setBreakevenOpen] = useState(initialSheet === 'breakeven')
  /** Indicators on the NIFTY 50 chart (the sheet adds and removes them, several at once). */
  // An indicator saved with DASH is applied straight away (and a favourite in the sheet), so it's already on the chart.
  const [applied, setApplied] = useState<string[]>(() => [...new Set([initialIndicator, createdIndicator].filter((n): n is string => Boolean(n)))])
  const [orderType, setOrderType] = useState<'market' | 'limit'>('market')
  const [quantity, setQuantity] = useState(LOT)
  /** Both charts tick (prototype: a random walk around the sample prices; the real app's market feed). */
  const spot = useLiveInstrument(scalperSpot, { tick: OPTION_TICK })
  const option = useLiveInstrument(scalperOption, { tick: OPTION_TICK })
  const last = option.price
  const breakeven = position ? breakevenPrice(position.entry, position.quantity) : null

  /** Buy at Mkt: opens a position at the last price with a TP and SL 10 either side (or adds to the open one, averaging
   * the entry). The first buy ever opens How breakeven works. */
  const buy = () => {
    if (position) {
      setPosition({ ...position, entry: round2((position.entry * position.quantity + last * quantity) / (position.quantity + quantity)), quantity: position.quantity + quantity })
    } else {
      const opened = { entry: last, quantity, takeProfit: round2(last + SCALPER_TP_SL_GAP), stopLoss: round2(last - SCALPER_TP_SL_GAP), trailing: false }
      setPosition(opened)
      setScaleFor(tpSl(opened))
    }
    if (!breakevenIntroSeen()) {
      markBreakevenIntroSeen()
      setBreakevenOpen(true)
    }
  }
  /** Sell at Mkt: sells the dock's quantity from the open position (all of it closes the position). */
  const sell = () => setPosition((p) => (p && p.quantity > quantity ? { ...p, quantity: p.quantity - quantity } : null))
  const closeTools = () => {
    setSheetOpen(false)
    setDraft(settings)
  }
  const openTools = () => {
    setDraft(settings)
    setSheetOpen(true)
  }

  const overlay = useMemo<PaneLine[]>(() => (applied.length ? [{ values: ema(spot.candles, 9), tone: 'fast' }, { values: ema(spot.candles, 21), tone: 'slow' }] : []), [applied.length, spot.candles])

  return (
    <Screen
      className={`${styles.screen} ${flat.flatCards}`}
      top={
        <div className={styles.top}>
          <div className={styles.header}>
            <Button variant="ghost" size="sm" iconLeft={<Icon icon={msArrowBack} />} aria-label={t('scalper.back')} onClick={onBack} className={styles.back} />
            <Tabs aria-label={t('scalper.strategies')} appearance="ribbon" size="md" value="all" onChange={() => {}} items={[{ value: 'all', label: t('scalper.all') }]} className={styles.strategies} />
            <button type="button" className={styles.addStrategies}>
              {t('scalper.addStrategies')}
              <span className={styles.addRing} aria-hidden="true"><Icon icon={msAdd} size={16} /></span>
            </button>
          </div>
          <nav className={styles.tools} aria-label={t('scalper.tools')}>
            <Button variant="ghost" size="sm" iconLeft={<Icon icon={msMonitoring} />} className={styles.tool}>{t('scalper.positions')}</Button>
            <span className={styles.divider} aria-hidden="true" />
            <Button variant="ghost" size="sm" iconLeft={<Icon icon={msReceiptLong} />} className={styles.tool}>{t('scalper.orders')}</Button>
            <span className={styles.divider} aria-hidden="true" />
            <Button variant="ghost" size="sm" iconLeft={<Icon icon={msLink} />} className={styles.tool}>{t('scalper.chain')}</Button>
            <button type="button" className={styles.active} aria-label={t('scalper.activeCount', { count: 14 })} onClick={() => setSignalsOpen(true)}>
              <span className={styles.activeIcon} aria-hidden="true">
                <Icon icon={msSwapHoriz} />
                <span className={styles.count}>14</span>
              </span>
              {t('scalper.active')}
            </button>
          </nav>
        </div>
      }
      bottom={
        <div className={styles.dock} data-surface="default">
          <Tabs
            aria-label={t('scalper.orderType')}
            appearance="pill-group"
            size="sm"
            value={orderType}
            onChange={setOrderType}
            items={[{ value: 'market', label: t('scalper.market') }, { value: 'limit', label: t('scalper.limit') }]}
            className={styles.orderType}
          />
          <div className={styles.order}>
            <div className={styles.side}>
              <Button variant="buy" size="md" fullWidth className={styles.buy} onClick={buy}>{t('scalper.buy')}</Button>
              <span className={styles.req}>{t('scalper.required', { amount: '₹7,059.75' })}</span>
            </div>
            <div className={styles.qty}>
              <Stepper label={t('scalper.quantity')} value={quantity} onChange={setQuantity} min={LOT} step={LOT} size="lg" sublabel={t('scalper.lots', { count: quantity / LOT })} />
              <span className={styles.funds}>{t('scalper.funds', { amount: '₹-39.96' })}</span>
            </div>
            <div className={styles.side}>
              <Button variant="sell" size="md" fullWidth className={styles.sell} onClick={sell}>{t('scalper.sell')}</Button>
              <span className={styles.req}>{t('scalper.required', { amount: '₹1,57,436.49' })}</span>
            </div>
          </div>
        </div>
      }
      sheet={
        breakevenOpen ? (
          <BreakevenSheet onClose={() => setBreakevenOpen(false)} />
        ) : signalsOpen ? (
          <SignalsSheet initial={initialSignals} onClose={() => setSignalsOpen(false)} />
        ) : sheetOpen && (
          <Sheet
            label={t('scalper.chartTools')}
            onClose={closeTools}
            className={styles.sheet}
            footer={
              toolsSection === 'settings' ? (
                <ButtonGroup aria-label={t('settings.title')} direction="horizontal">
                  <Button variant="secondary" onClick={closeTools}>{t('settings.cancel')}</Button>
                  <Button
                    variant="brand"
                    onClick={() => {
                      setSettings(draft)
                      setSheetOpen(false)
                    }}
                  >
                    {t('settings.apply')}
                  </Button>
                </ButtonGroup>
              ) : undefined
            }
          >
            <ChartToolsSheet
              section={toolsSection}
              onSectionChange={setToolsSection}
              settings={draft}
              onSettingsChange={setDraft}
              onBreakevenInfo={() => setBreakevenOpen(true)}
              yourIndicators={createdIndicator ? [createdIndicator] : []}
              applied={applied}
              guide={Boolean(createdIndicator) && openIndicators !== false}
              onCreateIndicator={onCreateIndicator}
              onToggle={(name) => {
                const on = applied.includes(name)
                setApplied((a) => (on ? a.filter((n) => n !== name) : [...a, name]))
                if (!on) onApplyIndicator?.(name)
              }}
              onClearAll={() => setApplied([])}
            />
          </Sheet>
        )
      }
    >
      <ChartPanel instrument={spot} lines={overlay} applied={applied.length} onTools={openTools} />
      <div className={styles.split}>
        <button type="button" className={styles.handle} aria-label={t('scalper.resize')} />
      </div>
      <ChartPanel
        instrument={position ? { ...option, ...recent(option, POSITION_CANDLES) } : option}
        room={position ? POSITION_ROOM : undefined}
        include={position ? scaleFor : undefined}
        tall={Boolean(position)}
        refresh
        onTools={openTools}
        overlay={
          position
            ? (scale) => (
                <PositionOverlay
                  scale={scale}
                  position={position}
                  last={last}
                  breakeven={settings.breakevenLine ? breakeven : null}
                  onChange={setPosition}
                  onExit={() => setPosition(null)}
                  onBreakevenInfo={() => setBreakevenOpen(true)}
                />
              )
            : undefined
        }
      />
    </Screen>
  )
}

/** One chart pane: the instrument (name ⇅, segment ⇅, link), its price and change, the pane's buttons, the chart. */
function ChartPanel({ instrument, lines, applied = 0, refresh, onTools, overlay, include, room, tall }: { instrument: ScalperInstrument; lines?: PaneLine[]; overlay?: TradingPaneProps['overlay']; include?: number[]; room?: number; /** With a position open the option pane takes more of the height, so its pills have room (Figma C). */ tall?: boolean; /** Indicators on this chart: "N ▾" at its top-left (opens the sheet). */ applied?: number; /** The live app's reset button, bottom centre of the option chart. */ refresh?: boolean; onTools: () => void }) {
  const { name, segment, side, price, change, percent } = instrument
  return (
    <section className={styles.panel} data-tall={tall || undefined} aria-label={name}>
      <div className={styles.panelHead}>
        <div className={styles.instrument}>
          <div className={styles.nameRow}>
            <button type="button" className={styles.picker} aria-label={t('scalper.pickInstrument')}>
              <span className={styles.name}>{name}</span>
              {side && <span className={styles.segment}>{side}</span>}
              <Icon icon={msUnfoldMore} size={16} />
            </button>
            {segment && (
              <button type="button" className={styles.picker} aria-label={t('scalper.pickSegment')}>
                <span className={styles.segment}>{segment}</span>
                <Icon icon={msUnfoldMore} size={16} />
              </button>
            )}
            <Button variant="ghost" size="sm" iconLeft={<Icon icon={msJoin} />} aria-label={t('scalper.link')} className={styles.link} />
          </div>
          <div className={styles.priceRow}>
            <span className={styles.price}>{inr(price)}</span>
            <span className={styles.up}>{inr(change)}</span>
            <span className={styles.up}>
              ({percent >= 0 ? '+' : '−'}{Math.abs(percent).toFixed(2)}%)
            </span>
          </div>
        </div>
        <Stack direction="horizontal" gap="08">
          <Button variant="tertiary" size="sm" iconLeft={<Icon icon={msPlaylistAdd} />} aria-label={t('scalper.chartTools')} onClick={onTools} className={styles.paneButton} />
        </Stack>
      </div>
      <div className={styles.chart}>
        <TradingPane candles={instrument.candles} start={instrument.start} minutes={instrument.minutes} lines={lines} include={include} room={room} overlay={overlay} label={t('scalper.chartLabel', { name })} />
        {applied > 0 && (
          <Button variant="ghost" size="sm" iconRight={<Icon icon={msKeyboardArrowDown} />} aria-label={t('scalper.indicatorCount', { count: applied })} onClick={onTools} className={styles.indicatorCount}>
            {applied}
          </Button>
        )}
        {refresh && <Button variant="tertiary" size="sm" iconLeft={<Icon icon={msRefresh} />} aria-label={t('scalper.refresh')} className={styles.refresh} />}
      </div>
    </section>
  )
}

const inr = (v: number) => v.toLocaleString('en-IN', { minimumFractionDigits: 2, maximumFractionDigits: 2 })

/** Exponential moving average of the closes — the applied indicator's illustrative lines. */
function ema(candles: ChartCandle[], period: number) {
  const k = 2 / (period + 1)
  return candles.reduce<number[]>((out, c, i) => [...out, i ? c.close * k + out[i - 1] * (1 - k) : c.close], [])
}

/** With a position open, the option chart shows the candles since the 13:55 spike (its last 19), thin, with room after
 * them for the price to run into (Figma C: the candles stop about three quarters across). */
const POSITION_CANDLES = 19
const POSITION_ROOM = 8
function recent(instrument: ScalperInstrument, count: number) {
  const skip = Math.max(0, instrument.candles.length - count)
  const [h, m] = instrument.start.split(':').map(Number)
  const total = h * 60 + m + skip * instrument.minutes
  return { candles: instrument.candles.slice(skip), start: `${Math.floor(total / 60)}:${String(total % 60).padStart(2, '0')}` }
}

const tpSl = (p?: ScalperPosition | null) => (p ? [p.takeProfit, p.stopLoss].filter((v): v is number => v !== null) : [])

const round2 = (v: number) => Math.round(v * 100) / 100

/** How breakeven works opens by itself on the first buy only (prototype: once per browser). */
const BREAKEVEN_INTRO_KEY = 'fno.breakevenIntroSeen'
function breakevenIntroSeen() {
  try { return localStorage.getItem(BREAKEVEN_INTRO_KEY) === '1' } catch { return false }
}
function markBreakevenIntroSeen() {
  try { localStorage.setItem(BREAKEVEN_INTRO_KEY, '1') } catch { /* storage off: it may show again next time */ }
}
```

### `src/flows/fno/sheets/BreakevenSheet.module.css`

```css
/* How breakeven works (Figma 11783:5569). L3 tokens; the explainer's timings are local tokens (src/local-tokens.css). */

/* The example card: 1px light edge, radius 12, a header line then the stage. */
.example {
  overflow: hidden;
  border: 1px solid var(--l3-border-light);
  border-radius: var(--l3-radius-12);
}

.exampleHead {
  margin: 0;
  padding: var(--l3-spacing-12) var(--l3-spacing-16);
  border-bottom: 1px solid var(--l3-border-light);
  color: var(--l3-content-primary);
  font: var(--l3-text-heading-12);
}

.exampleTag {
  color: var(--l3-content-secondary);
}

/* ---- The charges table: a calculation, built on L3 key-value rows (L3 has no table) ----
   A secondary-surface card (radius 12, no edge, no heading, no lines inside) so it stands apart from the white sheet:
   compact rows (4 / 16), the total last — L3's total row (bold label, larger value) on the same grey. */
.table {
  overflow: hidden;
  border-radius: var(--l3-radius-12);
  background: var(--l3-surface-secondary);
}

.tableRows {
  margin: 0;
  padding: var(--l3-spacing-08) 0;
}

.tableRow {
  padding: var(--l3-spacing-04) var(--l3-spacing-16);
  white-space: nowrap;
}

/* The total: L3's total row (bold label, larger value), no tint and no divider (L3's inset line off). */
.tableTotal.tableTotal {
  margin-top: var(--l3-spacing-04);
  padding-top: var(--l3-spacing-04);
  box-shadow: none;
}

/* The charges row opens the breakdown: its label is the toggle, stretched over the whole row so a tap anywhere works. */
.chargesRow {
  position: relative;
  cursor: pointer;
}

.chargesToggle {
  display: inline-flex;
  align-items: center;
  gap: var(--l3-spacing-04);
  padding: 0;
  border: 0;
  background: none;
  color: inherit;
  font: inherit;
  cursor: pointer;
}

.chargesToggle::after {
  content: '';
  position: absolute;
  inset: 0;
}

.chargesToggle:focus-visible {
  outline: none;
}

.chargesRow:has(.chargesToggle:focus-visible) {
  outline: var(--l3-spacing-02) solid var(--l3-border-dark);
  outline-offset: calc(-1 * var(--l3-spacing-02));
}

.chevron {
  display: inline-flex;
  transition: transform var(--l3-motion-duration-short) var(--l3-motion-easing-standard);
}

.chevron[data-open] {
  transform: rotate(180deg);
}

/* The breakdown: sm rows on a tertiary-surface panel inside the table (it sits on secondary). */
.breakdown {
  display: flex;
  flex-direction: column;
  gap: var(--l3-spacing-08);
  margin: var(--l3-spacing-04) var(--l3-spacing-16);
  padding: var(--l3-spacing-08) var(--l3-spacing-12);
  border-radius: var(--l3-radius-08);
  background: var(--l3-surface-tertiary);
}

.breakdown[hidden] {
  display: none;
}

/* ---- Info rows ---- */
.infoIcon {
  display: grid;
  flex: none;
  place-items: center;
  width: var(--l3-size-20);
  height: var(--l3-size-20);
}

.infoText {
  margin: 0;
  color: var(--l3-content-secondary);
  font: var(--l3-text-description-12);
}

.infoText strong {
  color: var(--l3-content-primary);
  font-weight: var(--l3-text-heading-12-weight);
}

/* ---- "I understand" with its loader (Figma 11783:12460): a 4 track across the button's top edge fills while the
   example chart plays once (6.3 s), then the button unlocks (BreakevenSheet listens for the fill's animationend). ---- */
.loader {
  position: relative;
  display: grid;
  width: 100%;
  overflow: hidden;
  border-radius: var(--l3-radius-12);
}

.track {
  position: absolute;
  inset: 0 0 auto;
  height: var(--l3-spacing-04);
  background: var(--l3-surface-tertiary);
}

.fill {
  display: block;
  height: 100%;
  background: var(--l3-surface-inverted);
  transform-origin: left;
  animation: fill var(--app-be-explainer) linear both;
}

@keyframes fill {
  from {
    scale: 0 1;
  }
}
```

### `src/flows/fno/sheets/BreakevenSheet.tsx`

```tsx
import { Fragment, useId, useState, type CSSProperties } from 'react'
import { BottomSheetHeader } from '@l3/components/BottomSheet'
import { Button } from '@l3/components/Button'
import { Icon } from '@l3/components/Icon'
import { msKeyboardArrowDown } from '@l3/components/icons/glyphs'
import { KeyValueRow } from '@l3/components/KeyValueList'
import { ButtonGroup } from '@l3/components/ButtonGroup'
import { Stack } from '@l3/components/Stack'
import { useFlowOption } from '../../../shared/prototype'
import { Sheet } from '../../../shared/ui/Sheet'
import { BreakevenExplainer, chargeInr, EXPLAINER_LENGTH } from '../components/BreakevenExplainer'
import { BreakevenIcon } from '../components/BreakevenIcon'
import { t } from '../copy'
import { breakevenCharges, breakevenExample, exampleChargesTotal, exampleGst } from '../data'
import styles from './BreakevenSheet.module.css'

/**
 * How breakeven works (Figma 11783:5569, dark 11783:6220) — opens the first time the user buys on the Scalper, and from
 * the ⓘ on the chart's breakeven chip.
 * - The example card ("Example: Bought 1 lot at ₹100") plays the explainer once and stops on the finished chart; a tap plays it again (BreakevenExplainer — copied from
 *   the designer's recording: the chart builds up to a sell above the breakeven line, then the Breakeven Line intro).
 * - "I understand" is locked while it plays (Figma's button variants 11783:12460: a loader line fills along the
 *   button's top edge, then the button turns primary) until the chart has played once (9.3 s). Reduced motion: the
 *   finished chart, the button ready.
 * - Under it, the same example as a table: bought at, order charges with GST (tap to open the breakdown, closed by
 *   default) and the breakeven price.
 */
export function BreakevenSheet({ onClose }: { onClose: () => void }) {
  const headingId = useId()
  const [still] = useState(prefersReducedMotion)
  const [ready, setReady] = useState(still)
  // Prototype setting "Breakeven sheet": v2 (default) = new heading + description + charges table, no info lines;
  // v1 = the sheet as it first shipped (How breakeven works, the two info lines, no table).
  const v1 = useFlowOption('fno', 'breakevenSheet', 'v2') === 'v1'

  return (
    <Sheet
      labelledBy={headingId}
      onClose={onClose}
      header={v1
        ? <BottomSheetHeader size="sm" headingId={headingId} heading={t('breakeven.title')} />
        : <BottomSheetHeader size="sm" headingId={headingId} heading={t('breakeven.titleV2')} />}
      footer={
        <ButtonGroup aria-label={t('breakeven.title')}>
          <div className={styles.loader} style={{ '--app-be-explainer': `${EXPLAINER_LENGTH}ms` } as CSSProperties}>
            <Button fullWidth disabled={!ready} onClick={onClose}>{t('breakeven.understand')}</Button>
            {!ready && (
              <span className={styles.track} role="progressbar" aria-label={t('breakeven.playing')}>
                <span className={styles.fill} onAnimationEnd={() => setReady(true)} />
              </span>
            )}
          </div>
        </ButtonGroup>
      }
    >
      <Stack gap="24">
        <section className={styles.example} aria-label={t('breakeven.exampleLabel')}>
          <p className={styles.exampleHead}>
            <span className={styles.exampleTag}>{t('breakeven.example')}</span> {t('breakeven.exampleTrade', { price: '₹100' })}
          </p>
          <BreakevenExplainer still={still} />
        </section>
        {v1 ? (
          <Stack gap="12">
            <InfoRow icon={<BreakevenIcon variant="line" />} text={t('breakeven.info1')} />
            <InfoRow icon={<BreakevenIcon variant="up" />} text={t('breakeven.info2')} />
          </Stack>
        ) : <ChargesTable />}
      </Stack>
    </Sheet>
  )
}

/** Breakdown order: what the trader pays most first, GST last (it's charged on the others). */
const BREAKDOWN_ORDER = ['stt', 'transaction', 'brokerage', 'stamp', 'sebi'] as const

/**
 * The example as a calculation table on a grey card (no heading, no lines), one row each —
 * Bought at, Order charges (incl. GST), Breakeven price (bold, L3's total row). The charges row opens and closes the breakdown (closed by default) — a tap anywhere on it.
 */
function ChargesTable() {
  const [open, setOpen] = useState(false)
  const breakdownId = useId()
  const { entry, breakeven } = breakevenExample
  const amountOf = (id: (typeof BREAKDOWN_ORDER)[number]) => breakevenCharges.find((c) => c.id === id)?.amount ?? 0
  const charges = `≈${chargeInr(exampleChargesTotal)}`
  return (
    <section className={styles.table} aria-label={t('breakeven.tableLabel')}>
      <dl className={styles.tableRows}>
        <KeyValueRow className={styles.tableRow} label={t('breakeven.tableBought')} value={inr(entry)} />
        <KeyValueRow
          className={`${styles.tableRow} ${styles.chargesRow}`}
          label={
            <button type="button" className={styles.chargesToggle} aria-expanded={open} aria-controls={breakdownId}
              aria-label={`${t('breakeven.tableCharges')}. ${t(open ? 'breakeven.tableHide' : 'breakeven.tableShow')}`} onClick={() => setOpen(!open)}>
              {t('breakeven.tableCharges')}
              <span className={styles.chevron} data-open={open || undefined}><Icon icon={msKeyboardArrowDown} size={16} /></span>
            </button>
          }
          value={charges}
        />
        <div id={breakdownId} className={styles.breakdown} hidden={!open}>
          {BREAKDOWN_ORDER.map((id) => <KeyValueRow key={id} size="sm" label={t(`breakeven.charge.${id}`)} value={chargeInr(amountOf(id))} />)}
          <KeyValueRow size="sm" label={t('breakeven.charge.gst')} value={chargeInr(exampleGst)} />
        </div>
        <KeyValueRow total className={`${styles.tableRow} ${styles.tableTotal}`} label={t('breakeven.tableBreakeven')} value={inr(breakeven)} />
      </dl>
    </section>
  )
}

const inr = (amount: number) => `₹${amount.toFixed(2)}`

/** A line of the explainer: a 20 icon and text with **bold** parts. */
function InfoRow({ icon, text }: { icon: React.ReactNode; text: string }) {
  return (
    <Stack direction="horizontal" gap="12" align="start">
      <span className={styles.infoIcon}>{icon}</span>
      <p className={styles.infoText}>
        {text.split('**').map((part, k) => (k % 2 ? <strong key={k}>{part}</strong> : <Fragment key={k}>{part}</Fragment>))}
      </p>
    </Stack>
  )
}

function prefersReducedMotion() {
  return typeof window !== 'undefined' && window.matchMedia?.('(prefers-reduced-motion: reduce)').matches
}
```

### `src/flows/fno/sheets/ChartSettingsPanel.tsx`

```tsx
import { Card } from '@l3/components/Card'
import { Checkbox, Radio } from '@l3/components/Checkbox'
import { Grid } from '@l3/components/Grid'
import { Icon } from '@l3/components/Icon'
import { ListCell } from '@l3/components/ListCell'
import { Stack } from '@l3/components/Stack'
import { Tag } from '@l3/components/Tag'
import { msBarChart, msCandlestickChart, msChevronRight, msInfo, msShowChart } from '@l3/icons/material'
import { AutoTpSlIcon } from '../components/AutoTpSlIcon'
import { t } from '../copy'
import type { ChartSettings, ChartType, StopLossPreference } from '../data'
import styles from './ChartToolsSheet.module.css'

type ChartSettingsPanelProps = {
  /** The settings as edited in the sheet (a draft: Apply keeps them, Cancel drops them). */
  value: ChartSettings
  onChange: (value: ChartSettings) => void
  /** The ⓘ after Breakeven line: How breakeven works. */
  onBreakevenInfo: () => void
}

const chartTypes: { value: ChartType; icon: typeof msShowChart }[] = [
  { value: 'candles', icon: msCandlestickChart },
  { value: 'heikinAshi', icon: msBarChart },
  { value: 'line', icon: msShowChart },
]

const stopLossOptions: StopLossPreference[] = ['market', 'limit']

/**
 * Chart tools → Settings (Figma 11754:69563, dark 11783:9335):
 * - Auto TP/SL: a card row with the animated mark, "Applied" (blue tag) and a chevron;
 * - Chart type: three cards — Candles, Heikin Ashi, Line — one selected (blue);
 * - Stop Loss Preference: At Market Price / At Limit Price (radio cards);
 * - View on chart: Breakeven line ⓘ (New), Buy/Sell executions, Sync Charts (checkbox cards).
 * Changes are a draft until Apply in the sheet's dock (Cancel leaves the chart as it was).
 */
export function ChartSettingsPanel({ value, onChange, onBreakevenInfo }: ChartSettingsPanelProps) {
  const set = <K extends keyof ChartSettings>(key: K, v: ChartSettings[K]) => onChange({ ...value, [key]: v })
  const views = [
    { key: 'breakevenLine', label: t('settings.breakeven'), info: true, isNew: true },
    { key: 'executions', label: t('settings.executions') },
    { key: 'syncCharts', label: t('settings.sync') },
  ] as const

  return (
    <Stack gap="24">
      <ListCell
        variant="card"
        size="sm"
        as="button"
        iconLeft={<AutoTpSlIcon />}
        label={t('settings.autoTpSl')}
        trailing={<Tag variant="secondary" color="discover" size="sm">{t('settings.applied')}</Tag>}
        iconRight={<Icon icon={msChevronRight} />}
        onClick={() => {}}
        className={styles.row}
      />

      <Stack as="section" gap="12" aria-labelledby="settings-chart-type">
        <h3 id="settings-chart-type" className={styles.subTitle}>{t('settings.chartType')}</h3>
        <Grid columns={3} gap="08">
          {chartTypes.map((type) => (
            <Card key={type.value} selected={value.chartType === type.value} onClick={() => set('chartType', type.value)} aria-label={t(`settings.type.${type.value}`)} className={styles.typeCard}>
              <Stack gap="04" align="center">
                <Icon icon={type.icon} size={20} />
                <span className={styles.typeLabel}>{t(`settings.type.${type.value}`)}</span>
              </Stack>
            </Card>
          ))}
        </Grid>
      </Stack>

      <Stack as="section" gap="12" aria-labelledby="settings-sl">
        <h3 id="settings-sl" className={styles.subTitle}>{t('settings.stopLoss')}</h3>
        <Stack gap="08" role="radiogroup" aria-labelledby="settings-sl">
          {stopLossOptions.map((option) => (
            <ListCell
              key={option}
              variant="card"
              size="sm"
              as="label"
              label={t(`settings.sl.${option}`)}
              selected={value.stopLoss === option}
              trailing={<Radio name="chart-sl-preference" checked={value.stopLoss === option} onChange={() => set('stopLoss', option)} />}
              className={styles.row}
            />
          ))}
        </Stack>
      </Stack>

      <Stack as="section" gap="12" aria-labelledby="settings-view">
        <h3 id="settings-view" className={styles.subTitle}>{t('settings.view')}</h3>
        <Stack gap="08">
          {views.map((view) => (
            <ListCell
              key={view.key}
              variant="card"
              size="sm"
              as="label"
              label={
                'info' in view ? (
                  <span className={styles.settingLabel}>
                    {view.label}
                    <button
                      type="button"
                      className={styles.infoButton}
                      aria-label={t('breakeven.title')}
                      onClick={(e) => {
                        e.preventDefault()
                        onBreakevenInfo()
                      }}
                    >
                      <Icon icon={msInfo} size={16} />
                    </button>
                    <Tag variant="primary" color="success" size="sm">{t('settings.new')}</Tag>
                  </span>
                ) : view.label
              }
              trailing={<Checkbox checked={value[view.key]} onChange={(e) => set(view.key, e.target.checked)} aria-label={view.label} />}
              className={styles.row}
            />
          ))}
        </Stack>
      </Stack>
    </Stack>
  )
}
```

### `src/flows/fno/sheets/ChartToolsSheet.module.css`

```css
/*
 * Chart tools sheet (live app): a 96 side-nav column with a hairline on its right, the panel beside it scrolls.
 * About two thirds of the screen tall (live app: 571 of 872).
 */
.body {
  position: relative;
  display: grid;
  grid-template-columns: var(--l3-size-96) minmax(0, 1fr);
  height: calc(var(--l3-size-128) * 4.5); /* 576 — the live sheet's height; L3 has no size this large */
  max-height: 100%;
  transition: height var(--l3-motion-duration-medium) var(--l3-motion-easing-standard);
}

/* Search: the sheet opens to its full height (the sheet caps it under the status bar). */
.body[data-search] {
  height: 100vh;
}

/* NEW on the Zing yellow: content/inverted (white in light, black in dark). Beats L3's [data-flag-tone='zing']. */
.nav.nav[data-flag-tone] {
  --side-nav-flag-content: var(--l3-content-inverted);
}

.nav {
  padding: var(--l3-spacing-16) var(--l3-spacing-08);
  overflow-y: auto;
  box-shadow: inset -1px 0 0 var(--l3-border-light); /* 1px: Figma stroke weight has no variable */
}

.panel {
  min-height: 0;
  overflow-x: clip; /* scrolls up and down only (the lit guide box reaches 8 past the rows) */
  overflow-y: auto;
  padding: 0 var(--l3-spacing-16) var(--l3-spacing-24);
}

/* The panel's header (title + actions, or the search field) stays put while the lists scroll under it: the panel's
   full width, a 1px border-light line under it, the content 16 below. */
.header {
  position: sticky;
  top: 0;
  z-index: 3;
  margin: 0 calc(-1 * var(--l3-spacing-16)) var(--l3-spacing-16);
  padding: var(--l3-spacing-12) var(--l3-spacing-16);
  background: var(--l3-surface-primary);
  box-shadow: inset 0 -1px 0 var(--l3-border-light); /* 1px: Figma stroke weight has no variable */
}

.titleRow {
  min-height: var(--l3-size-40);
}

/* Your indicators' heading row: as tall as its Create button (40), centred with it. */
.sectionHead {
  min-height: var(--l3-size-40);
}

/* Header icons (search, clear all): 20 — 4 up from the Small button's 16 (designer's call). */
.headerIcon.headerIcon {
  --btn-icon-size: var(--l3-icon-size-20);
}

.title {
  margin: 0;
  font: var(--l3-text-heading-16); /* the sheet's heading: Heading/16 (was Label/16) */
  color: var(--l3-content-primary);
}

.subTitle {
  margin: 0;
  font: var(--l3-text-heading-14);
  color: var(--l3-content-primary);
}

.subDescription {
  margin: 0;
  font: var(--l3-text-description-12);
  color: var(--l3-content-secondary);
}

.empty {
  margin: 0;
  font: var(--l3-text-description-14);
  color: var(--l3-content-tertiary);
}

/* Indicator rows: 48 tall — L3 card cell (Small), radius 8 (designer's call, 2026-10-27). */
.row.row.row {
  --cell-icon: var(--l3-icon-size-20); /* the star (and the applied ✕): 20, up from the Small cell's 16 */
  min-height: var(--l3-size-48);
  padding-block: var(--l3-spacing-06);
  border-radius: var(--l3-radius-08);
}

/* Flat rows: the light edge only, no drop shadow (designer's call, 2026-10-27; L3's clickable cell has elevation/low). */
.panel .row.row.row {
  box-shadow: inset 0 0 0 1px var(--l3-border-light); /* 1px: Figma stroke weight has no variable */
}

.star {
  color: var(--l3-content-accent-discover-default);
}

/* On the chart (live app): the row turns blue — discover tint, edge and text, ✕ to take it off. */
.panel .row.row.row[data-selected] {
  background: var(--l3-surface-accent-discover-light);
  box-shadow: inset 0 0 0 1px var(--l3-border-accent-discover-default); /* 1px: Figma stroke weight has no variable */
  color: var(--l3-content-accent-discover-default);
}

.panel .row.row.row[data-selected] :is(span, p, svg) {
  color: var(--l3-content-accent-discover-default);
}

/* fx with the count: the discover edge and glyph. */
.fx.fx {
  --btn-border: var(--l3-border-accent-discover-default);
  --btn-content: var(--l3-content-accent-discover-default);
  --btn-surface: var(--l3-surface-accent-discover-light);
}


/* The coach mark's anchor hugs its content (inline): here it takes the panel's width, like Lemonn indicators below. */
.yours > * {
  display: flex;
  width: 100%;
}

.yours > * > section {
  flex: 1;
  min-width: 0;
}

/* Focus guide: the sheet dims (surface/overlay); Your indicators stays lit above it on the sheet's own surface. */
.dim {
  position: absolute;
  inset: 0;
  z-index: 4; /* over the sticky header (3) too: only Your indicators stays lit */
  background: var(--l3-surface-overlay);
  animation: guide-in var(--l3-motion-duration-medium) var(--l3-motion-easing-decelerate) both;
}

/* The lit box is the tooltip's anchor itself, so the tooltip measures from the highlight's edge (its tip touches it). */
.yours[data-lit] {
  position: relative;
  z-index: 5;
}

/* The guide's tooltip: white with black text in both themes (static colours), lifted with the high elevation. Its
   arrow follows --tt-surface. */
.yours [role='tooltip'] {
  --tt-surface: var(--l3-static-white);
  color: var(--l3-static-black);
  box-shadow: var(--l3-shadow-elevation-high);
}

.yours [role='tooltip'] :is(button, svg, span) {
  color: inherit;
}

.yours[data-lit] > * {
  box-sizing: border-box;
  width: auto;
  max-width: none;
  margin: calc(-1 * var(--l3-spacing-08));
  padding: var(--l3-spacing-08);
  border-radius: var(--l3-radius-12);
  background: var(--l3-surface-primary);
}

@keyframes guide-in {
  from {
    opacity: 0;
  }
}

@media (prefers-reduced-motion: reduce) {
  .dim {
    animation: none;
  }
}

/* Your indicators' rows: a long press opens the details (no text selection / callout while holding). */
.pressable {
  -webkit-touch-callout: none;
  user-select: none;
}

/* The line under Your indicators: each hint slides up into place as it changes. */
.hint {
  display: inline-block;
  animation: tools-hint var(--l3-motion-duration-medium) var(--l3-motion-easing-decelerate) both;
}

@keyframes tools-hint {
  from {
    opacity: 0;
    transform: translateY(var(--l3-spacing-06));
  }
}

/* The details sheet's header icon: a ★ on a light discover tile (the colour Your indicators use). */
.detailsIcon {
  display: grid;
  place-items: center;
  width: var(--l3-size-64);
  height: var(--l3-size-64);
  border-radius: var(--l3-radius-16);
  background: var(--l3-surface-accent-discover-light);
  color: var(--l3-content-accent-discover-default);
}

@media (prefers-reduced-motion: reduce) {
  .hint {
    animation: none;
  }
}

/* ---- Settings (Figma 11754:69563) ---- */

/* Chart type: three small cards, icon over label; the chosen one is L3's selected card in the discover tint (Figma). */
.typeCard.typeCard {
  padding: var(--l3-spacing-12) var(--l3-spacing-04);
  border-radius: var(--l3-radius-08);
  color: var(--l3-content-primary);
}

.typeCard.typeCard[data-selected],
.typeCard.typeCard[aria-pressed='true'] {
  background: var(--l3-surface-accent-discover-light);
  box-shadow: inset 0 0 0 1px var(--l3-border-accent-discover-default); /* 1px: Figma stroke weight has no variable */
  color: var(--l3-content-accent-discover-default);
}

.typeLabel {
  font: var(--l3-text-label-12);
  text-align: center;
  white-space: nowrap;
}

/* "Breakeven line ⓘ New": the label, a tappable ⓘ (How breakeven works) and the New tag on one line. */
.settingLabel {
  display: inline-flex;
  align-items: center;
  gap: var(--l3-spacing-04);
}

.infoButton {
  display: grid;
  place-items: center;
  padding: 0;
  border: 0;
  background: none;
  color: var(--l3-content-secondary);
  cursor: pointer;
}

.settingLabel > :last-child {
  margin-left: var(--l3-spacing-04);
}
```

### `src/flows/fno/sheets/ChartToolsSheet.tsx`

```tsx
import { useEffect, useRef, useState } from 'react'
import { Badge } from '@l3/components/Badge'
import { Button } from '@l3/components/Button'
import { Icon } from '@l3/components/Icon'
import { ListCell } from '@l3/components/ListCell'
import { SideNav } from '@l3/components/SideNav'
import { Stack } from '@l3/components/Stack'
import { TextField } from '@l3/components/TextField'
import { Tooltip } from '@l3/components/Tooltip'
import { msAdd, msBookmarkFill, msClose, msDelete, msDraw, msFunction, msSearch, msSettings, msSpaceBar, msStar, msStarFill, msSwapHoriz } from '@l3/icons/material'
import { t } from '../copy'
import { lemonnIndicators, type ChartSettings } from '../data'
import { ChartSettingsPanel } from './ChartSettingsPanel'
import { IndicatorDetailsSheet } from './IndicatorDetailsSheet'
import styles from './ChartToolsSheet.module.css'

export type ToolsSection = 'range' | 'zing' | 'indicators' | 'drawings' | 'templates' | 'settings'

type ChartToolsSheetProps = {
  /** Indicators the user made with DASH AI (Your indicators). */
  yourIndicators: string[]
  /** Indicators on the chart now, in the order they were added. */
  applied: string[]
  /** A row tapped: on the chart → off, off → on. The sheet stays open. */
  onToggle: (name: string) => void
  /** The bin in the header: take every indicator off the chart. */
  onClearAll: () => void
  onCreateIndicator?: () => void
  /**
   * Focus guide (arriving from DASH's View indicator): the rest of the sheet dims, Your indicators stays lit with a
   * one-line tooltip above it and a ✕. ✕ (or picking one) ends it. Shown once only.
   */
  guide?: boolean
  /** The open group, when the screen keeps it (Settings brings a Cancel / Apply dock to the sheet). Default: Indicators. */
  section?: ToolsSection
  onSectionChange?: (section: ToolsSection) => void
  /** Settings: the draft being edited, its change, and the ⓘ after Breakeven line. */
  settings?: ChartSettings
  onSettingsChange?: (settings: ChartSettings) => void
  onBreakevenInfo?: () => void
}

/**
 * Chart tools (the chart's "add" button): a Side nav of tool groups on the left, the chosen group on the right. Only
 * Indicators is built, in the live app's states:
 * - nothing on the chart: "Indicators" · search;
 * - some on the chart: "Indicators (2)" · bin (take all off) · fx with the count · search; each one on the chart is a
 *   blue row with ✕ — tapping a row adds or removes it, several at once;
 * - search: a search field takes the title's place, the list filters as you type, the sheet opens to full height.
 * Your indicators ("Made with DASH AI" under the heading; or "No indicators created yet.") and Create indicator sit above
 * Lemonn indicators. An indicator made with DASH is a favourite from the start (filled star).
 */
export function ChartToolsSheet({ yourIndicators, applied, onToggle, onClearAll, onCreateIndicator, guide = false, settings, onSettingsChange, onBreakevenInfo, ...props }: ChartToolsSheetProps) {
  const [ownSection, setOwnSection] = useState<ToolsSection>('indicators')
  const section = props.section ?? ownSection
  const setSection = (next: ToolsSection) => {
    setOwnSection(next)
    props.onSectionChange?.(next)
  }
  const [guiding, setGuiding] = useState(() => guide && !guideSeen())
  // Shown once: as soon as it's up, it's remembered (prototype: in this browser).
  useEffect(() => { if (guiding) markGuideSeen() }, [guiding])
  const [searching, setSearching] = useState(false)
  const [query, setQuery] = useState('')
  const title = t(`tools.${section}`)
  const count = applied.length
  const toggle = (name: string) => {
    setGuiding(false)
    onToggle(name)
  }

  // Your indicators: a long press (½ s) opens its details sheet instead of adding / removing it.
  const [details, setDetails] = useState<string | null>(null)
  const pressTimer = useRef<number | undefined>(undefined)
  const longPressed = useRef(false)
  const root = useRef<HTMLDivElement>(null)
  const longPress = (name: string) => ({
    onPointerDown: () => {
      longPressed.current = false
      window.clearTimeout(pressTimer.current)
      pressTimer.current = window.setTimeout(() => {
        longPressed.current = true
        setDetails(name)
      }, LONG_PRESS_MS)
    },
    onPointerUp: () => window.clearTimeout(pressTimer.current),
    onPointerLeave: () => window.clearTimeout(pressTimer.current),
    onPointerCancel: () => window.clearTimeout(pressTimer.current),
    onContextMenu: (e: { preventDefault: () => void }) => e.preventDefault(),
    // the click that ends a long press doesn't also toggle the row
    onClickCapture: (e: { stopPropagation: () => void; preventDefault: () => void }) => {
      if (!longPressed.current) return
      longPressed.current = false
      e.stopPropagation()
      e.preventDefault()
    },
  })

  // "Made with DASH AI" ⇄ "Long press for more options" under Your indicators, every 3 s.
  const hints = [t('tools.byDash'), t('tools.longPressHint')]
  const [hint, setHint] = useState(0)
  useEffect(() => {
    if (!yourIndicators.length) return
    const id = window.setInterval(() => setHint((h) => (h + 1) % hints.length), HINT_MS)
    return () => window.clearInterval(id)
  }, [yourIndicators.length, hints.length])

  const row = (name: string, description?: string, wrap = false) => {
    const on = applied.includes(name)
    const mine = yourIndicators.includes(name)
    const cell = (
      <ListCell
        key={name}
        variant="card"
        size="sm"
        multiline={wrap}
        label={name}
        description={description}
        iconLeft={<Icon icon={yourIndicators.includes(name) ? msStarFill : msStar} className={styles.star} />}
        iconRight={on ? <Icon icon={msClose} /> : undefined}
        selected={on}
        onClick={() => toggle(name)}
        className={styles.row}
      />
    )
    return mine ? <div key={name} className={styles.pressable} {...longPress(name)}>{cell}</div> : cell
  }

  const q = query.trim().toLowerCase()
  const results = [...yourIndicators, ...lemonnIndicators].filter((name) => name.toLowerCase().includes(q))

  return (
    <div ref={root} className={styles.body} data-search={searching || undefined}>
      {guiding && <div className={styles.dim} aria-hidden="true" />}
      <SideNav<ToolsSection>
        selectedTone="discover"
        aria-label={t('scalper.chartTools')}
        aria-controls="chart-tools-panel"
        value={section}
        onChange={setSection}
        flagTone="zing"
        className={styles.nav}
        items={[
          { value: 'range', label: t('tools.range'), icon: <Icon icon={msSpaceBar} /> },
          { value: 'zing', label: t('tools.zing'), icon: <Icon icon={msSwapHoriz} />, flag: t('tools.new') },
          { value: 'indicators', label: t('tools.indicators'), icon: <Icon icon={msFunction} /> },
          { value: 'drawings', label: t('tools.drawings'), icon: <Icon icon={msDraw} /> },
          { value: 'templates', label: t('tools.templates'), icon: <Icon icon={msBookmarkFill} /> },
          { value: 'settings', label: t('tools.settings'), icon: <Icon icon={msSettings} /> },
        ]}
      />
      <section id="chart-tools-panel" className={styles.panel} role="tabpanel" aria-label={title}>
        <div className={styles.header}>
        {section === 'indicators' && searching ? (
          <TextField
            autoFocus
            value={query}
            onChange={(e) => setQuery(e.target.value)}
            placeholder={t('tools.searchPlaceholder')}
            aria-label={t('tools.search', { section: title })}
            iconLeft={<Icon icon={msSearch} />}
            iconRight={<Button variant="ghost" size="sm" iconLeft={<Icon icon={msClose} />} aria-label={t('tools.closeSearch')} onClick={() => { setSearching(false); setQuery('') }} />}
            className={styles.search}
          />
        ) : (
          <Stack direction="horizontal" align="center" justify="between" gap="12" className={styles.titleRow}>
            <h2 className={styles.title}>{section === 'indicators' && count ? t('tools.indicatorsCount', { count }) : title}</h2>
            <Stack direction="horizontal" align="center" gap="16">
              {section === 'indicators' && count > 0 && (
                <>
                  <Button variant="ghost" size="sm" iconLeft={<Icon icon={msDelete} />} aria-label={t('tools.clearAll')} onClick={onClearAll} className={styles.headerIcon} />
                  <Badge count={count} color="discover" label={t('tools.onChart')}>
                    <Button variant="tertiary" size="sm" iconLeft={<Icon icon={msFunction} />} aria-label={t('tools.onChartList', { count })} className={styles.fx} />
                  </Badge>
                </>
              )}
              <Button variant="ghost" size="sm" iconLeft={<Icon icon={msSearch} />} aria-label={t('tools.search', { section: title })} onClick={() => section === 'indicators' && setSearching(true)} className={styles.headerIcon} />
            </Stack>
          </Stack>
        )}
        </div>

        {section === 'settings' && settings && onSettingsChange ? (
          <ChartSettingsPanel value={settings} onChange={onSettingsChange} onBreakevenInfo={() => onBreakevenInfo?.()} />
        ) : section !== 'indicators' ? (
          <p className={styles.empty}>{t('tools.soon')}</p>
        ) : searching ? (
          results.length ? <Stack gap="12">{results.map((name) => row(name, undefined, true))}</Stack> : <p className={styles.empty}>{t('tools.noResults', { query })}</p>
        ) : (
          <Stack gap="24">
            <div className={styles.yours} data-lit={guiding || undefined}>
              <Tooltip open={guiding} content={t('tools.guideTip')} placement="bottom" onClose={() => setGuiding(false)}>
                <Stack as="section" gap="12" aria-label={t('tools.yours')}>
                  <Stack direction="horizontal" align="center" justify="between" className={styles.sectionHead}>
                    <Stack gap="00">
                      <h3 className={styles.subTitle}>{t('tools.yours')}</h3>
                      <p className={styles.subDescription} aria-live="polite">
                        <span key={hint} className={styles.hint}>{yourIndicators.length ? hints[hint] : t('tools.byDash')}</span>
                      </p>
                    </Stack>
                    <Button variant="tertiary" size="sm" iconLeft={<Icon icon={msAdd} />} aria-label={t('tools.createLabel')} onClick={onCreateIndicator}>{t('tools.create')}</Button>
                  </Stack>
                  {yourIndicators.length ? <Stack gap="12">{yourIndicators.map((name) => row(name))}</Stack> : <p className={styles.empty}>{t('tools.none')}</p>}
                </Stack>
              </Tooltip>
            </div>
            <Stack as="section" gap="12" aria-label={t('tools.lemonn')}>
              <h3 className={styles.subTitle}>{t('tools.lemonn')}</h3>
              <Stack gap="12">{lemonnIndicators.map((name) => row(name))}</Stack>
            </Stack>
          </Stack>
        )}
      </section>
      {details && (
        <IndicatorDetailsSheet
          name={details}
          onChart={applied.includes(details)}
          onToggle={() => onToggle(details)}
          onOpenInDash={() => {
            setDetails(null)
            onCreateIndicator?.()
          }}
          onClose={() => setDetails(null)}
          // Inside the Chart tools sheet's own layer, so it opens on top of it (over the same phone screen).
          container={root.current?.closest<HTMLElement>('[role="dialog"]')?.parentElement ?? undefined}
        />
      )}
    </div>
  )
}

/** Long press to open an indicator's details; how often the hint under Your indicators changes. */
const LONG_PRESS_MS = 500
const HINT_MS = 3000

/** The Your indicators guide shows once per person (here: once per browser). */
const GUIDE_KEY = 'fno.yourIndicatorsGuideSeen'
function guideSeen() {
  try { return localStorage.getItem(GUIDE_KEY) === '1' } catch { return false }
}
function markGuideSeen() {
  try { localStorage.setItem(GUIDE_KEY, '1') } catch { /* storage off: it may show again next visit */ }
}
```

### `src/flows/fno/sheets/HomeSheets.tsx`

```tsx
import { useId, useState } from 'react'
import { BottomSheetHeader } from '@l3/components/BottomSheet'
import { Button } from '@l3/components/Button'
import { ButtonGroup } from '@l3/components/ButtonGroup'
import { Inset } from '@l3/components/Inset'
import { ListCell } from '@l3/components/ListCell'
import { PriceChange } from '@l3/components/PriceChange'
import { Radio } from '@l3/components/Checkbox'
import { Stack } from '@l3/components/Stack'
import { TextField } from '@l3/components/TextField'
import { inr } from '../../../shared/data/format'
import { Sheet } from '../../../shared/ui/Sheet'
import { t } from '../copy'
import type { Contract } from '../data'

export function ChoiceSheet({ title, values, value, onPick, onClose }: { title: string; values: string[]; value: string; onPick: (v: string) => void; onClose: () => void }) {
  const id = useId()
  return <Sheet labelledBy={id} onClose={onClose} header={<BottomSheetHeader heading={title} headingId={id} />}><Inset paddingInline="16" paddingBlock="16"><Stack>{values.map((v) => <ListCell key={v} as="label" label={v} trailing={<Radio name={id} checked={v === value} onChange={() => { onPick(v); onClose() }} />} />)}</Stack></Inset></Sheet>
}

export function CreateWatchlistSheet({ onCreate, onClose }: { onCreate: (name: string) => void; onClose: () => void }) {
  const [name, setName] = useState('')
  const id = useId()
  return <Sheet labelledBy={id} onClose={onClose} header={<BottomSheetHeader heading={t('watchlists.create')} headingId={id} />} footer={<ButtonGroup aria-label={t('watchlists.create')}><Button disabled={!name.trim()} onClick={() => onCreate(name.trim())}>{t('watchlists.create')}</Button></ButtonGroup>}><Inset paddingInline="16" paddingBlock="24"><TextField label={t('watchlists.name')} value={name} onChange={(e) => setName(e.target.value)} maxLength={40} /></Inset></Sheet>
}

export function DetailSheet({ title, contract, onClose }: { title: string; contract?: Contract; onClose: () => void }) {
  const id = useId()
  return <Sheet labelledBy={id} onClose={onClose} header={<BottomSheetHeader heading={title} description={contract?.description ?? t('prototype.description')} headingId={id} />} footer={<ButtonGroup aria-label={title}><Button onClick={onClose}>{t('close')}</Button></ButtonGroup>}>
    {contract && <Inset paddingInline="16" paddingBlock="16"><Stack><ListCell label={t('contract.price')} trailing={inr(contract.price, 2)} /><ListCell label={t('contract.change')} trailing={<PriceChange value={contract.change} unit="percent" size="sm" />} /><ListCell label={t('contract.volume')} trailing={contract.volume.toLocaleString('en-IN')} /></Stack></Inset>}
  </Sheet>
}
```

### `src/flows/fno/sheets/IlliquidSheet.tsx`

```tsx
import { IlliquidSheet as SharedIlliquidSheet } from '../../../shared/ui/IlliquidSheet'
import { t } from '../copy'

/** F&O's “What does illiquidity mean?” sheet: the shared sheet with this flow's words. */
export function IlliquidSheet({ contract, onClose }: { contract?: string; onClose: () => void }) {
  return <SharedIlliquidSheet onClose={onClose} copy={{
    title: t('illiquid.title'),
    description: contract ? t('illiquid.forContract', { contract }) : t('illiquid.general'),
    points: [t('illiquid.point1'), t('illiquid.point2'), t('illiquid.point3')],
    ok: t('illiquid.ok'),
  }} />
}
```

### `src/flows/fno/sheets/IndicatorDetailsSheet.tsx`

```tsx
import { useId } from 'react'
import { BottomSheet, BottomSheetHeader } from '@l3/components/BottomSheet'
import { Button } from '@l3/components/Button'
import { ButtonGroup } from '@l3/components/ButtonGroup'
import { Icon } from '@l3/components/Icon'
import { ListCell } from '@l3/components/ListCell'
import { Switch } from '@l3/components/Switch'
import { msStarFill } from '@l3/icons/material'
import { t } from '../copy'
import styles from './ChartToolsSheet.module.css'

/**
 * Your indicator's details, from a long press on it in Chart tools: the large header (★ on a tile, its name, "Made
 * with DASH AI"), one switch card — Show on chart (adds / removes it, like a tap on its row) — and Open in DASH (to
 * change it) / Done. Opens over the Chart tools sheet, inside the phone.
 */
export function IndicatorDetailsSheet({ name, onChart, onToggle, onOpenInDash, onClose, container }: {
  name: string
  onChart: boolean
  onToggle: () => void
  onOpenInDash?: () => void
  onClose: () => void
  container?: HTMLElement | null
}) {
  const id = useId()
  return (
    <BottomSheet
      open
      onClose={onClose}
      container={container}
      aria-labelledby={id}
      header={<BottomSheetHeader size="lg" headingId={id} heading={name} description={t('tools.byDash')} icon={<span className={styles.detailsIcon}><Icon icon={msStarFill} size={24} /></span>} />}
      footer={
        <ButtonGroup aria-label={name} direction="horizontal">
          <Button variant="secondary" onClick={onClose}>{t('tools.detailsDone')}</Button>
          <Button onClick={onOpenInDash}>{t('tools.openInDash')}</Button>
        </ButtonGroup>
      }
    >
      <ListCell
        variant="card"
        as="label"
        label={t('tools.showOnChart')}
        description={onChart ? t('tools.isOnChart') : t('tools.notOnChart')}
        trailing={<Switch checked={onChart} onChange={onToggle} aria-label={t('tools.showOnChart')} />}
      />
    </BottomSheet>
  )
}
```

### `src/flows/fno/sheets/SignalStrip.module.css`

```css
/*
 * The nudge strip over a commodity signal's card (SignalStrip.tsx), after Figma 6946:42446 ("Commodities nudge") and its
 * improved gradient 6947:45037 (24 Nov), file 9r61YQp7QQZAQovDyz8hLF: a 28 strip behind the card's top edge, warm in its
 * top-left corner (halfway zing light → honey 200) fading to zing light 64 across; a 1 gold ring round strip and card
 * (zing light at the top → honey 300 at the bottom); the gold bars (18) on a soft white glow 16 in, a Heading/10 +
 * Label/10 line in honey 800.
 */

/* The strip's colours, per version (s2: per commodity). */
.nudge {
  --strip-from: var(--l3-surface-accent-zing-light);
  --strip-to: var(--l3-border-accent-zing-light);
  --strip-ink: var(--app-strip-gold-ink);
  --strip-shine: var(--app-strip-shine);
  --strip-shine-core: var(--app-strip-shine-core);
  /* The ring's bottom colour (Figma frame stroke: zing light → honey 300). */
  --strip-ring: var(--l3-border-accent-zing-default);
  position: relative;
  /* The ring: Figma's 1 stroke round strip and card. It sits just outside the card (padding 1, margin −1), so the card
     keeps its exact size and place when the strip is switched on — only the strip grows in above it. */
  padding: 1px;
  margin: -1px;
  border-radius: calc(var(--l3-radius-12) + 1px);
}
/* The ring (and what shows behind the card's corners): the strip's colour deepening to the ring colour at the bottom. */
.ring {
  position: absolute;
  inset: 0;
  border-radius: inherit;
  background: linear-gradient(180deg, var(--strip-from), var(--strip-ring));
}
.nudge[data-commodity='crude'], .nudge[data-commodity='silver'] {
  --strip-from: var(--l3-surface-secondary);
  --strip-to: var(--l3-border-intense);
  --strip-ring: var(--l3-border-intense);
  --strip-ink: var(--l3-content-primary);
}
.nudge[data-commodity='gas'] {
  --strip-from: var(--l3-surface-accent-orange-light);
  --strip-to: var(--l3-border-accent-orange-light);
  --strip-ring: var(--l3-border-accent-orange-default);
  --strip-ink: var(--app-strip-orange-ink);
}
.nudge[data-version='s3'] {
  --strip-from: var(--l3-surface-inverted);
  --strip-to: var(--l3-surface-inverted);
  --strip-ring: var(--l3-surface-inverted);
  --strip-ink: var(--app-strip-ticker-ink);
  --strip-shine: var(--app-strip-shine-dark);
  --strip-shine-core: var(--app-strip-shine-dark);
}

/* Entry, once the sheet is up (its own slide takes ~400): the strip slides out from behind the card (its row grows
   0 → 28), one card after another; then its line rises in; then the shimmer starts. */
.nudge { --strip-start: calc(var(--l3-motion-duration-long) + var(--l3-motion-duration-medium) + var(--strip-order, 0) * var(--l3-motion-duration-medium)); }
/*
 * The strip runs on 12 under the card (as Figma's 48 strip under the card from 28), so the card's rounded top corners
 * sit on the strip's colour — no notch where they curve away. It takes 27 of the layout (28 from the ring's outer edge).
 */
.reveal {
  position: relative;
  height: calc(var(--l3-size-28) - 1px + var(--l3-radius-12));
  margin-bottom: calc(-1 * var(--l3-radius-12));
  overflow: hidden;
  border-radius: calc(var(--l3-radius-12) - 1px) calc(var(--l3-radius-12) - 1px) 0 0;
  animation: strip-reveal var(--l3-motion-duration-long) var(--l3-motion-easing-decelerate) both;
  animation-delay: var(--strip-start);
}
@keyframes strip-reveal { from { height: var(--l3-radius-12); } }
/* The ring fades in as the strip comes out. */
.ring { animation: strip-ring var(--l3-motion-duration-long) var(--l3-motion-easing-decelerate) both; animation-delay: var(--strip-start); }
@keyframes strip-ring { from { opacity: 0; } }
/* Switched on while the sheet is up: no wait for the sheet's slide, just the top-down stagger. */
.nudge[data-switched='true'] { --strip-start: calc(var(--strip-order, 0) * var(--l3-motion-duration-short)); }

/* Switched off: the reverse — the line fades, the strip tucks back behind the card (27 → 0 seen) and the ring fades,
   then the strip goes (LEAVE_MS in SignalStrip.tsx = duration long). The card slides up with it. */
.nudge[data-leaving='true'] .reveal { animation: strip-hide var(--l3-motion-duration-long) var(--l3-motion-easing-standard) forwards; }
@keyframes strip-hide { from { height: calc(var(--l3-size-28) - 1px + var(--l3-radius-12)); } to { height: var(--l3-radius-12); } }
.nudge[data-leaving='true'] .ring { animation: strip-ring-out var(--l3-motion-duration-long) var(--l3-motion-easing-standard) forwards; }
@keyframes strip-ring-out { from { opacity: 1; } to { opacity: 0; } }
.nudge[data-leaving='true'] .strip > * { animation: strip-fade-out var(--l3-motion-duration-medium) var(--l3-motion-easing-accelerate) forwards; }
@keyframes strip-fade-out { from { opacity: 1; } to { opacity: 0; } }

.strip {
  position: relative;
  display: flex;
  align-items: center;
  gap: var(--l3-spacing-08);
  min-height: 0;
  height: 100%;
  padding: 0 var(--l3-spacing-12) var(--l3-radius-12) var(--l3-spacing-16); /* the line stays centred in the 27 seen */
  overflow: hidden;
  border-radius: inherit;
  /* Figma 6947:45038 "top strip": warm in the top-left corner (halfway between the two honeys), fading to zing light
     64 across (its gradient runs down-right at ~138°). */
  background: linear-gradient(138deg, color-mix(in srgb, var(--strip-from), var(--strip-to)) 0, var(--strip-from) var(--l3-size-64));
  color: var(--strip-ink);
}
.strip > :not(.shimmer) {
  animation: strip-rise var(--l3-motion-duration-long) var(--l3-motion-easing-decelerate) both;
  animation-delay: calc(var(--strip-start) + var(--l3-motion-duration-medium));
}
@keyframes strip-rise { from { opacity: 0; transform: translateY(var(--l3-spacing-06)); } }

/* The picture on a soft white glow under it (Figma Ellipse 6835: 29 × 8, white 50%). */
.glow {
  position: relative;
  display: inline-flex;
  flex: none;
  width: var(--l3-icon-size-18);
  height: var(--l3-icon-size-18);
}
.glow[data-glow='true']::before {
  content: '';
  position: absolute;
  left: 50%;
  bottom: calc(-1 * var(--l3-spacing-02));
  width: var(--app-strip-glow-width);
  height: var(--l3-size-08);
  translate: -50% 0;
  border-radius: var(--l3-radius-full);
  background: var(--app-strip-glow);
  filter: blur(var(--l3-spacing-02));
}
.picture { position: relative; display: block; width: 100%; height: 100%; object-fit: contain; border-radius: var(--l3-radius-full); }
.nudge:not([data-version='s2']) .picture { border-radius: 0; }
.fire { position: relative; color: var(--l3-content-accent-orange-default); }
/* s4's move line: a trend arrow (up or down) in the strip's text colour (honey 800 on gold). */
.trend { position: relative; color: var(--strip-ink); }

.text {
  flex: 1;
  min-width: 0;
  margin: 0;
  font: var(--l3-text-label-10);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.text b { font-weight: var(--l3-text-heading-10-weight); }

/* s2: a pulsing Live dot on the right. */
.live {
  display: inline-flex;
  align-items: center;
  gap: var(--l3-spacing-04);
  flex: none;
  font: var(--l3-text-heading-10);
}
.liveDot {
  position: relative;
  width: var(--l3-spacing-06);
  height: var(--l3-spacing-06);
  border-radius: var(--l3-radius-full);
  background: var(--l3-content-accent-indicator-up-default);
}
.liveDot::after {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: inherit;
  background: inherit;
  animation: strip-pulse 1.6s var(--l3-motion-easing-decelerate) infinite;
}
@keyframes strip-pulse { to { transform: scale(2.6); opacity: 0; } }

/* s4: one line at a time, the next rising from below (its picture too). */
.rotorPic { position: relative; display: inline-flex; width: 100%; height: 100%; align-items: center; justify-content: center; animation: strip-rise var(--l3-motion-duration-long) var(--l3-motion-easing-decelerate) both; }
.rotorLine { display: block; overflow: hidden; text-overflow: ellipsis; animation: strip-rise var(--l3-motion-duration-long) var(--l3-motion-easing-decelerate) both; }
.move { color: var(--l3-content-accent-indicator-down-default); }
.move[data-up='true'] { color: var(--l3-content-accent-indicator-up-default); }

/* The shimmer: a soft light band sweeping left → right across the strip, every 3 s once it's out. */
.shimmer {
  position: absolute;
  inset: 0;
  pointer-events: none;
  background: linear-gradient(105deg, transparent 36%, var(--strip-shine) 46%, var(--strip-shine-core) 50%, var(--strip-shine) 54%, transparent 64%);
  background-size: 300% 100%;
  background-repeat: no-repeat;
  background-position: 100% 0;
  animation: strip-shimmer 3s var(--l3-motion-easing-standard) infinite;
  animation-delay: calc(var(--strip-start) + var(--l3-motion-duration-long) * 2);
}
@keyframes strip-shimmer {
  0% { background-position: 100% 0; }
  40%, 100% { background-position: 0% 0; }
}

/* The card sits on the strip's lower part, as in Figma (it covers the gradient's last 21). */
.nudge > :last-child { position: relative; }

@media (prefers-reduced-motion: reduce) {
  .reveal, .ring, .strip > *, .rotorLine, .rotorPic, .shimmer, .liveDot::after { animation: none; }
}
```

### `src/flows/fno/sheets/SignalStrip.tsx`

```tsx
import { useEffect, useRef, useState, type CSSProperties, type ReactNode } from 'react'
import { Icon } from '@l3/components/Icon'
import { msLocalFireDepartmentFill, msTrendingDown, msTrendingUp } from '@l3/icons/material'
import { t } from '../copy'
import type { ZingSignal } from '../data'
import goldBars from '../assets/signals/gold-bars.png'
import styles from './SignalStrip.module.css'

/**
 * The nudge strip over a commodity signal's card (setting "Commodity nudge strip", Figma 6946:42446, 24 Nov): the
 * commodity cards didn't stand out enough among index and stock signals, so a strip peeks out from behind the card's
 * top edge with a reason to look — how many traded it today. It slides out from behind the card when the sheet opens,
 * then a shimmer runs across it every few seconds.
 * - s1 Gold glow (Figma): the honey gradient strip, the gold bars on a soft white glow, "2.1K+ people have traded on
 *   gold today" in honey 800.
 * - s2 Colour per commodity: as s1, but the strip takes the commodity's colour (gold honey, crude oil slate, natural gas
 *   tangerine), its logo, and a pulsing Live dot on the right.
 * - s3 Dark ticker: the strip in the inverted surface, a flame, "Trending on MCX · 2.1K+ traded today" in honey.
 * - s4 Rotating facts: s1's strip, no shimmer; its line (and its picture) turns over every 5 s — traded today · trending on MCX
 *   (the flame, as s3) · today's move (a trend arrow in the strip's text colour) · MCX hours.
 */
export type StripVersion = 'off' | 's1' | 's2' | 's3' | 's4'

/** How long the strip takes to tuck back behind the card when it's switched off (= --l3-motion-duration-long). */
const LEAVE_MS = 400

export function SignalStrip({ signal, version: wanted, logo, order, children }: { signal: ZingSignal; version: StripVersion; logo: string; order: number; children: ReactNode }) {
  // The version on screen. Switched off, the strip first tucks back behind the card (LEAVE_MS), then goes.
  const [version, setVersion] = useState(wanted)
  const [leaving, setLeaving] = useState(false)
  // Changed while the sheet is already up: the strip comes out straight away (no wait for the sheet's own slide).
  const [switched, setSwitched] = useState(false)
  const first = useRef(true)
  useEffect(() => {
    if (first.current) { first.current = false; return }
    setSwitched(true)
    if (wanted === 'off' && version !== 'off') {
      setLeaving(true)
      // Gone once the tuck-back animation ends (onAnimationEnd below); this is only the fallback.
      const id = window.setTimeout(() => { setVersion('off'); setLeaving(false) }, LEAVE_MS + 200)
      return () => window.clearTimeout(id)
    }
    setLeaving(false)
    setVersion(wanted)
  }, [wanted]) // only when the setting changes

  const nudge = signal.nudge
  const commodity = signal.commodity
  if (!nudge || !commodity) return <>{children}</>
  // Off: the same wrapper (so the card is never rebuilt), with no strip and no ring.
  if (version === 'off') return <div className={styles.nudge} data-version="off">{children}</div>
  const name = t(`signals.strip.name.${commodity}`)
  const people = t('signals.strip.people', { count: nudge.traders })
  const traded = <><b>{people}</b> {t('signals.strip.traded', { name })}</>

  const flame = <Icon icon={msLocalFireDepartmentFill} size={16} className={styles.fire} />
  // The gold bars sit on Figma's soft white glow; logos and icons don't.
  const bars = version !== 's2' && commodity === 'gold'
  const picture = version === 's3'
    ? flame
    : <img src={bars ? goldBars : logo} alt="" className={styles.picture} />
  const up = !nudge.move.startsWith('−')
  const trendIcon = <Icon icon={up ? msTrendingUp : msTrendingDown} size={16} className={styles.trend} />

  const trending = <><b>{t('signals.strip.trending')}</b> · {t('signals.strip.tradedShort', { count: nudge.traders })}</>
  const line = version === 's3' ? trending : traded

  return (
    <div className={styles.nudge} data-version={version} data-leaving={leaving} data-switched={switched} data-commodity={version === 's2' ? commodity : undefined} style={{ '--strip-order': order } as CSSProperties}>
      <span className={styles.ring} aria-hidden="true" />
      <div className={styles.reveal} onAnimationEnd={(e) => { if (leaving && e.target === e.currentTarget) { setVersion('off'); setLeaving(false) } }}>
        {/* Keyed by version: switching between versions, the new one's picture and line rise in. */}
        <div key={version} className={styles.strip}>
          {version === 's4' ? (
            <Rotating items={[
              { picture, glow: bars, line: traded },
              { picture: flame, line: trending },
              { picture: trendIcon, line: <>{t('signals.strip.moveIs', { name: t(`signals.strip.title.${commodity}`) })} <b className={styles.move} data-up={up}>{nudge.move}</b> {t('signals.strip.today')}</> },
              { picture, glow: bars, line: <>{t('signals.strip.open')}</> },
            ]} />
          ) : (
            <>
              <span className={styles.glow} data-glow={bars && version !== 's3'} aria-hidden="true">{picture}</span>
              <p className={styles.text}>{line}</p>
            </>
          )}
          {version === 's2' && <span className={styles.live}><span className={styles.liveDot} aria-hidden="true" />{t('signals.strip.live')}</span>}
          {/* No shimmer on Rotating facts: its lines already move (user, 24 Nov). */}
          {version !== 's4' && <span className={styles.shimmer} aria-hidden="true" />}
        </div>
      </div>
      {children}
    </div>
  )
}

/** s4: how long each line stays before the next rolls up. */
const ROTATE_MS = 5000

/**
 * s4: one line at a time (with its picture), the next rolling up from below every 5 s. The picture's box stays put
 * (only what's inside it changes), so the new picture comes in with its line — not after the strip's entry delay.
 */
function Rotating({ items }: { items: { picture: ReactNode; glow?: boolean; line: ReactNode }[] }) {
  const [index, setIndex] = useState(0)
  useEffect(() => {
    const id = window.setInterval(() => setIndex((i) => (i + 1) % items.length), ROTATE_MS)
    return () => window.clearInterval(id)
  }, [items.length])
  const item = items[index]
  return <>
    <span className={styles.glow} data-glow={Boolean(item.glow)} aria-hidden="true">
      <span key={index} className={styles.rotorPic}>{item.picture}</span>
    </span>
    <p className={styles.text} aria-live="polite">
      <span key={index} className={styles.rotorLine}>{item.line}</span>
    </p>
  </>
}
```

### `src/flows/fno/sheets/SignalsSheet.module.css`

```css
/*
 * Zing signals sheet (SignalsSheet.tsx) and its filter sheet, after Figma 6900:23853 ("Enrich signal filter",
 * file 9r61YQp7QQZAQovDyz8hLF) in L3 tokens.
 */

/* One height however many signals there are: 75% of the phone screen (user, 20 Nov; the screen is a size container —
   Screen.module.css); the list scrolls inside it. */
.sheet.sheet { height: 75cqh; }

/* The chip row in the sheet header's place: the filter button | the chips (they scroll sideways), a line under it. */
.chipBar {
  position: relative;
  display: flex;
  align-items: center;
  gap: var(--l3-spacing-12);
  padding: var(--l3-spacing-12) 0 var(--l3-spacing-12) var(--l3-spacing-16);
  box-shadow: inset 0 -1px 0 var(--l3-border-light); /* 1px: Figma stroke weight has no variable */
}
.chipBar > :last-child { min-width: 0; flex: 1; }
.chips { padding-right: var(--l3-spacing-16); }
/* Chips not picked: Label/12 in text secondary (user, 20 Nov). */
.chips [role='tab'][aria-selected='false'] { --tab-content: var(--l3-content-secondary); }
.chipLogo { display: block; width: 100%; height: 100%; border-radius: var(--l3-radius-full); object-fit: cover; }
/* The filter button: a round bordered pill like the chips (Figma: 32, border-intense, elevation low). */
.filterButton.filterButton { flex: none; --btn-radius: var(--l3-radius-full); }
/* View: Figma's fixed 60 wide. */
.view.view { min-width: calc(var(--l3-size-56) + var(--l3-size-04)); }
.divider {
  flex: none;
  width: 1px; /* hairline */
  height: var(--l3-size-20);
  background: var(--l3-border-light);
}
/* The flame on Win rate ≥ 50% (Figma: orange). */
.fire { color: var(--l3-content-accent-orange-default); }
.chipsWrap { min-width: 0; }
/*
 * The saved-filter tip points at Your filter: its anchor sits over the first chip (16 + the 32 filter button + 12 + the
 * 1 line + 12 in; the chip's own width), so the arrow lands under it as in Figma (6900:31347).
 */
.tip.tip {
  position: absolute;
  top: var(--l3-spacing-12);
  left: calc(var(--l3-spacing-16) + var(--l3-size-32) + var(--l3-spacing-24) + 1px); /* 1px: the divider hairline */
  pointer-events: none;
}
.tipTarget { display: block; width: calc(var(--l3-size-128) - var(--l3-size-16)); height: var(--l3-size-32); }
/* Figma's tip: discover blue, white Label/12 on one line, 8 / 12 · 8 inside, 4 to the ✕, radius 8, a soft shadow.
   L3's tooltip is the dark inverted bubble with Description/12 (L3 gap: no discover tone). */
.tip.tip [role='tooltip'] {
  --tt-surface: var(--l3-surface-accent-discover-default);
  pointer-events: auto;
  gap: var(--l3-spacing-04);
  max-width: none;
  padding: var(--l3-spacing-08) var(--l3-spacing-08) var(--l3-spacing-08) var(--l3-spacing-12);
  color: var(--l3-static-white);
  font: var(--l3-text-label-12);
  white-space: nowrap;
  box-shadow: var(--l3-shadow-elevation-medium);
}
.tip.tip [role='tooltip'] > span:first-child { padding: 0; }
.chipClose { display: inline-flex; width: var(--l3-size-16); height: var(--l3-size-16); cursor: pointer; }

.body { display: block; }

.heading {
  margin: 0;
  font: var(--l3-text-heading-14);
  color: var(--l3-content-primary);
}
.totalLabel, .pnlLabel { color: var(--l3-content-primary); }
.pnlLabel { color: var(--l3-content-secondary); }

/* A signal card: a smooth drop shadow under its edge (user, 20 Nov) — L3 elevation low (close) + soft (wide). */
.signalCard.signalCard { box-shadow: var(--card-border), var(--l3-shadow-elevation-low), var(--l3-shadow-elevation-soft); }
/* A signal card. */
.who { min-width: 0; flex: 1; }
.name {
  margin: 0;
  font: var(--l3-text-heading-12);
  color: var(--l3-content-primary); /* the strategy name in text primary (user, 20 Nov) */
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
/* Grey tags (market, win rate) read in text secondary (user, 20 Nov; L3's neutral tag is text primary). */
.greyTag.greyTag { --tag-content: var(--l3-content-secondary); }
.up { font-weight: var(--l3-text-heading-10-weight); color: var(--l3-content-accent-indicator-up-default); }
/* The trade, under a line: Buy Call 23950 • RR 1.4 • EMA 9 > EMA 21, spread across the card. */
.trade {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: var(--l3-spacing-08);
  padding-top: var(--l3-spacing-08);
  box-shadow: inset 0 1px 0 var(--l3-border-light); /* 1px: Figma stroke weight has no variable */
  font: var(--l3-text-label-12);
  color: var(--l3-content-primary);
  white-space: nowrap;
}
.muted { color: var(--l3-content-tertiary); }
.dot {
  flex: none;
  width: var(--l3-size-04);
  height: var(--l3-size-04);
  border-radius: var(--l3-radius-full);
  background: var(--l3-border-intense);
}

/* ---- Filter: the chart tools sheet's layout (ChartToolsSheet.module.css .body / .nav / .panel / .header) ---- */
/* The sheet brings its own layout: no content padding (as the Scalper's chart tools sheet). */
.toolsSheet.toolsSheet.toolsSheet [data-sheet-content] { padding: 0; }
.toolsSheet.toolsSheet.toolsSheet { box-shadow: var(--l3-shadow-elevation-high); }
/* The count in a side tab's corner: white on the discover blue in both modes (the tools sheet sets it for Zing yellow). */
.nav.nav.nav[data-flag-tone] { --side-nav-flag-content: var(--l3-static-white); }
/*
 * The filter is the Scalper's Settings sheet (chart tools → Settings) in look: the same side nav, white panel, title row
 * and rows (ChartToolsSheet.module.css). It stays shorter than Settings' 576: the list area is 412 (Indices' six rows
 * fit: title row 64 + 16 + 6 × 48 + 5 × 8), the picks' 44 strip under it when there are picks, then the dock.
 */
.filterGrid.filterGrid { height: calc(var(--l3-size-128) * 3 + var(--l3-size-28)); }

/* The Zing mark (Figma's own glyph), drawn in the tile's text colour like the Material icons beside it. */
.zingMark { display: block; width: var(--l3-icon-size-24); height: var(--l3-icon-size-24); } /* as the side nav's icons */
/* "Clear All" in Figma's discover blue (a text action). */
.clear.clear { --btn-content: var(--l3-content-accent-discover-default); color: var(--l3-content-accent-discover-default); }

/* The picks (Figma "applied", 44): 12 above the chips, 16 at the sides, one row that scrolls sideways. */
.pills {
  display: flex;
  gap: var(--l3-spacing-08);
  height: calc(var(--l3-size-32) + var(--l3-spacing-12));
  padding: var(--l3-spacing-12) var(--l3-spacing-16) 0;
  overflow-x: auto;
  scrollbar-width: none;
  background: var(--l3-surface-primary);
}
/* A pick is Figma's unselected pill: surface-primary, border-light, 8 inside, 4 to the ✕, Label/12 in secondary. */
.pill.pill {
  flex: none;
  --btn-radius: var(--l3-radius-full);
  --btn-surface: var(--l3-surface-primary);
  --btn-border: var(--l3-border-light);
  --btn-content: var(--l3-content-secondary);
  --btn-gap: var(--l3-spacing-04);
}
/* The ✕ (Figma "cross"): filled, in primary. */
.pillX { color: var(--l3-content-primary); }
/* A long strategy name is cut at 140 (Figma dev note "Max width: 140px"). */
.pillLabel {
  display: block;
  max-width: calc(var(--l3-size-128) + var(--l3-size-12));
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

/* ---- Commodity signals ---- */
/* Logos in tags: the tag's 12 icon slot (L3 Tag sm). */
.tagLogo { display: block; width: 100%; height: 100%; border-radius: var(--l3-radius-full); object-fit: cover; }
```

### `src/flows/fno/sheets/SignalsSheet.tsx`

```tsx
import { useState, type MouseEvent, type ReactNode } from 'react'
import { Avatar } from '@l3/components/Avatar'
import { Badge } from '@l3/components/Badge'
import { BottomSheetHeader } from '@l3/components/BottomSheet'
import { Button } from '@l3/components/Button'
import { ButtonGroup } from '@l3/components/ButtonGroup'
import { Card } from '@l3/components/Card'
import { Checkbox, Radio } from '@l3/components/Checkbox'
import { EmptyState } from '@l3/components/EmptyState'
import { Icon } from '@l3/components/Icon'
import { ListCell } from '@l3/components/ListCell'
import { MaskIcon } from '@l3/components/MaskIcon'
import { SideNav } from '@l3/components/SideNav'
import { Stack } from '@l3/components/Stack'
import { Tabs } from '@l3/components/Tabs'
import { Tag } from '@l3/components/Tag'
import { Tooltip } from '@l3/components/Tooltip'
import { msCancelFill, msFilterAltFill, msFormatListBulleted, msLocalFireDepartmentFill, msSpeed, msSwapVert } from '@l3/icons/material'
import { useFlowOption } from '../../../shared/prototype'
import { Sheet } from '../../../shared/ui/Sheet'
import { t } from '../copy'
import { filterCount, matchesFilter, noSignalFilter, signalMarkets, signalsTotalPnl, zingSignals, type SignalAvatar, type SignalCommodity, type SignalFilter, type SignalMarket, type ZingSignal } from '../data'
import goldLogo from '../commodities/assets/gold.png'
import silverLogo from '../commodities/assets/silver.png'
import crudeLogo from '../commodities/assets/crude-oil.png'
import gasLogo from '../commodities/assets/natural-gas.png'
import neeraj from '../assets/signals/neeraj.png'
import lemon from '../assets/signals/lemon.png'
import booming from '../assets/signals/booming.png'
import zingMark from '../assets/signals/zing-mark.svg'
import { SignalStrip, type StripVersion } from './SignalStrip'
import styles from './SignalsSheet.module.css'
import tools from './ChartToolsSheet.module.css'

/** The quick chips under the sheet's top edge. `yours` appears once a filter has been applied (and saved). */
export type SignalsChip = 'yours' | 'all' | 'win50' | 'win25' | 'commodity' | 'nifty' | 'sensex' | 'banknifty' | 'stocks' | SignalCommodity
/** The filter sheet's groups (its side nav). */
export type FilterSection = 'indices' | 'winRate' | 'direction' | 'strategies'

/** Where the sheet starts — the prototype's screens open it in each Figma state. */
export type SignalsSheetState = {
  chip?: SignalsChip
  /** The saved filter ("Your filter"), if one has been applied. */
  saved?: SignalFilter | null
  /** The filter, open on this group. */
  filter?: FilterSection | null
  /** The filter sheet's choices so far (before Apply). Default: the saved filter. */
  draft?: SignalFilter
  /** "Filter applied & saved for quick access", under Your filter (shows once, right after Apply). */
  savedTip?: boolean
  /** The plain "All Signals" look: a heading over every signal (Figma's last frame). */
  plain?: boolean
}

const avatars: Record<SignalAvatar, string> = { neeraj, lemon, booming }
/** The commodity logos the Commodities home uses (commodities/assets). */
const commodityLogos: Record<SignalCommodity, string> = { gold: goldLogo, silver: silverLogo, crude: crudeLogo, gas: gasLogo }

/**
 * How a commodity signal stands out from index and stock signals (24 Nov, the user's call — the earlier versions are
 * gone, and so are the segment tabs): the sheet starts with the filter button | the chips (All Signals · Win rate ≥ 50% ·
 * Nifty · Sensex · F&O Stocks · Commodities), a line under them; commodity cards have an amber tag with the
 * commodity's logo and name, and the nudge strip over them (setting "Commodity nudge strip", SignalStrip.tsx).
 */
const marketLabel = (market: SignalMarket) => t(`signals.market.${market}`)
const quick: Record<Exclude<SignalsChip, 'yours'>, (s: ZingSignal) => boolean> = {
  all: () => true,
  win50: (s) => (s.winRate ?? 0) >= 50,
  win25: (s) => (s.winRate ?? 0) >= 25,
  commodity: (s) => s.market === 'commodity',
  nifty: (s) => s.market === 'nifty',
  sensex: (s) => s.market === 'sensex',
  banknifty: (s) => s.market === 'banknifty',
  stocks: (s) => s.market === 'stocks',
  gold: (s) => s.commodity === 'gold',
  silver: (s) => s.commodity === 'silver',
  crude: (s) => s.commodity === 'crude',
  gas: (s) => s.commodity === 'gas',
}

/**
 * Zing signals (Scalper → the Active chip, top right): today's live signals from Zing strategies, across F&O — index
 * options (Nifty, Sensex, Bank Nifty), F&O stocks and commodities.
 * - The top row: the filter button, Your filter (once one is saved, ✕ removes it), All Signals, Win rate ≥ 50%, then
 *   Commodity · Nifty · Sensex. Each chip shows how many signals it holds.
 * - Active signals (n) with today's Total P&L, then one card per signal: strategy, its market and win rate (or P&L),
 *   View; under a line the trade: Buy Call 23950 · RR · the rule that fired.
 * - The filter button turns the sheet into the filter, laid out like the chart tools sheet (Indices · Win rate · Call/Put ·
 *   Strategies). Apply saves the choices as Your filter and selects it; Cancel drops them.
 */
export function SignalsSheet({ initial = {}, onClose }: { initial?: SignalsSheetState; onClose: () => void }) {
  const [saved, setSaved] = useState<SignalFilter | null>(initial.saved ?? null)
  const [chip, setChip] = useState<SignalsChip>(initial.chip ?? (initial.saved ? 'yours' : 'all'))
  const [filter, setFilter] = useState<FilterSection | null>(initial.filter ?? null)
  const [draft, setDraft] = useState<SignalFilter>(initial.draft ?? initial.saved ?? noSignalFilter)
  const [savedTip, setSavedTip] = useState(Boolean(initial.savedTip))

  const openFilter = () => {
    setDraft(saved ?? noSignalFilter)
    setSavedTip(false)
    setFilter('indices')
  }
  const apply = () => {
    const keep = filterCount(draft) ? draft : null
    setSaved(keep)
    setChip(keep ? 'yours' : 'all')
    setSavedTip(Boolean(keep))
    setFilter(null)
  }
  const removeSaved = () => {
    setSaved(null)
    setChip('all')
    setSavedTip(false)
  }

  /** The tab's press layer covers its icons, so a tap on Your filter's ✕ is caught here by where it lands. */
  const closeTap = (e: MouseEvent<HTMLDivElement>) => {
    const close = e.currentTarget.querySelector('[data-chip-close]')?.getBoundingClientRect()
    if (!close || e.clientX < close.left - 4 || e.clientX > close.right + 4 || e.clientY < close.top - 4 || e.clientY > close.bottom + 4) return
    e.stopPropagation()
    e.preventDefault()
    removeSaved()
  }
  const strip = useFlowOption('fno', 'commodityStrip', 's1') as StripVersion
  const inChip = (c: SignalsChip) => zingSignals.filter((s) => (c === 'yours' ? saved !== null && matchesFilter(s, saved) : quick[c](s)))
  const shown = inChip(chip)
  const count = (c: SignalsChip) => inChip(c).length

  // The quick chips after All Signals.
  const quickChips: Exclude<SignalsChip, 'yours' | 'all'>[] = ['win50', 'nifty', 'sensex', 'stocks', 'commodity']
  const chipItem = (c: Exclude<SignalsChip, 'yours' | 'all'>): { value: SignalsChip; label: string; iconLeft?: ReactNode } => {
    if (c === 'win50' || c === 'win25') return { value: c, label: t(`signals.${c}`, { count: count(c) }), iconLeft: <Icon icon={msLocalFireDepartmentFill} className={styles.fire} /> }
    if (c === 'gold' || c === 'silver' || c === 'crude' || c === 'gas') return { value: c, label: t(`signals.commodity.${c}`), iconLeft: <img src={commodityLogos[c]} alt="" className={styles.chipLogo} /> }
    if (c === 'commodity') return { value: c, label: t('signals.segment.commodity') }
    if (c === 'stocks') return { value: c, label: t('signals.market.stocks') }
    return { value: c, label: t(`signals.${c}`) }
  }
  const chips: { value: SignalsChip; label: string; iconLeft?: ReactNode; iconRight?: ReactNode }[] = [
    ...(saved
      ? [{
          value: 'yours' as const,
          label: t('signals.yours', { count: count('yours') }),
          // ✕ on the chip takes the saved filter off (a tap on the rest of the chip selects it): see closeTap.
          iconRight: <span data-chip-close="" className={styles.chipClose}><Icon icon={msCancelFill} size={16} /></span>,
        }]
      : []),
    { value: 'all', label: t('signals.all', { count: count('all') }) },
    ...quickChips.map((c) => chipItem(c)),
  ]

  const chipBar = (
    <div className={styles.chipBar}>
      <Badge dot={Boolean(saved)} color="error" label={t('signals.filterOn')}>
        <Button variant="tertiary" size="sm" iconLeft={<Icon icon={msFilterAltFill} />} aria-label={t('signals.filter')} onClick={openFilter} className={styles.filterButton} />
      </Badge>
      <span className={styles.divider} aria-hidden="true" />
      <div onClickCapture={closeTap} className={styles.chipsWrap}>
        <Tabs aria-label={t('signals.chips')} appearance="pill" size="md" value={chip} onChange={setChip} items={chips} className={styles.chips} />
      </div>
      {/* "Filter applied & saved for quick access", pointing at Your filter (the first chip), once after Apply. */}
      <Tooltip open={savedTip} content={t('signals.savedTip')} placement="bottom" onClose={() => setSavedTip(false)} className={styles.tip}>
        <span className={styles.tipTarget} />
      </Tooltip>
    </div>
  )
  const totalTag = (
    <Tag size="md" variant="tertiary" color="profit">
      <span className={styles.totalLabel}>{t('signals.totalPnl')}</span> {t('signals.plus', { amount: formatInr(signalsTotalPnl, 0) })}
    </Tag>
  )
  const activeTitle = t('signals.active', { count: shown.length })
  // The plain "All Signals" look (Figma's last frame): a heading over every signal.
  const plain = Boolean(initial.plain) && !saved
  const header = plain ? (
    <BottomSheetHeader heading={t('signals.allTitle')} />
  ) : (
    // No tabs: the sheet starts with the filter button | the chips, a line under them.
    chipBar
  )

  // The filter takes the sheet over in place, laid out like the chart tools sheet (side nav + panel, Cancel / Apply in
  // the sheet's dock); Cancel, or a scrim tap, brings the signals back.
  if (filter) {
    return (
      <Sheet label={t('signals.filterTitle')} onClose={() => setFilter(null)} className={styles.toolsSheet} footer={<FilterDock onCancel={() => setFilter(null)} onApply={apply} />}>
        <FilterPanel section={filter} onSection={setFilter} draft={draft} onDraft={setDraft} />
      </Sheet>
    )
  }

  return (
    <Sheet label={t('signals.title')} onClose={onClose} header={header} className={styles.sheet}>
      <div className={styles.body}>
        {plain ? (
          <Stack gap="16">{zingSignals.map((s) => <SignalCard key={s.id} signal={s} strip={strip} order={stripOrder(zingSignals, s)} />)}</Stack>
        ) : (
          <Stack gap="16">
            <Stack direction="horizontal" align="center" justify="between" gap="12">
              <h2 className={styles.heading}>{activeTitle}</h2>
              {totalTag}
            </Stack>
            {shown.length ? (
              <Stack gap="16">{shown.map((s) => <SignalCard key={s.id} signal={s} strip={strip} order={stripOrder(shown, s)} />)}</Stack>
            ) : (
              <EmptyState title={t('signals.none')} description={t('signals.noneHint')} />
            )}
          </Stack>
        )}
      </div>
    </Sheet>
  )
}

/** The card's market tag: grey for an index or stock (NIFTY); for a commodity, an amber tag with its logo and name. */
function MarketTags({ signal }: { signal: ZingSignal }) {
  const commodity = signal.commodity
  if (!commodity) return <Tag size="sm" variant="tertiary" color="neutral" className={styles.greyTag}>{signal.underlying}</Tag>
  return <Tag size="sm" variant="tertiary" color="warning" iconLeft={<img src={commodityLogos[commodity]} alt="" className={styles.tagLogo} />}>{t(`signals.commodity.${commodity}`)}</Tag>
}

/** One signal: who sent it, where and how good it is, View; the trade under a line. */
function SignalCard({ signal, strip = 'off', order = 0 }: { signal: ZingSignal; strip?: StripVersion; order?: number }) {
  return (
    <SignalStrip signal={signal} version={strip} logo={signal.commodity ? commodityLogos[signal.commodity] : ''} order={order}>
    <Card className={styles.signalCard}>
      <Stack gap="12">
        <Stack direction="horizontal" align="center" justify="between" gap="12">
          <Stack direction="horizontal" align="center" gap="12" className={styles.who}>
            <Avatar src={avatars[signal.avatar]} size={32} />
            <Stack gap="04" className={styles.who}>
              <p className={styles.name}>{signal.strategy}</p>
              <Stack direction="horizontal" gap="08" align="center">
                {signal.winRate !== undefined ? (
                  <>
                    <MarketTags signal={signal} />
                    <Tag size="sm" variant="tertiary" color="neutral" className={styles.greyTag}>{t('signals.winRate')} <b className={styles.up}>{t('signals.percent', { value: signal.winRate })}</b></Tag>
                  </>
                ) : (
                  <Tag size="sm" variant="tertiary" color="profit"><span className={styles.pnlLabel}>{t('signals.pnl')}</span> {t('signals.plus', { amount: formatInr(signal.pnl ?? 0, 2) })}</Tag>
                )}
              </Stack>
            </Stack>
          </Stack>
          <Button size="sm" aria-label={t('signals.viewLabel', { name: signal.strategy })} className={styles.view}>{t('signals.view')}</Button>
        </Stack>
        <div className={styles.trade}>
          <span><span className={styles.muted}>{signal.side}</span> {signal.contract}</span>
          <span className={styles.dot} aria-hidden="true" />
          <span><span className={styles.muted}>{t('signals.rr')}</span> {signal.rr}</span>
          <span className={styles.dot} aria-hidden="true" />
          <span>{signal.ruleMuted ? <><span className={styles.muted}>{signal.rule[0]}</span> {signal.rule[1]}</> : `${signal.rule[0]} ${signal.rule[1]}`}</span>
        </div>
      </Stack>
    </Card>
    </SignalStrip>
  )
}

/** Where a card's strip comes in the stagger: the strips slide out one after another, top down. */
const stripOrder = (list: ZingSignal[], signal: ZingSignal) => list.filter((s) => s.nudge).indexOf(signal)

type FilterProps = { draft: SignalFilter; onDraft: (draft: SignalFilter) => void }

/** The picks in a draft, each with how to take it off (the chips over the dock). */
function picks({ draft, onDraft }: FilterProps) {
  return [
    ...draft.markets.map((m) => ({ key: m, label: t(`signals.pill.${m}`), remove: () => onDraft({ ...draft, markets: draft.markets.filter((v) => v !== m) }) })),
    ...(draft.winRate !== 'all' ? [{ key: 'win', label: t(`signals.win.${draft.winRate}`), remove: () => onDraft({ ...draft, winRate: 'all' as const }) }] : []),
    ...(draft.direction !== 'all' ? [{ key: 'dir', label: t(`signals.dir.${draft.direction}`), remove: () => onDraft({ ...draft, direction: 'all' as const }) }] : []),
    ...draft.strategies.map((id) => ({ key: id, label: zingSignals.find((s) => s.id === id)?.strategy ?? id, remove: () => onDraft({ ...draft, strategies: draft.strategies.filter((v) => v !== id) }) })),
  ]
}

/** The filter's dock: Cancel · Apply (primary), as Figma's Buttons dock. */
function FilterDock({ onCancel, onApply }: { onCancel: () => void; onApply: () => void }) {
  return (
    <ButtonGroup aria-label={t('signals.filterTitle')} direction="horizontal">
      <Button variant="secondary" onClick={onCancel}>{t('signals.cancel')}</Button>
      <Button onClick={onApply}>{t('signals.apply')}</Button>
    </ButtonGroup>
  )
}

/**
 * The filter, in the Scalper's Settings sheet look (ChartToolsSheet.module.css: the 96 side nav, the white panel with its
 * sticky Heading/16 title row over a hairline, 48 card rows 8 apart, the chosen radio row in the discover tint): Indices · Win rate · Call/Put · Strategies on the
 * left (a group that narrows the list shows how many it picked), the group's choices on the right, Clear All in the
 * title row empties the group. The picks sit under it as chips (✕ takes one off), in Figma's 44 strip.
 */
function FilterPanel({ section, onSection, draft, onDraft }: FilterProps & { section: FilterSection; onSection: (section: FilterSection) => void }) {
  const picked: Record<FilterSection, number> = {
    indices: draft.markets.length,
    winRate: draft.winRate === 'all' ? 0 : 1,
    direction: draft.direction === 'all' ? 0 : 1,
    strategies: draft.strategies.length,
  }
  const flag = (s: FilterSection) => (picked[s] ? String(picked[s]) : undefined)
  const clear = () => onDraft({
    ...draft,
    ...(section === 'indices' && { markets: [] }),
    ...(section === 'winRate' && { winRate: 'all' as const }),
    ...(section === 'direction' && { direction: 'all' as const }),
    ...(section === 'strategies' && { strategies: [] }),
  })
  const toggle = <T extends string>(list: T[], value: T) => (list.includes(value) ? list.filter((v) => v !== value) : [...list, value])

  const title = t(`signals.section.${section}`)
  const pills = picks({ draft, onDraft })
  const check = (label: string, checked: boolean, onChange: () => void, iconLeft?: ReactNode) => (
    <ListCell key={label} variant="card" size="sm" as="label" label={label} iconLeft={iconLeft} trailing={<Checkbox checked={checked} onChange={onChange} aria-label={label} />} className={tools.row} />
  )
  const radio = (name: string, label: string, checked: boolean, onChange: () => void) => (
    <ListCell key={label} variant="card" size="sm" as="label" selected={checked} label={label} trailing={<Radio name={name} checked={checked} onChange={onChange} aria-label={label} />} className={tools.row} />
  )

  return (
    // Settings' look; the list area is 412, the picks' strip goes under it.
    <>
    <div className={`${tools.body} ${styles.filterGrid}`}>
      <SideNav<FilterSection>
        selectedTone="discover"
        aria-label={t('signals.filterTitle')}
        aria-controls="signals-filter-panel"
        value={section}
        onChange={onSection}
        className={`${tools.nav} ${styles.nav}`}
        items={[
          { value: 'indices', label: t('signals.section.indices'), icon: <Icon icon={msFormatListBulleted} />, flag: flag('indices') },
          { value: 'winRate', label: t('signals.section.winRate'), icon: <Icon icon={msSpeed} />, flag: flag('winRate') },
          { value: 'direction', label: t('signals.section.direction'), icon: <Icon icon={msSwapVert} />, flag: flag('direction') },
          { value: 'strategies', label: t('signals.section.strategies'), icon: <span className={styles.zingMark}><MaskIcon src={zingMark} /></span>, flag: flag('strategies') },
        ]}
      />
      <section id="signals-filter-panel" role="tabpanel" aria-label={title} className={tools.panel}>
        <div className={tools.header}>
          <Stack direction="horizontal" align="center" justify="between" gap="12" className={tools.titleRow}>
            <h2 className={tools.title}>{title}</h2>
            <Button variant="ghost" size="sm" onClick={clear} className={styles.clear}>{t('signals.clearAll')}</Button>
          </Stack>
        </div>
        <Stack gap="08">
          {section === 'indices' && [
            check(t('signals.allIndices'), draft.markets.length === 0, () => onDraft({ ...draft, markets: [] })),
            ...signalMarkets.map((m) => check(marketLabel(m), draft.markets.includes(m), () => onDraft({ ...draft, markets: toggle(draft.markets, m) }))),
          ]}
          {section === 'winRate' && (['all', '50', '30'] as const).map((v) => radio('signals-win', t(`signals.win.${v}`), draft.winRate === v, () => onDraft({ ...draft, winRate: v })))}
          {section === 'direction' && (['all', 'call', 'put'] as const).map((v) => radio('signals-dir', t(`signals.dir.${v}`), draft.direction === v, () => onDraft({ ...draft, direction: v })))}
          {section === 'strategies' && zingSignals.map((s) => check(s.strategy, draft.strategies.includes(s.id), () => onDraft({ ...draft, strategies: toggle(draft.strategies, s.id) }), <Avatar src={avatars[s.avatar]} size={24} />))}
        </Stack>
      </section>
    </div>
    {pills.length > 0 && (
      <div className={styles.pills} aria-label={t('signals.picked')}>
        {pills.map((p) => (
          <Button key={p.key} variant="secondary" size="sm" iconRight={<Icon icon={msCancelFill} className={styles.pillX} />} aria-label={t('signals.remove', { label: p.label })} onClick={p.remove} className={styles.pill}>
            <span className={styles.pillLabel}>{p.label}</span>
          </Button>
        ))}
      </div>
    )}
    </>
  )
}

/** ₹ in Indian grouping: 13367 → ₹13,367; 367.3 → ₹367.30. */
function formatInr(value: number, digits: number) {
  return `₹${value.toLocaleString('en-IN', { minimumFractionDigits: digits, maximumFractionDigits: digits })}`
}
```

### `src/flows/fno/strategies/components/Strategies.module.css`

```css
/* Strategies tab — flow-only pieces on L3 tokens. */
.section { display: flex; flex-direction: column; gap: var(--l3-spacing-16); }
.pillDivider { flex: none; align-self: stretch; width: 1px; background: var(--l3-border-light); }
.caption { font: var(--l3-text-label-10); color: var(--l3-content-tertiary); white-space: nowrap; }
.statLabel { font: var(--l3-text-label-12); color: var(--l3-content-tertiary); white-space: nowrap; }
.statValue { font: var(--l3-text-heading-12); white-space: nowrap; }
.title16 { font: var(--l3-text-heading-16); white-space: nowrap; }
.fill { width: 100%; }
.ellipsis { overflow: hidden; text-overflow: ellipsis; }
.muted { color: var(--l3-content-tertiary); }
.strike { font: var(--l3-text-label-10); color: var(--l3-content-tertiary); }
.apply { flex: none; min-width: var(--l3-size-80); }
.invest { flex: none; }
.play { display: inline-flex; color: var(--l3-content-accent-error-default); }
.fire { display: inline-flex; color: var(--l3-content-accent-warning-default); }

/* Last week: one 16 circle per weekday, tinted by result. */
.day { display: inline-flex; align-items: center; justify-content: center; width: var(--l3-size-16); height: var(--l3-size-16); border-radius: var(--l3-radius-full); font: var(--l3-text-heading-10); }
.win { background: var(--l3-surface-accent-indicator-up-light); color: var(--l3-content-accent-indicator-up-default); }
.loss { background: var(--l3-surface-accent-indicator-down-light); color: var(--l3-content-accent-indicator-down-default); }
.none { background: var(--l3-surface-secondary); color: var(--l3-content-disabled); }

/* Payoff sketch: loss area left of the breakeven, profit area right of it. */
.payoff { flex: none; width: var(--l3-size-40); height: var(--l3-size-28); }
.lossArea { fill: var(--l3-surface-accent-indicator-down-light); }
.profitArea { fill: var(--l3-surface-accent-indicator-up-light); }
.lossLine, .profitLine { fill: none; stroke-width: 1.5; }
.lossLine { stroke: var(--l3-content-accent-indicator-down-default); }
.profitLine { stroke: var(--l3-content-accent-indicator-up-default); }

/* Quick Trade: outlined up / down buttons (L3 has filled Buy / Sell only — see L3 gaps). */
.upButton.upButton[data-variant] { --btn-content: var(--l3-content-accent-indicator-up-default); --btn-border: var(--l3-border-accent-indicator-up-default); }
.downButton.downButton[data-variant] { --btn-content: var(--l3-content-accent-indicator-down-default); --btn-border: var(--l3-border-accent-indicator-down-default); }
```

### `src/flows/fno/strategies/components/StrategiesFeed.tsx`

```tsx
import { useState } from 'react'
import { Avatar } from '@l3/components/Avatar'
import { Button } from '@l3/components/Button'
import { Card } from '@l3/components/Card'
import { Icon } from '@l3/components/Icon'
import { SectionHeader } from '@l3/components/SectionHeader'
import { Select } from '@l3/components/Select'
import { Stack } from '@l3/components/Stack'
import { Tab, Tabs } from '@l3/components/Tabs'
import { lmSwitchArrowVertical } from '@l3/icons/lemonnade'
import { msBoltFill, msChevronRight, msLocalFireDepartmentFill, msPlayCircleFill, msStar, msTrendingDown, msTrendingUp, msVisibility, msVisibilityOff } from '@l3/icons/material'
import { inr } from '../../../../shared/data/format'
import { Rail } from '../../../../shared/ui/Rail'
import { Shortcuts } from '../../components/Discovery'
import type { Choose } from '../../components/ContractSection'
import { t } from '../../copy'
import { prebuilt, smartInvests, underlyings, zingTrades, type Prebuilt, type Segment, type SmartInvest, type View, type ZingTrade } from '../data'
import parts from '../../components/HomeParts.module.css'
import styles from './Strategies.module.css'

type Props = {
  /** Equity or Commodities (the pill group under the shortcuts). */
  segment: Segment
  onSegment: (segment: Segment) => void
  onChoose: Choose
  onDestination: (name: string) => void
  onWatchlist: () => void
}

/** The Strategies tab of F&O home (Figma 6754:64178 Equity, 6754:64607 Commodities). */
export function StrategiesFeed({ segment, onSegment, onChoose, onDestination, onWatchlist }: Props) {
  const [underlying, setUnderlying] = useState(underlyings[segment][0])
  const [quick, setQuick] = useState(underlyings[segment][0])
  const [view, setView] = useState<View>('bullish')
  const switchSegment = (next: Segment) => { onSegment(next); setUnderlying(underlyings[next][0]); setQuick(underlyings[next][0]) }
  const views = (['bullish', 'bearish', 'neutral', 'volatile'] as const).map((value) => ({ value, label: t(`strategies.${value}`) }))
  return <Stack gap="32" className={parts.feed}>
    <Shortcuts onWatchlist={onWatchlist} onDestination={onDestination} />
    <div className={parts.inset}><Tabs aria-label={t('strategies.segment')} appearance="pill-group" width="fill" value={segment} onChange={switchSegment} items={[{ value: 'equity', label: t('equity') }, { value: 'commodities', label: t('commodities') }]} /></div>

    <section className={styles.section} aria-label={t('strategies.zing')}>
      <div className={parts.inset}><SectionHeader title={t('strategies.zing')} action={{ type: 'view-all', label: t('strategies.explore'), onClick: () => onDestination(t('strategies.zing')) }} /></div>
      <Rail label={t('strategies.zing')} visible={1.08}>{zingTrades.map((trade) => <ZingTradeCard key={trade.id} trade={trade} onOpen={onDestination} />)}</Rail>
    </section>

    <section className={styles.section} aria-label={t('strategies.smartInvest')}>
      <div className={parts.inset}><SectionHeader title={t('strategies.smartInvest')} action={{ type: 'view-all', label: t('viewAll'), onClick: () => onDestination(t('strategies.smartInvest')) }} /></div>
      <Rail label={t('strategies.smartInvest')} visible={1.08}>{smartInvests[segment].map((invest) => <SmartInvestCard key={invest.id} invest={invest} onOpen={onDestination} />)}</Rail>
    </section>

    <section className={styles.section} aria-label={t('strategies.prebuilt')}>
      <div className={parts.inset}><SectionHeader title={t('strategies.prebuilt')} action={{ type: 'view-all', label: t('strategies.explore'), onClick: () => onDestination(t('strategies.prebuilt')) }} /></div>
      <Stack direction="horizontal" gap="08" align="center" className={[parts.filterRow, parts.inset].join(' ')}>
        <Tab appearance="pill" size="sm" emphasis="secondary" action iconRight={<Icon icon={lmSwitchArrowVertical} size={12} />} aria-label={t('strategies.underlying')} onClick={() => onChoose(t('strategies.pickUnderlying'), underlyings[segment], underlying, setUnderlying)}>{underlying}</Tab>
        <span className={styles.pillDivider} aria-hidden />
        <Tabs aria-label={t('strategies.prebuilt')} appearance="pill" size="sm" value={view} onChange={setView} items={views} />
      </Stack>
      <Rail label={t('strategies.prebuilt')} visible={1.08}>{prebuilt[view].map((strategy) => <PrebuiltCard key={strategy.id} strategy={strategy} onOpen={onDestination} />)}</Rail>
    </section>

    <div className={parts.inset}><QuickTrade underlying={quick} onUnderlying={() => onChoose(t('strategies.pickUnderlying'), underlyings[segment], quick, setQuick)} onTrade={onDestination} /></div>
  </Stack>
}

/** Zing Trades: trader, today's return, last week's Mon–Fri results, average trades and win rate; ☆ · Learn · Apply. */
function ZingTradeCard({ trade, onOpen }: { trade: ZingTrade; onOpen: (name: string) => void }) {
  const days = ['M', 'T', 'W', 'T', 'F']
  const dayNames = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
  return <Card onClick={() => onOpen(trade.name)} footerFilled footer={<Stack direction="horizontal" gap="08" align="center" className={styles.fill}>
    <Button variant="secondary" size="sm" aria-label={t('strategies.favourite', { name: trade.name })} iconLeft={<Icon icon={msStar} size={16} />} onClick={() => onOpen(t('strategies.favourite', { name: trade.name }))} />
    <Button variant="secondary" size="sm" fullWidth iconLeft={<span className={styles.play}><Icon icon={msPlayCircleFill} size={16} /></span>} iconRight={<Icon icon={msChevronRight} size={16} />} onClick={() => onOpen(t('strategies.learn'))}>{t('strategies.learn')}</Button>
    <Button variant="primary" size="sm" className={styles.apply} onClick={() => onOpen(`${t('strategies.apply')} ${trade.name}`)}>{t('strategies.apply')}</Button>
  </Stack>}>
    <Stack gap="12">
      <Stack direction="horizontal" gap="08" align="center" justify="between">
        <Stack direction="horizontal" gap="08" align="center"><Avatar initials={trade.trader.split(' ').map((n) => n[0]).join('')} size={32} label={trade.trader} /><Stack gap="04"><p className={parts.heading}>{trade.name}</p><p className={styles.caption}>{t('strategies.builtWith')}</p></Stack></Stack>
        <Stack gap="04" align="end"><p className={[parts.heading, parts.up].join(' ')}>{trade.todayReturn}%</p><p className={styles.caption}>{t('strategies.todayReturns')}</p></Stack>
      </Stack>
      <div className={parts.divider} />
      <Stack direction="horizontal" align="center" justify="between">
        <Stack gap="04"><p className={styles.statLabel}>{t('strategies.lastWeek')}</p><Stack direction="horizontal" gap="04">{trade.week.map((result, i) => <span key={i} className={[styles.day, styles[result]].join(' ')} aria-label={t(result === 'win' ? 'strategies.dayWin' : result === 'loss' ? 'strategies.dayLoss' : 'strategies.dayFlat', { day: dayNames[i] })}>{days[i]}</span>)}</Stack></Stack>
        <Stack gap="04" align="center"><p className={styles.statLabel}>{t('strategies.avgTrades')}</p><p className={styles.statValue}>{t('strategies.perDay', { count: trade.tradesPerDay })}</p></Stack>
        <Stack gap="04" align="end"><p className={styles.statLabel}>{t('strategies.winRate')}</p><Stack direction="horizontal" gap="04" align="center" className={parts.up}><Icon icon={msTrendingUp} size={16} /><p className={styles.statValue}>{trade.winRate}%</p></Stack></Stack>
      </Stack>
    </Stack>
  </Card>
}

/** Smart Invest: basket, min. deposit, 7 / 30 day P&L (switcher + hide), AUM, slots left; monthly charges + Invest now. */
function SmartInvestCard({ invest, onOpen }: { invest: SmartInvest; onOpen: (name: string) => void }) {
  const [days30, setDays30] = useState(false)
  const [hidden, setHidden] = useState(false)
  const pnl = days30 ? invest.pnl30 : invest.pnl7
  // Not a clickable card: its body holds the P&L switcher and the hide button (no buttons inside a button).
  return <Card footerFilled footer={<Stack direction="horizontal" align="center" justify="between" className={styles.fill}>
    <Stack gap="04"><p className={styles.statLabel}>{t('strategies.charges')}</p><p className={styles.statValue}>{inr(invest.charges, 0)} <s className={styles.strike}>{inr(invest.chargesBefore, 0)}</s></p></Stack>
    <Button variant="primary" size="sm" className={styles.invest} onClick={() => onOpen(`${t('strategies.invest')} · ${invest.name}`)}>{t('strategies.invest')}</Button>
  </Stack>}>
    <Stack gap="12">
      <Stack direction="horizontal" gap="08" align="center" justify="between">
        <Stack direction="horizontal" gap="08" align="center" className={parts.grow}><Avatar initials={invest.name.slice(0, 1)} size={40} /><Stack gap="04" className={parts.grow}><p className={[styles.title16, styles.ellipsis].join(' ')}>{invest.name}</p><p className={styles.statLabel}>{t('strategies.by', { name: invest.by })}</p></Stack></Stack>
        <Stack gap="04" align="end"><p className={styles.title16}>{inr(invest.minDeposit, 0)}</p><p className={styles.statLabel}>{t('strategies.minDeposit')}</p></Stack>
      </Stack>
      <div className={parts.divider} />
      <Stack direction="horizontal" align="center" justify="between">
        <Stack gap="04"><Select size="sm" onClick={() => setDays30(!days30)}>{t(days30 ? 'strategies.pnl30' : 'strategies.pnl7')}</Select><Stack direction="horizontal" gap="04" align="center"><p className={[styles.statValue, parts.up].join(' ')}>{hidden ? '••••' : `${pnl}%`}</p><Button variant="ghost" size="sm" aria-label={t('strategies.showPnl')} iconLeft={<Icon icon={hidden ? msVisibilityOff : msVisibility} size={16} />} onClick={() => setHidden(!hidden)} /></Stack></Stack>
        <Stack gap="04" align="center"><p className={styles.statLabel}>{t('strategies.aum')}</p><p className={styles.statValue}>{invest.aum}</p></Stack>
        <Stack gap="04" align="end"><p className={styles.statLabel}>{t('strategies.slots')}</p><Stack direction="horizontal" gap="04" align="center"><span className={styles.fire}><Icon icon={msLocalFireDepartmentFill} size={16} /></span><p className={styles.statValue}>{invest.slotsLeft}<span className={styles.muted}>/{invest.slots}</span></p></Stack></Stack>
      </Stack>
    </Stack>
  </Card>
}

/** A pre-build strategy: probability of profit, name, funds required, max profit / loss and a payoff sketch. */
function PrebuiltCard({ strategy, onOpen }: { strategy: Prebuilt; onOpen: (name: string) => void }) {
  return <Card onClick={() => onOpen(strategy.name)}>
    <Stack gap="12">
      <Stack direction="horizontal" align="center" justify="between"><p className={styles.title16}>{t('strategies.pop')}</p><p className={[styles.title16, parts.up].join(' ')}>+{strategy.probability}%</p></Stack>
      <Stack direction="horizontal" align="center" justify="between"><p className={styles.statLabel}>{strategy.name}</p><p className={styles.statLabel}>{t('strategies.funds', { amount: inr(strategy.funds, 0) })}</p></Stack>
      <div className={parts.divider} />
      <Stack direction="horizontal" align="center" justify="between">
        <Stack gap="04">
          <p className={styles.statLabel}>{t('strategies.maxProfit')} <span className={parts.up}>{strategy.maxProfit === null ? t('strategies.unlimited') : inr(strategy.maxProfit, 0)}</span></p>
          <p className={styles.statLabel}>{t('strategies.maxLoss')} <span className={parts.down}>{inr(strategy.maxLoss, 0)}</span></p>
        </Stack>
        <svg className={styles.payoff} viewBox="0 0 40 28" role="img" aria-label={t('strategies.payoff')}>
          <rect className={styles.lossArea} x="0" y="14" width="18" height="10" />
          <rect className={styles.profitArea} x="22" y="4" width="18" height="10" />
          <polyline className={styles.lossLine} points="0,24 16,24 20,14" />
          <polyline className={styles.profitLine} points="20,14 24,4 40,4" />
        </svg>
      </Stack>
    </Stack>
  </Card>
}

/** Quick Trade: "Which way will GOLD ⌄ move?" and an Up / Down choice. */
function QuickTrade({ underlying, onUnderlying, onTrade }: { underlying: string; onUnderlying: () => void; onTrade: (name: string) => void }) {
  return <Card>
    <Stack gap="12">
      <Stack direction="horizontal" align="center" justify="between"><Stack direction="horizontal" gap="04" align="center"><Icon icon={msBoltFill} size={16} /><p className={styles.statValue}>{t('strategies.quick')}</p></Stack><p className={styles.statLabel}>{t('strategies.beginner')}</p></Stack>
      <div className={parts.divider} />
      <Stack direction="horizontal" gap="04" align="center"><p className={styles.title16}>{t('strategies.which')}</p><Select size="lg" icon="chevron" aria-label={t('strategies.pickUnderlying')} onClick={onUnderlying}>{underlying}</Select><p className={styles.title16}>{t('strategies.move')}</p></Stack>
      <Stack direction="horizontal" gap="12">
        <Button variant="secondary" size="md" fullWidth className={styles.upButton} iconLeft={<Icon icon={msTrendingUp} size={16} />} onClick={() => onTrade(`${underlying} · ${t('strategies.up')}`)}>{t('strategies.up')}</Button>
        <Button variant="secondary" size="md" fullWidth className={styles.downButton} iconLeft={<Icon icon={msTrendingDown} size={16} />} onClick={() => onTrade(`${underlying} · ${t('strategies.down')}`)}>{t('strategies.down')}</Button>
      </Stack>
    </Stack>
  </Card>
}
```

### `src/flows/fno/strategies/data.ts`

```ts
/** Snapshot examples from Figma 6754:64178 (Strategies → Equity) and 6754:64607 (Strategies → Commodities); not live data. */

export type Segment = 'equity' | 'commodities'

/** A Zing Trades card: a strategy built with DASH Ai. `week` is Mon–Fri: won, lost, or no trade. */
export type ZingTrade = { id: string; name: string; trader: string; todayReturn: number; week: ('win' | 'loss' | 'none')[]; tradesPerDay: number; winRate: number }
const zing = (id: string, name: string, trader: string): ZingTrade => ({ id, name, trader, todayReturn: 78, week: ['win', 'win', 'none', 'win', 'loss'], tradesPerDay: 2, winRate: 58 })
export const zingTrades: ZingTrade[] = [zing('ema-9', 'EMA Cross 9', 'Arjun Mehta'), zing('rsi-rev', 'RSI Reversal', 'Neha Iyer'), zing('vwap', 'VWAP Bounce', 'Rahul Verma')]

/** A Smart Invest card: a managed basket. Amounts in rupees; `pnl7` is the 7-day P&L in percent. */
export type SmartInvest = { id: string; name: string; by: string; minDeposit: number; pnl7: number; pnl30: number; aum: string; slotsLeft: number; slots: number; charges: number; chargesBefore: number }
export const smartInvests: Record<Segment, SmartInvest[]> = {
  equity: [
    { id: 'osa', name: 'OptionsSensexAlpha', by: 'lemonn', minDeposit: 50000, pnl7: 64.4, pnl30: 81.2, aum: '10L', slotsLeft: 80, slots: 100, charges: 0, chargesBefore: 300 },
    { id: 'nifty-theta', name: 'NiftyThetaPlus', by: 'lemonn', minDeposit: 75000, pnl7: 22.1, pnl30: 40.5, aum: '25L', slotsLeft: 12, slots: 100, charges: 0, chargesBefore: 300 },
  ],
  commodities: [
    { id: 'osa', name: 'OptionsSensexAlpha', by: 'lemonn', minDeposit: 50000, pnl7: 64.4, pnl30: 81.2, aum: '10L', slotsLeft: 80, slots: 100, charges: 0, chargesBefore: 300 },
    { id: 'gold-carry', name: 'GoldCarryPro', by: 'lemonn', minDeposit: 60000, pnl7: 18.6, pnl30: 33.9, aum: '8L', slotsLeft: 41, slots: 100, charges: 0, chargesBefore: 300 },
  ],
}

/** Pre-build strategies per view. `funds` = funds required, `maxLoss` in rupees; `maxProfit` null = unlimited. */
export type View = 'bullish' | 'bearish' | 'neutral' | 'volatile'
export type Prebuilt = { id: string; name: string; probability: number; funds: number; maxProfit: number | null; maxLoss: number }
export const prebuilt: Record<View, Prebuilt[]> = {
  bullish: [
    { id: 'bcs', name: 'Bull call spread', probability: 59.8, funds: 186456, maxProfit: null, maxLoss: 99999 },
    { id: 'bps', name: 'Bull put spread', probability: 64.2, funds: 142300, maxProfit: 42500, maxLoss: 57500 },
  ],
  bearish: [
    { id: 'bpsd', name: 'Bear put spread', probability: 41.5, funds: 120800, maxProfit: 64000, maxLoss: 36000 },
    { id: 'bccs', name: 'Bear call spread', probability: 62.7, funds: 138900, maxProfit: 38200, maxLoss: 61800 },
  ],
  neutral: [
    { id: 'ic', name: 'Iron condor', probability: 71.3, funds: 165000, maxProfit: 28400, maxLoss: 71600 },
    { id: 'ss', name: 'Short strangle', probability: 68.9, funds: 245000, maxProfit: 31200, maxLoss: 99999 },
  ],
  volatile: [
    { id: 'ls', name: 'Long straddle', probability: 38.4, funds: 52300, maxProfit: null, maxLoss: 52300 },
    { id: 'lsg', name: 'Long strangle', probability: 33.1, funds: 31800, maxProfit: null, maxLoss: 31800 },
  ],
}

/** The underlying the Pre-build and Quick Trade cards are for, per view. */
export const underlyings: Record<Segment, string[]> = {
  equity: ['Nifty 50', 'Bank Nifty', 'Sensex'],
  commodities: ['GOLD', 'SILVER', 'CRUDEOIL'],
}
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

### `src/shared/data/user.ts`

```ts
// The sample user every flow uses. FICTIONAL — the live screenshots contain a real customer's details; never copy them.
export type User = {
  name: string
  fatherName: string
  mobile: string
  email: string
  pan: string
  dob: string
  occupation: string
  maritalStatus: string
}

export const user: User = {
  name: 'Rohan Mehta',
  fatherName: 'Suresh Mehta',
  mobile: '9876543210',
  email: 'rohan.mehta@gmail.com',
  pan: 'ABCPM1234K',
  dob: '14 Aug 1996',
  occupation: 'Private sector',
  maritalStatus: 'Single',
}

export type BankAccount = { bank: string; accountNumber: string; ifsc: string; type: 'Savings' | 'Current'; branch: string }

export const bankAccount: BankAccount = {
  bank: 'HDFC Bank',
  accountNumber: '50100234567821',
  ifsc: 'HDFC0001234',
  type: 'Savings',
  branch: 'Andheri West, Mumbai',
}

/** A linked bank account as the money screens show it: the bank's logo symbol (companies.ts) and the last 4 digits. */
export type LinkedBank = BankAccount & { id: string; logoSymbol: string; last4: string; primary?: boolean }

/** The user's linked bank accounts, primary first. "User status → Bank accounts" picks how many the prototype shows. */
export const linkedBanks: LinkedBank[] = [
  { ...bankAccount, id: 'hdfc', logoSymbol: 'HDFCBANK', last4: '7821', primary: true },
  { id: 'icici', bank: 'ICICI Bank', accountNumber: '002101554410', ifsc: 'ICIC0000021', type: 'Savings', branch: 'Powai, Mumbai', logoSymbol: 'ICICIBANK', last4: '4410' },
]

/**
 * A linked account at a bank that can't send money abroad for US Stocks (not an LRS partner) — "User status → Bank
 * accounts: Three" and "SBI only" add it, to show the US Stocks bank step with an account it can't use.
 */
export const otherBank: LinkedBank = { id: 'sbi', bank: 'State Bank of India', accountNumber: '38201945520', ifsc: 'SBIN0000300', type: 'Savings', branch: 'Fort, Mumbai', logoSymbol: 'SBIN', last4: '5520' }

/** The instant-balance offer (₹, for intraday, MTF and F&O): Profile's row and the Indian wallet's card show it. */
export const INSTANT_BALANCE = 149
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

### `src/shared/ui/FloatingNav.module.css`

```css
/*
 * Bottom navbar V2 — floating (FloatingNav.tsx), from the Figma floating nav (LM → Stocks Playground, node 6687:10922,
 * 20 Nov). In its 392 frame: the pill 16 / 16 in and 14 up, 56 tall (8 + 24 icon + 12 label + 12), radius full, on
 * surface/default with a 1px border/light edge and a soft double shadow; a 50 × 40 accent-green glow (Figma: lemon) blurred 23.3, its top
 * 27.87 above the pill's; behind it a blob of surface/default blurred 50. Figma values L3 has no token for are the
 * marked --app-fnav-* local tokens (src/local-tokens.css).
 * L3 gap: Bottom Navbar has no floating version, so this frame restyles it (fill, line, shadow, option sizes, colours).
 */

/* V1 (docked): the navbar as it is — the wrapper only marks it (data-bottom-nav) and adds no box of its own. */
.docked { display: contents; }

/* Takes no height in the page: what it holds hangs from the page's bottom edge over the body. */
.frame {
  position: relative;
  z-index: 1; /* above the body that scrolls under it — stacking order isn't a design token */
  height: 0;
}

/* The page fades out under the nav (20 Nov, user: stronger than Figma's blurred blob): the page's colour, solid from
   the bottom edge up past the pill's middle, then fading to clear just above the pill (23 Nov, user: half the old
   152, it rose too far up the page). It never takes a tap. */
.fade {
  position: absolute;
  right: 0;
  bottom: 0;
  left: 0;
  height: calc((var(--l3-size-128) + var(--l3-size-24)) / 2); /* 76: half the old 152, just over the pill (70) */
  background: linear-gradient(
    to top,
    var(--l3-surface-default) 0%,
    var(--l3-surface-default) 30%,
    color-mix(in srgb, var(--l3-surface-default) 85%, transparent) 50%,
    color-mix(in srgb, var(--l3-surface-default) 45%, transparent) 75%,
    color-mix(in srgb, var(--l3-surface-default) 0%, transparent) 100%
  );
  pointer-events: none;
}

.pill {
  position: absolute;
  right: var(--l3-spacing-16);
  bottom: var(--l3-spacing-14);
  left: var(--l3-spacing-16);
  box-sizing: border-box;
  overflow: hidden;
  padding: var(--l3-spacing-08) 0 var(--l3-spacing-12); /* end to end: no side padding (23 Nov, user) */
  border-radius: var(--l3-radius-full);
  background: var(--l3-surface-default);
  /* Figma's 1px stroke is inside the pill (it stays 56): an inset line, then the double shadow. */
  box-shadow: inset 0 0 0 1px var(--l3-border-light), var(--app-fnav-shadow); /* 1px: Figma stroke weight has no variable */
}

/* The chosen tab's glow (Figma Ellipse 6871, in accent green), centred on the tab, clipped by the pill. */
.glow {
  position: absolute;
  top: var(--app-fnav-glow-top);
  left: calc(var(--glow-x) - var(--app-fnav-glow-width) / 2); /* centred on the chosen tab (23 Nov, user) */
  width: var(--app-fnav-glow-width);
  height: var(--l3-size-40);
  border-radius: var(--l3-radius-full);
  background: var(--l3-surface-accent-success-default); /* accent green (20 Nov, user; Figma's was brand lime) */
  filter: blur(var(--app-fnav-glow-blur));
  pointer-events: none;
  transition: left var(--l3-motion-duration-medium) var(--l3-motion-easing-standard);
}

/* V3 (23 Nov, user): the glow under the chosen tab, mirrored — as far below the pill's foot as V2's is above its top. */
.frame[data-glow-at='bottom'] .glow {
  top: auto;
  bottom: var(--app-fnav-glow-top);
}
/* V3 (23 Nov, user: "hide the glow"): no glow at all — the coloured icon marks the chosen tab. */
.frame[data-glow-at='bottom'] .glow {
  display: none;
}

/* V3 (23 Nov, user): each tab full height, 56. */
/* 24 Nov, user: full width again — 16 in from each side, the five tabs sharing it equally, so they grow and shrink
   with the device width (no fixed 74). */
.frame[data-glow-at='bottom'] .pill {
  padding: 0;
}
.frame[data-glow-at='bottom'] .pill :is(button, a)[class] {
  height: var(--l3-size-56);
  white-space: nowrap;
}
/* Labels shown whole, never cut to "Mutual Fu…". FLAG (L3 gap): Bottom Navbar truncates labels; no fixed-size option. */
.frame[data-glow-at='bottom'] .pill :is(button, a)[class] > span:last-child {
  overflow: visible;
  text-overflow: clip;
}

/* L3 Bottom Navbar inside the pill: no fill, line, shadow or safe-area pad of its own; 4 between options. */
.pill > nav {
  position: relative;
  background: transparent;
  box-shadow: none;
  padding-bottom: 0;
}
.pill > nav > ul {
  gap: 0; /* equal options tile the pill edge to edge (23 Nov, user) */
}
/* Every option the same width, the row end to end across the pill (23 Nov, user). */
.pill > nav > ul > li {
  flex: 1 1 0;
  min-width: 0;
}
.pill > nav > ul > li > :is(button, a) {
  width: 100%;
}

/* Each option: the 24 icon right on its 12 label, no padding; content/secondary, the chosen one content/primary in
   L3 Heading/10. (Figma's unselected label is semibold 600; L3's nearest is Label/10, 650.) */
.pill :is(button, a)[class] {
  gap: 0;
  min-height: 0;
  padding: 0;
  color: var(--l3-content-secondary);
  background-image: none;
}
/* Inactive labels in L3 Description/10 (500), not Label/10 (650): at 650 the text read stronger than its thin icon in
   the same content/secondary (23 Nov, user: "keep the visual of the text and the icon the same"). */
.pill :is(button, a)[class]:not([data-selected]) > span:last-child {
  font: var(--l3-text-description-10);
}
.pill :is(button, a)[data-selected] {
  color: var(--l3-content-primary);
}
.pill :is(button, a)[data-selected] > span:last-child {
  font: var(--l3-text-heading-10);
}

/* The Figma icons (FloatingNavIcon): 24, masked in the option's colour. */
.icon {
  display: block;
  width: var(--l3-icon-size-24);
  height: var(--l3-icon-size-24);
}

/* ---------- Motion (23 Nov, user: "animate the whole navbar transitions") ----------
   Option colours ease; on a tab switch (data-motion="moved") the new tab's icon pops and its label comes up, the old
   tab fades back from content/primary; when the options themselves change (main nav ↔ a sub-nav, "swapped") they come
   in one by one. FLAG (L3 gap): Bottom Navbar has no selection motion; durations / easing are L3 motion tokens. */
.pill :is(button, a)[class] {
  transition: color var(--l3-motion-duration-medium) var(--l3-motion-easing-standard);
}
.frame[data-motion='moved'] .pill :is(button, a)[data-selected] .icon {
  animation: navPop var(--l3-motion-duration-long) var(--l3-motion-easing-standard) both;
}
.frame[data-motion='moved'] .pill :is(button, a)[data-selected] > span:last-child {
  animation: navRise var(--l3-motion-duration-medium) var(--l3-motion-easing-standard) both;
}
.frame[data-motion='moved'] .pill li[data-was-selected] :is(button, a) {
  animation: navFadeBack var(--l3-motion-duration-medium) var(--l3-motion-easing-standard) both;
}
.frame[data-motion='swapped'] .pill > nav > ul > li {
  animation: navRise var(--l3-motion-duration-medium) var(--l3-motion-easing-standard) both;
}
.frame[data-motion='swapped'] .pill > nav > ul > li:nth-child(2) { animation-delay: 40ms; }
.frame[data-motion='swapped'] .pill > nav > ul > li:nth-child(3) { animation-delay: 80ms; }
.frame[data-motion='swapped'] .pill > nav > ul > li:nth-child(4) { animation-delay: 120ms; }
.frame[data-motion='swapped'] .pill > nav > ul > li:nth-child(5) { animation-delay: 160ms; }
.frame[data-motion='swapped'] .glow { animation: navGlowIn var(--l3-motion-duration-long) var(--l3-motion-easing-standard) both; }

@keyframes navPop { 0% { transform: scale(.7); } 60% { transform: scale(1.12); } 100% { transform: scale(1); } }
@keyframes navRise { from { opacity: 0; transform: translateY(var(--l3-spacing-04)); } to { opacity: 1; transform: none; } }
@keyframes navFadeBack { from { color: var(--l3-content-primary); } to { color: var(--l3-content-tertiary); } }
@keyframes navGlowIn { from { opacity: 0; } to { opacity: 1; } }

@media (prefers-reduced-motion: reduce) {
  .glow { transition: none; }
  .frame .pill *, .frame .glow { animation: none !important; transition: none !important; }
}

/* V3 (24 Nov, user): 2 between the icon and its label, and the chosen tab's label in accent green, matching its
   coloured icon. */
.frame[data-glow-at='bottom'] .pill :is(button, a)[class] {
  gap: var(--l3-spacing-02);
}
.frame[data-glow-at='bottom'] .pill :is(button, a)[data-selected] > span:last-child {
  color: var(--l3-content-accent-success-default);
}

/* Inactive tabs (24 Nov, user): as light as the Mutual Fund / F&O navs' L3 icons (their 40 / 60 parts), and the label
   the same colour as its icon in every nav — content/tertiary for both. (The L3 NavIcons in the sub-navs keep their
   baked 40 / 60 shares.) A user call over the "no tertiary text" default. */
.pill :is(button, a)[class]:not([data-selected]) {
  color: var(--l3-content-tertiary);
}
/* …but the labels stay content/secondary (24 Nov, user: "labels back to secondary"); only the icons go lighter. */
.pill :is(button, a)[class]:not([data-selected]) > span:last-child {
  color: var(--l3-content-secondary);
}
```

### `src/shared/ui/FloatingNav.tsx`

```tsx
import { useLayoutEffect, useRef, useState, type CSSProperties, type ReactNode } from 'react'
import { MaskIcon } from '@l3/components/MaskIcon'
import { useFlowOption } from '../prototype'
import { USER_STATUS } from '../userStatus'
import stocksIcon from './assets/floating-nav/stocks.svg'
import marketIcon from './assets/floating-nav/market.svg'
import marketSelectedIcon from './assets/floating-nav/market-selected.svg'
import portfolioIcon from './assets/floating-nav/portfolio.svg'
import mutualFundIcon from './assets/floating-nav/mutual-fund.svg'
import fnoIcon from './assets/floating-nav/fno.svg'
import fnoSelectedIcon from './assets/floating-nav/fno-selected.svg'
import styles from './FloatingNav.module.css'

/** App setting "Bottom navbar" (A/B, 20 Nov): V1 docked (L3 Bottom Navbar) · V2 floating, the default at launch (20 Nov) ·
 * V3 V2's floating nav with L3's coloured icon on the chosen tab and the glow under it, not over it (23 Nov, user). */
export const BOTTOM_NAV_OPTION = 'bottomNav'
const useBottomNavVersion = () => useFlowOption(USER_STATUS, BOTTOM_NAV_OPTION, 'v2') // V2 by default (20 Nov, user)
/** V2 and V3: the floating nav (this frame and its own Figma icons). */
export const useFloatingNav = () => useBottomNavVersion() !== 'v1'
/** V3: the chosen tab shows L3's coloured (two-tone brand) icon instead of the black-and-white one. */
export const useColourNavIcons = () => useBottomNavVersion() === 'v3'
/** The L3 Bottom Navbar variant to pass: always docked now (V3 was L3's floating variant until 23 Nov; the frame floats it). */
export const useBottomNavVariant = (): 'docked' | 'floating' => 'docked'

/**
 * V2's main-nav icons, from the Figma floating nav (LM → Stocks Playground, node 6687:10998, 20 Nov). One colour
 * each, masked so they take the option's colour: content/primary when chosen, content/secondary when not. Market
 * and F&O have their own chosen shape; Portfolio's lighter part keeps its 40 / 60 share baked in.
 */
const floatingIcons = {
  stocks: [stocksIcon, stocksIcon],
  market: [marketIcon, marketSelectedIcon],
  portfolio: [portfolioIcon, portfolioIcon],
  mutualFund: [mutualFundIcon, mutualFundIcon],
  fno: [fnoIcon, fnoSelectedIcon],
} as const
export type FloatingIconName = keyof typeof floatingIcons

export function FloatingNavIcon({ name, selected = false }: { name: FloatingIconName; selected?: boolean }) {
  return <span className={styles.icon}><MaskIcon src={floatingIcons[name][selected ? 1 : 0]} /></span>
}

/**
 * Wraps a bottom navbar (an L3 <BottomNavbar>: the main nav, the F&O and Mutual Fund sub-navs). V1 passes it through.
 * V2 is the Figma floating nav (node 6687:10922): a pill 16 in from each side and 14 up from the bottom, on
 * surface/default with a light edge and a soft double shadow; 8 above the icons and 12 below the labels; a blurred
 * accent-green glow from the chosen tab's left edge, clipped by the pill; and behind it all the page's colour, solid at
 * the bottom and fading out above the pill (20 Nov), so the page fades out under the nav. The frame takes no height of
 * its own: the body runs on behind it and keeps its last content clear of the pill (Screen / Phone CSS).
 */
/** Where the last floating nav left off: each tab is its own screen, so the nav mounts afresh on every switch. */
let navMemory: { glowX: number | null; index: number | null; items: string | null } = { glowX: null, index: null, items: null }

export function FloatingNav({ children }: { children: ReactNode }) {
  const floating = useFloatingNav()
  const glowBelow = useColourNavIcons() // V3: the glow sits under the chosen tab (23 Nov, user)
  const pill = useRef<HTMLDivElement>(null)
  // A fresh nav starts where the last one left off (the glow at the old tab) and moves from there (23 Nov, user:
  // "animate the whole navbar transitions like tab switch, nav items change").
  const [glowX, setGlowX] = useState<number | null>(() => navMemory.glowX)
  const [motion, setMotion] = useState<'moved' | 'swapped' | undefined>(undefined)
  const firstPlace = useRef(true)

  // The glow sits behind the chosen tab: wherever L3 puts it (sub-navs have a Home option first).
  useLayoutEffect(() => {
    if (!floating || !pill.current) return
    const place = () => {
      const box = pill.current
      if (!box) return
      const options = [...box.querySelectorAll<HTMLElement>('nav > ul > li')]
      const chosenIndex = options.findIndex((li) => li.querySelector('[data-selected]'))
      if (chosenIndex < 0) return setGlowX(null)
      const tab = options[chosenIndex].getBoundingClientRect()
      const x = tab.left + tab.width / 2 - box.getBoundingClientRect().left // the chosen tab's centre (23 Nov, user)
      const items = options.map((li) => li.textContent).join('|')
      const before = navMemory
      navMemory = { glowX: x, index: chosenIndex, items }
      if (!firstPlace.current) return setGlowX(x) // a change within this nav: the CSS transition slides the glow
      firstPlace.current = false
      if (before.items !== null && before.items !== items) {
        setMotion('swapped') // another set of options (main nav ↔ a sub-nav): they come in one by one
        return setGlowX(x)
      }
      if (before.index === null || before.index === chosenIndex || before.glowX === null) return setGlowX(x)
      // A tab switch: the old tab fades back, the new one pops, and the glow (painted at the old x) slides over.
      options[before.index]?.setAttribute('data-was-selected', '')
      setMotion('moved')
      box.querySelector<HTMLElement>('[data-glow]')?.getBoundingClientRect() // style the glow at the old x first…
      setGlowX(x) // …so moving it runs the CSS transition (no frame wait: it works in a hidden tab too)
    }
    place()
    const watch = new MutationObserver(place)
    watch.observe(pill.current, { subtree: true, attributes: true, attributeFilter: ['data-selected'] })
    return () => watch.disconnect()
  }, [floating])

  // data-bottom-nav: the preview's V1 / V2 bubble shows only on screens that have a bottom navbar. V1's wrapper says
  // data-surface="primary" so the OS navigation bar still takes the navbar's colour (it looks for the page's last part).
  if (!floating) return <div className={styles.docked} data-bottom-nav="" data-surface="primary">{children}</div>
  return (
    <div className={styles.frame} data-floating-nav="" data-bottom-nav="" data-motion={motion} data-glow-at={glowBelow ? 'bottom' : undefined}>
      {/* The page's colour behind the nav: solid at the bottom, fading out above the pill. */}
      <div className={styles.fade} aria-hidden="true" />
      <div ref={pill} className={styles.pill}>
        {glowX !== null && <span className={styles.glow} data-glow="" style={{ '--glow-x': `${glowX}px` } as CSSProperties} aria-hidden="true" />}
        {children}
      </div>
    </div>
  )
}
```

### `src/shared/ui/IlliquidSheet.module.css`

```css
/* “What does illiquidity mean?” sheet — the DASH Pine Script sheet's points pattern, on L3 tokens. */
/* No padding of its own: the sheet's content area already frames it. */
.body { padding: 0; }
.points { display: flex; flex-direction: column; gap: var(--l3-spacing-12); margin: 0; padding: 0; list-style: none; }
.point { display: flex; align-items: center; gap: var(--l3-spacing-12); min-height: var(--l3-size-32); font: var(--l3-text-description-14); color: var(--l3-content-primary); }
.pointIcon { display: grid; flex: none; place-items: center; width: var(--l3-size-32); height: var(--l3-size-32); border-radius: var(--l3-radius-08); background: var(--l3-surface-secondary); color: var(--l3-content-secondary); }
```

### `src/shared/ui/IlliquidSheet.tsx`

```tsx
import { useId } from 'react'
import { BottomSheetHeader } from '@l3/components/BottomSheet'
import { Button } from '@l3/components/Button'
import { ButtonGroup } from '@l3/components/ButtonGroup'
import { Card } from '@l3/components/Card'
import { Icon } from '@l3/components/Icon'
import { msCompareArrows, msGroup, msShieldFill } from '@l3/icons/material'
import { Sheet } from './Sheet'
import styles from './IlliquidSheet.module.css'

export type IlliquidSheetCopy = {
  /** “What does illiquidity mean?” */
  title: string
  /** “{contract} is ILLIQUID right now”, or a general line. */
  description: string
  /** The three points: few traders · prices far apart (slippage) · Lemonn blocks orders. */
  points: [string, string, string]
  /** “Got it”. */
  ok: string
}

/**
 * “What does illiquidity mean?” — one sheet for every illiquid entry point in the app (F&O option chain, asset page,
 * Buy / Sell sheet, Gold Summary, Search). Small header, three icon + one-line points in a card (the DASH Pine Script
 * sheet's pattern), Got it. Each flow passes its own words (its copy.json).
 */
export function IlliquidSheet({ copy, onClose }: { copy: IlliquidSheetCopy; onClose: () => void }) {
  const id = useId()
  const icons = [msGroup, msCompareArrows, msShieldFill]
  return <Sheet labelledBy={id} onClose={onClose}
    header={<BottomSheetHeader headingId={id} heading={copy.title} description={copy.description} />}
    footer={<ButtonGroup aria-label={copy.title}><Button onClick={onClose}>{copy.ok}</Button></ButtonGroup>}>
    <div className={styles.body}>
      <Card as="section" aria-label={copy.title}>
        <ul className={styles.points}>{copy.points.map((text, i) => <li key={text} className={styles.point}>
          <span className={styles.pointIcon}><Icon icon={icons[i]} size={16} /></span>{text}
        </li>)}</ul>
      </Card>
    </div>
  </Sheet>
}
```

### `src/shared/ui/Rail.module.css`

```css
/*
 * Sideways rail. Item width = the row (inside its 16 insets) shared by `--rail-visible` items with 12 between them, so
 * the same rail reads well from 360 to 412. --rail-visible is a count (set inline), not a size.
 */
.rail {
  /* Positioned, so absolutely placed bits inside (e.g. PriceChange's screen-reader text) are clipped by the rail
     instead of hanging off a far-away ancestor and making the whole page scroll sideways. */
  position: relative;
  display: grid;
  grid-auto-flow: column;
  grid-auto-columns: calc((100% - (var(--rail-visible) - 1) * var(--l3-spacing-12)) / var(--rail-visible));
  gap: var(--l3-spacing-12);
  overflow-x: auto;
  overscroll-behavior-x: contain;
  padding-inline: var(--l3-spacing-16);
  scroll-padding-inline: var(--l3-spacing-16);
  scroll-snap-type: x mandatory;
  scrollbar-width: none;
  /* Room for the cards' shadow: a sideways scroller clips vertically too, so it pads 12 above and below and takes it
     back with a negative margin (same layout, shadow not cut). */
  padding-block: var(--l3-spacing-12);
  margin-block: calc(-1 * var(--l3-spacing-12));
}

.rail::-webkit-scrollbar {
  display: none;
}

.rail > * {
  scroll-snap-align: start;
  min-width: 0;
}

.rail[data-snap='center'] > * {
  scroll-snap-align: center;
}

/* Two rows that scroll together. */
.rail[data-rows='2'] {
  grid-auto-flow: column;
  grid-template-rows: repeat(2, auto);
}
```

### `src/shared/ui/Rail.tsx`

```tsx
import type { CSSProperties, ReactNode, Ref, UIEventHandler } from 'react'
import styles from './Rail.module.css'

type RailProps = {
  children: ReactNode
  /** What the row holds, for screen readers ("Top gainers"). */
  label: string
  /** How many items show across the screen — a fraction (2.3) lets the next one peek in, so it reads as scrollable. */
  visible: number
  /** Two rows that scroll together (a grid of cards). */
  rows?: 1 | 2
  /** Snap each item to the start (lists) or the centre (one featured card at a time, neighbours peeking). */
  snap?: 'start' | 'center'
  /** Extra room inside the row (e.g. above the cards, for a tag sitting on a card's top edge). */
  className?: string
  /** Called as the row scrolls (e.g. to follow which card is in view). */
  onScroll?: UIEventHandler<HTMLDivElement>
  /** The scrolling row itself (e.g. to scroll a tapped card into view). */
  railRef?: Ref<HTMLDivElement>
}

/**
 * A row that scrolls sideways — cards, baskets, ideas. Its first item lines up with the 16 page margin, items are
 * 12 apart and snap into place, and there's no scrollbar. Not L3 yet (a "carousel / rail" is missing there).
 */
export function Rail({ children, label, visible, rows = 1, snap = 'start', className, onScroll, railRef }: RailProps) {
  return (
    <div ref={railRef} className={[styles.rail, className].filter(Boolean).join(' ')} role="region" aria-label={label} data-rows={rows} data-snap={snap} style={{ '--rail-visible': visible } as CSSProperties} onScroll={onScroll}>
      {children}
    </div>
  )
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

### `src/shared/ui/ShortcutCircles.module.css`

```css
/* Shortcut circles (ShortcutCircles.tsx) — the Stocks Home's V6 look (flows/stocks/components/Home.module.css, "Small
   circles"). FLAG: raw mix / shadow values, as there (L3 has no coloured elevation or edge wash). */

.cell {
  --ring: var(--l3-content-accent-us-stock-default);
}
.cell[data-tone='in'] {
  --ring: var(--l3-content-accent-success-default);
}

/* The whole cell is the tap target: no card of its own (Figma 6754:62886 has none), rounded so its press layer isn't a hard box. */
.cell > .tap.tap.tap.tap { /* beats F&O Home's .flatCards ring on clickable cards */
  border-radius: var(--l3-radius-12);
  background: transparent;
  border-color: transparent;
  box-shadow: none;
}

.body {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--l3-spacing-08);
  padding-block: var(--l3-spacing-04);
  text-align: center;
}

.circle {
  display: inline-flex;
}

/* Figma 6754:62886 (24 Nov, user: "copy this exact design"): a 40 disc on surface-primary, a 1px subtle edge, a very
   soft glow; the 20 icon centred. FLAG (L3 gap): the 16 glow is a raw value (L3 has no such elevation). */
.disc.disc {
  background: var(--l3-surface-primary);
  box-shadow: inset 0 0 0 1px var(--l3-border-light), 0 0 var(--l3-spacing-16) color-mix(in srgb, var(--l3-content-secondary) 6%, transparent);
}

/* The 20 icon (Avatar's icon slot for a 40 avatar). */
.disc.disc > * {
  width: var(--l3-icon-size-20);
  height: var(--l3-icon-size-20);
}

/* The icon's colour is set on its own wrapper: L3 Avatar colours its icon slot itself. Artwork (an img) keeps its own colours. */
.icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: var(--l3-icon-size-20);
  height: var(--l3-icon-size-20);
  color: var(--ring);
}
.icon > img {
  display: block;
}

.label {
  font: var(--l3-text-label-12);
  color: var(--l3-content-secondary);
  white-space: nowrap;
}
```

### `src/shared/ui/ShortcutCircles.tsx`

```tsx
// Shortcut circles: the Stocks Home's shortcut row (Shortcuts V6, Figma 6662:8516) as a shared part, so every home
// that has a row of shortcuts draws them the same way (23 Nov, the user's call: F&O Home's shortcuts "same as the home
// page"). Four across: a 40 disc (white easing to a light grey, a 1px edge in the market's colour fading out, a very
// soft shadow) with a 24 icon in the market's colour, its name under it in secondary text. The whole cell is the tap target.
// Built from L3: the disc is an L3 Avatar (Type Icon, 40), the tap target a flat L3 Card, the layout Inset + Grid.
// FLAG (L3 gap): the disc's wash, edge and shadow are local (L3 Avatar has no such look); the Stocks Home still draws
// its own copy (flows/stocks/components/Instruments.tsx, look 'mini') — move it onto this part when that flow is next touched.
import type { ReactNode } from 'react'
import { Avatar } from '@l3/components/Avatar'
import { Card } from '@l3/components/Card'
import { Grid } from '@l3/components/Grid'
import { Inset } from '@l3/components/Inset'
import styles from './ShortcutCircles.module.css'

export type ShortcutCircle = { id: string; label: string; /** A 24 icon (L3 Icon); it takes the market's colour. */ icon: ReactNode }

/** `tone`: the market's colour for the icons and the disc's edge — `in` green (Indian markets), `us` blue (US Stocks). */
export function ShortcutCircles({ items, tone, label, onOpen }: { items: ShortcutCircle[]; tone: 'in' | 'us'; label: string; onOpen?: (id: string) => void }) {
  return (
    <Inset paddingInline="16" paddingBlock="00">
      <Grid columns={4} gap="08" role="list" aria-label={label}>
        {items.map((item) => (
          <div key={item.id} role="listitem" className={styles.cell} data-tone={tone}>
            <Card variant="flat" padding="none" className={styles.tap} onClick={() => onOpen?.(item.id)}>
              <span className={styles.body}>
                <span className={styles.circle}>
                  <Avatar size={40} className={styles.disc} icon={<span className={styles.icon}>{item.icon}</span>} />
                </span>
                <span className={styles.label}>{item.label}</span>
              </span>
            </Card>
          </div>
        ))}
      </Grid>
    </Inset>
  )
}
```

### `src/shared/ui/Splash.module.css`

```css
/* The launch splash: covers the app (above sheets and toasts) — the Lemonn logo centred on the page surface. */
.splash {
  position: absolute;
  inset: 0;
  z-index: var(--app-layer-splash);
  display: grid;
  place-items: center;
  background: var(--l3-surface-default);
  /* A button: no button chrome. */
  border: 0;
  padding: 0;
  cursor: pointer;
  transition: opacity var(--l3-motion-duration-medium) var(--l3-motion-easing-standard);
}

/* The logo rises in and settles as the splash opens. */
.logo {
  animation: logoIn var(--app-splash-in) var(--app-splash-ease-settle) both;
  animation-delay: var(--app-splash-logo-at);
}

@keyframes logoIn {
  from { opacity: 0; scale: 0.92; translate: 0 var(--l3-spacing-08); }
}

.splash[data-state='leaving'] {
  opacity: 0;
  pointer-events: none;
}

@media (prefers-reduced-motion: reduce) {
  .logo {
    animation: none;
  }

  .splash {
    transition-duration: 1ms;
  }
}
```

### `src/shared/ui/Splash.tsx`

```tsx
import { useEffect, useState, type ReactNode } from 'react'
import { BrandLogo } from '@l3/components/BrandLogo'
import { makeCopy } from '../copy'
import copy from './copy.json'
import styles from './Splash.module.css'

const t = makeCopy('shared', copy)

/**
 * The screens a launch can land on that open with the splash. Hidden for now (2026-11-04): none, so the app opens
 * straight on its page. To bring it back: ['stocks-01', 'fno-01'] (the two home pages).
 */
export const SPLASH_SCREENS: string[] = []
/** How long the logo stays before the splash fades away. */
export const SPLASH_MS = 1500

/**
 * Show the splash when the app launches (opens or reloads) onto a home page. A launch straight into an inner page (a
 * shared link to an L2 / L3 screen) skips it; so does every later move to a home page inside the app.
 */
export function shouldShowSplash(landing: string) {
  return SPLASH_SCREENS.includes(landing)
}

/** Longest the fade may take before the splash is removed anyway (a background tab never ends its transition). */
const FADE_FALLBACK_MS = 600

/**
 * The splash's own timing: shown for 1.5 s ('shown'), then fading ('leaving'), then gone ('done'). While `held` (prototype
 * only, see SplashCover) it stays shown; once let go it waits its 1.5 s again.
 */
function useSplashState(show: boolean, held = false) {
  const [state, setState] = useState<'shown' | 'leaving' | 'done'>(show ? 'shown' : 'done')
  useEffect(() => {
    if (state === 'done' || (state === 'shown' && held)) return
    const t = window.setTimeout(() => setState(state === 'shown' ? 'leaving' : 'done'), state === 'shown' ? SPLASH_MS : FADE_FALLBACK_MS)
    return () => window.clearTimeout(t)
  }, [state, held])
  return [state, setState] as const
}

/**
 * The white page with the Lemonn logo (lemon + name) in the middle, fading out once it's leaving. (The Diwali 2026
 * Garland splash and search bar are archived: src/shared/ui/archive/.)
 */
function SplashCover({ state, onHold, onLeave, onGone }: {
  state: 'shown' | 'leaving'
  onHold: (held: boolean) => void
  onLeave: () => void
  onGone: () => void
}) {
  // Prototype only (not app behaviour — leave out of the build): to look at the splash, hovering (mouse) holds it, a
  // tap / click pins it, and a second tap lets it fade.
  const [hovered, setHovered] = useState(false)
  const [pinned, setPinned] = useState(false)
  useEffect(() => onHold(hovered || pinned), [hovered, pinned]) // onHold is a new function every render
  return (
    <button
      type="button"
      className={styles.splash}
      data-state={state}
      aria-label={t('splash.label')}
      onClick={() => (pinned ? onLeave() : setPinned(true))}
      onPointerEnter={(e) => { if (e.pointerType === 'mouse') setHovered(true) }}
      onPointerLeave={(e) => { if (e.pointerType === 'mouse') setHovered(false) }}
      onTransitionEnd={(e) => { if (e.target === e.currentTarget) onGone() }}
    >
      <BrandLogo brand="lemonn" variant="full" size={48} decorative className={styles.logo} />
    </button>
  )
}

/**
 * The launch splash: the Lemonn logo in the middle of a plain screen for 1.5 seconds (it rises in as the splash opens),
 * then it fades and the home page
 * underneath shows. It covers the app (not the phone's status bar). Every launch onto a home page, reloads included.
 */
export function Splash({ landing }: { landing: string }) {
  const [held, setHeld] = useState(false)
  const [state, setState] = useSplashState(shouldShowSplash(landing), held)
  if (state === 'done') return null
  return <SplashCover state={state} onHold={setHeld} onLeave={() => setState('leaving')} onGone={() => setState('done')} />
}

/**
 * The splash as a page of its own (the Stocks and F&O flows list it before their home): it plays like the launch
 * splash — 1.5 s, then it fades over `home` (drawn underneath) and `onDone` moves to the home screen itself.
 */
export function SplashScreen({ home, onDone }: { home: ReactNode; onDone: () => void }) {
  const [held, setHeld] = useState(false)
  const [state, setState] = useSplashState(true, held)
  useEffect(() => {
    if (state === 'done') onDone()
  }, [state]) // once, when the splash is gone (onDone is a new function every render)
  return (
    <>
      {home}
      {state !== 'done' && <SplashCover state={state} onHold={setHeld} onLeave={() => setState('leaving')} onGone={() => setState('done')} />}
    </>
  )
}
```

### `src/shared/ui/TopBarAction.module.css`

```css
/* Home's round top-bar button (stocks TopBar .wallet): 38 circle, border/light edge, no shadow. L3 gap: see TopBarAction.tsx. */
.action.action {
  --btn-radius: var(--l3-radius-full);
  --btn-border: var(--l3-border-light);
  --btn-icon-size: var(--l3-icon-size-20);
  width: var(--app-stocks-topbar-control);
  height: var(--app-stocks-topbar-control);
  padding: 0;
}

/* A toggled action (pressed) takes border-dark, like any selected bordered control (as L3's ActionbarAction). */
.action.action[aria-pressed='true'] {
  --btn-border: var(--l3-border-dark);
}
```

### `src/shared/ui/TopBarAction.tsx`

```tsx
import { Button } from '@l3/components/Button'
import { Icon } from '@l3/components/Icon'
import { Stack } from '@l3/components/Stack'
import { msAccountBalanceWallet, msSearch } from '@l3/icons/material'
import styles from './TopBarAction.module.css'

/**
 * The app's icon button in a top bar (Actionbar `actions`): the same round button as Home's top bar — a 38 circle with
 * a 1px border/light edge, a 20 icon and no shadow — so every page's top-bar icons match.
 * It's L3's Tertiary Small button with three local changes (L3 gap: ActionbarAction is a 32 rounded square with
 * the tertiary border and a soft raise, no round option): fully round, border/light, raised none.
 * Icon-only actions with no box keep L3's `ActionbarAction variant="ghost"`.
 */
export function TopBarAction({ icon, label, onClick, pressed }: { icon: string; label: string; onClick: () => void; pressed?: boolean }) {
  return (
    <Button
      size="sm"
      variant="tertiary"
      raised="none"
      className={styles.action}
      iconLeft={<Icon icon={icon} size={20} />}
      onClick={onClick}
      aria-label={label}
      aria-pressed={pressed}
    />
  )
}

/**
 * The top bar's search and wallet, in this order, 8 apart — the same pair on every navbar tab (Stocks home, Market,
 * Portfolio, Mutual Fund), so nothing moves when you switch tabs. Copy it as is; don't redraw it per screen.
 */
export function SearchWalletActions({ searchLabel, walletLabel, onSearch, onWallet }: { searchLabel: string; walletLabel: string; onSearch: () => void; onWallet: () => void }) {
  return (
    <Stack direction="horizontal" align="center" gap="08">
      <TopBarAction icon={msSearch} label={searchLabel} onClick={onSearch} />
      <TopBarAction icon={msAccountBalanceWallet} label={walletLabel} onClick={onWallet} />
    </Stack>
  )
}
```

### `src/shared/ui/assets/floating-nav/fno-selected.svg`

```tsx
<svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="Options Botton Nav Icon 3">
<g id="Vector">
<path d="M19.9999 7.09802C19.9999 7.65031 19.5522 8.09802 18.9999 8.09802L15.7095 8.09802C15.3453 8.09802 15.0098 8.29607 14.8339 8.615L9.83879 17.6699C9.66285 17.9888 9.32742 18.1869 8.96318 18.1869H4.99989C4.44761 18.1869 3.9999 17.7392 3.9999 17.1869V17.1049C3.9999 16.5526 4.44761 16.1049 4.9999 16.1049H7.84407C8.20829 16.1049 8.54372 15.9068 8.71966 15.5879L13.7147 6.53392C13.8906 6.215 14.2261 6.01697 14.5903 6.01697H18.9999C19.5522 6.01697 19.9999 6.46469 19.9999 7.01697V7.09802ZM19.9286 16.9867C19.9286 17.539 19.4809 17.9867 18.9286 17.9867L14.9999 17.9867C14.4476 17.9867 13.9999 17.539 13.9999 16.9867V16.9047C13.9999 16.3524 14.4476 15.9047 14.9999 15.9047L18.9286 15.9047C19.4809 15.9047 19.9286 16.3524 19.9286 16.9047V16.9867Z" fill="#000" />
<path d="M3.9999 7.09882C3.9999 7.65116 4.44771 8.0989 5.00005 8.09882L9.00005 8.09818C9.55228 8.0981 9.9999 7.65041 9.9999 7.09818V7.01697C9.9999 6.46468 9.55218 6.01697 8.99989 6.01697L4.99989 6.01697C4.44761 6.01697 3.9999 6.46469 3.9999 7.01697V7.09882Z" fill="#000" />
</g>
</g>
</svg>
```

### `src/shared/ui/assets/floating-nav/fno.svg`

```tsx
<svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="Options Botton Nav Icon 2">
<g id="Vector">
<path d="M19.9999 7.09802C19.9999 7.65031 19.5522 8.09802 18.9999 8.09802L15.7095 8.09802C15.3453 8.09802 15.0098 8.29607 14.8339 8.615L9.83879 17.6699C9.66285 17.9888 9.32742 18.1869 8.96318 18.1869H4.99989C4.44761 18.1869 3.9999 17.7392 3.9999 17.1869V17.1049C3.9999 16.5526 4.44761 16.1049 4.9999 16.1049H7.84407C8.20829 16.1049 8.54372 15.9068 8.71966 15.5879L13.7147 6.53392C13.8906 6.215 14.2261 6.01697 14.5903 6.01697H18.9999C19.5522 6.01697 19.9999 6.46469 19.9999 7.01697V7.09802ZM19.9286 16.9867C19.9286 17.539 19.4809 17.9867 18.9286 17.9867L14.9999 17.9867C14.4476 17.9867 13.9999 17.539 13.9999 16.9867V16.9047C13.9999 16.3524 14.4476 15.9047 14.9999 15.9047L18.9286 15.9047C19.4809 15.9047 19.9286 16.3524 19.9286 16.9047V16.9867Z" fill="#000" />
<path d="M3.9999 7.09882C3.9999 7.65116 4.44771 8.0989 5.00005 8.09882L9.00005 8.09818C9.55228 8.0981 9.9999 7.65041 9.9999 7.09818V7.01697C9.9999 6.46468 9.55218 6.01697 8.99989 6.01697L4.99989 6.01697C4.44761 6.01697 3.9999 6.46469 3.9999 7.01697V7.09882Z" fill="#000" />
</g>
</g>
</svg>
```

### `src/shared/ui/assets/floating-nav/market-selected.svg`

```tsx
<svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="Frame 1000005189">
<path id="Union" d="M7.43553 13.6133C7.98781 13.6133 8.43553 14.061 8.43553 14.6133V18.4463C8.43552 18.9986 7.98781 19.4463 7.43553 19.4463H5.12498C4.57271 19.4463 4.125 18.9986 4.12498 18.4463V14.6133C4.12498 14.061 4.5727 13.6133 5.12498 13.6133H7.43553ZM12.8027 5.74611C13.355 5.74611 13.8027 6.19383 13.8027 6.74611V18.4453C13.8027 18.9976 13.355 19.4453 12.8027 19.4453H10.4922C9.93989 19.4453 9.49217 18.9976 9.49217 18.4453V6.74611C9.49218 6.19384 9.9399 5.74612 10.4922 5.74611H12.8027ZM18.1621 11.3438C18.7144 11.3438 19.1621 11.7915 19.1621 12.3438V18.4434C19.1621 18.9956 18.7144 19.4434 18.1621 19.4434H15.8515C15.2993 19.4434 14.8516 18.9956 14.8515 18.4434V12.3438C14.8515 11.7915 15.2993 11.3438 15.8515 11.3438H18.1621Z" fill="#000" />
</g>
</svg>
```

### `src/shared/ui/assets/floating-nav/market.svg`

```tsx
<svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="Frame 1000005188">
<path id="Union" d="M7.43553 13.6133C7.98781 13.6133 8.43553 14.061 8.43553 14.6133V18.4463C8.43552 18.9986 7.98781 19.4463 7.43553 19.4463H5.12498C4.57271 19.4463 4.125 18.9986 4.12498 18.4463V14.6133C4.12498 14.061 4.5727 13.6133 5.12498 13.6133H7.43553ZM12.8027 5.74611C13.355 5.74611 13.8027 6.19383 13.8027 6.74611V18.4453C13.8027 18.9976 13.355 19.4453 12.8027 19.4453H10.4922C9.93989 19.4453 9.49217 18.9976 9.49217 18.4453V6.74611C9.49218 6.19384 9.9399 5.74612 10.4922 5.74611H12.8027ZM18.1621 11.3438C18.7144 11.3438 19.1621 11.7915 19.1621 12.3438V18.4434C19.1621 18.9956 18.7144 19.4434 18.1621 19.4434H15.8515C15.2993 19.4434 14.8516 18.9956 14.8515 18.4434V12.3438C14.8515 11.7915 15.2993 11.3438 15.8515 11.3438H18.1621Z" fill="#000" />
</g>
</svg>
```

### `src/shared/ui/assets/floating-nav/mutual-fund.svg`

```tsx
<svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="Icon">
<path id="Vector" d="M5.03047 12.0001C5.03047 13.6284 5.51414 15.0754 6.48148 16.341C7.44881 17.6066 8.68217 18.4167 10.1815 18.7714C10.4073 18.8359 10.5967 18.9689 10.7499 19.1705C10.903 19.372 10.9796 19.6098 10.9796 19.8839C10.9796 20.2547 10.8224 20.557 10.508 20.7907C10.1936 21.0245 9.85103 21.085 9.48022 20.9721C7.46494 20.4078 5.83256 19.2994 4.58308 17.6469C3.3336 15.9944 2.70886 14.1121 2.70886 12.0001C2.70886 9.88805 3.3336 8.00577 4.58308 6.35324C5.83256 4.7007 7.46494 3.5923 9.48022 3.02802C9.85103 2.91516 10.1936 2.97562 10.508 3.20939C10.8224 3.44317 10.9796 3.74546 10.9796 4.11627C10.9796 4.39035 10.903 4.62815 10.7499 4.82968C10.5967 5.03121 10.4073 5.16422 10.1815 5.22871C8.68217 5.5834 7.44881 6.39354 6.48148 7.65914C5.51414 8.92474 5.03047 10.3717 5.03047 12.0001Z" fill="#000" />
<path id="Vector_2" d="M16.7106 20.0773C17.3877 19.6581 18.0084 19.1664 18.5727 18.6021C19.137 18.0379 19.6327 17.4131 20.06 16.7279C20.4872 16.0427 20.7895 15.2971 20.9668 14.4909C21.0475 14.104 20.9789 13.7574 20.7613 13.4511C20.5436 13.1447 20.2494 12.9916 19.8786 12.9916C19.6045 12.9916 19.3667 13.0682 19.1652 13.2213C18.9637 13.3745 18.8306 13.5639 18.7662 13.7896C18.5888 14.4023 18.3389 14.9666 18.0165 15.4825C17.694 15.9984 17.3152 16.474 16.8798 16.9093C16.4445 17.3446 15.9689 17.7235 15.453 18.0459C14.9371 18.3684 14.3809 18.6102 13.7844 18.7714C13.5587 18.8359 13.3692 18.9689 13.2161 19.1704C13.0629 19.372 12.9863 19.6098 12.9863 19.8839C12.9863 20.2547 13.1395 20.5489 13.4458 20.7665C13.7521 20.9842 14.0988 21.0527 14.4857 20.9721C15.2918 20.7948 16.0334 20.4965 16.7106 20.0773Z" fill="#000" />
<path id="Vector_3" d="M20.06 7.28433C19.6327 6.60719 19.137 5.98648 18.5727 5.4222C18.0084 4.85792 17.3877 4.36216 16.7106 3.93492C16.0334 3.50768 15.2918 3.20539 14.4857 3.02804C14.0988 2.94743 13.7521 3.01595 13.4458 3.2336C13.1395 3.45125 12.9863 3.74548 12.9863 4.1163C12.9863 4.39037 13.0629 4.62818 13.2161 4.82971C13.3692 5.03124 13.5587 5.16424 13.7844 5.22873C14.3809 5.38996 14.9371 5.63582 15.453 5.96633C15.9689 6.29684 16.4445 6.67974 16.8798 7.11504C17.3152 7.55034 17.694 8.02192 18.0165 8.52977C18.3389 9.03762 18.5888 9.59787 18.7662 10.2105C18.8306 10.4362 18.9637 10.6257 19.1652 10.7788C19.3667 10.932 19.6045 11.0086 19.8786 11.0086C20.2494 11.0086 20.5436 10.8554 20.7613 10.5491C20.9789 10.2428 21.0475 9.89614 20.9668 9.5092C20.7895 8.70309 20.4872 7.96146 20.06 7.28433Z" fill="#000" />
</g>
</svg>
```

### `src/shared/ui/assets/floating-nav/portfolio.svg`

```tsx
<svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="Icon">
<path id="Vector" d="M5.60779 10.9673C5.56188 11.0128 5.51552 11.0607 5.46875 11.111C5.51405 11.0628 5.56041 11.0149 5.60779 10.9673ZM12.3465 13.6011C11.353 13.2585 9.61878 12.4654 8.38278 10.8345C6.56251 10.8016 5.46875 11.111 5.46875 11.111C5.46875 11.111 6.06624 12.0923 7.31265 13.1392C8.33795 13.0754 9.51084 13.0886 10.7004 13.2736C11.2795 13.3646 11.8295 13.4764 12.3465 13.6011Z" fill-rule="evenodd" clip-rule="evenodd" fill="#000" />
<path id="Vector_2" d="M10.8387 17.76C9.90246 17.4565 8.29496 16.7642 7.02293 15.3313C5.48275 15.4306 4.22273 15.6775 3.78125 15.774C3.78125 15.774 4.5336 16.6893 5.6854 17.4895C6.67616 17.4064 8.06389 17.3997 9.8947 17.6143C10.2136 17.6526 10.5292 17.702 10.8387 17.76Z" fill-rule="evenodd" clip-rule="evenodd" fill="#000" />
<path id="Vector_3" d="M5.32422 19.6546C6.12798 20.5749 6.90023 21.1117 8.22407 21.6179C9.76855 22.2161 11.5179 21.986 12.3216 21.7713C11.7761 21.6565 9.68606 21.1927 7.9994 19.5387C6.4495 19.4355 5.59141 19.5868 5.32422 19.6546Z" fill-rule="evenodd" clip-rule="evenodd" fill="#000" />
<path id="Vector_4" d="M12.5281 1.99988L12.3547 2.32198C11.8031 3.33431 11.5982 4.45401 11.7085 5.51235C11.8977 7.29159 12.9693 8.94813 14.7029 9.85309L14.8763 9.53098C15.5855 8.2579 15.7116 6.83144 15.3806 5.52769C14.9866 4.08589 14.0095 2.76679 12.5281 1.99988Z" fill="#000" fill-opacity="0.667"/>
<path id="Vector_5" d="M20.2351 8.24279C19.715 9.17843 18.8798 9.83797 17.9184 10.1447C16.894 10.4822 15.7277 10.4055 14.7033 9.88398C15.2234 8.94834 16.0745 8.2888 17.0358 7.98204C18.0445 7.64459 19.2107 7.70595 20.2351 8.24279Z" fill="#000" fill-opacity="0.667"/>
<path id="Vector_6" d="M8.38279 10.8345C8.92603 10.8443 9.53398 10.8846 10.1968 10.9728C14.058 11.4943 14.5308 10.2672 14.5308 10.2672C14.5308 10.2672 12.75 8.70265 9.81863 8.9634C8.08764 9.1099 6.61531 9.95616 5.6078 10.9673C5.56041 11.0149 5.51406 11.0628 5.46875 11.111C5.46875 11.111 6.56252 10.8016 8.38279 10.8345Z" fill="#000" fill-opacity="0.667"/>
<path id="Vector_7" d="M10.6985 13.2735C9.50894 13.0885 8.33605 13.0753 7.31074 13.1391C5.70085 13.2393 4.45482 13.5292 4.07932 13.6416C4.06357 13.6416 4.04782 13.6569 4.03206 13.6723C4.0163 13.6876 4.00052 13.703 4.00052 13.7336C3.85868 14.2398 3.71807 15.053 3.78111 15.7739C4.22258 15.6775 5.4826 15.4305 7.02278 15.3313C8.17675 15.2569 9.48798 15.2654 10.73 15.4822C13.488 15.9577 15.9624 17.2001 16.7346 17.5989C16.7425 17.5989 16.7464 17.6027 16.7504 17.6066C16.7543 17.6104 16.7582 17.6142 16.7661 17.6142C16.7976 17.6142 16.8292 17.5989 16.8449 17.5529C17.0656 16.8933 17.1916 16.0804 17.2074 15.5436C17.2074 15.5282 17.2074 15.5129 17.1916 15.4975C17.1916 15.4822 17.1759 15.4669 17.1601 15.4669C16.7389 15.1978 14.9653 14.2333 12.3445 13.601C11.8275 13.4763 11.2776 13.3645 10.6985 13.2735Z" fill-rule="evenodd" clip-rule="evenodd" fill="#000" fill-opacity="0.667"/>
<path id="Vector_8" d="M5.68528 17.4895C6.67603 17.4064 8.06377 17.3997 9.89458 17.6143C10.2134 17.6526 10.529 17.702 10.8386 17.76C13.1302 18.1888 15.0972 19.0845 15.6942 19.4089C15.7257 19.4242 15.7415 19.4395 15.7415 19.4549C15.7415 19.4702 15.7415 19.5009 15.7257 19.5316C15.4263 19.9304 14.7959 20.5132 14.197 20.8967C14.1497 20.9273 14.1025 20.9427 14.0394 20.9427C14.0079 20.9427 13.9764 20.9273 13.9449 20.912C13.4405 20.6666 11.9591 20.0837 9.9261 19.7616C9.19278 19.6447 8.55203 19.5755 7.99928 19.5387C6.44937 19.4354 5.59129 19.5867 5.3241 19.6545C4.7725 19.041 4.34705 18.1818 4.18945 17.8137C4.18945 17.783 4.18947 17.7523 4.20523 17.737C4.22098 17.7216 4.23674 17.7063 4.25249 17.7063C4.57357 17.6282 5.04706 17.543 5.68528 17.4895Z" fill-rule="evenodd" clip-rule="evenodd" fill="#000" fill-opacity="0.667"/>
</g>
</svg>
```

### `src/shared/ui/assets/floating-nav/stocks.svg`

```tsx
<svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="Frame">
<path id="Vector" d="M10.45 12.62L11.82 13.99C11.9867 14.1633 12.1967 14.25 12.45 14.25C12.7033 14.25 12.9167 14.1633 13.09 13.99L16.26 10.83V12.03C16.26 12.2367 16.3333 12.41 16.48 12.55C16.6267 12.69 16.8 12.7567 17 12.75C17.2067 12.75 17.3833 12.6767 17.53 12.53C17.6767 12.3833 17.75 12.2067 17.75 12V9.15C17.75 8.89667 17.6633 8.68333 17.49 8.51C17.3167 8.33667 17.1033 8.25 16.85 8.25H13.98C13.7733 8.25 13.6 8.32333 13.46 8.47C13.32 8.61667 13.25 8.79333 13.25 9C13.25 9.21333 13.3233 9.39 13.47 9.53C13.6167 9.67 13.7933 9.74333 14 9.75H15.17L12.45 12.51L11.08 11.14C10.9067 10.96 10.6933 10.87 10.44 10.87C10.1867 10.87 9.98 10.96 9.82 11.14L6.87 14.07C6.72333 14.2167 6.65 14.3933 6.65 14.6C6.65 14.8067 6.72333 14.98 6.87 15.12C7.01667 15.2733 7.19333 15.35 7.4 15.35C7.60667 15.35 7.78 15.2733 7.92 15.12L10.44 12.61L10.45 12.62ZM5.31 20.5C4.80333 20.5 4.37667 20.3267 4.03 19.98C3.68333 19.6333 3.50667 19.2033 3.5 18.69V5.31C3.5 4.80333 3.67333 4.37667 4.02 4.03C4.36667 3.68333 4.79667 3.50667 5.31 3.5H18.69C19.1967 3.5 19.6233 3.67333 19.97 4.02C20.3167 4.36667 20.4933 4.79667 20.5 5.31V18.69C20.5 19.1967 20.3267 19.6233 19.98 19.97C19.6333 20.3167 19.2033 20.4933 18.69 20.5H5.31Z" fill="#000"/>
</g>
</svg>
```

### `src/shared/ui/copy.json`

```json
{
  "splash.label": "Lemonn"
}
```

### `src/shared/ui/dash/DashEntry.module.css`

```css
/*
 * DASH pill — Figma "Dash entry point" (DASH AI main flow, 11492:7740), copied as drawn: hugs its content (4 / 8
 * padding, 2 between the orb and the word), full radius, a 1px green-300 edge, a 176° fill from surface/primary
 * (37.5%) into the brand-light lime (93.4%), the orb at 21.8 without its halo, "DASH" in Heading/10, success green.
 */
.entry {
  display: inline-flex;
  flex: none;
  align-items: center;
  gap: var(--l3-spacing-02);
  padding: var(--l3-spacing-04) var(--l3-spacing-08);
  border: 1px solid var(--l3-base-hue-green-300); /* 1px: Figma stroke */
  border-radius: var(--l3-radius-full);
  background: linear-gradient(176deg, var(--l3-surface-primary) 37.508%, var(--l3-surface-accent-brand-light) 93.358%);
  color: var(--l3-content-accent-success-default);
  cursor: pointer;
  -webkit-tap-highlight-color: transparent;
  transition: transform var(--l3-motion-duration-short) var(--l3-motion-easing-standard);
}

.entry:active {
  transform: scale(var(--l3-motion-scale-press-default));
}

.entry:focus-visible {
  outline: 2px solid var(--l3-content-primary);
  outline-offset: 2px;
}

/* Figma "logo": 21.818 (local token — no L3 size). */
.entry > span:first-child {
  --orb-box: var(--app-dash-orb-pill);
}

.label {
  font: var(--l3-text-heading-10);
  text-align: center;
  white-space: nowrap;
}
```

### `src/shared/ui/dash/DashEntry.tsx`

```tsx
import { DashOrb } from './DashOrb'
import styles from './DashEntry.module.css'

type DashEntryProps = {
  /** The visible word ("DASH"), from the caller's copy file. */
  label: string
  /** What a screen reader says ("Open DASH AI"). */
  ariaLabel: string
  onClick?: () => void
}

/**
 * The way into DASH AI — a pill in the Stocks home top bar (Figma "Dash entry point", DASH AI main flow 11492:7740):
 * the orb and "DASH" on a white-into-lime fill with a thin green edge. It hugs its content (≈ 32 tall).
 */
export function DashEntry({ label, ariaLabel, onClick }: DashEntryProps) {
  return (
    <button type="button" className={styles.entry} onClick={onClick} aria-label={ariaLabel}>
      <DashOrb size="sm" halo={false} />
      <span className={styles.label} aria-hidden="true">{label}</span>
    </button>
  )
}
```

### `src/shared/ui/dash/DashOrb.module.css`

```css
/*
 * The orb artwork is the Figma vector component: every part keeps the exact Figma box (px inside a 100 × 100 frame —
 * artwork geometry, not layout), and the whole thing scales to the slot. Sizes come from L3 size tokens.
 */
.orb {
  --orb-box: var(--l3-size-96);
  position: relative;
  display: inline-block;
  flex: none;
  width: var(--orb-box);
  height: var(--orb-box);
}

.orb[data-size='lg'] { --orb-box: var(--l3-size-96); }
.orb[data-size='md'] { --orb-box: var(--l3-size-64); }
.orb[data-size='compact'] { --orb-box: var(--l3-size-40); }
.orb[data-size='sm'] { --orb-box: var(--l3-size-32); }

/* The art is drawn at 100 and scaled to the box. */
.scale {
  position: absolute;
  top: 0;
  left: 0;
  width: 100px;
  height: 100px;
  transform: scale(calc(var(--orb-box) / 100px));
  transform-origin: 0 0;
}

.art {
  position: absolute;
  inset: 0;
}

/* Figma: the halo copy sits 8 right / 10 down, layer blur 23.35. */
.halo {
  transform: translate(8px, 10px);
  filter: blur(var(--app-dash-orb-halo-blur));
}

.art img {
  display: block;
  max-width: none;
}

/* "Group 1000006113" (back leaf, blurred glow): box 55.5 × 57.8, bottom 49.7, centre +17.2. */
.leafBackBox,
.leafFrontBox {
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  transform: translateX(-50%);
}

.leafBackBox {
  bottom: 49.71px;
  left: calc(50% + 17.24px);
  width: 55.526px;
  height: 57.791px;
}

.leafBack,
.leafFront {
  position: relative;
  flex: none;
  /* Figma's order: rotate, then skew, then the vertical flip (Tailwind -scale-y-100 rotate-[-108.93deg] skew-x-1) */
  transform: rotate(-108.93deg) skewX(1deg) scaleY(-1);
}

.leafBack {
  width: 45.469px;
  height: 43.372px;
}

.leafBackImg {
  position: absolute;
  inset: -14.91% -14.25% -14.71% -13.92%;
  width: auto;
  height: auto;
}

/* "Group 1000006112" (front leaves). */
.leafFrontBox {
  bottom: 50.97px;
  left: calc(50% + 17.61px);
  width: 50.159px;
  height: 51.373px;
}

.leafFront {
  width: 40.069px;
  height: 39.526px;
}

.leafFront img {
  width: 100%;
  height: 100%;
}

/* "Ellipse 8": the ring's soft inner fill. */
.fill {
  position: absolute;
  top: 30.85px;
  left: 10.38px;
  width: 57.662px;
  height: 59.282px;
}

/* "circleGroup": the angular-gradient ring. */
.ringBox {
  position: absolute;
  top: 27.88px;
  left: 7.5px;
  width: 62.852px;
  height: 64.618px;
}

.ring {
  position: absolute;
  inset: -7.11% -7.31%;
  width: auto;
  height: auto;
}

/*
 * Idle motion (live app, 2026-10-23): the ring's yellow highlight goes round clockwise once a second, at a steady
 * speed — the ring and its soft fill turn on their own centres; the leaves stay still. Off for reduced motion.
 */
.ringBox,
.fill {
  animation: dash-orb-spin var(--app-dash-orb-spin) linear infinite;
}

@keyframes dash-orb-spin {
  to {
    transform: rotate(1turn);
  }
}

@media (prefers-reduced-motion: reduce) {
  .ringBox,
  .fill {
    animation: none;
  }
}
```

### `src/shared/ui/dash/DashOrb.tsx`

```tsx
import leafBack from './assets/leaf-back.svg'
import leafFront from './assets/leaf-front.svg'
import orbFill from './assets/orb-fill.svg'
import orbRing from './assets/orb-ring.svg'
import styles from './DashOrb.module.css'

export type DashOrbSize = 'sm' | 'compact' | 'md' | 'lg' // 32 · 40 · 64 · 96

/**
 * DASH's mascot — the lime ring with two leaves (Figma "Logo" / "BotIcon", the 100 × 100 vector component), drawn from
 * its own vector parts in the Figma positions, with the soft halo behind it (a blurred copy).
 * Sizes: lg 96 (landing pages), md 64 (sheet headers, on a soft disc), sm 32 (the rule card's icon). The DASH pill sets its own
 * box (21.8). Shared: DASH flows and the home's entry pill use the same artwork.
 * Decorative: screen readers skip it — the text next to it says what it is.
 */
export function DashOrb({ size = 'lg', halo = true }: { size?: DashOrbSize; halo?: boolean }) {
  return (
    <span className={styles.orb} data-size={size} aria-hidden="true">
      <span className={styles.scale}>
        {halo && <OrbArt className={styles.halo} />}
        <OrbArt />
      </span>
    </span>
  )
}

/** The artwork at its Figma size (100 × 100); the parent scales it. */
function OrbArt({ className }: { className?: string }) {
  return (
    <span className={[styles.art, className].filter(Boolean).join(' ')}>
      <span className={styles.leafBackBox}>
        <span className={styles.leafBack}>
          <img src={leafBack} alt="" className={styles.leafBackImg} />
        </span>
      </span>
      <span className={styles.leafFrontBox}>
        <span className={styles.leafFront}>
          <img src={leafFront} alt="" />
        </span>
      </span>
      <img src={orbFill} alt="" className={styles.fill} />
      <span className={styles.ringBox}>
        <img src={orbRing} alt="" className={styles.ring} />
      </span>
    </span>
  )
}
```

### `src/shared/ui/dash/assets/leaf-back.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="58.2771" height="56.2179" viewBox="0 0 58.2771 56.2179" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="Group 1000006113" filter="url(#filter0_f_0_282)">
<path id="Big_leaf_00000052817416241482779350000003325489541389591972_" d="M11.1805 6.4948L10.2325 8.23984C7.21698 13.7241 6.07176 19.8031 6.63218 25.5588C7.5941 35.2352 13.3302 44.2732 22.6694 49.2476L23.6172 47.5025C27.4934 40.6061 28.2232 32.8573 26.4785 25.7606C24.3978 17.9116 19.1614 10.7108 11.1805 6.4948Z" fill="#8EF087" style="fill:#8EF087;fill:color(display-p3 0.5578 0.9428 0.5275);fill-opacity:1;"/>
<path id="Small_leaf_00000086657169406454258550000009755690847739837326_" d="M51.7823 38.3919C48.9397 43.4603 44.4029 47.018 39.1965 48.6543C33.6484 50.4553 27.3477 50.0009 21.8287 47.1335C24.6713 42.065 29.2933 38.5078 34.4997 36.8715C39.9626 35.07 46.2638 35.4411 51.7823 38.3919Z" fill="#8EF087" style="fill:#8EF087;fill:color(display-p3 0.5578 0.9428 0.5275);fill-opacity:1;"/>
</g>
<defs>
<filter id="filter0_f_0_282" x="-7.45058e-08" y="2.2538e-07" width="58.2771" height="56.2179" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
<feFlood flood-opacity="0" result="BackgroundImageFix"/>
<feBlend mode="normal" in="SourceGraphic" in2="BackgroundImageFix" result="shape"/>
<feGaussianBlur stdDeviation="3.2474" result="effect1_foregroundBlur_0_282"/>
</filter>
</defs>
</svg>
```

### `src/shared/ui/dash/assets/leaf-front.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="40.0692" height="39.5257" viewBox="0 0 40.0692 39.5257" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="Group 1000006112">
<path id="Small_leaf_00000086657169406454258550000009755690847739837326_" d="M40.0554 29.6165C37.5947 34.0042 33.6673 37.084 29.1603 38.5005C24.3574 40.0595 18.9031 39.6661 14.1254 37.1839C16.5862 32.7963 20.5873 29.7169 25.0943 28.3004C29.8234 26.7409 35.2782 27.0621 40.0554 29.6165Z" fill="url(#paint0_linear_0_409)"/>
<path id="Big_leaf_00000052817416241482779350000003325489541389591972_" d="M4.19434 0.0243672L3.37396 1.5349C0.764101 6.28215 -0.226587 11.5445 0.259219 16.5271C1.09303 24.9038 6.05968 32.7283 14.1449 37.0356L14.9652 35.525C18.3199 29.5554 18.9507 22.8476 17.4396 16.704C15.6376 9.90912 11.1037 3.67494 4.19434 0.0243672Z" fill="url(#paint1_linear_0_409)"/>
</g>
<defs>
<linearGradient id="paint0_linear_0_409" x1="21.3968" y1="29.3938" x2="22.0238" y2="39.1604" gradientUnits="userSpaceOnUse">
<stop stop-color="#7CE883" style="stop-color:#7CE883;stop-color:color(display-p3 0.4863 0.9098 0.5137);stop-opacity:1;"/>
<stop offset="1" stop-color="#3EBF47" style="stop-color:#3EBF47;stop-color:color(display-p3 0.2433 0.7503 0.2802);stop-opacity:1;"/>
</linearGradient>
<linearGradient id="paint1_linear_0_409" x1="5.24577" y1="6.42552" x2="13.4379" y2="33.8372" gradientUnits="userSpaceOnUse">
<stop stop-color="#7CE883" style="stop-color:#7CE883;stop-color:color(display-p3 0.4863 0.9098 0.5137);stop-opacity:1;"/>
<stop offset="1" stop-color="#3EBF47" style="stop-color:#3EBF47;stop-color:color(display-p3 0.2433 0.7503 0.2802);stop-opacity:1;"/>
</linearGradient>
</defs>
</svg>
```

### `src/shared/ui/dash/assets/orb-fill.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="57.6624" height="59.2824" viewBox="0 0 57.6624 59.2824" fill="none" xmlns="http://www.w3.org/2000/svg">
<mask id="stroke0_0_416" fill="white">
<path d="M57.6624 29.6412C57.6624 46.0116 44.7543 59.2824 28.8312 59.2824C12.9082 59.2824 0 46.0116 0 29.6412C0 13.2708 12.9082 0 28.8312 0C44.7543 0 57.6624 13.2708 57.6624 29.6412Z"/>
</mask>
<path id="Ellipse 8" d="M57.6624 29.6412C57.6624 46.0116 44.7543 59.2824 28.8312 59.2824C12.9082 59.2824 0 46.0116 0 29.6412C0 13.2708 12.9082 0 28.8312 0C44.7543 0 57.6624 13.2708 57.6624 29.6412Z" stroke-width="16.8671" stroke="url(#paint0_linear_0_416)" mask="url(#stroke0_0_416)"/>
<defs>
<linearGradient id="paint0_linear_0_416" x1="17.0104" y1="56.2094" x2="43.5226" y2="4.92706" gradientUnits="userSpaceOnUse">
<stop stop-color="#72E780" style="stop-color:#72E780;stop-color:color(display-p3 0.4476 0.9047 0.5009);stop-opacity:1;"/>
<stop offset="1" stop-color="#FDFFB5" style="stop-color:#FDFFB5;stop-color:color(display-p3 0.9903 1.0000 0.7091);stop-opacity:1;"/>
</linearGradient>
</defs>
</svg>
```

### `src/shared/ui/dash/assets/orb-ring.svg`

```tsx
<svg preserveAspectRatio="none" overflow="visible" style="display: block;" width="72.0446" height="73.8103" viewBox="0 0 72.0446 73.8103" fill="none" xmlns="http://www.w3.org/2000/svg">
<g id="circleGroup">
<g id="Ellipse 9" filter="url(#filter0_f_0_407)">
<mask id="stroke0_0_407" fill="white">
<path d="M67.4483 36.9052C67.4483 54.7489 53.3784 69.2141 36.0223 69.2141C18.6662 69.2141 4.59628 54.7489 4.59628 36.9052C4.59628 19.0615 18.6662 4.59628 36.0223 4.59628C53.3784 4.59628 67.4483 19.0615 67.4483 36.9052Z"/>
</mask>
<mask id="stroke1_0_407">
<path d="M67.4483 36.9052C67.4483 54.7489 53.3784 69.2141 36.0223 69.2141C18.6662 69.2141 4.59628 54.7489 4.59628 36.9052C4.59628 19.0615 18.6662 4.59628 36.0223 4.59628C53.3784 4.59628 67.4483 19.0615 67.4483 36.9052Z" stroke-width="18.3851" stroke="white" mask="url(#stroke0_0_407)"/>
</mask>
<g clip-path="url(#paint0_angular_0_407_clip_path)" data-figma-skip-parse="true" mask="url(#stroke1_0_407)"><g transform="matrix(0.01625 -0.02375 0.0230642 0.0166474 37.0963 36.713)"><foreignObject x="-3827.82" y="-3827.82" width="7655.64" height="7655.64"><div xmlns="http://www.w3.org/1999/xhtml" style="background:conic-gradient(from 90deg,rgba(121, 234, 105, 1) 0deg,rgba(246, 253, 38, 1) 124.615deg,rgba(52, 177, 33, 1) 238.846deg,rgba(122, 235, 105, 1) 360deg);height:100%;width:100%;opacity:1"></div></foreignObject></g></g><path d="M67.4483 36.9052C67.4483 54.7489 53.3784 69.2141 36.0223 69.2141C18.6662 69.2141 4.59628 54.7489 4.59628 36.9052C4.59628 19.0615 18.6662 4.59628 36.0223 4.59628C53.3784 4.59628 67.4483 19.0615 67.4483 36.9052Z" stroke-width="18.3851" stroke="black" stroke-opacity="0" data-figma-gradient-stroke="{&#34;type&#34;:&#34;GRADIENT_ANGULAR&#34;,&#34;stops&#34;:[{&#34;color&#34;:{&#34;r&#34;:0.47711750864982605,&#34;g&#34;:0.92151820659637451,&#34;b&#34;:0.41342675685882568,&#34;a&#34;:1.0},&#34;position&#34;:0.0},{&#34;color&#34;:{&#34;r&#34;:0.96524602174758911,&#34;g&#34;:0.99325793981552124,&#34;b&#34;:0.15290218591690063,&#34;a&#34;:1.0},&#34;position&#34;:0.34615385532379150},{&#34;color&#34;:{&#34;r&#34;:0.20681096613407135,&#34;g&#34;:0.69540637731552124,&#34;b&#34;:0.13164243102073669,&#34;a&#34;:1.0},&#34;position&#34;:0.66346156597137451},{&#34;color&#34;:{&#34;r&#34;:0.47843137383460999,&#34;g&#34;:0.92156863212585449,&#34;b&#34;:0.41176471114158630,&#34;a&#34;:1.0},&#34;position&#34;:1.0}],&#34;transform&#34;:{&#34;m00&#34;:32.500003814697266,&#34;m01&#34;:46.128456115722656,&#34;m02&#34;:-2.2179441452026367,&#34;m10&#34;:-47.500007629394531,&#34;m11&#34;:33.294700622558594,&#34;m12&#34;:43.815639495849609},&#34;opacity&#34;:1.0,&#34;blendMode&#34;:&#34;NORMAL&#34;,&#34;stopsVar&#34;:[{&#34;color&#34;:{&#34;r&#34;:0.47711750864982605,&#34;g&#34;:0.92151820659637451,&#34;b&#34;:0.41342675685882568,&#34;a&#34;:1.0},&#34;position&#34;:0.0},{&#34;color&#34;:{&#34;r&#34;:0.96524602174758911,&#34;g&#34;:0.99325793981552124,&#34;b&#34;:0.15290218591690063,&#34;a&#34;:1.0},&#34;position&#34;:0.34615385532379150},{&#34;color&#34;:{&#34;r&#34;:0.20681096613407135,&#34;g&#34;:0.69540637731552124,&#34;b&#34;:0.13164243102073669,&#34;a&#34;:1.0},&#34;position&#34;:0.66346156597137451},{&#34;color&#34;:{&#34;r&#34;:0.47843137383460999,&#34;g&#34;:0.92156863212585449,&#34;b&#34;:0.41176471114158630,&#34;a&#34;:1.0},&#34;position&#34;:1.0}],&#34;visible&#34;:true}" mask="url(#stroke0_0_407)"/>
</g>
</g>
<defs>
<filter id="filter0_f_0_407" x="0" y="0" width="72.0446" height="73.8103" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
<feFlood flood-opacity="0" result="BackgroundImageFix"/>
<feBlend mode="normal" in="SourceGraphic" in2="BackgroundImageFix" result="shape"/>
<feGaussianBlur stdDeviation="2.29814" result="effect1_foregroundBlur_0_407"/>
</filter>
<clipPath id="paint0_angular_0_407_clip_path"><rect x="-41.3666" y="-41.3666" width="154.778" height="156.543"/></clipPath></defs>
</svg>
```

### `src/shared/ui/useSwipeBetween.ts`

```ts
import { useCallback, useLayoutEffect, useRef } from 'react'

// Ported from the US Stocks prototype (screens/home/useSwipeBetween.ts): swipe a page sideways to the next one —
// Stocks Home (IND ↔ US), a theme page, the Market list tabs.
// FLAG: hand-made swipe gesture (pointer events + translate) — L3 has no swipeable pages.

const MIN_DISTANCE = 48
const MIN_VELOCITY = 0.45
const EASING = 'cubic-bezier(0.2, 0, 0, 1)'
const SLIDE_MS = 280
// The rest of the page: a quick dissolve, done while the card is still moving.
const FADE_OUT_MS = 100
const FADE_IN_MS = 200

const reducedMotion = () => typeof matchMedia !== 'undefined' && matchMedia('(prefers-reduced-motion: reduce)').matches

/** The item `step` places after/before `current` in `list`, or null at the ends. */
export const neighbour = <T,>(list: T[], current: T, step: number): T | null => {
  const at = list.indexOf(current) + step
  return at >= 0 && at < list.length ? list[at] : null
}

// Is there a sideways-scrolling element between the touch target and the swipe container (a card rail)? Then it scrolls, not swipes.
const insideSideScroller = (from: HTMLElement | null, stop: HTMLElement) => {
  for (let el = from; el && el !== stop; el = el.parentElement) {
    const overflowX = getComputedStyle(el).overflowX
    if ((overflowX === 'auto' || overflowX === 'scroll') && el.scrollWidth > el.clientWidth + 1) return true
  }
  return false
}

/** Pointer-swipe on an element: `onSwipe(±1)` when released far/fast enough, `onDrag(dx)` while dragging (null when it ends). */
function useSwipe(onSwipe: (direction: 1 | -1) => void, onDrag: (dx: number | null) => void, area?: string) {
  const swipeRef = useRef(onSwipe)
  swipeRef.current = onSwipe
  const dragRef = useRef(onDrag)
  dragRef.current = onDrag
  const cleanup = useRef<(() => void) | null>(null)

  return useCallback((el: HTMLElement | null) => {
    cleanup.current?.()
    cleanup.current = null
    if (!el) return
    el.style.touchAction = 'pan-y'
    let start: { x: number; y: number; t: number; id: number } | null = null
    let swiped = false
    let dragging = false

    const down = (e: PointerEvent) => {
      const target = e.target as HTMLElement
      // `data-own-swipe`: a part with its own swipe (the activation card's benefits strip) keeps the gesture.
      if (e.button !== 0 || target.closest('input, textarea, [role="dialog"], [contenteditable], [data-own-swipe]') || insideSideScroller(target, el)) return
      // `area`: the swipe starts only there (the top card), not anywhere on the page.
      if (area && !target.closest(area)) return
      start = { x: e.clientX, y: e.clientY, t: e.timeStamp, id: e.pointerId }
      swiped = false
      dragging = false
    }
    const move = (e: PointerEvent) => {
      if (!start || e.pointerId !== start.id || !dragRef.current) return
      const dx = e.clientX - start.x
      const dy = e.clientY - start.y
      if (!dragging) {
        if (Math.hypot(dx, dy) < 8) return
        if (Math.abs(dx) < Math.abs(dy) * 1.5) {
          start = null
          return
        }
        dragging = true
      }
      dragRef.current(dx)
    }
    const up = (e: PointerEvent) => {
      if (!start || e.pointerId !== start.id) return
      const dx = e.clientX - start.x
      const dy = e.clientY - start.y
      const velocity = Math.abs(dx) / Math.max(1, e.timeStamp - start.t)
      start = null
      if (dragging) dragRef.current?.(null)
      dragging = false
      if (Math.abs(dx) < Math.abs(dy) * 1.5) return
      if (Math.abs(dx) >= MIN_DISTANCE || (Math.abs(dx) >= 24 && velocity >= MIN_VELOCITY)) {
        swiped = true
        swipeRef.current(dx < 0 ? 1 : -1)
      }
    }
    const cancel = () => {
      if (dragging) dragRef.current?.(null)
      start = null
      dragging = false
    }
    // A swipe that ends on a button must not also click it.
    const click = (e: Event) => {
      if (swiped) {
        swiped = false
        e.preventDefault()
        e.stopPropagation()
      }
    }
    el.addEventListener('pointerdown', down)
    el.addEventListener('pointermove', move)
    el.addEventListener('pointerup', up)
    el.addEventListener('pointercancel', cancel)
    el.addEventListener('click', click, true)
    cleanup.current = () => {
      el.removeEventListener('pointerdown', down)
      el.removeEventListener('pointermove', move)
      el.removeEventListener('pointerup', up)
      el.removeEventListener('pointercancel', cancel)
      el.removeEventListener('click', click, true)
    }
  }, [])
}

/**
 * Swipe between two markets' pages: only the top cards move sideways — a track with both, the other one beside it,
 * follows the finger and slides across so the other market's card comes into view, as in a carousel — while the rest of the page (`fades()`) just dissolves
 * into the other market's. A tap on a switcher (`go`) runs the same switch, so a swipe and a tap look alike.
 * `bind` goes on the scroll container; `area` is where a swipe may start (the cards); `slides()` returns what moves
 * sideways (the cards' track), `fades()` what dissolves (the feed under it).
 */
export function useSwipeBetween({ canGo, onSwitch, page, area, slides, fades }: { canGo: (direction: 1 | -1) => boolean; onSwitch: (direction: 1 | -1) => void; page: string; area?: string; slides: () => HTMLElement[]; fades: () => HTMLElement[] }) {
  const entering = useRef<number>(0)
  const settling = useRef(false)
  const leaving = useRef(false)
  const pageNow = useRef(page)
  pageNow.current = page

  const springBack = () => {
    for (const el of slides()) {
      if (!el.style.translate) continue
      const from = { translate: el.style.translate }
      el.style.translate = ''
      el.animate([from, { translate: '0 0' }], { duration: 240, easing: EASING })
    }
  }

  // The track slides to the other card (from where the finger left it) as the rest fades out; then the switch.
  const leave = (direction: 1 | -1, commit: () => void) => {
    if (leaving.current) return
    entering.current = direction
    const moving = slides()
    const dissolving = fades()
    if (reducedMotion() || (!moving.length && !dissolving.length)) return commit()
    leaving.current = true
    Promise.all([
      ...moving.map((el) => {
        const from = { translate: el.style.translate || '0 0' }
        el.style.translate = ''
        // The track moves one card's width: the other card is then where this one was.
        return el.animate([from, { translate: `${-direction * el.offsetWidth}px 0` }], { duration: SLIDE_MS, easing: EASING, fill: 'forwards' }).finished
      }),
      ...dissolving.map((el) => el.animate([{ opacity: 1 }, { opacity: 0 }], { duration: FADE_OUT_MS, easing: 'linear', fill: 'forwards' }).finished),
    ]).then(done, done)
    function done() {
      leaving.current = false
      const was = pageNow.current
      commit()
      // The switch didn't happen (still the same page once React has had time to render): bring the old one back
      // rather than leave it hidden.
      setTimeout(() => {
        if (pageNow.current !== was || !entering.current) return
        entering.current = 0
        for (const el of [...slides(), ...fades()]) el.getAnimations().forEach((a) => a.cancel())
      }, 120)
    }
  }

  const swipeBind = useSwipe(
    (direction) => {
      settling.current = false
      if (!canGo(direction)) return springBack()
      leave(direction, () => onSwitch(direction))
    },
    (dx) => {
      if (reducedMotion() || leaving.current) return
      if (dx === null) {
        settling.current = true
        setTimeout(() => {
          if (settling.current) springBack()
          settling.current = false
        }, 0)
        return
      }
      // Swiping is off altogether (neither way goes): the card doesn't even rubber-band.
      if (!canGo(1) && !canGo(-1)) return
      // Towards a market: the card follows the finger. Past the last one: a short rubber band.
      const pull = canGo(dx < 0 ? 1 : -1) ? 1 : 0.18
      for (const el of slides()) el.style.translate = `${dx * pull}px 0`
    },
    area,
  )

  useLayoutEffect(() => {
    const from = entering.current
    if (!from) return
    entering.current = 0
    const motion = !reducedMotion()
    // The track has already brought the new card into place: it just resets (now with that card in the middle).
    for (const el of slides()) {
      el.getAnimations().forEach((a) => a.cancel())
      el.style.translate = ''
    }
    for (const el of fades()) {
      el.getAnimations().forEach((a) => a.cancel())
      if (motion) el.animate([{ opacity: 0 }, { opacity: 1 }], { duration: FADE_IN_MS, easing: 'linear' })
    }
  }, [page])

  return {
    bind: swipeBind,
    /** Switch by tap (tabs, market button): the same switch as a swipe, towards `direction`. */
    go: (direction: 1 | -1, commit: () => void) => leave(direction, commit),
  }
}
```

### `src/shared/userStatus.ts`

```ts
// Where the user is in the app — the prototype's app-level settings ("User status" in the preview panel, the phone's
// settings sheet and a floating card beside the phone). Every screen that depends on it reads it here, so they all stay
// in sync: pick "User account state: Active · money on the way" once and the Home's US tab, a US stock page and the wallet all
// show that state. Picking never moves on by itself; taps in the prototype don't change it.
// In a real app these come from the user's account (KYC status, US Stocks activation, wallet, holdings).
import type { FlowOption } from '../flows/types'
import { setFlowOption, useFlowOption } from './prototype'
import { linkedBanks, otherBank, type LinkedBank } from './data/user'

/** The settings' owner in the preview (as a flow id: where the picks are remembered). */
export const USER_STATUS = 'app'

export type KycStatus = 'done' | 'pending'
export type UsActivation = 'kyc' | 'off' | 'review' | 'support' | 'failed' | 'active'
export type UsWallet = 'empty' | 'onTheWay' | 'funded'
export type UsHoldings = 'none' | 'some'
export type BankLinks = 'none' | 'one' | 'two' | 'three' | 'sbi'

/**
 * Screens that change with the user status: the settings float beside the phone on these (desktop preview). The Home,
 * its US tab screens (each one sets the status to its own state on arrival, then follows a pick), a US stock page and
 * the wallet's US tab.
 */
/** The add-money screens and the wallet: the bank row and its sheet change with the user's linked banks. */
const BANK_SCREENS = ['deposit-01', 'deposit-06', 'deposit-07', 'deposit-08', 'deposit-09', 'us-stocks-21', 'us-stocks-22', 'us-stocks-23', 'us-stocks-24', 'us-stocks-53', 'us-stocks-54', 'us-stocks-95']

const STATUS_SCREENS = ['stocks-01', 'stocks-09', 'stocks-10', 'stocks-13', 'stocks-14', 'stocks-15', 'stocks-16', 'stocks-17', 'stocks-19', 'stocks-20', 'stocks-21', 'us-stocks-13', 'us-stocks-54']

/** The app-level user status settings. */
export const userStatusOptions: FlowOption[] = [
  {
    // One list for the whole way in, in order — one row of states (18 Nov, the user's call; was three settings: US
    // Stocks activation, then USD wallet and US holdings under "Active"): not active while the Lemonn KYC is pending
    // (US Stocks can't be activated until it's done), not active, the activation steps, then active with $0, money on
    // the way, money in the wallet, US holdings. The values are the UsJourney steps.
    id: 'account',
    group: 'User status',
    label: 'User account state',
    picker: 'dropdown',
    values: [
      { value: 'kyc', label: 'Not active · KYC pending' },
      { value: 'activate', label: 'Not active' },
      { value: 'review', label: 'Under review' },
      { value: 'support', label: 'Under review · contact support' },
      { value: 'failed', label: 'Activation failed' },
      { value: 'activated', label: 'Active · $0' },
      { value: 'onTheWay', label: 'Active · money on the way' },
      { value: 'ready', label: 'Active · has money' },
      { value: 'holding', label: 'Active · US holdings' },
    ],
    // The prototype opens on a user who's all set: activated, money in the wallet, holding US stocks.
    default: 'holding',
    floatOn: STATUS_SCREENS,
  },
  {
    // Money on the way, more than once: a US deposit takes 1–2 working days, so adding money again before the first one
    // lands means two or three on the way (20 Nov). The wallet's bar and Home's card add them up; their sheet shows each one.
    id: 'deposits',
    group: 'User status',
    label: 'Deposits on the way',
    showIf: { account: ['onTheWay'] },
    values: [{ value: 'one', label: 'One' }, { value: 'two', label: 'Two' }, { value: 'three', label: 'Three' }],
    default: 'one',
    floatOn: [...STATUS_SCREENS, 'us-stocks-28', 'us-stocks-93'],
  },
  {
    // How the oldest deposit on the way is doing (20 Nov). Taking longer: past its day, still with the US bank — the
    // sheet says it's taking longer than usual, the money is safe, and a failed one is refunded to the bank it came from.
    // Failed: the US bank sent it back — where it stopped, the refund, Try again and Contact support. Home's card and the
    // wallet's bar say so.
    id: 'depositStatus',
    group: 'User status',
    label: 'Deposit status',
    showIf: { account: ['onTheWay'] },
    values: [{ value: 'onTime', label: 'On time' }, { value: 'delayed', label: 'Taking longer' }, { value: 'failed', label: 'Failed' }],
    default: 'onTime',
    floatOn: [...STATUS_SCREENS, 'us-stocks-28'],
  },
  {
    // Bank accounts linked to Lemonn (KYC adds the first). None = the add-money screens ask for one first.
    id: 'banks',
    group: 'User status',
    label: 'Bank accounts',
    picker: 'dropdown', // a dropdown like User account state (18 Nov: five choices didn't fit a segmented row)
    // Three / SBI only: with an account at a bank US Stocks money can't go from (State Bank of India).
    values: [{ value: 'none', label: 'None' }, { value: 'one', label: 'One' }, { value: 'two', label: 'Two' }, { value: 'three', label: 'Three (+ SBI)' }, { value: 'sbi', label: 'SBI only' }],
    default: 'three',
    floatOn: BANK_SCREENS,
  },
]

const option = (id: string) => userStatusOptions.find((o) => o.id === id)!
const useStatus = (id: string) => useFlowOption(USER_STATUS, id, option(id).default)

export type UserStatus = { kyc: KycStatus; us: UsActivation; usWallet: UsWallet; usHoldings: UsHoldings; banks: BankLinks }

/** The user status as picked (settings under one that's off keep their last pick). KYC comes from the activation list. */
export function useUserStatus(): UserStatus {
  return { ...statusOf(useStatus('account') as UsJourney), banks: useStatus('banks') as BankLinks }
}

/** One account state as the activation, wallet and holdings it means. */
function statusOf(step: UsJourney): Omit<UserStatus, 'banks'> {
  const us: UsActivation = step === 'activate' ? 'off' : ['kyc', 'review', 'support', 'failed'].includes(step) ? (step as UsActivation) : 'active'
  return {
    kyc: us === 'kyc' ? 'pending' : 'done',
    us,
    usWallet: step === 'activated' ? 'empty' : step === 'onTheWay' ? 'onTheWay' : 'funded',
    usHoldings: step === 'holding' ? 'some' : 'none',
  }
}

/**
 * The bank accounts the user has linked, as picked in "User status → Bank accounts" (primary first). Money in the USD
 * wallet (on the way or landed) came from a bank, so then "None" counts as one — as in the real app, a user with money
 * moving always has a bank.
 */
export function useLinkedBanks(): LinkedBank[] {
  const picked = useStatus('banks') as BankLinks
  const { us, usWallet } = statusOf(useStatus('account') as UsJourney)
  const moneyMoved = us === 'active' && usWallet !== 'empty'
  const banks = picked === 'none' && moneyMoved ? 'one' : picked
  const linked = { none: [], one: linkedBanks.slice(0, 1), two: linkedBanks, three: [...linkedBanks, otherBank], sbi: [{ ...otherBank, primary: true }] }[banks]
  return addedBank ? [...linked, addedBank] : linked
}

// A bank account added in the prototype ("Add bank account" → verified). Kept in memory, so a reload starts without it.
let addedBank: LinkedBank | undefined
let addBankOpener: string | undefined
let addBankForUsStocks = false

/**
 * An add-money screen (₹ or US) or the US Stocks activation opens "Add bank account": remember which, so the verified
 * account comes back to it. `usStocks`: the account is for US Stocks, so it must be at a bank that can send money abroad.
 */
export const startAddBank = (fromScreen?: string, { usStocks = false }: { usStocks?: boolean } = {}) => { addBankOpener = fromScreen; addBankForUsStocks = usStocks }
/** "Add bank account" was opened from US Stocks: only the supported banks can be added. */
export const addBankForUs = () => addBankForUsStocks
/** The add-money screen that opened "Add bank account" (undefined when it was opened straight from the screen list). */
export const addBankReturnScreen = () => addBankOpener
/** The ₹1 check passed: the account joins the linked banks, and the add-money screens pick it. */
export const linkBank = (bank: LinkedBank) => { addedBank = bank }
/** The account added in this session, if any. */
export const newlyLinkedBank = () => addedBank

/**
 * Where the user is with US Stocks, as one step: KYC pending → 'kyc'; not activated → 'activate'; under review /
 * contact support / failed; activated → $0 'activated', 'onTheWay', or with money 'ready' / 'holding'.
 * (The Stocks flow's UsState uses the same names.)
 */
export type UsJourney = 'kyc' | 'activate' | 'review' | 'support' | 'failed' | 'activated' | 'onTheWay' | 'ready' | 'holding'

export function usJourney({ kyc, us, usWallet, usHoldings }: UserStatus): UsJourney {
  if (kyc === 'pending' || us === 'kyc') return 'kyc'
  if (us === 'off') return 'activate'
  if (us !== 'active') return us
  if (usWallet === 'empty') return 'activated'
  if (usWallet === 'onTheWay') return 'onTheWay'
  return usHoldings === 'some' ? 'holding' : 'ready'
}

export const useUsJourney = () => usJourney(useUserStatus())

/** Sets the user status to one US Stocks step (a US tab screen showing its own state sets it on arrival). */
export function setUsJourney(step: UsJourney) {
  setFlowOption(USER_STATUS, 'account', option('account').default, step)
}
```
