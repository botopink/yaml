# yaml

`decisions-taken.md` is generated — from the meta repository's `specs/<milestone>/decisions-taken.md` by `scripts/decisions-split.py`; edit it there, never here.

> Repository: `botopink/yaml` (`git@github.com:botopink/yaml.git`) · in the meta checkout: `repository/yaml/`

One YAML subset read into `json`'s `Json` (decision 396): mappings, sequences, scalars; an anchor, an alias, a tag and a second document each refused with the line (decision 67). Seeded from rakun's `config.bp` reader by 142 step 2; depends on `json`.

A library of its own (decision 396, decision 326's rule). It is filled by
`specs/1.0.12-beta/03-bundled-libs/142-data-formats`; until its step lands this repository holds
only its scaffold.

## Hooks

Every clone runs the shared pre-commit gate:

```sh
git config core.hooksPath scripts/git-hooks
```

The hook applies `botopink format` to the commit's staged source files before its gate (decision 524 — the
staged version, into the index; formatting never fails it) and runs the gate with `--jobs 2`.

`scripts/gate.sh [--staged] [--no-conformance] [--jobs <N>]` is the gate's one entry (one text in every
library repository, CI check 4; it runs `scripts/git-hooks/lib/runner-standalone.sh`): the pre-commit hook
runs `scripts/gate.sh --staged --no-conformance` (decision 470), and CI on a push to `feat` and a front's
Conformance step run it whole, which adds the last stage, `botopink cell check conformance/` over this
repository's `conformance/` cells (decisions 463, 464; the stage exists when the directory does). It knows no
job pool: `--jobs` is the total it may use, and the meta repository's `scripts/gate.sh run <repository>`
hands it its share.

`scripts/git-hooks/pre-commit` and `scripts/git-hooks/lib/runner-standalone.sh` are byte-identical
across the library repositories (the meta repository's CI check 4); edit them in one place and copy.
