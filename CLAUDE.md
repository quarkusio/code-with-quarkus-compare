# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Purpose

This repository compares Quarkus project generator (code.quarkus.io) output across versions and build tools. It contains no application code — only a GitHub Actions workflow and documentation.

## Architecture

**Multi-branch structure:**
- `workflow` (main branch) — Contains only the GitHub Actions workflow, README, and config files
- `maven`, `gradle`, `gradle-kotlin-dsl` — Each holds a generated Quarkus project directly in the root directory

**Tagging:** `buildtool-version` format (e.g., `maven-3.31.2`, `gradle-kotlin-dsl-3.15.7`). Tags enable GitHub compare views between versions or across build tools.

**Workflow** (`.github/workflows/generate-quarkus-projects.yml`):
- Triggered weekly (Sunday midnight UTC) or manually via `workflow_dispatch`
- Runs in parallel for each build tool via matrix strategy
- Installs Quarkus CLI via JBang, generates a project, replaces branch content, commits, and tags
- Manual dispatch accepts an optional `quarkus_version` input (defaults to latest)

## Key Details

- No build/test/lint commands — this repo has no compilable code on the `workflow` branch
- The workflow uses `quarkus create app com.example:project:1.0.0-SNAPSHOT` with the appropriate build tool flag
- Changes to the workflow itself should be committed to the `workflow` branch only
