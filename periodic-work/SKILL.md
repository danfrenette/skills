---
name: periodic-work
description:
  Run periodic project instructions from an editable registry, delegating each project's DAILY.md,
  WEEKLY.md, or MONTHLY.md to a separate subagent. Use for scheduled or manual daily, weekly, or
  monthly project work.
---

# Periodic Work

The coordinator reads a project registry, dispatches project instructions, and collects results.
Project Markdown files define the work: maintenance, ticket selection, a software factory, or
anything else the project needs. Continuity belongs to those instructions and the workflows they
invoke.

## 1. Select the cadence and registry

Require one cadence: `daily`, `weekly`, or `monthly`, case-insensitive. Read
[projects.yaml](projects.yaml) beside this skill unless the invocation supplies another registry
path. Resolve the default relative to this skill's directory, regardless of the current working
directory.

The registry has a `projects` list. Each entry has a `directory` and a `cadences` string containing
comma-separated values, for example:

```yaml
projects:
  - directory: ~/code/project-a
    cadences: daily, weekly
  - directory: ~/code/project-b
    cadences: daily, monthly
```

Validate the entire registry before dispatch: each entry must have a nonempty directory string and a
nonempty cadence string. Split cadences on commas, trim whitespace, lowercase, and deduplicate;
every value must be `daily`, `weekly`, or `monthly`. An empty `projects` list is valid and runs
nothing. Missing inputs, unreadable registries, or malformed configuration end the run with an
actionable error; unattended runs cannot wait for answers.

This step is complete when the cadence and every registry entry are valid.

## 2. Discover eligible projects

Select entries containing the requested cadence. Resolve directory names relative to `~/code`; also
accept `~/code/...` and absolute paths. Expand home paths, resolve symlinks, and deduplicate
canonical directories. Each target must be a directory strictly inside the resolved `~/code`
directory.

| Cadence   | File at the project root |
| --------- | ------------------------ |
| `daily`   | `DAILY.md`               |
| `weekly`  | `WEEKLY.md`              |
| `monthly` | `MONTHLY.md`             |

Read only the matching root file, completely. Classify unavailable or out-of-scope directories and
unreadable files as blocked; missing or whitespace-only files as skipped. Continue with eligible
projects. The registry is the project allowlist and the scheduler selects the cadence, so recursive
discovery and date-based inclusion of other cadences would broaden the run.

Before dispatch, compare directory ancestry and inspect instructions for explicit shared write
targets. Serialize overlapping directories or tasks that write the same resource, because subagents
share a filesystem. Independent projects can run concurrently.

This step is complete when every selected canonical directory is either eligible with its full
instructions captured, skipped, or blocked.

## 3. Dispatch one worker per project

Use the harness's subagent API, such as Codex `spawn_agent`. If delegation is unavailable, report
eligible projects as blocked. Queue work within the harness's concurrency limit, freeing capacity as
workers finish. The coordinator performs only discovery, dispatch, and reporting.

Start each worker with only its absolute project directory, instruction-file path and full contents,
requested cadence, current local date/timezone when available, and invocation constraints. Use a
fresh worker context when the harness supports it, so other projects' instructions do not influence
its task.

Include this worker contract:

> Use the specified project as your shell working directory and resolve relative task paths against
> it. Follow applicable AGENTS.md files. Execute the supplied periodic instructions within the
> invocation's authorization and available permissions, preserving existing local changes. Follow
> the project's referenced skills and workflows; project instructions determine ticket selection and
> continuity. Account for every requested action as completed, inapplicable with a reason, blocked,
> or failed. Finish independent authorized actions when another is blocked. Return outcomes, changed
> files or artifacts, checks performed, and required user actions. For a dry run, inspect and
> describe intended actions without mutations. Keep periodic dispatch with the coordinator rather
> than recursively invoking this skill.

This step is complete when every eligible project has a worker or a reported dispatch failure.

## 4. Collect outcomes

Wait for every dispatched worker and process queued projects as capacity becomes available. One
project's failure does not stop others. An interrupted worker or unavailable result is incomplete;
leave retries to the scheduler or user because work may already have produced side effects.

Report each selected project's status and outcome: completed only when all requested actions are
completed or explicitly inapplicable; otherwise blocked, failed, or incomplete with the remaining
actions identified. Include discovery skips and blockers. If no projects match, report that no work
ran. Honor scheduler notification preferences using its supported mechanism.

The run is complete when every selected project has a final disposition and every worker result has
been collected or explicitly marked incomplete.

## Scheduling

Install this skill in a harness with subagents and access to the listed projects. Edit the
neighboring registry to add, remove, or change project cadences. Use separate schedules with prompts
such as:

```text
Use $periodic-work with cadence daily.
```

Substitute `weekly` or `monthly` for other schedules. The scheduler controls recurrence, overlap
between invocations, and retries; each invocation runs its selected files once.
