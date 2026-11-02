# Subagent-driven development pages

Animated pages that explain subagent-driven development and how to do it with the [Superpowers](https://github.com/obra/superpowers) skills. Each page is one self-contained HTML file with no build step.

## Pages

| File | What it is |
|---|---|
| [`index.html`](index.html) | Animated overview. A main agent sends cursor subagents across a task board, with a draggable timeline. |
| [`playbook.html`](playbook.html) | Practical guide to using Superpowers for this, with a walkthrough of one task's loop. |
| [`chat-demo.html`](chat-demo.html) | Simulated chat that plays a full Superpowers session, then lets you ask questions or run your own simulated build. |
| [`low-tide-demo.html`](low-tide-demo.html) | The earlier cursor-swarm animation, rebuilding a made-up website. Its cursors follow the mouse when it finishes. |

`index.html` and `playbook.html` link to each other.

## Run it

Open any file in a browser. Fonts come from Google Fonts, so they fall back to system fonts when offline.

To serve the folder locally:

```bash
python -m http.server 8765
```

## Docs

- [`docs/project-context.md`](docs/project-context.md): how the project got here, decisions made, and what's still open. **Start here when picking the work back up.**
- [`docs/architecture.md`](docs/architecture.md): how each page works, how to change it, and how to test it.
- [`docs/superpowers-notes.md`](docs/superpowers-notes.md): what the pages rely on from Superpowers, and which version.

## Accuracy

The features, file names, commits and context percentages in the demos are made up to show the idea. `chat-demo.html` is a script: no AI is connected, and nothing is really built.

This project is independent, and isn't made by Anthropic or the Superpowers team. Superpowers is by Jesse Vincent and Prime Radiant, under the MIT license.
