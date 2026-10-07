# Set up the Mac app

Install the [Montagist Mac app](https://montagist.haoliucha.com/download) and sign in. The Skill's `bin/hnc` locates the app's command; it does not store a second login. The packaged command can start the app in the background. If it cannot connect, ask the user to open the app. Capture and production need the Mac that holds the episode's material.

```sh
bin/hnc version --json
bin/hnc whoami --json
bin/hnc doctor --json
bin/hnc keys list --json
```

Check `whoami.data.signedIn` and the account before touching an episode. If it is false, have the user run `bin/hnc login --json` and confirm the code in their browser. If `doctor` reports missing tools needed for this episode, run `bin/hnc tools install --json` and check the result. `keys list` reports status only. Set missing model, search or voice keys in the app or workbench; never request the key value in chat or pass it on the command line. `keys test` can incur a small voice charge and asks on the Mac.

For errors, read [troubleshooting](troubleshooting.md). For the stable response fields, read [JSON contract](json.md).
