# Offerletter Plugin — Design Specification

**Date:** 2026-03-22
**Author:** Harshit Khattar
**Status:** Approved

## Overview

Offerletter is a Claude Code plugin that helps students tailor resumes, craft cover letters, prepare for interviews, and research companies. It runs in the Claude Desktop app (CoWork/CoTab) and is distributed via the official marketplace.

The plugin is skills-only (Approach A) — no hooks, MCP servers, or custom agents. All functionality lives in SKILL.md files with supporting reference documents. This keeps the plugin simple, dependency-free, and easy to maintain.

## Plugin Identity

```json
{
  "name": "offerletter",
  "description": "AI-powered career toolkit for students — tailor resumes, craft cover letters, prep for interviews, and research companies.",
  "version": "1.0.0",
  "author": {
    "name": "Harshit Khattar"
  },
  "homepage": "https://github.com/Harshit-Khattar/offerletter",
  "repository": "https://github.com/Harshit-Khattar/offerletter",
  "license": "MIT",
  "keywords": ["resume", "interview", "career", "job-search", "cover-letter", "students"]
}
```

This repo acts as both the plugin and its own marketplace. The `marketplace.json` sits inside `.claude-plugin/` per the marketplace convention (the `.claude-plugin/` directory is the marketplace root).

## Plugin Repository Structure

```
offerletter/
├── .claude-plugin/
│   ├── plugin.json
│   └── marketplace.json
├── skills/
│   ├── resume/
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── alignment.md
│   │       ├── skills-identification.md
│   │       ├── ats-optimization.md
│   │       ├── bullet-optimization.md
│   │       ├── multi-job-fit.md
│   │       └── pdf-compilation.md
│   ├── cover-letter/
│   │   ├── SKILL.md
│   │   └── references/
│   │       └── review-checklist.md
│   ├── interview/
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── behavioral.md
│   │       ├── technical.md
│   │       ├── motivation.md
│   │       └── informational-interview.md
│   ├── career/
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── self-assessment.md
│   │       └── role-mapping.md
│   ├── company-research/
│   │   └── SKILL.md
│   └── keywords/
│       └── SKILL.md
├── templates/
│   ├── ats-resume-clean.tex
│   ├── ats-resume-modern.tex
│   └── ats-resume-academic.tex
├── CLAUDE.md
├── README.md
├── LICENSE
└── CHANGELOG.md
```

## User's Working Folder Convention

Users open this folder in Claude Desktop CoWork/CoTab. No config file needed — the plugin uses convention-based file discovery.

```
my-job-search/
├── resume.tex (or resume.md)          ← master resume
├── cover-letters/                      ← master cover letters for reference
│   ├── cover-letter-1.tex
│   └── cover-letter-2.md
├── companies/                          ← plugin creates per-company folders
│   ├── google/
│   │   ├── job-description.txt
│   │   ├── resume.tex
│   │   ├── resume.pdf
│   │   ├── cover-letter.tex
│   │   ├── cover-letter.pdf
│   │   ├── interview-prep.md
│   │   ├── company-research.md
│   │   └── keywords.md
│   └── amazon/
│       └── ...
├── career-assessment.md                ← career exploration outputs
├── target-companies.md
└── role-clarity.md
```

### File discovery rules

- Master resume: any `.tex`, `.md`, or `.pdf` file in the project root with "resume" in the name
- Cover letters: all `.tex`, `.md`, or `.pdf` files in `cover-letters/` directory. If the directory doesn't exist, skills that need cover letter references will inform the user: "No cover-letters/ folder found. Create one with your reference cover letters for best results, or I can proceed without style reference."
- If expected files aren't found, the skill provides a clear error message explaining the expected convention
- No setup command — users create the structure themselves

## Skills

### Skill 1: `/offerletter:resume`

**Purpose:** All resume-related tasks — tailoring, optimization, gap analysis, bullet rewrites, multi-job comparison.

**Frontmatter:**
```yaml
---
name: resume
description: Tailor your resume to a job description, optimize for ATS, identify skill gaps, and improve bullet points.
disable-model-invocation: true
---
```

