# When a command stops

Read the final JSON envelope's `error.code`, `message`, and optional `hint`. A progress event is not the final result. Retry only after the cause is resolved, and read `status` before starting a paid or destructive action again.

| Exit / code | Next step |
|---|---|
| 1 `network`, `server`, `failed` | Check connection and `status`; if work might already have started, do not blindly repeat it. |
| 2 `usage` | Use `bin/mtg help <命令> --json` and correct the named argument. |
| 3 `app-unreachable`, `app-auth`, `path-too-long` | Open or update the Mac app, then run the locator's version and `whoami` checks. A local connection problem is not a reason to bypass the app. |
| 4 `not-signed-in`, `account-mismatch` | Ask the user to run `bin/mtg login --json` in their browser, or switch to the expected account. |
| 5 `not-found` | Verify the slug and signed-in account; another account's episode is intentionally hidden. |
| 6 `needs-key` | Tell the user which provider is missing from `needsKey`; they enter it in the app or workbench, never in chat or CLI flags. |
| 7 `declined` | Stop. The Mac question was declined, dismissed, or timed out. Wait for a new user request. |
| 8 `not-ready`, `busy`, `read-only` | Inspect `status` and `episode show`; complete the missing human review, wait for current work, or use a writable episode. |
| 8 `cap-reached` | Stop spending today; do not route around the daily cap. |
| 8 `needs-mac`, `not-on-this-mac` | Use the Mac that owns the material, or let it reconnect. Do not substitute another episode's files. |
| 9 `timeout` | The wait ended; read `status` before deciding whether to retry. |
| 10 `upgrade` | Update the app before continuing. |
| 130 interrupted | Only local waiting stopped. The app or cloud task may still run; check `status` later. |

When a step is `waiting-you`, show `agent.lastMessage`, `agent.pendingPlan`, or the review artifact and ask the user. If no decision is given, stop at that point. `waiting-mac` means the local machine must be available; repeated requests do not wake it.
