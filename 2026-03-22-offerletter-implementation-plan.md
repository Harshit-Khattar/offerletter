# Offerletter Plugin Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build the `offerletter` Claude Code plugin — a skills-only career toolkit for students with 6 slash commands for resume tailoring, cover letters, interview prep, career exploration, company research, and keyword extraction.

**Architecture:** Pure skills-based Claude Code plugin. Each feature is a SKILL.md file with supporting reference documents in a `references/` subdirectory. No hooks, MCP servers, or custom agents. Templates directory provides fallback ATS-friendly LaTeX resume templates. The plugin acts as its own marketplace for distribution.

**Tech Stack:** Markdown (SKILL.md files), YAML frontmatter, JSON (plugin.json, marketplace.json), LaTeX (resume templates)

**Spec:** `2026-03-22-offerletter-plugin-design.md` in the project root.

---

## File Structure

```
offerletter/
├── .claude-plugin/
│   ├── plugin.json                              ← plugin manifest
│   └── marketplace.json                         ← marketplace catalog
├── skills/
│   ├── resume/
│   │   ├── SKILL.md                             ← /offerletter:resume
│   │   └── references/
│   │       ├── alignment.md                     ← JD alignment prompts
│   │       ├── skills-identification.md         ← soft/transferable skills
│   │       ├── ats-optimization.md              ← ATS formatting rules
│   │       ├── bullet-optimization.md           ← tasks→accomplishments
│   │       ├── multi-job-fit.md                 ← multi-JD comparison
│   │       └── pdf-compilation.md               ← cross-platform PDF instructions
│   ├── keywords/
│   │   └── SKILL.md                             ← /offerletter:keywords
│   ├── cover-letter/
│   │   ├── SKILL.md                             ← /offerletter:cover-letter
│   │   └── references/
│   │       └── review-checklist.md              ← review criteria
│   ├── interview/
│   │   ├── SKILL.md                             ← /offerletter:interview
│   │   └── references/
│   │       ├── behavioral.md                    ← STAR framework
│   │       ├── technical.md                     ← technical question logic
│   │       ├── motivation.md                    ← "why this company" prep
│   │       └── informational-interview.md       ← networking questions
│   ├── company-research/
│   │   └── SKILL.md                             ← /offerletter:company-research
│   └── career/
│       ├── SKILL.md                             ← /offerletter:career
│       └── references/
│           ├── self-assessment.md               ← career goals questionnaire
│           └── role-mapping.md                  ← skills-to-roles mapping
├── templates/
│   ├── ats-resume-clean.tex                     ← minimal single-column
│   ├── ats-resume-modern.tex                    ← modern with accent colors
│   └── ats-resume-academic.tex                  ← academic/research focused
├── CLAUDE.md                                    ← project instructions
├── README.md                                    ← marketplace/GitHub description
├── LICENSE                                      ← MIT license
└── CHANGELOG.md                                 ← version history
```

---

## Task 1: Plugin Scaffold — Manifest, Marketplace, and Directory Structure

**Files:**
- Create: `.claude-plugin/plugin.json`
- Create: `.claude-plugin/marketplace.json`
- Create: `LICENSE`
- Create: `CHANGELOG.md`
- Modify: `CLAUDE.md`
- Create all empty skill directories and placeholder SKILL.md files
- Create empty `templates/` directory

- [ ] **Step 1: Initialize git repository**

```bash
cd /Users/harshitkhattar/Desktop/offerletter
git init
```

- [ ] **Step 2: Create `.claude-plugin/plugin.json`**

```json
{
  "name": "offerletter",
  "description": "AI-powered career toolkit for students — tailor resumes, craft cover letters, prep for interviews, and research companies.",
  "version": "1.0.0",
  "author": {
    "name": "Harshit Khattar"
  },
  "homepage": "https://github.com/Harshit-Khattar/offerletter",
  "repository": "https://github.com/Harshit-Khattar/offerletter",
  "license": "MIT",
  "keywords": ["resume", "interview", "career", "job-search", "cover-letter", "students"]
}
```

