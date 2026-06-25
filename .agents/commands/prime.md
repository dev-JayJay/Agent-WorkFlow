---
description: Prime agent with codebase understanding
---

# Prime: Load Project Context

## Objective

Build a comprehensive understanding of the codebase by analyzing structure, documentation, configuration, architecture, and current git state.

This command is for context loading only.

Do not modify files.
Do not write implementation code.
Do not create commits.

## Process

### 1. Analyze Project Structure

List all tracked files:
!`git ls-files`

Show directory structure:
On Linux, run: `tree -L 3 -I 'node_modules|__pycache__|.git|dist|build|coverage|.next'`

### 2. Read Core Documentation

- Read the PRD.md or similar spec file
- Read AGENT.md or similar global rules file
- Read README files at project root and major directories
- Read any architecture documentation
- Read the drizzle config so you understand the database schema

### 3. Identify Key Files

Based on the structure, identify and read:
- Main entry points (main.ts, index.ts, app.ts, etc.)
- Core configuration files (
        package.json
        tsconfig.json
        vite.config.*
        next.config.*
        eslint.config.*
        pyproject.toml
        requirements.txt
        composer.json
        Dockerfile
        docker-compose.yml
        .env.example
    )
- Key model/schema definitions
- Important service or controller files

### 4. Understand Current State

Check recent activity:
!`git log -10 --oneline`

Check current branch and status:
!`git status`

## Output Report

Provide a concise summary covering:

### Project Overview
- Purpose and type of application
- Primary technologies and frameworks
- Current version/state

### Architecture
- Overall structure and organization
- Key architectural patterns identified
- Important directories and their purposes

### Tech Stack
- Languages and versions
- Frameworks and major libraries
- Build tools and package managers
- Testing frameworks

### Core Principles
- Code style and conventions observed
- Documentation standards
- Testing approach

### Current State
- Active branch
- Recent changes or development focus
- Any immediate observations or concerns

**Make this summary easy to scan - use bullet points and clear headers.**
