# yaml — conformance/

- `modules/decisions-taken/<slug>-<N>/` — front 166's decision cells (decision 651: the subtree is that front's alone): one
  per code-bearing row of `../decisions-taken.md`, a `docs.md` (first line generated) and, in phase 1, `draft/main.bp` (decision
  649; no `src/`, no manifest, so `botopink cell check` finds no cell there); kept by `scripts/decision-cells.py` of the meta
  repository and its CI check 7.
- `docs.md` — the library's reference, in botopink-lang's `conformance/docs.md` pattern (no fenced `botopink`; a table or
  layout is fenced as `text`; every example is a decision cell's draft, linked). One section each: *The library* (the
  subset `yaml` reads and what it refuses), *Reading a document* (`decode` and its `Error`, with the line), *Decisions*
  (the ledger's index). The repository holds its scaffold only, so the reference follows decision 396 until `src/` lands.
