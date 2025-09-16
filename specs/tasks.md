# Tasks für Feature: Task List (MVP)

Feature-Name: Task List (MVP)
Feature-Spezifikation: /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/specs/feature-tasklist-mvp.md

Hinweis: [P] kennzeichnet Tasks, die parallel ausgeführt werden können. Abhängigkeiten werden im Feld "Depends on" angegeben. Jeder Task ist so formuliert, dass ein LLM-Agent ihn ausführen kann.

T001 - Setup Repository & Verzeichnisse
- Description: Erstelle Basisordner für frontend, backend und infra und initialisiere git-ignorierte Konfigurationsdateien.
- Files to create/modify:
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/backend/  (directory)
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/frontend/ (directory)
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/infra/ (directory)
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/.env.example
- Commands (agent): mkdir -p backend frontend infra && echo "POSTGRES_USER=dev POSTGRES_PASSWORD=dev POSTGRES_DB=dev dburl=postgresql://dev:dev@db:5432/dev" > .env.example
- Depends on: none
- Status: DONE (T001)  <!-- geändert -->

T002 - Create docker-compose.yml (infra)
- Description: Erstelle docker-compose.yml mit services: frontend, backend, db (postgres) und Volume für Postgres.
- File: /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/docker-compose.yml
- Commands (agent): write docker-compose.yml with services: backend (build ./backend, ports 8000:8000), frontend (build ./frontend, ports 3000:3000), db (image: postgres:15, env from .env, volume named pgdata)
- Depends on: T001
- Status: DONE (T002)  <!-- geändert -->

T003 - Backend: package.json und TypeScript Setup
- Description: Initialisiere Node.js Projekt mit TypeScript im backend-Ordner.
- Files: /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/backend/package.json, tsconfig.json
- Commands (agent): cd backend && npm init -y && npm install express prisma @prisma/client cors dotenv && npm install -D typescript ts-node-dev @types/express @types/node && npx tsc --init
- Depends on: T001
- [P]

T004 - Backend: Prisma Schema & Migration
- Description: Erstelle prisma schema mit Task Modell und initiale migration.
- Files: /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/backend/prisma/schema.prisma
- Commands (agent): create schema.prisma with datasource env("DATABASE_URL") provider "postgresql" and Task model (see data-model.md). Then cd backend && npx prisma migrate dev --name init --preview-feature (or npx prisma migrate deploy in container)
- Depends on: T003, T002 (DB up for migration) 

T005 - Backend: Implementiere Express-Server & CRUD Endpoints
- Description: Implementiere Express App mit Endpunkten unter /api/tasks (GET, POST, GET/:id, PUT/:id, DELETE/:id) und Prisma-Client Integration.
- Files:
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/backend/src/index.ts
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/backend/src/routes/tasks.ts
- Commands (agent): Create index.ts that loads express, cors, dotenv, connects to Prisma client, mounts /api/tasks router. Create tasks router implementing endpoints and using prisma.task.
- Depends on: T003, T004

T006 - Backend: Dockerfile
- Description: Erstelle Dockerfile für Backend mit Node 18, baue TypeScript zu JS und setze Entrypoint.
- File: /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/backend/Dockerfile
- Commands (agent): write Dockerfile that copies package.json, installs deps, copies source, runs tsc, and starts node dist/index.js (or use node -r ts-node/register for dev).
- Depends on: T003
- [P]

T007 - Frontend: Vite React App (TypeScript) und Tailwind
- Description: Initialisiere Vite React App im frontend-Ordner, installiere Tailwind CSS.
- Files:
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/frontend/package.json
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/frontend/src/main.tsx
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/frontend/index.html
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/frontend/tailwind.config.cjs
- Commands (agent): cd frontend && npm init vite@latest . -- --template react-ts && npm install && npm install -D tailwindcss postcss autoprefixer && npx tailwindcss init -p; add Tailwind directives to src/index.css
- Depends on: T001
- [P]

T008 - Frontend: Implementiere UI Komponenten (List, Item, Form)
- Description: Baue React-Komponenten: TaskList, TaskItem, TaskForm. Nutze fetch an /api/tasks.
- Files:
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/frontend/src/components/TaskList.tsx
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/frontend/src/components/TaskItem.tsx
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/frontend/src/components/TaskForm.tsx
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/frontend/src/App.tsx
- Commands (agent): Implement components using fetch to GET/POST/PUT/DELETE and Tailwind classes for styling
- Depends on: T007, T005

