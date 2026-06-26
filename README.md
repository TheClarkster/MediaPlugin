# Media (Dial)

> **Warning:** This fork is heavily vibe-coded (AI-generated). Upstream is not, if you want to use the [original Media plugin](https://github.com/StreamController/MediaPlugin) instead.

A fork of the [StreamController **Media** plugin](https://github.com/StreamController/MediaPlugin)
by [Core447](https://github.com/Core447) that adds **dial support** while keeping every original
button action intact.

## What's added

A combined **Media (Dial)** action, designed for a dial (such as the Stream Deck Plus encoders):

| Input | Action |
|-------|--------|
| Turn clockwise | Next track |
| Turn counter-clockwise | Previous track |
| Press (short) | Play / Pause |
| LCD screen | Album art (blurred-fill background), with the song title and artist over it |

### LCD display

The dial's LCD shows the **album art**, with the **song title** (top) and **artist** (bottom)
over it (falling back to a dimmed play/pause glyph when there's no art or nothing is playing).
Names too wide for the cell scroll horizontally.

Because the LCD cell is wide (~2:1) but covers are square, the sharp cover is centered and the
empty sides are filled with a **zoomed, blurred, dimmed copy of the cover** — so the strip picks
up the album's colours instead of showing black bars. Blur strength and the background dimming are
constants in `MediaDial._compose_art_cell`.

The scrolling uses StreamController's own rolling-label feature, but the engine doesn't refresh a
scroll-only dial often enough on its own (its animation tick only wakes for key/background video,
not dial labels), so the action drives the redraws with a small timer. The repaint interval
(`MediaDial.REPAINT_INTERVAL_MS`) doubles as the scroll-speed knob — shorter is faster and
smoother, longer is slower. A faint once-a-second hitch can appear when another dial repaints the
shared touch strip; removing it entirely would mean poking fragile engine internals, so it's left
as-is.

### Dial sensitivity

A quick flick of the dial emits a *burst* of turn events — StreamController fires one event per
detent and does no debouncing of its own (it doesn't even forward the rotation's tick count), so
turning a lot would otherwise skip a fistful of tracks at once. The action throttles them: it acts
on the first turn immediately, then ignores further turns until a short cooldown elapses
(`MediaDial.TURN_COOLDOWN_US`, 350 ms). A fast spin advances about one track per window, while
slow, deliberate turns still register one-for-one, and reversing direction responds instantly.

All original actions (Play, Pause, Play/Pause, Next, Previous, Info, Thumbnail Background) are
still included. This fork uses a separate plugin id (`dev_clark_MediaDial`) so it can be installed
alongside the official Media plugin without conflicting.

## Credit & license

Fork of [StreamController/MediaPlugin](https://github.com/StreamController/MediaPlugin) by Core447.
Licensed under **GPL-3.0**, same as the original — see [LICENSE](LICENSE).
