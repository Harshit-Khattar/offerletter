---
name: keywords
description: Extract the top ATS keywords from a job description to optimize your resume.
disable-model-invocation: true
---

# ATS Keyword Extraction

Extract the most important keywords from a job description that a student should include in their resume to pass ATS (Applicant Tracking System) filters.

## Getting Started

When the user invokes this skill:

1. **Ask for the company name** if not provided via `$ARGUMENTS`
2. **Ask for the job description** — user pastes it directly
3. If a company folder already exists at `companies/<company-name>/`, check for an existing `job-description.txt` and use it if the user confirms

## Process

### Step 1: Save the Job Description

Create the company folder if it doesn't exist (lowercase, hyphens for spaces):
- `companies/<company-name>/job-description.txt`

### Step 2: Extract Keywords

Analyze the job description and extract the top 20 keywords, organized into three categories:

**Technical Skills** — programming languages, frameworks, tools, platforms, methodologies
- Example: Python, TensorFlow, AWS, Agile, Docker, SQL, React

**Soft Skills** — interpersonal and professional competencies
- Example: Leadership, Communication, Problem-solving, Collaboration, Mentorship

**Domain/Industry Terms** — industry-specific vocabulary, methodologies, certifications
- Example: Machine Learning, CI/CD, RESTful APIs, HIPAA compliance, A/B testing

### Step 3: Prioritize

For each keyword, indicate priority:
- **Critical** — appears in "Required" section or mentioned 2+ times
- **Important** — appears in "Preferred" section or mentioned once
- **Helpful** — implied by responsibilities or context

### Step 4: Output

Save the analysis to `companies/<company-name>/keywords.md` in this format:

```markdown
# Keywords: [Company Name] — [Role Title]

## Technical Skills
| Keyword | Priority | In Your Resume? |
|---------|----------|----------------|
| Python | Critical | Check your resume |
| TensorFlow | Important | Check your resume |
...

## Soft Skills
| Keyword | Priority | In Your Resume? |
|---------|----------|----------------|
...

## Domain Terms
| Keyword | Priority | In Your Resume? |
|---------|----------|----------------|
...

## Summary
- Total keywords: X
- Critical: X | Important: X | Helpful: X
- Target: Include ~60% of these keywords naturally in your tailored resume

## Suggested Next Step
Run `/offerletter:resume` to tailor your resume using these keywords.
```

### Step 5: Confirm

Tell the user:
- Where the file was saved
- How many keywords were found in each category
- Remind them that ~60% keyword coverage is a good target (don't force all 20)

## Rules

- Only include keywords that accurately describe real skills or qualifications — never suggest the user claim skills they don't have
- Use the exact phrasing from the JD (ATS matches exact strings)
- If a keyword appears as both an abbreviation and full term in the JD (e.g., "ML" and "Machine Learning"), list both
- This is a single-output skill — no back-and-forth needed. Extract, save, confirm.
