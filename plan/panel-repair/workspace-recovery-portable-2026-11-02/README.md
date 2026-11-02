# Workspace recovery extraction, 2026-11-02

PR: https://github.com/storytold/photocraft/pull/10910
Branch: codex/panel-workspace-recovery, source 3dbd11e35.
Local checkout F:/photocraft-panel-integration. Parent adoption aa5cd1dcf (#10908), not merged at preparation. Main source stays F:/photocraft codex/panel-layout-upstream 69b370d2d. Do not run from the handoff branch root.

Same-version unreadable Workspace data and five companion keys preserved through fallback, idle persistence and explicit snapshot. Explicit panel edit replaces it; readable/bare/default behavior and future envelopes without a layout field covered. A restore notice is shown. No compact/Tools geometry changes.

31 dock +43 docking +9 workspace tests passed. fmt/check/layers/wasm passed. Offscreen WGPU warning PNG inspected. Strict Clippy stops at unchanged main IO document.rs106 drop_non_drop and smart_map/import.rs784 nonminimal_bool. No full UI, EXE, physical native or fresh perf claims. Red regression recorded before fix. Tests/final source evidence in evidence.zip.

Next: #10908 before #10910; migration/compact/resize/Tools remain further review units. Do not merge PRs automatically or change other contributors/CI. Credits @KotovGGG. Preserve old D:/photocraft and profiles.
