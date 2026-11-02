# Float and resize the whole Tools palette

The Tools header/grip now moves the whole palette; individual tool buttons keep selecting tools and opening their flyouts. The detached palette resizes in both axes and restores its position/size through the Workspace's view metadata. Workspace lock, modal/generation cancellation and invalid coordinates/sizes are handled without partial state changes. Chrome metrics match the compact panels across themes.

Depends on the compact/resize PR. This delta contains the Tools owner, command routing, toolbar layout adaptation and Tools-specific tests; shared Workspace geometry and migration are in its parents. The 13 historical GIF illustrations remain in the full reference PR with their existing provenance; they are not presented as fresh acceptance of this branch.

Validation on the combined branch: 171 panel tests (2 ignored), 31 dock, 2 atomic/lock Tools command tests, 8 toolbar, 2 embedding, 10 document-tab and 9 workspace tests passed. Desktop check/fmt passed; correctly scoped layers/wasm passed. Engine panic_hunt passed (separate engine guard, not a substitute for the UI command regressions). Four isolated WGPU capture tests produced 444 PNGs; the Tools palette capture produced another 16 PNGs at four scales. Representative floating Tools PNG inspected.

Idle persistence test-profile p50 4.469 us, versus 18.606 us for serialize-every-frame on the same state. Strict Clippy limitations are unchanged IO diagnostics plus the six unchanged no-deps UI diagnostics. Standard release-example perf --quick is still running; its final result and limits will be added to the portable package before handoff completion.


No local shared-library override or CI changes are included. This series consumes the immutable upstream revision accepted in storytold/craft-libs#470. Physical multi-monitor/mixed-DPI, native focus/IME and GPU latency remain manual desktop acceptance; the product EXE was not built or launched. No full UI-suite or strict Clippy pass is claimed.
