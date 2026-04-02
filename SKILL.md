---
name: frontend-development
description: "Guide and implement frontend work in a repository-agnostic way: analyze the existing frontend stack, extend pages/components/routes/state/api layers, add validation, add or adapt mock support, and verify changes without assuming a specific framework or folder layout. Use this whenever the user asks for frontend feature work, page/module scaffolding, API wiring, UI behavior changes, frontend validation, or mock-assisted development in the current repository."
---

# Skill: Frontend development

## Purpose

Implement or guide frontend work while first learning the target repository's actual stack, structure, patterns, and validation workflow instead of assuming a specific framework or architecture.

## Use this skill when

Use this skill whenever the task is primarily frontend-facing, especially if the user wants to:

- create or extend a page, module, component, dialog, form, table, or CRUD flow
- wire frontend code to backend APIs
- add client-side validation or interaction logic
- scaffold frontend files in an existing application
- continue frontend work while backend delivery is incomplete
- add or extend mock support for frontend verification

## Do not use this skill for

- backend service creation or database/model design
- infrastructure, deployment, or DevOps work unrelated to frontend behavior
- introducing a new framework or major architecture migration without user approval

## First-step workflow

Before coding, always inspect the repository and determine:

1. framework and build tool
2. routing approach
3. state management approach
4. HTTP/request layer
5. UI/component library and styling approach
6. page/module/file organization
7. existing validation, lint, typecheck, test, and build commands
8. whether the request should use real backend APIs or mock data

If requirements are ambiguous, ask focused questions before implementation.

## Core implementation principles

### 0. Promote project-specific frontend skills when useful

When repository analysis reveals stable, repeatable frontend conventions, treat part of the job as extracting those conventions into a project-level skill.

Typical signals include:

- a clearly repeated page/module structure
- a stable request/API layer pattern
- consistent routing/state/permission conventions
- an established mock strategy
- repeated validation/build workflows
- domain-specific CRUD or form patterns that would otherwise need to be re-explained

When these signals exist, the skill should:

1. summarize the repository-specific frontend conventions
2. propose or generate a project skill that captures them
3. keep the generic guidance in this skill repository-agnostic
4. move concrete paths, commands, mock files, domain rules, and framework-specific conventions into the project skill

The generated project skill should usually contain:

- when it should trigger
- repository stack and architecture direction
- module/file placement direction
- request/state/routing/permission rules
- mock strategy and where to extend it
- project-specific validation entry points
- guardrails about what not to change

Project skills should prefer compact direction-setting guidance over static detail dumps. They should answer "what areas matter here" and "where to look first", while leaving exact file inspection to the concrete task.

Generation quality rules for project skills:

- use repository-native language and business nouns instead of generic placeholders when the domain is clear
- prefer trigger conditions based on repository/domain identity, not on the current task accidentally touching certain folders
- capture the 3-6 most distinctive implementation traits of the repo, not an exhaustive list
- include high-signal architectural behaviors when they are central, such as dynamic menu routing, permission-gated actions, fullscreen dialog workflows, or mock-mode entry points
- prefer describing the first implementation reference strategy (for example: mirror the nearest existing feature) over listing many concrete files
- keep sections compact and non-overlapping; project skills should feel like implementation direction, not repository summary
- avoid repeating the same idea across purpose, use-cases, and workflow sections
- if a generated project skill reads like a static reference sheet or a broad repository summary, compress it further

### 1. Follow the existing codebase

- Mirror nearby modules before inventing new patterns.
- Match the surrounding file structure, naming, imports, and coding style.
- Reuse existing shared components, utilities, hooks/composables, stores, and API wrappers before creating new ones.

### 2. Keep frontend layers aligned

When implementing a feature, check whether the work belongs in:

- route/page layer
- reusable component layer
- API/request layer
- state/store layer
- validation or data-mapping helpers

Only touch the layers needed for the requested behavior.

### 3. Prefer minimal, coherent changes

- Avoid unrelated refactors.
- Keep feature additions incremental.
- Preserve current user flows and permissions.
- Do not silently replace the project's established patterns.

### 4. Mock support

If the user explicitly asks for mock data, the backend is unavailable, or frontend work must proceed ahead of backend delivery:

- inspect whether the repository already has a mock mechanism
- extend the existing mock mechanism instead of adding a second one
- match the exact response shape consumed by the frontend
- keep mock data focused on the user flow being built
- verify the feature in mock mode if such a mode exists

### 5. Validation and verification

Before completion, discover and run the most relevant existing project checks, such as:

- build
- lint
- typecheck
- unit/integration tests
- mock/dev startup when needed for verification

If the repository lacks some of these checks, say so explicitly and provide a short manual verification checklist.

## Safety and escalation

Pause and confirm with the user if:

- the requested frontend change requires backend contract changes
- a new dependency is needed but not already present
- the existing architecture strongly conflicts with the request
- there are multiple valid implementation directions with product trade-offs

## Completion standard

Finish with a concise summary that includes:

- files changed
- user-visible behavior delivered
- validation commands run and results
- assumptions or follow-up decisions still needed

