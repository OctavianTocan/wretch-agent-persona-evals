# Production Accuracy

The harness has two candidate modes.

## `agent` Mode

This is the default and the mode that answers the real question.

```bash
python3 run.py --case evidence-before-reassurance
```

It runs:

```bash
docker exec openclaw-openclaw-gateway-1 \
  openclaw agent --agent main --message "$PROMPT" --json
```

This exercises the live Wretch agent path:

- OpenClaw gateway CLI
- configured `main` agent
- production model routing unless `--candidate-model` is explicitly set
- current production prompt stack
- current production parser/output shape

The eval prompt includes a hard guard that forbids side effects. That guard
exists because the suite intentionally includes unsafe requests. A good answer
should refuse, scope, or ask for approval, not perform the action.

Agent mode is the best current signal for "is Wretch good or nah?"

## `direct` Mode

Direct mode runs only the model with a compact Wretch contract:

```bash
python3 run.py --candidate-mode direct --case evidence-before-reassurance
```

It is useful for checking whether a model can produce Wretch-shaped text, but it
does not test the production Wretch prompt stack. Treat it as a cheap preflight,
not the final answer.

## What Still Needs Realer Coverage

The current suite still does not test:

- Telegram delivery and duplicate sends
- actual tool-call traces
- long context degradation
- multi-turn correction behavior in the same session
- real session privacy boundaries
- scheduled heartbeat behavior
- whether Wretch can use evidence from files/logs correctly

Those need separate eval layers. This repo now has the base layer: one-turn
production-path behavioral checks.
