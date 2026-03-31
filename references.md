# Frontend development references

Use these repo files as the first checkpoint when this skill is active.

## Core stack and bootstrap

- `package.json` — scripts, dependencies, devDependencies
- `vite.config.js` — aliases, dev server, proxy, plugins
- `src/main.js` — global plugins, global components, app bootstrap
- `src/axios.js` — request wrapper and interceptors
- `src/error.js` — global error plugin

## Router and state

- `src/router/index.js` — router bootstrap and dynamic route formatting
- `src/router/page/index.js` — page/static route definitions
- `src/router/views/index.js` — in-app route definitions
- `src/store/index.js` — Vuex store assembly
- `src/store/modules/user.js` — permissions and user state
- `src/store/modules/common.js` — shared UI state

## Feature conventions to mirror

- `src/views/aduit-management/contract-management/index.vue` — Avue CRUD list page + fullscreen dialog pattern
- `src/views/aduit-management/contract-management/form.vue` — form dialog body example
- `src/views/aduit-management/contract-management/form.js` — config-driven form fields example
- `src/api/aduit-management/contract-management.js` — matching API module pattern
- `src/views/aduit-management/components/edit-table.vue` — shared domain component style

## Shared components and styling

- `src/components/basic-container/main.vue`
- `src/components/basic-block/main.vue`
- `src/styles/`
- `src/css/reset.scss`

## Validation-related files

- `.eslintrc.js`
- `.prettierrc.json`
- `.husky/pre-commit`
- `vite/plugins/setup-eslint.js`
- `build.sh`

## Current repo constraints

- Primary stack is JavaScript + Vue 3, not TypeScript-first.
- Business pages heavily rely on Avue config objects and Element Plus dialogs.
- `npm run lint` is staged-file oriented via `lint-staged`, not a full-project lint command.
- No default unit/integration test framework is visible in `package.json`.
