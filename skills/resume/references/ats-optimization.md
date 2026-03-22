# ATS Optimization Reference

Rules and guidelines for making resumes compatible with Applicant Tracking Systems.

## What ATS Systems Look For

ATS software parses resumes into structured data. It extracts:
- Contact information (name, email, phone, LinkedIn)
- Section headers (Education, Experience, Skills, etc.)
- Job titles and company names
- Dates of employment/education
- Skills and keywords
- Degree information

## Section Organization (Recommended Order)

1. **Contact Information** — Name, email, phone, LinkedIn, GitHub (if relevant)
2. **Summary/Objective** — Optional, 2-3 sentences tailored to the role
3. **Education** — For students, this often comes before experience
4. **Technical Skills** — Grouped by category
5. **Experience** — Reverse chronological
6. **Projects** — Relevant technical or academic projects
7. **Certifications / Awards** — If applicable

Note: For experienced professionals, Experience comes before Education. For students and recent graduates, Education first is standard.

## Formatting Rules for ATS

### DO:
- Use standard section headers: "Experience", "Education", "Skills", "Projects" (ATS looks for these)
- Use reverse chronological order within each section
- Include full dates (Month Year – Month Year), not just years
- Use standard fonts (in LaTeX: Computer Modern, Latin Modern, or similar)
- Use bullet points (not paragraphs) for experience descriptions
- Keep to one column layout
- Include the exact job title from the JD in your experience section if truthful
- Save as PDF (maintains formatting across systems)

### DON'T:
- Use tables or multi-column layouts (ATS can't parse them reliably)
- Use images, logos, or icons
- Use text boxes or floating elements
- Use headers/footers for important information (many ATS skip these)
- Use uncommon section headers like "What I've Done" instead of "Experience"
- Use abbreviations without the full term (write "Machine Learning (ML)" first time)
- Use fancy formatting like sidebars, progress bars for skills, or infographics

## Keyword Strategy

### Density Guidelines
- Target ~60% coverage of the top 20 keywords from the JD
- Each critical keyword should appear at least once
- Important keywords should appear in the Skills section AND in an experience/project bullet
- Use exact phrases from the JD (ATS matches exact strings)

### Natural Integration
- Keywords should read naturally in context
- Never list keywords in a hidden or white-text section (ATS can detect this, and it's an auto-reject)
- Vary the form: "Developed machine learning models" + "Machine Learning" in skills section

### Keyword Placement Priority
1. Skills section (highest weight for keyword matching)
2. Job titles and section headers
3. Experience bullet points
4. Project descriptions
5. Summary/objective

## Common ATS-Breaking Issues

| Issue | Fix |
|---|---|
| Two-column layout | Convert to single column |
| Skill bars / progress indicators | Replace with text list |
| Icons for contact info | Use text labels |
| Custom section headers | Use standard names |
| Missing dates | Add Month Year format |
| PDF from design tool (Canva, etc.) | Recompile from LaTeX or use clean template |
| Non-standard characters | Stick to ASCII for section headers |

## LaTeX-Specific ATS Tips

- Use `\section{}` for section headers (standard and parsable)
- Avoid `\begin{tabular}` for layout — use `\begin{itemize}` for bullets
- `hyperref` package is fine for links — ATS handles them well
- Avoid `multicol` package
- Avoid `tikz` for decorative elements
- `enumitem` package is safe for customizing lists
