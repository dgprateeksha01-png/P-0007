# Workspace

## Overview

pnpm workspace monorepo using TypeScript. Each package manages its own dependencies.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- `pnpm --filter @workspace/api-server run dev` — run API server locally

See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details.

## Artifacts

### Medicine Reminder (`artifacts/medicine-reminder`)
- React + Vite web app
- Preview path: `/`
- A personal medication tracker called MedTrack
- Teal/mint color theme

### API Server (`artifacts/api-server`)
- Express 5 backend
- Handles all medication, schedule, dose, and summary endpoints

## Database Schema

Tables:
- `medications` — stores medication name, dosage, unit, notes, color
- `schedules` — links medications to times of day and days of week
- `doses` — logs each dose as taken or skipped

## API Endpoints

- `GET/POST /api/medications` — list and create medications
- `GET/PUT/DELETE /api/medications/:id` — manage individual medications
- `GET/POST /api/schedules` — list and create schedules (filterable by medicationId)
- `DELETE /api/schedules/:id` — remove a schedule
- `GET/POST /api/doses` — list and log doses (filterable by medicationId, date)
- `DELETE /api/doses/:id` — remove a dose log
- `GET /api/summary/today` — today's summary stats
- `GET /api/summary/adherence` — 7/30 day adherence percentages + streak
- `GET /api/summary/upcoming` — today's upcoming doses with taken status
