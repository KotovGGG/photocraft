Restore the earlier fork's bare layout and column metadata as one shared Workspace instead of resetting it. Preserve tab order/selection, weighted rows, column placement/size, native-window positions and hidden return locations; save/reload the resulting versioned Workspace with independently validated view metadata.

Unsupported attachment sides retain the original payload rather than losing a panel. The old 44 pt view default upgrades once; explicit later widths remain personal. This part does not introduce the compact renderer or floating Tools input. Palette view metadata is persisted now for the dependent presentation changes.

Depends on #10910, which follows #10908. Review only the migration delta: six files (+513/-8). The rendering and Tools branches are separate review units.

Validation: 52 docking/migration tests, 35 dock tests and 9 workspace integration tests passed; desktop check/fmt passed. Correct-checkout layers/wasm passed using an isolated xtask binary (earlier shared-target xtask logs are superseded). The migrated stock-layout offscreen PNG was inspected. Strict UI Clippy remains blocked at unchanged upstream IO diagnostics (document.rs106 drop_non_drop; smart_map/import.rs784 nonminimal_bool).


No local shared-library override or CI changes are included. This series consumes the immutable upstream revision accepted in storytold/craft-libs#470. Physical multi-monitor/mixed-DPI, native focus/IME and GPU latency remain manual desktop acceptance; the product EXE was not built or launched. No full UI-suite or strict Clippy pass is claimed.

Recovery follow-up: explicit native fallback edits replace retained unreadable data; appearance/no-op edits preserve it. Restore/reset clears only its owned warning, and the notice remains accessible with hidden status chrome/fullscreen. These parent changes are tested again in this branch. The Window panel menu routes also distinguish actual reveal/hide/expand edits from no-op show requests; the notice explicitly explains that panel edits or a reset replace the preserved layout.

Prepared head: `0332e0bdb4a40401f51db1bf3313d01b9255b71a`. Parent: `b42f8dd0557efe40a53e8fa7d52f30733bb7767f`. Incremental delta: 6 files changed, 513 insertions(+), 8 deletions(-).
