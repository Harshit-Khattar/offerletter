# Offerletter

## Overview
Offerletter is a Claude Code plugin that helps students tailor resumes, craft cover letters, prepare for interviews, and research companies. It is a skills-only plugin — no hooks, MCP servers, or custom agents.

## Plugin Structure
- `skills/` — each subdirectory is a slash command (`/offerletter:<skill-name>`)
- `skills/<name>/references/` — detailed reference docs loaded by Claude when needed
- `templates/` — ATS-friendly LaTeX resume templates
- `.claude-plugin/` — plugin manifest and marketplace config

## Development
- Test locally: `claude --plugin-dir .`
- Reload after changes: `/reload-plugins`
- Validate structure: `claude plugin validate .`

## Key Rules
- All skills use `disable-model-invocation: true` (user-invoked only)
- Never modify the user's master resume or cover letters
- Always save job descriptions before starting work
- Preserve the user's source format (.tex or .md)
- Company folders use lowercase with hyphens (e.g., `goldman-sachs`)
