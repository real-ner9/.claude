# Prisma 7 Notes

## Breaking Change: No `url` in schema datasource
Prisma 7 removed `url = env("DATABASE_URL")` from `schema.prisma`. Instead:

1. Schema only declares provider:
```prisma
datasource db {
  provider = "sqlite"
}
```

2. Connection config goes in `prisma.config.ts`:
```ts
import "dotenv/config";
import { defineConfig, env } from "prisma/config";

export default defineConfig({
  schema: "prisma/schema.prisma",
  migrations: { path: "prisma/migrations" },
  datasource: { url: env("DATABASE_URL") },
});
```

## Generator
- Use `prisma-client` (not `prisma-client-js`) for Prisma 7
- Output to custom dir: `output = "../src/generated/prisma"`
