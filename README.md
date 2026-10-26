# ABTH CDN

Chart pictures and note counts for [A Better Taiko Hiroba](https://github.com/HicirTech/A-Better-Taiko-Hiroba), drawn ahead of time from the charts of [ESE](https://ese.tjadataba.se/ESE/ESE) and published on GitHub Pages at <https://hicirtech.github.io/abth-cdn/>. The app reads them as its default chart source, so a song's charts show even while ESE is slow to answer.

## What it holds

- `charts/<song>/<difficulty>.webp`: each chart as the app draws it with TJA Renderer, every branch stacked, kept as a near-lossless WebP. `<song>` is the song's number on Donder Hiroba, and `<difficulty>` one of `easy`, `normal`, `hard`, `oni` and `ura`.
- `densities/<song>.json`: each chart's notes per second, in the shape the app keeps them.
- `manifest.json`: ESE's commit the charts were drawn from, when, how many, and any drawing left out.

No chart file is kept here, and none is published: the build reads ESE's charts, draws and counts them, and deletes its copy.

## How it is built

[`.github/workflows/build.yml`](.github/workflows/build.yml) runs every three hours. It asks ESE whether its `master` branch moved, and only then clones it without the audio ESE keeps in Git LFS, reads OurTaiko's map of songs to charts (`cdn.ourtaiko.org`), and runs the app's own [`gui/scripts/abth-cdn/build.ts`](https://github.com/HicirTech/A-Better-Taiko-Hiroba/blob/main/gui/scripts/abth-cdn/build.ts). It then deletes the clone, publishes the site, and commits `manifest.json`. Run it by hand from the Actions tab: `force` draws everything again, and `app_ref` names another branch of the app to draw with.

## Credits

The charts are ESE's, by the TJADB community; each picture names it. The drawings are made with [TJA Renderer](https://github.com/jack9966qk/TJARenderer) (MIT), as enhanced by HicirTech. OurTaiko's map ties Donder Hiroba's songs to ESE's files.
