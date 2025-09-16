# Research: Technologieentscheidungen

Kurz: Ziel ist ein einfaches, modernes MVP mit minimaler Komplexität, gutem Entwickler-Feedback und einfacher lokaler Containerisierung.

Entscheidungen

- Frontend: React mit Vite
  - Gründe: Sehr schneller Start, moderne Toolchain, große Community, einfache Integration mit TypeScript und Tailwind.
- Styling: Tailwind CSS
  - Gründe: Schnelle, konsistente, moderne UI ohne großen Overhead.
- Backend: Node.js + Express (TypeScript optional)
  - Gründe: Leichtgewichtig, einfach zu schreiben, viele Bibliotheken. Express ist für kleine APIs sehr geeignet.
- ORM: Prisma
  - Gründe: Moderne DX, gute Postgres-Unterstützung, einfache Migrations- und Schemaverwaltung.
- Datenbank: PostgreSQL in einem Container
  - Gründe: Produktionsnah, stabil, unterstützt Volumes für Persistenz.
- Containerisierung: Docker Compose mit drei Services: frontend, backend, db
  - Gründe: Einfaches lokales Setup, klare Trennung der Komponenten.

Ports (Empfehlung)
- Frontend: 3000
- Backend: 8000
- Postgres: 5432 (intern), Host-Exposition optional

Env-Variablen (Beispiele)
- POSTGRES_USER, POSTGRES_PASSWORD, POSTGRES_DB
- DATABASE_URL (für Prisma)
- BACKEND_PORT, FRONTEND_PORT

Persistenz
- Postgres-Volume für dauerhafte Speicherung der Daten in dev-Umgebung.

Monitoring & Entwicklung
- Hot-reload für Frontend (Vite) und Backend (ts-node-dev / nodemon).

Abgrenzungen
- Keine Auth im MVP.
- Keine Produktions-Tuning-Maßnahmen wie Backups oder Replikation.

Empfehlung
- Start mit TypeScript in Backend und Frontend, aber TypeScript kann aus Zeitgründen weggelassen werden, wenn schnelle Iteration bevorzugt wird.
