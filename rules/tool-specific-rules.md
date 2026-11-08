# Tool-Specific Development Guidance

## Purpose
This document provides specific operational conventions, coding standards, and tooling expectations for developers and AI coding agents operating across modern AI environments (Cursor, Codex, Claude Code, GitHub Copilot, Gemini Code Assist, etc.).

---

## 1. Technical Stack & Language Standards
- **Runtime Environment**: Python 3.11 or newer (Python 3.12 recommended).
- **Code Style**: Strictly follow [PEP 8](https://peps.python.org/pep-0008/) style standards:
  - 4-space indentation (no hard tabs).
  - Explicit type hinting on all function signatures (`def calculate_completion(submitted: list[str], required: list[str]) -> float:`).
  - Clear, explanatory docstrings adhering to Google or NumPy style.
- **Dependencies**: Keep external dependencies lightweight and explicit. Standard library modules (`json`, `pathlib`, `re`, `dataclasses`) are strongly preferred.

---

## 2. Testing Framework & Protocol
- **Primary Test Runner**: `pytest`
  ```bash
  pytest -v tests/
  ```
- **Test Requirements**:
  - All mathematical calculations (percentage completion, deduplication) must have deterministic test assertions.
  - Test suites must cover both nominal cases (100% complete) and edge cases (0% submissions, duplicate submissions, extra irrelevant files, adversarial filenames).
  - Never silence or mock out core business rule failures to make a test suite pass.

---

## 3. Tool Safety & Operational Guardrails
- **Environment Isolation**: Never assume write permissions outside the repository boundary.
- **Environment Variables**: Avoid reading or printing unverified environment variables that may contain system tokens.
- **Execution Safeguards**: Report failed terminal commands immediately with precise error traces rather than repeatedly executing failing commands blindly.
- **Deployment Gate**: Under no circumstances should an AI agent attempt automated production deployments without explicit human interactive confirmation.

---

## 4. Version Control Conventions
- **Commit Format**: Follow the Conventional Commits standard:
  - `docs:` for documentation, instructions, and specification updates.
  - `feat:` for new validation logic or skill definitions.
  - `test:` for test suites and benchmark datasets.
  - `fix:` for bug fixes or corrections to calculation rules.
- **Staging Hygiene**:
  - Always run `git status` and inspect `git diff` prior to staging files.
  - Never stage untracked secrets, cache directories, or system artifacts.
  - Stage logical change units independently rather than making monolithic bulk commits.
