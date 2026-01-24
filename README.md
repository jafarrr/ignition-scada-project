# Ignition SCADA Development Project

A portable Ignition 8.3 development environment using Docker for experimentation, development, and testing.

## Overview

This project provides a Docker-based Ignition 8.3 SCADA environment with local file editing capabilities. Ignition 8.3 uses JSON files for project assets (unlike 8.1 which uses SQLite), making it ideal for version control with Git.

## Prerequisites

- Docker Desktop installed and running
- Git installed
- At least 4GB of free RAM

## Quick Start

1. Clone this repository:
   ```bash
   git clone <repository-url>
   cd ignition-scada-project
   ```

2. Start the Ignition container:
   ```bash
   docker compose up -d
   ```

3. Access the Ignition Gateway:
   - Gateway: http://localhost:8088
   - Designer Launcher: http://localhost:8088/main/web/home/designer-launch
   - Default credentials: admin / password

4. Stop the container:
   ```bash
   docker compose down
   ```

## Project Structure

```
ignition-scada-project/
├── docker-compose.yml    # Docker configuration
├── data/                 # Ignition data directory (mounted volume)
│   └── projects/        # Your Ignition projects (JSON format)
├── .gitignore           # Git ignore rules
└── README.md            # This file
```

## Volume Mounts

The `./data` directory is mounted to `/usr/local/bin/ignition/data` in the container. This allows you to:
- Edit project files locally
- Track changes with Git
- Persist data between container restarts

## Configuration

Default gateway credentials are set in [docker-compose.yml](docker-compose.yml):
- Username: admin
- Password: password

**Important:** Change these credentials for production use.

## Development Workflow

1. Start the container with `docker compose up -d`
2. Create/modify projects through the Ignition Gateway or Designer
3. Project files will be saved as JSON in `./data/projects/`
4. Commit your changes to Git
5. Push to GitHub for backup and portability

## Portability

This project can be cloned and run on any system with Docker installed:
```bash
git clone <repository-url>
cd ignition-scada-project
docker compose up -d
```

## Ports

- 8088: HTTP Gateway interface
- 8043: HTTPS Gateway interface
- 8060: Gateway Network (for redundancy/connections)

## Troubleshooting

**Container won't start:**
- Check Docker is running: `docker ps`
- Check logs: `docker compose logs`

**Can't access Gateway:**
- Verify container is running: `docker compose ps`
- Check port 8088 isn't already in use

**Permission issues with data directory:**
- The container may need write permissions to the `./data` directory

## License

This project configuration is open source. Ignition itself requires proper licensing from Inductive Automation.
