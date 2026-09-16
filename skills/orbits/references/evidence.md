# Show the change

A pull request that changes what a user sees should carry a picture. A reviewer who can see
the change reviews it better than one reading a description of it.

## What to capture

| Source | Good for |
|---|---|
| Device screenshot | The real thing — real data, real fonts, real density |
| Screen recording | Flows, animation, timing, gestures |
| Component previews | Many states at once, cheaply, with no device |
| Design frame beside the build | Proving the implementation matches the spec |
| A chart of the metric | Fixes where "before" is a number, not a picture |

## Three rules

1. **Capture during Test**, while the build is on a device and the state is already set up.
   Reconstructing it later costs far more.
2. **Before and after, side by side**, beats after-only. For a fix, the "before" is the whole
   argument.
3. **Most platform CLIs cannot upload images to a pull request** — hosting normally happens
   through the web interface. So capture the files, name them clearly, and hand over a
   ready-made markdown block to drop in. Do not pretend an automated upload happened, and do
   not commit screenshots into the source tree to work around it.

## The handover block

When the CLI cannot upload, produce this and say plainly that the person has to paste it:

```markdown
| Before | After |
|---|---|
| ![before](PASTE_URL_1) | ![after](PASTE_URL_2) |
```

with the local file paths listed underneath, named so the order is obvious:

```
01-before-checkout-crash.png
02-after-checkout-crash.png
```

## UI comparison

Compare against the design frame and its **tokens** — the numbers, not the vibe. Spacing,
type scale, colour token names, corner radii, state colours. "Looks right" is not a
comparison.

Add previews for the states this change affects. Thin preview coverage is normal; adding them
for the affected states is usually a real improvement rather than noise.
