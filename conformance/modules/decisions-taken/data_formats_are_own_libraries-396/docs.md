# Decision 396 — Markdown, YAML and JSON are three libraries of their own — `markdown`, `yaml`, `json` (`botopink/{markdown,yaml,json}` at `repository/{markdown,yaml,json}`, 326's rule) — and std knows nothing of JSON.

The example turns YAML into JSON with two libraries. `yaml`'s `decode` reads the text into `json`'s `Json`, and `json`'s `encode` writes it back out as JSON text. Neither comes from std: `Json` and `encode` are imported `from "json"`, and the program declares both libraries as dependencies. std has no JSON module to fall back on.

The first document covers the subset `yaml` reads. It has a block mapping (`name`, `port`, `debug`), a comment, a block sequence (`pages`), a flow sequence (`locales`), and plain scalars that come out as a string, a number and a boolean. `kinds` lists each member with its `Json` kind, which shows that the value is an ordinary `Json` that `members` and `kindName` can read. The last three documents fall outside the subset: an anchor with its alias, a tag, and a second document. Each one answers an `Error` that names the line it is on. None is silently read as some other value.

Proving cells: none in this repository yet.

[draft/main.bp](draft/main.bp)
