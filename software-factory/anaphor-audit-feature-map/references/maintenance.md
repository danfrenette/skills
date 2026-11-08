# Maintain project verification

Use the audit procedure to keep one named project's verification guide, feature map, and owned
harness helpers current. This contract adds unattended inputs and publication to that procedure.

## Establish the run

Resolve the owning checkout, verification guide/map, runtime target, access/setup pointers, allowed
write paths, evidence location, and publication authorization from the invocation or project
instructions. Preserve unrelated local changes. Several candidate maps require selection; missing
inputs block unattended work with an actionable report. A missing map returns a bootstrap
dependency.

Limit corrections to the named verification documents and their owned helpers. Product regressions
retain their expected assertions and return to implementation with evidence. Project-record changes
outside that scope require a separately authorized reconciliation pass.

Execute the entire audit, including its source coverage, recent-change sweep, live driving,
recovery, and cleanup. Store concise run receipts in the named evidence location, separate from
durable recipes. Each receipt identifies tested contents, feature/entry-point results, corrections,
and blockers.

## Publish the outcome

- **Clean:** every mapped recipe has source coverage and a passing live result; no corrections are
  needed. Return the receipt without creating a branch or PR.
- **Changed:** every mapped recipe passes, and corrections have been re-driven. Review all changed
  documents and helper code; helper changes also need applicable repository checks and
  [Anaphor review](../../anaphor-review/SKILL.md), supplied with the intended correction, baseline,
  testing decisions, and receipts. Within publication authorization, push one scoped branch and open
  or update at most one draft PR linking the corrections, tested revision, and proof. Verify its
  final head and draft status. Readiness, merge, and deployment remain user decisions.
- **Blocked:** required coverage failed, was inaccessible, remains unrun, or proven corrections
  cannot be published within authorization. Keep useful corrections and evidence for continuation;
  publish no PR. Identify the cause, attempted recovery, remaining features, and needed action.

An unreachable route is blocked coverage, with its attempted action and missing prerequisite.
Product failures are named as defects, rather than access problems or documentation drift. A
complete audit report can contain those failures; it cannot satisfy the maintenance publication
gate.

Reuse an existing maintenance PR after interrupted publication. Track its identity in project-owned
continuation records and recheck its head before updating it; an existing receipt cannot certify new
contents. Keep run receipts out of the corrections commit.

**Done:** the result is clean, changed with a verified draft PR, or blocked with retained evidence
and a concrete continuation dependency. Every mapped feature has a reported source and live
disposition.

## Schedule through the project

The host scheduler owns cadence, retries, and overlap between invocations. Choose cadence from
observed churn and audit cost when scheduling is requested. Serialize runs that share a checkout,
target, or maintenance PR; serialize against delivery work using those same writable resources.

When using the separately installed `periodic-work`, resolve it through the host's skill catalog.
Put the maintenance invocation and the run inputs above in the project's selected `DAILY.md`,
`WEEKLY.md`, or `MONTHLY.md`, then include that project and cadence in its registry. The
instructions should name `anaphor-audit-feature-map` in maintenance mode and explicitly authorize
draft-PR publication if desired. Keep project-specific paths and access procedures there rather than
in this reusable skill.

Remain quiet for unchanged successful runs unless periodic status was requested. Notify on proven
corrections, product failures, blocked prerequisites, or required user action through the host's
notification mechanism. A schedule needs authorization of its own; running this skill creates none.
