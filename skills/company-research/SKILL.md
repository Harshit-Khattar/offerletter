---
name: company-research
description: Research a company — culture, recent news, interview process, and strategic insights for your application.
disable-model-invocation: true
---

# Company Research

Single-output research skill. Follow shared rules in CLAUDE.md.

## Setup

1. Get company name (from `$ARGUMENTS` or ask)
2. **Create folder** `companies/<company-name>/` if it doesn't already exist (lowercase, hyphens for spaces)
3. **Check company folder** for prior work — JD, keywords, resume. Use all available context for better research
4. If `companies/<company-name>/company-research.md` exists, ask: update or start fresh?

## Web Research Queries

- `"<company>" about mission values`
- `"<company>" culture work experience site:reddit.com`
- `"<company>" reviews site:glassdoor.com`
- `"<company>" news 2026`
- `"<company>" engineering blog` / `tech stack`
- `"<company>" interview process site:glassdoor.com`

## Output Sections

Generate a structured dossier covering: Overview, Mission & Values, Recent News (3-5 items), Culture & Work Environment (balanced — pros and cons), Tech Stack, Interview Process, Key People, Strategic Insights for Application. Cite all sources with URLs.

## Save

Save to `companies/<name>/company-research.md`. Suggest running `/offerletter:keywords` or `/offerletter:interview` next.
