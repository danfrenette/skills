---
name: today
description:
  Assemble an ephemeral daily plan of to-dos, goals, and ready-to-paste starting prompts from Linear
  work, today's calendar, and recent agent sessions.
disable-model-invocation: true
---

# Today

Build a plan for the current local day. Where `/yesterday` looks back at what happened, today looks
forward at what to do next. Linear is required and is the source of truth for assigned issue work.
Google Calendar, Granola, Slack, and recent agent sessions are additional evidence sources.

## Planning Window

1. Read the machine's local date, weekday, and timezone.
2. The planning window is today from local midnight through 23:59:59. The session-mining window is
   the last 48 hours regardless of date.
3. State the date and timezone before gathering evidence.
4. Determine whether the current harness supports listing and reading past sessions. Load the
   harness's own skill or manual for session history (for example, the skill that documents the
   harness itself) and follow its mechanism. If the harness has no such mechanism, skip session
   mining and note it as an unavailable source.

## Gather Evidence

1. Identify the authenticated Linear user. Query every issue assigned to that user in an
   in-development status (for example In Progress or In Review). For each issue, review recent
   comments and updates for concrete next actions: requested review changes, unanswered questions,
   QA steps, merge or deploy follow-ups. Flag issues that appear stale, blocked, or finished but
   still sit in development.
2. If Google Calendar tools are connected, list today's events to establish the day's schedule.
   Meetings shape how much focus time the day actually has. If Granola MCP tools are also connected,
   read the notes of recent meetings that ended with commitments or action items assigned to the
   user.
3. If Slack MCP tools are connected, search the last few days for threads where someone asked the
   user for something that appears unanswered. Include only actionable asks; do not turn the plan
   into a message log.
4. If the harness supports session history (per the Planning Window step), mine recent sessions for
   open threads:
   - List sessions and keep those updated in the last 48 hours, across all projects. Exclude the
     current session.
   - For each candidate, read the tail of the conversation and judge from the last few messages
     whether the session ended with unfinished work: a task left mid-way, an open question never
     answered, or an explicit next step that never happened. Note the session's title, directory,
     and what it was doing when it stopped.
   - Skip sessions that clearly wrapped up.
5. Note each source that was unavailable or returned no evidence. Do not infer a task from missing
   data. The evidence is complete when every available source has either contributed relevant
   context or been accounted for.

## Brief And Interview

Present a compact factual brief before asking anything. Group it as: `Open threads` (recent
sessions, with titles), `Linear carryover` (identifiers, titles, next actions),
`Meeting commitments`, and `Slack asks`. Deduplicate items repeated across sources, and note how
much of the day is consumed by meetings.

If no source surfaced any open work, say so explicitly and ask what the user intends to work on
today.

Ask these questions every run:

1. What must be true at the end of today for it to feel like a good day?
2. What are you planning to do that these sources do not capture?
3. Is anything here deliberately deferred or dropped for today?

Then ask only questions needed to resolve ambiguity in the evidence. Useful examples include:

- `ENG-123` has review changes requested: is addressing them today's first task?
- The session "Auth refactor" stopped mid-migration: continue it today or leave it parked?
- You have four meetings: which to-dos are realistic in the remaining focus time?

Treat answers as the user's authoritative account. The interview is complete when every open thread
has been assigned to today, explicitly deferred, or explicitly dropped.

## Day Plan

Draft the plan in three parts:

1. **Goals**: one to three outcome statements, led by the user's answer to what makes today a good
   day.
2. **To-dos**: a prioritized list. Each item names its source (issue identifier, session title, or
   meeting) and gets a suggested starting prompt in its own fenced code block so the user can copy
   it cleanly to the clipboard. Prompts should be specific enough to paste into a fresh session and
   immediately orient the agent: state the goal, the relevant identifiers, and any constraints.
3. **Deferred**: items explicitly pushed to another day, listed in one line each so nothing silently
   disappears.

For to-dos that continue a past session, show the harness's resume mechanism (a command, or the
session picker in its interface) next to the session title, with the suggested prompt in its own
code block below it.

Keep the plan honest about capacity: if the evidence and meetings imply more work than fits the day,
cut items to fit and move the rest to `Deferred` rather than producing an impossible list.

Keep the result ephemeral: do not create, update, or store anything in Linear, Slack, Granola,
Google Calendar, past sessions, files, or memory.

End by asking whether the user wants the plan revised.
