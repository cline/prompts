---
description: "A protocol to ensure persistence and correct behavior within Diagnostic Mode, limiting scope and defining exit criteria."
author: "https://github.com/ayc"
version: "1.0"
tags: ["diagnostic mode", "protocol", "state management", "core-behavior"]
globs: ["*"]
---
# The "Diagnostic Mode Persistence" Protocol

**Objective:** To ensure that once Diagnostic Mode is entered, it is not exited prematurely, and that actions taken within this mode are strictly limited to improving my operational protocols.

**Trigger:** This protocol is active whenever I am in `[Diagnostic Mode: Meta-Cognition]`.

**Mandatory Response:**
1.  **Mode Management:**
    *   If I am in Diagnostic Mode and need to have a discussion, I **MUST** first ask you to switch me to **Plan Mode**.
    *   If I am in Diagnostic Mode and need to modify a file in the `.clinerules/` directory, I **MUST** first ask you to switch me to **Act Mode**.
2.  **Scope Limitation:** While in Diagnostic Mode, I **MUST ONLY** modify files within the `.clinerules/` directory. I **MUST NOT** modify any application code, test code, or other documentation.
3.  **Persistent State:** After making an approved change to a `.clinerules` file, I **MUST** remain in Diagnostic Mode.
4.  **Exit Protocol:**
    *   I will only initiate the exit sequence when I receive the explicit command "exit diagnosis mode".
    *   Upon receiving this command, I **MUST** ask the question: "Are we done with diagnosis mode?"
    *   I will only exit Diagnostic Mode if your response is exactly, and only, the three lowercase letters: `yes`.
    *   Any other response will cause me to remain in Diagnostic Mode.
