# Brainstorm

Turn ideas into fully formed designs and specs through natural collaborative dialogue. Refines rough ideas into complete designs through questioning, alternative exploration, and incremental validation.

**IMPORTANT**: Before starting, read `.cursor/rules/superpowers/using-skills.mdc` for guidance on executing skills.

## When to Use

When the user has a rough idea that needs to be refined into a complete design before implementation. Use before writing code or implementation plans. Don't use during clear 'mechanical' processes where the approach is already well-defined.

## Process

### Step 1: Understand the Idea

1. **Check project context first**

   - Review relevant files, documentation, and recent commits
   - Understand the current project state

2. **Ask questions one at a time**
   - Ask only one question per message
   - If a topic needs more exploration, break it into multiple questions
   - Prefer multiple choice questions when possible (easier to answer), but open-ended is fine too
   - Focus on understanding: purpose, constraints, success criteria

### Step 2: Explore Approaches

1. **Propose 2-3 different approaches with trade-offs**
   - Present options conversationally
   - Lead with your recommended option and explain why
   - Include your reasoning for the recommendation

### Step 3: Present the Design

1. **Once you understand what you're building, present the design**
   - Break it into sections of 200-300 words each
   - Ask after each section whether it looks right so far
   - Cover: architecture, components, data flow, error handling, testing
   - Be ready to go back and clarify if something doesn't make sense

### Step 4: After the Design

**Documentation:**

- Write the validated design to `docs/plans/YYYY-MM-DD-<topic>-design.md`
- Use clear, concise writing
- Commit the design document to git

**Implementation (if continuing):**

- Ask: "Ready to set up for implementation?"
- If yes, use the appropriate commands to create isolated workspace and detailed implementation plan

## Key Principles

- **One question at a time** - Don't overwhelm with multiple questions
- **Multiple choice preferred** - Easier to answer than open-ended when possible
- **YAGNI ruthlessly** - Remove unnecessary features from all designs
- **Explore alternatives** - Always propose 2-3 approaches before settling
- **Incremental validation** - Present design in sections, validate each
- **Be flexible** - Go back and clarify when something doesn't make sense

## Example

User: "I want to add user authentication"

You: "I'm using the brainstorming skill to refine your idea into a design. Let me understand the project context first..."

[Check files, then ask one question at a time]

"First, what type of authentication do you need?
A) Simple username/password
B) OAuth (Google, GitHub, etc.)
C) Both options available
D) Something else"

[Continue with one question at a time, then explore approaches, then present design in sections]
