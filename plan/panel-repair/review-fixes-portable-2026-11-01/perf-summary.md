## Performance (quick run)

- Machine: AMD64 Family 25 Model 33 Stepping 2, AuthenticAMD (12 cores, ?), GPU NVIDIA GeForce RTX 3060, Microsoft Windows [Version 10.0.19045.6456] x86_64; class `windows-x86-64-amd64-family-25-model-33-stepping-2-authenticamd-nvidia-geforce-rtx-3060`
- Commit adaae9cd48832486b268fbfd2f79e85cd3b6ed6d, 2026-10-31T22:56:07Z
- Load average (1/5/15 min): n/a at start, n/a at end
- baseline is from machine class `macos-aarch64-apple-m4-pro-apple-m4-pro`, this is `windows-x86-64-amd64-family-25-model-33-stepping-2-authenticamd-nvidia-geforce-rtx-3060`: regression check skipped
- Quick mode: small documents, budgets not applied (they are set for full-size documents).
- Bench `bench_filters2`: ok, 1 s, load n/a
- Bench `bench_multiband`: ok, 0 s, load n/a
- Bench `bevel_bench`: ok, 4 s, load n/a
- Bench `camera_raw_bench`: ok, 1 s, load n/a
- Bench `layout_bench`: ok, 77 s, load n/a
- Bench `perf_scenarios`: ok, 16 s, load n/a
- Bench `perf_scenarios_cpu`: ok, 4 s, load n/a
- Bench `type_bench`: ok, 1 s, load n/a

