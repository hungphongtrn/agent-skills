---
name: consult-smart-model-with-agy
description: >
  Consult a Gemini smart model for second opinions, decision support, and analysis.
  Use when the user wants a second opinion on an implementation plan, is facing a
  tough architectural or design decision, needs to validate an approach, wants help
  weighing tradeoffs, or asks for analytical reasoning on a complex problem. Do NOT
  use this skill for code generation, file manipulation, or execution - it is purely
  for consultation and decision-making support. The skill runs agy in headless
  mode to ask questions and returns the model's response.
---

# Consult Smart Model with Agy

## Purpose

Use agy in headless mode to ask Gemini a question and return its analysis. This skill is for consulting the model as a thinking partner - not for doing work. The current agent remains responsible for all execution.

## Decision Tree

```
User asks about a tough decision or wants analysis
  └─ Is this purely for consultation/analysis?
       ├─ YES → Use this skill. Ask agy, return the response.
       └─ NO  → Decline. This skill is not for code generation or file work.
```

## Quick Start

```bash
agy --model gemini-3.5-flash-medium -p "<question>"
```

## Usage Guidelines

### When to Use

- Weighing tradeoffs between architectural approaches
- Validating an implementation plan before executing
- Getting a second opinion on a technical decision
- Analyzing a complex problem where another perspective helps
- Reviewing a plan or design proposal critically

### When NOT to Use

- Code generation or scaffolding
- Writing or editing files
- Running commands or executing work
- Tasks the current agent can handle independently

## Instructions

1. **Frame the question precisely** - Include relevant context, constraints, and the specific decision to be made. The better the question, the better the answer.

2. **Run agy headless**:

   ```bash
   agy --model gemini-3.5-flash-medium -p "<your question>"
   ```

3. **Present the response** - Show the user what Gemini said. Synthesize if the response is long, but preserve the key reasoning and recommendation.

4. **Do NOT act on the advice** - The current agent may incorporate the consultation into its own thinking, but the user decides what to do with the analysis.


## Example Session

**User:** "Should I use PostgreSQL or MongoDB for my content management system?"

**Agent loads this skill, then:**

```bash
agy --model gemini-3.5-flash-medium -p "We're building a CMS with user-authored content, versioning, and relational metadata like categories/tags. Team size: 2 backend devs. Expected scale: 50k documents initially. Should we use PostgreSQL or MongoDB? Consider: schema flexibility needs, query patterns (filtering by multiple related fields), operational overhead, and migration experience over time."
```

Returns the response to the user for consideration.
