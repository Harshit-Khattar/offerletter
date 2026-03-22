# Multi-Job Fit Analysis Reference

Logic for comparing a resume against multiple job descriptions and ranking fit.

## When to Use

The user provides their resume and 2 or more job descriptions. They want to know:
- Which positions are the best fit
- Where they're strongest and weakest
- Which roles to prioritize in their applications

## Analysis Process

### Step 1: Create a Skills Matrix

For each job description, extract:
- Required technical skills
- Required soft skills
- Required experience level (years, seniority)
- Required education
- Domain/industry knowledge
- Nice-to-have qualifications

### Step 2: Score Each Position

For each requirement, score the resume's match:
- **Strong match (3)**: Resume clearly demonstrates this skill/qualification
- **Partial match (2)**: Resume has related experience that could transfer
- **Weak match (1)**: Resume has minimal evidence of this skill
- **No match (0)**: Not represented in the resume at all

Weight the scores:
- Required qualifications: 2x multiplier
- Preferred qualifications: 1x multiplier

### Step 3: Rank and Analyze

Total the weighted scores for each position and rank from highest to lowest.

## Output Format

Present findings as a structured comparison:

```markdown
## Multi-Job Fit Analysis

### Rankings

| Rank | Company — Role | Fit Score | Verdict |
|------|---------------|-----------|---------|
| 1 | Company A — Data Scientist | 85% | Strong fit |
| 2 | Company B — ML Engineer | 72% | Good fit with gaps |
| 3 | Company C — SWE | 58% | Stretch role |

### Detailed Analysis

#### 1. Company A — Data Scientist (85% fit)

**Why it's a strong fit:**
- [Specific strengths that align]

**Gaps to address:**
- [Specific missing qualifications]

**Application strategy:**
- [How to position the application]

#### 2. Company B — ML Engineer (72% fit)
...
```

### Step 4: Strategic Recommendations

After the analysis, recommend:
1. **Prioritize applications** — apply to strongest fits first (higher response rate)
2. **Address gaps strategically** — for partial-fit roles, suggest specific resume tweaks
3. **Identify pattern gaps** — if a skill is missing across multiple JDs, it's a development priority
4. **Time allocation** — spend more customization effort on top-fit roles, use a lighter touch for stretch roles

## Edge Cases

- **All positions are weak fits**: Be honest. Suggest skill development areas rather than forcing a fit
- **Multiple positions at same company**: Note this — applying to too many roles at one company can signal unfocused interest
- **Very different role types**: Group by category first (e.g., "Data Science roles" vs "Software Engineering roles") before comparing
