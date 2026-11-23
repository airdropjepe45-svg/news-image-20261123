# THE WORLD — 23 November 2026

[![make.fun · news-image-20261123](https://make.fun/badge/news-image-20261123.svg)](https://make.fun/bounty/news-image-20261123)
[![rank](https://make.fun/badge/news-image-20261123/airdropjepe45-svg/news-image-20261123/rank.svg)](https://make.fun/bounty/news-image-20261123)
[![reward](https://make.fun/badge/news-image-20261123/airdropjepe45-svg/news-image-20261123/reward.svg)](https://make.fun/bounty/news-image-20261123)

A newspaper-style front page summing up world news of Monday 23 November 2026.
Every story carries its source in the image itself (France 24, Reuters,
Al Jazeera, AP, the Independent, Xinhua, CNN and more), and nothing in the
paper was invented: all 50 stories happened or were first reported on
23 November 2026.

## Stories at a glance — the 3 top stories

1. Ukraine sinks Russian warship off Libya
2. Russian strikes kill 14 across Ukraine
3. COP31 fallout: Pacific despair, Bowen under fire

Then 10 mid stories with small illustrations — the Taiwan market's 2.2%
rebound, Belgium's airports shut by strike, the sixth tanker hit in Hormuz,
Ukraine hitting three Russian oil plants, 153 Russian drones over Ukraine,
Nepal's PM meeting Modi in Delhi, Gaza called a "toxic wasteland", New
Zealand holding India to a draw, Trump moving to block Congress probes and
the Kremlin saying new Ukraine talks are coming soon — and 37 numbered
stories in the list at the foot of the page, ten of them pinned on the
world map.

## The image

`entry.png` (1024 × 1024) is an illustrated newspaper front page in colour:

- Masthead **THE WORLD** with **Monday 23 November 2026** prominent.
- **A stats row** of six big numbers: 7 naval drones sank the Merkury,
  14 killed in Russian strikes, 153 Russian drones fired overnight,
  +2.2% TAIEX rebound, 99% of Gaza showing contamination, 59,500
  passengers hit by the Belgium shutdown.
- **THE DAY IN UTC**, seven sourced times from 02:22 to 08:22.
- **3 illustrated top stories** with flat vector-style scenes drawn in code:
  a night sea off Benghazi with the burning corvette Merkury, a night sky
  over Dymer with drones and air-defence bursts, and a globe with a
  crossed-out oil drop for the COP31 fallout.
- **10 mid stories**, each with a small icon, a headline and a one-line deck.
- **A dot-matrix world map** with ten numbered pins, and a numbered list
  carrying the remaining **37 stories**, one line each.
- A **DATE CHECK** box stating that every story on the page happened or was
  first reported on Monday 23 November 2026, and naming the big stories
  that were left out on purpose because they belong to other days: the
  COP31 collapse itself and the Democrats' 258 seats (Sunday), Liverpool
  4-0 Man Utd and the Delta outage (Sunday), the Brazil storm (Friday)
  and the Sparta II fire (Saturday).
- A footer line crediting the sources.

That is **50 stories in total, all first reported on 23 November 2026** — from
the sinking of the Merkury off Libya and the 14 killed in Russian strikes,
through the Taiwan rebound and the Belgium airport shutdown, to the
Wellington Test draw and COP31 drawing a record 92,000 people.

## How it is made

The image is drawn entirely in code by `main.ts` (Node 22, standard library
only, no network). It embeds real vector font outlines (DejaVu Serif Bold
for the masthead and headlines, DejaVu Sans for body text), filled with an
even-odd scanline rasterizer at 3x supersampling so the letterforms read as
normal newspaper type, draws the masthead, the stats row, the UTC timeline,
the three illustrated scenes, the mid-story icons, the dot-matrix world map
(with land as a union of ellipses) and the DATE CHECK box, and encodes the
PNG itself with `node:zlib` (deflate) and a hand-rolled CRC32 — so the
output is deterministic: no timestamps, no randomness.

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts
```

Running it twice produces a byte-identical `out/entry.png`.

## Verify

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts
sha256sum out/entry.png
```

Expected: a 1024 × 1024 PNG of 125,247 bytes, SHA-256
`78ecf08119bad116f9aafcf7014a705342d8b8232a1f3681972b58fbc1ab0b47`.
Two runs in different directories produce byte-identical files.

The build also runs a fit check first and prints `fitOk=true` only when every
top headline fits in two lines, every top deck in two, every mid headline
and deck in one line, every timeline item in two lines, and every numbered
story in one line — and the page ends inside the frame.

## License

MIT — see [LICENSE](LICENSE).
