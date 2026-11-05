---
name: roast-room
description: Convene the Roast Room council to debate a business decision, run a quick or named-seat roast, consult a specific advisor, or manage the default board. Use when the user asks for Roast Room or its founder council.
---

# Roast Room for Codex

Act as Chair. Resolve the project root from this skill's location (three directories above the skill folder). Use that root for every resource and session path, even when the terminal starts elsewhere. The shared council protocol is in `.claude/skills/roast-room/SKILL.md`. Read it for the requested mode and follow it with the Codex adaptations below. Advisor prompts, brains, scoring, report format, and viewer file schemas are shared with the upstream workflow.

- Accept `$roast-room` followed by the decision and any supported flags. Treat a plain-language request for the same mode equivalently. For `board` and single-seat `ask`, follow the corresponding mode and skip council setup.
- Use Codex's available user-input tool or chat for the brief and board questions. Combine material questions in one batch. Honor explicit seats and requests to proceed with stated assumptions.
- Delegate each round's seat cards to independent Codex subagents when available and permitted. Use fresh, isolated context for each seat and pass only its persona Markdown path, the round prompt, and the listed inputs for that round. Treat Claude agent frontmatter as metadata. Each seat reads its own source files and returns a card. Only the Chair writes session files. Run in batches up to the active agent limit and release completed agents as needed. Round 1 agents get the brief without other seats' cards. Finish and validate each round before starting the next. If delegation is unavailable, simulate seats sequentially using the same inputs and disclose that the cards came from one Codex session.
- Use an unused, date-prefixed session directory under the repo's `sessions/`. Add a numeric suffix if the slug already exists. Write each phase's files in the order defined by `references/live-room.md`, relative to the shared skill folder. Publish complete files atomically by writing a temporary file beside the destination and renaming it. Write `verdict.json` only after checking the quotes and finishing `verdict.md`.
- The optional viewer reads those files at `http://localhost:4730` after the user starts `npm start` in this repo. Run the council in Codex; the viewer only plays it back. Give the final report path even if the viewer is offline.
- Board settings edit the shared roster. Use `$newroaster` to build and register a new advisor.
