# typst-edit

[![CI](https://github.com/mlavrinenko/typst-edit/actions/workflows/ci.yml/badge.svg)](https://github.com/mlavrinenko/typst-edit/actions/workflows/ci.yml)
[![crates.io](https://img.shields.io/crates/v/typst-edit.svg)](https://crates.io/crates/typst-edit)
[![License: MIT](https://img.shields.io/crates/l/typst-edit.svg)](LICENSE-MIT)

In-place editing for Typst source: parse-plane span queries and an atomic, non-overlapping changeset over typst-syntax; no eval, no World, no IO

## Install

```bash
cargo add typst-edit
```

## Usage

```rust
use typst_edit::{Edit, apply, find_link_targets};

let src = "see #link(\"old.typ\")[here]";
let targets = find_link_targets(src);
let target = targets.first().expect("one link");
let edit = Edit::new(target.range.clone(), "\"new.typ\"");
let out = apply(src, vec![edit]).expect("apply");
assert_eq!(out, "see #link(\"new.typ\")[here]");
```

`find_calls`/`find_method_calls` locate any function or method call with its
argument value spans and trailing content block; `find_link_targets` is the
thin link-only case. `apply` rewrites a source string from a validated `Edit`
set — edits are validated as a whole before anything is written, so a rejected
set leaves no partial result. Enable the `serde` feature to derive
`Serialize` on the located types (`Call`, `Arg`, `Body`, `Edit`, `LinkTarget`).

## Development

Prerequisites: [Nix](https://nixos.org/) with flakes enabled.

```bash
direnv allow         # or: nix develop

just check           # fmt + clippy + tests + file-size + drift check
just build
just test
just cover           # code coverage (70% minimum)
just fmt             # format code
```

See [CONTRIBUTING.md](CONTRIBUTING.md) for coding conventions.

## License

MIT
