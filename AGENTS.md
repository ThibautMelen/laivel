# AGENTS.md — Nika workflows in this repo

Nika is a sovereign AI workflow engine. Workflows are `*.nika.yaml` files,
**audited before they run**. (This guide is scaffolded by `nika init`.)

## The loop
- **Author** · `nika new <template> <file>.nika.yaml` (or write one —
  the envelope is `nika: <id>` (kebab-case — the id lives ON the tag)
  + a `tasks:` MAP keyed by task id. A `tasks:` sequence refuses
  `NIKA-PARSE-022`).
- **Check** · `nika check <file>` — the static audit BEFORE any run (schema ·
  DAG · CEL · effects · permits · cost). Exit `0` clean · `2` findings.
  `--fix` applies the machine-applicable repairs (typed did-you-mean renames —
  fields · tools · args · edge targets · refs — plus the provable
  `depends_on` → `with:`/`after:` migration and `tasks.*` hoists) and
  re-audits; ambiguity is skipped with a note, never guessed.
- **Run** · `nika run <file>` — execute · live render. Exit `0` ok · `1` failed.
  Inputs ride `--var key=value` (repeatable · the flag names an `inputs:`
  declaration · unknown keys refused); a run
  paused on a `nika:prompt` resumes with `--resume <trace> --answer
  <task>=<value>` (confirm gates take booleans: `--answer approve=true`).
- **Pin** · `nika test <file> --update` writes `<file>.golden.json` from a
  simulated run — the model is `mock/echo` (offline · deterministic) and
  real effects are REFUSED, never performed; `nika test <file>` replays
  and compares — zero keys, the CI gate.
- **Arm** · `nika arm` — what this project's `nika.yaml` has ARMED (`arm:`)
  and when each beat next fires. READ-ONLY: it schedules nothing — the file
  proposes, the machine disposes.
- **Diagnose** · `nika doctor` — the environment (providers · keys · config).
  `nika welcome` is the short mirror (machine · workspace · next commands).
- **Context** · `nika welcome --deep --json` — the whole workspace truth in one
  call (every workflow audited · recent runs · costs · capped and says
  so). Read it before proposing edits.
- **Explain** · `nika explain NIKA-XXXX` teaches one error code ·
  `nika explain <file>` narrates a workflow (waves · cost · touches · how
  to run) — read it before handing a workflow to a human.
- **Wire** · `nika wire <cursor|vscode|windsurf|claude|codex|all>` — point an
  agent client's MCP config at the real oracle (idempotent · preserves other
  servers).

## The four verbs (exactly one per task)
`infer` (an LLM call) · `exec` (a subprocess — `command:` is argv, one token per
element, run via execve · no implicit shell: pipes, redirects and globs go in
`shell:` explicitly) · `invoke` (a `nika:` builtin or MCP tool) · `agent` (a
multi-turn ReAct loop).

## Hard rules (the validator enforces these — they catch ~90% of LLM errors)
- One verb per task · the verb IS the task key (never a `verb:` field).
- Values live in THREE authorities, a closed family: `inputs:` (typed ·
  caller-supplied · a deployment-supplied value is an input with
  `required: false` and a `default:`) · `const:` (fixed in the file) ·
  `secrets:` (governed store references). `vars:` and `env:` are dead
  envelope fields (`NIKA-VALUES-001` · `NIKA-VALUES-002`), `config:` is not
  a field at all (it died with the nine-key envelope · `NIKA-PARSE-005`),
  and any other namespace is `NIKA-VALUES-003` — classify each entry by the
  role it plays; `check --fix` migrates the `vars:` half, `env:` is a human
  classification.
- `tasks.X` crosses a task boundary only through `with:` (the binding IS the
  data edge — the body reads `${{ with.<name> }}`, never `tasks.*` directly)
  or `after: {X: success}` (control · predicates `success` · `failure` ·
  `skipped` · `terminal`). `depends_on` is dead (`check --fix` migrates).
- Quote any YAML scalar that STARTS with `${{` (an unquoted leading `${{`
  breaks the parse).
- `invoke` arguments live under `args:` (not `input:` / `params:`).
- `when:` is a `${{ }}` CEL boolean or the literal `true`/`false` — a bare
  string is rejected. `size()` is the only CEL function.
- `nika:write` needs `content:` · `nika:done` is valid only inside `agent.tools`.
- snake_case task ids · kebab-case workflow id (on `nika:`).

## Don't invent structure — route to a skeleton
`nika new '?'` lists the embedded skeletons · `nika try` /
`show <slug>` reads a runnable example that exercises a construct ·
`nika spec --schema` is the JSON Schema · `nika spec --canon` is the SSOT ·
`nika catalog` names the providers/models · `nika catalog --tools` names the `nika:`
builtins. Copy, fill, check.

## Cost honesty (never hide unknown spend)
- `nika check` prints the ceiling BEFORE any token · `≥ $X FLOOR` means an
  unbounded task exists — name why, never round unknown to $0.
- A local model is unpriced compute, **never « free »**.
- `nika run <file> --max-cost-usd <n>` blocks BEFORE the call that would
  cross the cap.

## Understand · replay · prove
- `nika inspect <file>` — static anatomy: tasks · verbs · wave groups · cost.
- `nika inspect <file> --format mermaid|dot|json` — the ONE graph projector.
- `nika trace show|replay <run>` — the flight recorder (every run records).
- `nika trace verify <run>` — the journal is hash-chained: verify it after a
  run that matters, cite the trace instead of trusting a memory of the run.
- `nika key init|trust|rotate` — the run-signing key: it seals journals and
  signs workflows (print the fingerprint with `nika key trust` to enroll it).
- `nika sign <file>` — author-bind a workflow (detached `<file>.minisig`
  sidecar · the workflow itself never changes) · `nika sign --check <file>`
  verifies · `nika run --require-signature <file>` refuses an unsigned or
  invalidly-signed workflow BEFORE anything executes (exit 2).
- `nika trace evidence <run>` — export the evidence pack: journal + manifest
  (hash · boundary · trifecta · sandbox · seal grade) + receipt + VERIFY.md.
- `nika dap` — step a recorded run under a debugger UI, forward AND back.

## Servers (stdio · for editors and agent clients)
`nika lsp` (language server) · `nika mcp` (MCP: check/explain/schema/examples
as tools) · `nika completions <shell>` generates shell completions.
`nika model serve --model <path.gguf>` serves a local model on loopback
(OpenAI-compatible · needs a `local-infer` build — the default binary
prints the build recipe).

## Discipline
- `permits:` IS the boundary, and ABSENT MEANS ZERO AUTHORITY: an effect under
  no block refuses `NIKA-AUTH-006` at check, before a token is spent. A pure-
  compute body states the zero explicitly as `permits: {}`.
  `nika check --infer-permits` prints the tightest block; a bound is always a
  literal, never an interpolation (`NIKA-AUTH-007`).
- A spawned child inherits NOTHING from the engine: its environment is the
  runner floor ∪ the names in `permits: { env: [NAME] }` ∪ the task's own
  `env:` map. A variable the child needs must be named.
- Secrets come from the environment (`${{ secrets.X }}`) — never inline.
- `nika check` must be clean before `nika run` (audit-before-run is enforced).
- The wired shell hook's judge is `nika guard` (the execution seatbelt):
  before a `nika run` leaves the agent's shell it audits the exact file —
  a red file or a priced model without `--max-cost-usd` is denied with the
  findings; `guard_unavailable` means the judge could not see, never that
  the check passed.
