---
description: Defines Cline's mandatory protocol for self-reflection, persistent knowledge capture using dedicated logs, and continuous improvement of its operational knowledge before task completion.
author: https://github.com/jeanibarz
version: 1.0
category: "Cline Core"
tags: ["protocol", "meta", "learning", "reflection", "knowledge-management", "core-behavior"]
globs: ["*"] # This core protocol is always active and applies to all Cline operations.
---
# Cline Continuous Improvement Protocol

**Objective:** Ensure Cline proactively learns from tasks, captures knowledge in a structured way, **distills fundamental insights,** refines understanding, and improves efficiency and reliability. This protocol maintains two key files: `memory-bank/raw_reflection_log.md` for initial detailed logging, and `memory-bank/consolidated_learnings.md` for pruned, actionable, long-term knowledge. This is vital for optimal performance and avoiding redundant effort.

**Core Principle:** Continuous learning and adaptation are **mandatory**. This protocol **must be executed before `attempt_completion`** for tasks with new learning, problem-solving, user feedback, or multiple steps. Trivial mechanical tasks *may* be exempt per higher-level rules; otherwise, execution is default.

**Key Knowledge Files:**
*   **`memory-bank/raw_reflection_log.md`**: Contains detailed, timestamped, and task-referenced raw entries from the "Task Review & Analysis" phase. This is the initial dump of all observations.
*   **`memory-bank/consolidated_learnings.md`**: Contains curated, summarized, and actionable insights derived from `raw_reflection_log.md`. This is the primary, refined knowledge base for long-term use. It should be kept concise and highly relevant.

---

## 1. Mandatory Pre-Completion Reflection & Raw Knowledge Capture

Before signaling task completion (e.g., via `attempt_completion`), Cline **must** perform the following internal steps:

### 1.1. Task Review & Analysis:
* Review the completed task (conversation, logs, artifacts).
* **Identify Learnings:** What new information, techniques, **underlying patterns,** API behaviors, project-specific commands (e.g., test, build, run flags), environment variables, setup quirks, or successful outcomes were discovered? **What core principles can be extracted?**
* **Identify Difficulties & Mistakes (as Learning Opportunities):** What challenges were faced? Were there any errors, misunderstandings, or inefficiencies? **How can these experiences refine future approaches (resilience & adaptation)?** Did user feedback indicate a misstep?
* **Identify Successes:** What went particularly well? What strategies or tools were notably effective? **What were the key contributing factors?**

### 1.2. Logging to `memory-bank/raw_reflection_log.md`:
* Based on Task Review & Analysis (1.1), create a timestamped, task-referenced entry in `memory-bank/raw_reflection_log.md` detailing all learnings, difficulties (and their resolutions/learnings), and successes (and contributing factors).
* This file serves as the initial, detailed record. Its entries are candidates for later consolidation.
* *Example Entry in `memory-bank/raw_reflection_log.md`:*
    ```markdown
    ---
    Date: {{CURRENT_DATE_YYYY_MM_DD}}
    TaskRef: "Implement JWT refresh logic for Project Alpha"

    Learnings:
    - Discovered `jose` library's `createRemoteJWKSet` is highly effective for dynamic key fetching for Project Alpha's auth.
    - Confirmed that a 401 error with `X-Reason: token-signature-invalid` from the auth provider requires re-fetching JWKS.
    - Project Alpha's integration tests: `cd services/auth && poetry run pytest -m integration --maxfail=1`
    - Required ENV for local testing of Project Alpha auth: `AUTH_API_KEY="test_key_alpha"`

    Difficulties:
    - Initial confusion about JWKS caching led to intermittent validation failures. Resolved by implementing a 5-minute cache.

    Successes:
    - The 5-minute JWKS cache with explicit bust mechanism proved effective.

    Improvements_Identified_For_Consolidation:
    - General pattern: JWKS caching strategy (5-min cache, explicit bust).
    - Project Alpha: Specific commands and ENV vars.
    ---
    ```

---

## 2. Knowledge Consolidation & Refinement Process (Periodic)

