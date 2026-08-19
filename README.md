# laivel

A lead-tech tool that places a developer on the official AIDD grid.

Built for [LAIVEL UP](https://github.com/ai-driven-dev/laivel-up) · 28–31 August 2026.

The model extracts four axes. `jq` applies the law *all axes or nothing*. The model then says how to climb one level. It cannot change the level.

## Run it

```bash
brew install supernovae-st/tap/nika   # or the install at https://nika.sh
nika run laivel.nika.yaml --input profile=./fixtures/green.md
```

Zero-key rehearsal:

```bash
nika run laivel.nika.yaml --model mock/echo --input profile=./fixtures/incomplete.md
```

Output: `out/verdict.md` plus `--output json`.

## How it works

See [METHOD.md](./METHOD.md). Official grid: [ai-driven-dev/laivel-up `levels/aidd.md`](https://github.com/ai-driven-dev/laivel-up/blob/main/levels/aidd.md).

```
profile  →  extract (infer)  →  score (jq)  →  explain (infer)  →  verdict
                 │                    │
            typed signals        the law lives here
```

## Author

Thibaut Melen

- GitHub · [ThibautMelen](https://github.com/ThibautMelen)
- X · [@ThibautMelen](https://x.com/ThibautMelen)
- LinkedIn · [ThibautMelen](https://www.linkedin.com/in/ThibautMelen)

MIT. AI-Driven Dev may reuse this work, including commercially, with attribution.
