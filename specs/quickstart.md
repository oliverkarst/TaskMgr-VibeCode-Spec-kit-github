# Quickstart

Voraussetzungen

- Docker und Docker Compose installiert

Starten

1. Im Repo-Root `docker-compose up --build` ausführen.
2. Frontend: http://localhost:3000
3. Backend: http://localhost:8000

Env

- Kopiere `.env.example` nach `.env` und passe Variablen an (POSTGRES_USER, POSTGRES_PASSWORD, POSTGRES_DB, DATABASE_URL)

Datenbank

- Postgres speichert Daten in einem Docker-Volume, so bleiben Daten nach Neustarts erhalten.

Entwicklung

- Frontend: Vite Dev Server mit HMR
- Backend: ts-node-dev oder nodemon für automatischen Neustart
