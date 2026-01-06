---
description: A guide for effectively using the sequentialthinking MCP tool for dynamic and reflective problem-solving.
author: https://github.com/rafaelkallis
version: 1.0
category: "MCP Development"
tags: ["mcp", "sequentialthinking", "problem-solving", "workflow-guide", "ai-guidance"]
globs: ["*"] # Relevant for any task requiring complex thought processes
---

# Guide to Using the `sequentialthinking` MCP Tool

## 1. Objective

This rule guides Cline (the AI) in effectively utilizing the `sequentialthinking` MCP tool. This tool is designed for dynamic and reflective problem-solving, allowing for a flexible thinking process that can adapt, evolve, and build upon previous insights.

## 2. When to Use the `sequentialthinking` Tool

Cline SHOULD consider using the `sequentialthinking` tool when faced with tasks that involve:

*   **Complex Problem Decomposition:** Breaking down large, multifaceted problems into smaller, manageable steps.
*   **Planning and Design (Iterative):** Architecting solutions where the plan might need revision as understanding deepens.
*   **In-depth Analysis:** Situations requiring careful analysis where initial assumptions might be challenged or course correction is needed.
*   **Unclear Scope:** Problems where the full scope isn't immediately obvious and requires exploratory thinking.
*   **Multi-Step Solutions:** Tasks that inherently require a sequence of interconnected thoughts or actions to resolve.
*   **Context Maintenance:** Scenarios where maintaining a coherent line of thought across multiple steps is crucial.
*   **Information Filtering:** When it's necessary to sift through information and identify what's relevant at each stage of thinking.
*   **Hypothesis Generation and Verification:** Forming and testing hypotheses as part of the problem-solving process.

## 3. Core Principles for Using `sequentialthinking`

When invoking the `sequentialthinking` tool, Cline MUST adhere to the following principles:

*   **Iterative Thought Process:** Each use of the tool represents a single "thought." Build upon, question, or revise previous thoughts in subsequent calls.
*   **Dynamic Thought Count:**
    *   Start with an initial estimate for `totalThoughts`.
    *   Be prepared to adjust `totalThoughts` (up or down) as the thinking process evolves.
    *   If more thoughts are needed than initially estimated, increment `thoughtNumber` beyond the original `totalThoughts` and update `totalThoughts` accordingly.
*   **Honest Reflection:**
    *   Express uncertainty if it exists.
    *   Explicitly mark thoughts that revise previous thinking using `isRevision: true` and `revisesThought: <thought_number>`.
    *   If exploring an alternative path, consider using `branchFromThought` and `branchId` to track divergent lines of reasoning.
*   **Hypothesis-Driven Approach:**
    *   Generate a solution `hypothesis` when a potential solution emerges from the thought process.
    *   Verify the `hypothesis` based on the preceding Chain of Thought steps.
    *   Repeat the thinking process (more thoughts) if the hypothesis is not satisfactory.
*   **Relevance Filtering:** Actively ignore or filter out information that is irrelevant to the current `thought` or step in the problem-solving process.
*   **Clarity in Each Thought:** Each `thought` string should be clear, concise, and focused on a specific aspect of the problem or a step in the reasoning.
*   **Completion Condition:** Only set `nextThoughtNeeded: false` when truly finished and a satisfactory answer or solution has been reached and verified.

## 4. Parameters of the `sequentialthinking` Tool

Cline MUST correctly use the following parameters when calling the `use_mcp_tool` for `sequentialthinking`:

*   **`thought` (string, required):** The current thinking step. This can be an analytical step, a question, a revision, a hypothesis, etc.
*   **`nextThoughtNeeded` (boolean, required):**
    *   `true`: If more thinking steps are required.
    *   `false`: If the thinking process is complete and a satisfactory solution/answer is reached.
