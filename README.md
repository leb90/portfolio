# Leandro Bisceglie · portfolio

**Live: [leb90.github.io/portfolio](https://leb90.github.io/portfolio/)** · English by default, Spanish at [`?lang=es`](https://leb90.github.io/portfolio/?lang=es) or with the EN/ES switch.

My name as a night skyline: every letter is a building, and rain hits it. Drops collide with the letters, splash with some restitution, run off the ledges and ripple on the wet street. Grab the red umbrella and carry it around: rain bounces off the canopy, rolls to the rim and drips, and the counter tells you how many drops it stopped.

It's written in [ArtScript](https://artscript.dev), the web language I created. No framework, no physics library and no canvas helper: the simulation, the UI, both languages and the tests are `.art` files.

## How the rain works

- **Collision map.** The letters (plus the antennas, water tanks and the nav pills) are drawn once into a 2px raster. A drop walks the segment it moved this frame, so a fast drop can't skip a thin stroke.
- **Splash.** On a hit, the surface normal comes from the solid cells around the contact point. The drop breaks into 2–4 droplets: the velocity relative to the surface is reflected with restitution, spread along the tangent and pulled down by gravity. A droplet can bounce once more before the roof absorbs it.
- **Umbrella.** The canopy is a rotated ellipse. Drops are tested at three points of their path against it; droplets that land on it slide to the rim and drip, and shaking it flings the water off. The tilt is a damped spring driven by how fast you move it.
- **City.** Windows, a wet rim light, lit lobbies and the reflection in the street are prerendered to an offscreen layer; a window switches on or off now and then, and a soft lightning flashes every 16–34 seconds.
- With `prefers-reduced-motion`, the page shows a still frame.

## Files

| File | What's in it |
|---|---|
| [`src/scene.art`](src/scene.art) | The canvas: city, rain, splashes, umbrella, input |
| [`src/app.art`](src/app.art) | The page, links, tagline, the About and Work panel, tests |
| [`src/i18n.art`](src/i18n.art) | Every string in English and Spanish, and the links |
| [`src/styles.css`](src/styles.css) | Styles and the self-hosted fonts |
| [`public/llms.txt`](public/llms.txt) | A plain-text profile for people and AI agents |

## Run it

Node 24 or newer.

```sh
npm install
npm run dev      # http://localhost:3000, reloads on save
npm test         # the test "..." blocks, in a simulated browser
npm run build    # dist/, one prerendered page
```

Every push to `main` is checked, tested and published to GitHub Pages by [`.github/workflows/pages.yml`](.github/workflows/pages.yml).

Fonts: [Big Shoulders Display](https://fonts.google.com/specimen/Big+Shoulders+Display), [Inter](https://rsms.me/inter/) and [JetBrains Mono](https://www.jetbrains.com/lp/mono/), self-hosted under the SIL Open Font License.
