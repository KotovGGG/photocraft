# Migrate legacy panel layouts into the shared Workspace

Restore the earlier fork's bare layout and column metadata as one shared Workspace instead of resetting it. Preserve tab order/selection, weighted rows, column placement/size, native-window positions and hidden return locations; save/reload the resulting versioned Workspace with independently validated view metadata.

Unsupported attachment sides retain the original payload rather than losing a panel. The old 44 pt view default upgrades once; explicit later widths remain personal. This part does not introduce the compact renderer or floating Tools input. Palette view metadata is persisted now for the dependent presentation changes.

Depends on #10910, which follows #10908. Review only the migration delta: six files (+513/-8). The rendering and Tools branches are separate review units.

Validation: 52 docking/migration tests, 31 dock tests and 9 workspace integration tests passed; desktop check/fmt passed. Correct-checkout layers/wasm passed using an isolated xtask binary (earlier shared-target xtask logs are superseded). The migrated stock-layout offscreen PNG was inspected. Strict UI Clippy remains blocked at unchanged upstream IO diagnostics (document.rs106 drop_non_drop; smart_map/import.rs784 nonminimal_bool).


No local shared-library override or CI changes are included. This series consumes the immutable upstream revision accepted in storytold/craft-libs#470. Physical multi-monitor/mixed-DPI, native focus/IME and GPU latency remain manual desktop acceptance; the product EXE was not built or launched. No full UI-suite or strict Clippy pass is claimed.
