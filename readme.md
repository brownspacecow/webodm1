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

- `WO_PORT` - Port to access the web interface (default: 6001)
- `WO_DEBUG` - Debug mode (NO/YES)
- `WO_MEDIA_DIR` - Directory for media files
- `WO_DB_DIR` - Database volume location
- `WO_BROKER` - Redis broker URL

## Running Multiple Instances

This setup supports running multiple WebODM instances simultaneously. Each instance uses:
- A unique project name prefix (`webodm1`, `webodm2`, etc.)
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

## Logs

View logs from all services:
```bash
docker-compose logs -f
```

View logs from a specific service:
```bash
docker-compose logs -f webapp
```

## Upgrading

To upgrade to the latest image versions:

```bash
docker-compose pull
docker-compose up -d
```

## Storage

Media files and database data are persisted in Docker volumes:
- `webodm1_dbdata` - PostgreSQL database
- `webodm1_appmedia` - Uploaded drone images and processing results

## Support

For more information about WebODM, visit: https://www.opendronemap.org/webodm/
