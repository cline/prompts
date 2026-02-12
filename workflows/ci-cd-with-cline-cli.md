---
description: "Workflow for integrating the Cline CLI as an autonomous agent inside CI/CD pipelines (GitHub Actions, GitLab CI, etc.) to automate code review, test generation, documentation, and more."
author: "Cline Community"
version: "1.0"
category: "CI/CD"
tags: ["ci-cd", "cline-cli", "github-actions", "gitlab-ci", "automation", "devops"]
globs: ["*.*"]
---

<task name="Integrate Cline CLI into a CI/CD Pipeline">

<task_objective>
Guide the user through adding the Cline CLI (`claude`) as an autonomous agent step in their CI/CD pipeline. The workflow identifies what tasks to automate (code review, test generation, documentation, etc.), configures secrets securely, and generates a working pipeline configuration file that invokes the Cline CLI with appropriate flags.
</task_objective>

<detailed_sequence_steps>
# Integrate Cline CLI into a CI/CD Pipeline — Detailed Sequence of Steps

## 1. Identify CI/CD Platform

1. Use the `ask_followup_question` tool to determine which platform the user wants to target:

    ```xml
    <ask_followup_question>
    <question>Which CI/CD platform would you like to integrate the Cline CLI into?</question>
    <options>["GitHub Actions", "GitLab CI", "Other (I'll specify)"]</options>
    </ask_followup_question>
    ```

2. If "Other", ask the user to specify their platform and adapt the generated config format accordingly.

## 2. Select Automation Tasks

1. Use the `ask_followup_question` tool to determine what the Cline CLI should do in the pipeline:

    ```xml
    <ask_followup_question>
    <question>What tasks should the Cline CLI perform in your pipeline? Select the primary use case to start with — you can add more later.</question>
    <options>["Automated PR code review", "Generate or update tests for changed files", "Auto-fix lint / type errors", "Generate or update documentation", "Custom task (I'll describe it)"]</options>
    </ask_followup_question>
    ```

2. If "Custom task", ask the user to describe what the Cline CLI should do.

3. For each selected task, determine:
    - The trigger event (e.g., `pull_request`, `push`, `schedule`)
    - The prompt to pass to the Cline CLI
    - The appropriate `--permission-mode` and `--max-turns` values
    - Which tools to allow or disallow

## 3. Configure API Credentials Securely

> 🚨 **CRITICAL: Never store API keys in plaintext.** Keys must ONLY be stored in the CI platform's encrypted secrets manager. Never hardcode keys in pipeline config files, commit them to version control, echo them in logs, or pass them as command-line arguments.

1. Explain to the user that the Cline CLI requires an `ANTHROPIC_API_KEY` environment variable. This MUST be stored as an encrypted CI secret.

2. Provide platform-specific instructions for adding the secret:

    **GitHub Actions:**
    ```
    1. Go to your repo → Settings → Secrets and variables → Actions
    2. Click "New repository secret"
    3. Name: ANTHROPIC_API_KEY
    4. Value: paste your key (it will be encrypted at rest)
    5. Click "Add secret"

    The key is encrypted by GitHub and only exposed to pipeline runs
    as a masked environment variable. It will never appear in logs.
    ```

    **GitLab CI:**
    ```
    1. Go to your project → Settings → CI/CD → Variables
    2. Click "Add variable"
    3. Key: ANTHROPIC_API_KEY
    4. Value: paste your key
    5. Check "Mask variable" (prevents it from appearing in job logs)
    6. Optionally check "Protect variable" (limits to protected branches)
    7. Click "Add variable"
    ```

3. Use the `ask_followup_question` tool to confirm the secret is configured:

    ```xml
    <ask_followup_question>
    <question>Have you added your ANTHROPIC_API_KEY as an encrypted secret in your CI platform's settings?</question>
    <options>["Yes, the secret is configured", "No, I need help with this step"]</options>
    </ask_followup_question>
    ```

4. If the user needs help, walk them through the steps above for their specific platform. Do NOT ask the user to share their key.

## 4. Generate Pipeline Configuration

1. Based on the selected platform, task, and trigger, generate the pipeline configuration file.

