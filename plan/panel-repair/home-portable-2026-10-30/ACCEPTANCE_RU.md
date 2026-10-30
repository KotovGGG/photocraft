# Приёмка восстановленной ветки — 2026-10-30

Ветка: `codex/panel-layout-upstream`. Upstream: `b1cfff9d30298eea4f446a8f6a5e4285cb43c6e7`.
Пять конфликтов объединены по существу; shared Workspace, vendor snapshot и ревизии
craft-ui/egui сохранены. Source commit пакета указан в `manifest.json`.
Windows / Rust MSVC 1.95.0. Основной продуктовый EXE агент не собирал и не запускал.

## Подтверждено на объединённом коде

| Проверка | Результат |
|---|---|
| Panel docking | 136 passed, 0 failed, 2 opt-in benchmarks ignored |
| Dependency contract / dock / workspace / Tools / type flyouts / visibility / overflow | Все относящиеся фильтры прошли; в том числе новый upstream screen-mode test |
| Engine, lib + tests | 2762 passed, 0 failed, 22 ignored, 12 test targets |
| `panic_hunt --ignored` | 1 passed |
| Workspace integration | 9 passed |
| Shared docking | 346 passed; optional fixtures из immutable 92d392c, вне Git |
| fmt / layers | Прошли; 31 crate без нарушения слоёв |
| wasm | 24 crates + codecs/heif прошли; UI source path в логе — F:/photocraft |
| parity / scorecard | Перегенерированы; 11 неиспользуемых настроек из 182 |
| UI/engine doctest check | Команда прошла; 0 doc examples в обоих crates |
| Shared Clippy | Прошёл |
| PR diff whitespace check | Прошёл относительно upstream/main |
| Новая offscreen-матрица | 570 PNG: 132 final, 120 seam, 72 corner, 230 audit, 16 port |
| Физические швы / replay / GIF | 72 pixel assertions; 515 replay PNG; 15 новых GIF |
| Неизменность проверяемого кода | Совпали SHA 1267 исходных файлов до/после прогонов |

Просмотрены новые transition/theme и DPI montage, raw full join/detach, collapsed
bar, problem-ru-125, mixed seam и corner hover. Все кадры — новый offscreen egui/WGPU
прогон. Они не являются native desktop capture или измерением FPS/GPU latency.
Два after PNG в docs обновлены; before PNG сохранены как исторические свидетельства.
Старые CPU timings относятся только к прежнему checkpoint; новых timing claims нет.

## Незелёные проверки

Полный UI **library** run: `4460 passed; 95 failed; 23 ignored` (exit 101).
92 имени совпадают с историческим списком; это НЕ новый независимый полный baseline
нынешнего upstream. Ещё 3 — неизменённые upstream `selected_fonts_commit_pattern_0/2/3`:
ArrowDown+Enter выбирает установленный Inter Hewn вместо ожидаемого Inter.
Probe рисует Character/options без docking; наличие Inter-Bold-Hewn подтверждено
реестром шрифтов этого ПК. Шрифты и текстовый код не менялись.
Списки и конкретные assertion errors сохранены в `full-ui-classification.json` и логе.
Полный workspace suite не запускался и не объявляется зелёным.

Стандартный UI/engine all-targets Clippy (exit 101) остановился на
`text/src/psd_path.rs:157` (`overly_complex_bool_expr`). Дополнительные прогоны
с `--no-deps` для уточнения охвата также НЕ зелёные:

- `engine/src/crop_fill.rs:78`: nonminimal_bool;
- `ui-egui/src/canvas/strokes.rs:495,500`: collapsible_match;
- `ui-egui/src/dialogs/vp_ui.rs:989`: nonminimal_bool;
- `ui-egui/src/widgets/text_field.rs:29`: collapsible_match;
- `ui-egui/src/dialogs/color_picker_ui/tests.rs:130`: manual_range_contains.

Все шесть файлов с семью диагностическими точками по Git diff совпадают
с upstream/main. Это не исправлялось через unrelated text/PSD/painting изменения
или подавление lint/CI. Подтверждение — `upstream-lint-provenance.json`.
Strict UI/engine Clippy остаётся непройденным; shared Clippy прошёл отдельно.

## Остаётся пользователю / перед Ready for review

Собрать основной EXE по README_RU.md и проверить реальные жесты на своём профиле,
focus/IME, физические мониторы, mixed DPI и GPU stalls. User profiles и старый
D:/photocraft не сбрасывались. Эти пункты не закрываются offscreen-кадрами.
Учесть документированные upstream Clippy/UI failures перед переводом PR в Ready.
PR #10322 остаётся draft; второй PR не создавался, merge PR не выполнялся.

В diff относительно upstream нет наших ATN/PSD/action-name/text, CI и чужих credits.
Новые собственные коммиты — KotovGGG. Исходный архив и его 23 SHA-записи сохранены.
