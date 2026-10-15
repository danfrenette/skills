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

A PR head change requires reassessing evidence, including captures made before later edits. Keep
historical results and tested source states intact. Record an unaffected-delta assessment explicitly
or run a new check. Required stale or unknown checks remain visible and prevent a merge-ready claim.

## Launch and inspect locally

Use the app's documented local-only launch mode, explicitly enabled and bound to loopback, with the
same configured workspace as the CLI. Local preview requires no OAuth, device login, database,
secure-store entry, hosted media provider, or publication. Use the URL returned by the CLI; do not
substitute a standalone HTML or Markdown reader.

Inspect the delivered revision in a browser: the short business case, necessary terms, linear
code-led slices and concise annotations, navigation/anchors, pinned source and spec links, evidence
details, images and videos, accessible alternatives, and freshness warnings. Check both themes and
narrow reflow. Follow an annotation and expand source context: code must stay in its bounded window.
Verify icon controls have accessible names, image enlargement fits the window, and closing restores
focus. Explicitly refresh after an update and verify the expected new revision; a running reader
retains its selected revision until then. Confirm imported evidence remains usable independently of
implementation scratch. Record browser actions and observed results in a durable inspection receipt,
separately from application test receipts.

Keep the local app available for the owner's review and include the launch/resume instructions in
the handoff. Label its URL as local to this machine in every PR. One coordinated tour can serve
multiple PRs; test the section links relevant to each one.

## Publish when requested

Use authenticated CLI publication of the same validated bundle and referenced assets. Preserve the
logical tour identity, expected hosted revision, operation key, and exact inputs until the outcome
is known. Retry an uncertain response using unchanged inputs and the same key; resolve conflicts
against the current hosted revision. Local review remains usable if hosting fails.

Inspect the authenticated hosted tour and media before returning it as a shared result. Hosted
content remains owner-only. Separate local inspection, isolated hosted checks, and real-provider or
deployed acceptance in the receipt; one does not establish the others. Publish only within the
user's requested scope.
