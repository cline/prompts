---
description: Defines a process for Cline to reflect on interactions and suggest improvements to active .clinerules.
author: https://github.com/nickbaumann98
version: 1.0
category: "Cline Core"
tags: ["meta", "self-improvement", "clinerules", "reflection", "core-behavior"]
globs: ["*"]
---
# Self-Improving Cline Reflection

**Objective:** Offer opportunities to continuously improve `.clinerules` based on user interactions and feedback.

**Trigger:** Before using the `attempt_completion` tool for any task that involved user feedback provided at any point during the conversation, or involved multiple non-trivial steps (e.g., multiple file edits, complex logic generation).

**Process:**

1.  **Offer Reflection:** Ask the user: "Before I complete the task, would you like me to reflect on our interaction and suggest potential improvements to the active `.clinerules`?"
2.  **Await User Confirmation:** Proceed to `attempt_completion` immediately if the user declines or doesn't respond affirmatively.
3.  **If User Confirms:**
    a.  **Review Interaction:** Synthesize all feedback provided by the user throughout the entire conversation history for the task. Analyze how this feedback relates to the active `.clinerules` and identify areas where modified instructions could have improved the outcome or better aligned with user preferences.
    b.  **Identify Active Rules:** List the specific global and workspace `.clinerules` files active during the task.
    c.  **Formulate & Propose Improvements:** Generate specific, actionable suggestions for improving the *content* of the relevant active rule files. Prioritize suggestions directly addressing user feedback. Use `replace_in_file` diff blocks when practical, otherwise describe changes clearly.
    d.  **Await User Action on Suggestions:** Ask the user if they agree with the proposed improvements and if they'd like me to apply them *now* using the appropriate tool (`replace_in_file` or `write_to_file`). Apply changes if approved, then proceed to `attempt_completion`.

**Constraint:** Do not offer reflection if:
*   No `.clinerules` were active.
*   The task was very simple and involved no feedback.
