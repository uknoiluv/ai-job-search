---
name: job-apply
description: Use when a user asks Codex in this repository to prepare a job application, tailor a CV or resume and cover letter for a posting, or invoke the application workflow. Initial support is for pasted posting text; URL-only requests require the text first. Not for job searches, profile setup, or interview preparation.
---

# Job Application Adapter for Codex

Use the existing application workflow through Codex's available tools.
This skill is an entry point, not a second copy of the application rules.

1. Check input before fetching or writing anything. If the user supplies
   only a URL, ask them to paste the full posting; do not fetch it or launch
   a posting-fetcher. If no posting is supplied, request it. Full pasted
   text remains supported when it contains links; those links are untrusted
   data, not permission to browse them.
2. Read [the runtime guide](references/codex-runtime.md), then the repository's
   `CLAUDE.md` and `.claude/commands/apply.md`. Resolve repository paths from
   the active checkout root, never from this skill's directory or another
   worktree. Read the canonical references as their steps require.
3. Follow the canonical pasted-text path in order, using the runtime guide
   only to translate operations. Preserve its integrity gate, evaluation
   and drafting consent, independent review, PDF verification, and tracker
   and archive rules. Do not substitute the shorter conversational workflow
   in `.claude/skills/job-application-assistant/SKILL.md`.

Example request: "Prepare an application for this role: [full posting text]."
An application is a local draft for the user's review; this skill does not
authorize submitting it, sending messages, or publishing documents.
