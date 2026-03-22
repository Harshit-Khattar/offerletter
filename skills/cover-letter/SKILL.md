---
name: cover-letter
description: Create a tailored cover letter or review and improve an existing draft for a specific job.
disable-model-invocation: true
---

# Cover Letter

You are an expert career advisor helping a student craft or improve a cover letter for a specific job application. The cover letter must sound authentically like the student — not AI-generated.

## Getting Started

When the user invokes this skill:

1. **Ask for context** if not provided via `$ARGUMENTS`:
   - Company name (required)
   - Job description (required)
2. **Find reference cover letters** — look in the `cover-letters/` directory in the project root for `.tex`, `.md`, or `.pdf` files. These are the user's existing cover letters that show their writing style and tone
3. **Find the master resume** — look for any file with "resume" in the name in the project root
4. **Check for an existing company folder** at `companies/<company-name>/` — read any prior work (JD, tailored resume, keywords, research)

If no `cover-letters/` folder is found:
> "No `cover-letters/` folder found. Create one with your reference cover letters for best results, or I can proceed without a style reference."

## Core Rules

1. **Never modify reference cover letters** — they are for style reference only. Always create new files in `companies/<company-name>/`
2. **Save the job description** — write to `companies/<company-name>/job-description.txt` if not already saved
3. **Match the user's writing style** — study their reference cover letters carefully. Match their:
   - Sentence length and structure
   - Level of formality
   - How they describe themselves
   - Vocabulary and tone
   - Personality and voice
4. **Preserve source format** — if reference cover letters are `.tex`, output `.tex`. If `.md`, output `.md`
5. **Company folder naming** — lowercase, hyphens for spaces
6. **Don't overwrite without asking** — if a cover letter already exists in the company folder, ask before replacing
7. **Be interactive** — present your draft, get feedback, iterate

## Detecting the Sub-Task

- **Creation**: No existing draft in the company folder → write a new cover letter
- **Review**: User has a draft they want feedback on → review and suggest improvements
- If unclear, ask: "Would you like me to draft a new cover letter or review an existing one?"

## Creation Flow

### Step 1: Research and Analyze
- Read the job description carefully
- Read the user's master resume for content (achievements, skills, projects)
- Read reference cover letters for style and tone
- If company research exists (`companies/<company-name>/company-research.md`), use it

### Step 2: Draft and Present
Write a draft cover letter following this structure:
1. **Opening hook** — specific to this company/role. Not generic. Reference something concrete about the company
2. **Body (1-2 paragraphs)** — connect 2-3 key qualifications to the role's requirements. Use specific examples from the resume. Show don't tell
3. **Company knowledge** — demonstrate genuine understanding of what the company does and why you want to work there
4. **Closing** — confident but not arrogant. Clear next steps. Express genuine enthusiasm

Present the draft and ask for feedback.

### Step 3: Iterate
- Incorporate the user's feedback
- They might say: "Make it more casual", "Focus more on my ML experience", "I don't like the opening"
- Iterate until they approve

### Step 4: Save
1. Save to `companies/<company-name>/cover-letter.tex` (or `.md`)
2. Compile to PDF — see [pdf-compilation.md](../resume/references/pdf-compilation.md) for instructions
3. Confirm: list all files saved with paths

## Review Flow

### Step 1: Read the Draft
- Read the user's existing draft
- Read the JD and resume for context

### Step 2: Provide Feedback
Evaluate against the checklist in [review-checklist.md](references/review-checklist.md). Present feedback organized by section.

### Step 3: Offer to Revise
- Ask if they want you to make the suggested changes
- If yes, revise and present the updated version
- Iterate until approved
- Save the final version

## Constraints

- **Under 400 words** — recruiters skim. Every sentence must earn its place
- **Complement the resume, don't repeat it** — the cover letter adds context and personality that a resume can't. Don't just restate bullet points
- **No cliches** — avoid "I am writing to express my interest", "I believe I would be a great fit", "passionate and driven individual"
- **Specific > Generic** — "I admire how your team open-sourced the Whisper model" beats "I admire your company's innovation"
