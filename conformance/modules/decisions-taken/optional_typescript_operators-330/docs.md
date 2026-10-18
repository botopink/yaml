# Decision 330 — `?T` is read with TypeScript's operators and has no methods; `result` goes; a type declared in a type is its associated type.

The example decodes a small YAML document and reads it into `Page.Meta`. Every optional value is read with TypeScript's operators, never with a method. `doc.field("title")?.str() ?? "untitled"` reads a member that may be missing: `field` answers `?Json`, `?.str()` reads it only when it is there, and `??` supplies the default. `tags?.[0]?.str()` indexes through an optional array. `?.` flattens: the first item of an optional array is a `?Json` and not a `??Json`, so the next `?.` reads it directly. `fallback(true)?.("summary")` calls an optional function value. `meta.firstTag!` takes the value when the program knows it is there, and a `null` at that point would abort with the location.

The parentheses in `(meta.summary ?? "") == "" || …` are required: `??` next to `||` with no parentheses is a compile error. The decode result is a `Result`, and it is read with its own methods: `parsed.isOk()`, `parsed.map(…)` and `.unwrapOr(…)`. A `?T` has none of these, and there is no `result` namespace. `Meta` is declared inside the body of `Page`, so it is `Page`'s associated type and is written `Page.Meta` in signatures and constructors.

Proving cells: none in this repository yet; the language's are botopink-lang's `conformance/modules/optional_operators`, `optional_call_operator`, `optional_bang_aborts`, `optional_has_no_methods`, `nullish_beside_logical`, `nullish_never_null`, `optional_operator_never_null`, `result_namespace_removed` and `std_type_field_associated`.

[draft/main.bp](draft/main.bp)
