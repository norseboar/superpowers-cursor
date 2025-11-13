# General Approach: Adapting Claude Skills to Cursor

## Understanding Claude Skills

Claude skills are reusable reference guides that auto-discover based on context. They activate automatically when relevant or via slash commands.

## Cursor Adaptation Strategy

Cursor doesn't have auto-discovery. **Commands are the primary mechanism** - they can load rules as needed.

### Cursor Commands (Primary)

Commands are `.md` files in `.cursor/commands/` invoked via `/CommandName`. They:

- Execute workflows explicitly
- Can load `.mdc` rule files for guidance
- Are the main way users invoke skills

### Cursor Rules (Supporting)

Rules are `.mdc` files in `.cursor/rules/` subdirectories that provide automatic guidance. They:

- Load at chat start or when attached to directories/file types
- Cannot auto-activate based on context (e.g., "when debugging")
- Can be loaded by commands when needed
- May auto-apply if configured, but don't rely on it

**Important constraints:**

- Don't assume rules are always loaded
- Don't tie rules to specific file extensions
- Commands are the primary activation mechanism

## Adaptation Process

1. **Analyze skill type**: Command (workflow) vs Rule (principle)
2. **Extract core principles**: Remove Claude-specific mechanisms
3. **Create command** (if workflow) that loads relevant rule (if principle)
4. **Keep rules concise**: Focus on "do X when Y" patterns

## Principles

- **Commands load rules**: Commands invoke workflows and load rules for guidance
- **Preserve essence**: Keep core principles, adapt activation mechanism
- **Be explicit**: Cursor needs explicit invocation, not auto-discovery
