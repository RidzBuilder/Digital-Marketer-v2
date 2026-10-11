# Digital Marketer v2 — Minimal Runnable Skeleton Design

## Status
Proposed implementation design for SESI 2 / FASE 0. Strict free-tier only. Database selection is intentionally deferred.

## Goal
Create the smallest repository baseline that installs, runs, type-checks, tests, and builds. It must leave a clean path toward the later Brief → Generate → CCO → Approve → Publish Telegram workflow without implementing provider integrations prematurely.

## Decisions
- Framework: Next.js App Router + TypeScript.
- Package manager: pnpm.
- Runtime: Node.js LTS supported by the selected Next.js version.
- UI: minimal landing/status page; no authentication or database yet.
- Tests: Vitest for pure/unit-level checks; production build and TypeScript checking as verification gates.
- CI: GitHub Actions workflow for install, lint/typecheck, tests, and build on pushes and pull requests.
- Secrets: no secrets or API keys in source control; no external credentials required for this phase.
- Deployment: compatible with a free-tier deployment, but do not add deployment configuration that requires paid services.

## Minimal repository shape
- `app/layout.tsx`: root layout and metadata.
- `app/page.tsx`: minimal project status page.
- `src/lib/health.ts`: pure health/status helper with deterministic behavior.
- `src/lib/health.test.ts`: unit test for the helper.
- `package.json`, `pnpm-lock.yaml`, `tsconfig.json`, `next.config.ts`, `eslint.config.mjs`, `.gitignore`, `.npmrc`.
- `.github/workflows/ci.yml`: free GitHub Actions CI.
- `README.md`: local install/run/test commands and current scope.

## Acceptance criteria
1. `pnpm install --frozen-lockfile` succeeds.
2. `pnpm lint` succeeds.
3. `pnpm typecheck` succeeds.
4. `pnpm test` succeeds.
5. `pnpm build` succeeds.
6. The home page renders a clear Digital Marketer v2 status without requiring credentials or a database.
7. CI runs the same verification commands.
8. No secrets, paid-only dependency, database, auth provider, or publishing integration is introduced in this phase.

## Out of scope
Database/auth/RLS, LLM provider integrations, Telegram publishing, dashboard features, analytics, and multi-tenant data models. These will be added only when the corresponding phase requires them.

## [ASUMSI] requiring confirmation
- Next.js App Router + TypeScript and pnpm are acceptable defaults.
- A minimal status page is sufficient for this bootstrap phase.
- CI may run on GitHub Actions for a public repository, subject to current platform terms and usage limits.
