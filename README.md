# Reading the Mind in the Eyes Test (RMET) — local copy

A self-contained local copy of the revised (adult) RMET, built in the same
720×450 scaling shell as the other Top Hat embeds.

```
index.html             full test — all 36 items
RMET-noneutral.html    short form — 18 items, 9 positive + 9 negative
RMET-team.html         head-to-head game for 1-3 players, landscape phone
img/0.jpg              practice item
img/1-36.jpg           the 36 test items
```

Open any of them in a browser. No build step, no server required. All three
share the same `img/` folder, so keep them in the same directory.

| | Items | Time | Layout | Valence |
|---|---|---|---|---|
| `index.html` | 36 | ~10 min | 720×450 embed | 9 pos / 14 neg / 13 neutral |
| `RMET-noneutral.html` | 18 | ~5 min | 720×450 embed | 9 pos / 9 neg |
| `RMET-team.html` | 18 | ~5–8 min | landscape phone | 9 pos / 9 neg |

### The head-to-head version

`RMET-team.html` runs the same 18 balanced items as a group game on one phone.

- Pick **1, 2 or 3 players** on the start screen.
- Everyone answers the same photograph in turn on the same screen. Each pick
  shows up in the roster along the bottom the moment it is tapped, so players
  can see each other's answers and argue about them as they go. There is no
  pass-the-phone screen — it is meant to be played together, out loud.
- Results stack the players best-first, with the leader starred, each showing
  their overall percentage plus their positive and negative splits.

### How it adapts to the screen

There is no fixed layout and no orientation requirement — it reshapes itself to
whatever it is opened on.

**Two layouts**, switched on aspect ratio:

- *Portrait* stacks everything: full-width photograph, four full-width answer
  buttons, and the roster as a vertical list so nobody's answer gets truncated.
- *Landscape* goes side by side: photograph left, answers right, roster along
  the bottom, and the results become one compact row per player.
- Below 330px of height in landscape — a phone whose browser is eating most of
  the screen — the answer buttons also go 2×2 to halve their height.

**Type scales with the viewport.** Every size derives from one unit,
`--u: min(2.6vmax, 5.2vh)`, wrapped in `clamp()`. Taking the *smaller* of a
width-based and a height-based measure is what makes this work in both
orientations: `vmax` alone grows text until it overflows a short landscape
screen, `vh` alone makes it tiny in portrait. In practice the answer buttons
run about 16.6px on a small portrait phone, 20.4px in landscape, and cap at
22px so they do not balloon on a laptop.

**Height comes from `visualViewport.height`** via a `--app-h` custom property,
not from `100vh`. iOS Safari's `100vh` counts the space behind its own toolbars,
which pushed the card off the top and bottom of the screen. `100dvh` is the CSS
fix but is unreliable on older iOS, so JS sets the value and `100dvh` is only
the fallback.

Verified with no clipping on all four screens at 360×640, 393×720, 768×1024,
852×225, 852×393 and 1440×900.

**True fullscreen:** iPhone Safari has no Fullscreen API, so no page can hide
the browser chrome on its own. The one way to get an edge-to-edge screen is
*Share → Add to Home Screen* and launching from that icon — the standalone meta
tags are already in the file, so it opens with no browser UI at all. Worth doing
for a phone you reuse in class; too much friction to ask of students scanning a
QR code, which is why the layout above carries the in-browser case.

Scoring is identical to the short form; there are no population bands, since
ranking players against each other is the point.

### What the short form cuts, and why

It is a strict subset — item wording, option order, answer key and image files
are all untouched. Two cuts were made:

1. **All 13 neutral-valence items**, so the test measures only positive and
   negative emotion recognition.
2. **Five of the 14 negative items**, to balance the two categories at 9 and 9.
   The five dropped are the ones the valence review flagged as least secure:
   the four **doubt-cluster** items — 12 *sceptical*, 17 *doubtful*,
   34 *distrustful*, 36 *suspicious* — which name states of disbelief rather
   than felt emotions, plus 23 *defiant*, whose gloss ("insolent, bold") is
   mixed in valence. What remains are the nine unambiguous negative emotions.

