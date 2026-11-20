# Linear

Prefer Linear MCP tools. With only the CLI, discover commands through `linear issue list --help`.

1. Identify the authenticated Linear user.
2. Find issues assigned to that user with activity in the reporting window. For each issue, gather
   its identifier, title, status transitions, and every issue comment posted in the window,
   including comments by other people.
3. Query every issue assigned to the user in an in-development status (for example In Progress or In
   Review), regardless of recent activity. Review each issue's recent comments and updates to check
   that the status still looks accurate, and to surface activity that the movement-based query
   missed. Flag issues that appear stale or finished but still sit in development.

Done when every assigned issue with window activity and every in-development issue has its status
movement and window comments recorded.