| Id | Scenario | Target | p50 ms | p95 ms | max ms | Peak RSS | GPU | vs baseline | Status | Issue |
|---|---|---|---:|---:|---:|---:|---:|---:|---|---|
| P1 | Move a layer with layer styles (per drag update) | ≤ 25 ms p95 | 5.61 | 6.84 | 6.84 | 384 MB | 75 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P2 | Change layer opacity | ≤ 20 ms p95 | 3.55 | 4.03 | 4.03 | 387 MB | 75 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P3 | Change layer fill | ≤ 20 ms p95 | 3.58 | 4.10 | 4.10 | 386 MB | 75 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P4 | Change blend mode | ≤ 20 ms p95 | 3.87 | 4.16 | 4.16 | 386 MB | 75 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P5 | Toggle visibility | ≤ 10 ms p95 | 3.49 | 3.52 | 3.52 | 386 MB | 75 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P6 | Undo a move | ≤ 25 ms p95 | 4.82 | 5.32 | 5.32 | 390 MB | 75 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P7 | Redo a property change | ≤ 25 ms p95 | 3.93 | 4.50 | 4.50 | 388 MB | 75 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P8 | Duplicate a 12 MP layer (first) | ≤ 100 ms p95 | 6.05 | 6.48 | 6.48 | 392 MB | 167 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P9 | Duplicate a 12 MP layer (repeat) | ≤ 20 ms p95 | 4.96 | 5.54 | 5.54 | 392 MB | 167 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P10 | Paste a 12 MP layer (first) | ≤ 100 ms p95 | 6.12 | 6.96 | 6.96 | 423 MB | 227 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P11 | Paste a 12 MP layer (repeat) | ≤ 20 ms p95 | 7.43 | 8.55 | 8.55 | 422 MB | 227 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P12 | Arrow-key nudge in a 150-layer document | ≤ 30 ms p95 | 1.82 | 8.58 | 8.58 | 430 MB | 71 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P51 | New layer in a 150-layer document | ≤ 16 ms p95 | 0.58 | 0.68 | 0.68 | 378 MB | 71 MB | – | tracked | [#1771](https://github.com/storytold/photocraft/issues/1771) |
| P13 | Brush dab on a 15000×10000 16-bit document | ≤ 80 ms p95 | 1.18 | 8.65 | 8.65 | 421 MB | 176 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P14 | Move a layer on a 15000×10000 16-bit document | ≤ 80 ms p95 | 3.05 | 3.92 | 3.92 | 454 MB | 176 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P16 | Brush dab on a 32-bit document with 20 layers | ≤ 100 ms p95 | 1.93 | 2.22 | 2.22 | 524 MB | 121 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P17 | Move a layer on a 32-bit document with 20 layers | ≤ 100 ms p95 | 3.66 | 4.29 | 4.29 | 573 MB | 121 MB | – | tracked | [#209](https://github.com/storytold/photocraft/issues/209) |
| P18 | Open a 20 MP layered PSD: first pixels (today: fully opened) | ≤ 1000 ms p95 | 92.9 | 97.6 | 97.6 | 540 MB | 279 MB | – | tracked | [#210](https://github.com/storytold/photocraft/issues/210) |
| P19 | Open a 20 MP layered PSD: editable | ≤ 3000 ms p95 | 92.9 | 97.6 | 97.6 | 540 MB | 279 MB | – | tracked | [#210](https://github.com/storytold/photocraft/issues/210) |
| P20 | Open a 2 GB PSD: editable | opens with progress, editable, never blank | – | – | – | – | – | – | not run | [#210](https://github.com/storytold/photocraft/issues/210) |
| P63 | Open a 4–5 GB PSB: editable | opens with progress, editable, never blank | – | – | – | – | – | – | not run | [#210](https://github.com/storytold/photocraft/issues/210) |
| P21 | Content-Aware Fill on 10 MP | ≤ 1500 ms p95 | 115 | 121 | 121 | 567 MB | 270 MB | – | tracked | [#210](https://github.com/storytold/photocraft/issues/210) |
| P22 | Spot Healing stroke on 10 MP | ≤ 500 ms p95 | 38.9 | 44.5 | 44.5 | 561 MB | 216 MB | – | tracked | [#210](https://github.com/storytold/photocraft/issues/210) |
| P24 | Import 500 brushes (longest UI-thread step) | ≤ 100 ms max | 1.48 | 1.88 | 1.88 | 531 MB | 211 MB | – | tracked | [#210](https://github.com/storytold/photocraft/issues/210) |
| P25 | Cancel a Gaussian Blur job on 24 MP (until the worker exits) | ≤ 200 ms p95 | 0.35 | 0.57 | 0.57 | 627 MB | 211 MB | – | tracked | [#210](https://github.com/storytold/photocraft/issues/210) |
| P49 | Cancel a Content-Aware Fill job on 24 MP (until the worker exits) | ≤ 200 ms max | 1.39 | 4.19 | 4.19 | 541 MB | 211 MB | – | tracked | [#210](https://github.com/storytold/photocraft/issues/210) |
| P50 | App frame time while a 24 MP Gaussian Blur job runs | ≤ 16 ms p95 | 1.09 | 4.62 | 13.9 | 582 MB | 211 MB | – | tracked | [#210](https://github.com/storytold/photocraft/issues/210) |
| P26 | Select › Modify › Smooth on 24 MP (radius 50) | ≤ 100 ms p95 | 2.90 | 3.09 | 3.09 | 390 MB | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P27 | Select › Modify › Feather on 24 MP (radius 50) | ≤ 100 ms p95 | 5.10 | 5.36 | 5.36 | 405 MB | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P28 | Content-Aware Scale 24 MP (to 90 % width) | ≤ 3000 ms p95 | 70.3 | 70.3 | 70.3 | 464 MB | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P29 | Select Subject on 24 MP, repeated | ≤ 100 ms p95 | 0.35 | 0.35 | 0.35 | 410 MB | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P30 | Liquify 800 px brush on 3500×2200 at full resolution | ≤ 1 ms per update | 4.57 | 4.88 | 4.88 | 418 MB | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P31 | Camera Raw exposure change (proxy) | ≤ 10 ms | 8.01 | 9.06 | 9.06 | – | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P32 | Brush release on a long stroke | ≤ 16 ms (no hitch at mouse-up) | 0.87 | 0.95 | 0.95 | 433 MB | 93 MB | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P33 | Brush dab on A4 300 ppi CMYK (dab to screen) | ≤ 6 ms p95 | 1.14 | 6.30 | 6.30 | 408 MB | 86 MB | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P36 | Camera Raw exposure change with all SDR scopes (CPU) | ≤ 10 ms p95 | 14.3 | 14.9 | 14.9 | – | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P40 | Brush dab 60 px on 36 MP | track only | – | – | – | – | – | – | not run |  |
| P41 | Gaussian Blur r 40 on 36 MP | track only | – | – | – | – | – | – | not run |  |
| P42 | Curves dialog change, layer preview, 36 MP | track only | – | – | – | – | – | – | not run |  |
| P43 | Save .psd, 36 MP, 3 layers | track only | – | – | – | – | – | – | not run |  |
| P44 | Open .psd, 36 MP, 3 layers | track only | – | – | – | – | – | – | not run |  |
| P45 | Full refresh with layer effects, warm caches, 36 MP (GPU) | track only | – | – | – | – | – | – | not run |  |
| P46 | Brush dab on a layer with effects, 36 MP (GPU) | track only | – | – | – | – | – | – | not run |  |
| P47 | Font-size drag step, 50 type layers | track only | 2.57 | 3.06 | 3.06 | 60 MB | – | – | tracked |  |
| P48 | Full refresh of a 14000×14000 document | track only | – | – | – | – | – | – | not run |  |
| P52 | Chisel bevel size change, 12 MP ellipse, size 8 (GPU) | track only | 23.9 | 25.6 | 25.6 | 361 MB | – | – | tracked |  |
| P53 | Chisel bevel size change, 12 MP ellipse, size 50 (GPU) | track only | 32.6 | 41.1 | 41.1 | 337 MB | – | – | tracked |  |
| P54 | Chisel bevel size change, 12 MP ellipse, size 250 (GPU) | track only | 73.7 | 74.9 | 74.9 | 416 MB | – | – | tracked |  |
| P55 | Chisel bevel size change, 12 MP text paragraph, size 8 (GPU) | track only | 30.6 | 32.6 | 32.6 | 450 MB | – | – | tracked |  |
| P56 | Chisel bevel size change, 12 MP text paragraph, size 50 (GPU) | track only | 33.5 | 33.6 | 33.6 | 486 MB | – | – | tracked |  |
| P57 | Chisel bevel size change, 12 MP text paragraph, size 250 (GPU) | track only | 64.7 | 67.8 | 67.8 | 560 MB | – | – | tracked |  |
| P58 | Chisel bevel size change, 12 MP ellipse, size 8 (CPU) | track only | 41.4 | 42.5 | 42.5 | 361 MB | – | – | tracked |  |
| P59 | Chisel bevel size change, 12 MP text paragraph, size 8 (CPU) | track only | 51.3 | 56.0 | 56.0 | 450 MB | – | – | tracked |  |
| P60 | Layer opacity among 150 full-canvas layers, 6 MP (app GPU budget) | ≤ 30 ms p95 | 1.11 | 7.29 | 7.29 | 472 MB | 96 MB | – | tracked | [#5973](https://github.com/storytold/photocraft/issues/5973) |
| P61 | Hide a layer among 150 full-canvas layers, 6 MP (app GPU budget) | ≤ 30 ms p95 | 0.86 | 0.96 | 0.96 | 472 MB | 96 MB | – | tracked | [#5973](https://github.com/storytold/photocraft/issues/5973) |
| P62 | File > New 10 x 5 m at 200 ppi (3.1 GP) + first reduced canvas refresh | track only | 34.5 | 34.8 | 34.8 | 516 MB | – | – | tracked | [#4017](https://github.com/storytold/photocraft/issues/4017) |
| P64 | Oil Paint on 24 MP | ≤ 1000 ms p95 | 185 | 185 | 185 | – | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P65 | Smart Blur r 12 on 24 MP (High quality) | ≤ 1000 ms p95 | 218 | 218 | 218 | – | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P66 | Relight on 24 MP | ≤ 1000 ms p95 | 52.9 | 52.9 | 52.9 | – | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P67 | Reduce Noise on 24 MP | ≤ 1000 ms p95 | 56.4 | 56.4 | 56.4 | – | – | – | tracked | [#211](https://github.com/storytold/photocraft/issues/211) |
| P68 | Photomerge multi-band blend, synthetic | track timing and peak RSS; no calibrated performance budget | 15.5 | 15.7 | 15.7 | 36 MB | – | – | tracked | [#7758](https://github.com/storytold/photocraft/issues/7758) |
| P69 | Move a layer with layer styles, CPU compositor | track only | 17.7 | 18.7 | 18.7 | 97 MB | – | – | tracked | [#9330](https://github.com/storytold/photocraft/issues/9330) |
| P70 | Change layer opacity, CPU compositor | ≤ 40 ms p95 | 5.48 | 6.30 | 6.30 | 120 MB | – | – | tracked | [#9330](https://github.com/storytold/photocraft/issues/9330) |
| P71 | Change layer fill, CPU compositor | ≤ 40 ms p95 | 5.90 | 6.25 | 6.25 | 119 MB | – | – | tracked | [#9330](https://github.com/storytold/photocraft/issues/9330) |
| P72 | Change blend mode, CPU compositor | ≤ 40 ms p95 | 5.55 | 5.84 | 5.84 | 120 MB | – | – | tracked | [#9330](https://github.com/storytold/photocraft/issues/9330) |
| P73 | Toggle visibility, CPU compositor | ≤ 20 ms p95 | 4.35 | 5.94 | 5.94 | 120 MB | – | – | tracked | [#9330](https://github.com/storytold/photocraft/issues/9330) |
| P74 | Undo a move, CPU compositor | track only | 5.95 | 6.91 | 6.91 | 137 MB | – | – | tracked | [#9330](https://github.com/storytold/photocraft/issues/9330) |
| P75 | Redo an opacity change, CPU compositor | track only | 5.56 | 6.04 | 6.04 | 138 MB | – | – | tracked | [#9330](https://github.com/storytold/photocraft/issues/9330) |
| P76 | Change layer opacity with Advanced Blending on another layer | ≤ 40 ms p95 | 8.96 | 9.76 | 9.76 | 377 MB | 8 MB | – | tracked | [#6689](https://github.com/storytold/photocraft/issues/6689) |
| P77 | Toggle an adjustment layer's visibility | ≤ 10 ms p95 | 5.96 | 6.32 | 6.32 | 362 MB | 107 MB | – | tracked | [#6535](https://github.com/storytold/photocraft/issues/6535) |
| P78 | Hide the top adjustment layer among 150 full-canvas layers, 6 MP, GPU budget forced to 512 MB (CPU fallback) | ≤ 30 ms p95 | 0.62 | 0.70 | 0.70 | 472 MB | 96 MB | – | tracked | [#6533](https://github.com/storytold/photocraft/issues/6533) |
| P79 | Zoomed-out reduced composite of a 30000x30000 document with one painted layer (#9330 target: 60000x60000) | track only | 46.4 | 46.4 | 46.4 | 650 MB | – | – | tracked | [#1015](https://github.com/storytold/photocraft/issues/1015) |
| P80 | App frame: full CPU refresh of a 24 MP document | ≤ 50 ms p95 | 24.5 | 32.6 | 32.6 | 602 MB | 211 MB | – | tracked | [#9328](https://github.com/storytold/photocraft/issues/9328) |
| P81 | Undo a brush dab on a full-canvas 16-bit 15000 x 10000 layer + refresh | track only | 0.71 | 0.82 | 0.82 | 485 MB | 205 MB | – | tracked | [#9329](https://github.com/storytold/photocraft/issues/9329) |
| P82 | Fill a 2 % selection on a full-canvas 24 MP layer + refresh | track only | 0.57 | 1.24 | 1.24 | 485 MB | 160 MB | – | tracked | [#9329](https://github.com/storytold/photocraft/issues/9329) |

**Not measurable yet** (the code can't do it yet; no number is recorded):

| Id | Scenario | Target | Why | Issue |
|---|---|---|---|---|
| P15 | Zoom / pan frame time on a 15000×10000 16-bit document | ≤ 16 ms per frame | no headless canvas frame harness yet (zoom and pan sample the GPU texture in the egui paint callback) | [#209](https://github.com/storytold/photocraft/issues/209) |
| P23 | Warp / Puppet / Perspective preview at 4K | ≤ 16 ms per frame, commit in the background | the previews run inside the UI tools; no headless frame harness, no background commit | [#210](https://github.com/storytold/photocraft/issues/210) |
| P34 | Brush preview memory, small dab on an 8K viewport | ≤ 2 MiB | the live brush preview buffers are UI-side; no headless counter yet | [#211](https://github.com/storytold/photocraft/issues/211) |
| P35 | Marquee drag on 24 MP with Alt/Shift | ≤ 17 ms p95 | Shift/Alt marquee modifiers don't exist yet (#208) and the drag preview is UI-side | [#211](https://github.com/storytold/photocraft/issues/211) |
