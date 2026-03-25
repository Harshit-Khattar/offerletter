---
name: keywords
description: Extract the top ATS keywords from a job description to optimize your resume.
disable-model-invocation: true
---

# ATS Keyword Extraction

Single-output skill. Follow shared rules in CLAUDE.md.

## Setup

1. Get company name (from `$ARGUMENTS` or ask)
2. Get JD — user pastes it, or check existing `companies/<name>/job-description.txt`

## Process

1. Save JD to `companies/<name>/job-description.txt` if not already saved
2. Extract top 20 keywords in 3 categories: **Technical Skills**, **Soft Skills**, **Domain Terms**
3. Mark each as **Critical** (required/mentioned 2+), **Important** (preferred/mentioned once), or **Helpful** (implied)
4. Use exact phrasing from JD. If abbreviation and full term both appear (e.g., "ML" and "Machine Learning"), list both
5. Save to `companies/<name>/keywords.md` in table format with Priority and "In Your Resume?" columns
6. Tell user: ~60% keyword coverage is a good target. Suggest running `/offerletter:resume` next
