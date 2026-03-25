# Offerletter

AI-powered career toolkit for students — tailor resumes, craft cover letters, prep for interviews, and research companies. A Claude Code plugin that works in the Claude Desktop app.

## Commands

| Command | Description |
|---|---|
| `/offerletter:resume` | Tailor your resume to a job description, optimize for ATS, identify skill gaps, and improve bullet points |
| `/offerletter:keywords` | Extract the top ATS keywords from a job description |
| `/offerletter:cover-letter` | Create a tailored cover letter or review an existing draft |
| `/offerletter:interview` | Prepare for interviews with targeted questions and answer frameworks |
| `/offerletter:company-research` | Research a company — culture, news, interview process, and strategic insights |
| `/offerletter:career` | Explore career paths, assess your goals, and find target companies |

## Setup

1. Create a folder for your job search (e.g., `my-job-search/`)
2. Place your master resume in the root as `resume.tex` or `resume.md`
3. Create a `cover-letters/` folder with your reference cover letters
4. Open the folder in Claude Desktop (CoWork/CoTab)

```
my-job-search/
├── resume.tex (or resume.md)
├── cover-letters/
│   ├── cover-letter-1.tex
│   └── cover-letter-2.md
└── companies/                    ← created automatically
    └── google/
        ├── job-description.txt
        ├── resume.tex + resume.pdf
        ├── cover-letter.tex + cover-letter.pdf
        ├── interview-prep.md
        ├── company-research.md
        └── keywords.md
```

The plugin creates a `companies/` folder automatically. Each company gets its own subfolder with tailored documents, interview prep, and research.

## Installation

```
/plugin marketplace add Harshit-Khattar/offerletter
/plugin install offerletter@offerletter-marketplace
```

## Supported File Formats

| Input | What happens |
|---|---|
| `.tex` | Edited directly, compiled to PDF |
| `.md` | Edited directly, converted to LaTeX, compiled to PDF |
| `.pdf` (fallback) | Content extracted, new resume generated from ATS-friendly template |

## PDF Compilation

The plugin automatically compiles your tailored resume to PDF. It detects available LaTeX compilers (`pdflatex`, `xelatex`, `tectonic`) and uses whichever is installed. If none are found, it automatically installs [tectonic](https://tectonic-typesetting.github.io/) — a lightweight (~30MB) cross-platform LaTeX compiler.

## Tips for Saving Credits

- **Run `/offerletter:keywords` before `/offerletter:resume`** — extracted keywords get reused automatically
- **Paste the job description directly** — faster and cheaper than providing a URL
- **Company data carries over** — research, keywords, and JD are saved in `companies/` and reused across skills
- **Do `/offerletter:career` once** — self-assessment and role clarity don't change per company
- **Be specific** — `/offerletter:resume google` with a clear request is faster than letting Claude ask clarifying questions

## License

MIT
