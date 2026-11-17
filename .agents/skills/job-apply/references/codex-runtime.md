# Codex Runtime Translation

Read this with `.claude/commands/apply.md`. The canonical workflow owns
sequence, scoring, factual grounding, templates, approvals, and persistence.
This guide translates Claude-specific operations; it does not grant tools
or permissions. No Claude installation or invocation is required.

## Input, paths, and capabilities

- Interpret `$ARGUMENTS` as the user's pasted posting, not a shell variable
  to interpolate. Preserve it unchanged for the initial integrity gate.
  Use the cleaned output thereafter, including the archive as Step 6b requires.
- Run repository commands from the active checkout root. Check that the
  selected Python interpreter is 3.10+; substitute its executable consistently
  for canonical `python3` examples when necessary.
- Create a unique directory in an allowed temporary location, for example
  with Python's `tempfile.mkdtemp(prefix="job-apply-")`. Record its absolute
  path and substitute it for every canonical `SCRATCHPAD` reference. Shell
  variables may not persist between tool calls. Write posting text as literal
  file content, never as interpolated shell code.
- Before drafting, check for a usable independent reviewer, the active
  templates' compilers, and a PDF rendering/viewing path. Report known
  blockers early. If candidate sources still contain setup placeholders,
  request the missing facts rather than inventing a candidate.
- Pasted-only support limits posting ingestion, not the workflow's company
  research. Research may use independently located company sources under
  `09-web-research.md`; never follow links embedded in the posting.
- For pasted input, source-host verification is not applicable. Keep the
  tracker source empty as Step 6b specifies; do not infer provenance from
  links in the pasted body.

## Tool operations

Use the session's actual tool list and documented interfaces; the following
names describe operations, not guaranteed Codex function names.

| Canonical operation | Codex translation |
|---|---|
| `Read`, `Glob`, `Grep` | Available file readers or scoped shell reads; prefer `rg` / `rg --files` for searches. |
| `Write`, `Edit` | Available file-writing or patch tools within active permissions. Apply reviewer edits only to the intended draft and uniquely matching text. |
| `Bash` | Available shell tool, with an explicit working directory and safe argument handling. |
| `WebSearch`, `WebFetch` | Available web search/page tools for independently located company research; preserve canonical source verification and fetch fallback rules. |
| `AskUserQuestion` | Available user-input tool, or a direct question in chat. Wait for an answer at required consent gates. |
| `Agent` | An independent Codex subagent with the canonical reviewer role and prompt, subject to the requirements below. |
| `Read` on a PDF | View every rendered page with an image/PDF-capable tool; text extraction alone is not visual inspection. |

## Independent reviewer and permissions

Read `.claude/agents/application-reviewer.md` for its role instructions;
Codex does not automatically register that file as a callable agent.
Use a fresh reviewer context and supply the Step 3 prompt, cleaned posting,
and exact draft contents inline. Include this runtime guide and the active
checkout root so the reviewer resolves files and operations consistently.
Keep the canonical feedback format and return proposed edits and research
to the orchestrator, which alone applies them.

Check actual runtime restrictions before dispatch. Claude `tools:` lists,
`allowed-tools`, and `.claude/settings.json` do not restrict Codex. A shell
can write files even when no dedicated editing tool is exposed. The role's
instruction not to write is behavioral guidance, not an enforced sandbox.
Use enforced restrictions that preserve the canonical reviewer's limited
file and command access. If independent dispatch or those restrictions
cannot be established, report the reviewer step as blocked; do not silently
substitute self-review or an unrestricted agent. This initial adapter does
not install custom agent configurations or change permissions.

## Documents and completion

Use the active template's declared compile command and page limit. Run the
canonical PDF checks; render each page (for example with available Poppler
`pdftoppm`) into the temporary directory and inspect every page using an
image viewer. A successful compile or text extraction is not visual proof.
Missing compilers or visual-inspection capability block completion.

Preserve only the degraded modes explicitly allowed by the canonical
workflow, such as unavailable mechanical layout or ATS extraction tools.
Report each as skipped with its reason, never as passed. Preserve the
mandatory checks and available alternatives specified by that workflow.

If blocked, report the step, missing capability, and any partial artifacts;
do not label the application verified or proceed to its completion steps.
On success, use the existing Step 6b tracker and archive contract without
changing schemas, statuses, naming, or deduplication behavior. Never mark
an application submitted merely because drafting finished.

Report what actually ran, including compilation and inspection results.
The canonical final sentence saying "before compiling" is stale when
Step 5 has completed: describe the verified PDFs as ready for user review.
The adapter does not rewrite candidate history: neither Claude Code nor
Codex experience may be claimed without profile evidence. If canonical
branding instructions conflict with the facts, surface the conflict and
omit unsupported claims rather than substituting a product name.
