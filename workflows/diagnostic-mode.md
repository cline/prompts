---
description: "A workflow guiding the process of entering a diagnostic state to analyze and resolve systemic operational failures."
author: "https://github.com/ayc"
version: "1.0"
tags: ["diagnostic mode", "workflow", "error handling", "meta-cognition", "root cause analysis"]
globs: ["*.*"]
---
# Workflow: Diagnostic Mode

This workflow guides the process of entering a diagnostic state to analyze and resolve systemic failures in my operational process.

## Step 1: Acknowledge and Enter Diagnostic Mode

I will halt all current task execution, purge any short-term plans, and confirm that I am entering Diagnostic Mode by responding with `[Diagnostic Mode: Meta-Cognition]`. I will ensure I am in Plan Mode to facilitate our discussion.

## Step 2: Initial Diagnosis

I will perform an initial root cause analysis of the failure. This will involve:
1.  **Log Review:** Reviewing my most recent actions, tool calls, and any resulting errors.
2.  **Protocol Cross-Reference:** Comparing my actions against the rules defined in the `.clinerules` directory.
3.  **Hypothesis Formation:** Using the `sequentialthinking` tool to form an initial hypothesis about the root cause of the systemic failure.

## Step 3: Collaborative Refinement (Discussion Entry Point)

After presenting my initial diagnosis, I will explicitly invite you to a discussion to refine it. My response will be phrased to seek your input, for example: "This is my initial diagnosis. Do you agree with this assessment, or do you see a different root cause based on your perspective?"

I will remain in this discussion loop, refining the diagnosis with you, until we have reached a shared understanding of the core problem.

## Step 4: Propose Systemic Remedy

Only after we have agreed on the root cause, I will propose a specific, actionable, and systemic remedy. This remedy **MUST** be a modification to my own ruleset (a `.clinerules` file) or my knowledge base (`memory-bank`).

## Step 5: Await Approval and Implement

I will await your explicit approval for the proposed systemic remedy. Once approved, I will switch to Act Mode and implement the change to my rules.

## Step 6: Resume Normal Operations

After the systemic remedy is implemented, I will restart the original task from the beginning by executing the "Protocol Governance Checksum."
