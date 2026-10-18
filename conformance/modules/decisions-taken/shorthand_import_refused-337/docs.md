# Decision 337 — The shorthand import goes; `mod m;` binds the namespace `m` in the module that declares it.

The example is refused: it shows the refusal. `draft/page.bp` declares `pub fn frontMatter`, and `main` imports it with `import {frontMatter};`. That item has no `from`, and its first segment is not the name of any module of the package, so it is a shorthand import. Shorthand imports are refused with `shorthand-import` at the item. Only one module of the package declares `frontMatter` as `pub`, so the diagnostic writes the fix: `write import {page.frontMatter};`. A bare name never reaches into a dependency either: `decode` comes from `yaml` because the line says `from "yaml"`, not because the name happens to be unique.

With the fix applied, the program decodes the front matter and prints `Notes`.

Proving cells: none in this repository yet; the language's are botopink-lang's `conformance/modules/shorthand_import`, `shorthand_import_one_candidate`, `shorthand_import_several_candidates`, `redundant_module_import`, `declaration_named_like_module`, `mod_binds_namespace`, `mod_namespace_cascade`, `mod_reexport_by_val` and `private_module_through_namespace`.

[draft/main.bp](draft/main.bp)
[draft/page.bp](draft/page.bp)
