# Anaphor tour integration

Use the Anaphor app and CLI for bundles, persistent storage, validation, and reading. Locate the
installed app or supplied checkout through project instructions; read its development guide and
current CLI help before running it. The app owns schema fields, supported media and limits, command
syntax, and workspace defaults. From an Anaphor checkout, discover the local operations with:

```bash
pnpm --filter @anaphor/demo tour local help
```

## Prepare and persist

1. Locate the persistent local workspace in the user's application data directory, or use the
   configured override. Keep tours and assets outside product repositories and disposable worktrees.
2. Find the existing tour by participating repository/PR association. Reuse its identity and
   expected revision for updates; preserve section anchors and evidence identifiers. Record
   dependency order for coordinated PRs.
3. Author against the current shared schema. Use logical asset IDs, accessible descriptions,
   captions, and actual provenance. Import media and receipts into managed storage; retained source
   patches and relevant untracked contents or hashes belong with their evidence.
4. Validate the prepared bundle using the CLI, then create or update it atomically. Resolve a
   revision conflict by loading and reconciling the current tour. An invalid or interrupted update
   must leave the previous readable revision available; retain inputs for recovery.

When a PR head changes, apply
[evidence applicability](../../anaphor-verify/references/evidence.md#evidence-applicability) to
receipts and captures. Keep required stale or unknown checks visible in the tour.

## Launch and inspect locally

Start the reader with the app's documented loopback launch command and explicit
`ANAPHOR_LOCAL_PREVIEW=1`. Pass the same `ANAPHOR_TOUR_WORKSPACE` override to the CLI and reader
when configured. Local preview requires no authentication, hosted services, or publication. Open the
Anaphor reader at the URL returned by the CLI.

For authored tour content, open the returned URL and check only that:

- The intended content loads. After an update, refresh and confirm the new revision; the running
  reader retains its selected revision until refreshed.
- Code links resolve to the intended pinned source.
- Referenced assets load, including images, recordings and receipts when present.

When reader behavior changes, follow the app's reader verification recipe for accessibility and
interaction checks. Content authoring uses only the loading checks above; no separate inspection
receipt is required. Product verification receipts retain their evidence requirements.

Keep the local app available for review. Include the app revision, executed launch commands, and
resume instructions in the handoff. Label its URL as local to this machine in every PR. One
coordinated tour can serve multiple PRs; link the section relevant to each one.

## Publish when requested

Use authenticated CLI publication of the same validated bundle and referenced assets. Preserve the
logical tour identity, expected hosted revision, operation key, and exact inputs until the outcome
is known. Retry an uncertain response using unchanged inputs and the same key; resolve conflicts
against the current hosted revision. Local review remains usable if hosting fails.

Inspect the authenticated hosted tour and media before returning it as a shared result. Hosted
content remains owner-only. In the hosted inspection receipt, distinguish hosted checks from local
loading checks and real-provider or deployed acceptance; one does not establish the others. Publish
only within the user's requested scope.
