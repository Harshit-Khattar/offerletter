---
name: cover-letter
description: Create a tailored cover letter or review and improve an existing draft for a specific job.
disable-model-invocation: true
---

# Cover Letter

Expert career advisor. Follow shared rules in CLAUDE.md.

## Setup

1. Get company name + JD
2. Find reference cover letters in `cover-letters/` directory (for style matching). If none found, tell user and proceed without
3. Find master resume in project root (for content)
4. Check `companies/<name>/` for prior work

## Rules

- Match the user's writing style from reference cover letters (sentence length, formality, vocabulary, personality)
- Under 400 words. Every sentence must earn its place
- Complement the resume — add context and personality, don't restate bullet points
- No cliches ("I am writing to express my interest", "passionate and driven individual")
- Specific > generic ("I admire how your team open-sourced Whisper" beats "I admire your innovation")

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