T009 - Frontend: Dockerfile
- Description: Erstelle Dockerfile für Frontend, baue Produktion mit Vite und bediene mit nginx oder serve.
- File: /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/frontend/Dockerfile
- Commands (agent): write multistage Dockerfile: build with node, serve static with nginx (or use serve)
- Depends on: T007
- [P]

T010 - .env und .env.example aktualisieren
- Description: Erstelle .env.example und Dokumentation für DATABASE_URL und Ports.
- Files:
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/.env.example (update)
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/backend/.env.example (optional)
- Commands (agent): ensure DATABASE_URL=postgresql://dev:dev@db:5432/dev in .env.example
- Depends on: T001

T011 - Contracts tests [P]
- Description: Erstelle einfache contract/integration tests für die API-Verträge (basierend auf specs/contracts/api.md). Markiert [P] da unabhängig.
- Files:
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/backend/tests/contract_api.test.ts
- Commands (agent): Write tests using node-fetch or supertest to assert endpoints behave per contracts (GET /api/tasks returns 200 array, POST creates etc.)
- Depends on: T003
- [P]

T012 - Model creation task [P]
- Description: Erzeuge Prisma Model für Task (gemäß data-model.md). Dies ist ein eigenständiger Model-Task.
- Files:
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/backend/prisma/schema.prisma
- Commands (agent): Ensure Task model exists in schema.prisma (id,title,description,completed,createdAt,updatedAt) and run prisma generate.
- Depends on: T003
- [P]

T013 - Integration: DB Connection & Health Endpoint
- Description: Implementiere DB-Connection-Check und /health Endpoint auf Backend.
- Files:
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/backend/src/index.ts (or health.ts)
- Commands (agent): Add /health route that returns 200 and verifies Prisma can query SELECT 1.
- Depends on: T004, T005

T014 - Integration tests for user stories [P]
- Description: Erstelle Integrationstests, die User Stories abdecken (Create, Read, Update, Delete flows).
- Files:
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/backend/tests/integration_tasks.test.ts
- Commands (agent): Implement tests that run against running docker-compose (or spin up test DB) and verify full flow: create task -> fetch list -> update -> delete.
- Depends on: T005, T004
- [P]

T015 - Docker Compose Run & Smoke Test
- Description: Baue alle Images und starte docker-compose, prüfe, dass Frontend (3000) und Backend (8000) erreichbar.
- Commands (agent): docker-compose up --build -d && curl -fsS http://localhost:8000/api/tasks && curl -fsS http://localhost:3000 || (report failures)
- Depends on: T006, T009, T002

T016 - Documentation: Quickstart und README Update
- Description: Aktualisiere quickstart.md und README im Repo-Root mit Start-Anleitung und Ports.
- Files:
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/specs/quickstart.md
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/README.md
- Commands (agent): Ensure quickstart contains `docker-compose up --build` steps, ports, and .env instructions
- Depends on: T002, T010

T017 - Polish: Basic Unit Tests and Lint
- Description: Füge einfache unit tests für backend service layer und ESLint/Prettier config.
- Files:
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/backend/.eslintrc.js
  - /Users/oliverkarst/Development/ai/VibeCoding/spec-kit-tasks-app/backend/tests/unit_service.test.ts
- Commands (agent): npm install -D jest ts-jest @types/jest and add simple test for service functions
- Depends on: T005

T018 - Optional: Switch id to UUID
- Description: Wenn gewünscht, migriere Prisma Task.id zu UUID und passe Code/Migrations an.
- Files: prisma/schema.prisma and migration files
- Commands (agent): modify schema.prisma id to String @id @default(uuid()) and run migration
- Depends on: T012

Parallel Execution Guidance
- Can run in parallel: T003, T007, T011, T012 (independent installs and model creation) as [P]
- Sequence required: T005 depends on T003/T004; T008 depends on T007 and T005.

Agent Commands Summary (examples)
- Create backend skeleton: mkdir -p backend && cd backend && npm init -y
- Create frontend skeleton: npm create vite@latest frontend --template react-ts
- Start dev stack locally: docker-compose up --build

Progress Tracking (initial)
- Setup tasks: completed (T001)
- Tests: templates created (contract & integration) pending implementation
- Core implementation: pending

End of tasks
