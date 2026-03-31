---
name: frontend-development
description: Guide and implement frontend project setup, module creation, page/component development, API integration, mock support, and verification in this repository. Use this whenever the user asks to create or extend frontend features, scaffold pages/components/routes/store/api files, build CRUD forms, wire existing backend endpoints, add frontend validation, or explain how to start a new frontend module in the current Vue 3 + Vite + Element Plus + Avue stack, even if they only say “做个页面”, “新增模块”, “接接口”, “补测试”, or “搭前端项目”.
---

# Skill: Frontend development

## Purpose

Implement or guide frontend work in this repository while preserving the existing stack, directory structure, coding style, and validation habits.

## Repository context

This project is not a blank-slate frontend. It already has strong conventions:

- Framework: Vue 3 + Vite 2
- UI stack: Element Plus, Avue, `@saber/nf-design-base-elp`
- Routing: Vue Router 4 with dynamic menu formatting through `src/router/avue-router.js`
- State: Vuex modules under `src/store/modules`
- I18n: `src/lang`
- HTTP layer: centralized Axios wrapper in `src/axios.js`
- Main feature style: config-driven CRUD and forms with `avue-crud` / `avue-form`
- Common feature layout: `src/views/<domain>/<feature>/index.vue`, `form.vue`, `form.js`, optional `components/`
- API layout: `src/api/<domain>/<feature>.js`

## Use this skill when

Use this skill aggressively whenever the task is primarily frontend-facing, especially if the user wants to:

- create a new page, module, component, dialog, form, table, or CRUD flow
- extend an existing Vue feature under `src/views`
- add or modify API integration under `src/api`
- follow this repo's Avue + Element Plus patterns
- wire permissions, route entry points, or shared business components
- add mock-driven verification or explain how to validate frontend work
- plan a new frontend module or subproject while staying aligned with the current repository

## Do not use this skill for

- backend service creation or database/model changes
- auth or permission model redesign
- introducing a new framework, UI kit, or testing stack without user approval
- broad architecture migrations unrelated to the requested feature

## Inputs to gather first

Before coding, identify as many of these as possible from the repo and the user request:

- target business domain and feature path
- existing page or module to mirror
- relevant API endpoints and request/response fields
- whether the change is list page, detail page, form flow, approval flow, or shared component work
- permission points or button visibility rules
- whether mock mode or real backend should be used for validation

If a critical product decision is missing, ask the user targeted questions before implementation.

## Repo-specific conventions to preserve

### Mock-first development when backend is unavailable

This repository now has a project-level API interception mock for the audit-management domain.

- Mock definitions live in `mock/audit.js`
- Mock registration is wired through `src/mockProdServer.js`
- Mock enablement is controlled in `vite/plugins/setup-mock.js`
- Dev proxy switching is controlled in `vite.config.js`
- Use `npm run mock` to start the app in mock mode (`VITE_APP_ENV=mock`)

When the user explicitly asks for mock data, says the backend is unavailable, or asks to continue frontend development before backend delivery, prefer extending this existing interception-based mock instead of inventing a second mock mechanism.

Mock implementation rules:

1. Add or update handlers in `mock/audit.js` for the affected endpoints.
2. Match the real frontend-consumed response shape from `src/api/**` and the touched `src/views/**` files.
3. Reuse the existing success envelope style (`code`, `success`, `msg`, `data`) where the page expects it.
4. Keep mock data focused on the user flow being built; do not attempt a fake full backend unless required.
5. If the feature belongs outside audit-management, first verify whether it should extend this mock file or use the existing non-audit mock files under `mock/`.

### 1. File placement

- Put feature pages under `src/views/<domain>/<feature>/`
- Mirror backend wrappers under `src/api/<domain>/<feature>.js`
- Put reusable cross-feature components under `src/components/`
- Put domain-specific reusable pieces under that domain's local `components/`

### 2. Page structure

For business CRUD pages, prefer the existing pattern:

- `index.vue`: list/search/table/actions
- `form.vue`: create/edit/view/approve dialog body
- `form.js`: Avue form or table option configs
- optional local helpers/components when the page is too large

