# Personal Blog

A personal blog built with Strapi (backend) and Nuxt.js (frontend).

## Development Setup with Docker

This project uses Docker Compose for local development while connecting to a production Railway PostgreSQL database.

### Prerequisites

- Docker and Docker Compose
- Railway account with PostgreSQL database

### Setup

1. Clone this repository with submodules:
   ```
   git clone --recurse-submodules <repository-url>
   ```

2. Create an `.env` file:
   ```
   cp .env.example .env
   ```

3. Fill in your Railway database credentials and Strapi secrets in the `.env` file.

4. Build and start the containers:
   ```
   docker-compose up -d
   ```

5. Access:
   - Frontend: http://localhost:3000
   - Strapi Admin: http://localhost:1337/admin

### Development Workflow

- Backend (Strapi) code changes will automatically reload
- Frontend (Nuxt.js) code changes will automatically reload
- Database changes will directly affect your production database - use with caution

### Notes on Using Production Database

- This setup connects directly to your production Railway database for simplicity
- Be careful when making schema changes or bulk operations
- Consider creating backups before significant changes