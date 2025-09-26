# CONTRIBUTING — Mini CRM

Goal: Consistent, testable, secure code. PRs will not be merged unless the rules are followed.

## 1) Architecture Layers
- UI → Application → Domain → Infrastructure (dependency direction downward).
- The UI must not import Infrastructure. Reach it through Application.
- Repository ports are defined in Domain/Application; implementations live in Infrastructure.
- Mutations use Server Actions; input validation uses Zod.

## 2) Boundaries & Import Rules
- Allowed: UI→Application, Application→Domain (+Ports), Infrastructure→Domain types.
- Forbidden: UI→Infrastructure, Infrastructure→UI.
- Use path aliases (e.g., `@/modules/...`); avoid deep relative paths.

## 3) Code Quality
- TypeScript strict mode (noImplicitAny, etc.) enabled.
- Functions have a single responsibility; split large functions.
- Side effects live only in Application/Infrastructure.

## 4) Tests
- **Unit (Vitest)**: Domain & Application are mandatory.
- **Integration**: Server Actions + test DB.
- **E2E (Playwright)**: core flow (login→dashboard→CRUD).
- Target: Domain/Application coverage ≥ **90%**, overall ≥ **85%**.
- Add a regression test for every bug fix.

## 5) Commit & PR
- Branches: `feat/*`, `fix/*`, `chore/*`, `docs/*`, `ci/*`.
- Conventional Commits: `feat(contacts): ...`, `fix(deals): ...`
- PRs must be small and focused (< ~400 lines changed).
- PR description: Purpose / Changes / Tests / Screenshot or recording.
- **main is protected**; merge only through PR.

## 6) CI Gates (required to merge)
- `pnpm lint` ✅
- `pnpm typecheck` ✅
- `pnpm test` ✅ (unit + integration if present)
- `pnpm build` ✅

## 7) Security
- Do not commit `.env*`; production/preview env lives in Vercel.
- Mask PII in logs.
- Validate all Server Action inputs with **Zod**.

## 8) Database
- Provide a descriptive migration for every schema change.
- Seed must be idempotent.
- Add release notes for breaking changes.

## 9) Versioning
- **SemVer** + **Conventional Commits**.
- Use **Changesets** for automated version PRs + git tags (once set up).

## 10) Definition of Done (every task)
- [ ] Unit/Integration tests added and green.
- [ ] Typecheck & Lint are green.
- [ ] Layer boundaries are respected.
- [ ] PR description is clear, includes verification steps/screenshots.
