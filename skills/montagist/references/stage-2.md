# Stage 2 · Capture and material review

The CLI counts capture as 2b: accepting the 2a plan finishes 2a; `run 2b` starts capture. Inspect the proposed plan and ask the user before accepting or replacing it.

```sh
bin/mtg run <期> 2a --json
bin/mtg episode show <期> 2a --json
bin/mtg accept <期> 2a --json
bin/mtg run <期> 2b --json
bin/mtg episode show <期> 2b --json
```

Read `step.state`, `waitingOn`, `agent.lastMessage`, `agent.pendingPlan`, and the proposed plan in `artifact`. `accept` is the user's decision, even though it has no `--note` option. Capture needs the material-holding Mac; if it says `waiting-mac`, see [troubleshooting](troubleshooting.md). When the app asks for capture consent, the user must decide on their Mac.

The 2b detail contains `materials[]` with `n`, `title`, `url`, `got`, `verdict`, and `note`. Show each obtained material and source. Only after the user explicitly passes or sends back a particular item, use `bin/mtg verdict <期> <素材号> pass --note "<人的原话>" --json` or `back` with their exact reason. Do not claim that an unseen or missing item passed.

Once capture is finished and the user has reviewed the material, the 2b gate still needs a separate explicit decision. Use [gates](gates.md); neither a passed item nor a completed capture approves the whole stage.
