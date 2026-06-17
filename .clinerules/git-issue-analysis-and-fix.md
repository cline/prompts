---
description: Guides Cline to analyze a reported Git or GitHub issue, determine root cause, implement a fix, and validate the outcome.
author: Community
version: 1.0
category: "Issue Resolution"
tags: ["git", "github", "issue-analysis", "bug-fix", "workflow", "mcp"]
globs: ["*"]
---

# Git Issue Analysis and Fix

Objective: Follow a structured process to understand a reported Git or GitHub issue, investigate the relevant code or repository history, implement a focused fix, and validate the result before completion.

Trigger: Use this rule when the task involves debugging, analyzing, or fixing a reported issue, bug, regression, repository problem, or GitHub issue.

## Process

1. Understand the Issue First
   - Read the issue description carefully.
   - Identify expected behavior, actual behavior, reproduction steps, and any referenced files, commits, pull requests, or discussions.
   - If the issue is unclear or incomplete, ask follow-up questions before making assumptions.

2. Gather Context Before Editing
   - Inspect the relevant files, modules, configuration, and tests.
   - Search for related symbols, error messages, and nearby implementation patterns.
   - Understand how the affected area fits into the broader codebase before proposing a fix.

3. Use GitHub MCP When Available
   - If a GitHub MCP server is available, use it to gather additional issue context.
   - This can include:
     - reading the GitHub issue directly
     - reviewing issue comments and linked discussions
     - inspecting related pull requests
     - checking changed files and commits
     - reviewing CI, review comments, or related implementation history
   - GitHub MCP context should complement local repository inspection, not replace it.

4. Reproduce or Isolate the Problem
   - Reproduce the issue locally when possible.
   - Run relevant tests, inspect logs, and isolate the smallest failing case.
   - If reproduction is not possible, clearly state that and reason from the available evidence.

5. Form a Root-Cause Hypothesis
   - Identify the most likely reason the problem occurs.
   - Tie the hypothesis to specific code paths, configuration, or repository state.
   - Avoid speculative fixes that are not connected to observed evidence.

6. Implement a Focused Fix
   - Make the smallest reasonable change that resolves the root cause.
   - Preserve existing architecture, naming, and project conventions.
   - Avoid unrelated refactoring unless it is required to safely fix the issue.
   - Update tests or documentation if the fix changes behavior or expectations.

7. Validate Before Completion
   - Run targeted tests and other relevant checks.
   - Use build, lint, or manual verification steps when appropriate.
   - If full validation is not possible, explicitly state what was verified and what remains unverified.

8. Summarize the Resolution Clearly
   - Explain the root cause.
   - Describe the files or areas changed.
   - State how the fix addresses the issue.
   - Report what validation was performed.
   - Mention any follow-up work, assumptions, or remaining risks.

## Behavioral Guidance

- ALWAYS investigate before editing.
- ALWAYS inspect relevant files and existing patterns before applying changes.
- SHOULD ask clarifying questions if issue details or reproduction steps are missing.
- SHOULD use GitHub MCP tools when available for issue and PR context.
- MUST NOT report a fix as complete without validation details.
- MUST NOT introduce broad unrelated changes while addressing a focused issue.
- MUST NOT rely on guesswork when the issue can be clarified or investigated further.

## Completion Checklist

Before finishing, verify the following:

- [ ] The issue has been understood clearly.
- [ ] Relevant code and repository context have been inspected.
- [ ] GitHub MCP context was used if available and helpful.
- [ ] A root cause has been identified or clearly justified.
- [ ] The implemented fix is focused and aligned with existing patterns.
- [ ] Validation has been performed or limitations have been stated.
- [ ] The final summary explains the outcome clearly.

## Output Expectation

The final response should preferably include:

1. Issue Summary
2. Root Cause
3. Changes Made
4. Validation Performed
5. Remaining Risks or Next Steps