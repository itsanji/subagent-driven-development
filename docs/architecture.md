# Architecture

All pages are plain HTML, CSS and JavaScript in one file, with no dependencies except Google Fonts. Colours and fonts are CSS variables in the `:root` block at the top of each file.

## `index.html`: overview with a timeline

Everything is worked out in advance, so any moment can be drawn directly from the time. That's what makes dragging the timeline exact in both directions.

- **Content:** edit `TASKS`, `WAVES` and `SAY`.
- **`buildTimeline()`** fills the `TL` object: `jobs` (one per subagent), `entries` (what each board cell says and when), `says` (captions), `bumps` (context meter changes), `chapters`, `fails`, and `mainSegs` (the main cursor's path).
- **`render()`** draws the page for the current time `T`. It should stay free of saved animation state: the same `T` must always draw the same page.
- **`frame()`** only moves `T` forward and calls `render()`. Scrubbing sets `T` directly through `seek()`.
- **The end state:** subagent cursors are hidden once their job ends, and only the main cursor remains.

Each job has four times: `start`, `arrive`, `workEnd` and `back`. To add a step, add it in `buildTimeline()`, and the slider, ticks and counters update from there.

## `low-tide-demo.html`: swarm over a page

- Mark any element with `data-l="t"` (text) or `data-l="b"` (block), and it joins the build automatically.
- `run()` sorts layers top to bottom, and `assignLayers()` hands them to free agents on a simulated clock.
- `moveAgent()` moves each cursor. In the `flock` phase, cursors orbit the real mouse.
- Unlike the overview, this animation is event-driven and can't be scrubbed.

## `playbook.html`: guide with one looping demo

The page is mostly static HTML. The task loop is driven by four arrays:

- `ACTORS`: each cursor's path as `[time, place]` keyframes. `:r` means the right edge of a place.
- `WRITES`: what appears in each station, and when.
- `LEDGER`: ledger lines.
- `CAPTIONS`: the narration.

`render()` draws the current time, so the slider works the same way as on the overview.

## `chat-demo.html`: simulated chat

- **The clock:** every wait goes through `sleep()`, so pause, speed and skip work everywhere. Replay calls `cancelAll()`, which rejects pending waits with `ABORT` to stop a running script.
- **One script for both modes:** `workflow(config)` runs the whole session. `DEMO` is the autoplay's config, and `buildConfig(feature)` makes one from what the viewer types.
- **Autoplay or real choice:** `ask(options, autoIndex)` lets the fake pointer pick when `autoIndex` is set, and otherwise waits for a click.
- **Branches:** `subagentBuild()` and `nativeBuild()` follow the viewer's execution choice.
- **Free chat:** `handle()` routes each message. `buildRequest()` spots build requests, and `answerFor()` matches questions against the `KB` list by keyword. Keywords match from the start of a word, and those of four characters or fewer must match the whole word, so "ai" doesn't match "main".
- **Safety:** viewer text goes through `esc()` or `textContent`. A test request containing HTML stayed plain text, and any new output must do the same.

To add an answer, add an entry to `KB`, then check its question actually reaches it. One bug came from a chip's own wording not matching its keywords.

## Conventions

- Respect `prefers-reduced-motion`: those viewers get the finished state straight away.
- A page opened in a background tab waits until it's visible before playing.
- There should be no sideways scrolling at phone width (about 375px).
- Write captions in plain language, and label made-up content.

## Testing

There are no automated tests. Serve the folder and check by hand:

```bash
python -m http.server 8765
```

Checks worth repeating after a change:

- Each page plays through to its end state with no console errors.
- On the timeline pages, moving away from a moment and back gives an identical state.
- There's no sideways scrolling at 375px, and light and dark themes both work on the chat demo.
- On the chat demo, try skip, replay during a choice, typed questions and a build request.
- Try sending with a real keyboard, not only by script.

**Testing in a hidden browser pane:** hidden panes throttle `requestAnimationFrame` to about two frames per second, and screenshots can come back blank. Before starting a run, you can replace it from the console:

```js
window.requestAnimationFrame = (cb) => setTimeout(() => cb(performance.now()), 40);
```

This confirms behaviour only. It says nothing about how smooth the page looks.

## Publishing as a Claude Artifact

Artifacts are published without the page's own `<!doctype>`, `<html>`, `<head>` and `<body>` tags, because the host adds them. Remove those tags first, and swap the relative links between pages for artifact URLs.
