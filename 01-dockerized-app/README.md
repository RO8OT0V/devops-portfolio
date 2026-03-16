# Dockerized Application

Simple web application demonstrating Docker best practices.

## What This Shows

- Multi-stage Docker builds for optimized image size
- Docker Compose for local development
- Health checks and proper signal handling
- Environment-based configuration

## Quick Start

```bash
# Build and run
docker-compose up --build

# Run tests
docker-compose run app pytest

# Production build
docker build -t myapp:latest --target production .
```

## Project Structure

```
.
├── Dockerfile           # Multi-stage build
├── docker-compose.yml   # Local development
├── docker-compose.prod.yml  # Production overrides
├── src/
│   └── app.py          # Application code
├── tests/
│   └── test_app.py     # Unit tests
└── README.md
```

## Features

- ✅ Multi-stage build (dev → production)
- ✅ Non-root user in container
- ✅ Health check endpoint
- ✅ Graceful shutdown handling
- ✅ Environment variables for config