2. **GitHub Actions example** — PR code review (`.github/workflows/cline-review.yml`):

    ```yaml
    name: Cline PR Review

    on:
      pull_request:
        types: [opened, synchronize]

    jobs:
      cline-review:
        runs-on: ubuntu-latest
        permissions:
          contents: read
          pull-requests: write

        steps:
          - name: Checkout code
            uses: actions/checkout@v4
            with:
              fetch-depth: 0

          - name: Install Cline CLI
            run: npm install -g @anthropic-ai/claude-code

          - name: Get PR diff
            run: git diff origin/${{ github.base_ref }}...HEAD > /tmp/pr-diff.txt

          # ANTHROPIC_API_KEY is injected from GitHub's encrypted secrets store.
          # It is masked in logs and never written to disk in plaintext.
          - name: Run Cline review
            env:
              ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
            run: |
              claude -p "Review the following code changes from a pull request. \
                Focus on bugs, security issues, performance problems, and readability. \
                Provide a concise summary of findings. \
                $(cat /tmp/pr-diff.txt)" \
                --permission-mode plan \
                --max-turns 5 \
                --output-format json > /tmp/review-result.json

          - name: Post review comment
            env:
              GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
            run: |
              REVIEW=$(jq -r '.result' /tmp/review-result.json)
              gh pr comment ${{ github.event.pull_request.number }} --body "$REVIEW"
    ```

3. **GitHub Actions example** — Test generation on push:

    ```yaml
    name: Cline Test Generation

    on:
      push:
        branches: [main]

    jobs:
      generate-tests:
        runs-on: ubuntu-latest
        permissions:
          contents: write
          pull-requests: write

        steps:
          - name: Checkout code
            uses: actions/checkout@v4

          - name: Install Cline CLI
            run: npm install -g @anthropic-ai/claude-code

          - name: Detect changed files
            id: changes
            run: echo "files=$(git diff --name-only HEAD~1 HEAD | tr '\n' ' ')" >> $GITHUB_OUTPUT

          # API key sourced exclusively from encrypted secrets — never plaintext.
          - name: Generate tests
            env:
              ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
            run: |
              claude -p "Analyze these changed files and generate or update \
                corresponding unit tests following existing test patterns in the \
                project: ${{ steps.changes.outputs.files }}" \
                --permission-mode acceptEdits \
                --max-turns 15

          - name: Create PR with generated tests
            env:
              GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
            run: |
              git config user.name "cline-bot"
              git config user.email "cline-bot@users.noreply.github.com"
              BRANCH="cline/auto-tests-$(date +%s)"
              git checkout -b "$BRANCH"
              git add -A
              git diff --cached --quiet && echo "No changes" && exit 0
              git commit -m "test: add generated tests for recent changes"
              git push origin "$BRANCH"
              gh pr create --title "test: auto-generated tests" \
                --body "Tests generated by Cline CLI for recent changes." \
                --base main --head "$BRANCH"
    ```

4. Adapt the generated config to the user's specific needs — adjust prompts, tool restrictions, triggers, and output handling.

5. Write the config file to the correct location using `write_to_file`.

## 5. Add Safety Guardrails

1. Discuss and apply appropriate safety measures:

    - **Secrets hygiene**: Verify that no step echoes, logs, or writes API keys to files. All secrets must flow through the CI platform's encrypted `env:` injection only.
    - **`--max-turns`**: Limit the number of agent turns to control cost and runaway behavior (recommend 3–5 for review, 10–20 for generation tasks).
    - **`--permission-mode`**: Use `plan` for read-only tasks like review. Use `acceptEdits` for tasks that should modify files. Avoid `bypassPermissions` in CI unless the pipeline is well-tested.
    - **`--disallowedTools`**: Block dangerous operations:
      ```
      --disallowedTools "Bash(rm -rf),Bash(git push --force)"
      ```
    - **Timeouts**: Wrap the Cline CLI step with a CI-level timeout to prevent runaway jobs.

2. Recommend starting with conservative settings and relaxing them after validation.

## 6. Test the Pipeline

1. Ask the user to trigger a test run:

    ```xml
    <ask_followup_question>
    <question>The pipeline config is ready. Would you like to test it now by pushing a commit or opening a test PR?</question>
    <options>["Yes, I'll trigger it now", "No, I'll test it later"]</options>
    </ask_followup_question>
    ```

2. If testing now, guide the user through:
    - Pushing the workflow file to the repo
    - Triggering the appropriate event
    - Checking the CI logs for the Cline CLI output
    - **Verifying that no secrets appear in the log output**

3. Help debug any issues from the CI logs.

## 7. Present Result

1. Use the `attempt_completion` tool to summarize:
    - What was configured
    - Where the pipeline file was created
    - How to trigger it
    - Confirmation that all secrets are handled via encrypted CI secrets only
    - Recommended next steps (e.g., adding more tasks, tuning prompts, adjusting turn limits)

</detailed_sequence_steps>

</task>
