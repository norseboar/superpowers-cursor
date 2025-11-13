# Review Code

Systematic code review workflow for assessing production readiness. Reviews code changes against requirements/plans, checks code quality, architecture, testing, and categorizes issues by severity.

Before starting, read `.cursor/rules/superpowers/using-skills.mdc` for guidance on executing skills.

## When to Use

When the user requests code review for:

- Completed features or tasks
- Code changes before merging
- Implementation verification against plans
- Quality assessment before proceeding

**Use this ESPECIALLY when:**

- After completing major features
- Before merging to main
- After implementing tasks from a plan
- When verification is needed against requirements

## Process

### Step 1: Gather Context

**Get the following information from the user:**

- What was implemented (description of changes)
- Requirements or plan reference (what it should do)
- Git range to review (base SHA and head SHA, or file paths if no git)

**If git SHAs provided:**

```bash
git diff --stat {BASE_SHA}..{HEAD_SHA}
git diff {BASE_SHA}..{HEAD_SHA}
```

**If file paths provided:**
Read the relevant files and understand what changed.

### Step 2: Create Review Document

Save review to: `docs/reviews/YYYY-MM-DD-<feature-or-change-name>.md`

**Naming convention:**

- Use date prefix: `YYYY-MM-DD-`
- Follow with descriptive name (feature name, task name, or change description)
- Use kebab-case (lowercase with hyphens)
- Examples:
  - `2024-01-15-user-authentication.md`
  - `2024-01-15-task-3-api-endpoints.md`
  - `2024-01-15-bugfix-index-repair.md`

**Review document header:**

```markdown
# Code Review: [Feature/Change Name]

**Date:** YYYY-MM-DD
**Reviewed:** [What was implemented]
**Against:** [Plan/Requirements reference]
**Git Range:** {BASE_SHA}..{HEAD_SHA} (if applicable)

---
```

### Step 3: Review Against Checklist

Create TodoWrite todos for each checklist category and work through them systematically.

#### Code Quality

- [ ] Clean separation of concerns?
- [ ] Proper error handling?
- [ ] Type safety (if applicable)?
- [ ] DRY principle followed?
- [ ] Edge cases handled?

#### Architecture

- [ ] Sound design decisions?
- [ ] Scalability considerations?
- [ ] Performance implications?
- [ ] Security concerns?

#### Testing

- [ ] Tests actually test logic (not mocks)?
- [ ] Edge cases covered?
- [ ] Integration tests where needed?
- [ ] All tests passing? (Ask user to run tests and provide results)

#### Requirements

- [ ] All plan requirements met?
- [ ] Implementation matches spec?
- [ ] No scope creep?
- [ ] Breaking changes documented?

#### Production Readiness

- [ ] Migration strategy (if schema changes)?
- [ ] Backward compatibility considered?
- [ ] Documentation complete?
- [ ] No obvious bugs?

### Step 4: Categorize Issues

For each issue found, categorize by severity:

**Critical (Must Fix):**

- Bugs
- Security issues
- Data loss risks
- Broken functionality

**Important (Should Fix):**

- Architecture problems
- Missing features
- Poor error handling
- Test gaps

**Minor (Nice to Have):**

- Code style
- Optimization opportunities
- Documentation improvements

### Step 5: Format Review Output

**Save the formatted review to the document created in Step 2.**

Present findings in this structure:

#### Strengths

[What's well done? Be specific with file:line references where applicable.]

#### Issues

##### Critical (Must Fix)

[For each issue:]

- **File:line reference**
- **What's wrong**
- **Why it matters**
- **How to fix** (if not obvious)

##### Important (Should Fix)

[Same format as Critical]

##### Minor (Nice to Have)

[Same format as Critical]

#### Recommendations

[Improvements for code quality, architecture, or process]

#### Assessment

**Ready to merge?** [Yes/No/With fixes]

**Reasoning:** [Technical assessment in 1-2 sentences]

## Critical Rules

**DO:**

- Categorize by actual severity (not everything is Critical)
- Be specific (file:line, not vague)
- Explain WHY issues matter
- Acknowledge strengths
- Give clear verdict
- Ask user to run tests and provide results (don't assume tests pass)

**DON'T:**

- Say "looks good" without checking
- Mark nitpicks as Critical
- Give feedback on code you didn't review
- Be vague ("improve error handling")
- Avoid giving a clear verdict
- Run tests yourself (ask user to run and provide results)

## Example Output

```
### Strengths
- Clean database schema with proper migrations (db.ts:15-42)
- Comprehensive test coverage (18 tests, all edge cases)
- Good error handling with fallbacks (summarizer.ts:85-92)

### Issues

#### Important
1. **Missing help text in CLI wrapper**
   - File: index-conversations:1-31
   - Issue: No --help flag, users won't discover --concurrency
   - Fix: Add --help case with usage examples

2. **Date validation missing**
   - File: search.ts:25-27
   - Issue: Invalid dates silently return no results
   - Fix: Validate ISO format, throw error with example

#### Minor
1. **Progress indicators**
   - File: indexer.ts:130
   - Issue: No "X of Y" counter for long operations
   - Impact: Users don't know how long to wait

### Recommendations
- Add progress reporting for user experience
- Consider config file for excluded projects (portability)

### Assessment

**Ready to merge: With fixes**

**Reasoning:** Core implementation is solid with good architecture and tests. Important issues (help text, date validation) are easily fixed and don't affect core functionality.
```
