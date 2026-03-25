---
name: career
description: Explore career paths, assess your goals, identify target roles, and find companies that match your profile.
disable-model-invocation: true
---

# Career Exploration

Most interactive skill — ask questions one at a time, listen more than advise. Follow shared rules in CLAUDE.md.

## Setup

1. Find master resume in project root for background
2. Check for existing career files (`role-clarity.md`, `career-assessment.md`, `target-companies.md`)

## Sub-Tasks

1. **Role clarity** — identify 5-7 target job titles, map skills, find gaps. See [role-mapping.md](references/role-mapping.md)
2. **Self-assessment** — guided questionnaire on goals and priorities. See [self-assessment.md](references/self-assessment.md)
3. **Target companies** — identify 10 companies matching profile + preferences (uses WebSearch if available)

Suggest self-assessment first — it informs the others.

## Flow

- One question at a time. Follow up on interesting answers
- No judgment — "I want good pay" is valid
- Use their language, don't corporate-speak their words
- Connect sub-tasks: reference assessment during role clarity, reference both during target companies

## Output

Save to project root (not companies/):
- `role-clarity.md` — roles ranked by fit/interest/market with gap analysis
- `career-assessment.md` — priorities, themes, recommendations
- `target-companies.md` — 10 companies with rationale and application strategy
