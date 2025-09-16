# TaskMgr - VibeCode Spec-Kit

Ein moderner Task-Manager entwickelt mit dem GitHub Spec-Kit Framework und VibeCode. Diese Anwendung demonstriert eine vollständige Full-Stack-Lösung mit React Frontend, Node.js Backend und PostgreSQL Datenbank.

## 🎯 Projektübersicht

**TaskMgr** ist eine containerisierte Task-Management-Anwendung, die als MVP (Minimum Viable Product) entwickelt wird. Das Projekt nutzt das GitHub Spec-Kit für strukturierte Entwicklung und zeigt moderne Web-Entwicklungspraktiken.

### Hauptfunktionen
- ✅ Tasks erstellen, bearbeiten und löschen (CRUD)
- 📝 Task-Details mit Titel, Beschreibung und Status
- 🎨 Modernes, responsives UI mit Tailwind CSS
- 🐳 Vollständig containerisiert mit Docker Compose
- 🔄 RESTful API mit JSON-Responses
- 💾 Persistente Datenspeicherung mit PostgreSQL

## 🏗️ Architektur

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Frontend      │    │    Backend      │    │   Database      │
│   React + TS    │◄──►│  Node.js + TS   │◄──►│  PostgreSQL     │
│   Port: 3000    │    │   Port: 8000    │    │   Port: 5432    │
│   Tailwind CSS  │    │   Express API   │    │   Prisma ORM    │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

### Tech Stack
- **Frontend**: React 18, TypeScript, Vite, Tailwind CSS
- **Backend**: Node.js, Express, TypeScript, Prisma ORM
- **Database**: PostgreSQL 15
- **Containerisierung**: Docker, Docker Compose
- **Development**: GitHub Spec-Kit Framework

## 🚀 Quickstart

### Voraussetzungen
- Docker & Docker Compose installiert
- Git installiert
- Node.js 18+ (für lokale Entwicklung)

### Installation & Start

1. **Repository klonen**
   ```bash
   git clone <repository-url>
   cd TaskMgr-VibeCode-Spec-kit-github
   ```

2. **Umgebungsvariablen konfigurieren**
   ```bash
   cp spec-kit-tasks-app/.env.example spec-kit-tasks-app/.env
   ```

3. **Anwendung starten**
   ```bash
   cd spec-kit-tasks-app
   docker-compose up --build
   ```

4. **Anwendung öffnen**
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:8000
   - API Dokumentation: http://localhost:8000/api/tasks

### Entwicklungsmodus

Für lokale Entwicklung ohne Docker:

```bash
# Backend starten
cd spec-kit-tasks-app/backend
npm install
npm run dev

# Frontend starten (neues Terminal)
cd spec-kit-tasks-app/frontend
npm install
npm run dev
```

## 📋 API Endpoints

| Method | Endpoint | Beschreibung |
|--------|----------|--------------|
| GET | `/api/tasks` | Alle Tasks abrufen |
| POST | `/api/tasks` | Neuen Task erstellen |
| GET | `/api/tasks/:id` | Einzelnen Task abrufen |
| PUT | `/api/tasks/:id` | Task aktualisieren |
| DELETE | `/api/tasks/:id` | Task löschen |
| GET | `/health` | Health Check |

### Beispiel API Calls

```bash
# Alle Tasks abrufen
curl http://localhost:8000/api/tasks

# Neuen Task erstellen
curl -X POST http://localhost:8000/api/tasks \
  -H "Content-Type: application/json" \
  -d '{"title": "Mein erster Task", "description": "Task Beschreibung"}'

# Task als erledigt markieren
curl -X PUT http://localhost:8000/api/tasks/1 \
  -H "Content-Type: application/json" \
  -d '{"completed": true}'
```

## 📊 Datenmodell

```typescript
interface Task {
  id: number;
  title: string;
  description?: string;
  completed: boolean;
  createdAt: Date;
  updatedAt: Date;
}
```

## 📁 Projektstruktur

