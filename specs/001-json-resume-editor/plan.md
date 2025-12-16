# Implementation Plan: Stand-alone JSON Resume Editor

**Branch**: `001-json-resume-editor` | **Date**: 2025-12-15 | **Spec**: [spec.md](./spec.md)
**Input**: Feature specification from `/specs/001-json-resume-editor/spec.md`

**Note**: This template is filled in by the `/speckit.plan` command. See `.specify/templates/commands/plan.md` for the execution workflow.

## Summary

A local-only, containerized web application that allows users to load, edit, and save a "JSON Resume" file through a visual interface. The application is built using Elm for the frontend and Go for the backend, packaged in a single Docker image. It enables users to manage their resume without editing raw JSON, providing a form-based interface that corresponds to the JSON Resume schema.

## Technical Context

**Language/Version**: Elm 0.19+ (frontend), Go 1.22+ (backend)
**Primary Dependencies**: Elm Land framework, elm-ui for UI, Go standard library (net/http, embed, os, io)
**Storage**: File system - direct read/write to resume.json file on host system via Docker volume mount
**Testing**: Go `testing` package for backend, elm-explorations/test for frontend, with mandatory 70% coverage minimum as required by project constitution
**Target Platform**: Docker container with web interface accessible at http://localhost:8080
**Project Type**: Web application (frontend + backend in single container)
**Performance Goals**: Load resume (up to 10MB) in under 5 seconds on standard hardware (4-core CPU, 8GB RAM), save changes with confirmation in under 3 seconds on standard hardware
**Constraints**: Local-only (no external dependencies), single Docker image, offline-capable, 70% test coverage minimum, constitution's dual testing layers (unit tests for core logic, integration tests for API/file I/O)
**Scale/Scope**: Single-user local application, supports any file size, validates against JSON Resume schema

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

- **GitHub Flow**: All changes will be performed via Pull Requests (compliant)
- **Step-by-Step Isolation**: Development will occur in logically isolated steps (compliant)
- **Documentation First**: Implementation follows documented specification (compliant)
- **Commit Discipline**: Commit messages will follow conventional commits (compliant)
- **Test Mandate**: Tests will be written and must pass before completion (compliant)
- **Coverage Threshold**: Minimum 70% code coverage will be maintained (compliant)
- **Dual Testing Layers**: Unit tests for core logic, integration tests for API and file I/O (compliant)
- **Declarative Preference**: Elm naturally enforces declarative style, Go implementation will prefer declarative patterns (compliant)
- **Self-Documenting Code**: Code will be written to be self-explanatory with comments only for rationale (compliant)
- **Strict Typing**: Leveraging Elm and Go type systems to prevent runtime errors (compliant)
- **Containerization**: Final artifact will be a single Docker image (compliant)
- **Local-Only**: No external authentication or cloud dependencies (compliant)

*Post-Design Constitution Check:* All principles continue to be satisfied by the implemented architecture.

## Project Structure

### Documentation (this feature)

```text
specs/001-json-resume-editor/
├── plan.md              # This file (/speckit.plan command output)
├── research.md          # Phase 0 output (/speckit.plan command)
├── data-model.md        # Phase 1 output (/speckit.plan command)
├── quickstart.md        # Phase 1 output (/speckit.plan command)
├── contracts/           # Phase 1 output (/speckit.plan command)
└── tasks.md             # Phase 2 output (/speckit.tasks command - NOT created by /speckit.plan)
```

### Source Code (repository root)

```text
backend/
├── src/
│   ├── main.go
│   ├── handlers/
│   │   └── resume_handler.go
│   ├── models/
│   │   └── resume.go
│   └── utils/
│       └── file_utils.go
├── Dockerfile
├── go.mod
└── go.sum

frontend/
├── src/
│   ├── Main.elm
│   ├── Types.elm
│   ├── Update.elm
│   ├── View.elm
│   ├── Api.elm
│   └── Models/
│       └── Resume.elm
├── elm.json
├── index.html
└── tailwind.config.js

docker-compose.yml
```

**Structure Decision**: Web application with separate backend (Go) and frontend (Elm) directories following the constitution's architecture principles. The frontend will be embedded in the Go binary at build time, creating a single container image.

## Complexity Tracking

> **Fill ONLY if Constitution Check has violations that must be justified**

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
