# My Friend Riley — Verse website page

A self-contained product page for **My Friend Riley**. No framework, no build
step, no dependencies beyond Google Fonts.

## Files

| File | Use |
|---|---|
| `index.html` | Standalone page. Open it directly or deploy it as-is. |
| `mfr-snippet.html` | The same page as an embeddable fragment (fonts link, `<style>`, markup, `<script>`). Drop it into any page body. |
| `assets/` | Optimized media: 15 trailer stills, Riley mascot frames, 9 emotion pets (each with a tap-reaction pose), the web trailer, and its poster. |

## Integrating into the Verse site

- **Scoped styles:** every rule lives under `.mfr`, so nothing leaks into the
  host site. The only globals are the `--mfr-*` color tokens on `:root` and one
  `body { background }` line. Remove that line if the host controls the page
  background.
- **Asset paths:** media is referenced as `assets/...`. Serve `assets/` next to
  the page, or find-and-replace `assets/` with your CDN path.
- **Theme:** light by default, with a dark palette following
  `prefers-color-scheme`. A host can force a theme with
  `<html data-theme="light|dark">`.
- **Anchors:** `#mfr-feelings` and `#mfr-trailer` are linkable section ids.
- **Fonts:** Baloo 2 (display), Lexend (body), and JetBrains Mono (labels),
  loaded from Google Fonts, with system fallbacks declared.

## Interactions

- **Riley (hero):** idle breathing frames, leans toward the pointer, and taps
  cycle friendly lines with a sparkle burst.
- **Hold to hum:** press and hold the button (mouse, touch, or Space/Enter) to
  fill the dial like the in-game HumDial. Riley stands in front of the game's
  real Starflower gate (rendered from the game's 3D model into frame + door
  layers). A full dial slides the doors open onto a warm glow, counts the gate,
  and celebrates. After 4 seconds the doors close on their own and Riley
  invites the visitor to open another gate (`GATE_OPEN_MS` in the script). Letting go early drains the dial.
- **Feelings picker:** the game's nine emotion pets. Tapping one shows that
  pet's reaction pose and its in-game line.

## Performance

- Animations use `transform` and `opacity` only. Pointer tracking is batched to
  one `requestAnimationFrame` per frame, and burst sparkles remove themselves
  when their animation ends.
- `prefers-reduced-motion` turns off floating, tilting, idle cycling, and
  bursts.
- Images below the hero use `loading="lazy"`. The trailer uses
  `preload="none"` with a poster, so its 9.8 MB downloads only on play.
- Total weight: about 2 MB of WebP images plus the optional trailer.

## Content notes

All copy is drawn from the current build: features, pet names and lines, the
gate pitch progression, and the zero-punishment design principle. The
"For kids 7–14" range comes from the HumDial whitepaper. Review the
"in development" labels before launch, and add store links once they exist.
