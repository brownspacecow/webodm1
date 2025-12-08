# What is this project?

This is my simple docker-compose file that allows for more than one webodm instance to run on the same host.  To spin up multiple instances just copy the folder to a new location and modify desired values in
.env file

# WebODM 

A Docker Compose setup for running WebODM (Web Orthomosaic and Digital Elevation Model) - an open-source toolkit for processing drone imagery into maps and 3D models.

## Overview

This project deploys a complete WebODM instance using Docker Compose with the following services:

- **PostgreSQL Database** (`webodm1_db`) - Stores all project and user data
- **Redis Broker** (`webodm1_broker`) - Message queue for task processing
- **WebODM Webapp** (`webodm1_webapp`) - Main web interface
- **Worker** (`webodm1_worker`) - Background task processor for image processing

## Quick Start

### Prerequisites
- Docker and Docker Compose installed
- At least 2GB of available disk space

### Installation

1. Navigate to the project directory:
```bash
cd /home/sun/webodm1
```

2. Start all services:
```bash
docker-compose up -d
```

3. Access WebODM at: `http://localhost:6001`

### Stopping Services

```bash
docker-compose down
```

## Configuration

Environment variables are stored in `.env`:

## Running Multiple Instances

This setup supports running multiple WebODM instances simultaneously. Each instance uses:
- A unique project name prefix (`webodm1`, `webodm2`, etc.) (only changes needed are in the .env file)
- A different port number
- Isolated databases and volumes
- Separate media directories

Example for a second instance:
```bash
cd /home/sun/webodm2
docker-compose up -d
# Access at http://localhost:6002
```

## Database Access

To query the PostgreSQL database directly:

```bash
docker exec -it webodm1_db psql -U postgres
```

Common PostgreSQL commands:
- `\l` - List databases
- `\dt` - List tables
- `\q` - Quit

## Upgrading

To upgrade to the latest image versions:

```bash
docker-compose pull
docker-compose up -d
```

## Storage

Media files and database data are persisted in mapped paths in the example .env

## Support

For more information about WebODM, visit: https://www.opendronemap.org/webodm/
