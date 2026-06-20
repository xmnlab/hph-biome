# AI Contributor Guide: hphbiome

This file is the shared operating manual for AI contributors working in the
`hphbiome` repository.

## Project Snapshot

- Package: `hphbiome`
- Repository: `hph-biome`
- Runtime: Python `>=3.10,<4`
- Packaging: `setuptools` with a `src` layout
- Development environment: `conda/dev.yaml`

## Core Objectives

1. Keep package metadata, CI, release, and tooling configuration aligned with
   the `hphbiome` package name.
2. Make minimal, targeted infrastructure changes with clear intent.
3. Do not commit secrets, credentials, real PHI, or sensitive data.
4. Keep standard checks green when project code and tests are added.

## Repository Layout

- `src/hphbiome/`: future package implementation
- `tests/`: future pytest coverage
- `conda/dev.yaml`: cross-platform development environment definition
- `.makim.yaml`: task runner definitions
- `.github/workflows/`: CI, docs, and release workflows
- `pyproject.toml`: package metadata, dependencies, and tool configuration

## Tooling And Commands

Environment setup:

```bash
conda env create -f conda/dev.yaml
conda activate hphbiome
python -m pip install -e ".[dev]"
```

If using mamba:

```bash
mamba env create -f conda/dev.yaml
mamba activate hphbiome
python -m pip install -e ".[dev]"
```

High-value commands:

```bash
# unit tests with coverage threshold from .makim.yaml
makim tests.unit

# CI-like local checks
makim tests.ci

# lint/pre-commit stack
makim tests.linter
pre-commit run --all-files --verbose

# targeted static checks
ruff check src tests
ruff format src tests
mypy src/hphbiome

# package build
makim package.build
```

## Contributor Workflow Expectations

1. Inspect local files before planning changes.
2. Make focused edits and avoid unrelated churn.
3. Add or update tests when behavior changes.
4. Run targeted checks first, then broader checks when feasible.
5. Report any checks that could not be run and why.
