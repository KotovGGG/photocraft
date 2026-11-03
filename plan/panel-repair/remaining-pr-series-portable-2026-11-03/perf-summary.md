## Performance (quick run)

- Machine: AMD64 Family 25 Model 33 Stepping 2, AuthenticAMD (12 cores, ?), GPU NVIDIA GeForce RTX 3060, Microsoft Windows [Version 10.0.19045.6456] x86_64; class `windows-x86-64-amd64-family-25-model-33-stepping-2-authenticamd-nvidia-geforce-rtx-3060`
- Commit 2052a95ed4b0fbbf0eee762767a4cbdf8b8f2b50, 2026-11-03T00:41:31Z
- Load average (1/5/15 min): n/a at start, n/a at end
- baseline is from machine class `macos-aarch64-apple-m4-pro-apple-m4-pro`, this is `windows-x86-64-amd64-family-25-model-33-stepping-2-authenticamd-nvidia-geforce-rtx-3060`: regression check skipped
- Quick mode: small documents, budgets not applied (they are set for full-size documents).
- Bench `bench_filters2`: ok, 1 s, load n/a
- Bench `bench_multiband`: ok, 0 s, load n/a
- Bench `bevel_bench`: ok, 3 s, load n/a
- Bench `camera_raw_bench`: ok, 1 s, load n/a
- Bench `layout_bench`: ok, 74 s, load n/a
- Bench `perf_scenarios`: ok, 15 s, load n/a
- Bench `perf_scenarios_cpu`: ok, 3 s, load n/a
- Bench `type_bench`: ok, 1 s, load n/a