**Kept — positive (9):** 1, 3, 6, 20, 21, 25, 28, 30, 31
**Kept — negative (9):** 2, 5, 7, 8, 11, 14, 26, 33, 35

Balancing valence costs face balance: the short form runs 10 male / 8 female
rather than the full test's 18/18. The men and women breakouts still work, but
they rest on smaller and unequal bases, so read them loosely.

## Where the content came from

**Images** (`img/0.jpg`–`img/36.jpg`) were downloaded from the online version at
`https://psytests.org/arc/rmeten.html`. All 37 are 800×310 grayscale JPEGs.

**Items, option wording, and option order** were scraped from the same site, then
checked line by line against **Appendix A** of the original paper. They match
exactly, including the order the four words appear in.

**The answer key** was taken from the paper itself, not from the website — the
site scores server-side and never exposes the key. Appendix A prints the target
word for each item *in italics*, so the key was recovered by reading the PDF's
font runs and pulling the word set in `TimesCUP-Italic`. Each of the 36 items has
exactly one italicised word, and every one of them appears among that item's four
options.

Three independent sources agree on all 36 answers: the paper's italics, the
option lists scraped from psytests, and the published key. Two items are also
confirmed in the paper's own figure captions (item 32 = *serious*, item 29 =
*reflective*).

## Scoring

One point per item matching the key. **Results are reported as percentages**,
not raw counts, so the full test and the short form read on the same scale.
Unanswered items count as wrong.

### Population bands

The results screen places the total on a Low / Average / High track. The bands
come from the general-population norm in the original paper, **26.2 ± 3.6 out
of 36** — that is **72.8% correct, SD 10.0** — with one SD either side:

| Band | Percentage | On the 36-item test | Basis |
|---|---|---|---|
| Low | under 62.8% | 0–22 | more than 1 SD below the mean |
| Average | 62.8–82.8% | 23–29 | within 1 SD of the mean |
| High | above 82.8% | 30–36 | more than 1 SD above the mean |

Holding the bands as percentages rather than raw scores is what lets the same
cut-points apply to both files. For reference, **13 of 36** is above chance
(4 options, so chance is 25%).

The cut-points live in the `NORM` object in the script.

> **On the short form:** the norm was established on all 36 items. Applying it
> to an 18-item subset assumes the dropped items were of average difficulty,
> which is not established — difficulty varies with valence, and the short form
> deliberately removed only neutral and marginal items. The bands there are a
> rough reference, not a validated classification, and the results screen says
> so. For anything beyond a classroom demo, use the full test.

### Breakout subscales

Four extra percentages are shown: **positive emotions**, **negative emotions**,
**eyes of men**, **eyes of women**. On the full test, neutral-valence items
count toward the total but appear in no breakout, so the two valence bars do
not sum to the total. On the short form there are no neutral items, so they do.

**None of this is part of the original test** — Baron-Cohen et al. score one
total and nothing else. These are interpretive layers, so treat them as
discussion prompts, not scores. Published valence schemes disagree with each
other, and Hudson et al. (2020) argue the categories are largely arbitrary and
sample-dependent.

**Face in the photograph** (`face: "m" | "f"`) was determined by inspecting all
36 images. Two things corroborate it: the split comes out at exactly **18 male /
18 female**, which is what the paper states the revised version was built to
have, and it agrees with the "Model Sex" column of a published Spanish
adaptation on all 16 items that column covers (items 1–15 and 18). Item 12 is
the one I read as ambiguous; the Spanish table codes it male, and that is what
is used here.

**Valence** (`valence: "positive" | "negative" | "neutral"`) was assigned from
the definitions in the paper's own Appendix B glossary rather than by gut, which
gives **9 positive / 14 negative / 13 neutral**. These calls were reviewed
against the glossary and confirmed; the borderline ones were considered and
deliberately left where they are.

