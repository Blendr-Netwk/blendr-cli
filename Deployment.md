# Deployment Guide for blendrnetwork_cli

This guide explains how to deploy new versions of the blendrnetwork_cli package to PyPI.

## Prerequisites

1. Install required packages:
```bash
pip install build twine
```

2. Make sure you have a PyPI account and API token
   - Go to https://pypi.org/manage/account/token/
   - Create a new token with "Upload" scope
   - Save the token securely

## Deployment Steps

### 1. Update Version Number

Update the version in `pyproject.toml`:
```toml
[project]
name = "blendrnetwork_cli"
version = "x.x.x"  # Increment this version number
```

Version numbering convention:
- Bug fixes: increment last number (e.g., 0.2.0 → 0.2.1)
- New features: increment middle number (e.g., 0.2.1 → 0.3.0)
- Major changes: increment first number (e.g., 0.3.0 → 1.0.0)

### 2. Clean Old Builds

Remove old build artifacts:
```bash
rm -rf dist/
rm -rf build/
rm -rf *.egg-info
```

### 3. Build Package

Build new distribution files:
```bash
python -m build
```

### 4. Upload to PyPI

Upload using twine:
```bash
python -m twine upload dist/*
```

When prompted:
- Username: `__token__`
- Password: Your PyPI API token

### 5. Verify Installation

Test the new version:
```bash
# Create a new virtual environment for testing
python -m venv test_env
source test_env/bin/activate  # On Windows: test_env\Scripts\activate

# Install the package
pip install blendrnetwork_cli

# Test the CLI
blendr --help
```

## Installation for Users

Users can install the package using:
```bash
pip install blendrnetwork_cli
```

To upgrade to the latest version:
```bash
pip install --upgrade blendrnetwork_cli
```

## Troubleshooting

### Uninstalling Old Versions

If you need to remove old installations:
```bash
pip uninstall blendr-cli
pip uninstall blendr_cli
pip uninstall blendrnetwork_cli
```

### Command Conflicts

If the `blendr` command is not working properly:
1. Check which version is being used:
   ```bash
   which blendr
   ```
2. Deactivate and reactivate your virtual environment:
   ```bash
   deactivate
   source venv/bin/activate
   ```

## Package Configuration Reference

The package configuration is managed in `pyproject.toml`. Key sections:

```toml
[build-system]
requires = ["setuptools>=45", "wheel"]
build-backend = "setuptools.build_meta"

[project]
name = "blendrnetwork_cli"
version = "x.x.x"
authors = [
    { name="Blendr Network", email="tech@blendr.network" }
]
description = "Blendr CLI tool for GPU Lending"
readme = "README.md"
requires-python = ">=3.8"
license = {text = "MIT"}

[project.scripts]
blendr = "blendr.cli:main"
```

## Notes

- Always test the package locally before deploying
- Keep track of changes in a CHANGELOG.md
- Update documentation when adding new features
- The package name (blendrnetwork_cli) differs from the command name (blendr)