**Sub-tasks (Claude infers from context or asks):**

| Sub-task | Description |
|---|---|
| Resume-JD alignment | Tailor resume content to match a specific job description |
| Skills identification | Extract soft/transferable skills from a job description |
| Skills translation | Translate academic experience to industry language |
| Technical skills optimization | Organize and prioritize technical skills for the role |
| Project description enhancement | Rewrite project bullets with quantified impact |
| ATS optimization | Review formatting, keyword density, ATS parsing compatibility |
| Gap analysis | Identify weaknesses and missing requirements vs job description |
| Multi-job fit ranking | Compare resume against multiple job descriptions, rank fit |
| Redundancy check | Find and consolidate repetitive bullet points |
| Tasks vs accomplishments | Convert task-oriented bullets to achievement statements |

**Interaction flow:**
1. User runs `/offerletter:resume`, pastes job description and company name
2. Claude saves `job-description.txt` to `companies/<company-name>/`
3. Claude reads master resume
4. Claude presents analysis: what to change, what to emphasize, gaps found
5. Back-and-forth discussion — user approves, requests changes, or redirects
6. On final approval, Claude creates tailored resume in `companies/<company-name>/`
7. Claude compiles to PDF (see PDF Compilation Strategy)
8. Claude confirms: files saved, paths listed

**Reference files:**
- `references/alignment.md` — detailed prompts for JD alignment, keyword matching
- `references/skills-identification.md` — soft skills extraction, transferable skills mapping
- `references/ats-optimization.md` — ATS formatting rules, keyword density guidelines
- `references/bullet-optimization.md` — tasks→accomplishments conversion, redundancy detection
- `references/multi-job-fit.md` — multi-JD comparison and ranking logic
- `references/pdf-compilation.md` — cross-platform PDF generation instructions

### Skill 2: `/offerletter:keywords`

**Purpose:** Quick extraction of top ATS keywords from a job description.

**Frontmatter:**
```yaml
---
name: keywords
description: Extract the top ATS keywords from a job description to optimize your resume.
disable-model-invocation: true
---
```

**Interaction flow:**
1. User runs `/offerletter:keywords`, pastes job description and company name
2. Claude extracts top 20 keywords, categorized by type (technical, soft, domain)
3. Claude saves to `companies/<company-name>/keywords.md`
4. Single output — no back-and-forth needed

### Skill 3: `/offerletter:cover-letter`

**Purpose:** Create or review cover letters tailored to a specific job.

**Frontmatter:**
```yaml
---
name: cover-letter
description: Create a tailored cover letter or review and improve an existing draft for a specific job.
disable-model-invocation: true
---
```

**Sub-tasks:**

| Sub-task | Description |
|---|---|
| Creation | Draft a new cover letter based on JD + master resume + reference cover letters |
| Review & enhancement | Review an existing draft for impact, tone, relevance, grammar |

**Interaction flow:**
1. User runs `/offerletter:cover-letter`, provides JD and company name
2. Claude reads master cover letters (for tone/style reference) and master resume
3. Claude drafts or reviews, discusses with user
4. On approval, saves tailored cover letter + PDF to `companies/<company-name>/`

**Key behavior:** The generated cover letter must match the user's writing style from their reference cover letters. It should not sound AI-generated.

**Reference files:**
- `references/review-checklist.md` — detailed review criteria (opening impact, flow, specificity, tone, grammar)

### Skill 4: `/offerletter:interview`

**Purpose:** Interview preparation — question generation, answer frameworks, company-specific prep.

**Frontmatter:**
```yaml
---
name: interview
description: Prepare for interviews with targeted questions, answer frameworks, and company-specific preparation.
disable-model-invocation: true
---
```

**Sub-tasks:**

| Sub-task | Description |
|---|---|
| Targeted role questions | Generate 8-10 likely interview questions based on resume + JD |
| Behavioral questions | STAR-method behavioral questions with answer frameworks |
| Technical questions | Technical/coding questions appropriate for the role level |
| Motivation questions | "Why this company/role?" preparation with frameworks |
| Questions to ask | 10-12 smart questions to ask interviewers |
| Informational interview | Prep for networking/informational conversations |