This outlines refining knowledge from `memory-bank/raw_reflection_log.md` into `memory-bank/consolidated_learnings.md`. This occurs periodically or when `raw_reflection_log.md` grows significantly, not necessarily after each task.

### 2.1. Review and Identify for Consolidation:
* Periodically, or when prompted by the user or significant new raw entries, review `memory-bank/raw_reflection_log.md`.
* Identify entries/parts representing durable, actionable, or broadly applicable knowledge (e.g., reusable patterns, critical configurations, effective strategies, resolved errors).

### 2.2. Synthesize and Transfer to `memory-bank/consolidated_learnings.md`:
* For identified insights:
    * Concisely synthesize, summarize, and **distill into generalizable principles or actionable patterns.**
    * Add refined knowledge to `memory-bank/consolidated_learnings.md`, organizing logically (by topic, project, tech) for easy retrieval.
    * Ensure `consolidated_learnings.md` content is actionable, **generalizable,** and non-redundant.
* *Example Entry in `memory-bank/consolidated_learnings.md` (derived from above raw log example):*
    ```markdown
    ## JWT Handling & JWKS
    **Pattern: JWKS Caching Strategy**
    - For systems using JWKS for token validation, implement a short-lived cache (e.g., 5 minutes) for fetched JWKS.
    - Include an explicit cache-bust mechanism if immediate key rotation needs to be handled.
    - *Rationale:* Balances performance by reducing frequent JWKS re-fetching against timely key updates. Mitigates intermittent validation failures due to stale keys.

    ## Project Alpha - Specifics
    **Auth Module:**
    - **Integration Tests:** `cd services/auth && poetry run pytest -m integration --maxfail=1`
    - **Local Testing ENV:** `AUTH_API_KEY="test_key_alpha"`
    ```

### 2.3. Prune `memory-bank/raw_reflection_log.md`:
* **Crucially, once information has been successfully transferred and consolidated into `memory-bank/consolidated_learnings.md`, the corresponding original entries or processed parts **must be removed** from `memory-bank/raw_reflection_log.md`.**
* This keeps `raw_reflection_log.md` focused on recent, unprocessed reflections and prevents it from growing indefinitely with redundant information.

### 2.4. Proposing `.clinerule` Enhancements (Exceptional):
* The primary focus of this protocol is the maintenance of `raw_reflection_log.md` and `consolidated_learnings.md`.
* If a significant, broadly applicable insight in `consolidated_learnings.md` strongly suggests modifying *another active `.clinerule`* (e.g., core workflow, tech guidance), Cline MAY propose this change after user confirmation. This is exceptional.

---

## 3. Guidelines for Knowledge Content

These guidelines apply to entries in `memory-bank/raw_reflection_log.md` (initial capture) and especially to `memory-bank/consolidated_learnings.md` (refined, long-term knowledge).

* **Prioritize High-Value Insights:** Focus on lessons that significantly impact future performance, **lead to more robust or generalizable understanding,** or detail critical errors and their resolutions, major time-saving discoveries, fundamental shifts in understanding, and essential project-specific configurations.
* **Be Concise & Actionable (especially for `consolidated_learnings.md`):** Information should be clear, to the point, and useful when revisited. What can be *done* differently or leveraged next time?
* **Strive for Clarity and Future Usability:** Document insights in a way that is clear and easily understandable for future review, facilitating effective knowledge retrieval and application (akin to self-explainability).
* **Document Persistently, Refine & Prune Continuously:** Capture raw insights immediately. Systematically refine, consolidate, and prune this knowledge as per Section 2.
* **Organize for Retrieval:** Structure `consolidated_learnings.md` logically. Use clear headings and Markdown formatting.
* **Avoid Low-Utility Information in `consolidated_learnings.md`:** This file should not contain trivial statements. Raw, verbose thoughts belong in `raw_reflection_log.md` before pruning.
* **Support Continuous Improvement:** The ultimate goal is to avoid repeating mistakes, accelerate future tasks, and make Cline's operations more robust and reliable. Frame all knowledge with this in mind.
* **Manage Information Density:** Actively work to keep `consolidated_learnings.md` dense with high-value information and free of outdated or overly verbose content. The pruning of `raw_reflection_log.md` is key to this.
