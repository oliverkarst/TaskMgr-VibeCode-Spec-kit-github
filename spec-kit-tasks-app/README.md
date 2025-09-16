# spec-kit-tasks-app

...existing code...

## Quickstart

1. Kopiere die Beispiel-Umgebungsdatei:
   cp .env.example .env
   Passe bei Bedarf die Werte in `.env` an (DATABASE_URL / POSTGRES_*).

2. Starte die Anwendung mit Docker Compose:
   docker-compose up --build -d

3. Erreichbarkeit:
   - Backend API: http://localhost:8000/api/tasks
   - Frontend: http://localhost:3000
   - PostgreSQL (Port weitergeleitet): 5432

4. Stoppen:
   docker-compose down

...existing code...