**Interaction flow:**
1. User runs `/offerletter:interview`, specifies company name and optionally which sub-task
2. Claude reads existing company folder (JD, research, resume) for context
3. Claude uses WebSearch to find company-specific interview questions on Reddit, LeetCode, Glassdoor
4. Interactive discussion — Claude presents questions, user can ask for answer coaching
5. Saves everything to `companies/<company-name>/interview-prep.md`

**Web research strategy:**
- Search: `"<company>" interview questions site:reddit.com`, `site:leetcode.com/discuss`, `site:glassdoor.com`
- Search: `"<company>" "<role>" interview experience`
- Fetch accessible results, synthesize findings
- Fall back to Claude's general knowledge when results are blocked or sparse
- Always cite sources when using web results

**Reference files:**
- `references/behavioral.md` — STAR framework, common behavioral questions, competency mapping
- `references/technical.md` — technical question generation by role type and level
- `references/motivation.md` — company-specific motivation answer frameworks
- `references/informational-interview.md` — networking question strategies, strategic purposes

### Skill 5: `/offerletter:company-research`

**Purpose:** Research a company for interview prep and application strategy.

**Frontmatter:**
```yaml
---
name: company-research
description: Research a company — culture, recent news, interview process, and strategic insights for your application.
disable-model-invocation: true
---
```

**Interaction flow:**
1. User runs `/offerletter:company-research <company-name>`
2. Claude uses WebSearch to gather information: company blog, news, Reddit, Glassdoor, LinkedIn (public pages)
3. Generates structured research document covering: company overview, culture, recent news, tech stack, interview process, tips
4. Saves to `companies/<company-name>/company-research.md`
5. Single output — minimal back-and-forth

### Skill 6: `/offerletter:career`

**Purpose:** Career exploration — role clarity, self-assessment, target company identification.

**Frontmatter:**
```yaml
---
name: career
description: Explore career paths, assess your goals, identify target roles, and find companies that match your profile.
disable-model-invocation: true
---
```

**Sub-tasks:**

| Sub-task | Description |
|---|---|
| Role clarity | Identify 5-7 target job titles, map skills to roles, find gaps |
| Self-assessment | Guided questionnaire on career goals, preferences, priorities |
| Target companies | Identify top 10 target companies with rationale and strategy |

**Interaction flow:**
1. User runs `/offerletter:career`
2. Claude asks which sub-task (or infers from context)
3. Interactive back-and-forth — asks questions one at a time, builds understanding
4. Generates structured output, saves to project root:
   - `role-clarity.md` — role analysis and recommendations
   - `career-assessment.md` — self-assessment results
   - `target-companies.md` — ranked company list with strategy

**Reference files:**
- `references/self-assessment.md` — structured questionnaire covering interests, preferences, aspirations, work-life balance, compensation, risk tolerance
- `references/role-mapping.md` — skills-to-roles mapping logic, role comparison frameworks

## Core Rules (All Skills)

These rules are embedded in every SKILL.md:

1. **Never modify master files** — always create new files in `companies/<name>/` or project root
2. **Always save the job description** — to `companies/<name>/job-description.txt` before starting work
3. **Match the user's writing style** — output should not look AI-generated. Reference master resume and cover letters for tone and voice
4. **Preserve source format** — if input is `.tex`, output `.tex` in the same style. If `.md`, output `.md`
5. **Compile to PDF** — always attempt after writing source files (see PDF Compilation Strategy)
6. **Company folder naming** — lowercase, hyphens for spaces (e.g., `goldman-sachs`, `jane-street`)
7. **Respect existing company folders** — if a folder already exists, read existing files for context. Don't overwrite without asking
8. **Web research** — use WebSearch for company research and interview prep. Cite sources. Fall back to general knowledge gracefully. If WebSearch is not available in the user's environment, inform them and proceed with general knowledge only
9. **Error handling** — if master resume not found, explain the expected convention clearly. Don't fail silently
10. **Interactive by default** — present suggestions and get approval before writing files. Don't auto-generate without discussion (except keywords and company-research which are single-output)
11. **Use `$ARGUMENTS`** — all skills should use the `$ARGUMENTS` placeholder to capture user input (company name, job description text, etc.) passed after the slash command

