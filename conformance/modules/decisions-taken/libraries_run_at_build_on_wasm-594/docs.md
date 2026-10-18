# Decision 594 — Every library runs at build on the wasm comptime runtime (434), jhonstart first; a function only Erlang or Node can run is a located error there.

The example converts a YAML document to JSON text twice: once inside a `comptime`, which runs at build, and once at run time. The build-time call goes through `yaml`'s `decode` and `json`'s `encode`, and it runs on the wasm comptime runtime whatever `--target` the build uses. Both libraries are written in botopink, so every function the `comptime` reaches has a wasm form. The JSON text is computed during the build and spliced into the program as a literal, so `atBuild == atRun` is `true` on every target. The third line computes a refusal, an anchor, at build in the same way: the `Error` text is spliced as a constant. Nothing in the program is refused at build.

Proving cells: none in this repository yet.

[draft/main.bp](draft/main.bp)
