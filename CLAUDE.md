# Claude Code Development Guide

This document contains information to help Claude Code assist with development of this project.

## Project Structure

- **Backend**: Strapi application (submodule connected to Railway)
  - Postgres database hosted on Railway
  - Environment variables managed through Railway
  - GraphQL plugin enabled
  - Digital Ocean Spaces for media storage

- **Frontend**: Nuxt.js application
  - Vue 3 based frontend
  - Connects to Strapi API

## Development Environment

- Docker Compose setup for local development
- The project uses the production Railway database directly in development
- Project uses Yarn as the package manager (not npm)

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
docker-compose exec backend yarn add <package-name>

# Run Strapi CLI commands
docker-compose exec backend yarn strapi <command>
```

### Frontend (Nuxt)

```bash
# Access Nuxt container
docker-compose exec frontend sh

# Install a new package
docker-compose exec frontend yarn add <package-name>
```

## Configuration Files

- `.env` - Contains environment variables (not committed to git)
- `docker-compose.yml` - Docker Compose configuration
- `backend/Dockerfile.dev` - Dockerfile for Strapi development (uses Node 20.12.2)
- `frontend/Dockerfile.dev` - Dockerfile for Nuxt development

## Digital Ocean Spaces Configuration

Required environment variables for Digital Ocean Spaces:
- `DO_SPACE_ACCESS_KEY` - Digital Ocean Spaces access key
- `DO_SPACE_SECRET_KEY` - Digital Ocean Spaces secret key
- `DO_SPACE_ENDPOINT` - Digital Ocean Spaces endpoint (e.g., 'nyc3.digitaloceanspaces.com')
- `DO_SPACE_BUCKET` - Digital Ocean Spaces bucket name
- `DO_SPACE_REGION` - Digital Ocean Spaces region (e.g., 'nyc3')
- `DO_SPACE_BASE_URL` - (Optional) CDN URL if configured

## Notes for Claude

- This is a personal blog project
- The backend is a git submodule connected to Railway
- The project uses production database in development (personal choice for this project)
- When testing, make sure to use a local test data approach rather than affecting production data
- IMPORTANT: Project uses Yarn instead of npm for all package management

## GraphQL Schema Reference

This project uses Strapi v5 with GraphQL. Here are reference queries for common operations:

### Posts Query with Dynamic Content Zones

```graphql
query {
  posts {
    title
    slug
    publishedAt
    updatedAt
    content {
      __typename
      ... on ComponentContentBlockHeadingBlock {
        heading
        level
      }
      ... on ComponentContentBlockTextBlock {
        text
      }
      ... on ComponentContentBlockMediaGrid {
        images {
          caption
          image {
            url
            alternativeText
          }
        }
      }
      ... on ComponentContentBlockImageBlock {
        caption
        image {
          url
          width
          height
          alternativeText
          formats
        }
      }
    }
  }
}
```

### Landing Page Query

```graphql
query {
  landingPage {
    Title
    Description
  }
}
```

### Important Notes on GraphQL in Strapi v5

- Response format is flattened compared to v4 (no data/attributes nesting)
- Dynamic Zones require explicit type selection with fragments
- Media fields need nested selection of properties (url, width, etc.)
- Always check field names in GraphQL playground before writing queries