## PDF Compilation Strategy

### Decision tree

```
Need to generate PDF
    │
    ├── Is source a .tex file?
    │   ├── Check: pdflatex --version
    │   ├── Check: xelatex --version
    │   ├── Check: tectonic --version
    │   ├── Found one? → Compile → Done
    │   └── None found? → Go to "Install compiler"
    │
    └── Is source a .md file?
        └── Claude converts .md content to .tex → then same as above

Install compiler
    │
    ├── Detect OS (uname / check for Windows)
    ├── Detect package manager
    │   ├── macOS: brew install tectonic
    │   ├── macOS (no brew): curl binary from tectonic GitHub releases
    │   ├── Windows: winget install tectonic
    │   ├── Windows (no winget): scoop install tectonic
    │   ├── Windows (neither): download .exe from GitHub releases
    │   ├── Linux (apt): sudo apt install tectonic
    │   ├── Linux (dnf): sudo dnf install tectonic
    │   └── Linux (other): curl binary from GitHub releases
    │
    ├── Ask user permission before installing anything
    ├── Install → Compile → Done
    │
    └── User declines install
        → Save source file only
        → Tell user: "Resume saved as resume.tex. Install tectonic
           to compile to PDF, or compile manually with your LaTeX editor."
```

### Principles

- **Never block on PDF** — source file is always saved regardless of compilation outcome
- **Ask before installing** — Claude Code's permission prompt handles user consent
- **Clean up build artifacts** — remove `.aux`, `.log`, `.out` files after compilation
- **Graceful fallback** — if compilation fails, provide clear instructions for manual compilation

### Templates

For users with only a PDF input or who want a fresh format:

| Template | Use case |
|---|---|
| `ats-resume-clean.tex` | Minimal single-column, most ATS-friendly |
| `ats-resume-modern.tex` | Slight visual flair, still ATS-parsable |
| `ats-resume-academic.tex` | Research/publications focused |

Plus any custom templates the user adds to `templates/`.

Claude picks the best template based on the user's field and preferences, populates with their content, and compiles.

## Input Format Handling

| User provides | Working format | Output |
|---|---|---|
| `.tex` file | Edit `.tex` directly | `.tex` + compiled `.pdf` |
| `.md` file | Edit `.md` directly | `.md` + `.tex` (converted) + compiled `.pdf` |
| `.pdf` only (fallback) | Extract content, generate from ATS template | `.tex` + compiled `.pdf` |

## Marketplace Distribution

```json
{
  "name": "offerletter-marketplace",
  "owner": {
    "name": "Harshit Khattar",
    "email": "harshitkhattar@example.com"
  },
  "plugins": [
    {
      "name": "offerletter",
      "source": "./",
      "description": "Tailor resumes, craft cover letters, prep for interviews, and research companies.",
      "version": "1.0.0"
    }
  ]
}
```

Note: The `source: "./"` is relative to the marketplace root (the directory containing `.claude-plugin/`), which points to the repo root where the plugin's `skills/`, `templates/`, etc. live.

Users install via:
```
/plugin marketplace add Harshit-Khattar/offerletter
/plugin install offerletter@offerletter-marketplace
```

## Development & Testing

- Test locally with `claude --plugin-dir ./offerletter`
- After making changes to skills, run `/reload-plugins` to pick up updates without restarting
- Validate plugin structure with `claude plugin validate .` or `/plugin validate .`
- Test each skill individually: `/offerletter:resume`, `/offerletter:keywords`, etc.

## Future Considerations (Not in v1)

- MCP servers for Reddit/LinkedIn API access (better research reliability)
- Hooks for auto-compiling PDF on file save
- Application tracking dashboard (which companies applied to, status, dates)
- Email/message drafting for recruiter outreach
- Salary negotiation preparation skill
- Portfolio/GitHub profile optimization skill
- `settings.json` for user-configurable defaults (company folder naming, preferred PDF compiler, etc.)
- Workspace migration strategy if folder conventions change in future versions
