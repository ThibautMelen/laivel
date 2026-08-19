# laivel

**30 seconds.** One Nika workflow places a developer on the official AIDD
grid (White → Gold). OpenAI extracts cited facts. `jq` applies the law:
a level is reached only if every axis is. `nika:decide` publishes or
abstains. Incomplete or contradictory notes go White — never a guessed
belt. Clone standalone, install Nika, run.

Built for [LAIVEL UP](https://github.com/ai-driven-dev/laivel-up) · 28-31 August 2026.

[METHOD.md](./METHOD.md) · [VIDEO.md](./VIDEO.md) · grid [levels/aidd.md](./levels/aidd.md)

## Run it

**Clone standalone.** If another `nika.yaml` sits above this folder
(a monorepo), `nika` loads that file first and refuses.

```bash
brew install supernovae-st/tap/nika   # https://nika.sh
git clone https://github.com/ThibautMelen/laivel.git
cd laivel
export OPENAI_API_KEY=...             # openai/gpt-5-mini
nika run laivel.nika.yaml --max-cost-usd 3
```

Default glob: `./fixtures/*.md`.

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

## Outputs

| path | what |
|---|---|
| `out/verdicts/*.md` | one note per profile |
| `out/team.md` · `out/team.json` · `out/team.yaml` | roster |
| `out/team.svg` · `out/belts.svg` · `out/axes.svg` | charts |
| `out/receipt.json` | blake3 of the roster + `nika:date` + `nika:uuid` |
| `out/JURY.md` | one page for the jury (jq, not the model) |
| `out/self-test.patch.json` | empty array when `self_test` matches |

## How it works

```
glob (exclude README) → read → infer (facts) → retry → fallback
     → jq (law) → nika:decide (publish?) → infer (story)
     → assert cards==glob → log decide+belts
     → nika:hash + nika:validate + 3 charts + JURY.md
```

Contradiction or two fighting facts → White, never a guessed belt.
The model never writes a belt. The law lives in `jq`, frozen.

## Author

Thibaut Melen

- GitHub · [ThibautMelen](https://github.com/ThibautMelen)
- X · [@ThibautMelen](https://x.com/ThibautMelen)
- LinkedIn · [ThibautMelen](https://www.linkedin.com/in/ThibautMelen)

MIT. AI-Driven Dev may reuse this work, including commercially, with attribution.
