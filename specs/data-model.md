# Data Model

Datenmodell für Tasks (Postgres)

Prisma Schema (Beispiel)

generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model Task {
  id         Int      @id @default(autoincrement())
  title      String
  description String?
  completed  Boolean  @default(false)
  createdAt  DateTime @default(now())
  updatedAt  DateTime @updatedAt
}

Hinweis: Alternativ kann id als UUID verwendet werden, mit @id @default(uuid()).
