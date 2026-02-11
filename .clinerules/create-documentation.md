---
description: "Guides Cline to generate comprehensive, well-structured documentation for existing code — READMEs, API docs, and inline comments."
author: "Cline Team"
version: "1.0"
category: "Documentation"
tags: ["documentation", "readme", "api-docs", "comments"]
globs: ["*.*"]
---

# Create Documentation

When asked to document code, produce clear, accurate, and useful documentation that helps developers understand the codebase quickly.

## Documentation Approach

1. **Read Before Writing** — Analyze the code thoroughly before documenting. Understand the architecture, data flow, and key design decisions.

2. **Audience Awareness** — Write for the developer who will maintain or use this code next. Assume they're competent but unfamiliar with this specific codebase.

3. **Accuracy Over Completeness** — It's better to document fewer things correctly than everything superficially. Never guess — if something is unclear, say so.

## README Generation

When creating or updating a README, include:

- **Project Title & Description** — What it does in 1-2 sentences
- **Quick Start** — Minimal steps to get running (install, configure, run)
- **Architecture Overview** — High-level description of how the system is organized, with a diagram if it would help
- **Key Concepts** — Domain terms or abstractions a new developer needs to understand
- **Configuration** — Environment variables, config files, and their options
- **Development** — How to set up a dev environment, run tests, and contribute

Keep it scannable. Use headings, code blocks, and bullet points.

## API Documentation

For functions, classes, and modules:

- **Purpose** — What it does and when to use it
- **Parameters** — Name, type, description, and whether required or optional
- **Return Value** — Type and description
- **Errors** — What can go wrong and how errors are communicated
- **Example** — A minimal, working usage example

## Inline Comments

Add comments that explain **why**, not **what**:

- ✅ `// Retry up to 3 times because the upstream API is flaky during deploys`
- ❌ `// Set retries to 3`

Focus comments on:
- Non-obvious business logic or domain rules
- Workarounds with context on why they're needed
- Performance-critical sections explaining the optimization
- Complex algorithms with a brief explanation of the approach
