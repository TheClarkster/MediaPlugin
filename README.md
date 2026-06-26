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
| LCD screen | Album art (falls back to a play/pause glyph when no art is available) |

All original actions (Play, Pause, Play/Pause, Next, Previous, Info, Thumbnail Background) are
still included. This fork uses a separate plugin id (`dev_clark_MediaDial`) so it can be installed
alongside the official Media plugin without conflicting.

## Credit & license

Fork of [StreamController/MediaPlugin](https://github.com/StreamController/MediaPlugin) by Core447.
Licensed under **GPL-3.0**, same as the original — see [LICENSE](LICENSE).
