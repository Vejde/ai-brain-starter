# Lighthouse API

REST API for managing lighthouse monitoring data. Tracks lighthouse status, sensor readings, maintenance schedules, and alert conditions across the Nordic coast.

## Tech Stack

- TypeScript (strict mode), Node.js 20, Express
- PostgreSQL 15 with node-pg (no ORM)
- Jest for testing, ESLint + Prettier for formatting
- Docker Compose for local development

## Key Directories

- `api/` -- Express app: routes, controllers, services, middleware
- `api/routes/` -- Route definitions, one file per resource
- `api/controllers/` -- Request/response handling, input validation
- `api/services/` -- Business logic, database queries
- `api/middleware/` -- Auth, error handling, request logging
- `shared/` -- Types, constants, and utilities shared across packages
- `migrations/` -- SQL migration files (sequential numbering)
- `tests/` -- Integration and unit tests mirroring api/ structure

## Verification Commands

```bash
npm test                  # Run all tests
npm run test:unit         # Unit tests only
npm run test:integration  # Integration tests (requires DB)
npm run build             # TypeScript compilation (strict mode)
npm run lint              # ESLint + Prettier check
npm run lint:fix          # Auto-fix lint issues
npm run migrate           # Run pending migrations
```

Always run `npm run build` and `npm test` before committing.

## Patterns

- **Naming**: camelCase for variables/functions, PascalCase for types/interfaces, snake_case for DB columns
- **Error handling**: All services throw typed errors from `shared/errors.ts`. Controllers catch and map to HTTP status codes. Never throw raw Error objects.
- **Database queries**: Parameterized queries only. All queries live in service files. No SQL in controllers.
- **Types**: Define request/response types in `shared/types/`. Use Zod schemas for runtime validation.
- **Tests**: Every service function needs a unit test. Every endpoint needs an integration test. Test file mirrors source path: `api/services/lighthouse.service.ts` -> `tests/services/lighthouse.service.test.ts`
- **API responses**: Consistent envelope: `{ data, meta, error }`. See `shared/types/api-response.ts`.

## Never

- Modify migration files after they've been applied. Create a new migration instead.
- Push directly to main. All changes go through pull requests.
- Store secrets in code. Use environment variables via `api/config.ts`.
- Use `any` type. If you need flexibility, use `unknown` with type guards.
- Write raw SQL without parameterization. Always use `$1, $2` placeholders.

## Agents

- **explorer** -- codebase exploration, tracing routes and models
- **code-reviewer** -- TypeScript review with security and performance focus

## Commands

- `/start` -- session start: git status, tests, establish context
- `/review` -- code review workflow
