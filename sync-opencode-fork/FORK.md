# OpenCode Fork Intent

`dan-dev` carries a focused web permission-review patch stack over upstream OpenCode. Preserve current upstream architecture and reapply the behavior, not obsolete implementation details.

## Live Web Workflow

- `dev:web:live` runs only local Vite on port 4444 against an already-running backend, defaulting to port 4096.
- The backend remains the sole database and server-process owner. The launcher never starts, stops, restarts, or replaces it.
- HTTP, SSE, and WebSocket traffic use the same-origin Vite proxy and the backend's native Basic authentication challenge.
- `OPENCODE_DEV_SERVER_URL` selects another existing HTTP origin without exposing credentials through Vite variables or repository files.
- Server-owned sessions and permissions are shared; browser-local tabs, drafts, preferences, and storage are not.

Primary surfaces: `packages/app/script/dev-web-live.ts`, `packages/app/vite.config.ts`, launcher/proxy tests, and `CONTRIBUTING.md`.

## Permission Decisions

- Web permissions use one request-keyed staged controller for Allow once, conditional Allow always confirmation, and Deny with optional corrective feedback.
- Replies are authoritative, not optimistic. Controls remain visible and disabled in flight; failed replies preserve state for retry.
- Child-session requests identify their source while decisions remain routed through the parent session.
- Core propagates corrective permission feedback to the model.

## Pending Edit Review

- Valid canonical edit metadata renders Pierre-based inline diffs with bounded large previews and multi-file selection.
- Malformed or absent preview metadata warns without blocking permission decisions.
- Pending diffs can temporarily occupy existing V2 desktop and mobile review surfaces without mutating persisted Git, branch, or last-turn review state.
- Compact and expanded views share file selection, decision stage, feedback, and responding state through the same controller and reply path.
- Pending review disables normal line comments and restores the exact prior review state after authoritative resolution, replacement, or navigation.

Primary surfaces: `packages/app/src/pages/session/composer`, `packages/app/src/pages/session.tsx`, shared session review components, and `packages/app/e2e/regression/session-request-docks.spec.ts`.

## Current Patch Stack

Derive the authoritative patch list on every run with:

```bash
git log --reverse --oneline <selected-base>..dan-dev
```

The completed feature lineage is Linear END-185 through END-189 and fork PRs through `danfrenette/opencode#5`. Use those records for intent when a conflict cannot be understood from code and tests alone.
