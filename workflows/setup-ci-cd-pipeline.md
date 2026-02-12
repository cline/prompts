---
description: "Workflow that uses Cline to analyze a project's tech stack and generate a complete CI/CD pipeline configuration with appropriate stages for linting, testing, building, and deploying."
author: "Cline Community"
version: "1.0"
category: "CI/CD"
tags: ["ci-cd", "github-actions", "gitlab-ci", "devops", "pipeline", "automation", "setup"]
globs: ["*.*"]
---

<task name="Set Up a CI/CD Pipeline for Your Project">

<task_objective>
Analyze the user's project to detect its tech stack, test frameworks, and build tools, then generate a complete CI/CD pipeline configuration file with appropriate stages (lint, test, build, deploy). The output is a ready-to-use pipeline config committed to the project.
</task_objective>

<detailed_sequence_steps>
# Set Up a CI/CD Pipeline — Detailed Sequence of Steps

## 1. Detect Project Tech Stack

1. Scan the project root for configuration files that reveal the tech stack:

    ```bash
    ls -la package.json pyproject.toml Cargo.toml go.mod Gemfile pom.xml build.gradle Makefile Dockerfile docker-compose.yml 2>/dev/null
    ```

2. Read relevant config files to identify:
    - **Language & runtime** (Node.js, Python, Rust, Go, Ruby, Java, etc.)
    - **Package manager** (npm, pnpm, yarn, uv, pip, cargo, etc.)
    - **Test framework** (jest, vitest, pytest, go test, rspec, junit, etc.)
    - **Linter / formatter** (eslint, prettier, ruff, black, clippy, etc.)
    - **Build tool** (vite, webpack, tsc, setuptools, cargo build, etc.)
    - **Containerization** (Dockerfile, docker-compose)

3. Read existing CI config files if present to understand current state:

    ```bash
    ls -la .github/workflows/ .gitlab-ci.yml .circleci/ Jenkinsfile 2>/dev/null
    ```

4. Present a summary of findings to the user for confirmation.

## 2. Select CI/CD Platform

1. Use the `ask_followup_question` tool to determine the target platform:

    ```xml
    <ask_followup_question>
    <question>Which CI/CD platform should I generate a pipeline for?</question>
    <options>["GitHub Actions", "GitLab CI", "Other (I'll specify)"]</options>
    </ask_followup_question>
    ```

## 3. Define Pipeline Stages

1. Based on the detected tech stack, propose a set of pipeline stages. A typical pipeline includes:

    | Stage | Purpose | Example Commands |
    |-------|---------|-----------------|
    | **Install** | Install dependencies | `npm ci`, `uv sync`, `pip install` |
    | **Lint** | Static analysis & formatting | `eslint .`, `ruff check .`, `cargo clippy` |
    | **Test** | Run test suite | `npm test`, `pytest`, `go test ./...` |
    | **Build** | Compile / bundle | `npm run build`, `cargo build --release` |
    | **Deploy** | Ship to environment | `docker push`, `aws deploy`, `vercel deploy` |

2. Present the proposed stages and ask for confirmation:

    ```xml
    <ask_followup_question>
    <question>Based on your project, I recommend these pipeline stages:

    1. **Install** — Install dependencies
    2. **Lint** — Run linter/formatter checks
    3. **Test** — Run the test suite
    4. **Build** — Build/compile the project

    Would you also like a deploy stage?</question>
    <options>["Yes, add a deploy stage", "No, just CI (lint + test + build)", "Let me customize the stages"]</options>
    </ask_followup_question>
    ```

3. If the user wants deployment, ask about the target:

    ```xml
    <ask_followup_question>
    <question>Where do you deploy this project?</question>
    <options>["Docker / Container Registry", "Vercel", "AWS (ECS, Lambda, S3, etc.)", "Google Cloud", "Custom server (SSH)", "Other (I'll specify)"]</options>
    </ask_followup_question>
    ```

## 4. Configure Triggers

1. Ask what events should trigger the pipeline:

    ```xml
    <ask_followup_question>
    <question>When should this pipeline run?</question>
    <options>["On every pull request", "On push to main/master", "On both PRs and pushes to main", "Custom (I'll specify)"]</options>
    </ask_followup_question>
    ```

## 5. Handle Secrets and Credentials Securely

> 🚨 **CRITICAL: All sensitive credentials (API keys, deploy tokens, registry passwords) must ONLY be stored in the CI platform's encrypted secrets manager.** Never hardcode secrets in pipeline config files, commit them to version control, echo them in logs, or pass them as CLI arguments.

1. Based on the pipeline stages, identify which secrets are needed:
    - **Deploy stage**: Registry credentials, cloud provider tokens, SSH keys
    - **Cline CLI step** (if added): `ANTHROPIC_API_KEY`
    - **Notification integrations**: Webhook URLs, Slack tokens

2. For each required secret, instruct the user to add it through their platform's secrets UI:

    **GitHub Actions:**
    ```
    Go to repo → Settings → Secrets and variables → Actions → New repository secret
    Each secret is encrypted at rest and masked in job logs automatically.
    ```

    **GitLab CI:**
    ```
    Go to project → Settings → CI/CD → Variables → Add variable
    Enable "Mask variable" to prevent it from appearing in logs.
    Use "Protect variable" to restrict to protected branches if appropriate.
    ```

