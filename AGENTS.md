---
framework_version: 1.0.2
---

# Agent Guidelines: AI Job Search

This workspace is structured to manage job search activities, scraper tools, CVs, cover letters, and interview preparation.

## Thin-Pointer Design (Single Source of Truth)

To prevent duplication and configuration drift across different AI agent frameworks (Claude Code, Google Antigravity, Codex, Cursor, Gemini CLI, etc.), this workspace uses a unified thin-pointer design. All agent runtimes should load the canonical specifications and candidate profiles from the files and directories below:

1. **Personal Candidate Profile:**
   - The candidate profile, contact details, education, and target preferences are defined in [CLAUDE.md](CLAUDE.md) and the individual profile methodology files under [.claude/skills/job-application-assistant/](.claude/skills/job-application-assistant/) (specifically `01-*.md` etc.).
2. **Canonical Workflow Specifications:**
   - The step-by-step instructions and triggers for tasks (setup, scrape, rank, apply, upskill, interview) are defined in the [.claude/](.claude/) directory (specifically under `.claude/skills/` and `.claude/commands/`).
   - Do not duplicate these rules or specifications. Treat `.claude/` files as the single source of truth.
3. **Portal Search Skills:**
   - Job-portal search CLIs are installed under `.agents/skills/` in the portable Agent Skills format (with a `SKILL.md` per portal). None ship with this repo: copy them in from [community-portals](https://github.com/ai-job-search-dev/community-portals). Codex and Antigravity discover these automatically; the `/scrape` workflow in [.claude/skills/job-scraper/](.claude/skills/job-scraper/) orchestrates them.

## Codex Application Adapter

When running in Codex:

- For requests to prepare a job application, read
  `.agents/skills/job-apply/SKILL.md` and follow its entry instructions.
- The adapter translates runtime-specific operations only. The canonical
  application workflow remains `.claude/commands/apply.md`; candidate
  information and methodology remain in the locations listed above.
- Apply the adapter's translation rules when canonical instructions refer
  to Claude-specific tools, argument placeholders, or temporary directories.
  Do not use those translations to omit workflow steps or weaken factual
  accuracy and document-verification requirements.
- Claude permission settings and tool allowlists do not configure Codex.
  Follow the active Codex permissions, and do not describe an agent as
  restricted unless those restrictions are actually enforced.
- If a required capability is unavailable, explain the blocked step.
  Do not silently substitute a weaker check or report it as completed.
- The initial adapter supports user-pasted job postings. For URL input,
  explain this limitation and request the posting text.
