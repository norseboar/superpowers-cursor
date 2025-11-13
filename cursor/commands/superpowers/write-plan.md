# Write Plan

Create comprehensive implementation plans assuming the engineer has zero context for the codebase. Document everything needed: which files to touch for each task, complete code examples, verification steps, and how to verify it works. Give them the whole plan as bite-sized tasks.

Before starting, read `.cursor/rules/superpowers/using-skills.mdc` for guidance on executing skills.

**Announce at start:** "I'm using the write-plan skill to create the implementation plan."

## When to Use

When design is complete and you need detailed implementation tasks for engineers with zero codebase context. This creates comprehensive implementation plans with exact file paths, complete code examples, and verification steps assuming the engineer has minimal domain knowledge.

**Context:** This should ideally be run in a dedicated worktree (created by brainstorming skill).

## Process

### Step 1: Plan Document Structure

Save plans to: `docs/plans/YYYY-MM-DD-<feature-name>.md`

**Every plan MUST start with this header:**

```markdown
# [Feature Name] Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** [One sentence describing what this builds]

**Architecture:** [2-3 sentences about approach]

**Tech Stack:** [Key technologies/libraries]

---
```

### Step 2: Create Bite-Sized Tasks

**Each step is one action (2-5 minutes):**

- "Create the file structure" - step
- "Write the implementation" - step
- "Ask user to verify it works" - step
- "Commit" - step

**Task Structure:**

````markdown
### Task N: [Component Name]

**Files:**

- Create: `exact/path/to/file.py`
- Modify: `exact/path/to/existing.py:123-145`
- Test: `tests/exact/path/to/test.py` (if applicable)

**Step 1: Create file structure**

Create the file at `exact/path/to/file.py` with the following structure:

```python
def function(input):
    # Implementation here
    return result
```
````

**Step 2: Implement the functionality**

Add the following code to `exact/path/to/existing.py` at lines 123-145:

```python
# Complete code example here
```

**Step 3: Ask user to verify**

Stop and ask the user to:

1. Run the code/application
2. Test the specific behavior
3. Provide logs or results showing it works

**Verification command:** `[exact command to run]`
**Expected behavior:** [What should happen]

**Step 4: Commit**

```bash
git add exact/path/to/file.py exact/path/to/existing.py
git commit -m "feat: add specific feature"
```

````

### Step 3: Remember Key Principles

- **Exact file paths always** - Never use vague references like "the file" or "somewhere"
- **Complete code in plan** - Not "add validation" but the actual validation code
- **Exact commands with expected output** - What command to run and what should happen
- **Reference relevant skills** - Use @ syntax or explicit references when appropriate
- **DRY, YAGNI, frequent commits** - Apply these principles throughout
- **Assume zero context** - The engineer doesn't know your codebase conventions, so document everything

### Step 4: Execution Handoff

After saving the plan, inform the user:

**"Plan complete and saved to `docs/plans/<filename>.md`. To execute this plan, open a new session in the worktree and use the superpowers:executing-plans command for batch execution with checkpoints."**

## Example

```markdown
# User Authentication Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add user authentication with email/password login and JWT tokens.

**Architecture:** REST API endpoints for login/register, JWT token generation and validation middleware, password hashing with bcrypt.

**Tech Stack:** Express.js, bcrypt, jsonwebtoken, PostgreSQL

---

### Task 1: User Model

**Files:**
- Create: `src/models/User.js`

**Step 1: Create user model**

Create `src/models/User.js`:

```javascript
const bcrypt = require('bcrypt');

class User {
  constructor(email, passwordHash) {
    this.email = email;
    this.passwordHash = passwordHash;
  }

  static async hashPassword(password) {
    return await bcrypt.hash(password, 10);
  }

  async verifyPassword(password) {
    return await bcrypt.compare(password, this.passwordHash);
  }
}

module.exports = User;
````

**Step 2: Ask user to verify**

Stop and ask the user to:

1. Create a simple test file that imports this model
2. Try creating a user instance
3. Provide any errors or confirmation it works

**Step 3: Commit**

```bash
git add src/models/User.js
git commit -m "feat: add User model with password hashing"
```

```

```
