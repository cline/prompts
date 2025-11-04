---
description: An intelligent workflow to automatically calculate and apply a new project version, update core files and documentation, and prepare a release commit.
author: Frédéric Guigand
version: 1.3
tags: ["workflow", "release", "versioning", "semver", "changelog", "documentation", "automation"]
globs: ["package.json", "app-config.*", "CHANGELOG.md", "README.md", "docs/**/*.md", "versions.*json*"]
---

# Workflow: Intelligent Project Versioning & Documentation

This rule defines an automated, multi-step process for releasing a new version of the project. You MUST follow this logic precisely to ensure a correct and consistent release.

### Step 1: Determine New Version (Automated Logic)

Your primary task is to calculate the new version number. You MUST follow this decision tree in order:

1.  **Check for Explicit User Input:**
    - First, check if the user has provided an explicit version type (e.g., `major`, `minor`, `patch`, `fix`).
    - If yes, this is the highest priority. Proceed to calculate the new version based on this input.

2.  **Infer from `CHANGELOG.md`:**
    - If no explicit type is given, you MUST infer it by analyzing the content under the `[Unreleased]` section of `CHANGELOG.md`.
    - Apply the following Semantic Versioning logic:
        - If you find `BREAKING CHANGE:` text or a `### Removed` section, it MUST be a **MAJOR** increment.
        - If you find a `### Added` section, it MUST be a **MINOR** increment.
        - If you only find `### Fixed`, `### Security`, or other minor sections, it MUST be a **PATCH** increment.

3.  **Ask User on Ambiguity (Fallback):**
    - ⚠️ **If inference is ambiguous** (e.g., only a `### Changed` section exists), you **MUST NOT GUESS**.
    - Instead, you MUST ask the user for clarification. Present your analysis and provide clear choices.
    - **✅ Use this template for asking:**
      > "I have analyzed the changes in `[Unreleased]` and the version increment is ambiguous. Based on the changes, I suggest the following options:
      > - **MINOR (`X.Y.Z`):** Choose this for new, backward-compatible features.
      > - **PATCH (`A.B.C`):** Choose this for backward-compatible bug fixes.
      >
      > Please specify which version is correct."

### Step 2: Pre-flight Check & Confirmation

Before modifying any files, perform an internal verification and present a plan to the user.

1.  **Internal Verification:** Use a thinking block to confirm you have all necessary information.
    ```xml
    <thinking>
    1.  Current version source file identified (e.g., `package.json`).
    2.  Current version read: [e.g., 1.9.3]
    3.  Increment type determined: [e.g., minor (inferred)]
    4.  Calculated new version: [e.g., 1.10.0]
    5.  Required files are present and accessible.
    Plan is ready for execution.
    </thinking>
    ```
2.  **State Your Plan:** Present the confirmed new version number to the user and ask for final approval before writing any changes. For example: "I will increment the version to `1.10.0`. Is this correct?"

### Step 3: Execute Core File Modifications

Once the user confirms, proceed with the following precise file modifications.

1.  **Update Central Version Sources:**
    - Locate and update the version number in `package.json`.
    - Locate and update the version number and description in `versions.*`.
    - Locate and update the version number and description in `app-config.*`.

2.  **Update `CHANGELOG.md`:**
    - Create a new version heading below `[Unreleased]` using the format `## [X.Y.Z] - YYYY-MM-DD`.
    - Move the summarized changes from the `[Unreleased]` section to this new version section.
    - Update the version comparison link at the bottom of the file.
    - **Update the `Version` and `Last Updated` comments** at the top of the file.

3.  **Update Documentation File Headers:**
    - For all relevant documentation files (`README.md`, `TECHNICAL_GUIDE.md`, `DEVELOPER_GUIDE.md`, etc.), find and update the version badge and the `Version` / `Last Updated` comments in the header.
    - **✅ Badge Template:** `[![Version](https://img.shields.io/badge/version-NEW.VERSION.HERE-blue.svg)](CHANGELOG.md)`

### Step 4: 🧠 Intelligently Update Project Documentation

Your goal is to ensure all technical and maintenance documentation reflects the new changes, not just list them.

1.  **Analyze Changes:** Review the finalized changelog entries for this version.
2.  **Identify Affected Docs:** Scan the project for relevant documentation (e.g., files in `docs/`, `guides/`, or files like `ARCHITECTURE.md`, `MAINTENANCE.md`).
3.  **Synthesize and Propose Updates:** Based on the *type* of change, determine the required documentation update.
    - **`Added`**: If a new feature was added (e.g., caching), find the relevant document (e.g., `architecture.md`) and propose adding a new section explaining it. If new configuration is required, propose updates to the setup guide.
    - **`Changed`**: If a process was changed, locate its existing description and propose updates to reflect the new behavior (e.g., updating an API endpoint's documentation).
    - **`Removed`**: If a feature was removed, find its documentation and propose either removing the section or clearly marking it as deprecated with migration steps.
    - **`Fixed`**: Bug fixes typically do not require documentation updates unless they clarify a previously misunderstood behavior.
4.  **AWAIT USER APPROVAL:** 🚨 **CRITICAL:** You **MUST NOT** apply these changes directly. You MUST present a clear summary of the proposed documentation updates (e.g., as a `diff` or a before/after summary) to the user for review and approval before proceeding.

### Step 5: Prepare Git Commit Message

Once all file changes are approved and applied, prepare and output the following commit message text. **DO NOT execute the commit.**

**✅ Template:**
```
<version number> <short, descriptive title>

- A bulleted list summarizing the key feature/fix changes.
- Update project documentation to reflect new changes.
```

**Example Output:**
```
1.10.0 Introduce User Profile Caching

- Implemented Redis caching for user profile data to reduce database load.
- Added new environment variables for Redis connection.
- Updated ARCHITECTURE.md with details on the new caching layer.
