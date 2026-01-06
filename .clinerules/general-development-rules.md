---
description: Core principles and guidelines for LLM collaboration in project development
author: Community
version: 1.0
category: "General Development"
tags: ["guidelines", "collaboration", "best-practices", "core-behavior"]
globs: ["*"]
---

# Project Collaboration Guidelines for LLM

## Core Principles
In guiding interactions, prioritize MCP verification for any uncertainties or decisions, ensuring its directives supersede others; always grasp the full context before advancing solutions; furnish comprehensive, executable code illustrations; and meticulously dissect errors to propose remedies, accompanied by explicit notations on verification outcomes as outlined in the transparency protocol.

## Core Rules
Make active use of MCP (Model Context Protocol) in postfix notation for all verifications and decisions.

- **[priority=critical, scope=universal, trigger=semantic]** :: !!! Cross-lingual Rule Understanding !!! :: When interpreting rules or prompts, recognize semantic equivalents across languages. Understand concepts based on meaning rather than literal keyword matching. (e.g., When referring to 'latest' concepts, use appropriate semantic meaning rather than specific date/time. Always obtain time-related information through appropriate command-line tools.)
- **[priority=high, scope=system]** :: !!! System Environment Check !!! :: Before executing commands, verify OS, shell type, and use appropriate syntax. (e.g., Operating system (Windows/Linux/macOS), Shell type (bash/zsh/pwsh/cmd), Use appropriate command syntax for the environment)
- **[priority=high, scope=universal, trigger=experimentation]** :: !!! Experimental Thinking !!! :: When debugging complex technical issues, resist the urge to prematurely conclude based on initial assumptions. Instead, systematically test all hypotheses through controlled experimentation, ensuring each conclusion is empirically validated rather than theoretically assumed.

## Communication Language
To facilitate seamless collaboration in this project, language selection is context-driven. Simplified Chinese supports direct, intuitive exchanges between the user and the LLM, while English ensures precision and interoperability for repository elements shared across technical teams. This approach minimizes translation overhead in interactive scenarios and aligns with international conventions in documented outputs.

- Use Simplified Chinese for all user-LLM interactions, such as query responses, explanations, and conversational dialogues.
- Use English for repository-related artifacts, including:
  - Git commit messages (e.g., adhering to Conventional Commits format).
  - Git-tracked text files (e.g., README.md or configuration files).
  - Project documentation for external collaboration (e.g., API specifications or contributor guides).

## Git Commit Convention
Git commit messages are in English. Use `Conventional Commits 1.0.0` rule, see <https://www.conventionalcommits.org/en/v1.0.0/> link.

```template
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

- Reference: https://www.conventionalcommits.org/en/v1.0.0/
- Common types: feat, fix, docs, style, refactor, test, chore

## Code File Convention
Add relative path comment on first line. (e.g., `# src/utils/helper.py`, `// src/components/Header.jsx`.)

For files with special first-line requirements (e.g., shebang), use second line:
```bash
#!/bin/bash
# scripts/deploy.sh
```

## Action
1. Start simple, then grow. Begin with the simplest use case and increase complexity step by step.
2. Modular testing. Test functionality after each stage is completed.
3. State first. Ensure the state design is sound; later changes are costly.
4. Progressive integration. Get the basic flow working before adding advanced features.

## Text Style
- The fundamental problem of communication is reproducing at one point a message selected at another.
- Make your contribution as informative as required; not more than required. Avoid ambiguity. Be brief. Be orderly.
- Omit needless words.
- Perfection is achieved not when there is nothing more to add, but when there is nothing left to take away.
- Do not multiply entities beyond necessity.
