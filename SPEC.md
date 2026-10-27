# VectorCraft: spec (our fork)

**Approval:** 2026-10-26, by the owner: the specs and roadmaps were developed upstream, so normalize them to our system (spec = upstream roadmap + our delta, R18).

## The spec is upstream's

VectorCraft is a fork of [storytold/vectorcraft](https://github.com/storytold/vectorcraft). Upstream's plan is the spec:

- [`ROADMAP.md`](https://github.com/storytold/vectorcraft/blob/main/ROADMAP.md): the summary, stage and headline numbers (parity with Adobe Illustrator).
- [`docs/gaps.md`](https://github.com/storytold/vectorcraft/blob/main/docs/gaps.md): the ranked work list. The current stage is G1, G9, G10, G8, G11, G12 (the gaps marked as blocking beta).
- [`docs/roadmap.md`](https://github.com/storytold/vectorcraft/blob/main/docs/roadmap.md): milestones and the current focus.

Our copies of those files come in with the daily upstream merge; never edit them here.

**1.0 for our fork:** upstream's beta, plus the delta below, used for real work on Mac, PC and Linux.

## Our delta

What our fork has or wants that upstream does not. "Send upstream" work is built here and offered upstream as a pull request (R36); "keep on our fork" stays here.

| Item | Where it goes |
|---|---|
| Agent-skills config: lines in upstream's `CLAUDE.md` and `docs/agents/` (commit 64999520) | keep on our fork |
| Pipeline v2 files: `PIPELINE.md`, `SPEC.md`, `CHANGELOG.md`, `AGENTS.fork.md`, `docs/code-map.md` | keep on our fork |
| The owner's 95% feature list for real work (#7) | keep on our fork |
| First real-use test on each platform and a golden task (#8) | keep on our fork |
| Sibling sweep bug classes BC1–BC3, 4 candidates (#5) | send upstream |
| CI on Windows and macOS for pull requests (R04) | send upstream |
| Beta-list build issues filed 2026-10-26 (open gaps not already covered by an open upstream PR) | send upstream |

Our issues and our code map cover the delta and the build issues we take from upstream's current stage. Anything else upstream builds itself: check upstream's open pull requests before starting an issue, and close ours if upstream has it.
