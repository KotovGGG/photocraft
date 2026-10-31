Hosts drawing compact columns or custom group chrome need to use the workspace's fitted rectangles without also receiving stock painting/input. This adds opt-in host hooks and independent floating resize axes while retaining one shared layout model.

Changes:
- Report fitted column rectangles, allow exclusive iconic columns/custom groups, and forward all hooks through `show_customized`.
- Allow host-owned seam painting and independent ownership of horizontal frame edges/internal dividers while preserving stock vertical handles, including at corners.
- Add an optional side-dock gap and top-gutter opt-out. Default hooks remain no-op/false; constructors preserve the normal gap and both resize axes. Exhaustive `DockStyle` literals need `dock_gap: None`.
- Keep dock seam input above sibling canvas input and avoid pointer-derived focus on empty headers.

Scope: six implementation files, one focused test module and its registration, and README. No application code, vendored snapshot, fonts, binary assets, dependency/CI changes or additional layout tree.

Ten focused tests cover corner axes, top gutter geometry, exclusive host surfaces and fitted float sizes, stripless collapse, separate frame/internal-divider ownership, real pointer resizing, adapter forwarding, and invalid numeric gaps.

Validation:
- `cargo test -p craft-ui --features serde,native-windows,screen-testing`: 589 unit tests, 10 integration tests, and 8 doctests passed (2 doctests ignored).
- `cargo fmt --check`: passed.
- `cargo check --target wasm32-unknown-unknown -p craft-ui`: passed.
- Strict UI Clippy is not green: two `nonminimal_bool` diagnostics in unchanged `crates/ui/src/docking/render/preview.rs:120`.
- Workspace Clippy stops in unchanged `crates/keymap/src/profiles.rs:474` (`nonminimal_bool`).
- `cargo test --workspace` does not complete: Rust 1.95.0 MSVC reports an internal compiler error (broken MIR) while compiling unchanged `craft-text` test `linebreak::tests::every_line`, at `crates/text/src/linebreak/tests.rs:95`. No workspace-wide pass is claimed. All three failure-site files have no diff from the current base; no suppressions or unrelated changes are included.

This is the first, focused extraction from storytold/photocraft#10322 following the maintainer's request to split that large PR. Accepting these APIs lets PhotoCraft pin an immutable upstream revision and remove its roughly 41k-line shared-library snapshot. The remaining PhotoCraft integration/persistence, compact/resize and Tools changes will follow as dependent PRs with their own tests.


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Docking content can customize or take ownership of iconic columns, tab groups, resize handles, and split separators, and control group-collapse presentation and floating-window width resizing.
  * Floating frames support configurable horizontal and vertical resizing, plus an optional top resize band. The band is reserved by default when resizing is enabled.
  * Dock layouts can set a separate gap for docked panels.
* **Bug Fixes**
  * Resize controls and docking geometry now respect configured axes, gaps, and host-owned content.
* **Documentation**
  * Added guidance on docking customization, ownership options, defaults, and compatibility.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->