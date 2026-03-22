# Technical Interview Reference

Rules for generating appropriate technical interview questions based on the role, level, and job description.

## Calibration for New Grads / Entry-Level

- Questions should be solvable in a 15-20 minute discussion
- Focus on fundamentals and problem-solving approach, not obscure edge cases
- System design questions should be scoped to small systems (e.g., "design a URL shortener" not "design Netflix")
- Coding questions should test understanding, not memorization of algorithms

## Question Categories

### 1. Fundamental Concepts

Test understanding of core CS/DS concepts relevant to the role.

**Software Engineering roles:**
- Data structures: arrays, hash maps, trees, graphs — when to use which
- Algorithms: time/space complexity, common patterns (two pointers, sliding window, BFS/DFS)
- OOP principles: inheritance, polymorphism, encapsulation — with real examples
- Database basics: SQL queries, indexing, normalization

**Data Science / ML roles:**
- Statistics: hypothesis testing, p-values, confidence intervals, distributions
- ML fundamentals: bias-variance tradeoff, overfitting, cross-validation, feature engineering
- Model evaluation: precision/recall, ROC-AUC, confusion matrices
- Data wrangling: handling missing data, outliers, feature scaling

**AI / ML Engineering roles:**
- Deep learning: neural network architectures, backpropagation, gradient descent
- NLP/CV fundamentals: transformers, attention, CNNs, transfer learning
- MLOps: model deployment, monitoring, versioning, A/B testing
- System design for ML: feature stores, training pipelines, inference optimization

### 2. Problem-Solving Approach

These questions test HOW the candidate thinks, not just what they know.

**Format:** Present a scenario, ask for their approach before asking for code.

Example prompts:
- "You notice that your model's accuracy dropped 5% after retraining. Walk me through how you'd investigate."
- "A user reports that the API is slow. How would you diagnose the issue?"
- "You need to process 10 million records daily. What architecture would you consider?"

**What to evaluate:**
- Do they ask clarifying questions before jumping in?
- Do they consider edge cases?
- Can they break down a large problem into smaller steps?
- Do they discuss tradeoffs?

### 3. Coding Component

For roles that include coding interviews:

**Question design rules:**
- One clear problem statement with example inputs/outputs
- Solvable with basic data structures (no need for advanced algorithms)
- Has a brute force solution AND an optimized solution
- Tests communication as much as coding ability

**Good coding question characteristics:**
- Relates to real work scenarios (parsing data, transforming records, API design)
- Can be solved in multiple valid ways
- Has natural follow-ups ("How would this change if the data didn't fit in memory?")

### 4. System Design (Simplified)

For entry-level, system design is about demonstrating awareness, not expertise.

**Appropriate scope:**
- Design a simple feature, not an entire platform
- Focus on component choices and tradeoffs, not precise scaling numbers
- "Design a job application tracker" not "Design LinkedIn"

**Key areas to cover:**
- Data model (what entities, what relationships)
- API design (what endpoints, what inputs/outputs)
- Storage choice (SQL vs NoSQL, why)
- One scalability consideration ("What if we had 100x users?")

## Role-Specific Question Templates

### Software Engineer
1. Fundamental: "Explain when you'd use a hash map vs a tree. Give a real example."
2. Problem-solving: "How would you design an API for [feature from the JD]?"
3. Coding: A string/array manipulation problem relevant to the company's domain
4. System design: "Design a simplified version of [company's product feature]"

### Data Scientist
1. Fundamental: "Walk me through how you'd set up an A/B test for [company feature]."
2. Problem-solving: "You have a dataset with 30% missing values. What's your approach?"
3. Coding: A data manipulation/analysis problem (pandas/SQL)
4. Case study: "How would you measure the success of [company initiative]?"

### ML Engineer
1. Fundamental: "Explain the difference between batch and online learning. When would you use each?"
2. Problem-solving: "Your deployed model's latency is too high. What are your options?"
3. Coding: An ML pipeline or data processing problem
4. System design: "Design a recommendation system for [company's product]"

### AI Engineer
1. Fundamental: "Explain attention mechanisms in transformers. Why are they important?"
2. Problem-solving: "How would you evaluate a generative AI feature for [company product]?"
3. Coding: A text processing or model integration problem
4. System design: "Design a RAG pipeline for [company's domain]"

## Generating Questions from the JD

For each required skill in the job description:
1. Identify the skill
2. Create one question that tests understanding (conceptual)
3. Create one question that tests application (practical scenario)

Example:
- JD says: "Experience with distributed systems"
- Conceptual: "What is the CAP theorem and why does it matter?"
- Practical: "Our service needs to handle 10K requests/second. Walk me through your approach."

## Expected Answer Key Points

For each generated question, provide:
- 3-5 key points the interviewer expects to hear
- Common mistakes to avoid
- What distinguishes a good answer from a great one
