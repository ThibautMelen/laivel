# laivel

A lead-tech tool that places each developer on the official AIDD grid.

Built for [LAIVEL UP](https://github.com/ai-driven-dev/laivel-up) · 28-31 August 2026.

One Nika workflow. No other runtime. OpenAI extracts facts. `jq` applies
the law *all axes or nothing*. `nika:decide` says whether to publish or
abstain. The model never writes the level.

## Run it

```bash
brew install supernovae-st/tap/nika   # https://nika.sh
export OPENAI_API_KEY=...             # openai/gpt-5-mini
nika run laivel.nika.yaml --max-cost-usd 3
```

Official profiles (Friday): drop them in `profiles/` then

```bash
nika run laivel.nika.yaml --var profiles=./profiles/*.md --max-cost-usd 3
```

Self-test (structured fixtures):

```bash
nika run laivel.nika.yaml --var self_test=true --max-cost-usd 1
```

Held-out e2e (prose only, like Friday):

```bash
nika run laivel.nika.yaml \
  --var profiles=./held/*.md \
  --var expected=./held/expected.json \
  --var self_test=true \
  --max-cost-usd 1
```

Zero-key rehearsal: `--model mock/echo`.

Outputs: `out/verdicts/*.md` · `out/team.md` · `out/team.json` · `out/team.svg`.

Run from a **standalone clone**. If another `nika.yaml` sits above this
folder (a monorepo), `nika` will load that file first and refuse.

## How it works

See [METHOD.md](./METHOD.md). Official grid (vendored):
[levels/aidd.md](./levels/aidd.md).

```
glob → read → infer (facts) → retry misses → jq (law) → nika:decide (publish?) → infer (story)
```

Contradiction or two fighting facts → White, never a guessed belt.

## Author

Thibaut Melen

- GitHub · [ThibautMelen](https://github.com/ThibautMelen)
- X · [@ThibautMelen](https://x.com/ThibautMelen)
- LinkedIn · [ThibautMelen](https://www.linkedin.com/in/ThibautMelen)

MIT. AI-Driven Dev may reuse this work, including commercially, with attribution.
