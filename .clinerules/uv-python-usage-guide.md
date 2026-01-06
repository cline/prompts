---
description: A comprehensive guide to using UV for Python project management, covering installation, environment management, package handling, and best practices.
author: Cline
version: 1.0
category: "Language-Specific"
tags: ["uv", "python", "package-manager", "venv", "guide"]
globs: ["**/*.py", "pyproject.toml"]
---

# UV Python Project Management Guide

## Table of Contents
- [Introduction](#introduction)
- [Installation](#installation)
- [Managing Python Versions](#managing-python-versions)
- [Project Management](#project-management)
- [Virtual Environment Management](#virtual-environment-management)
- [Package Management](#package-management)
- [Advanced Configuration](#advanced-configuration)
- [Development Workflows](#development-workflows)
- [Best Practices](#best-practices)
- [Security Considerations](#security-considerations)
- [Performance Optimization](#performance-optimization)
- [Troubleshooting](#troubleshooting)
- [Environment Variables](#environment-variables)
- [Tool Integration](#tool-integration)
- [Common Commands Reference](#common-commands-reference)

## Introduction

UV is a modern Python package manager and virtual environment tool that offers significant performance improvements over traditional tools like pip and venv. This guide covers how to effectively use UV for Python project management.

## Installation

### macOS
```bash
# Using Homebrew
brew install uv

# Using the installer script
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### Linux
```bash
# Using the installer script
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### Windows
```powershell
# Using winget
winget install --id=astral-sh.uv -e

# Using scoop
scoop install main/uv
```

## Managing Python Versions

UV can manage Python installations for you. Here's how to work with Python versions:

### Installing Python
```bash
# Install latest Python version
uv python install

# Install specific Python version
uv python install 3.12

# Install multiple versions
uv python install 3.11 3.12

# Install PyPy
uv python install pypy@3.10
```

### Listing Python Versions
```bash
# List available and installed versions
uv python list

# Show all versions including other platforms
uv python list --all-versions

# Only show installed versions
uv python list --only-installed
```

### Finding Python Executables
```bash
# Find default Python
uv python find

# Find specific version
uv python find >=3.11
```

## Project Management

UV provides robust project management capabilities through its project system.

### Creating a New Project
```bash
# Create a new project
uv init my-project
cd my-project

# Or initialize in current directory
mkdir my-project
cd my-project
uv init
```

This creates:
- `pyproject.toml` - Project configuration and dependencies
- `.python-version` - Python version specification
- `README.md` - Project documentation
- `main.py` - Initial Python file

### Project Structure
```
my-project/
├── .venv/               # Virtual environment (created on first use)
├── .python-version      # Python version specification
├── pyproject.toml       # Project configuration
├── uv.lock             # Dependency lock file
├── README.md           # Project documentation
└── main.py             # Main Python file
```

### Managing Dependencies

```bash
# Add dependencies
uv add requests
uv add 'flask>=2.0.0'
uv add 'pytest[testing]'

# Remove dependencies
uv remove requests

# Update dependencies
uv lock --upgrade-package requests

# Install all dependencies
uv sync
```

## Virtual Environment Management

UV automatically manages virtual environments for projects and can work with existing environments.

### Creating Virtual Environments
```bash
# Create venv in default location (.venv)
uv venv

# Create venv with specific name
uv venv my-env

# Create venv with specific Python version
uv venv --python 3.12
```

### Working with Virtual Environments

```bash
# Activate virtual environment
# On Unix/macOS:
source .venv/bin/activate

# On Windows:
.venv\Scripts\activate

# On Fish shell:
source .venv/bin/activate.fish

# Deactivate virtual environment
deactivate
```

### Using Existing Environments

UV automatically detects and uses virtual environments in the following order:
1. Active virtual environment (VIRTUAL_ENV)
2. Active Conda environment (CONDA_PREFIX)
3. `.venv` in current or parent directories

## Package Management

UV provides both high-level project commands and pip-compatible commands for package management.

### Project-Based Package Management
```bash
# Add package to project
uv add package-name

# Remove package from project
uv remove package-name

# Sync project dependencies
uv sync

# Update lockfile
uv lock
```

### Pip-Compatible Commands
```bash
# Install packages
uv pip install package-name
uv pip install -r requirements.txt

# Install in editable mode
uv pip install -e .

# Uninstall packages
uv pip uninstall package-name

# List installed packages
uv pip list

# Show package info
uv pip show package-name

# Generate requirements.txt
uv pip freeze > requirements.txt
```

## Advanced Configuration

### pyproject.toml Configuration
```toml
[project]
name = "my-project"
version = "0.1.0"
description = "Project description"
readme = "README.md"
requires-python = ">=3.8"
license = { text = "MIT" }
authors = [
    { name = "Your Name", email = "your.email@example.com" }
]

dependencies = [
    "requests>=2.28.0",
    "flask[async]>=2.0.0",
    "sqlalchemy",
]

[project.optional-dependencies]
test = ["pytest>=7.0", "pytest-cov"]
dev = ["black", "mypy", "ruff"]

[tool.uv]
python-version = "3.12"
```

### UV Configuration Options
```toml
[tool.uv]
# Package index configuration
[[tool.uv.index]]
url = "https://pypi.org/simple"
default = true

[[tool.uv.index]]
url = "https://test.pypi.org/simple"
secondary = true

# Build settings
no-binary = ["cryptography", "numpy"]
build-isolation = true

# Cache settings
cache-dir = "~/.cache/uv"
```

### Environment-Specific Settings
```toml
[tool.uv.env]
development = { extras = ["dev", "test"] }
production = { extras = [] }
```

## Development Workflows

### Local Development Setup
```bash
# Initialize new project
uv init my-project
cd my-project

# Set up development environment
uv add --dev black ruff mypy pytest
uv add --dev 'pre-commit>=3.0.0'

# Create pre-commit config
cat > .pre-commit-config.yaml << EOF
repos:
-   repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.3.0
    hooks:
    -   id: ruff
        args: [--fix]
-   repo: https://github.com/psf/black
    rev: 24.2.0
    hooks:
    -   id: black
EOF

# Install pre-commit hooks
uv run pre-commit install
```

### CI/CD Integration
```yaml
# .github/workflows/python-ci.yml
name: Python CI

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    
    - name: Install UV
      run: curl -LsSf https://astral.sh/uv/install.sh | sh

    - name: Setup Python
      run: uv python install 3.12

    - name: Install dependencies
      run: |
        uv pip install -e ".[test]"
        
    - name: Run tests
      run: uv run pytest
```

### Working with Multiple Python Versions
```bash
# Create test environments
for version in 3.8 3.9 3.10 3.11 3.12; do
    uv venv "venv-$version" --python "$version"
    source "venv-$version/bin/activate"
    uv pip install -e ".[test]"
    uv run pytest
    deactivate
done
```

## Best Practices

### 1. Project Structure
```
my-project/
├── .git/
├── .gitignore
├── .pre-commit-config.yaml
├── .python-version
├── .venv/
├── src/
│   └── my_project/
│       ├── __init__.py
│       ├── core.py
│       └── utils/
├── tests/
│   ├── __init__.py
│   └── test_core.py
├── docs/
├── pyproject.toml
├── uv.lock
└── README.md
```

### 2. Version Control Best Practices
```gitignore
# .gitignore
.venv/
__pycache__/
*.py[cod]
*$py.class
.pytest_cache/
.coverage
htmlcov/
dist/
build/
*.egg-info/
```

### 3. Dependency Management
- Use semantic versioning for dependencies:
  ```toml
  dependencies = [
      "requests~=2.28.0",     # Compatible releases (>=2.28.0, <2.29.0)
      "flask>=2.0.0,<3.0.0",  # Specific version range
      "sqlalchemy==2.0.0",    # Exact version
  ]
  ```

- Lock dependencies for reproducibility:
  ```bash
  # Update lockfile
  uv lock
  
  # Sync environment with lockfile
  uv sync
  ```

### 4. Testing and Quality Assurance
```bash
# Install test dependencies
uv add --dev pytest pytest-cov black mypy ruff

# Run tests with coverage
uv run pytest --cov=src/my_project

# Run type checking
uv run mypy src/my_project

# Run linting
uv run ruff check src/my_project
```

### 5. Documentation
- Use docstrings for all public APIs
- Maintain up-to-date README.md
- Document environment setup requirements
- Include example usage

### 6. Security Best Practices
- Keep UV and Python updated
- Use UV's hash verification
- Audit dependencies regularly
- Use private package indexes securely

### 7. Performance Optimization
- Use UV's concurrent downloads
- Leverage caching effectively
- Optimize dependency resolution
- Use prebuilt wheels when possible

## Security Considerations

### Package Verification
```bash
# Enable hash verification
uv pip install --require-hashes -r requirements.txt

# Generate requirements with hashes
uv pip freeze --all --require-hashes > requirements.txt
```

### Private Package Indexes
```toml
[tool.uv]
[[tool.uv.index]]
url = "https://private.pypi.org/simple"
username = "${PYPI_USERNAME}"
password = "${PYPI_PASSWORD}"
```

### Dependency Auditing
```bash
# Install safety checker
uv tool install safety

# Check for known vulnerabilities
safety check
```

## Performance Optimization

### Caching Configuration
```bash
# Set custom cache directory
export UV_CACHE_DIR="/path/to/cache"

# Clear cache
uv cache clean

# Prune old cache entries
uv cache prune
```

### Build Optimization
```bash
# Set concurrent build limit
export UV_CONCURRENT_BUILDS=4

# Disable build isolation for speed
uv pip install --no-build-isolation package-name
```

## Troubleshooting

### Common Issues and Solutions

1. **Package Installation Failures**
   ```bash
   # Try with --verbose for more information
   uv pip install --verbose package-name
   
   # Force reinstall
   uv pip install --force-reinstall package-name
   ```

2. **Virtual Environment Issues**
   ```bash
   # Recreate virtual environment
   rm -rf .venv
   uv venv
   uv sync
   ```

3. **Dependency Conflicts**
   ```bash
   # Check for conflicts
   uv pip check
   
   # Show dependency tree
   uv pip tree
   ```

### Debug Mode
```bash
# Enable debug logging
export RUST_LOG=debug
uv pip install package-name
```

## Environment Variables

### Common Environment Variables
```bash
# Cache configuration
export UV_CACHE_DIR="/path/to/cache"
export UV_NO_CACHE=1

# Python configuration
export UV_PYTHON_INSTALL_DIR="/path/to/pythons"
export UV_PYTHON_PREFERENCE="managed"

# Network configuration
export UV_HTTP_TIMEOUT=30
export UV_OFFLINE=1

# Build configuration
export UV_CONCURRENT_BUILDS=4
export UV_NO_BUILD_ISOLATION=1
```

## Tool Integration

### Editor Integration (VSCode)
```json
{
    "python.defaultInterpreterPath": "${workspaceFolder}/.venv/bin/python",
    "python.analysis.typeCheckingMode": "basic",
    "python.formatting.provider": "black",
    "python.linting.enabled": true,
    "python.linting.lintOnSave": true
}
```

### Pre-commit Integration
```yaml
# .pre-commit-config.yaml
repos:
-   repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.3.0
    hooks:
    -   id: ruff
        args: [--fix]
-   repo: https://github.com/psf/black
    rev: 24.2.0
    hooks:
    -   id: black
-   repo: https://github.com/pre-commit/mirrors-mypy
    rev: v1.8.0
    hooks:
    -   id: mypy
        additional_dependencies: [types-all]
```

### Docker Integration
```dockerfile
FROM python:3.12-slim

# Install UV
RUN curl -LsSf https://astral.sh/uv/install.sh | sh

WORKDIR /app
COPY . .

# Install dependencies
RUN uv pip install -e ".[prod]"

CMD ["uv", "run", "python", "-m", "my_project"]
```

## Advanced Package Management

### Monorepo Support
```
monorepo/
├── .git/
├── pyproject.toml      # Workspace configuration
├── project1/
│   ├── pyproject.toml  # Project 1 configuration
│   ├── src/
│   └── tests/
├── project2/
│   ├── pyproject.toml  # Project 2 configuration
│   ├── src/
│   └── tests/
└── shared/
    ├── pyproject.toml  # Shared library configuration
    └── src/
```

Root pyproject.toml for monorepo:
```toml
[workspace]
members = [
    "project1",
    "project2",
    "shared"
]

[tool.uv.workspace]
python-version = "3.12"
```

### Complex Dependency Scenarios

1. **Git Dependencies with Specific References**
   ```toml
   dependencies = [
       "mypackage @ git+https://github.com/user/repo.git@main",
       "otherpackage @ git+https://github.com/user/repo.git@v1.0.0",
       "debugtools @ git+ssh://git@github.com/user/repo.git@d34db33f"
   ]
   ```

2. **Local Development Dependencies**
   ```toml
   dependencies = [
       "mypackage @ file:///path/to/package",
       "devtool @ file:///${PROJECT_ROOT}/tools/devtool"
   ]
   ```

3. **Complex Version Constraints**
   ```toml
   dependencies = [
       "requests>=2.28.0,<3.0.0,!=2.29.0",  # Exclude specific version
       "flask~=2.0.0",                       # Compatible release
       "sqlalchemy>2.0.0",                   # Greater than
       "pandas==2.0.*",                      # Wildcard matching
   ]
   ```

### Advanced Installation Scenarios

1. **Installing with Extras**
   ```bash
   # Install multiple extras
   uv add 'flask[async,dotenv]'
   
   # Install all extras
   uv add 'flask[all]'
   ```

2. **Platform-Specific Dependencies**
   ```toml
   [project.dependencies]
   pywin32 = { version = ">=305", markers = "sys_platform == 'win32'" }
   pyobjc-framework-Cocoa = { version = ">=9.0", markers = "sys_platform == 'darwin'" }
   ```

3. **Development Dependencies with Groups**
   ```toml
   [project.optional-dependencies]
   test = [
       "pytest>=7.0",
       "pytest-cov>=4.0",
       "pytest-asyncio>=0.21.0"
   ]
   lint = [
       "black>=23.0",
       "ruff>=0.1.0",
       "mypy>=1.0"
   ]
   docs = [
       "sphinx>=7.0",
       "sphinx-rtd-theme>=1.0"
   ]
   dev = [
       "ipython>=8.0",
       "debugpy>=1.6"
   ]
   ```

### Package Publishing Workflow
```bash
# Build distribution
uv build

# Check distribution
uv run twine check dist/*

# Upload to TestPyPI
uv publish --index testpypi

# Upload to PyPI
uv publish

# Upload with trusted publishing (GitHub Actions)
uv publish --oidc
```

### Advanced Cache Management
```bash
# View cache information
uv cache info

# Clean specific cache types
uv cache clean --wheels    # Clean wheel cache
uv cache clean --sources   # Clean source cache
uv cache clean --http      # Clean HTTP cache

# Set cache retention period
uv cache prune --older-than 30d
```

### Custom Index Configuration
```toml
[tool.uv]
# Configure multiple package indexes
[[tool.uv.index]]
url = "https://pypi.org/simple"
default = true

[[tool.uv.index]]
url = "https://test.pypi.org/simple"
secondary = true

[[tool.uv.index]]
url = "https://private.pypi.org/simple"
username = "${PYPI_USERNAME}"
password = "${PYPI_PASSWORD}"

# Index-specific settings
[tool.uv.index-settings]
timeout = 30
verify-ssl = true
retries = 3
```

## Common Commands Reference

### Project Commands
```bash
uv init              # Create new project
uv add              # Add dependency
uv remove           # Remove dependency
uv sync             # Install dependencies
uv lock             # Update lockfile
uv run              # Run command in project environment
```

### Virtual Environment Commands
```bash
uv venv             # Create virtual environment
uv pip install      # Install packages
uv pip uninstall    # Remove packages
uv pip list         # List installed packages
uv pip freeze       # Generate requirements.txt
```

### Python Management Commands
```bash
uv python install   # Install Python
uv python list      # List Python versions
uv python find      # Find Python executable
uv python pin       # Pin Python version
```

### Tool Commands
```bash
uvx                 # Run tool without installing
uv tool install     # Install tool globally
uv tool uninstall   # Remove tool
uv tool list        # List installed tools