### 3. UI implementation style

- Prefer `script setup` and Composition API for feature pages when the surrounding module already uses it
- Mixed Options API exists in core shell/shared areas; follow the style of the touched file instead of rewriting it
- Reuse `avue-crud`, `avue-form`, Element Plus dialogs, and existing shared components before writing bespoke UI
- Use slots to customize Avue-rendered fields and table cells instead of bypassing the pattern prematurely

### 4. Routing and state

- Respect the router split in `src/router/page` and `src/router/views`
- Be aware that menu-driven dynamic routes are formatted through `Router.$avueRouter.formatRoutes(...)`
- Reuse Vuex modules and existing getters/actions instead of inventing parallel state patterns

### 5. Permissions and business controls

- Button and action visibility commonly depend on `store.state.user.permission.*`
- Approval, edit, delete, and export operations often have status-based visibility rules
- Preserve fullscreen dialog workflows where existing modules already use them

### 6. Imports and formatting

- Reuse aliases: `@`, `components`, `styles`, `utils`
- Follow current formatting: single quotes, semicolons, 2-space indentation, concise arrow functions where appropriate
- Do not add new dependencies unless they already exist in `package.json` or the user approved them

## Default workflow

### A. Existing-feature development

1. Inspect nearby files in the same domain and choose the closest implementation to mirror.
2. Confirm whether the work belongs in an existing feature folder or needs a new folder under `src/views/<domain>/`.
3. Add or update the matching API module in `src/api/...`.
4. Implement list, form, dialog, and slot customizations using Avue/Element Plus patterns already used nearby.
5. Reuse existing shared components, utilities, dict APIs, and permission guards.
6. Verify only the touched flow and avoid unrelated refactors.

### B. New module or page scaffold inside this repo

When the user asks to “create a project/module/page” in this repository, default to this checklist:

1. Determine the domain directory under `src/views/` and `src/api/`.
2. Create the minimum feature skeleton needed by the request.
3. Follow the repo's CRUD/form split if the page is business-data heavy.
4. Add route integration only where the current architecture expects it.
5. Keep naming consistent with sibling modules.
6. If the request implicitly needs backend support that does not exist, stop and surface that dependency.

### C. Entirely new frontend app creation

If the user truly wants a brand-new frontend app rather than a feature inside this repo:

1. First verify that a separate app is actually desired.
2. Inspect existing stack and ask whether the new app should still use Vue 3 + Vite + Element Plus style conventions.
3. Do not silently switch to React, Next.js, TypeScript-heavy scaffolds, or a new testing stack just because they are popular.
4. Prefer consistency with the current repository unless the user explicitly chooses otherwise.

## Testing and verification rules

Always discover available scripts before claiming completion.

In this repository, the currently visible checks are:

- `npm run build`
- `npm run build:prod`
- `npm run mock`
- `npm run dev`
- `npm run lint` only for staged files through `lint-staged`

Important repo reality:

- There is no dedicated automated unit-test framework visible by default.
- There is no separate typecheck script.
- Husky pre-commit exists, but repo-wide lint is not wired as a normal validation command.

So follow this verification policy:

1. Run the most relevant existing validation commands, usually `npm run build`.
2. If the feature depends on mock data, use `npm run mock` when practical.
3. If automated tests already exist in the touched area, update and run them.
4. If no test framework exists, do not introduce Jest/Vitest/Cypress/Playwright unless the user asks for that setup.
5. When automated tests are absent, provide a short manual verification checklist covering:
   - happy path
   - empty/loading/error states when relevant
   - permission-gated actions
   - create/edit/view/approve transitions when relevant

## Safety and escalation

Stop and ask the user before continuing if:

- the feature requires backend contract changes
- a new dependency or framework is needed but not already installed
- the request conflicts with existing router, permission, or data-flow architecture
- the requested validation requires infrastructure not present in the repo

## Completion standard

When using this skill, finish with a concise summary that includes:

- files changed
- user-visible behavior delivered
- validation commands run and their results
- any assumptions, blockers, or follow-up decisions still needed
