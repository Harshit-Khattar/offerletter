# PDF Compilation Reference

Shared across resume and cover-letter skills.

## Steps

### 1. Source Format

- `.tex` → compile directly
- `.md` → convert to LaTeX first (article class, geometry/enumitem/hyperref/titlesec packages), save as `.tex`, then compile

### 2. Check Compilers

```bash
pdflatex --version 2>/dev/null && echo "FOUND: pdflatex"
xelatex --version 2>/dev/null && echo "FOUND: xelatex"
tectonic --version 2>/dev/null && echo "FOUND: tectonic"
```

Prefer pdflatex (matches Overleaf output). If none found → step 3.

### 3. Auto-Install Tectonic

Tell user: "No compiler found. Installing tectonic (~30MB)." Never suggest MacTeX/TeX Live.

```bash
uname -s  # Darwin/Linux/MINGW
```

**macOS:** `which brew && brew install tectonic` or download binary from GitHub releases
**Windows:** `winget install tectonic-typesetting.tectonic` or `scoop install tectonic`
**Linux:** `sudo apt install tectonic` or download binary from GitHub releases

If install fails, tell user how to install manually.

### 4. Compile

Use same filename as master resume. Quote paths with spaces.

```bash
# pdflatex (run twice)
pdflatex -interaction=nonstopmode "filename.tex" && pdflatex -interaction=nonstopmode "filename.tex"

# OR tectonic
tectonic "filename.tex"
```

### 5. Verify Page Count

```bash
mdls -name kMDItemNumberOfPages "filename.pdf" 2>/dev/null  # macOS
pdfinfo "filename.pdf" 2>/dev/null | grep Pages              # cross-platform
```

If >1 page: stop, tell user, suggest cuts, wait for decision, recompile.

### 6. Clean Up

```bash
rm -f *.aux *.log *.out *.synctex.gz *.fls *.fdb_latexmk
```

### 7. Failures

Fix .tex errors if possible and retry. If unresolvable, save .tex and tell user to compile manually with tectonic.

## Templates

When user has only PDF or wants fresh format, use from `${CLAUDE_PLUGIN_ROOT}/templates/`:

| Template | Use For |
|---|---|
| `ats-resume-clean.tex` | Any field, maximum ATS compatibility |
| `ats-resume-modern.tex` | Tech roles, subtle accent colors |
| `ats-resume-academic.tex` | Research/academic, includes publications |
