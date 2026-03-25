# Offerletter

## Overview
Claude Code plugin helping students tailor resumes, craft cover letters, prep for interviews, and research companies. Skills-only — no hooks, MCP servers, or agents.

## Structure
- `skills/` — slash commands (`/offerletter:<name>`)
- `skills/<name>/references/` — detailed docs loaded when needed
- `templates/` — ATS-friendly LaTeX resume templates
- `.claude-plugin/` — plugin manifest and marketplace config

## Development
- Test: `claude --plugin-dir .`
- Reload: `/reload-plugins`
- Validate: `claude plugin validate .`

## Shared Rules (all skills follow these)

1. **Never modify originals** — never edit the user's master resume or reference cover letters. Always create new files in `companies/<company-name>/`
2. **Company folders** — lowercase, hyphens for spaces (e.g., `goldman-sachs`). Save JD to `companies/<name>/job-description.txt` before starting work
3. **Preserve format** — if master is `.tex`, output `.tex`. If `.md`, output `.md`. For `.tex` files: copy the entire preamble (everything before `\begin{document}`) verbatim. Only change content inside `\begin{document}...\end{document}`
4. **Keep filenames** — output uses the same base filename as the master (e.g., `main 2.tex` stays `main 2.tex`, not `resume.tex`)
5. **One page max** — student resumes must fit on one page. Verify after PDF compilation. If over, ask user what to cut
6. **Approval before edits** — always present proposed changes as a numbered list and wait for explicit user approval before writing any file
7. **WebSearch fallback** — if WebSearch is unavailable, use general knowledge and inform the user
8. **PDF compilation** — see `skills/resume/references/pdf-compilation.md`. Prefer pdflatex, auto-install tectonic if nothing available. Never suggest MacTeX/TeX Live
9. **Job links** — if user provides a URL, use WebFetch to get JD. If blocked/incomplete, ask user to paste it
