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
4. Ask: **"What type of interview prep do you need?"**

## Sub-Tasks

Present this menu if user doesn't specify:

1. **Behavioral** — STAR-method questions on leadership, teamwork, conflict, adaptability. See [behavioral.md](references/behavioral.md)
2. **Technical** — role-specific technical questions (see below). See [technical.md](references/technical.md)
3. **Motivation** — "why this company/role?" + questions to ask interviewers. See [motivation.md](references/motivation.md)
4. **Informational interview** — networking conversation prep. See [informational-interview.md](references/informational-interview.md)

## Technical Sub-Task — Role-Aware

When user picks technical, ask what their role/focus is and tailor accordingly:

- **SWE / Full-Stack**: data structures, algorithms, system design, coding problems, API design
- **Data Scientist / Analyst**: statistics, SQL, A/B testing, ML fundamentals, case studies, data wrangling
- **ML / AI Engineer**: deep learning, model deployment, training pipelines, system design for ML, RAG
- **DevOps / SRE**: infrastructure, CI/CD, monitoring, incident response, system reliability
- **Product Manager**: product sense, estimation, prioritization frameworks, metrics, stakeholder scenarios
- **Any other role**: ask user about focus areas and generate relevant questions

Generate 8-10 questions mixing fundamentals, problem-solving scenarios, and practical application. Calibrate for entry-level/new grad.

## Web Research + Own Knowledge

**Always generate questions from your own knowledge first.** Then search online for company-specific questions:
- `"<company>" interview questions site:reddit.com`
- `"<company>" "<role>" interview experience site:glassdoor.com`
- `"<company>" interview process`
- `"<company>" "<role>" technical interview`

**Combine both sources.** Present your own questions AND anything found online. Label online findings: "Found online on [source]: ..." If WebSearch unavailable, your own questions are the primary output — don't skip generating just because search failed.

## Flow

1. Generate questions from own knowledge + web research
2. Present with answer strategies for each
3. Offer coaching: user picks a question → gives answer → you give feedback
4. Save to `companies/<name>/interview-prep.md` (append if file exists)

## Key Rules

- Infer experience level from resume (graduation dates, years of work) and calibrate question difficulty accordingly — a fresh grad gets fundamentals, someone with 4 years gets deeper system design
- Be specific — "Explain how you'd design a URL shortener" not "Tell me about system design"
- Interactive — present questions, then coach. Don't dump everything at once
