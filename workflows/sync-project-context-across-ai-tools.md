---
description: "Keep Cline's .clinerules in sync with the same project instructions used by Claude Code, Cursor, Gemini CLI, Copilot, Roo Code, and other AI coding agents."
author: "https://github.com/caioribeiroclw-pixel"
version: "1.0"
category: "Workflow"
tags: ["cline", "clinerules", "context", "ai-tools", "project-instructions", "pluribus"]
globs: ["pluribus.md", ".clinerules", "AGENTS.md", "CLAUDE.md", "GEMINI.md", ".roo/rules/*.md", ".github/copilot-instructions.md"]
---

<task name="Sync Project Context Across AI Tools">

<task_objective>
Use a single reviewed project-context file as the source of truth, then generate Cline's `.clinerules` and the equivalent native instruction files for the other AI coding agents used in the repository. This reduces instruction drift when a team switches between Cline, Claude Code, Cursor, Gemini CLI, Copilot, Roo Code, Windsurf, Continue, Zed, Amazon Q, Junie, Warp, OpenCode, or OpenClaw.
</task_objective>

<detailed_sequence_steps>
# Sync Project Context Across AI Tools - Detailed Sequence of Steps

## 1. Confirm the repository's context source of truth

1. Inspect the repository root for an existing canonical context file:
   - `pluribus.md`
   - `AGENTS.md`
   - `CLAUDE.md`
   - `.clinerules`
   - `.cursor/rules/*.mdc`
   - `GEMINI.md`
   - `.roo/rules/*.md`
   - `.github/copilot-instructions.md`

2. If more than one instruction file exists, compare them before changing anything. Treat drift as a review problem, not something to overwrite silently.

3. If there is no clear source of truth, ask the user whether to create `pluribus.md` as the canonical file.

## 2. Create or update `pluribus.md`

1. Keep the file small and intentional. Pluribus expects these top-level sections:
   - `# Identity`
   - `# Stack`
   - `# Conventions`
   - `# Goals`
   - `# Constraints`

2. Put durable project guidance inside those sections, such as:
   - project purpose and architecture boundaries;
   - build/test/lint commands;
   - coding conventions;
   - directories the agent must not modify;
   - security, privacy, or destructive-action limits;
   - reviewer expectations.

3. If starting from scratch, initialize a valid skeleton first:

```bash
npm exec --yes --package github:caioribeiroclw-pixel/pluribus#v0.3.51 -- pluribus init --dry-run
npm exec --yes --package github:caioribeiroclw-pixel/pluribus#v0.3.51 -- pluribus init
```

4. Do not copy raw secrets, private transcripts, customer data, environment files, or giant generated docs into the context file.

5. If converting from existing `.clinerules` or `CLAUDE.md`, preserve meaning first. Do not add new policy unless the user explicitly approves it.

## 3. Run Pluribus to generate native agent instruction files

Use the GitHub release package while the npm registry may lag behind the latest adapter release:

```bash
npm exec --yes --package github:caioribeiroclw-pixel/pluribus#v0.3.51 -- pluribus sync --tools cline,claude,cursor,gemini-cli,copilot,roo --dry-run
```

Review the dry-run output. If it looks correct, run:

```bash
npm exec --yes --package github:caioribeiroclw-pixel/pluribus#v0.3.51 -- pluribus sync --tools cline,claude,cursor,gemini-cli,copilot,roo
```

Expected generated files include:

- `.clinerules` for Cline
- `CLAUDE.md` / `AGENTS.md` for Claude Code and AGENTS-compatible tools
- Cursor rule files
- `GEMINI.md` for Gemini CLI
- `.github/copilot-instructions.md` for GitHub Copilot
- `.roo/rules/pluribus.md` for Roo Code

## 4. Validate before relying on the generated files

1. Run the project checks listed in the generated context file, for example:

```bash
npm test
```

2. Validate Pluribus output and check for drift:

```bash
npm exec --yes --package github:caioribeiroclw-pixel/pluribus#v0.3.51 -- pluribus validate
npm exec --yes --package github:caioribeiroclw-pixel/pluribus#v0.3.51 -- pluribus audit --json --fidelity-report
```

3. Review the changed files with `git diff`. Confirm the generated `.clinerules` matches the canonical intent before committing.

4. If Cline's behavior still differs after the file is generated, do not assume the rule is bad. Check whether Cline actually loaded the expected rule surface and whether another global/project rule conflicts with it.

## 5. Commit the context source and generated targets together

1. Commit `pluribus.md` and the generated instruction files in the same change so reviewers can compare source intent against target files.

2. Use a clear commit message, for example:

```text
chore: sync AI agent project instructions
```

3. In the pull request, mention:
   - which file is canonical;
   - which agent targets were generated;
   - which validation commands passed;
   - any intentionally omitted private or local-only context.

## 6. Maintenance rule

When project instructions change later, edit the canonical context file first, re-run the sync, then review the generated files. Avoid hand-editing `.clinerules`, `CLAUDE.md`, `GEMINI.md`, or Copilot instructions independently unless the change is intentionally tool-specific.

</detailed_sequence_steps>

</task>