- [ ] **Step 3: Create `.claude-plugin/marketplace.json`**

```json
{
  "name": "offerletter-marketplace",
  "owner": {
    "name": "Harshit Khattar",
    "email": "harshitkhattar@example.com"
  },
  "plugins": [
    {
      "name": "offerletter",
      "source": "./",
      "description": "Tailor resumes, craft cover letters, prep for interviews, and research companies.",
      "version": "1.0.0"
    }
  ]
}
```

Note: Replace `harshitkhattar@example.com` with real email before publishing.

- [ ] **Step 4: Create MIT LICENSE file**

Standard MIT license with "2026 Harshit Khattar".

- [ ] **Step 5: Create CHANGELOG.md**

```markdown
# Changelog

## [1.0.0] - 2026-03-22

### Added
- `/offerletter:resume` — resume tailoring, ATS optimization, gap analysis, multi-job fit
- `/offerletter:keywords` — ATS keyword extraction from job descriptions
- `/offerletter:cover-letter` — cover letter creation and review
- `/offerletter:interview` — interview prep with web research
- `/offerletter:company-research` — company research and dossier generation
- `/offerletter:career` — career exploration, self-assessment, target companies
- 3 built-in ATS-friendly LaTeX resume templates
```

- [ ] **Step 6: Update CLAUDE.md with project instructions**

Update the existing `CLAUDE.md` with actual project description, setup instructions, and development guidelines relevant to the plugin.

- [ ] **Step 7: Create all skill directories with placeholder SKILL.md files**

Create the full directory tree:
```bash
mkdir -p skills/resume/references
mkdir -p skills/keywords
mkdir -p skills/cover-letter/references
mkdir -p skills/interview/references
mkdir -p skills/company-research
mkdir -p skills/career/references
mkdir -p templates
```

Create a minimal placeholder SKILL.md in each skill directory with just the frontmatter (name, description, disable-model-invocation). The full content will be written in subsequent tasks. This ensures the plugin structure validates immediately.

- [ ] **Step 8: Create .gitignore**

```
.superpowers/
.DS_Store
*.aux
*.log
*.out
*.synctex.gz
```

- [ ] **Step 9: Create README.md**

