# yaml — conformance

> Path: `repository/yaml/conformance/`
> Sibling (AGENTS): [`./AGENTS.md`](AGENTS.md)

`yaml` reads one YAML subset into `json`'s `Json` (decision 396). Markdown, YAML and JSON are three
libraries of their own, and std knows nothing of JSON. This reference describes the library as the
decisions fix it; every example is a conformance cell (decision 461), and a decision's example is its
directory under `modules/decisions-taken/`, linked from the section it shows. A table, a grammar or a
file layout is not a program and is fenced as `text`.

| Section | What |
|---|---|
| *The library* | what `yaml` reads, what it refuses, its dependency |
| *Reading a document* | `decode` and its `Error` |
| *Decisions* | `modules/decisions-taken/`: the ledger's index |

## The library

`yaml` reads one YAML subset into `json`'s `Json`: mappings, sequences, scalars and flow collections
(decision 396 (2)). It depends on `json`, which holds the `Json` value type and its methods
(`members`, `field`, `str`, `items`, `isObject`, `kindName`, …) and `encode`; a program declares both
libraries in its `"dependencies"` and imports `Json` and `encode` `from "json"`, since std has no JSON
module. The subset is small on purpose, and what falls outside it is refused rather than read as some
other value (decision 67):

```text
read      block mapping, block sequence, flow collections ([a, b]), plain scalars, comments
refused   an anchor and its alias, a tag, a second document — each with the line it is on
```

rakun's `config.bp` reader was the seed of this library and is deleted; `rakun-ssr`'s content reads its
frontmatter through `yaml` (decision 396 (2)).

Departure: the repository holds its scaffold only, with no `src/` yet, so there is no public module to
describe beyond what decision 396 fixes; the sections below follow the decision, and the declarations
and their `///` comments replace them when the reader lands (front 142 step 2).

## Reading a document

The reader is `decode` from `yaml`, taking the text of a document and answering a `Result` whose `Ok`
is the document as `Json`. A block mapping with `name`, `port` and `debug` comes out as an object whose
members `kindName` reports as a string, a number and a boolean, a block sequence and a flow sequence as
arrays, and a comment is skipped. Written back with `json`'s `encode`, the document is JSON text.

Each construct outside the subset answers an `Error` naming the line: an anchor with its alias, a tag,
and a second document. None is silently read as another value. The example is
[data_formats_are_own_libraries-396](modules/decisions-taken/data_formats_are_own_libraries-396/draft/main.bp).

## Decisions

`modules/decisions-taken/` is the ledger's index: one `<slug>-<N>/` per code-bearing row of this
repository's generated `decisions-taken.md` (front 166, decisions 646-651), its `docs.md` walking through
one example program. The cells that show a point of a section above are linked from it:
[data_formats_are_own_libraries-396](modules/decisions-taken/data_formats_are_own_libraries-396/draft/main.bp) (the reader and `json`, together).
The rows that bind every library show the language the library is written in:
[own_module_import_without_from-206](modules/decisions-taken/own_module_import_without_from-206/draft/main.bp) (a module of the package imported by its path, with no `from`),
[shorthand_import_refused-337](modules/decisions-taken/shorthand_import_refused-337/draft/main.bp) (a bare name never reaches a dependency's modules),
[optional_typescript_operators-330](modules/decisions-taken/optional_typescript_operators-330/draft/main.bp) (`?T` read with TypeScript's operators) and
[libraries_run_at_build_on_wasm-594](modules/decisions-taken/libraries_run_at_build_on_wasm-594/draft/main.bp) (a library at build on the wasm comptime runtime).
