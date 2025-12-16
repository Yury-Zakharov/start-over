<!--
Sync Impact Report:
- Version change: N/A -> 1.0.0 (initial constitution for project)
- Modified principles: N/A (new principles added)
- Added sections: Development Process & Workflow, Testing & Quality Assurance, Coding Standards & Principles, Architecture & Isolation
- Removed sections: N/A
- Templates requiring updates:
  - .specify/templates/plan-template.md ✅ updated
  - .specify/templates/spec-template.md ✅ updated
  - .specify/templates/tasks-template.md ✅ updated
  - .specify/commands/*.toml ⚠ pending
  - README.md ⚠ pending
- Follow-up TODOs: None
-->

# Project Constitution

## Core Principles

### Development Process & Workflow
* **GitHub Flow:** All changes must be performed via Pull Requests (PRs). No direct commits to `main`.
* **Step-by-Step Isolation:** Development must occur in logically isolated steps. A step is considered complete only when it results in a stable, working application. Project readme.md file must be updated on each step to reflect current state of the project.
* **Documentation First:** Requirements and specifications must be documented in the repository before any code is written for a given feature.
* **Commit Discipline:** Commit messages must be clear and follow conventional commits (e.g., `feat:`, `fix:`, `docs:`).

### Testing & Quality Assurance
* **Test Mandate:** Editing or disabling failing tests is strictly forbidden. Code must be fixed to pass the tests.
* **Coverage Threshold:** The codebase must maintain a minimum of **70% code coverage**.
* **Dual Testing Layers:**
    * **Unit Tests:** Required for all core logic (Elm update functions, Go JSON handling).
    * **Integration Tests:** Required for the API endpoints and JSON file I/O operations.
* **Passing Gate:** All tests must pass before a development step is marked as complete.

### Coding Standards & Principles
* **Declarative Preference:** Use declarative programming styles wherever possible (naturally enforced by Elm, preferred in Go setup).
* **Self-Documenting Code:** Avoid comments explaining *what* code does. Only document *why* a decision was made if it is not obvious.
* **Strict Typing:** Leverage the type systems of Elm and Go to prevent runtime errors. Avoid `any` or loose typing.

### Architecture & Isolation
* **Containerization:** The final artifact must be a single Docker image runnable via Docker Compose.
* **Local-Only:** No external authentication or cloud dependencies are permitted. The app must function entirely offline.

## Governance
Project constitution supersedes all other practices except legal requirements. All changes must follow amendment procedures documented here. All team members are expected to be familiar with these principles and apply them consistently throughout development. Code reviews must verify compliance with these principles.

**Version**: 1.0.0 | **Ratified**: 2025-12-15 | **Last Amended**: 2025-12-15
