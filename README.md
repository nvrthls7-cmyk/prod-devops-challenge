KANBAN APP (React + Spring Boot + PostgreSQL)

A simple Kanban board application built with a React (Vite) frontend, Spring Boot backend, and PostgreSQL database.
The application is containerized with Docker, runs locally using Docker Compose, and is ready for Kubernetes / EKS deployment.

TECH STACK
Frontend: React (Vite) served via NGINX
Backend: Spring Boot (Java 17, Maven) running on port 8085
Database: PostgreSQL 15
Containerization: Docker & Docker Compose
Orchestration-ready: Kubernetes / Helm / CI/CD

PREREQUISITES
Docker & Docker Compose
Java 17 (only if running backend without Docker)
Node.js >= 16 (only if running frontend without Docker)

ENVIRONMENT CONFIGURATION
Secrets are not committed to the repository.
Create a .env file at the project root (same level as docker-compose.yml).

Example .env file:

POSTGRES_DB=kanbandb
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres

SPRING_DATASOURCE_URL=jdbc:postgresql://postgres:5432/kanbandb
SPRING_DATASOURCE_USERNAME=postgres
SPRING_DATASOURCE_PASSWORD=postgres
SERVER_PORT=8085

The .env file is ignored using .gitignore.

RUN WITH DOCKER COMPOSE (RECOMMENDED)
This starts PostgreSQL, backend, and frontend together.

docker compose up --build

SERVICES
Frontend: http://localhost:3001
Backend API: http://localhost:8085
PostgreSQL: Internal Docker network (not exposed)

RUN SERVICES MANUALLY (OPTIONAL)

Start PostgreSQL:
docker compose up -d postgres

Run Backend (Java 17 + Maven required):
cd backend
mvn spring-boot:run

Backend runs on:
http://localhost:8085

Run Frontend (Node.js >= 16 required):
cd frontend
npm install
npm run dev

Frontend runs on:
http://localhost:5173

API requests are routed through NGINX to the backend using /api.

API ENDPOINTS
GET /api/tasks
POST /api/tasks
PUT /api/tasks/{id}
DELETE /api/tasks/{id}

NOTES
Configuration is fully environment-variable driven.
No secrets are hardcoded in the repository.
Frontend communicates with backend via /api reverse proxy.
Works locally, with Docker, and in Kubernetes without code changes.

PRODUCTION & KUBERNETES
Backend reads database credentials from environment variables.
PostgreSQL credentials should be injected using Kubernetes Secrets.
Frontend uses relative API paths (/api/*) and works behind Ingress.
Ready for Helm charts and CI/CD pipelines.
