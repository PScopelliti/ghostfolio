**Docker Commands for Ghostfolio**

🚀 Production Build (docker-compose.build.yml)
Build and run the complete application stack:
# Start all services (build image locally)
docker compose -f docker/docker-compose.build.yml up -d

# Start with fresh build (no cache)
docker compose -f docker/docker-compose.build.yml up -d --build

# Stop all services
docker compose -f docker/docker-compose.build.yml down

# Stop and remove volumes (wipes database!)
docker compose -f docker/docker-compose.build.yml down -v

# Restart all services
docker compose -f docker/docker-compose.build.yml restart

# View status
docker compose -f docker/docker-compose.build.yml ps

# View logs (all services)
docker compose -f docker/docker-compose.build.yml logs -f

# View logs (specific service)
docker compose -f docker/docker-compose.build.yml logs -f ghostfolio
docker compose -f docker/docker-compose.build.yml logs -f postgres
docker compose -f docker/docker-compose.build.yml logs -f redis

🛠️ Development (docker-compose.dev.yml)
Run only PostgreSQL and Redis for local development:
# Start database and Redis only
docker compose -f docker/docker-compose.dev.yml up -d

# Stop services
docker compose -f docker/docker-compose.dev.yml down

# Stop and wipe database
docker compose -f docker/docker-compose.dev.yml down -v

# View logs
docker compose -f docker/docker-compose.dev.yml logs -f

🐳 Production (docker-compose.yml)
Use the official pre-built image:
# Start with official image
docker compose -f docker/docker-compose.yml up -d

# Pull latest image and restart
docker compose -f docker/docker-compose.yml pull
docker compose -f docker/docker-compose.yml up -d

# Stop all services
docker compose -f docker/docker-compose.yml down

🔧 Useful Docker Commands
# Execute shell in container
docker exec -it ghostfolio sh
docker exec -it gf-postgres-build psql -U user -d ghostfolio-db
docker exec -it gf-redis-build redis-cli

# Check container health
docker inspect ghostfolio --format='{{.State.Health.Status}}'

# View resource usage
docker stats ghostfolio gf-postgres-build gf-redis-build

# Clean up unused images
docker image prune -a

# Clean up everything (containers, networks, volumes, images)
docker system prune -a --volumes

📁 Configuration Files
* docker/docker-compose.ymlb- Production with official image
* docker/docker-compose.build.yml- Build locally + full stack
* docker/docker-compose.dev.yml- DB/Redis only for local dev
* .env - Environment variables (hosts must use service names for Docker)
