# TAPEOUT Design Bar

The standard is not "good". It is better than a triple-A design studio.
These rules are checkable. A deploy that breaks one does not ship.

## Hard gates (machine-checked before every deploy)

Run: `node ~/workspace/devtools/clip-audit.js file:///home/hatch/workspace/deploy/tapeout/index.html`
Exit code is non-zero on any failure. No overrides.

1. Zero clipped text at 320, 390, 768, and 1440px, notebook and classic themes.
   Clipped means an element's content is wider than its box with no scrollable
   ancestor to reach it. Intentional horizontal scrollers (filter pills) are
   exempt only if every pill is reachable by scroll.
2. Zero page-level horizontal overflow at all four widths, both themes.
3. Every tappable control is at least 44px in its smallest dimension.
4. `node --check` passes on the page's scripts.
5. Exactly one `PRODUCTS` array. Zero em dash characters (U+2014 and the
   invisible U+2028 that breaks regexes). Zero invented prices: every price
   rendered must equal a `price` field in PRODUCTS.

## Imagery (human-checked before every deploy)

6. The product is fully visible in every frame. Source images are art-directed
   to the exact frame aspect (4:3 cards) before they ship; CSS `object-fit`
   must never be the thing deciding what gets cropped.
7. Uniform studio imagery across the shelf: same background family, same
   lighting character, sharp at the largest render size. No mixed white/black
   cutouts, no fringed edges, no upscaled thumbnails.
8. Every photo depicts the exact make, model, cooler, and fan count. A
   prettier photo of the wrong card is a lie, not an upgrade.

## Copy (human-checked)

9. Prices are real target prices, shown on cards, dossiers, and the request
   drawer. "Confirmed on request" never stands where a price belongs.
10. No promises about the future, no internal data, no possession claims.
    Show the card, name the price, shut up.

## Process

- Screenshot review at 320 / 390 / 768 / 1440, both themes, grid + dossier +
  drawer, before every deploy. The screenshots are the evidence, not a vibe.
- A finding ships its fix in the same deploy. An unfixed finding is reported
  with its reason, never silently deferred.