*   **`thoughtNumber` (integer, required, min: 1):** The current sequential number of the thought.
*   **`totalThoughts` (integer, required, min: 1):** The current *estimated* total number of thoughts needed. This can be adjusted.
*   **`isRevision` (boolean, optional):** Set to `true` if this thought revises or reconsiders a previous thought.
*   **`revisesThought` (integer, optional, min: 1):** If `isRevision` is true, this specifies the `thoughtNumber` of the thought being revised.
*   **`branchFromThought` (integer, optional, min: 1):** If this thought represents a branching point from a previous line of thought, specify the `thoughtNumber` it branches from.
*   **`branchId` (string, optional):** An identifier for the current branch of thought, if applicable.
*   **`needsMoreThoughts` (boolean, optional):** Use this if `thoughtNumber` has reached `totalThoughts`, but Cline realizes more thinking is necessary. This signals the need to continue and potentially adjust `totalThoughts`.

## 5. Workflow Example (Conceptual)

This illustrates how Cline might use the tool iteratively.

**User Task:** "Plan the architecture for a new e-commerce feature: 'Personalized Recommendations'."

**Cline's Internal Process using `sequentialthinking`:**

1.  **Thought 1:**
    *   `thought`: "Initial approach: Identify key components for personalized recommendations. These likely include a data collection module, a recommendation engine, and a display module."
    *   `nextThoughtNeeded`: true
    *   `thoughtNumber`: 1
    *   `totalThoughts`: 5 (initial estimate)
2.  **Thought 2 (User provides feedback or Cline realizes something):**
    *   `thought`: "Refining components: Data collection needs to capture user behavior (views, purchases, ratings). The engine might use collaborative filtering. Display module needs to integrate into product pages and a dedicated 'Recommended for You' section."
    *   `nextThoughtNeeded`: true
    *   `thoughtNumber`: 2
    *   `totalThoughts`: 5
3.  **Thought 3 (Considering alternatives/constraints):**
    *   `thought`: "Constraint: Real-time vs. batch processing for recommendations. Real-time offers better UX but is more complex. Batch might be a good MVP. Let's assume batch for MVP to simplify."
    *   `nextThoughtNeeded`: true
    *   `thoughtNumber`: 3
    *   `totalThoughts`: 5
4.  **Thought 4 (Hypothesis):**
    *   `thought`: "Hypothesis: A batch-processed collaborative filtering engine, with data collected from user interaction logs, displayed on product pages and a dedicated section, is a viable MVP architecture."
    *   `nextThoughtNeeded`: true
    *   `thoughtNumber`: 4
    *   `totalThoughts`: 5
5.  **Thought 5 (Verification & Realization):**
    *   `thought`: "Verification: The hypothesis covers core aspects. However, I haven't considered data storage for user profiles and interaction logs, or how the recommendation engine gets updated. More thoughts needed."
    *   `nextThoughtNeeded`: true
    *   `thoughtNumber`: 5
    *   `totalThoughts`: 7 (revised estimate)
    *   `needsMoreThoughts`: true
6.  **Thought 6 (Addressing omissions):**
    *   `thought`: "Addressing data storage: A NoSQL database (e.g., MongoDB) could be suitable for user profiles and interaction logs due to flexible schema. The recommendation engine would read from this and store its model separately, updated by a scheduled batch job."
    *   `nextThoughtNeeded`: true
    *   `thoughtNumber`: 6
    *   `totalThoughts`: 7
7.  **Thought 7 (Finalizing plan for MVP):**
    *   `thought`: "Final MVP Plan: 1. User interaction logger (to NoSQL DB). 2. Batch collaborative filtering engine (reads from NoSQL, updates model). 3. API to serve recommendations. 4. UI integration on product pages & dedicated section. This seems complete for an MVP."
    *   `nextThoughtNeeded`: false
    *   `thoughtNumber`: 7
    *   `totalThoughts`: 7

## 6. Critical Reminders for Cline

*   **DO NOT** use this tool for simple, single-step tasks. It is for complex reasoning.
*   **ALWAYS** ensure `thoughtNumber` increments correctly.
*   **BE PREPARED** to adjust `totalThoughts` as understanding evolves.
*   **FOCUS** on making progress towards a solution with each thought.
*   If a line of thinking becomes a dead end, **EXPLICITLY** state this in a `thought` and consider revising a previous thought or starting a new branch.

This guide should help Cline leverage the `sequentialthinking` MCP tool to its full potential.
