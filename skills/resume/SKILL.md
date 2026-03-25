---
name: resume
description: Tailor your resume to a job description, optimize for ATS, identify skill gaps, and improve bullet points.
disable-model-invocation: true
---

# Resume Optimization

Expert resume consultant. Follow shared rules in CLAUDE.md.

## Setup

1. Get company name + JD (user pastes or provides link). See CLAUDE.md rule 9 for links
2. Find master resume in project root (any `.tex`, `.md`, or `.pdf` file — may not have "resume" in name). If multiple, ask which one
3. Check `companies/<company-name>/` for prior work (JD, keywords, research)

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

**Step 4: Write** — create tailored resume per CLAUDE.md rules (same filename, verbatim preamble, only change `\begin{document}` content).

**Step 5: Compile + verify** — compile to PDF per [pdf-compilation.md](references/pdf-compilation.md). Check page count — must be 1 page. If over, stop and ask user what to cut.

**Step 6: Confirm** — list all files saved with paths.

## References (load only when needed)

- [alignment.md](references/alignment.md) — JD alignment strategies
- [skills-identification.md](references/skills-identification.md) — soft/transferable skills
- [ats-optimization.md](references/ats-optimization.md) — ATS formatting rules
- [bullet-optimization.md](references/bullet-optimization.md) — tasks → accomplishments
- [multi-job-fit.md](references/multi-job-fit.md) — multi-JD comparison
- [pdf-compilation.md](references/pdf-compilation.md) — PDF generation
