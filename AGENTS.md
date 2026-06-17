# Agent Instructions for TanPress

## Project Overview

TanStack Start monorepo with shadcn/ui. pnpm workspaces + Turborepo.

## Commands (run from repo root)

| Task | Command |
|------|---------|
| Install | `pnpm install` |
| Dev server | `pnpm dev` (port 3000) |
| Build all | `pnpm build` |
| Lint all | `pnpm lint` |
| Typecheck all | `pnpm typecheck` |
| Format all | `pnpm format` |

Per-package (from `apps/web` or `packages/ui`):
- `pnpm lint` — ESLint with @tanstack/eslint-config
- `pnpm typecheck` — `tsc --noEmit`
- `pnpm format` — Prettier

## Architecture

```
apps/web/         → TanStack Start app (React 19, Vite 8, Tailwind 4)
packages/ui/      → Shared UI components (shadcn, Radix, CVA)
```

- **Routing**: TanStack Router with file-based routes in `apps/web/src/routes/`
- **Route tree**: Auto-generated at `apps/web/src/routeTree.gen.ts` — do not edit manually
- **UI components**: Live in `packages/ui/src/components/`
- **Styling**: Tailwind v4 with CSS variables in `packages/ui/src/styles/globals.css`

## Adding shadcn Components

```bash
pnpm dlx shadcn@latest add button -c apps/web
```

Components install to `packages/ui/src/components/`.

## Import Aliases

- `@/*` → `apps/web/src/*`
- `@workspace/ui/*` → `packages/ui/src/*`

## Code Style

- Prettier: no semicolons, double quotes, trailing commas (es5), 80 char width
- Tailwind classes sorted by `prettier-plugin-tailwindcss`
- TypeScript strict mode in both packages
- ESLint ignores `import/no-cycle`, `import/order`, `sort-imports`

## Gotchas

- `routeTree.gen.ts` is auto-generated — never hand-edit
- UI package exports are defined in `packages/ui/package.json` `exports` field
- Tailwind scans `apps/**` and `packages/ui/**` via `@source` in globals.css
