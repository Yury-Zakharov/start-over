---

description: "Task list for JSON Resume Editor implementation"
---

# Tasks: Stand-alone JSON Resume Editor

**Input**: Design documents from `/specs/001-json-resume-editor/`
**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md, contracts/

**Tests**: Tests for backend Go and frontend Elm will be included based on constitution requirements.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

## Path Conventions

- **Web app**: `backend/src/`, `frontend/src/`, `docker-compose.yml`

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Project initialization and basic structure

- [ ] T001 Create project structure per implementation plan (backend/, frontend/, docker-compose.yml)
- [ ] T002 Initialize Go project with dependencies in backend/ (go.mod, go.sum)
- [ ] T003 [P] Initialize Elm project with dependencies in frontend/ (elm.json)
- [ ] T004 Create initial Dockerfile for multi-stage build in backend/
- [ ] T005 Create docker-compose.yml for development and deployment

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Core infrastructure that MUST be complete before ANY user story can be implemented

**⚠️ CRITICAL**: No user story work can begin until this phase is complete

Examples of foundational tasks for this project:

- [ ] T006 [P] Create foundational Go models (resume.go) in backend/src/models/
- [ ] T007 [P] Create foundational Elm models (Resume.elm) in frontend/src/Models/
- [ ] T008 Create main Go application entry point (main.go) in backend/src/
- [ ] T009 [P] Create basic Elm application structure (Types.elm, Update.elm, View.elm) in frontend/src/
- [ ] T010 Implement file utilities for resume operations in backend/src/utils/file_utils.go
- [ ] T011 Create API handler structure in backend/src/handlers/resume_handler.go
- [ ] T012 [P] Create Elm JSON encoders/decoders in frontend/src/Models/Resume.elm
- [ ] T013 Setup static file serving for Elm frontend in backend/main.go
- [ ] T014 Create Elm API interface module in frontend/src/Api.elm

**Checkpoint**: Foundation ready - user story implementation can now begin in parallel

---

## Phase 3: User Story 1 - Load and View Resume File (Priority: P1) 🎯 MVP

**Goal**: Enable users to start the application and load a resume file via UI prompt, displaying it in a form interface

**Independent Test**: Application starts successfully, prompts user for resume file, loads and displays resume data in form interface

### Tests for User Story 1 (REQUIRED by constitution) ⚠️

> **CRITICAL: Write these tests FIRST and VERIFY they FAIL before any implementation (constitution requirement)**

- [ ] T015 [P] [US1] Unit test for resume JSON decoding in backend/tests/unit/test_resume_model.go
- [ ] T016 [P] [US1] Unit test for file reading operations in backend/tests/unit/test_file_utils.go
- [ ] T017 [P] [US1] Elm decoder test for resume structure in frontend/tests/ResumeTests.elm
- [ ] T018 [P] [US1] Contract test for GET /api/resume endpoint in backend/tests/contract/test_resume_api.go

### Implementation for User Story 1

- [ ] T019 [P] [US1] Implement GET /api/file-path endpoint in backend/src/handlers/resume_handler.go
- [ ] T020 [P] [US1] Implement POST /api/file-path endpoint in backend/src/handlers/resume_handler.go
- [ ] T021 [US1] Implement GET /api/resume endpoint in backend/src/handlers/resume_handler.go
- [ ] T022 [US1] Implement Elm UI to prompt user for file selection in frontend/src/View.elm
- [ ] T023 [US1] Implement Elm UI to display loaded resume in form interface in frontend/src/View.elm
- [ ] T024 [US1] Create Elm model state for file path management in frontend/src/Types.elm
- [ ] T025 [US1] Implement Elm API calls to file-path endpoints in frontend/src/Api.elm
- [ ] T026 [US1] Implement Elm update functions for resume loading state in frontend/src/Update.elm
- [ ] T027 [US1] Add Elm RemoteData pattern for loading/success/error states in frontend/src/Types.elm
- [ ] T028 [US1] Add file permission error handling in backend/src/handlers/resume_handler.go
- [ ] T029 [US1] Implement UI feedback for file loading errors in frontend/src/View.elm

**Checkpoint**: At this point, User Story 1 should be fully functional and testable independently

---

