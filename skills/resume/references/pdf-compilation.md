# PDF Compilation Reference

Cross-platform instructions for compiling LaTeX files to PDF. This reference is shared across the resume and cover-letter skills.

## Decision Tree

After writing a `.tex` or `.md` file, always attempt PDF compilation:

### 1. Determine the Source Format

- **If `.tex` file** → proceed to step 2
- **If `.md` file** → first convert the markdown content to LaTeX:
  - Create a minimal LaTeX document wrapping the markdown content
  - Use `article` document class with `geometry`, `enumitem`, `hyperref`, `titlesec` packages
  - Map markdown headings to LaTeX sections, bullets to itemize, bold/italic to LaTeX equivalents
  - Save as `.tex` alongside the `.md` file
  - Proceed to step 2

### 2. Check for Available Compilers

Run these checks in order (use Bash tool):

```bash
pdflatex --version 2>/dev/null && echo "FOUND: pdflatex"
xelatex --version 2>/dev/null && echo "FOUND: xelatex"
tectonic --version 2>/dev/null && echo "FOUND: tectonic"
```

- If **any** compiler is found → use it (prefer pdflatex > xelatex > tectonic for speed)
- If **none** found → proceed to step 3

### 3. Auto-Install Tectonic

If no compiler is found, **automatically install tectonic** — a lightweight LaTeX compiler (~30MB, no dependencies). Do NOT suggest MacTeX or TeX Live — they are multi-GB installs and unnecessary.

Tell the user:
> "No LaTeX compiler found. I'll install tectonic — a lightweight compiler (~30MB) — so I can generate your PDF."

Then detect the OS and install:

```bash
uname -s  # Darwin = macOS, Linux = Linux, MINGW/MSYS = Windows
```

**macOS:**
```bash
# Try Homebrew first
which brew && brew install tectonic

# No Homebrew — download binary directly
curl -LO https://github.com/tectonic-typesetting/tectonic/releases/latest/download/tectonic-x86_64-apple-darwin.tar.gz
tar xzf tectonic-x86_64-apple-darwin.tar.gz
chmod +x tectonic
sudo mv tectonic /usr/local/bin/
rm tectonic-x86_64-apple-darwin.tar.gz
```

**Windows:**
```bash
# Try winget first
winget install tectonic-typesetting.tectonic

# Fallback: try scoop
scoop install tectonic
```

**Linux:**
```bash
# Debian/Ubuntu
sudo apt install tectonic

# Fedora
sudo dnf install tectonic

# Arch
sudo pacman -S tectonic

# Fallback: download binary
curl -LO https://github.com/tectonic-typesetting/tectonic/releases/latest/download/tectonic-x86_64-unknown-linux-gnu.tar.gz
tar xzf tectonic-x86_64-unknown-linux-gnu.tar.gz
chmod +x tectonic
sudo mv tectonic /usr/local/bin/
rm tectonic-x86_64-unknown-linux-gnu.tar.gz
```

**Do not ask for permission** — just install it and inform the user. Tectonic is small and safe. If the install fails (e.g., no sudo access), then fall back to telling the user how to install it manually.

### 4. Compile

```bash
cd companies/<company-name>/

# Using pdflatex (run twice for references)
pdflatex -interaction=nonstopmode resume.tex
pdflatex -interaction=nonstopmode resume.tex

# OR using tectonic (handles multiple passes automatically)
tectonic resume.tex
```

### 5. Clean Up Build Artifacts

```bash
cd companies/<company-name>/
rm -f *.aux *.log *.out *.synctex.gz *.fls *.fdb_latexmk
```

Keep only the `.tex` and `.pdf` files.

### 6. Handle Failures

If compilation fails:
- Read the error output carefully
- Common issues:
  - Missing package → install it or simplify the template
  - Unicode characters → switch from pdflatex to xelatex or tectonic
  - Missing fonts → use standard fonts (Computer Modern, Latin Modern)
- If you can fix the `.tex` file, fix it and retry
- If compilation cannot be resolved, save the `.tex` file and tell the user:
  > "Your tailored resume has been saved as `resume.tex`. I wasn't able to compile it to PDF because [reason]. You can compile it manually using your LaTeX editor, or install tectonic (https://tectonic-typesetting.github.io/) and run `tectonic resume.tex`."

**Never block on PDF failure** — the source file is the primary deliverable. PDF is a convenience.

## Template Selection

When the user only has a PDF or wants a fresh format, use a template from `${CLAUDE_PLUGIN_ROOT}/templates/`:

| Template | Best for |
|---|---|
| `ats-resume-clean.tex` | Any field. Minimal, single-column, maximum ATS compatibility |
| `ats-resume-modern.tex` | Tech roles. Clean with subtle accent colors |
| `ats-resume-academic.tex` | Research/academic roles. Includes publications, teaching sections |

Choose based on the user's field and the job they're applying for. Ask if unsure.

To use a template:
1. Read the template file
2. Replace placeholder content with the user's information
3. Save to the company folder
4. Compile as normal
