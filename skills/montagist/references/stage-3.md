# Stage 3 · Script and storyboard

Ask the assistant to draft openers, show the options to the user, and wait for their explicit choice. `pick` is a human choice even though this command has no `--note` option.

```sh
bin/mtg run <期> 3a --json
bin/mtg episode show <期> 3a --json
bin/mtg pick <期> 3a <编号> --json
bin/mtg run <期> 3a --json
bin/mtg episode show <期> 3a --json
bin/mtg run <期> 3a --say "稿子定了，读一遍。" --json
bin/mtg episode show <期> 3a --json
bin/mtg run <期> 3b --json
bin/mtg episode show <期> 3b --json
bin/mtg run <期> 3p --json
```

Read `data.artifact` for the current opener, script, and shots; `data.agent.lastMessage` may ask a question or explain what changed. An agent step can stop at `waiting-you` without being complete. Show the question or candidate text and wait for the user's instruction before continuing. Do not send a fabricated answer. After the full script is ready, show it to the user. Only when they confirm it, send the **exact** reading sentence `稿子定了，读一遍。` with `run 3a --say`; wait for the assistant's reply and check that 3a is `done` before running 3b. A different sentence does not mark the script as read. Show the storyboard to the user; when they confirm the visual match, run 3p. Its successful preflight records the match and allows production to start. `accept` applies only to an actual `agent.pendingPlan` that the user has explicitly approved; it is not the script-reading or storyboard-confirmation command. A newer 2a plan may reopen earlier work; recheck `status` if the storyboard is locked.

You can show an exact text export with `bin/mtg export <期> --script --json` or `--storyboard`; [export](export.md) explains the output. After 3p succeeds, continue with the preview in [stage 4](stage-4.md).
