# Decision 206 — `import {…} from "<name>"` resolves only to a package — std, a bundled package or a declared dependency.

The example reads a page's front matter. The package has a module of its own named `yaml` (`draft/yaml.bp`, which cuts the front matter out of the page) and declares the `yaml` library as a dependency, so one name means two things and the import line says which. `import {yaml.frontMatter};` is the brace form with no `from`: the module's path, then the item, so it reaches this package's `yaml.bp`. `import {decode} from "yaml";` names a package, so it reaches the dependency and never the module beside it, even though the module has the same name. `json` and `std` are packages too, imported the same way (`from "json"`, `from "std"`).

`main` cuts the front matter with the module's `frontMatter`, decodes it with the library's `decode` into `json`'s `Json`, and prints the title, `Notes`. If the example had written `import {frontMatter} from "yaml";`, the import would look for `frontMatter` in the dependency, and the dependency does not declare it.

Proving cells: none in this repository yet; the language's are botopink-lang's `conformance/modules/import_own_module_with_from`, `import_bundled_package_beside_own_module`, `import_module_path_in_braces` and `import_module_paths`.

[draft/main.bp](draft/main.bp)
[draft/yaml.bp](draft/yaml.bp)
