# es-theme-minuark-4x3-media

MinUI look for **4:3 / 640×480** handhelds (R36S, RG353PS…) **with game media** — the
plain-list `es-theme-minuark-4x3` deliberately shows no videos or boxart; this fork adds
them, while keeping the layout selectable back to the purist look.

## Lineage

- `MinUI` — original design by [Shaun Inman](https://github.com/shauninman/MinUI)
- `es-theme-MinUArk` — ArkOS/MinUI port by [Vidnez](https://github.com/Vidnez/es-theme-MinUArk)
- `es-theme-minuark-4x3` — 4:3 rewrite by [offalynne](https://github.com/offalynne/es-theme-minuark-4x3)
- this fork: media elements grafted on; video/art geometry follows the pattern proven
  on-device by the RetroDark theme (`textlist zIndex 3`, `<video>` with `maxSize` +
  `showSnapshotNoVideo`).

License: CC-BY-NC-SA (inherited). All art/fonts come from the upstream 4:3 theme.

## Install

```bash
git clone https://github.com/v3rse/es-theme-minuark-4x3.git /roms/themes/es-theme-minuark-4x3-media
```

The **folder name is the theme name** ES shows under *UI Settings → Theme*, hence the
`-media` suffix — it must differ from upstream's folder or the two themes collide.
`theme.xml` has to sit at the top level of that folder.

## Repo

Fork of [`offalynne/es-theme-minuark-4x3`](https://github.com/offalynne/es-theme-minuark-4x3).
This work lives on the **`media` branch**, which is the fork's default; `master` is upstream
untouched, so the delta is always inspectable:

```bash
git fetch upstream && git diff upstream/master..media
```

## Media modes

Chosen in **Start → UI Settings → Theme Configuration → Media**:

| Mode | List | Media |
|---|---|---|
| **Video panel** (default) | left 53 %, rows retuned for the narrower column | scraped video on the right, falling back to the game's image when no video exists (`showSnapshotNoVideo` + `snapshotSource=image`) |
| **Art panel** | left 53 % | static boxart/screenshot on the right, no video playback |
| **Art backdrop** | full width, upstream geometry | the game's art dimmed (`555555`) full-screen behind the list |
| **Off (plain MinUI)** | full width, upstream geometry | no media at all — identical to `es-theme-minuark-4x3` |

## Layout notes

- `zIndex`: theme background `0` → `md_image` `1` → `md_video` `2` → `textlist` `3`
  (the list must win, or the media covers the rows).
- Media panel box is `0.4 × 0.5` centred at `0.78 0.47`; a 4:3 screenshot fills it as
  256×192 px and is never stretched.
- All geometry lives in the `<variables>` block of `theme.xml` (defaults = Video panel)
  and each mode file in `options/media/` overrides the same variable set, so a mode file
  is the only thing to edit when retuning a position.
