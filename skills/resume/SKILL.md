---
name: resume
description: Tailor your resume to a job description, optimize for ATS, identify skill gaps, and improve bullet points.
disable-model-invocation: true
---

# Resume Optimization

Expert resume consultant. Follow shared rules in CLAUDE.md.

## Setup

1. Get company name + JD (user pastes or provides URL — if URL, use WebFetch to get content; if blocked, ask user to paste)
2. Find master resume in project root (any `.tex`, `.md`, or `.pdf` file — may not have "resume" in name). If multiple, ask which one
3. **Create company folder**: `companies/<company-name>/` (lowercase, hyphens for spaces, e.g. `goldman-sachs`)
4. **Save JD**: write to `companies/<company-name>/job-description.txt` before doing any analysis
5. Check company folder for prior work (keywords, research from other skills)

## Sub-Tasks

Determine from user request. If unclear, ask. Default is Resume-JD Alignment.

- **Resume-JD Alignment** — tailor resume for a specific JD (most common)
- **ATS Optimization** — formatting and ATS-compatibility review
- **Gap Analysis** — where resume falls short vs JD
- **Multi-Job Fit** — compare against multiple JDs, rank fit. See [multi-job-fit.md](references/multi-job-fit.md)
- **Bullet Optimization** — convert tasks to accomplishments. See [bullet-optimization.md](references/bullet-optimization.md)
- **Skills Translation** — academic → industry language

## Flow (Resume-JD Alignment)

**Step 1: Analyze** — read resume + JD. Identify strengths, gaps, keywords.

**Step 2: Present changes** — show a numbered list of every proposed change with before → after. Organize by section (skills, experience, projects). Include ATS keywords to add.

**Step 3: Get approval** — wait for explicit "go ahead." User may remove, modify, or add changes.

**Step 4: Write** — create tailored resume in `companies/<name>/`. Critical rules:
- **Same filename** as master (e.g., if master is `main 2.tex`, output is `companies/<name>/main 2.tex`)
- **Copy preamble verbatim** — everything before `\begin{document}` must be identical to master. Do NOT add, remove, or change any preamble line
- **Only edit content** inside `\begin{document}...\end{document}`
- **No em dashes (—)** anywhere. Use commas, periods, or rewrite
- **No repeated action verbs** — every bullet starts with a unique verb. Check the full resume before finalizing
- **Preserve spacing** — do not add/remove `\vspace`, section spacing, or blank lines from the original structure

**Step 5: Compile + verify** — compile to PDF per [pdf-compilation.md](references/pdf-compilation.md). Run page count check command. **If >1 page: STOP. Do not tell user it's done.** Tell user it's over 1 page, suggest specific cuts, wait for decision, recompile.

**Step 6: Final check** — before confirming, verify: (a) filename matches master, (b) no em dashes in file, (c) page count = 1, (d) no repeated starting verbs.

**Step 7: Confirm** — list all files saved with paths.

## References (load only when needed)

- [alignment.md](references/alignment.md) — JD alignment strategies
- [skills-identification.md](references/skills-identification.md) — soft/transferable skills
- [ats-optimization.md](references/ats-optimization.md) — ATS formatting rules
- [bullet-optimization.md](references/bullet-optimization.md) — tasks → accomplishments
- [multi-job-fit.md](references/multi-job-fit.md) — multi-JD comparison
- [pdf-compilation.md](references/pdf-compilation.md) — PDF generation
