# Research Summary: JSON Resume Editor

## Decision: Technology Stack
* **Frontend**: Elm 0.19+ with elm-ui for declarative UI and strong type safety
* **Backend**: Go 1.22+ with standard library for HTTP and file operations
* **Rationale**: Elm provides excellent JSON handling and prevents runtime errors; Go offers simple deployment via single binary and excellent file I/O capabilities

## Decision: Architecture Pattern
* **Single Binary Approach**: Elm frontend assets embedded in Go binary using `embed` package
* **Rationale**: Meets constitution requirement for single Docker image while keeping frontend/backend concerns separated during development

## Decision: JSON Schema Validation
* **Validation Level**: Validate against JSON Resume schema but allow all valid schema fields (for extensibility)
* **Implementation**: Use Go's json package with proper struct tags, and Elm's JSON decoders with optional fields for extensibility

## Decision: File Access Pattern
* **Approach**: Prompt user for file location via UI when application starts
* **Rationale**: Provides flexibility for users to select their resume file from any location

## Decision: Large File Handling
* **Policy**: No size limits - allow any size file without restrictions
* **Rationale**: User controls their own files; application should support any valid resume

## Decision: External File Change Detection
* **Method**: Alert user to changes when the file has been modified externally
* **Implementation**: Use filesystem watchers to detect changes and notify the user through the UI

## Decision: Docker Configuration
* **Setup**: Multi-stage Docker build with volume mount for resume.json
* **Ports**: 8080:8080
* **Rationale**: Follows containerization principle from constitution while enabling file persistence

## Technical Unknowns Resolved
* Elm/Go integration approach - Using embed package to compile Elm assets into Go binary
* JSON Resume schema handling - Using optional fields in type definitions for extensibility
* File I/O error handling - Fail gracefully with clear UI feedback as per specification