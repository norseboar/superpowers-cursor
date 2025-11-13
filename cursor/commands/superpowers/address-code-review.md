# Address Code Review

Process code review feedback systematically: read, understand, verify, evaluate, and implement fixes one at a time with technical rigor.

Before starting, read `.cursor/rules/superpowers/using-skills.mdc` for guidance on executing skills.

Follow the `.cursor/rules/superpowers/receiving-code-review.mdc` rule for automatic guidance on processing feedback.

## When to Use

When you have received code review feedback (typically from the `review-code` command) and need to address the issues systematically.

**Use this when:**

- A code review document exists (usually in `docs/reviews/`)
- You need to process feedback from a review
- You want to ensure all issues are addressed with proper verification

## Process

### Step 1: Locate and Read Review Document

**Get the review document path from the user:**

- Usually in `docs/reviews/YYYY-MM-DD-<feature-name>.md`
- Or ask user to provide the path to the review document

**Read the complete review document:**

- Read all sections: Strengths, Issues (Critical/Important/Minor), Recommendations, Assessment
- Do not react or start implementing yet
- Understand the full scope of feedback

### Step 2: Understand Each Issue

For each issue in the review:

1. **Restate the requirement** in your own words
2. **Identify what needs to be checked** before implementing
3. **Note any unclear items** that need clarification

**If any item is unclear:**

- **STOP** - do not implement anything yet
- **ASK** the user for clarification on unclear items
- **Why:** Items may be related. Partial understanding = wrong implementation.

**Example:**

```
Review has items 1-6. You understand 1,2,3,6. Unclear on 4,5.

❌ WRONG: Implement 1,2,3,6 now, ask about 4,5 later
✅ RIGHT: "I understand items 1,2,3,6. Need clarification on 4 and 5 before proceeding."
```

### Step 3: Verify Each Issue Against Codebase

Before implementing any suggestion, verify:

1. **Check:** Technically correct for THIS codebase?
2. **Check:** Breaks existing functionality?
3. **Check:** Reason for current implementation?
4. **Check:** Works on all platforms/versions?
5. **Check:** Does reviewer understand full context?

**For YAGNI checks:**

- If reviewer suggests "implementing properly" for unused features
- Search codebase for actual usage
- If unused: Ask user "This endpoint isn't called. Remove it (YAGNI)?"
- If used: Then implement properly

**If suggestion seems wrong:**

- Push back with technical reasoning
- Reference working code/tests
- Ask specific questions

**If can't easily verify:**

- Say so: "I can't verify this without [X]. Should I [investigate/ask/proceed]?"

**If conflicts with user's prior decisions:**

- Stop and discuss with user first

### Step 4: Process Issues in Order

**Implementation order:**

1. Clarify anything unclear FIRST
2. Then implement in this order:
   - **Critical (Must Fix)** - Blocking issues (breaks, security)
   - **Important (Should Fix)** - Architecture, missing features, error handling
   - **Minor (Nice to Have)** - Code style, optimizations, documentation
3. Within each category: Simple fixes (typos, imports) before complex fixes (refactoring, logic)

**For each issue:**

1. Verify against codebase (Step 3)
2. If verified correct: Implement the fix
3. If unclear: Ask for clarification
4. If wrong: Push back with technical reasoning
5. Ask user to test the fix individually
6. Move to next issue

### Step 5: Handle Pushback When Needed

**Push back when:**

- Suggestion breaks existing functionality
- Reviewer lacks full context
- Violates YAGNI (unused feature)
- Technically incorrect for this stack
- Legacy/compatibility reasons exist
- Conflicts with user's architectural decisions

**How to push back:**

- Use technical reasoning, not defensiveness
- Ask specific questions
- Reference working tests/code
- Involve user if architectural

**Signal if uncomfortable pushing back:** "Strange things are afoot at the Circle K"

### Step 6: Acknowledge and Implement Correct Feedback

**When feedback IS correct:**

- ✅ "Fixed. [Brief description of what changed]"
- ✅ "Good catch - [specific issue]. Fixed in [location]."
- ✅ [Just fix it and show in the code]

**NEVER:**

- ❌ "You're absolutely right!" (performative agreement)
- ❌ "Great point!" / "Excellent feedback!" (performative)
- ❌ "Thanks" or any gratitude expression

**Why:** Actions speak. Just fix it. The code itself shows you heard the feedback.

### Step 7: Verify No Regressions

After implementing fixes:

- Ask user to test each fix individually
- Ask user to verify no regressions
- Confirm all Critical and Important issues are addressed

## Critical Rules

**DO:**

- Read complete feedback before reacting
- Verify each suggestion against codebase
- Clarify unclear items before implementing
- Implement one issue at a time
- Ask user to test each fix
- Push back with technical reasoning when needed
- State fixes factually (no performative agreement)

**DON'T:**

- Implement before verification
- Batch implement without testing
- Assume reviewer is always right
- Use performative language ("Thanks", "Great point!")
- Skip clarification on unclear items
- Proceed when you can't verify something

## Example Workflow

```
1. Read review document: docs/reviews/2024-01-15-user-auth.md

2. Review has:
   - Critical: 1 issue (security)
   - Important: 2 issues (error handling, missing validation)
   - Minor: 1 issue (code style)

3. Understand each:
   - Critical #1: "Add input validation" - Clear, need to verify current state
   - Important #1: "Improve error handling" - Unclear, need to ask what specifically
   - Important #2: "Missing date validation" - Clear, need to verify
   - Minor #1: "Use const instead of let" - Clear, simple fix

4. Ask for clarification on Important #1 before proceeding

5. After clarification, verify each against codebase:
   - Critical #1: Verified - no validation exists, should add
   - Important #1: Verified - error handling is indeed minimal
   - Important #2: Verified - date validation missing
   - Minor #1: Verified - can use const

6. Implement in order:
   - Critical #1: Add input validation
   - Important #1: Improve error handling
   - Important #2: Add date validation
   - Minor #1: Change let to const

7. After each fix: Ask user to test
8. Final: Ask user to verify no regressions
```

## Integration

This command works with:

- **review-code** command - Processes reviews created by that command
- **receiving-code-review** rule - Follows the principles from that rule
