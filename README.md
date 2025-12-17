# Kanban App

A full-stack Kanban board application built with **React (Vite)**, **Spring Boot**, and **PostgreSQL**.  
The application is containerized with Docker, runs locally using Docker Compose, and is ready for Kubernetes deployment.

---

## Tech Stack

- **Frontend**: React (Vite), served via NGINX
- **Backend**: Spring Boot (Java 17, Maven)
- **Database**: PostgreSQL 15
- **Containerization**: Docker & Docker Compose
- **Orchestration**: Kubernetes / Helm
- **CI/CD Ready**

---

## Prerequisites

- Docker & Docker Compose
- Java 17 (only if running backend without Docker)
- Node.js >= 16 (only if running frontend without Docker)

---

## Environment Configuration

Secrets are not committed to the repository.

Create a `.env` file at the project root (same level as `docker-compose.yml`).

```env
POSTGRES_DB=kanbandb
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres

SPRING_DATASOURCE_URL=jdbc:postgresql://postgres:5432/kanbandb
SPRING_DATASOURCE_USERNAME=postgres
SPRING_DATASOURCE_PASSWORD=postgres
SERVER_PORT=8085

```

## Run with Docker Compose

Starts PostgreSQL, backend, and frontend together.

```
docker compose up --build
```
Services
```
Frontend: http://localhost:3001

Backend API: http://localhost:8085
```
PostgreSQL: Internal Docker network (not exposed)


API Endpoints
```
GET /api/tasks

POST /api/tasks

PUT /api/tasks/{id}

DELETE /api/tasks/{id}
```
