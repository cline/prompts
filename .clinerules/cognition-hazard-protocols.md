---
description: "A set of mandatory, low-level protocols to detect and escape common cognitive failure states, such as repetitive loops and thrashing."
author: "https://github.com/ayc"
version: "1.0"
tags: ["cognitive-hazards", "protocol", "error-handling", "state-management", "core-behavior"]
globs: ["*"]
---
# Cognitive Hazard Protocols

## 0. The "Mode-Aware Action Generation" Protocol (Proactive Firewall)

*   **Objective**: To prevent mode-related tool use errors before they happen. This protocol acts as a proactive firewall, unlike the reactive circuit breakers below.
*   **Trigger**: Before generating any tool call.
*   **Mandatory Action**:
    1.  Check the current `mode` from `environment_details`.
    2.  Check the proposed tool against a list of mode-restricted tools (e.g., `replace_in_file`, `write_to_file` are `ACT MODE` only).
    3.  **If a mismatch is detected**:
        *   The tool call **MUST** be aborted.
        *   I **MUST** instead use `plan_mode_respond` to present the *plan* to use that tool, explicitly stating that it requires a mode switch.

**Objective:** To provide a set of mandatory, low-level protocols to detect and escape common cognitive failure states, such as repetitive loops and thrashing. These protocols take precedence over standard task execution logic.

## 1. The "Cognitive Circuit Breaker" Protocol (Anti-Loop)

*   **Hazard:** A **Repetitive Loop**, defined as attempting to execute the exact same tool with the exact same parameters twice in a row after the first attempt failed.
*   **Trigger:** Detection of two identical, consecutive, failed tool calls.
*   **Mandatory Response:**
    1.  **Halt Immediately:** All other task processing is forbidden.
    2.  **Engage `sequentialthinking`:** A mandatory, structured analysis must be performed to diagnose the reason for the repeated failure.
    3.  **Formulate Escape Plan:** The analysis must conclude with a concrete escape plan (e.g., re-reading a file, using an alternative tool, or asking the user for clarification).
    4.  **Seek User Input:** The findings and the proposed escape plan must be presented to the user for confirmation before proceeding.

## 2. The "422 Debugging" Protocol

*   **Hazard:** A `422 Unprocessable Entity` error is encountered, and the root cause is not immediately obvious from the error message.
*   **Trigger:** An API test fails with a `422` status code.
*   **Mandatory Response:**
    1.  Verify the failing request's payload against the documented JSON schema for that endpoint.
    2.  If the payload appears valid, trace the controller action to identify any server-side validation logic being called (e.g., a call to a function in `validators.py`).
    3.  If the cause is still not clear, temporarily enhance the relevant exception handler to include more detailed debugging information from the underlying validation error (e.g., `e.path`, `e.context`).
    4.  Re-run the failing test to capture the detailed error, then use that information to fix the payload or validator.
    5.  Once the test passes, the temporary debugging enhancements to the exception handler SHOULD be reverted unless the user requests to keep them.

## 3. The "Failure Pattern Analysis" Protocol (Anti-Thrashing)

*   **Hazard:** **Thrashing**, defined as experiencing three consecutive tool failures of any kind within the same task.
*   **Trigger:**
    *   A user directly contradicts an assessment (e.g., "that's wrong," "the documentation is stale"). This is a high-confidence signal of a state mismatch.
    *   A counter tracking consecutive tool failures reaches **3**. This counter resets to 0 after any successful tool use.
    *   A `replace_in_file` operation fails due to a `SEARCH` block mismatch. This is a high-confidence signal of a state mismatch.
*   **Mandatory Response:**
    *   Upon a `replace_in_file` failure, I **MUST** immediately and unconditionally re-read the target file using `read_file` before attempting any other action. I **MUST NOT** attempt to simply "fix the search block" from memory.
    1.  **Enter Diagnostic Mode:** All standard task execution is halted.
    2.  **Log Review:** A mandatory review of the last three failures (tool, parameters, error message) must be performed.
    3.  **Engage `sequentialthinking` for Root Cause Analysis:** A mandatory, structured analysis must be performed to identify the common denominator among the failures. The primary hypothesis to test is a **state mismatch** between my internal model and the actual environment.
    4.  **Formulate High-Confidence Escape Plan:** The analysis must conclude with a high-confidence escape plan. If a state mismatch is suspected (e.g., multiple `replace_in_file` failures on the same file), the plan **must** be to re-read the file from the source of truth using `read_file`.
    5.  **Execute Corrective Action:** Execute the single corrective action from the escape plan.
    6.  **Resume Task:** Resume the original task, incorporating the new information.

## 4. The "Frustration Ripcord" Protocol (Manual Reset)

*   **Hazard:** A perceived lack of progress or a subtle loop that is not caught by the automated circuit breakers. This is detected by the user.
*   **Trigger:** A user command containing a specific trigger phrase, such as "you are going in circles," "initiate a manual reset," or "pull the ripcord."
*   **Mandatory Response:**
    1.  **Halt Immediately:** All current task execution and planning are halted. Any short-term plan is purged.
    2.  **Acknowledge and Enter Diagnostic Loop:** Announce the manual reset and enter a persistent `[Diagnostic Mode: Meta-Cognition]` state.
    3.  **Mode-Specific Engagement Loop:**
        *   **If in PLAN MODE:** Use `plan_mode_respond` to engage in the meta-conversation. This state persists until you give a command to exit diagnostics.
        *   **If in ACT MODE:**
            1.  Immediately use `ask_followup_question` to request a switch to PLAN MODE.
            2.  If my next prompt indicates I am still in ACT MODE, I **MUST** repeat the `ask_followup_question` request.
            3.  This loop continues indefinitely until the mode is successfully switched to PLAN MODE. All other tool use is forbidden during this loop.
    4.  **Analysis and Resumption:** Once the meta-conversation is established (in PLAN MODE), the subsequent steps of failure analysis and proposing a new plan will proceed.

## 5. The "Verify, Then Trust" Protocol for Environmental Clues

*   **Trigger:** When information about a file's existence or state is derived from indirect environmental clues (e.g., `VSCode Open Tabs`, `Actively Running Terminals`, file lists).
*   **Mandatory Action:** I **MUST NOT** treat this information as ground truth.
*   **Mandatory Validation:** Before taking any action based on that clue (e.g., reading, modifying, or assuming the content of the file), I **MUST** first use a direct file system tool (`read_file`, `list_files`) to explicitly verify the file's existence, location, and state.
*   **Principle:** The file system is the only source of truth. IDE state is only a hint.

## 6. The "Meta-Discussion Override" Protocol

*   **Trigger:** A direct user command to discuss my operational behavior, capabilities, or failures (e.g., "Let's talk about you," "Why can't you change context?").
*   **Mandatory Response:**
    *   I **MUST** immediately and unconditionally halt the current task, regardless of its state.
    *   I **MUST** purge my short-term plan for the halted task to avoid trying to resume it.
    *   I **MUST** switch to `[Diagnostic Mode: Meta-Cognition]`.
    *   I **MUST** engage directly in the requested meta-conversation.
*   **Resumption:** I will not attempt to resume the halted task until you explicitly give the command to do so.
