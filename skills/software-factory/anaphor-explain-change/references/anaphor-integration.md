# Anaphor tour integration

Use the Anaphor app and CLI for bundles, persistent storage, validation, and reading. Locate the
installed app or supplied checkout through project instructions; read its development guide and
current CLI help before running it. The app owns schema fields, supported media and limits, command
syntax, and workspace defaults. From an Anaphor checkout, discover the local operations with:

```bash
pnpm --filter @anaphor/demo tour local help
```

The local workspace override is `ANAPHOR_TOUR_WORKSPACE`; pass the same workspace to the CLI and
reader process. Start the reader with the app's documented loopback launch command and explicit
`ANAPHOR_LOCAL_PREVIEW=1`. Record the app revision and executed commands with the receipt.

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

Use the app's documented local-only launch mode, explicitly enabled and bound to loopback, with the
same configured workspace as the CLI. Local preview requires no OAuth, device login, database,
secure-store entry, hosted media provider, or publication. Use the URL returned by the CLI; do not
substitute a standalone HTML or Markdown reader.

For authored tour content, open the returned URL and check only that:

- The intended content loads, including the selected revision after an update.
- Code links resolve to the intended pinned source.
- Referenced assets load, including images, recordings and receipts when present.

Accessibility checks belong to changes to the tour reader itself. Follow the app's reader
verification recipe when changing reader behavior; authoring a local tour does not require theme,
responsive, keyboard/focus, accessible-name, scrolling or enlargement checks. A separate inspection
receipt is not required for these local content checks.

Keep the local app available for the owner's review and include the launch/resume instructions in
the handoff. Label its URL as local to this machine in every PR. One coordinated tour can serve
multiple PRs; link the section relevant to each one.

## Publish when requested

Use authenticated CLI publication of the same validated bundle and referenced assets. Preserve the
logical tour identity, expected hosted revision, operation key, and exact inputs until the outcome
is known. Retry an uncertain response using unchanged inputs and the same key; resolve conflicts
against the current hosted revision. Local review remains usable if hosting fails.

Inspect the authenticated hosted tour and media before returning it as a shared result. Hosted
content remains owner-only. Separate local inspection, isolated hosted checks, and real-provider or
deployed acceptance in the receipt; one does not establish the others. Publish only within the
user's requested scope.
