# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.1.0] - 2026-07-05

### Added

- Initial release, extracted from the MindTape workspace (`crates/typst-edit`).
- `find_calls`/`find_method_calls` locate function/method calls with argument
  value spans and a trailing content block; `find_link_targets` is the thin
  link-only case over `link(...)`.
- `apply` rewrites a source string from a validated, atomic, non-overlapping
  `Edit` set — rejects overlapping, out-of-bounds, or non-char-boundary edits
  before writing anything.
- Optional `serde` feature deriving `Serialize` on `Call`, `Arg`, `Body`,
  `Edit`, and `LinkTarget`.
- No eval, no `World`, no IO — works on plain text and the `typst-syntax`
  parse tree alone.
