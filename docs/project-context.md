# Project context

Read this first when continuing the work. Last updated 2026-11-02.

## How it started

The idea came from an [Instagram reel by @dododididaw](https://www.instagram.com/reel/DfMhyC7Ma31/): a swarm of coloured "agent" cursors appears to rebuild a portfolio site, ending on "Rebuilt by 30 agents in 51.4s". Everything here reuses that visual idea with original content. The reel itself is not in this repo and shouldn't be added, because it's someone else's work.

## Order of the work

1. `low-tide-demo.html`: the swarm animation on a made-up field recording studio site. Cursors follow the mouse after the build.
2. `index.html`: the same animation style applied to explaining subagent-driven development.
3. `index.html` revised: no subagent cursors after the end, a timeline controller, a pink main agent.
4. `playbook.html`: a guide based on reading the Superpowers skill files.
5. `chat-demo.html`: a simulated chat session that becomes interactive when the animation ends.

## What the owner asked for

Keep these unless told otherwise:

- **Overview page:** subagent cursors must not remain or follow the mouse after the animation ends. The main agent has its own colour (pink). There's a draggable timeline.
- **Low Tide page:** cursors do follow the real mouse after the build.
- **Chat demo:** it should look like a chat screen, play a simulated session, then be interactive.
- **Navigation:** the overview links to the playbook at the bottom.

## Decisions and why

- **One HTML file per page, no build step.** They're easy to open, share and host anywhere.
- **Links between pages are relative in this repo.** The owner's private Claude Artifact copies use artifact URLs instead (see below).
- **The chat demo resembles a chat product without copying one.** It has no logo or product name, and it's labelled "Simulated demo" with a note that no AI is connected, so it can't be mistaken for the real thing. Keep those labels, and don't add a logo or trademark.
- **Made-up content is labelled as made up.** Keep that in the page footers and captions.
- **The playbook follows the skill files over the README** where they disagree (see [superpowers-notes.md](superpowers-notes.md)).

## Open items

1. **The overview's animation doesn't match Superpowers in three ways.** It shows three implementers in parallel, separate spec and code reviewers, and a new fixer per failed review. Superpowers runs one implementer at a time, uses one reviewer with two verdicts, and resumes the same implementer for fix rounds 1 to 3. The owner hasn't decided whether to change it or keep it as the general pattern. The playbook's footer explains the difference for now.
2. **Whether to share the chat demo more widely is undecided.** It was held back from publishing as a Claude Artifact so that sharing stayed the owner's call.
3. **The chat demo's answers are scripted.** Real answers would need a connection to a model, which hasn't been explored.
4. **No license file yet.** The owner hasn't chosen one.
5. **GitHub Pages isn't set up.** Because `index.html` is at the root, it would load at the site's main address.

## Not yet checked

- Smoothness at normal speed. Testing ran in a hidden browser pane with a substitute frame timer (see [architecture.md](architecture.md)).
- Touch input on a real phone. Phone widths were only emulated.
- Running Superpowers itself. These pages come from reading its files, not from using it.

## Private Artifact copies

The owner also has private published copies, which only their account can open. They're separate from this repo, so a change here doesn't update them.

| Page | Artifact |
|---|---|
| Overview | https://claude.ai/artifact/SdnCUCQZ6V2ZzzHutSzRx5 |
| Playbook | https://claude.ai/artifact/2ZuLMiLhQjgVyaenPtPDHX |
| Low Tide demo | https://claude.ai/artifact/1ac8BBg3Rzq7eRrANuoweU |
