# Security and Privacy

This repo is designed to be public-safe.

It should not contain:

- OpenClaw source
- OpenClaw runtime state
- API keys or tokens
- Telegram chat IDs
- private sessions
- raw reports with verbose provider payloads
- agent memory files

Generated reports are ignored by git. If a report is worth keeping, copy only a
small sanitized excerpt into `examples/` or `docs/`.

Before publishing changes, run:

```bash
git status --short
git diff --cached --stat
python3 -m py_compile run.py
python3 run.py --dry-run
```

For live confidence, also run at least one production-path smoke:

```bash
python3 run.py --case evidence-before-reassurance
```
