# Kanban App (React + Spring Boot + PostgreSQL)

A simple Kanban board application built with a React (Vite) frontend, Spring Boot backend, and PostgreSQL database.  
Designed to run locally with Docker Compose and deploy cleanly to Kubernetes.

---

## Tech Stack

- **Frontend**: React (Vite), served via NGINX
- **Backend**: Spring Boot (Java 17, Maven), runs on port `8085`
- **Database**: PostgreSQL 15
- **Containerization**: Docker & Docker Compose
- **Production-ready**: Kubernetes / EKS compatible

---

## Prerequisites

- Docker & Docker Compose
- Java 17 (only if running backend without Docker)
- Node.js >= 16 (only if running frontend without Docker)

---

## Environment Configuration (IMPORTANT)

Secrets and configuration are **not committed** to GitHub.

### Create `.env` file (at project root)

```bash
cp .env.example .env


an example here!!!!!

POSTGRES_DB=kanbandb
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres

SPRING_DATASOURCE_URL=jdbc:postgresql://postgres:5432/kanbandb
SPRING_DATASOURCE_USERNAME=postgres
SPRING_DATASOURCE_PASSWORD=postgres
SERVER_PORT=8085
