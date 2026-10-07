# Stage 4 · Preview, whole voice, final cut

The local Mac makes these artifacts. After the user confirms the storyboard and 3p succeeds in [stage 3](stage-3.md), make each artifact and let the user review it before its gate. `run` waits by default; progress events are not approval. Use `--detach` only when the user wants to come back later.

```sh
bin/hnc run <期> 4v --json
bin/hnc episode show <期> 4v --json
```

Show the preview in the app with `bin/hnc open <期> 4v --json`. Ask for the user's explicit visual decision. Only after 4v is approved should you select the voice with the user and start 4s. `--voice` takes `providerId:voiceId` (for example, `openai-tts:alloy`), not a display name. The 4s detail's `voice` may contain an earlier selection; omitting `--voice` reuses that selection. If no selection exists, ask the user to choose an available voice in the app, then use its exact identifiers. Do not guess or silently choose the example voice. A paid step may need Mac consent and is subject to the user's settings and daily cap. `--fresh` asks for a new whole take rather than reuse and may spend again; never set it without the user's request.

```sh
bin/hnc run <期> 4s --voice <providerId:voiceId> --json
bin/hnc episode show <期> 4s --json
bin/hnc open <期> 4s --json
```

The user listens and decides at the 4s gate. Then make and inspect the final cut:

```sh
bin/hnc run <期> 4f --json
bin/hnc episode show <期> 4f --json
bin/hnc open <期> 4f --json
```

Only the user's explicit final-review decision can pass 4f. `step.lastGate`, `step.state`, and `production.onMac` tell you whether the review is ready and where the artifact lives; `production.version` is a workbench version number, not a local file path. Read [gates](gates.md) before recording a decision. Once approved, [export](export.md) can prepare local publication materials; publication itself remains the user's work.
