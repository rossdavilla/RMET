# Reading the Mind in the Eyes (`RMET`)

A local copy of the revised adult RMET (Baron-Cohen et al., 2001) for **PSY170**: judge what a
person is thinking or feeling from the eye region alone. Live at
<https://rossdavilla.github.io/RMET/>.

**`README.md` is the real documentation** — the four versions, their item counts, timings and
valence balance, how the head-to-head game plays, and how the layout adapts to the screen. Read
it first.

## The four versions

| File | Items | Layout |
|---|---|---|
| `index.html` | 36 — the full test | 720 × 450 embed |
| `RMET-noneutral.html` | 18 — 9 positive, 9 negative | 720 × 450 embed |
| `RMET-team.html` | 18 — head-to-head for 1–3 players on one phone | any screen |
| `RMET-team10.html` | 10 — the short version of that game | any screen |

They are four separate files, not generated from one another, and **they all share the same
`img/` folder** (`img/0.jpg` is the practice item, `img/1.jpg`–`img/36.jpg` the test items). Keep
them in the same directory, and remember that a change to the test flow has to be made in each
file it applies to.

No build step, no server needed, nothing fetched from outside the repo.

## Things to keep

- **The valence balance is deliberate.** The short forms are built to be 9 positive / 9 negative
  (and 5/5 at ten items). Dropping or swapping an item breaks that; check the README's table
  before changing the item set.
- **The team game is played out loud, together.** There is no pass-the-phone screen: every player
  answers the same photograph in turn on one screen, the banner names whose turn it is in that
  player's colour, and each pick appears in the roster the moment it is tapped so the group can
  argue about it. Solo play hides the banner and the roster. That is the design, not an oversight.
- The embeds must fit 720 × 450 without scrolling.
- Nothing is collected: no backend, no analytics, no storage.
- The instrument is published and cited — keep the attribution to Baron-Cohen et al. (2001).

## Publishing

GitHub Pages serves `main` from the repository root, so a push to `main` is the deploy. Already
listed in `data/sites.json` in the
[`rossdavilla.github.io`](https://github.com/rossdavilla/rossdavilla.github.io) repo under the
`PSY170` tag.