| # | Target | Appendix B definition | Valence |
|---|---|---|---|
| 1 | playful | full of high spirits and fun | positive |
| 2 | upset | agitated, worried, uneasy | negative |
| 3 | desire | passion, lust, longing for | positive |
| 4 | insisting | demanding, persisting, maintaining | neutral |
| 5 | worried | anxious, fretful, troubled | negative |
| 6 | fantasizing | daydreaming | positive |
| 7 | uneasy | unsettled, apprehensive, troubled | negative |
| 8 | despondent | gloomy, despairing, without hope | negative |
| 9 | preoccupied | absorbed, engrossed in one's own thoughts | neutral |
| 10 | cautious | careful, wary | neutral |
| 11 | regretful | sorry | negative |
| 12 | sceptical | doubtful, suspicious, mistrusting | negative |
| 13 | anticipating | expecting | neutral |
| 14 | accusing | blaming | negative |
| 15 | contemplative | reflective, thoughtful, considering | neutral |
| 16 | thoughtful | thinking about something | neutral |
| 17 | doubtful | dubious, suspicious, not really believing | negative |
| 18 | decisive | already made your mind up | neutral |
| 19 | tentative | hesitant, uncertain, cautious | neutral |
| 20 | friendly | sociable, amiable | positive |
| 21 | fantasizing | daydreaming | positive |
| 22 | preoccupied | absorbed, engrossed in one's own thoughts | neutral |
| 23 | defiant | insolent, bold, don't care what anyone else thinks | negative |
| 24 | pensive | thinking about something slightly worrying | neutral |
| 25 | interested | inquiring, curious | positive |
| 26 | hostile | unfriendly | negative |
| 27 | cautious | careful, wary | neutral |
| 28 | interested | inquiring, curious | positive |
| 29 | reflective | contemplative, thoughtful | neutral |
| 30 | flirtatious | brazen, saucy, teasing, playful | positive |
| 31 | confident | self-assured, believing in oneself | positive |
| 32 | serious | solemn, grave | neutral |
| 33 | concerned | worried, troubled | negative |
| 34 | distrustful | suspicious, doubtful, wary | negative |
| 35 | nervous | apprehensive, tense, worried | negative |
| 36 | suspicious | disbelieving, suspecting, doubting | negative |

The calls worth knowing about, if you ever want to revisit them:

- **The doubt cluster** (12, 17, 34, 36) is defined almost entirely through
  itself — these are states of disbelief rather than felt emotions. Kept
  negative on the strength of "mistrusting" and "wary". Moving all four to
  neutral would leave 10 negative / 17 neutral, and is the single change that
  moves the negative bar most.
- **fantasizing** (6, 21) is glossed only as "daydreaming", which carries no
  valence marker. Kept positive; moving it would cut the positive base to 7.
- **pensive** (24), **serious** (32) and **tentative** (19) each lean negative
  in their own definitions ("slightly worrying", "grave", "uncertain") but are
  kept neutral.

### A caveat worth raising in class

The RMET is **structurally skewed**: at most 9 of 36 targets are positive under
any reasonable reading, against 14 negative and 13 neutral. The positive bar
therefore always rests on a small base, where a single miss moves it about 11
points. That imbalance is a documented criticism of the test, and the breakout
makes it visible rather than hiding it.

## Citation and terms

> Baron-Cohen, S., Wheelwright, S., Hill, J., Raste, Y., & Plumb, I. (2001).
> The "Reading the Mind in the Eyes" Test revised version: A study with normal
> adults, and adults with Asperger syndrome or high-functioning autism.
> *Journal of Child Psychology and Psychiatry, 42*(2), 241–251.

The test is distributed by the Autism Research Centre at Cambridge **free for
academic, non-commercial use** — it is *not* public domain, and the photographs
are not freely licensed. Keep use educational and keep the citation on the start
screen.

## Tweaking it

Everything lives in the `ITEMS` array near the top of the `<script>` block:

```js
{ n: 1, img: "img/1.jpg", options: ["playful","comforting","irritated","bored"],
  answer: "playful", answerIndex: 0, valence: "positive", face: "m" },
```

The item count, progress bar, scoring, and the `/ 36` on the results screen are
all derived from `ITEMS.length`, so deleting items just works — a 12-item short
form scores out of 12 with no other edits. If you reorder an item's `options`,
update `answerIndex` to match; the inline console checks at the bottom of the
file will flag it if the two disagree.

## Not included

The original administration gives participants a **glossary** of the mental-state
terms (Appendix B of the paper). That is omitted here. If you want it, it is worth
adding before using the test for anything beyond a classroom demo, since
unfamiliar vocabulary otherwise becomes part of what the test measures.