## Phase 4: User Story 2 - Edit Resume Sections (Priority: P1)

**Goal**: Provide form-based interface that mirrors JSON Resume schema allowing users to edit sections without corrupting JSON structure

**Independent Test**: Load a resume, make edits to different sections, verify JSON structure remains valid

### Tests for User Story 2 (REQUIRED by constitution) ⚠️

> **CRITICAL: Write these tests FIRST and VERIFY they FAIL before any implementation (constitution requirement)**

- [ ] T030 [P] [US2] Unit test for resume structure validation in backend/tests/unit/test_resume_validation.go
- [ ] T031 [P] [US2] Elm test for form update operations in frontend/tests/ResumeFormTests.elm
- [ ] T032 [P] [US2] Integration test for resume editing workflow in backend/tests/integration/test_edit_workflow.go

### Implementation for User Story 2

- [ ] T033 [P] [US2] Implement Elm form view for Basics section in frontend/src/View.elm
- [ ] T034 [P] [US2] Implement Elm form view for Work section in frontend/src/View.elm
- [ ] T035 [P] [US2] Implement Elm form view for Education section in frontend/src/View.elm
- [ ] T036 [P] [US2] Implement Elm form view for Skills section in frontend/src/View.elm
- [ ] T037 [P] [US2] Implement Elm form view for other sections (Awards, Publications, etc.) in frontend/src/View.elm
- [ ] T038 [US2] Implement Elm update functions for editing resume fields in frontend/src/Update.elm
- [ ] T039 [US2] Add form validation to prevent JSON structure corruption in frontend/src/Update.elm
- [ ] T040 [US2] Implement dynamic list management for sections (add/remove entries) in frontend/src/Update.elm
- [ ] T041 [US2] Add JSON schema validation in backend/src/handlers/resume_handler.go
- [ ] T042 [US2] Implement extensibility support for custom fields in backend/src/models/resume.go

**Checkpoint**: At this point, User Stories 1 AND 2 should both work independently

---

## Phase 5: User Story 3 - Save Resume File (Priority: P1)

**Goal**: Allow users to save changes back to resume.json file on host disk with visual feedback for success/failure

**Independent Test**: Make changes to resume in interface, click save, verify changes are written to file

### Tests for User Story 3 (REQUIRED by constitution) ⚠️

> **CRITICAL: Write these tests FIRST and VERIFY they FAIL before any implementation (constitution requirement)**

- [ ] T043 [P] [US3] Unit test for resume file writing in backend/tests/unit/test_file_utils.go
- [ ] T044 [P] [US3] Unit test for resume JSON encoding in backend/tests/unit/test_resume_model.go
- [ ] T045 [P] [US3] Elm test for save operation in frontend/tests/ResumeSaveTests.elm
- [ ] T046 [P] [US3] Contract test for POST /api/resume endpoint in backend/tests/contract/test_resume_api.go

### Implementation for User Story 3

- [ ] T047 [P] [US3] Implement POST /api/resume endpoint in backend/src/handlers/resume_handler.go
- [ ] T048 [US3] Add file writing with permission checks in backend/src/utils/file_utils.go
- [ ] T049 [US3] Implement Elm save button UI in frontend/src/View.elm
- [ ] T050 [US3] Implement Elm API call to save resume in frontend/src/Api.elm
- [ ] T051 [US3] Add Elm update function for save operation in frontend/src/Update.elm
- [ ] T052 [US3] Add Elm UI feedback for save success/error in frontend/src/View.elm
- [ ] T053 [US3] Implement resume validation before save in backend/src/handlers/resume_handler.go
- [ ] T054 [US3] Add JSON schema validation error feedback in frontend/src/View.elm
- [ ] T055 [P] [US3] Implement file system watcher to detect external changes to resume file in backend/src/utils/file_utils.go
- [ ] T056 [US3] Add external file change detection notification in frontend/src/Update.elm

**Checkpoint**: All user stories should now be independently functional

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Improvements that affect multiple user stories

