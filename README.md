# Careline — medical appointments and clinical history

Local TypeScript system using PostgreSQL 16, NestJS REST API and a React SPA.

## Run

```sh
docker compose up --build
```

- SPA: http://localhost:8080
- REST API: http://localhost:3000 (`/health`)
- PostgreSQL: localhost:5432

For local defaults, seed users use `Seed!Passw0rd`; set `SEED_PASSWORD` to override. Set database values in `.env` if needed (see `.env.example`). Database migrations run before seeding on backend startup. Migrations include reversible `*.down.sql` counterparts. Attachments are stored in a private named Docker volume.

OAuth is authorization-code with PKCE S256. The SPA stores short-lived tokens in sessionStorage, proactively refreshes before expiry, verifies the OAuth state on return, and revokes tokens on logout. API requests are authenticated with bearer access tokens.

## Tests

```sh
npm install
npm run test:unit
npx playwright install chromium
# with docker compose stack running:
npx playwright test
```

Authorization and booking-invariant unit tests are in `backend/src/security.test.ts`; browser smoke tests are in `tests/`.
