# Quickstart Guide: JSON Resume Editor

## Prerequisites
- Docker (v20.10 or higher)
- Docker Compose (v2.0 or higher)
- A JSON Resume file (e.g., `resume.json`)

## Getting Started

### 1. Clone and Navigate
```bash
# If you haven't already, clone the repository
git clone <repository-url>
cd <repository-name>
```

### 2. Prepare Your Resume File
Place your `resume.json` file in the project directory, or have the path ready to the JSON Resume file you want to edit.

### 3. Start the Application
```bash
# From the project root directory
docker compose up
```

### 4. Access the Application
Open your browser and navigate to `http://localhost:8080`

### 5. Load Your Resume
When the application starts, you'll be prompted to select your resume file. Browse to your `resume.json` file and load it.

### 6. Edit Your Resume
Make changes to your resume through the form-based interface. The application will preserve the JSON structure while you edit.

### 7. Save Your Changes
Click the "Save" button to write your changes back to the resume file on disk.

## Development

### Building from Source
```bash
# Build the frontend (Elm)
cd frontend
npx elm make src/Main.elm --output=../backend/dist/main.js

# Build the backend (Go)
cd ../backend
go build -o ../dist/resume-editor .

# Build the Docker image
docker build -t resume-editor .
```

### Running with Docker Compose for Development
```bash
# This mounts the current directory to allow real-time file access
docker compose up
```

## Troubleshooting

### Application Won't Start
- Ensure Docker and Docker Compose are running
- Check that port 8080 isn't already in use

### Can't Find Resume File
- Ensure your resume.json file is in the same directory as docker-compose.yml
- Check that the application has read/write permissions for the file

### Save Operations Fail
- Verify that the application has write permissions to the resume file
- Check that your resume JSON is valid according to the schema