| Id | Scenario | Target | p50 ms | p95 ms | max ms | Peak RSS | GPU | vs baseline | Status | Issue |
|---|---|---|---:|---:|---:|---:|---:|---:|---|---|
| P1 | Move a layer with layer styles (per drag update) | ≤ 25 ms p95 | 5.21 | 5.62 | 5.62 | 257 MB | 75 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P2 | Change layer opacity | ≤ 20 ms p95 | 3.86 | 4.33 | 4.33 | 268 MB | 75 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P3 | Change layer fill | ≤ 20 ms p95 | 3.42 | 3.54 | 3.54 | 268 MB | 75 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P4 | Change blend mode | ≤ 20 ms p95 | 3.44 | 3.57 | 3.57 | 269 MB | 75 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P5 | Toggle visibility | ≤ 10 ms p95 | 3.46 | 4.19 | 4.19 | 269 MB | 75 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P6 | Undo a move | ≤ 25 ms p95 | 4.21 | 5.06 | 5.06 | 280 MB | 75 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P7 | Redo a property change | ≤ 25 ms p95 | 3.42 | 4.27 | 4.27 | 280 MB | 75 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P8 | Duplicate a 12 MP layer (first) | ≤ 100 ms p95 | 5.37 | 5.95 | 5.95 | 597 MB | 167 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P9 | Duplicate a 12 MP layer (repeat) | ≤ 20 ms p95 | 4.48 | 4.80 | 4.80 | 553 MB | 167 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P10 | Paste a 12 MP layer (first) | ≤ 100 ms p95 | 5.64 | 5.92 | 5.92 | 577 MB | 227 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P11 | Paste a 12 MP layer (repeat) | ≤ 20 ms p95 | 6.60 | 6.92 | 6.92 | 578 MB | 227 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P12 | Arrow-key nudge in a 150-layer document | ≤ 30 ms p95 | 1.35 | 9.45 | 9.45 | 641 MB | 71 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P51 | New layer in a 150-layer document | ≤ 16 ms p95 | 0.52 | 0.54 | 0.54 | 583 MB | 71 MB | – | tracked | [#1771](https://github.com/storytold/photocraft/issues/1771) |
| P13 | Brush dab on a 15000×10000 16-bit document | ≤ 80 ms p95 | 1.22 | 1.71 | 1.71 | 639 MB | 176 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P14 | Move a layer on a 15000×10000 16-bit document | ≤ 80 ms p95 | 2.50 | 4.04 | 4.04 | 638 MB | 176 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P16 | Brush dab on a 32-bit document with 20 layers | ≤ 100 ms p95 | 1.92 | 1.97 | 1.97 | 707 MB | 121 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P17 | Move a layer on a 32-bit document with 20 layers | ≤ 100 ms p95 | 3.34 | 3.78 | 3.78 | 759 MB | 121 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P18 | Open a 20 MP layered PSD: first pixels (today: fully opened) | ≤ 1000 ms p95 | 79.7 | 85.0 | 85.0 | 861 MB | 279 MB | – | tracked | [#210](https://github.com/storytold/photocraft/issues/210) |
| P19 | Open a 20 MP layered PSD: editable | ≤ 3000 ms p95 | 79.7 | 85.0 | 85.0 | 861 MB | 279 MB | – | tracked | [#210](https://github.com/storytold/photocraft/issues/210) |
| P20 | Open a 2 GB PSD: editable | opens with progress, editable, never blank | – | – | – | – | – | – | not run | [#210](https://github.com/storytold/photocraft/issues/210) |
| P63 | Open a 4–5 GB PSB: editable | opens with progress, editable, never blank | – | – | – | – | – | – | not run | [#210](https://github.com/storytold/photocraft/issues/210) |
| P21 | Content-Aware Fill on 10 MP | ≤ 1500 ms p95 | 109 | 118 | 118 | 885 MB | 270 MB | – | tracked | [#210](https://github.com/storytold/photocraft/issues/210) |
| P22 | Spot Healing stroke on 10 MP | ≤ 500 ms p95 | 37.6 | 44.0 | 44.0 | 861 MB | 216 MB | – | tracked | [#210](https://github.com/storytold/photocraft/issues/210) |
| P24 | Import 500 brushes (longest UI-thread step) | ≤ 100 ms max | 1.55 | 1.63 | 1.63 | 480 MB | 211 MB | – | tracked | [#210](https://github.com/storytold/photocraft/issues/210) |
| P25 | Cancel a Gaussian Blur job on 24 MP (until the worker exits) | ≤ 200 ms p95 | 0.04 | 0.05 | 0.05 | 822 MB | 211 MB | – | tracked | [#210](https://github.com/storytold/photocraft/issues/210) |
| P49 | Cancel a Content-Aware Fill job on 24 MP (until the worker exits) | ≤ 200 ms max | 1.40 | 2.73 | 2.73 | 780 MB | 211 MB | – | tracked | [#210](https://github.com/storytold/photocraft/issues/210) |
| P50 | App frame time while a 24 MP Gaussian Blur job runs | ≤ 16 ms p95 | – | – | – | – | – | – | **missing**: only 9 frames while the job ran | [#210](https://github.com/storytold/photocraft/issues/210) |
| P26 | Select › Modify › Smooth on 24 MP (radius 50) | ≤ 100 ms p95 | 2.86 | 3.56 | 3.56 | 544 MB | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P27 | Select › Modify › Feather on 24 MP (radius 50) | ≤ 100 ms p95 | 5.46 | 5.73 | 5.73 | 560 MB | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P28 | Content-Aware Scale 24 MP (to 90 % width) | ≤ 3000 ms p95 | 62.7 | 62.7 | 62.7 | 586 MB | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P29 | Select Subject on 24 MP, repeated | ≤ 100 ms p95 | 0.37 | 0.41 | 0.41 | 566 MB | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P30 | Liquify 800 px brush on 3500×2200 at full resolution | ≤ 1 ms per update | 4.62 | 5.04 | 5.04 | 581 MB | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P31 | Camera Raw exposure change (proxy) | ≤ 10 ms | 7.31 | 7.69 | 7.69 | – | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P32 | Brush release on a long stroke | ≤ 16 ms (no hitch at mouse-up) | 0.82 | 0.89 | 0.89 | 486 MB | 93 MB | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P33 | Brush dab on A4 300 ppi CMYK (dab to screen) | ≤ 6 ms p95 | 1.27 | 6.32 | 6.32 | 437 MB | 86 MB | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P36 | Camera Raw exposure change with all SDR scopes (CPU) | ≤ 10 ms p95 | 14.5 | 18.7 | 18.7 | – | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P40 | Brush dab 60 px on 36 MP | track only | – | – | – | – | – | – | not run |  |
| P41 | Gaussian Blur r 40 on 36 MP | track only | – | – | – | – | – | – | not run |  |
| P42 | Curves dialog change, layer preview, 36 MP | track only | – | – | – | – | – | – | not run |  |
| P43 | Save .psd, 36 MP, 3 layers | track only | – | – | – | – | – | – | not run |  |
| P44 | Open .psd, 36 MP, 3 layers | track only | – | – | – | – | – | – | not run |  |
| P45 | Full refresh with layer effects, warm caches, 36 MP (GPU) | track only | – | – | – | – | – | – | not run |  |
| P46 | Brush dab on a layer with effects, 36 MP (GPU) | track only | – | – | – | – | – | – | not run |  |
| P47 | Font-size drag step, 50 type layers | track only | 2.66 | 3.35 | 3.35 | 122 MB | – | – | tracked |  |
| P48 | Full refresh of a 14000×14000 document | track only | – | – | – | – | – | – | not run |  |
| P52 | Chisel bevel size change, 12 MP ellipse, size 8 (GPU) | track only | 24.8 | 26.2 | 26.2 | 342 MB | – | – | tracked |  |
| P53 | Chisel bevel size change, 12 MP ellipse, size 50 (GPU) | track only | 30.9 | 32.2 | 32.2 | 479 MB | – | – | tracked |  |
| P54 | Chisel bevel size change, 12 MP ellipse, size 250 (GPU) | track only | 70.8 | 72.8 | 72.8 | 607 MB | – | – | tracked |  |
| P55 | Chisel bevel size change, 12 MP text paragraph, size 8 (GPU) | track only | 28.8 | 30.1 | 30.1 | 627 MB | – | – | tracked |  |
| P56 | Chisel bevel size change, 12 MP text paragraph, size 50 (GPU) | track only | 34.4 | 36.6 | 36.6 | 727 MB | – | – | tracked |  |
| P57 | Chisel bevel size change, 12 MP text paragraph, size 250 (GPU) | track only | 64.9 | 67.2 | 67.2 | 833 MB | – | – | tracked |  |
| P58 | Chisel bevel size change, 12 MP ellipse, size 8 (CPU) | track only | 36.8 | 39.1 | 39.1 | 342 MB | – | – | tracked |  |
| P59 | Chisel bevel size change, 12 MP text paragraph, size 8 (CPU) | track only | 46.3 | 46.8 | 46.8 | 627 MB | – | – | tracked |  |
| P60 | Layer opacity among 150 full-canvas layers, 6 MP (app GPU budget) | ≤ 30 ms p95 | 0.90 | 5.77 | 5.77 | 664 MB | 96 MB | – | tracked | [#5973](https://github.com/storytold/photocraft/issues/5973) |
| P61 | Hide a layer among 150 full-canvas layers, 6 MP (app GPU budget) | ≤ 30 ms p95 | 0.83 | 0.84 | 0.84 | 664 MB | 96 MB | – | tracked | [#5973](https://github.com/storytold/photocraft/issues/5973) |
| P62 | File > New 10 x 5 m at 200 ppi (3.1 GP) + first reduced canvas refresh | track only | 34.3 | 34.4 | 34.4 | 650 MB | – | – | tracked | [#4017](https://github.com/storytold/photocraft/issues/4017) |
| P64 | Oil Paint on 24 MP | ≤ 1000 ms p95 | 154 | 154 | 154 | – | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P65 | Smart Blur r 12 on 24 MP (High quality) | ≤ 1000 ms p95 | 211 | 211 | 211 | – | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P66 | Relight on 24 MP | ≤ 1000 ms p95 | 51.6 | 51.6 | 51.6 | – | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P67 | Reduce Noise on 24 MP | ≤ 1000 ms p95 | 43.7 | 43.7 | 43.7 | – | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P68 | Photomerge multi-band blend, synthetic | track timing and peak RSS; no calibrated performance budget | 16.6 | 17.1 | 17.1 | 41 MB | – | – | tracked | [#7758](https://github.com/storytold/photocraft/issues/7758) |
| P69 | Move a layer with layer styles, CPU compositor | track only | 15.0 | 16.3 | 16.3 | 247 MB | – | – | tracked | [#9330](https://github.com/storytold/photocraft/issues/9330) |
| P70 | Change layer opacity, CPU compositor | ≤ 40 ms p95 | 3.91 | 4.13 | 4.13 | 320 MB | – | – | tracked | [#9330](https://github.com/storytold/photocraft/issues/9330) |
| P71 | Change layer fill, CPU compositor | ≤ 40 ms p95 | 4.05 | 4.15 | 4.15 | 353 MB | – | – | tracked | [#9330](https://github.com/storytold/photocraft/issues/9330) |
| P72 | Change blend mode, CPU compositor | ≤ 40 ms p95 | 4.32 | 5.17 | 5.17 | 383 MB | – | – | tracked | [#9330](https://github.com/storytold/photocraft/issues/9330) |
| P73 | Toggle visibility, CPU compositor | ≤ 20 ms p95 | 3.94 | 4.18 | 4.18 | 394 MB | – | – | tracked | [#9330](https://github.com/storytold/photocraft/issues/9330) |
| P74 | Undo a move, CPU compositor | track only | 4.20 | 4.83 | 4.83 | 475 MB | – | – | tracked | [#9330](https://github.com/storytold/photocraft/issues/9330) |
| P75 | Redo an opacity change, CPU compositor | track only | 4.12 | 5.15 | 5.15 | 535 MB | – | – | tracked | [#9330](https://github.com/storytold/photocraft/issues/9330) |
| P76 | Change layer opacity with Advanced Blending on another layer | ≤ 40 ms p95 | 6.32 | 7.55 | 7.55 | 479 MB | 8 MB | – | tracked | [#6689](https://github.com/storytold/photocraft/issues/6689) |
| P77 | Toggle an adjustment layer's visibility | ≤ 10 ms p95 | 6.12 | 8.30 | 8.30 | 488 MB | 107 MB | – | tracked | [#6535](https://github.com/storytold/photocraft/issues/6535) |
| P78 | Hide the top adjustment layer among 150 full-canvas layers, 6 MP, GPU budget forced to 512 MB (CPU fallback) | ≤ 30 ms p95 | 0.43 | 0.47 | 0.47 | 664 MB | 96 MB | – | tracked | [#6533](https://github.com/storytold/photocraft/issues/6533) |
| P79 | Zoomed-out reduced composite of a 30000x30000 document with one painted layer (#9330 target: 60000x60000) | track only | 38.6 | 38.6 | 38.6 | 739 MB | – | – | tracked | [#1015](https://github.com/storytold/photocraft/issues/1015) |
| P80 | App frame: full CPU refresh of a 24 MP document | ≤ 50 ms p95 | 22.1 | 31.1 | 31.1 | 659 MB | 211 MB | – | tracked | [#9328](https://github.com/storytold/photocraft/issues/9328) |
| P81 | Undo a brush dab on a full-canvas 16-bit 15000 x 10000 layer + refresh | track only | 0.69 | 0.72 | 0.72 | 697 MB | 205 MB | – | tracked | [#9329](https://github.com/storytold/photocraft/issues/9329) |
| P82 | Fill a 2 % selection on a full-canvas 24 MP layer + refresh | track only | 0.52 | 0.58 | 0.58 | 697 MB | 160 MB | – | tracked | [#9329](https://github.com/storytold/photocraft/issues/9329) |

**Not measurable yet** (the code can't do it yet; no number is recorded):

| Id | Scenario | Target | Why | Issue |
|---|---|---|---|---|
| P15 | Zoom / pan frame time on a 15000×10000 16-bit document | ≤ 16 ms per frame | no headless canvas frame harness yet (zoom and pan sample the GPU texture in the egui paint callback) | [#209](https://github.com/storytold/photocraft/issues/209) |
| P23 | Warp / Puppet / Perspective preview at 4K | ≤ 16 ms per frame, commit in the background | the previews run inside the UI tools; no headless frame harness, no background commit | [#210](https://github.com/storytold/photocraft/issues/210) |
| P34 | Brush preview memory, small dab on an 8K viewport | ≤ 2 MiB | the live brush preview buffers are UI-side; no headless counter yet | [#211](https://github.com/storytold/photocraft/issues/211) |
| P35 | Marquee drag on 24 MP with Alt/Shift | ≤ 17 ms p95 | Shift/Alt marquee modifiers don't exist yet (#208) and the drag preview is UI-side | [#211](https://github.com/storytold/photocraft/issues/211) |
