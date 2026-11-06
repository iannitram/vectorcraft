Stage: Parked
Since: 2026-11-06
Kind: fork (upstream: storytold/vectorcraft)
Spec: SPEC.md   Roadmap: ROADMAP.md (upstream's) and docs/gaps.md   Code map: docs/code-map.md
Platforms: mac, windows, linux
Notes: Parked 2026-11-06 on my call; no satellite takes issues here until I unpark it (R26). PR #33 stays open, held. Before parking: Spec = upstream roadmap + our delta (2026-10-26). Build issues for upstream's current stage: #17-#28 (1 Easy, 8 Medium, 3 Hard; #26 resized to Medium 2026-10-26); start with #17 (CI on Windows and macOS). Every build issue is "send upstream": check upstream's open PRs first. Agent rules for our pipeline: AGENTS.fork.md (upstream owns AGENTS.md and CLAUDE.md). Integration branch: main.

Stages: Proposal -> Spec -> Roadmap -> Dev Loop -> Prototype / Beta.
What each stage means and who moves a project: `PIPELINE.md` in the pipeline repo (private).
The Project Manager updates this file when the stage changes and adds a CHANGELOG line.