Write a marketplace-ready README covering:
- What the plugin does (one paragraph)
- Available commands (table of 6 skills with descriptions)
- Expected folder structure (user's working directory convention)
- Installation instructions (`/plugin marketplace add`, `/plugin install`)
- Supported file formats (.tex, .md, .pdf fallback)
- PDF compilation (auto-detects/installs tectonic)

- [ ] **Step 10: Validate plugin structure**

Run: `claude plugin validate .`
Expected: No errors.

- [ ] **Step 11: Test plugin loads**

Run: `claude --plugin-dir .`
Verify all 6 skills appear with `/help`.
Test: `/offerletter:resume` responds (even if just placeholder content).

- [ ] **Step 12: Commit scaffold**

```bash
git add .claude-plugin/ skills/ templates/ CLAUDE.md README.md LICENSE CHANGELOG.md .gitignore
git commit -m "feat: scaffold offerletter plugin with manifest, marketplace, and skill placeholders"
```

---

## Task 2: Resume Skill — SKILL.md and All Reference Files

**Files:**
- Create: `skills/resume/SKILL.md` (full content, replacing placeholder)
- Create: `skills/resume/references/alignment.md`
- Create: `skills/resume/references/skills-identification.md`
- Create: `skills/resume/references/ats-optimization.md`
- Create: `skills/resume/references/bullet-optimization.md`
- Create: `skills/resume/references/multi-job-fit.md`
- Create: `skills/resume/references/pdf-compilation.md`

**Context:** This is the largest skill. The SKILL.md is the main orchestrator that handles all resume sub-tasks. Reference files contain detailed prompts and rules that Claude loads when needed for specific sub-tasks. Refer to the spec's "Skill 1" section and "Core Rules" section for requirements.

- [ ] **Step 1: Write `skills/resume/SKILL.md`**

The SKILL.md must include:
- Frontmatter: `name: resume`, `description`, `disable-model-invocation: true`
- `$ARGUMENTS` placeholder for company name and job description
- All 11 core rules embedded (never modify master, save JD, match writing style, etc.)
- Sub-task detection logic (how Claude determines which sub-task to perform)
- Full interaction flow (read master resume → analyze → discuss → write → compile PDF → confirm)
- File discovery instructions (find resume in root by name pattern, supported formats)
- Company folder creation instructions (lowercase, hyphens for spaces)
- References to supporting files in `references/` for detailed sub-task prompts
- Instructions to read reference files only when the specific sub-task is needed (progressive disclosure)

- [ ] **Step 2: Write `skills/resume/references/alignment.md`**

Detailed prompts for resume-JD alignment:
- How to compare resume content against job description requirements
- Keyword matching and natural integration strategy
- Section-by-section analysis approach (skills, experience, projects, education)
- How to reorder and emphasize content based on JD priorities
- Specific examples of before/after bullet rewrites

Source: Spec prompts 1.1 (Resume-Job Description Alignment), 1.3 (Skills Translation), 1.4 (Technical Skills Optimization), 1.5 (Project Description Enhancement)

- [ ] **Step 3: Write `skills/resume/references/skills-identification.md`**

Detailed prompts for skills extraction:
- How to extract explicit soft skills from a JD
- How to identify implied/transferable skills
- How to categorize skills by importance
- How to demonstrate skills through academic/project contexts
- Mapping between academic experience and industry language

Source: Spec prompts 1.2 (Skills Identification), 1.3 (Skills Translation and Highlighting)

- [ ] **Step 4: Write `skills/resume/references/ats-optimization.md`**

ATS formatting rules and guidelines:
- Section organization hierarchy (Contact → Summary → Skills → Experience → Projects → Education)
- Font and formatting rules for ATS parsing
- Keyword density guidelines (target ~60% of top keywords)
- Header optimization rules
- Common ATS-breaking formatting to avoid
- How to test ATS compatibility

Source: Spec prompt 1.6 (Resume Format and ATS Optimization), 1.11 (ATS Keywords)

- [ ] **Step 5: Write `skills/resume/references/bullet-optimization.md`**

Bullet point improvement rules:
- Tasks vs accomplishments identification criteria
- STAR method for bullet points (Situation, Task, Action, Result)
- Quantification strategies (how to add numbers when user doesn't have them)
- Action verb list organized by skill category
- Redundancy detection rules (same skill demonstrated multiple times)
- Before/after examples for each transformation type

Source: Spec prompts 1.9 (Resume Redundancy), 1.10 (Tasks vs Accomplishments)

- [ ] **Step 6: Write `skills/resume/references/multi-job-fit.md`**

Multi-job comparison logic:
- How to rank positions from strongest to weakest fit
- Scoring criteria (technical match, experience level, qualifications)
- Strengths and gaps analysis per position
- Strategic recommendations for which roles to prioritize
- Output format for the comparison report

Source: Spec prompt 1.8 (Multi-Job Fit Analysis and Ranking)

- [ ] **Step 7: Write `skills/resume/references/pdf-compilation.md`**

Cross-platform PDF generation instructions:
- Complete decision tree (check pdflatex → xelatex → tectonic → install)
- OS detection commands (macOS, Windows, Linux)
- Package manager detection and install commands for each OS
- Tectonic installation fallback (curl binary from GitHub releases)
- .md to .tex conversion instructions (for markdown resumes)
- Build artifact cleanup (.aux, .log, .out removal)
- Error handling and graceful fallback messaging
- Template selection logic (when to use built-in templates)

Source: Spec's "PDF Compilation Strategy" section

- [ ] **Step 8: Test resume skill loads**

Run: `claude --plugin-dir .`
Test: `/offerletter:resume` — verify Claude receives the skill content and responds appropriately.

- [ ] **Step 9: Commit resume skill**

```bash
git add skills/resume/
git commit -m "feat: add resume skill with alignment, ATS, bullet optimization, multi-job fit, and PDF compilation references"
```

---

## Task 3: Keywords Skill

**Files:**
- Create: `skills/keywords/SKILL.md` (full content, replacing placeholder)

**Context:** Simplest skill — single output, no back-and-forth. Refer to spec's "Skill 2" section.

- [ ] **Step 1: Write `skills/keywords/SKILL.md`**

The SKILL.md must include:
- Frontmatter: `name: keywords`, `description`, `disable-model-invocation: true`
- `$ARGUMENTS` placeholder for company name
- Instructions to read the job description (from user input or existing `companies/<name>/job-description.txt`)
- Extract top 20 keywords categorized by type: technical skills, soft skills, domain/industry terms
- Include keyword frequency/priority indicators
- Save output to `companies/<company-name>/keywords.md`
- Create company folder if it doesn't exist (lowercase, hyphens for spaces)
- Save job description to `companies/<company-name>/job-description.txt` if not already saved
- Note that ~60% keyword coverage is a good target for resume optimization

- [ ] **Step 2: Test keywords skill**

Run: `claude --plugin-dir .`
Test: `/offerletter:keywords` with a sample job description.

- [ ] **Step 3: Commit keywords skill**

```bash
git add skills/keywords/
git commit -m "feat: add keywords skill for ATS keyword extraction"
```

---

## Task 4: Cover Letter Skill

**Files:**
- Create: `skills/cover-letter/SKILL.md` (full content, replacing placeholder)
- Create: `skills/cover-letter/references/review-checklist.md`

**Context:** Refer to spec's "Skill 3" section. Key behavior: must match user's writing style from reference cover letters.

- [ ] **Step 1: Write `skills/cover-letter/SKILL.md`**

The SKILL.md must include:
- Frontmatter: `name: cover-letter`, `description`, `disable-model-invocation: true`
- `$ARGUMENTS` placeholder for company name
- Core rules embedded (never modify master, match writing style, etc.)
- File discovery: read all files in `cover-letters/` directory for style reference
- Also read master resume for content reference
- Sub-task detection: creation vs review (based on whether a draft exists in company folder)
- Creation flow: read references → draft → discuss → save
- Review flow: read existing draft → provide feedback on 7 criteria → revise → save
- Cover letter structure guidance: strong hook, connect experience to needs, 2-3 key qualifications, company knowledge, confident close
- Under 400 words
- Professional but personable tone — must NOT sound AI-generated
- Save to `companies/<company-name>/cover-letter.tex` (or .md matching user's format)
- Compile to PDF using same strategy as resume skill (reference `skills/resume/references/pdf-compilation.md`)

- [ ] **Step 2: Write `skills/cover-letter/references/review-checklist.md`**

Detailed review criteria:
- Opening paragraph: Does it hook? Is it specific to this company/role?
- Body paragraphs: Flow, persuasiveness, concrete examples with quantified achievements
- Company knowledge: Does it demonstrate genuine research?
- Closing: Strength of call-to-action, confidence without arrogance
- Tone: Professional yet personable, authentic voice
- Length: Under 400 words
- Grammar, style, readability
- Complementary to resume (not repetitive)

Source: Spec prompts 2.1 (Cover Letter Creation), 2.2 (Cover Letter Review)

- [ ] **Step 3: Test cover letter skill**

Run: `claude --plugin-dir .`
Test: `/offerletter:cover-letter` — verify it responds and asks for context.

- [ ] **Step 4: Commit cover letter skill**

```bash
git add skills/cover-letter/
git commit -m "feat: add cover letter skill with creation, review, and style matching"
```

---

## Task 5: Interview Skill

**Files:**
- Create: `skills/interview/SKILL.md` (full content, replacing placeholder)
- Create: `skills/interview/references/behavioral.md`
- Create: `skills/interview/references/technical.md`
- Create: `skills/interview/references/motivation.md`
- Create: `skills/interview/references/informational-interview.md`

**Context:** Second largest skill. Uses web research. Refer to spec's "Skill 4" section.

- [ ] **Step 1: Write `skills/interview/SKILL.md`**

The SKILL.md must include:
- Frontmatter: `name: interview`, `description`, `disable-model-invocation: true`
- `$ARGUMENTS` placeholder for company name and optional sub-task
- Core rules embedded
- Read existing company folder for context (JD, research, tailored resume)
- Sub-task menu: targeted questions, behavioral, technical, motivation, questions to ask, informational interview
- Web research instructions: use WebSearch with specific query patterns (`"<company>" interview questions site:reddit.com`, etc.)
- WebSearch availability check: if not available, inform user and proceed with general knowledge
- Always cite sources when using web results
- Interactive flow: present questions → user can ask for answer coaching → discuss
- Save to `companies/<company-name>/interview-prep.md`
- Append to existing interview-prep.md if it exists (don't overwrite previous prep)
- References to sub-task-specific reference files

- [ ] **Step 2: Write `skills/interview/references/behavioral.md`**

STAR framework and behavioral question guide:
- What STAR method is and how to structure answers
- 10 common behavioral questions for CS/DS/AI roles
- The underlying competency each question assesses
- Tips for relating academic/research experience to professional scenarios
- How to quantify impact in responses
- Common follow-up questions for each category
- Categories: leadership, problem-solving, teamwork, conflict resolution, adaptability

Source: Spec prompt 3.2 (Behavioral Interview Questions)

- [ ] **Step 3: Write `skills/interview/references/technical.md`**

Technical question generation rules:
- How to generate questions appropriate for entry-level roles
- Question complexity calibration (15-20 minute discussion scope)
- Categories: fundamental concepts, problem-solving approach, coding component, system design
- Role-specific question templates (Software Engineer, Data Scientist, AI Engineer, ML Engineer)
- Expected approach and key points to cover for each question type
- Connection to practical work scenarios

Source: Spec prompt 3.3 (Technical Interview Questions)

- [ ] **Step 4: Write `skills/interview/references/motivation.md`**

Company-specific motivation answer frameworks:
- "Why do you want to work at [Company]?" framework
- "Why this specific role?" framework
- "How do you see yourself contributing?" framework
- "What attracts you to our industry/product?" framework
- "Where do you see yourself growing?" framework
- How to connect personal background to company needs authentically
- How to demonstrate genuine research and interest

Also covers "Questions to Ask Interviewers":
- 10-12 categorized questions (technical/role, team/culture, growth, strategy/vision)
- How each question demonstrates engagement and knowledge
- Questions to avoid

Source: Spec prompts 3.4 (Company-Specific Motivation), 3.5 (Questions to Ask Interviewers)

- [ ] **Step 5: Write `skills/interview/references/informational-interview.md`**

Networking and informational interview preparation:
- How to generate 5-6 strategic questions based on target role, background, interests, and context
- Question progression: broad industry insights → specific role details
- Required categories: daily responsibilities, career development, growth opportunities
- Strategic purpose explanation for each question type
- Appropriate question calibration based on relationship context (alumni, LinkedIn, conference, etc.)
- Networking-focused closing question that opens doors

Source: Spec prompt 3.6 (Strategic Informational Interview Questions)

- [ ] **Step 6: Test interview skill**

Run: `claude --plugin-dir .`
Test: `/offerletter:interview` — verify sub-task menu and web research instructions.

- [ ] **Step 7: Commit interview skill**

```bash
git add skills/interview/
git commit -m "feat: add interview skill with behavioral, technical, motivation, and informational references"
```

---

## Task 6: Company Research Skill

**Files:**
- Create: `skills/company-research/SKILL.md` (full content, replacing placeholder)

**Context:** Single-output skill with web research. Refer to spec's "Skill 5" section.

- [ ] **Step 1: Write `skills/company-research/SKILL.md`**

The SKILL.md must include:
- Frontmatter: `name: company-research`, `description`, `disable-model-invocation: true`
- `$ARGUMENTS` placeholder for company name
- Web research instructions with specific search queries:
  - Company overview and mission
  - Recent news and developments
  - Company culture (Glassdoor, Reddit)
  - Tech stack and engineering blog
  - Interview process and tips
  - Key people and leadership
- WebSearch availability check with graceful fallback
- Structured output format with clear sections
- Save to `companies/<company-name>/company-research.md`
- Create company folder if it doesn't exist
- Cite all sources with URLs

- [ ] **Step 2: Test company research skill**

Run: `claude --plugin-dir .`
Test: `/offerletter:company-research Google` — verify it attempts research.

- [ ] **Step 3: Commit company research skill**

```bash
git add skills/company-research/
git commit -m "feat: add company research skill with web search and structured dossier output"
```

---

## Task 7: Career Skill

**Files:**
- Create: `skills/career/SKILL.md` (full content, replacing placeholder)
- Create: `skills/career/references/self-assessment.md`
- Create: `skills/career/references/role-mapping.md`

**Context:** Most interactive skill. Refer to spec's "Skill 6" section.

- [ ] **Step 1: Write `skills/career/SKILL.md`**

The SKILL.md must include:
- Frontmatter: `name: career`, `description`, `disable-model-invocation: true`
- `$ARGUMENTS` placeholder for optional sub-task specification
- Sub-task menu: role clarity, self-assessment, target companies
- Interactive approach: ask questions one at a time, build understanding
- Read master resume for background context
- Role clarity flow: analyze background → identify 5-7 job titles → map skills → find gaps → recommend strategy
- Self-assessment flow: guided questionnaire → synthesize answers → save results
- Target companies flow: analyze goals + skills + preferences → identify 10 companies → provide rationale and strategy
- Output saved to project root (not companies/ folder):
  - `role-clarity.md`
  - `career-assessment.md`
  - `target-companies.md`
- References to sub-task-specific reference files

- [ ] **Step 2: Write `skills/career/references/self-assessment.md`**

Structured career goals questionnaire:
- Technical interests and preferred working styles
- Industry preferences and company culture fit
- Short-term and long-term career aspirations
- Work-life balance and location preferences
- Learning and growth priorities
- Impact and mission alignment
- Compensation and benefits priorities
- Risk tolerance: startup vs established company
- Format as systematic self-assessment with clear sections

Source: Spec prompt 4.2 (Career Goals Self-Assessment)

- [ ] **Step 3: Write `skills/career/references/role-mapping.md`**

Skills-to-roles mapping logic:
- How to identify target job titles from a background summary
- Key differences between similar roles (e.g., Data Scientist vs ML Engineer vs AI Researcher)
- Skills gap analysis framework
- Entry-level vs advanced position mapping
- Job search strategy recommendations by role type
- Industry/company size/location preference integration

Source: Spec prompts 4.1 (Role Clarity), 4.3 (Target Company Identification)

- [ ] **Step 4: Test career skill**

Run: `claude --plugin-dir .`
Test: `/offerletter:career` — verify sub-task menu and interactive approach.

- [ ] **Step 5: Commit career skill**

```bash
git add skills/career/
git commit -m "feat: add career skill with self-assessment questionnaire and role mapping"
```

---

## Task 8: LaTeX Resume Templates

**Files:**
- Create: `templates/ats-resume-clean.tex`
- Create: `templates/ats-resume-modern.tex`
- Create: `templates/ats-resume-academic.tex`

**Context:** These are fallback templates for users who only have a PDF or want a fresh format. They must be ATS-parsable, well-structured, and easy for Claude to populate with content. Use only standard LaTeX packages that tectonic/pdflatex can handle.

- [ ] **Step 1: Write `templates/ats-resume-clean.tex`**

Minimal single-column ATS-friendly template:
- Clean, simple layout with no columns or tables
- Standard sections: Contact Info, Summary, Skills, Experience, Projects, Education
- Uses only `article` document class with basic packages (`geometry`, `enumitem`, `hyperref`, `titlesec`)
- Placeholder content with clear `% REPLACE:` comments showing where to insert user data
- ATS-safe: no images, no text boxes, no fancy formatting
- Compiles with both pdflatex and tectonic

- [ ] **Step 2: Write `templates/ats-resume-modern.tex`**

Modern template with subtle visual flair:
- Single-column with accent color for section headers
- Slightly more visual than clean template but still ATS-parsable
- Uses `xcolor` for accent colors
- Subtle horizontal rules between sections
- Same standard sections as clean template
- Compiles with both pdflatex and tectonic

- [ ] **Step 3: Write `templates/ats-resume-academic.tex`**

Academic/research-focused template:
- Includes sections for: Publications, Research Experience, Teaching, Awards
- Standard sections plus academic-specific ones
- Citation-friendly formatting
- Compiles with both pdflatex and tectonic

- [ ] **Step 4: Test template compilation**

Compile each template to verify no errors:
```bash
cd templates
pdflatex ats-resume-clean.tex    # or tectonic ats-resume-clean.tex
pdflatex ats-resume-modern.tex
pdflatex ats-resume-academic.tex
```
Clean up build artifacts after testing.

- [ ] **Step 5: Commit templates**

```bash
git add templates/
git commit -m "feat: add 3 ATS-friendly LaTeX resume templates (clean, modern, academic)"
```

---

## Task 9: Final Validation and Polish

**Files:**
- Modify: `CLAUDE.md` (final polish)
- Modify: `README.md` (final polish if needed)

- [ ] **Step 1: Validate full plugin structure**

Run: `claude plugin validate .`
Expected: No errors, no warnings.

- [ ] **Step 2: Load plugin and verify all 6 skills**

Run: `claude --plugin-dir .`
Run: `/help`
Verify all 6 skills appear:
- `/offerletter:resume`
- `/offerletter:keywords`
- `/offerletter:cover-letter`
- `/offerletter:interview`
- `/offerletter:company-research`
- `/offerletter:career`

- [ ] **Step 3: Smoke test each skill**

Invoke each skill briefly to verify it loads and responds:
1. `/offerletter:resume` — should ask for job description
2. `/offerletter:keywords` — should ask for job description
3. `/offerletter:cover-letter` — should ask for company and JD
4. `/offerletter:interview` — should show sub-task menu
5. `/offerletter:company-research Google` — should attempt research
6. `/offerletter:career` — should show sub-task menu

- [ ] **Step 4: Verify README is marketplace-ready**

Check README includes:
- Clear description
- Command table
- Folder convention diagram
- Installation instructions
- File format support
- PDF compilation info

- [ ] **Step 5: Final commit**

```bash
git add -A
git commit -m "feat: finalize offerletter plugin v1.0.0 — ready for marketplace"
```

- [ ] **Step 6: Tag release**

```bash
git tag v1.0.0
```

---

## Task Order and Dependencies

| Task | Name | Depends On | Estimated Complexity |
|------|------|------------|---------------------|
| 1 | Plugin scaffold | None | Light |
| 2 | Resume skill | Task 1 | Heavy (largest skill, 7 files) |
| 3 | Keywords skill | Task 1 | Light (1 file) |
| 4 | Cover letter skill | Task 1, Task 2 (shares pdf-compilation.md reference) | Medium |
| 5 | Interview skill | Task 1 | Heavy (5 files, web research) |
| 6 | Company research skill | Task 1 | Light (1 file) |
| 7 | Career skill | Task 1 | Medium (3 files) |
| 8 | LaTeX templates | Task 1 | Medium (3 LaTeX files, need compilation testing) |
| 9 | Final validation | Tasks 1-8 | Light |

Tasks 2-8 can be worked on in parallel after Task 1 is complete (except Task 4 references Task 2's pdf-compilation.md). Task 9 must be last.
