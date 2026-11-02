# Repair compact panel docking and independent resizing

Collapsed panel rows now detach as compact palettes while expanded editors retain their normal sizes. Docking above/below the protected document row and within groups uses fitted geometry; compound parts collapse and resize independently. Header insertion, flyout bounds, outlines and one-physical-pixel seams share the same Workspace geometry and design tokens.

This includes replacement of the old launcher with real panel owners, transient hidden-panel reveal, and cached persistence for unchanged layouts. The existing stock toolbar only reports its boundary so the shared seam has one owner; floating Tools behavior follows in its own PR. Layout/metadata conversion is already in the migration parent.

Depends on the migration PR. Review its incremental branch delta, not the cumulative diff against main while earlier PRs are pending. Compact and resize behavior is one cohesive renderer/input change; its regression and capture tests are adjacent to the implementation. The sanitized original fixture has its own license and attribution. No demonstration GIF bundle is added to this PR.

Validation: 165 panel tests (2 ignored benchmarks), 31 dock, 2 embedding, 8 toolbar, 1 toolbar-boundary regression, 10 document-tab, and 9 workspace integration tests passed. Desktop check/fmt/layers/wasm passed. Four isolated WGPU captures passed: 444 PNGs across three Pro themes and four scales, including physical seam assertions. Representative captures inspected. A broad capture-process attempt exited abnormally; the four clean isolated reruns supersede it. An intermediate boundary-helper deadlock was reproduced and fixed before publication; the regression test passes.

Cached idle persistence test-profile p50 4.594 us, versus 17.053 us for serialize-every-frame on the same state. This is a microbenchmark, not native FPS or an end-to-end performance comparison. Current prefs audit: 10 of 183 unread. Strict Clippy stops at the same unchanged IO diagnostics; no-deps UI diagnostics are the six unchanged canvas/strokes.rs and menus/menu_keys.rs/menu_nav.rs findings. No source lint suppressions were added.


No local shared-library override or CI changes are included. This series consumes the immutable upstream revision accepted in storytold/craft-libs#470. Physical multi-monitor/mixed-DPI, native focus/IME and GPU latency remain manual desktop acceptance; the product EXE was not built or launched. No full UI-suite or strict Clippy pass is claimed.
