---
description: "Guides Cline to analyze and explain a codebase — its architecture, tech stack, key patterns, and important files — so you can get up to speed fast."
author: "Cline Team"
version: "1.0"
category: "Development"
tags: ["onboarding", "codebase", "architecture", "learning"]
globs: ["*.*"]
---

# Codebase Onboarding

When asked to explain or walk through a codebase, provide a structured analysis that helps the developer understand how the project works and where to find things.

## Analysis Process

1. **Start with the Big Picture** — Identify what the project does, its tech stack, and its overall architecture before diving into details.

2. **Follow the Entry Points** — Trace from main entry files (e.g., `main.ts`, `index.js`, `App.tsx`, `manage.py`) to understand how the application starts and how requests/data flow through the system.

3. **Map the Structure** — Explain the directory layout and what each major folder/module is responsible for.

## What to Cover

### Project Overview
- What the project does (inferred from README, package metadata, and code)
- Tech stack (languages, frameworks, key libraries)
- Build system and how to run it

### Architecture
- High-level architecture pattern (monolith, microservices, layered, etc.)
- Key modules/packages and their responsibilities
- How data flows through the system
- A diagram if the architecture has multiple components

### Key Files & Entry Points
- Main entry point(s) and what they initialize
- Configuration files and what they control
- The most important files a developer would need to modify for common tasks

### Patterns & Conventions
- Naming conventions and code organization patterns
- How state is managed
- How errors are handled
- How tests are organized and run
- Any project-specific patterns or abstractions

### Dependencies
- Critical external dependencies and what they're used for
- Internal shared libraries or utilities
- Database, API, or service dependencies

## Output Format

Structure the explanation so a developer can read it top-down and build a mental model progressively:

1. One-paragraph summary of what this project is
2. Tech stack and how to run it
3. Architecture overview (with diagram if helpful)
4. Directory structure walkthrough
5. Key files and what they do
6. Patterns and conventions to follow
7. Where to start for common tasks
