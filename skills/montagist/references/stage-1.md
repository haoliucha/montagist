# Stage 1 · Topic and facts

Start only after checking the account in [setup](setup.md). Ask for the user's topic or working title; do not invent one for them.

```sh
bin/mtg episode new "<标题>" --json
bin/mtg run <期> 1a --say "<用户想做什么>" --json
bin/mtg episode show <期> 1a --json
```

The new episode returns `data.slug`; use it in later commands. `run 1a` requires `--say`; use the user's topic request, not an invented brief. `run` waits by default. Read the final envelope and, for a waiting step, `data.step.state`, `data.artifact` and `data.agent.lastMessage`. Show the actual topic cards and their evidence to the user. Wait for their explicit choice, then `bin/mtg pick <期> 1a <编号> --json`. The topic gate still needs their explicit approval: pass their original words with `bin/mtg approve <期> 1a --note "<人的原话>" --json`, or use `reject` with their exact reason. Do not infer approval from `pick`.

Then start facts and inspect the ledger:

```sh
bin/mtg run <期> 1b --json
bin/mtg episode show <期> 1b --json
```

Read `agent.lastMessage` and `artifact`; report uncertainty and sources honestly. If the assistant pauses to ask the user, relay the question and wait for their answer. Use [gates](gates.md) for all gate decisions and [JSON contract](json.md) for progress events.