- [ ] T057 [P] Update README.md with quickstart instructions from quickstart.md (per constitution's step-by-step isolation requirement to update readme.md on each step)
- [ ] T058 Add Elm and Go code formatting/linting configuration files
- [ ] T059 [P] Add comprehensive error handling across all endpoints in backend/src/handlers/resume_handler.go
- [ ] T060 [P] Add comprehensive error UI in Elm frontend for all error scenarios in frontend/src/View.elm
- [ ] T061 [P] Add Elm unit tests for all update operations in frontend/tests/
- [ ] T062 [P] Add Go integration tests for complete resume workflow in backend/tests/integration/
- [ ] T063 Add performance optimizations for large resume files in backend/src/utils/file_utils.go
- [ ] T064 Add loading indicators for resume operations in frontend/src/View.elm
- [ ] T065 [P] Set up Go test coverage reporting to meet 70% requirement in backend/
- [ ] T066 [P] Set up Elm test coverage reporting to meet 70% requirement in frontend/
- [ ] T067 Verify combined coverage meets 70% minimum threshold across both Go and Elm components
- [ ] T068 Add Elm documentation comments to all functions in frontend/src/
- [ ] T069 Add Go documentation comments to all functions in backend/src/
- [ ] T070 Run quickstart.md validation to ensure deployment instructions work

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - can start immediately
- **Foundational (Phase 2)**: Depends on Setup completion - BLOCKS all user stories
- **User Stories (Phase 3+)**: All depend on Foundational phase completion
  - User stories can then proceed in parallel (if staffed)
  - Or sequentially in priority order (P1 → P2 → P3)
- **Polish (Final Phase)**: Depends on all desired user stories being complete

### User Story Dependencies

- **User Story 1 (P1)**: Can start after Foundational (Phase 2) - No dependencies on other stories
- **User Story 2 (P2)**: Can start after Foundational (Phase 2) - Depends on US1 models and basic UI structure
- **User Story 3 (P3)**: Can start after Foundational (Phase 2) - Depends on US1/US2 models and UI

### Within Each User Story

- Tests (if included) MUST be written and FAIL before implementation
- Models before services
- Services before endpoints
- Core implementation before integration
- Story complete before moving to next priority

### Parallel Opportunities

- All Setup tasks marked [P] can run in parallel
- All Foundational tasks marked [P] can run in parallel (within Phase 2)
- Once Foundational phase completes, all user stories can start in parallel (if team capacity allows)
- All tests for a user story marked [P] can run in parallel
- Models within a story marked [P] can run in parallel
- Different user stories can be worked on in parallel by different team members

---

## Parallel Example: User Story 1

```bash
# Launch all tests for User Story 1 together:
Task: "Unit test for resume JSON decoding in backend/tests/unit/test_resume_model.go"
Task: "Unit test for file reading operations in backend/tests/unit/test_file_utils.go"
Task: "Elm decoder test for resume structure in frontend/tests/ResumeTests.elm"
Task: "Contract test for GET /api/resume endpoint in backend/tests/contract/test_resume_api.go"

# Launch all models for User Story 1 together:
Task: "Implement GET /api/file-path endpoint in backend/src/handlers/resume_handler.go"
Task: "Implement POST /api/file-path endpoint in backend/src/handlers/resume_handler.go"
Task: "Implement GET /api/resume endpoint in backend/src/handlers/resume_handler.go"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup
2. Complete Phase 2: Foundational (CRITICAL - blocks all stories)
3. Complete Phase 3: User Story 1
4. **STOP and VALIDATE**: Test User Story 1 independently
5. Deploy/demo if ready

### Incremental Delivery

1. Complete Setup + Foundational → Foundation ready
2. Add User Story 1 → Test independently → Deploy/Demo (MVP!)
3. Add User Story 2 → Test independently → Deploy/Demo
4. Add User Story 3 → Test independently → Deploy/Demo
5. Each story adds value without breaking previous stories

### Parallel Team Strategy

With multiple developers:

1. Team completes Setup + Foundational together
2. Once Foundational is done:
   - Developer A: User Story 1
   - Developer B: User Story 2
   - Developer C: User Story 3
3. Stories complete and integrate independently

---

## Notes

- [P] tasks = different files, no dependencies
- [Story] label maps task to specific user story for traceability
- Each user story should be independently completable and testable
- Verify tests fail before implementing
- Commit after each task or logical group
- Stop at any checkpoint to validate story independently
- Avoid: vague tasks, same file conflicts, cross-story dependencies that break independence