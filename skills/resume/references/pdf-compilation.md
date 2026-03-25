# PDF Compilation Reference

Shared across resume and cover-letter skills.

## Steps

### 1. Source Format

- `.tex` → compile directly
- `.md` → convert to LaTeX first (article class, geometry/enumitem/hyperref/titlesec packages), save as `.tex`, then compile

### 2. Check for pdflatex

```bash
pdflatex --version 2>/dev/null && echo "FOUND: pdflatex"
```

If pdflatex found → skip to step 4. If not → step 3.

### 3. Auto-Install pdflatex

Tell user: "No LaTeX compiler found. Installing pdflatex (one-time setup, matches Overleaf output)." Never suggest MacTeX full or TeX Live full.

```bash
uname -s  # Darwin/Linux/MINGW
```

**macOS:**
```bash
brew install --cask basictex
# Reload shell PATH to pick up new install
eval "$(/usr/libexec/path_helper)"
# Install common resume packages
sudo tlmgr update --self
sudo tlmgr install fontawesome5 enumitem titlesec preprint ragged2e everysel tocloft
```

**Windows:**
```bash
winget install MiKTeX.MiKTeX
```
MiKTeX auto-installs missing packages on first compile — no extra steps needed.

**Linux:**
```bash
sudo apt update && sudo apt install -y texlive-base texlive-latex-extra texlive-fonts-extra texlive-fonts-recommended
```

If install fails, tell user the exact command to run manually. **Last resort only**: install tectonic (`brew install tectonic` / `winget install tectonic-typesetting.tectonic`).

### 4. Compile

Use **same filename as master resume**. Quote paths with spaces.

```bash
# pdflatex (run twice for references)
pdflatex -interaction=nonstopmode "filename.tex" && pdflatex -interaction=nonstopmode "filename.tex"
```

**If pdflatex fails on a missing package**: install it with `sudo tlmgr install <package-name>` (macOS/Linux) and retry. MiKTeX (Windows) handles this automatically.

**Tectonic fallback only**: if pdflatex is unavailable and tectonic is installed:
- Comment out `\input{glyphtounicode}` and `\pdfgentounicode=1` (pdflatex-only, tectonic will error)
- Run `tectonic "filename.tex"`
- Restore the commented lines after compiling
- Warn user: fonts may look slightly different from Overleaf

### 6. Verify Page Count (HARD GATE)

```bash
mdls -name kMDItemNumberOfPages "filename.pdf" 2>/dev/null  # macOS
pdfinfo "filename.pdf" 2>/dev/null | grep Pages              # cross-platform
```

**If >1 page: DO NOT tell user it's done.** Stop immediately, tell user it's over 1 page, suggest specific lines to cut, wait for their decision, then recompile and re-verify. Never claim "1 page" without running this check.

### 7. Clean Up

```bash
rm -f *.aux *.log *.out *.synctex.gz *.fls *.fdb_latexmk
```

### 8. Failures

Fix .tex errors if possible and retry. If unresolvable, save .tex and tell user to compile manually with tectonic.

## Templates

When user has only PDF or wants fresh format, use from `${CLAUDE_PLUGIN_ROOT}/templates/`:

| Template | Use For |
|---|---|
| `ats-resume-clean.tex` | Any field, maximum ATS compatibility |
| `ats-resume-modern.tex` | Tech roles, subtle accent colors |
| `ats-resume-academic.tex` | Research/academic, includes publications |
