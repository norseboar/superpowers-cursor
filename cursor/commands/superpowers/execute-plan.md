# Execute Plan

Execute a complete implementation plan in controlled batches with review checkpoints. Load plan, review critically, execute tasks in batches, and report for review between batches.

**IMPORTANT**: Before starting, read `.cursor/rules/superpowers/using-skills.mdc` for guidance on executing skills.

## When to Use

When the user provides a complete implementation plan that needs to be executed. Use this for systematic, controlled implementation with checkpoints for review.

## Process

### Step 1: Load and Review Plan

1. Read the plan file
2. Review critically - identify any questions or concerns about the plan
3. If concerns: Raise them with your human partner before starting
4. If no concerns: Create TodoWrite todos for the tasks and proceed

### Step 2: Execute Batch

**Default: First 3 tasks**

For each task:

1. Mark as in_progress
2. Follow each step exactly (plan has bite-sized steps)
3. For verifications specified in the plan: Stop and ask the user to run the verification and provide the results/logs
4. Mark as completed

### Step 3: Report

When batch complete:

- Show what was implemented
- Show verification output (from user-provided results)
- Say: "Ready for feedback."

### Step 4: Continue

Based on feedback:

- Apply changes if needed
- Execute next batch
- Repeat until complete

### Step 5: Complete Development

After all tasks complete and verified:

- Announce: "I'm using the finishing-a-development-branch skill to complete this work."
- **REQUIRED SUB-SKILL:** Use the finishing-a-development-branch command/rule if available
- Follow that skill to verify tests, present options, execute choice

## When to Stop and Ask for Help

**STOP executing immediately when:**

- Hit a blocker mid-batch (missing dependency, test fails, instruction unclear)
- Plan has critical gaps preventing starting
- You don't understand an instruction
- Verification fails repeatedly

**Ask for clarification rather than guessing.**

## When to Revisit Earlier Steps

**Return to Review (Step 1) when:**

- Partner updates the plan based on your feedback
- Fundamental approach needs rethinking

**Don't force through blockers** - stop and ask.

## Key Principles

- Review plan critically first
- Follow plan steps exactly
- Don't skip verifications - prompt user to run them and provide results
- Reference skills when plan says to
- Between batches: just report and wait
- Stop when blocked, don't guess

## Example

User: "Execute the plan in `docs/plans/2024-01-15-auth-design.md`"

You: "I'm using the executing-plans skill to implement this plan. Let me load and review it first..."

[Load plan, review critically, create todos, execute first batch, report, wait for feedback]
