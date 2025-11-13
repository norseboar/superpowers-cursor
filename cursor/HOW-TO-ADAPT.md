# How to Adapt a Claude Skill to Cursor

## Step 1: Analyze the Skill

**Is it a workflow?** → Command

- User initiates (brainstorming, planning, executing)
- Multi-step process
- Explicit invocation makes sense

**Is it a principle?** → Rule

- Discipline pattern (TDD, verification)
- Always-applicable guidance
- "Do X when Y" behavior

**Both?** → Command + Rule

- Command executes workflow
- Rule provides automatic guidance
- Command loads rule when invoked

## Step 2: Extract Core Content

From the skill's `SKILL.md`:

- **Overview**: Core principle in 1-2 sentences
- **When to Use**: Triggers and symptoms
- **Core Pattern**: Before/after examples
- **Implementation**: Code patterns or steps
- **Common Mistakes**: What to avoid

Remove:

- Claude-specific language ("Claude should...")
- Auto-discovery references
- Subagent testing details
- YAML frontmatter (not used in Cursor)

## Step 3: Create the Command

**Location**: `cursor/commands/superpowers/CommandName.md`

**Note**: This is a template. Users will copy commands from `cursor/commands/superpowers/` to their project's `.cursor/commands/superpowers/` directory.

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

## Step 4: Create the Rule (if needed)

**Location**: `cursor/rules/superpowers/rule-name.mdc`

**Note**: This is a template. Users will copy rules from `cursor/rules/superpowers/` to their project's `.cursor/rules/superpowers/` directory.

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

## Step 5: Link Them Together

**In the command**, reference the rule:

```markdown
Follow the `.cursor/rules/superpowers/[rule-name].mdc` rule for automatic guidance on [principle].
```

**In the rule**, reference the command for workflows:

```markdown
For detailed workflows, use the `.cursor/commands/superpowers/[command-name].md` command.
```

## Example: Condition-Based Waiting

**Original Skill**: Technique for async testing

**Adaptation**:

- **Rule** (`cursor/rules/superpowers/condition-based-waiting.mdc`): Always use condition-based waiting instead of arbitrary timeouts
- **Command** (`cursor/commands/superpowers/fix-flaky-test.md`): Apply condition-based waiting to fix flaky tests

The command loads the rule and walks through applying the technique to a specific test.

## Checklist

- [ ] Analyzed skill type (command/rule/both)
- [ ] Extracted core principles from skill
- [ ] Removed Claude-specific language
- [ ] Created command with clear workflow
- [ ] Created rule with core principles (if needed)
- [ ] Linked command and rule together
- [ ] Tested adaptation works in Cursor
