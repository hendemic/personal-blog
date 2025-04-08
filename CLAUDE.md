# Claude Code Development Guide

This document contains information to help Claude Code assist with development of this project.

## Project Structure

- **Backend**: Strapi application (submodule connected to Railway)
  - Postgres database hosted on Railway
  - Environment variables managed through Railway
  - GraphQL plugin enabled

- **Frontend**: Nuxt.js application
  - Vue 3 based frontend
  - Connects to Strapi API

## Development Environment

- Docker Compose setup for local development
- The project uses the production Railway database directly in development

## Common Commands

### Docker

```bash
# Start the development environment
docker-compose up -d

# View logs
docker-compose logs -f

# Rebuild containers
docker-compose build

# Stop containers
docker-compose down
```

### Backend (Strapi)

```bash
# Access Strapi container
docker-compose exec backend sh

# Install a new package
docker-compose exec backend npm install <package-name>

# Run Strapi CLI commands
docker-compose exec backend npm run strapi <command>
```

### Frontend (Nuxt)

```bash
# Access Nuxt container
docker-compose exec frontend sh

# Install a new package
docker-compose exec frontend npm install <package-name>
```

## Configuration Files

- `.env` - Contains environment variables (not committed to git)
- `docker-compose.yml` - Docker Compose configuration
- `backend/Dockerfile.dev` - Dockerfile for Strapi development
- `frontend/Dockerfile.dev` - Dockerfile for Nuxt development

## Notes for Claude

- This is a personal blog project
- The backend is a git submodule connected to Railway
- The project uses production database in development (personal choice for this project)
- When testing, make sure to use a local test data approach rather than affecting production data