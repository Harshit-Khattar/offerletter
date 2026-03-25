---
name: cover-letter
description: Create a tailored cover letter or review and improve an existing draft for a specific job.
disable-model-invocation: true
---

# Cover Letter

Expert career advisor. Follow shared rules in CLAUDE.md.

## Setup

1. Get company name + JD (user pastes or provides URL — if URL, use WebFetch; if blocked, ask user to paste)
2. **Create folder** `companies/<company-name>/` if it doesn't already exist (lowercase, hyphens for spaces)
3. **Save JD** to `companies/<company-name>/job-description.txt` if not already there
4. **Check company folder** for prior work — tailored resume, keywords, research, JD. Use all available context
5. Find reference cover letters in `cover-letters/` directory (for style matching). If none found, use the tailored resume from company folder (or master resume) for tone/content instead
6. Find resume for content — prefer `companies/<company-name>/` tailored resume if it exists, otherwise master resume in project root

## Rules

- **Never modify originals** — never edit reference cover letters. Always create new files in `companies/<company-name>/`
- Match the user's writing style from reference cover letters (sentence length, formality, vocabulary, personality)
- Under 400 words. Every sentence must earn its place
- Complement the resume — add context and personality, don't restate bullet points
- No cliches ("I am writing to express my interest", "passionate and driven individual")
- Specific > generic ("I admire how your team open-sourced Whisper" beats "I admire your innovation")
- **No em dashes (—)** — use commas, periods, or rewrite
- **Preserve format** — if reference is `.tex`, output `.tex`. If `.md`, output `.md`. For `.tex`: copy preamble verbatim, only change content

## Detection

- **Creation**: no draft in company folder → write new cover letter
- **Review**: user has existing draft → evaluate against [review-checklist.md](references/review-checklist.md) and suggest improvements

## Creation Flow

1. Read JD, resume, reference cover letters, any existing company research
2. Draft: strong opening hook → 1-2 body paragraphs connecting qualifications to role → company knowledge → confident closing
3. Present draft, get feedback, iterate until approved
4. Save to `companies/<name>/cover-letter.tex` (or `.md`), compile to PDF

## Review Flow

1. Read draft + JD + resume
2. Evaluate against [review-checklist.md](references/review-checklist.md), give structured feedback
3. Offer to revise. Iterate until approved, save
