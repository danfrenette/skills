# T3 Code

T3 Code exposes its threads through tools, across every provider it runs and every linked machine.

1. Call `t3_thread_list` with `allProjects: true`. Page with `cursor` until threads fall before the
   session window. Subagent threads are excluded by default.
2. For each thread updated inside the window, call `t3_thread_read` with `view: "messages"` and read
   the messages timestamped in the window.
3. If `t3_environment_links` lists linked machines, repeat both steps with each `environmentId`.

Use the thread `link` when the brief names a thread.
