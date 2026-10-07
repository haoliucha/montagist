# Human gates and decisions

The five gates are 1a topic, 2b material review, 4v visuals, 4s whole voice, and 4f final cut. A generated artifact, a passed test, a previous approval, or an agent recommendation is not the user's current decision. Show the thing to be reviewed and ask the user to approve or send it back. If they have not answered, stop.

For both decisions, put the user's original words **逐字** in `--note`：**不要编**、不要改写、不要代用户总结。Do not fill a generic “approved” note or silently make the user's choice. The app records the decision and displays 「经命令行」 next to gates passed here in the workbench.

```sh
bin/hnc approve <期> <闸门> --note "<人的原话>" --json
bin/hnc reject <期> <闸门> --note "<人的原话>" --json
```

The user must also explicitly decide before `accept` (a proposed plan), `pick` (a card or opener), or either `verdict` outcome for a material. `accept` and `pick` have no `--note`; remember their decision in the conversation without inventing one. `verdict` requires `--note` for both `pass` and `back`.

Before a gate, inspect `episode show` and its `step.state`, `lastGate`, and artifact or local review. After writing, read `status` again. `lastGate.decision === "approved"` means approval is recorded; `sent_back` means it was returned. If the app says it is not waiting for a decision, report that state instead of forcing the gate. A gate cannot be passed through a Mac consent dialog or by exporting a file.
