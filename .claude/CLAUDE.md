# ghost-editor: instructions for Claude Code

ghost-editor is a Claude Code skill that turns a raw talking-head phone recording
into a vertical 1080x1920 reel. Read `SKILL.md` for the pipeline and `docs/PLAYBOOK.md`
for named styles before changing anything in the pipeline.

## Working rules

- The creative choices (takes, hook, beats) are made by the agent with the user.
  Scripts do the mechanical work. Do not hardcode choices for one reel into a shared script.
- Never commit media: video, audio, images or rendered output. `.gitignore` already
  covers `library/` media. Check `git status` before every commit.
- Never commit secrets, API keys or `.env` files. `library/me/` holds face embeddings and stays local.
- Before a reel's final render, wait for the user's approval of the preview. Do not skip the approval step.
- Keep scripts idempotent. Re-running a step must not corrupt `reel.json` or `build/`.

## Tests

Run the existing tests before a commit that touches `scripts/`:

```bash
python3 -m pytest tests -q
```

If a test needs media that is not in the repo, report it as skipped. Do not delete the test.

## Git

- Work on a feature branch, never directly on `main`.
- Commit messages use Conventional Commits (`feat:`, `fix:`, `docs:`, `chore:`).
- Open pull requests as drafts.
