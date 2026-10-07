---
name: montagist
description: "Use Montagist · 奇镜（好牛叉）to make documentary-grade explainer videos: create and advance an episode through research, footage, script, storyboard, preview, voice and final cut, then export with the user's decisions. Use when the user mentions Montagist, 奇镜, 好牛叉, hnc, or asks ‘帮我做一期视频’."
---

# Montagist · 奇镜

Work through the installed Mac app with this Skill's `bin/hnc` locator. Use `--json` on **every** command, including checks. The packaged tool can start the app in the background; if it cannot connect, ask the user to open the app. Login is shared with the tool.

## Start

1. Run `bin/hnc version --json`. The locator checks the app command before forwarding. If it cannot find one, use [setup](references/setup.md).
2. Run `bin/hnc whoami --json`. Check the signed-in account. If unsigned, ask the user to run `bin/hnc login --json` and confirm in their browser. Do not handle credentials or guess which account to use.
3. For an existing episode, run `bin/hnc status <期> --json` and read `next`, the relevant step `state`, and `waitingOn`. For a new episode, ask for its topic or title, then use [stage 1](references/stage-1.md).

## Human decisions

- The five gates are **1a, 2b, 4v, 4s, 4f**. Only approve or reject after the user explicitly says so. Put the user's original words **逐字** in `--note`: **不要编**、不要改写、不要代用户总结。If they have not decided, show the result to review, ask them, and stop at that gate. Read [gates](references/gates.md) before the first decision.
- `accept` (plan), `pick` (topic card or opener), and both outcomes of `verdict` (material) also represent the user's decisions. Do not run them until the user has explicitly chosen; `verdict --note` records their exact words. Do not treat an AI suggestion, a status change, or a previous choice as fresh permission.
- Spending on 4s when required, deleting an episode, and exporting a publication package prompt on the Mac. Tell the user to answer there. A cancellation or timeout is a decision to stop; never retry to bypass it. For exit codes 6, 7 and 8, follow [troubleshooting](references/troubleshooting.md).
- Stop at 5p and 5r. The user completes publication and registration in the workbench. Exporting a package does not publish or change those steps.

## Route

| Work | Inspect and act | Read |
|---|---|---|
| Prepare the app and account | `version`, `whoami`, `doctor`, `keys list` | [setup](references/setup.md) |
| Choose a topic and check facts | `episode new`, `run 1a`, `pick 1a`, `approve 1a`, `run 1b` | [stage 1](references/stage-1.md) |
| Plan and review captured material | `run 2a`, `accept 2a`, `run 2b`, `verdict`, `approve 2b` | [stage 2](references/stage-2.md) |
| Write the script and storyboard | `run 3a`, `pick 3a`, read with exact `run 3a --say`, `run 3b`, confirm with `run 3p` | [stage 3](references/stage-3.md) |
| Preview, voice and final cut | `run 4v`, `run 4s`, `run 4f`, the three review gates | [stage 4](references/stage-4.md) |
| Export reviewed work | `export` | [export](references/export.md) |

Use [JSON contract](references/json.md) to read responses and progress events. Use [troubleshooting](references/troubleshooting.md) when an action stops. Read only the reference for the current stage and its decision or error.
