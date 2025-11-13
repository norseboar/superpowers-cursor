# Conversion Tracking

This file tracks which Claude skills have been adapted to Cursor commands and rules.

## Converted Skills

### using-superpowers

**Original**: `skills/using-superpowers/SKILL.md`

**Created**:

- `cursor/rules/superpowers/using-skills.mdc`

**Notes**: Converted to a rule that provides guidance for executing skills. Removed Claude-specific auto-discovery mechanisms (checking for skills, using Skill tool) and focused on how to execute skills when invoked via commands. Kept mandatory workflows, checklist handling with TodoWrite, announcing usage, and the principle that instructions don't override workflows.

### brainstorming

**Original**: `skills/brainstorming/SKILL.md`

**Created**:

- `cursor/commands/superpowers/brainstorm.md`

**Notes**: Converted to a command that guides the workflow of turning ideas into designs. Removed Claude-specific language (Skill tool references) and adapted the workflow for Cursor. Kept all key principles (one question at a time, YAGNI, explore alternatives, incremental validation) and the complete process from understanding the idea through presenting the design. The command follows the same structure: understand context, ask questions one at a time, explore approaches, present design in sections, then document.

### writing-plans

**Original**: `skills/writing-plans/SKILL.md`

**Created**:

- `cursor/commands/superpowers/write-plan.md`

**Notes**: Converted to a command that guides the workflow of creating comprehensive implementation plans. Removed ALL TDD-related content (test-first steps, RED-GREEN-REFACTOR references) and adapted all testing/execution instructions to prompt the user to run tests and provide results instead of the agent running them. Kept all key principles: bite-sized tasks (2-5 minutes each), exact file paths, complete code examples, verification steps, plan document header structure, and execution handoff options. The command maintains the structure for creating plans that assume zero codebase context.

### executing-plans

**Original**: `skills/executing-plans/SKILL.md`

**Created**:

- `cursor/commands/superpowers/execute-plan.md`

**Notes**: Converted to a command that guides the workflow of executing implementation plans in batches with checkpoints. Removed YAML frontmatter and Claude-specific language. Adapted verification instructions to prompt the user to run verifications and provide results instead of the agent running them. Kept all workflow steps (load/review, execute batch, report, continue, complete), all "when to stop" guidance, and all key principles. The command maintains the batch execution pattern with review checkpoints between batches.

### systematic-debugging

**Original**: `skills/systematic-debugging/SKILL.md`

**Created**:

- `cursor/commands/superpowers/debug.md`
- `cursor/rules/superpowers/systematic-debugging.mdc`

**Notes**: Converted to both a command (workflow) and a rule (principles). Removed TDD references (replaced with prompting user to create tests) and adapted all testing/execution instructions to prompt the user to run tests, reproduce issues, and provide results instead of the agent running them. Kept all four phases (root cause investigation, pattern analysis, hypothesis testing, implementation), all rationalizations, don'ts, exceptions, warnings, and the iron law "NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST". The command includes the complete workflow with explicit steps, and the rule distills core principles for automatic guidance. Both reference root-cause-tracing as a required sub-skill.

### root-cause-tracing

**Original**: `skills/root-cause-tracing/SKILL.md`

**Created**:

- `cursor/rules/superpowers/root-cause-tracing.mdc`

**Notes**: Converted to a rule that provides guidance on tracing bugs backward through call stacks. Removed Claude-specific language and adapted testing instructions to prompt the user to add instrumentation and provide stack traces instead of the agent running them. Kept all key principles (never fix just the symptom, trace backward to source, add defense-in-depth), the tracing process steps, stack trace tips, and the visual diagram showing the tracing flow. This rule is referenced as REQUIRED by systematic-debugging when errors occur deep in call stacks.

### verification-before-completion

**Original**: `skills/verification-before-completion/SKILL.md`

**Created**:

- `cursor/rules/superpowers/verification-before-completion.mdc`

**Notes**: Converted to a rule that provides guidance on verifying work before claiming completion. Removed TDD-specific references (red-green cycle) and adapted all execution instructions to prompt the user to run verification commands and provide results instead of the agent running them. Kept all key principles: the iron law "NO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION EVIDENCE", the gate function (identify, run, read, verify, claim), all red flags, rationalizations, and common failure patterns. The rule applies automatically before any completion claims. Referenced as REQUIRED by systematic-debugging in Phase 4 when verifying fixes.

### code-reviewer

**Original**: `skills/requesting-code-review/code-reviewer.md`

**Created**:

- `cursor/commands/superpowers/review-code.md`

**Notes**: Converted the code-reviewer template into a command for performing code reviews. Removed placeholder syntax and converted to instructions for the AI. Kept all review checklist categories (code quality, architecture, testing, requirements, production readiness), issue categorization by severity (Critical/Important/Minor), output format structure, and all critical rules. Adapted testing instructions to prompt the user to run tests and provide results instead of the agent running them. The command provides a systematic workflow for reviewing code changes against requirements/plans and assessing production readiness.

### receiving-code-review

**Original**: `skills/receiving-code-review/SKILL.md`

**Created**:

- `cursor/rules/superpowers/receiving-code-review.mdc`
- `cursor/commands/superpowers/address-code-review.md`

**Notes**: Converted to both a rule (principles) and a command (workflow). The rule provides guidance on how to receive and process code review feedback. The command provides a systematic workflow for addressing code review documents (typically created by the review-code command). Removed YAML frontmatter and Claude-specific language. Adapted testing instructions to prompt the user to test each fix and verify no regressions instead of the agent running tests. Kept all key principles: verify before implementing, no performative agreement, technical correctness over social comfort, handling unclear feedback, source-specific handling (human partner vs external reviewers), YAGNI checks, implementation order, when to push back, and all forbidden responses. Preserved all rationalizations, don'ts, exceptions, and warnings. The command assumes a review document exists and walks through reading, understanding, verifying, and implementing fixes in the proper order (Critical → Important → Minor).

## Pending Conversion

<!-- Skills that haven't been converted yet -->