```
TaskMgr-VibeCode-Spec-kit-github/
├── spec-kit-tasks-app/           # Hauptanwendung
│   ├── frontend/                 # React Frontend
│   │   ├── src/
│   │   │   ├── components/       # React Komponenten
│   │   │   ├── App.tsx          # Haupt-App Komponente
│   │   │   └── main.tsx         # Entry Point
│   │   ├── Dockerfile           # Frontend Container
│   │   └── package.json
│   ├── backend/                  # Node.js Backend
│   │   ├── src/
│   │   │   ├── routes/          # API Routes
│   │   │   └── index.ts         # Server Entry Point
│   │   ├── prisma/
│   │   │   └── schema.prisma    # Datenbankschema
│   │   ├── Dockerfile           # Backend Container
│   │   └── package.json
│   ├── infra/                   # Infrastructure Code
│   ├── docker-compose.yml       # Container Orchestrierung
│   └── .env.example            # Umgebungsvariablen Template
├── specs/                       # Spezifikationen
│   ├── tasks.md                # Task-Definitionen
│   ├── feature-tasklist-mvp.md # Feature-Spezifikation
│   └── data-model.md           # Datenmodell
├── scripts/                     # Entwicklungsscripts
└── README.md                   # Diese Datei
```

## 🔧 Entwicklung

### Spec-Kit Framework

Dieses Projekt nutzt das GitHub Spec-Kit für strukturierte Entwicklung:

- **Spezifikationen** in `/specs/` definieren Features und Anforderungen
- **Tasks** in `/specs/tasks.md` beschreiben konkrete Implementierungsschritte
- **Scripts** in `/scripts/` automatisieren Entwicklungsprozesse

### Verfügbare Scripts

```bash
# Setup neues Feature
./scripts/create-new-feature.sh

# Task-Voraussetzungen prüfen
./scripts/check-task-prerequisites.sh

# Agent-Kontext aktualisieren
./scripts/update-agent-context.sh
```

## 📈 Aktueller STATUS

### ✅ Abgeschlossen
- [x] **T001**: Repository & Verzeichnisstruktur Setup
- [x] **T002**: Docker Compose Konfiguration
- [x] Projektdokumentation und README

### 🚧 In Arbeit
- [ ] **T003**: Backend Node.js & TypeScript Setup
- [ ] **T007**: Frontend React & Vite Setup

### 📋 Geplant
- [ ] **T004**: Prisma Schema & Database Migration
- [ ] **T005**: Backend API Endpoints Implementation
- [ ] **T008**: Frontend UI Komponenten
- [ ] **T006/T009**: Docker Container für Backend/Frontend
- [ ] **T015**: Integration & Smoke Tests

Detaillierte Task-Liste siehe: [specs/tasks.md](specs/tasks.md)

## 🧪 Tests

```bash
# Backend Tests
cd spec-kit-tasks-app/backend
npm test

# Integration Tests
npm run test:integration

# Contract Tests
npm run test:contract
```

## 🐳 Docker Commands

```bash
# Alle Services starten
docker-compose up --build

# Services im Hintergrund starten
docker-compose up -d

# Logs anzeigen
docker-compose logs -f

# Services stoppen
docker-compose down

# Volumes löschen (Daten zurücksetzen)
docker-compose down -v
```

## 🔍 Troubleshooting

### Häufige Probleme

**Port bereits belegt**
```bash
# Ports prüfen
lsof -i :3000
lsof -i :8000
lsof -i :5432
```

**Database Connection Error**
```bash
# Container Status prüfen
docker-compose ps

# Database Logs prüfen
docker-compose logs db
```

**Frontend Build Fehler**
```bash
# Node Modules neu installieren
cd spec-kit-tasks-app/frontend
rm -rf node_modules package-lock.json
npm install
```

## 🤝 Beitragen

1. Fork das Repository
2. Erstelle einen Feature Branch (`git checkout -b feature/amazing-feature`)
3. Committe deine Änderungen (`git commit -m 'Add amazing feature'`)
4. Push zum Branch (`git push origin feature/amazing-feature`)
5. Öffne eine Pull Request

## 📝 Lizenz

Dieses Projekt ist unter der MIT Lizenz veröffentlicht. Siehe `LICENSE` Datei für Details.

## 🔗 Links

- [GitHub Spec-Kit](https://github.com/github/spec-kit)
- [VibeCode Documentation](https://vibecode.dev)
- [React Documentation](https://react.dev)
- [Prisma Documentation](https://prisma.io)
- [Docker Compose Documentation](https://docs.docker.com/compose/)

---

**Entwickelt mit ❤️ und dem GitHub Spec-Kit Framework**