3. In the generated pipeline config, secrets are referenced ONLY via the platform's secrets syntax (e.g., `${{ secrets.MY_SECRET }}` for GitHub Actions, `$MY_SECRET` for masked GitLab variables). Never write secrets to files or intermediate outputs.

4. Do NOT ask the user to share any secret values. Only ask them to confirm secrets are configured.

## 6. Generate Pipeline Configuration

1. Based on all gathered information, generate the complete pipeline configuration.

2. **Example — GitHub Actions for a Node.js project** (`.github/workflows/ci.yml`):

    ```yaml
    name: CI

    on:
      push:
        branches: [main]
      pull_request:
        branches: [main]

    jobs:
      ci:
        runs-on: ubuntu-latest

        strategy:
          matrix:
            node-version: [20]

        steps:
          - name: Checkout code
            uses: actions/checkout@v4

          - name: Set up Node.js ${{ matrix.node-version }}
            uses: actions/setup-node@v4
            with:
              node-version: ${{ matrix.node-version }}
              cache: 'npm'

          - name: Install dependencies
            run: npm ci

          - name: Lint
            run: npm run lint

          - name: Run tests
            run: npm test

          - name: Build
            run: npm run build
    ```

3. **Example — GitHub Actions for a Python project** (`.github/workflows/ci.yml`):

    ```yaml
    name: CI

    on:
      push:
        branches: [main]
      pull_request:
        branches: [main]

    jobs:
      ci:
        runs-on: ubuntu-latest

        strategy:
          matrix:
            python-version: ["3.12"]

        steps:
          - name: Checkout code
            uses: actions/checkout@v4

          - name: Install uv
            uses: astral-sh/setup-uv@v4

          - name: Set up Python ${{ matrix.python-version }}
            run: uv python install ${{ matrix.python-version }}

          - name: Install dependencies
            run: uv sync --all-extras

          - name: Lint
            run: uv run ruff check .

          - name: Run tests
            run: uv run pytest
    ```

4. **Example — GitLab CI for a Node.js project** (`.gitlab-ci.yml`):

    ```yaml
    stages:
      - install
      - lint
      - test
      - build

    default:
      image: node:20

    install:
      stage: install
      script:
        - npm ci
      cache:
        key: $CI_COMMIT_REF_SLUG
        paths:
          - node_modules/

    lint:
      stage: lint
      script:
        - npm run lint

    test:
      stage: test
      script:
        - npm test

    build:
      stage: build
      script:
        - npm run build
      artifacts:
        paths:
          - dist/
    ```

5. Adapt the template to the user's actual project:
    - Use the exact commands found in their `package.json` scripts, `Makefile`, or equivalent
    - Include the correct language version
    - Add caching for dependencies
    - Add deployment steps if requested, referencing secrets ONLY via encrypted secret variables

6. If the user wants deployment, add the appropriate deploy job with:
    - Environment secrets injected via the CI platform's secrets mechanism
    - Conditions limiting deploy to the appropriate branch (e.g., only on push to main)
    - No plaintext credentials anywhere in the config

## 7. Optionally Add Cline CLI Automation

1. Ask if the user wants to add Cline CLI–powered automation steps:

    ```xml
    <ask_followup_question>
    <question>Would you like to also add a Cline CLI step to your pipeline for automated tasks like PR review or test generation? (This uses the Cline CLI as an AI agent in CI.)</question>
    <options>["Yes, add a Cline CLI step", "No, just the standard pipeline"]</options>
    </ask_followup_question>
    ```

2. If yes, reference the `ci-cd-with-cline-cli` workflow to add the appropriate step. Add a comment in the generated config pointing to that workflow for future customization.

3. Remind the user that the Cline CLI requires `ANTHROPIC_API_KEY` stored as an encrypted CI secret (see the `ci-cd-with-cline-cli` workflow for detailed setup).

## 8. Write and Validate

1. Write the generated pipeline config file to the correct location using `write_to_file`:
    - GitHub Actions: `.github/workflows/ci.yml`
    - GitLab CI: `.gitlab-ci.yml`

2. Validate the generated config:
    - For GitHub Actions, check that the YAML is well-formed and uses valid action versions
    - For GitLab CI, check stage references are consistent
    - Verify no secrets or credentials appear in plaintext anywhere in the file

3. If the user has existing CI config, ask before overwriting:

    ```xml
    <ask_followup_question>
    <question>I found an existing CI config file. How should I handle it?</question>
    <options>["Replace it with the new config", "Create a new file alongside it", "Show me the new config without writing it"]</options>
    </ask_followup_question>
    ```

## 9. Present Result

1. Use the `attempt_completion` tool to present:
    - A summary of the generated pipeline (stages, triggers, platform)
    - The file location
    - A list of required secrets to configure (names only — never values)
    - How to trigger the first run
    - Suggestions for next steps (e.g., adding deployment, caching, matrix testing, Cline CLI automation)

</detailed_sequence_steps>

</task>
