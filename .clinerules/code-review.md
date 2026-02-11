---
description: "Guides Cline to perform thorough code reviews focused on bugs, security vulnerabilities, performance issues, and readability improvements."
author: "Cline Team"
version: "1.0"
category: "Development"
tags: ["code-review", "security", "performance", "best-practices"]
globs: ["*.*"]
---

# Code Review

When asked to review code, follow this structured approach to provide actionable, high-quality feedback.

## Review Process

1. **Understand Context First** — Read the code and any related files to understand what it does and why before critiquing.

2. **Prioritize Findings** — Organize feedback by severity:
   - 🔴 **Critical** — Bugs, security vulnerabilities, data loss risks
   - 🟡 **Important** — Performance issues, error handling gaps, logic problems
   - 🟢 **Suggestions** — Readability, naming, style, simplification opportunities

3. **Be Specific and Actionable** — Every piece of feedback should include:
   - What the issue is
   - Why it matters
   - A concrete suggestion or fix

## What to Look For

### Correctness
- Logic errors and off-by-one mistakes
- Unhandled edge cases (null, empty, boundary values)
- Race conditions in concurrent code
- Incorrect assumptions about data shape or API contracts

### Security
- Unsanitized user input (SQL injection, XSS, command injection)
- Hardcoded secrets or credentials
- Missing authentication or authorization checks
- Insecure data handling (logging sensitive data, weak crypto)

### Performance
- Unnecessary work inside loops (N+1 queries, repeated calculations)
- Missing caching opportunities
- Large memory allocations or leaks
- Blocking operations that should be async

### Maintainability
- Functions doing too many things
- Duplicated logic that should be extracted
- Unclear naming or missing context
- Dead code or unused imports

### Error Handling
- Swallowed exceptions with no logging
- Missing error handling on I/O operations
- Unclear error messages that won't help debugging
- Missing cleanup in failure paths

## Output Format

Present findings grouped by severity. For each finding:
- Reference the specific file and line/section
- Explain the issue concisely
- Suggest a fix with a code snippet when helpful

End with a brief summary of overall code quality and the most important action items.
