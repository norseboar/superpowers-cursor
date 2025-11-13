# Adapt Skill

Adapt a Claude skill from the `skills/` directory into Cursor commands and/or rules.

## When to Use

When you need to convert a Claude skill into Cursor-usable formats (commands and rules).

## Process

**IMPORTANT**: Before starting, read `.cursor/rules/superpowers/using-skills.mdc` for guidance on executing skills. All commands should begin by referencing this rule.

### Step 1: Analyze the Skill

Read the skill's `SKILL.md` file in `skills/[skill-name]/SKILL.md`.

**IMPORTANT**: If the skill is primarily about Test-Driven Development (TDD), do NOT adapt it. Inform the user that TDD skills are excluded from adaptation.

Determine the adaptation type:

- **Is it a workflow?** → Command

  - User initiates (brainstorming, planning, executing)
  - Multi-step process
  - Explicit invocation makes sense

- **Is it a principle?** → Rule

  - Discipline pattern (verification, systematic debugging)
  - Always-applicable guidance
  - "Do X when Y" behavior

- **Both?** → Command + Rule
  - Command executes workflow
  - Rule provides automatic guidance
  - Command loads rule when invoked

### Step 2: Extract Core Content

From the skill's `SKILL.md`, extract:

- **Overview**: Core principle in 1-2 sentences
- **When to Use**: Triggers and symptoms
- **Core Pattern**: Before/after examples
- **Implementation**: Code patterns or steps
- **Common Mistakes**: What to avoid
- **Rationalizations**: All warnings and "don't" lists
- **Exceptions**: When not to use

Remove:

- Claude-specific language ("Claude should...", "Use the Skill tool...")
- Auto-discovery references ("check for skills", "list available skills")
- Subagent testing details
- YAML frontmatter (not used in Cursor)
- Parts about finding/discovering skills (doesn't apply to Cursor)
- **Test-Driven Development (TDD) content** - Leave out ALL references to TDD, RED-GREEN-REFACTOR, writing tests first, etc. If the skill contains TDD content, you MUST remove it AND notify the user that TDD content was excluded.

Adapt (replace with user prompts):

- **Testing/execution instructions** - Any instruction for the agent to test, run, or verify by running code should be replaced with prompting the user to do it and provide results/logs.

**Key principle**: Be faithful to the original skill. Keep all rationalizations, don'ts, exceptions, and warnings unless they specifically don't apply to Cursor.

**IMPORTANT - TDD Exclusion**: Test-Driven Development content should NOT be included in adaptations. If you encounter TDD references in the skill:

1. Remove all TDD-related content
2. Explicitly inform the user: "Note: I've excluded TDD-related content from this adaptation as requested."

**IMPORTANT - Testing Adaptation**: We do NOT run automated tests. If the skill suggests the agent should:

- Test something out
- Try something and see what happens
- Run tests
- Get logs or output from running code
- Verify behavior by executing code

Replace these with: **Stop and prompt the user**. The agent should:

1. Stop what it's doing
2. Ask the user to test/try the thing
3. Request that the user provide logs or results
4. Wait for user feedback before continuing

**Example adaptations**:

- "Run the test to verify" → "Stop and ask the user to run the test and provide the results"
- "Try this and see what happens" → "Stop and ask the user to try this and report what happens"
- "Check the logs" → "Stop and ask the user to check the logs and share them"

### Step 3: Create the Command (if needed)

**Location**: `cursor/commands/superpowers/CommandName.md`

**Note**: Files are created in this project's `cursor/` directory, but when executed in other projects, they will be in `.cursor/commands/superpowers/`.

**Structure**:

```markdown
# Command Name

Brief description of what this command does.

## When to Use

[When should the user invoke this?]

## Process

[Step-by-step workflow from the skill]

## Example

[Brief usage example]
```

**Key changes**:

- Write as instructions for the AI: "When the user invokes this command..."
- Include explicit steps from the skill
- Reference the rule if one exists: "Follow the [rule-name] rule for guidance"
- **Start with**: "Before starting, read `.cursor/rules/superpowers/using-skills.mdc` for guidance on executing skills."

### Step 4: Create the Rule (if needed)

**Location**: `cursor/rules/superpowers/rule-name.mdc`

**Note**: Files are created in this project's `cursor/` directory, but when executed in other projects, they will be in `.cursor/rules/superpowers/`.

**Structure**:

```markdown
# Rule Name

Core principle in 1-2 sentences.

## When This Applies

[Conditions when this rule should guide behavior]

## Principles

- [Key principle 1]
- [Key principle 2]

## Common Mistakes

- [Mistake] → [Fix]
```

**Key changes**:

- Distill to core principles only
- Remove workflow details (those go in commands)
- Write as "always do X when Y" patterns
- Keep concise for context efficiency
- **Preserve all rationalizations, don'ts, and warnings** from the original skill

### Step 5: Link Them Together

**In the command**, reference the rule:

```markdown
Follow the `.cursor/rules/superpowers/[rule-name].mdc` rule for automatic guidance on [principle].
```

**In the rule**, reference the command for workflows:

```markdown
For detailed workflows, use the `.cursor/commands/superpowers/[command-name].md` command.
```

### Step 6: Update TRACKING.md

Add an entry to `cursor/TRACKING.md` in the "Converted Skills" section:

```markdown
### [skill-name]

**Original**: `skills/[skill-name]/SKILL.md`

**Created**:

- `cursor/commands/superpowers/[command-name].md`
- `cursor/rules/superpowers/[rule-name].mdc` (if applicable)

**Notes**: [1-2 sentences describing how it was adapted, what was kept, what was removed]
```

## Checklist

- [ ] Read `.cursor/rules/superpowers/using-skills.mdc` first
- [ ] Checked if skill is primarily about TDD (if yes, inform user and skip adaptation)
- [ ] Analyzed skill type (command/rule/both)
- [ ] Extracted core principles from skill
- [ ] Removed only Claude-specific mechanisms (not content)
- [ ] **Removed ALL TDD content and notified user if TDD was found**
- [ ] **Adapted all testing/execution instructions to prompt user instead**
- [ ] Preserved all rationalizations, don'ts, exceptions
- [ ] Created command with clear workflow (if needed)
- [ ] Created rule with core principles (if needed)
- [ ] Linked command and rule together
- [ ] Updated TRACKING.md with conversion entry
- [ ] Command starts with reference to using-skills.mdc

## Reference

See `cursor/HOW-TO-ADAPT.md` for detailed adaptation guidelines.
