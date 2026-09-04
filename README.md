# The Deciding Coin

A coin-flip decision maker for when you're stuck between two things. You write both
sides, you start the toss, and you stop it yourself.

Single HTML file. No build step, no dependencies, no tracking. Open `index.html`.

## What it does

- **You name both sides.** Type your question ("Should I buy the bike?") and what
  heads and tails each mean. Whatever you type on the heads plaque is struck onto
  the coin itself — the engraving updates as you type.
- **Start and stop are both yours.** Tap to spin, tap again to stop. Hold-and-release
  works, and so does the spacebar. The result is drawn from `crypto.getRandomValues`
  the moment you stop it — an honest 50/50.
- **Best of three.** Switch modes in the header: first side to win two tosses takes
  it, with a round tracker that dims the third round when it isn't needed.
- **The point of it.** After it lands: *relieved, or quietly annoyed?* That reaction
  is the real answer — which is the actual reason people flip coins over decisions.

## How the coin is drawn

The coin is painted per-frame on a `<canvas>`, not an image or a CSS card:

- Rotation about the horizontal axis, with the face ellipse squashed to `R·|cos θ|`
  and both faces offset by `±(T/2)·sin θ`, so the milled edge appears and disappears
  the way a real coin's does.
- The edge is a path between the two face ellipses, filled with a metal gradient and
  striped with reeding that compresses toward the rim.
- Faces carry a beaded ring, two rim rings, engraved inscriptions (drawn three times
  — dark, light, then fill — for an intaglio cut), and a travelling specular sheen.
- Three motion-blur samples while the coin is fast; a damped wobble as it settles;
  a contact shadow that tightens as the coin drops.

Audio is synthesized with the Web Audio API — a filtered sawtooth whir while spinning,
a struck-metal chime on landing (four notes instead of three when a series is won).

## Details

- Light and dark themes, both defined at token level.
- Respects `prefers-reduced-motion` (shorter spin, no blur, no ambient sheen).
- Your question, both labels, sound setting, mode, and the last 40 tosses persist in
  `localStorage`.
- Haptic feedback on landing where the device supports it.

## Deploy

It's one file, so anything that serves static HTML works. For GitHub Pages: enable
Pages on the `main` branch at the repository root.
