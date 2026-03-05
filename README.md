# Stance Ref

Personal fighting game stance cheatsheet — frame data, hit levels & properties at a glance. Built for in-session reference.

## Features

- **Multi-character** — switch between characters from the header dropdown
- **Frame data** — startup (i#), on block, on hit, on counter hit for every move
- **Color-coded at a glance** — green = your advantage, red = opponent's advantage; hit levels (H/M/L/SL) each have a distinct color
- **Entry routes** — each stance shows how to get into it, with frame data
- **Sortable columns** — click Startup, Block, or Hit to sort; default is fastest move first
- **Filters** — filter by hit level (H/M/L/SL) or property tag (Launcher, Tornado, WallSplat, Homing…)
- **NSS/Heat variants** — tagged inline so they're distinct without cluttering the table

## Characters

| Character | Game | Stances |
|-----------|------|---------|
| Yoshimitsu | Tekken 8 | FLE, DGF, KIN, MED, IND, FC, BDS |
| Jin | Tekken 8 | ZEN, FC, BKS, DVS |

## Adding a New Character

Open `index.html` and find the `CHARACTERS` array at the top of the `<script>` block. Append a new object following this structure:

```js
{
  id: "character_id",       // unique slug, no spaces
  name: "Character Name",
  game: "Game Title",
  stances: [
    {
      id: "ST1",            // stance abbreviation shown in tabs
      name: "Stance Name",
      input: "f+3+4",       // input to enter the stance (or null)
      entries: [
        // moves that transition INTO this stance
        { input: "df+2", i: 16, oB: -9, oH: 6 },
      ],
      moves: [
        // moves available FROM this stance
        { input: "ST1.1", i: 15, oB: -5, oH: 8, oCH: null, lvl: ["M"], props: ["Launcher"] },
      ]
    },
  ]
}
```

### Move fields

| Field | Type | Description |
|-------|------|-------------|
| `input` | string | Input notation |
| `i` | number \| null | Startup frames |
| `oB` | number \| null | Advantage on block |
| `oH` | number \| null | Advantage on hit |
| `oCH` | number \| null | Advantage on counter hit |
| `lvl` | string[] | Hit levels: `"H"`, `"M"`, `"L"`, `"SL"`, `"M!"` (unblockable) |
| `props` | string[] | Properties (see below) |
| `to` | string | Stance this move transitions to (optional) |
| `nss` | `"NSS"` \| `"H"` | Variant tag shown as a badge (optional) |

### Supported properties

`Launcher` · `Tornado` · `WallSplat` · `FloorBreak` · `ForceCrouch` · `Homing` · `HeatEngager` · `PowerCrush` · `Unblockable` · `Grab`

## Notation

| Symbol | Meaning |
|--------|---------|
| `i#` | Startup frames (speed) |
| `oB` | On block — negative means opponent's turn |
| `oH` | On hit |
| `oCH` | On counter hit |
| `H / M / L / SL` | High / Mid / Low / Special Low |
| `!` | Unblockable (e.g. `M!`) |
| `★` | Just-frame or alternate input variant |

## Deployment

Hosted via [GitHub Pages](https://pages.github.com/). Any commit to `main` updates the live site within ~30 seconds.
