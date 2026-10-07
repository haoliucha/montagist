# Stable CLI JSON (hnc 1)

Always pass `--json`. Success has `{"hnc":1,"ok":true,"command":"…","data":…}`; failure has `{"hnc":1,"ok":false,"command":"…","error":{"code":"…","message":"…","exit":N}}`. Optional error fields include `hint`, `needsKey`, and `needsConsent.kind`. Check `ok`; do not infer success from text or a progress event.

While waiting, each earlier line may be an event: `{"hnc":1,"event":"progress","step":"4s","state":"running","text":"…","at":"…"}` or a `note` with `text` and `at`. The final line is the success or failure envelope. Ctrl-C ends local waiting with 130; it does not stop the cloud work.

`status` returns episode `id`, `slug`, `title`, `sample`, `mac`, `steps[]`, and `next`. A step has `id`, `name`, `gate`, `state`, `waitingOn`, `progress`, `failure`, `lastGate`. States: `locked`, `ready`, `queued`, `running`, `waiting-you`, `waiting-mac`, `done`, `sent-back`, `failed`. `lastGate` is null or `{decision,note,via,at}`; `via=cli` displays as 「经命令行」 in the workbench. `next` is null or `{step,who,hint}`.

`status` may also include `videoLanguage: "zh" | "en"`, the language saved on this episode. It is independent of the interface language preference. This is an optional addition within v1: older responses without it remain valid, and clients treat an absent value as `"zh"`. Existing v1 fields and the version number are unchanged. For `run` on 1b, 2a, 3a, and 3b without `--say`, the system opening message follows this saved language. A consent retry sends the same opening message. User-provided `--say` text is sent verbatim; 1a still requires `--say`.

`episode show <期> <步>` adds `episode`, `step`, `artifact`, `agent`, `materials`, `production`, and `voice`. `agent` has `lastMessage`, `pendingPlan`, and `needsConsent`; each material has `n`, `id`, `title`, `url`, `got`, `verdict`, `note`; `production` has a numeric workbench `version` and `onMac`. `artifact` and `voice` vary by step. Never turn the numeric workbench version into a local file path.

| Exit | Error codes | Action |
|---:|---|---|
| 0 | success | Read the final envelope. |
| 1 | `failed`, `network`, `server` | Read the message; check status before retrying. |
| 2 | `usage` | Correct the command or flags. |
| 3 | `app-unreachable`, `app-auth`, `path-too-long` | Check app and local connection. |
| 4 | `not-signed-in`, `account-mismatch` | Sign in or check the expected account. |
| 5 | `not-found` | Verify the episode name under the current account. |
| 6 | `needs-key` | Add the required key in the app or workbench. |
| 7 | `declined` | Stop; the user declined or did not answer on the Mac. |
| 8 | `not-ready`, `busy`, `cap-reached`, `needs-mac`, `not-on-this-mac`, `read-only` | Inspect the specific message and current status. |
| 9 | `timeout` | Check status; the work may still continue. |
| 10 | `upgrade` | Update the app. |
| 130 | user interruption, no `CliErrorCode` | Local wait ended; check status later. |

See [troubleshooting](troubleshooting.md) for what to do next.
