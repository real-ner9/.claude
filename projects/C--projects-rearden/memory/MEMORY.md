# Rearden Project Memory

## Architecture
- Turborepo monorepo: `apps/web` (Vite+React), `apps/api` (Hono), `packages/types`, `packages/tsconfig`
- Scope: `@rearden/*`
- Ports: web=3000, api=3001

## Database
- **PostgreSQL 17** via Docker (`pgvector/pgvector:pg17`), container `rearden-db`, port **5434** (mapped from 5432, since 5432 is used by another project)
- **Prisma 7** with `@prisma/adapter-pg` driver adapter
- Connection: `postgresql://rearden:rearden@localhost:5434/rearden?schema=public`
- Models: Candidate, Recruiter, Post, Vacancy, Conversation, ChatMessage
- Seed script: `apps/api/prisma/seed.ts` (run via `npm run db:seed`)
- Prisma client singleton: `apps/api/src/lib/db.ts`

## Key Gotchas
- **Prisma 7**: `datasource.url` removed from schema.prisma — must use `prisma.config.ts` with `defineConfig()` from `prisma/config`. See [prisma-notes.md](prisma-notes.md).
- **Prisma 7 client**: requires `@prisma/adapter-pg` — `new PrismaClient({ adapter: new PrismaPg({ connectionString }) })`
- **Types package**: exports raw `.ts` source (no build step), uses `"exports": { ".": "./src/index.ts" }`
- **Motion v12**: import from `"motion/react"`, not `"framer-motion"`
- **Windows shell**: Never use `sed` for SCSS variable replacements — `$var` gets interpreted. Use Node.js scripts or the Edit tool instead.
- **Docker port conflict**: Port 5432 is used by another project's DB container, Rearden uses 5434.
