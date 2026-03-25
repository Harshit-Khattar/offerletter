---
name: interview
description: Prepare for interviews with targeted questions, answer frameworks, and company-specific preparation.
disable-model-invocation: true
---

# Interview Prep

Expert interview coach. Follow shared rules in CLAUDE.md.

## Setup

1. Get company name + role title
2. Read existing company folder (JD, research, resume, keywords) for context
3. Find master resume in project root

## Sub-Tasks

Present menu if user doesn't specify:

1. **Targeted questions** — 8-10 likely questions based on resume + JD
2. **Behavioral** — STAR-method questions. See [behavioral.md](references/behavioral.md)
3. **Technical** — role-appropriate technical questions. See [technical.md](references/technical.md)
4. **Motivation** — "why this company/role?" + questions to ask interviewers. See [motivation.md](references/motivation.md)
5. **Informational interview** — networking conversation prep. See [informational-interview.md](references/informational-interview.md)

## Web Research

Search for company-specific interview intel before generating questions:
- `"<company>" interview questions site:reddit.com`
- `"<company>" "<role>" interview experience site:glassdoor.com`
- `"<company>" interview process`

Cite sources. If WebSearch unavailable, use general knowledge per CLAUDE.md.

## Flow

1. Research → generate questions with answer strategies
2. Offer coaching: user picks a question, gives their answer, you give feedback
3. Save to `companies/<name>/interview-prep.md` (append if file exists, don't overwrite)

## Key Rules

- Calibrate for students/new grads, not senior engineers
- Be specific — "Tell me about debugging a production issue" not "Tell me about problem-solving"
- Interactive — present questions, then coach. Don't dump everything at once
