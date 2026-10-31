Panel moves and resize gestures now follow the shared workspace's fitted geometry. This repairs compact rows tearing off as wide strips, editors inheriting miniature heights, closed tabs appearing selected, overlapping/missing seams, and compound resizing that changes neighbours or ignores the bottom corners.

### Behavior

- Dock panels above or immediately below document tabs, and above/below another panel within a group. Collapsed top/bottom rows remain attached and accept tab insertion before, between and after existing tabs.
- Tear a collapsed row off as a compact palette; an expanded editor retains its normal floating size. Joining a full editor to a short compact owner preserves its height on join and detach.
- Collapse neighbouring parts independently, resize the middle floating part without resizing its neighbours, and resize a group's bottom edge/corners before changing its width. Repeated collapse/expand restores normal group heights.
- Move Tools only as a whole palette and resize it on both axes. Ordinary layer selection keeps Properties closed; adjustment/fill reveal remains available.
- Keep one serialized shared `Workspace`, legacy/unsupported-layout recovery, and token-derived single-owner seams and outlines.

### Integration and scope

Current main `422ca7beda90d927643bcd074646ebbd37706d75` is integrated; all merge conflicts are resolved. The explicit `vendor/craft-ui` snapshot is reconciled with main's immutable `c5a1cbfb5f9049f9270955caffb5bee5997aebf7` revision. Of its source files, 76 match upstream; six contain the documented optional host hooks/geometry patch. The build-time revision contract remains enforced and egui's pin is unchanged.

Review the [host/shared contract](https://github.com/KotovGGG/photocraft/blob/d0e052e48434fa13f4ad60eebd20eb125bacac24/docs/panel-docking-contract.md) and [local shared-library patch](https://github.com/KotovGGG/photocraft/blob/d0e052e48434fa13f4ad60eebd20eb125bacac24/vendor/craft-ui/PATCH.md). Scope is panel UI, shell command registrations, persistence and existing auto-show wiring. No CI, ATN/PSD, action-name/text or contributor-credit changes relative to main. The two earlier CodeRabbit documentation findings are fixed.

### Validation and acceptance

Validated code: `88da5a9142c9c55bbb9fb93abe8ddc5192f83929`; the final commit updates only documentation/assets.

- **164 panel tests**, **579 shared UI tests** (including 346 docking tests), and **9 workspace integration tests** passed.
- Desktop all-targets `cargo check`, fmt, 31-crate layering, and 24-crate wasm plus codecs/heif checks passed.
- **444 fresh offscreen PNGs**, three Pro themes, 100/125/150/200% scale; all four capture runs and their seam assertions passed. The after PNGs and GIFs were regenerated on the integrated code.
- **Full UI library suite is not green:** 4494 passed, 95 failed, 23 ignored. All 95 failure names exactly match the pre-merge repaired v0.18.0 snapshot; this is not an independently rerun clean-main baseline.
- **Strict Clippy is not green:** unchanged main text/UI findings and a boolean-style finding in unchanged pinned shared-library `docking/render/preview.rs`. No suppressions or unrelated fixes were added. Exact commands, locations and limitations are in the [validation notes](https://github.com/KotovGGG/photocraft/blob/d0e052e48434fa13f4ad60eebd20eb125bacac24/docs/panel-docking-validation.md).

The contributor rebuilt and tested the repaired v0.18.0 Windows EXE and reported no remaining major panel issues. That manual acceptance preceded the final main/shared-widget merge; the integration has the automated coverage above. Native focus/IME, physical mixed-DPI/monitor coverage and GPU/input latency are not separately certified. The agent did not build or launch the product EXE.

<details>
<summary>Latest regression demonstrations (offscreen gesture states)</summary>

Panel insertion below document tabs:

![Insert below document tabs](https://raw.githubusercontent.com/KotovGGG/photocraft/d0e052e48434fa13f4ad60eebd20eb125bacac24/docs/images/panel-repair/below-document-tabs.gif)

Normal heights when expanding and restoring a compact group:

![Restore compact group heights](https://raw.githubusercontent.com/KotovGGG/photocraft/d0e052e48434fa13f4ad60eebd20eb125bacac24/docs/images/panel-repair/compact-group-height.gif)

Outer bottom resize without a preliminary width change:

![Resize the floating group bottom](https://raw.githubusercontent.com/KotovGGG/photocraft/d0e052e48434fa13f4ad60eebd20eb125bacac24/docs/images/panel-repair/floating-bottom-resize.gif)

[Before/after demonstrations and reproduction](https://github.com/KotovGGG/photocraft/blob/d0e052e48434fa13f4ad60eebd20eb125bacac24/docs/panel-docking-demo.md). Recordings contain only panel UI and synthetic blank documents; provenance and licenses are adjacent.

</details>

Related to #217.
