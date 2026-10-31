Hosts drawing compact columns or custom group chrome need to use the workspace's fitted rectangles without also receiving stock painting/input. This adds opt-in host hooks and independent floating resize axes while retaining one shared layout model.

Changes:
- Report fitted column rectangles, allow exclusive iconic columns/custom groups, and forward all hooks through `show_customized`.
- Allow host-owned seam painting and horizontal floating sizing while preserving stock vertical handles, including at corners.
- Add an optional side-dock gap and top-gutter opt-out. Default hooks remain no-op/false; constructors preserve the normal gap and both resize axes. Exhaustive `DockStyle` literals need `dock_gap: None`.
- Keep dock seam input above sibling canvas input and avoid pointer-derived focus on empty headers.

Scope: six implementation files, one focused test module and its registration, and README. No application code, vendored snapshot, fonts, binary assets, dependency/CI changes or additional layout tree.

Five new tests cover corner-axis behavior (including stock defaults), top gutter geometry, exclusive-group forwarding/targets, fitted iconic-column callbacks, and invalid numeric gaps.

Validation:
- `cargo test -p craft-ui --features serde,native-windows,screen-testing`: 584 unit tests, 10 integration tests, and 8 doctests passed (2 doctests ignored).
- `cargo fmt --check`: passed.
- `cargo check --target wasm32-unknown-unknown -p craft-ui`: passed.
- Strict UI Clippy is not green: two `nonminimal_bool` diagnostics in unchanged `crates/ui/src/docking/render/preview.rs:120`.
- Workspace Clippy stops in unchanged `crates/keymap/src/profiles.rs:474` (`nonminimal_bool`).
- `cargo test --workspace` does not complete: Rust 1.95.0 MSVC reports an internal compiler error (broken MIR) while compiling unchanged `craft-text` test `linebreak::tests::every_line`, at `crates/text/src/linebreak/tests.rs:95`. No workspace-wide pass is claimed. All three failure-site files have no diff from the current base; no suppressions or unrelated changes are included.

This is the first, focused extraction from storytold/photocraft#10322 following the maintainer's request to split that large PR. Accepting these APIs lets PhotoCraft pin an immutable upstream revision and remove its roughly 41k-line shared-library snapshot. The remaining PhotoCraft integration/persistence, compact/resize and Tools changes will follow as dependent PRs with their own tests.
