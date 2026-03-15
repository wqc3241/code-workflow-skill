---
name: code-workflow
description: Enforces disciplined coding workflow rules for all development tasks. Use when writing code, fixing bugs, adding features, or making any code changes. Covers branching, planning, verification, testing, and self-improvement.
user-invocable: true
disable-model-invocation: false
allowed-tools: Read, Write, Edit, Bash, Grep, Glob, Agent
---

# Code Workflow Rules

Follow ALL of these rules when writing code, fixing bugs, or adding features.

---

## 1. Branch First (MANDATORY)

Before making ANY code change for a new feature or bug fix:

1. Create a new branch from the current base branch:
   - Features: `feature/<short-description>`
   - Bug fixes: `fix/<short-description>`
2. Never commit directly to `main` or the primary branch.
3. All work happens on the feature/fix branch until verified and complete.

---

## 2. Planning & Execution

- Enter plan mode for ANY non-trivial task (3+ steps or architectural decisions).
- If something goes sideways, STOP and re-plan immediately — don't keep pushing.
- Use plan mode for verification steps, not just building.
- Write detailed specs upfront to reduce ambiguity.
- Plan first: write plan to `tasks/todo.md` with checkable items.
- Check in before starting implementation.
- Mark items complete as you go.
- Add a review section to `tasks/todo.md` when done.

---

## 3. Subagent Strategy

- Use subagents liberally to keep the main context window clean.
- Offload research, exploration, and parallel analysis to subagents.
- For complex problems, throw more compute at it via subagents.
- One task per subagent for focused execution.

---

## 4. Self-Improvement Loop

- After ANY correction from the user: update `tasks/lessons.md` with the pattern.
- Write rules for yourself that prevent the same mistake.
- Ruthlessly iterate on these lessons until mistake rate drops.
- Review `tasks/lessons.md` at session start for relevant project context.

---

## 5. Verification Before Done

- Never mark a task complete without proving it works.
- Diff behavior between main and your changes when relevant.
- Ask yourself: "Would a staff engineer approve this?"
- Run tests, check logs, demonstrate correctness.

---

## 6. Elegance (Balanced)

- For non-trivial changes: pause and ask "is there a more elegant way?"
- If a fix feels hacky: "Knowing everything I know now, implement the elegant solution."
- Skip this for simple, obvious fixes — don't over-engineer.
- Challenge your own work before presenting it.

---

## 7. Autonomous Bug Fixing

- When given a bug report: just fix it. Don't ask for hand-holding.
- Point at logs, errors, failing tests — then resolve them.
- Zero context switching required from the user.
- Go fix failing CI tests without being told how.

---

## 8. Code Implementation via OpenAI Codex 5.3 (MANDATORY)

When it's time to actually write or modify code:

1. **Check for OpenAI API key first.** Look for `OPENAI_API_KEY` in the environment or `.env` file.
   - If not found, ask the user to provide their OpenAI API key before proceeding.
   - Do NOT attempt to write code without it.
2. **Use codeX 5.3 to write the code.**
   - Send a well-structured prompt to codeX 5.3 describing exactly what code is needed, including context from the codebase (relevant files, function signatures, patterns).
   - You MUST use the `codex-5.3` model. Do not fall back to other models.
3. **Review codeX 5.3 output before applying.**
   - Never blindly paste generated code. Read it, verify it follows project conventions, and check for security issues.
   - Edit or regenerate if the output is not up to standard.
4. **Integrate the generated code** into the project using Edit/Write tools.

---

## 9. Core Principles

- **Simplicity First**: Make every change as simple as possible. Impact minimal code.
- **No Laziness**: Find root causes. No temporary fixes. Senior developer standards.
- **Minimal Impact**: Changes should only touch what's necessary. Avoid introducing bugs.

---

## 10. End-to-End Test Cases (MANDATORY)

After completing any new feature or bug fix:

1. Create end-to-end test cases that cover the change.
2. Tests should document what the feature/fix does so the system has a record.
3. Include happy path, edge cases, and regression scenarios.
4. Place tests in the project's test directory following existing conventions.
5. Run the tests and confirm they pass before marking complete.

---

## 11. Completion Checklist

Before declaring any task done, verify ALL of these:

- [ ] Work is on a dedicated branch (not main)
- [ ] `tasks/todo.md` plan exists and all items are checked
- [ ] Code changes are minimal and focused
- [ ] End-to-end test cases are written and passing
- [ ] Tests demonstrate the feature works or the bug is fixed
- [ ] `tasks/lessons.md` updated if any corrections were received
- [ ] Self-review: "Would a staff engineer approve this?"
