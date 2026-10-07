# Export reviewed work

Export reads the currently available script or storyboard. It never grants approval. `--json` returns `{filename,text}` for text; without `--out`, the terminal form prints the text. To save to a new file, use `--out`; an existing file is not overwritten.

```sh
bin/hnc export <期> --script --json
bin/hnc export <期> --storyboard --json
```

After the user's 4s approval, `--srt` exports the subtitle file aligned with that approved whole voice. It is available on the Mac that holds that episode's material.

```sh
bin/hnc export <期> --srt --json
```

After the user's 4f approval, `--package` prepares the final MP4, its matching subtitles, script, storyboard, source credits, and an AI-label reminder in a local folder. The Mac asks the user before creating it. If they cancel or the folder already contains files, stop and explain; do not bypass the dialog or overwrite anything. An explicit destination can be passed with `--out`.

```sh
bin/hnc export <期> --package --out "<新目录>" --json
```

The package does not propose a title or cover, publish to a platform, or mark 5p/5r complete. The user handles those steps in the workbench. Check the result and tell the user where it was saved; never claim publication from a successful export.
