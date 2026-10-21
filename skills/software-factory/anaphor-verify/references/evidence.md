# Evidence and blockers

## Evidence record

Use a short Markdown table or the project's existing report format. For each criterion record:

| Field     | Required content                                                      |
| --------- | --------------------------------------------------------------------- |
| Criterion | Spec identifier and the outcome being proved                          |
| Target    | Repository, revision, running surface, and relevant role/data context |
| Action    | Actual command or user steps executed                                 |
| Expected  | Outcome from the accepted requirement                                 |
| Observed  | Result actually seen, including persisted effects                     |
| Evidence  | Durable artifact or captured output location                          |
| Status    | Pass, fail, blocked, or not run                                       |

For committed work, record commit SHAs. For uncommitted work, also retain a patch and the relevant
untracked source contents or content hashes; HEAD alone identifies neither. Keep secrets and session
state out of artifacts. Link existing evidence rather than copying its narrative into multiple
documents.

Record what was run, not what a script name suggests. Screenshots illustrate a state; pair them with
the action and assertions supporting the claim. Mocks and test modes require disclosed coverage
limits at the substituted boundary.

## Evidence applicability

A new source state makes prior evidence stale until assessed. Inspect the delta for each affected
check: rerun it, or record why its original result still applies. Preserve the original tested
revision, date, and result; a rerun creates a new record. Tour revisions and tested source revisions
are separate facts. Required stale or unknown evidence prevents a merge-ready claim.

Integrated changes require integration evidence. Documentation-only follow-up may retain prior
application evidence with an inspected-delta rationale. Executable, configuration, or recipe changes
return to affected review and verification.

## Triage a failed attempt

1. **Product failure:** the target and harness work, but the observed outcome violates the accepted
   requirement. Mark fail and return the defect to implementation. Keep the expectation intact.
2. **Recipe drift:** working behavior is unreachable through an outdated selector or instruction.
   Repair against source and observed controls, without weakening the assertion. Retry the affected
   recipe once.
3. **Prerequisite failure:** required target, access, data, service, or tool is unavailable. Use one
   relevant, safe recovery from the documented procedure, then retry the failed check once. Examples
   include restarting an owned process or resetting owned test data. Infrastructure creation or
   credential provisioning belongs to the setup owner.
4. **Still unavailable:** mark blocked and stop the factory run. Report the failed prerequisite,
   attempted recovery, affected criteria, retained evidence, and the input or repair needed. Do not
   create a draft PR while required checks remain blocked or not run.

The recovery allowance belongs to the underlying failed prerequisite; relabelling it or starting
another agent does not reset it. If a retry reaches the app and reveals a product defect, classify
that result as fail rather than blocked.

An inaccessible mapped feature is a coverage limit, not a functional pass. When the user resolves
the prerequisite, rerun doctor and the missing checks before resuming delivery.
