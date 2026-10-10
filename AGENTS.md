# yaml

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

`scripts/git-hooks/pre-commit` and `scripts/git-hooks/lib/runner-standalone.sh` are byte-identical
across the library repositories (the meta repository's CI check 4); edit them in one place and copy.
