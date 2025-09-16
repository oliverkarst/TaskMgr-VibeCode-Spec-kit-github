# Feature: Task List (MVP)

## Zusammenfassung
Eine einfache, moderne Task-Listen-Anwendung (MVP) namens "VibeCoding Tasks". Nutzer können Tasks anlegen, bearbeiten und löschen. Frontend und Backend laufen containerisiert lokal (separate Container) und das Backend stellt eine HTTP-API zur Persistierung in einer Datenbank bereit.

## Motivation
Ich möchte VibeCoding besser kennenlernen, indem ich eine kleine, vollständige Anwendung entwickle, die Frontend, Backend, Persistenz und Containerisierung demonstriert. Der Fokus liegt auf einfacher Bedienbarkeit, modernem UI und einfacher lokaler Entwicklung.

## Ziele
- CRUD-Funktionalität für Tasks (Create, Read, Update, Delete).
- Modernes, responsives Frontend (React oder vergleichbar).
- RESTful JSON-API im Backend (z. B. Node/Express oder Python/FastAPI).
- Persistenz in einer lokal laufenden Datenbank (z. B. PostgreSQL oder SQLite in einem Container).
- Containerisierte Entwicklung mit Docker Compose, so dass Frontend, Backend und DB separat laufen.
- Minimaler, klarer MVP-Umfang, einfaches Setup (ein Befehl zum Starten).

## Nicht-Ziele
- Authentifizierung/Autorisierung (in MVP nicht enthalten).
- Umfangreiche UI-Animationen oder komplexe Offline-Funktionalität.
- Skalierung für Produktion oder CI/CD-Pipelines (nur lokales MVP).

## Stakeholder
- Produktbesitzer: Projektinhaber (VibeCoding)
- Entwickler: Lokaler Entwickler, der die Architektur kennenlernen will
- Nutzer: Entwickler/Tester, die die Taskliste lokal nutzen

## Annahmen
- Die Entwicklung erfolgt lokal auf einem Rechner mit Docker/Docker Compose installiert.
- Ziel ist ein schneller, leichter Einstieg, nicht Produktionsbetrieb.

## Anforderungen (hochlevel)
- API-Endpunkte: GET /tasks, POST /tasks, GET /tasks/:id, PUT /tasks/:id, DELETE /tasks/:id
- Task-Daten: id, title, description (optional), completed (bool), created_at, updated_at
- Frontend: Liste, Erstellen-Form, Editier-UI, Löschen-Action
- Persistenz: relationale DB; einfache Migration / Start-Skript
- Container: Dockerfile für Frontend und Backend, docker-compose.yml für lokale Orchestrierung

## User Stories
- Als Nutzer möchte ich eine Liste aller Tasks sehen, damit ich Überblick habe.
- Als Nutzer möchte ich einen neuen Task erstellen, damit ich Arbeit/Ideen notieren kann.
- Als Nutzer möchte ich einen Task bearbeiten, damit ich Details anpassen kann.
- Als Nutzer möchte ich einen Task löschen, damit ich erledigte/irrelevante Einträge entfernen kann.

## Akzeptanzkriterien
- UI zeigt alle Tasks an und aktualisiert nach Erstellen/Bearbeiten/Löschen.
- API antwortet mit JSON und passenden HTTP-Statuscodes.
- Daten bleiben nach Neustart der Container erhalten (DB-Volume oder persistente DB).
- Projekt startet lokal mit einem einzigen Befehl: `docker-compose up --build`.

## API-Spezifikation (kurz)
- GET /tasks
  - Antwort: 200 OK, JSON-Array von Tasks
- POST /tasks
  - Body: { title: string, description?: string }
  - Antwort: 201 Created, JSON Task
- GET /tasks/:id
  - Antwort: 200 OK oder 404 Not Found
- PUT /tasks/:id
  - Body: { title?: string, description?: string, completed?: boolean }
  - Antwort: 200 OK oder 404
- DELETE /tasks/:id
  - Antwort: 204 No Content oder 404

## Datenmodell
Task
- id: uuid oder auto-increment integer
- title: string (required)
- description: text (optional)
- to_be_completed_dt: date (optional)
- completed: boolean (default: false)
- created_at: timestamp
- updated_at: timestamp

## UI/UX (kurz)
- Hauptansicht: Liste von Cards/Rows mit Title, evtl. Description und Controls (Edit, Delete, Toggle Complete)
- Floating Action Button oder sichtbarer Button zum Erstellen eines Tasks
- Modal oder Inline-Form zum Erstellen/Bearbeiten
- Modernes, klares Design (z. B. Tailwind CSS / Material-UI)

## Technisches Design
- Frontend: React mit Vite (oder Create React App), TypeScript optional
- Backend: Node.js + Express oder FastAPI (Python) mit einfachen Endpunkten
- DB: PostgreSQL empfohlen; für minimale Komplexität kann SQLite genutzt werden, aber mit Containern ist Postgres realistischer
- Containerisierung: Zwei Dockerfiles (frontend, backend) + docker-compose.yml mit Postgres-Service

## Lokales Setup / Runbook
1. Docker & Docker Compose installieren.
2. Im Repo-Root `docker-compose up --build` ausführen.
3. Frontend verfügbar unter http://localhost:3000, Backend unter http://localhost:8000 (Portbeispiele).
4. Die Ports sollen einfach konfigurierbar sein.

## Tests
- Backend: einfache Integrationstests für API-Endpunkte (optional für MVP).
- Frontend: smoke tests, manuelles Testen für Kern-Workflows.

## Sicherheit & Datenschutz
- Keine Authentifizierung im MVP; keine sensiblen Daten erwartet.
- DB-Zugangsdaten in .env, nicht ins Repo einchecken.

## Metriken / Erfolgskriterien
- MVP lauffähig lokal mit Docker Compose.
- Kernfunktionalität (CRUD) manuell getestet und dokumentiert.

## Nächste Schritte / Erweiterungen
- Authentifizierung (z. B. OAuth oder JWT)
- Sync/Real-time (WebSockets)
- Testsuite & CI/CD
- Deployment-Setup für Produktion

---

(Ende der Spezifikation)
