# Lighthouse API -- Architecture

## Overview

REST API for tracking lighthouse status, sensor readings, maintenance schedules, and alerts. Built for Nordic maritime authorities managing coastal infrastructure.

## Request Flow

```
HTTP Request
    |
    v
Express Router (api/routes/)
    |
    v
Middleware chain: auth -> validate -> log
    |
    v
Controller (api/controllers/)
    -- validates input with Zod
    -- calls service
    -- maps result to HTTP response
    |
    v
Service (api/services/)
    -- business logic
    -- database queries (parameterized SQL)
    -- throws typed errors
    |
    v
PostgreSQL
```

## Directory Structure

```
api/
  routes/
    lighthouse.routes.ts    # /api/v1/lighthouses
    reading.routes.ts       # /api/v1/readings
    maintenance.routes.ts   # /api/v1/maintenance
    alert.routes.ts         # /api/v1/alerts
  controllers/
    lighthouse.controller.ts
    reading.controller.ts
    maintenance.controller.ts
    alert.controller.ts
  services/
    lighthouse.service.ts
    reading.service.ts
    maintenance.service.ts
    alert.service.ts
  middleware/
    auth.ts                 # JWT verification
    validate.ts             # Zod schema validation
    error-handler.ts        # Global error -> HTTP status mapping
    request-logger.ts       # Structured request logging
  config.ts                 # Environment variables (never hardcode)
  app.ts                    # Express app setup
  server.ts                 # Entry point

shared/
  types/
    lighthouse.ts           # Lighthouse, LighthouseCreate, LighthouseUpdate
    reading.ts              # SensorReading, ReadingQuery
    maintenance.ts          # MaintenanceRecord, MaintenanceSchedule
    alert.ts                # Alert, AlertCondition, AlertSeverity
    api-response.ts         # ApiResponse<T> envelope
  errors.ts                 # NotFoundError, ValidationError, AuthError, ConflictError
  constants.ts              # Shared constants (alert thresholds, status enums)
  utils/
    pagination.ts           # Pagination helpers
    date.ts                 # Date formatting utilities

migrations/
  001_create_lighthouses.sql
  002_create_readings.sql
  003_create_maintenance.sql
  004_create_alerts.sql
  005_add_reading_indexes.sql

tests/
  services/                 # Unit tests (mocked DB)
  integration/              # Full request tests (test DB)
  fixtures/                 # Shared test data
  setup.ts                  # Test DB setup/teardown
```

## Database Schema

Four core tables:

- **lighthouses** -- id, name, latitude, longitude, status, commissioned_date, region
- **readings** -- id, lighthouse_id (FK), timestamp, light_intensity, battery_level, wind_speed, wave_height
- **maintenance** -- id, lighthouse_id (FK), scheduled_date, completed_date, type, notes, technician
- **alerts** -- id, lighthouse_id (FK), condition, severity, triggered_at, resolved_at, reading_id (FK)

Key indexes: `readings(lighthouse_id, timestamp)`, `alerts(lighthouse_id, resolved_at)`.

## Authentication

JWT-based. The `auth` middleware verifies tokens and attaches the user to `req.user`. Three roles:

- **viewer** -- read-only access to all endpoints
- **operator** -- can create readings and acknowledge alerts
- **admin** -- full access including lighthouse management and maintenance scheduling

Role checks happen in controllers, not middleware.

## Error Handling

All service errors extend a base `AppError` class in `shared/errors.ts`:

```typescript
class NotFoundError extends AppError { statusCode = 404 }
class ValidationError extends AppError { statusCode = 400 }
class AuthError extends AppError { statusCode = 401 }
class ConflictError extends AppError { statusCode = 409 }
```

The global `error-handler` middleware catches these and returns:

```json
{
  "data": null,
  "meta": null,
  "error": {
    "code": "NOT_FOUND",
    "message": "Lighthouse with id 42 not found"
  }
}
```

Untyped errors return 500 with a generic message. The original error is logged but never exposed to clients.

## API Response Envelope

All responses follow the same shape:

```typescript
interface ApiResponse<T> {
  data: T | null;
  meta: { page?: number; limit?: number; total?: number } | null;
  error: { code: string; message: string } | null;
}
```

Success responses have `data` populated and `error` as null. Error responses have `data` as null and `error` populated.
