# Финальная приёмка ремонта панелей — 2026-10-30

Worktree:C:/Users/pavel/.codex/worktrees/panel-layout-upstream/photocraft.
Ветка:codex/panel-layout-upstream. Base:382b047c30483024159aaa63831947bc99a5e28b.
Автор:@KotovGGG. Последнее поручение разрешает создание PR после двух исправлений.
Предыдущие архивы не использованы; основной exe не строился и не запускался.
Исходники и профиль D:/photocraft не менялись, использован согласованный общий target.

## Два последних исправления

1. Передаётся высота видимого полного источника, а не только его ширина. Принимающий
короткий float увеличивается до max своей и входящей высоты. Normal sizes сохраняются
перед структурными переносами; после отрыва Color возвращается с прежней высотой.
2. Корневые top/bottom tab groups сворачиваются на месте через существующие collapse
flags. Закрытая группа остаётся26pt строкой. Fitted header observer даёт реальные slots
до/между/после вкладок даже без body callback. Вставка наследует закрытое состояние
принимающей строки, повторное раскрытие/сворачивание и restore сохраняют прикрепление.

Три регрессии воспроизведены до правок:before-tests.log (3 failed). После правок136
панельных тестов прошли; height join/detach проверены также для80pt mini receiver,
400/520pt полного источника, всех tab slots и обоих горизонтальных краёв.

## Гейты на текущем коде

- 136 panel tests passed (two opt-in benchmarks ignored in the regular filter); dependency contract and related docking/workspace/Tools/visibility/overflow filters passed.
- 2711 engine tests passed; adversarial command `panic_hunt` passed separately.
- 346 shared docking tests passed with the documented optional test inputs.
- Formatting, UI/engine all-targets Clippy, shared-library Clippy, engine/UI doctest checks, 31-crate layer check, 24-crate wasm plus codecs/heif, and parity/scorecard regeneration passed.
- 570 offscreen matrix PNGs across three Pro themes and 100/125/150/200% scale, including the sanitized problem layout, plus 515 replay frames; 72 physical-pixel seam checks passed.
- Five scoped CPU hover/drag runs completed; reproduction and results are in [validation notes](https://github.com/KotovGGG/photocraft/blob/COMMIT/docs/panel-docking-validation.md).
- The full UI run is **not green**: 92 failures. 92 match independently recorded historical baseline failures; 0 do not match that record. This is separate from the passing panel suite.

Доктесты UI/engine проверены отдельно:doc-tests.log/doc-tests.exit. В results.json
отражены коды основного конвейера; полный UI suite намеренно не объявляется зелёным.
Полные summaries:test result: FAILED. 4303 passed; 92 failed; 21 ignored; 0 measured; 0 filtered out; finished in 221.62s
Полный список failed/baseline matches — full-ui-classification.json; историческое
сопоставление не является новым полным прогоном нынешнего upstream main.

Изолированный xtask собран вtarget/panel-repair-xtask-c-worktree. Его compile-time
root — C-worktree, wasm.log явно проверяет текущий UI0.17.0 из C:/Users/pavel/… .
Gate-root.json содержит SHA helper. Shared top-level xtask.exe для приёмки не принят.
Прежние панельные и завершённые engine test exe/PDB перемещены в локальный build-artifacts
с проверкой SHA, чтобы освободить место; исходники/профиль старого fork не затронуты.

## Визуальная матрица (offscreen)

Все текущие кадры относятся к этому source fingerprint. Основные PNG просматриваются
при100/125/150/200%,Pro/ProMedium/ProLight; RU problem125 дополнительно. Результат
«пройдено» здесь означает egui/WGPU + pointer replay, а не физический desktop.

| Сценарий | Результат и свидетельство |
|---|---|
| Floating compact1/2/5 | Пройдено:audit-captures/Pro-1.25-floating-1/2/5.png |
| Attached left/rightInner/rightOuter, соседние колонки | Пройдено:seam-captures/pro-1.25-Left-left/rightInner/rightOuter.png, replay09-right-* |
| Hover швов и уход | Пройдено:audit-captures/Pro-1.25-hover-seam-actions/history/layers.png, hover-away.png |
| Пустая шапка,arrow/menu/X,промежутки | Пройдено:empty-header-hover.png, corner-captures/*-idle/expand/close.png, pointer cursor assertions |
| Icon click/repeat,adjacent flyout | Пройдено:replay01-group-flyout-tearoff и02-insert-redock; linked behavioral tests |
| Chevron collapse/expand,порядок/heights | Пройдено:seam-captures/*-mixed-expanded/collapsed-again.png и final-review-captures/*-top-tabs-* |
| Flyout left/right/floating | Пройдено:audit-captures/*-adjacent-left/rightInner.png,seam-captures/*-Left-floating/rightOuter.png |
| Full float/stack | Пройдено:replay03-expanded-stack-resize; final-review-captures/*-full-joined-to-mini/full-detached.png |
| Detach одного/группы | Пройдено:replay01/02 и final full-detached; размеры и соседние части проверены отдельно |
| Вставка top/middle/bottom и tab slots | Пройдено:replay01/02; final *-top-added-tab/top-between-preview/top-between-inserted.png |
| Правые границы pointer drop | Пройдено:replay09-right-full/compact-inner/outer; корректный fitted marker |
| Attached left↔right | Пройдено:replay09 и gesture tests; не требуется промежуточный ручной float |
| Attached resize intermediate/release/Escape | Пройдено:audit *-resize-30/60/90/released.png,replay03/06 |
| Compact width min→labels→max→min | Пройдено:replay05-compact-width; icon anchor assertions |
| Width float/dock/close/restore | Пройдено:replay07-workspace-restore; presentation width ownership tests |
| Whole Tools detach/2-axis resize | Пройдено:replay04-whole-tools, toolbar filters; отдельные инструменты не отделяются |
| Tab/Shift+Tab/auto-show/auto-collapse | Пройдено:replay08-visibility-preferences и related visibility filters |
| Keyboard focus | Пройдено:shared docking + host focus tests; mouse hover пустой шапки не создаёт focus outline |
| Problem layout/narrow/restore | Пройдено:audit-captures/problem-ru-125.png,*-narrow.png,*-restored.png |
| Themes/DPI и physical seams | Пройдено:570 PNG,72 seam assertions; final-transition-review.png/final-dpi-review.png |
| Synthetic document/no click-through | Пройдено:audit *-document.png;515 replay frames assert history unchanged |
| Height full→short mini→detach | Пройдено:132 final PNG +новые regressions; docs/images/panel-repair/full-height-after.png |
| Horizontal collapsed tab bar | Пройдено:132 final PNG, before/between/after slots и top/bottom restore; top-collapse-after.png |
| Native focus/IME/monitor/mixed-DPI | Открыто:старый Windows capture дал FrameArrived timed out; пользователь собирает desktop exe |

Просмотрены final-transition-review.png (33 состояния), final-dpi-review.png,
raw Pro125 full-join/top-recollapse, corner42-hover, mixed-seam, problem-ru125
и resize60. Реплеи и GIF — текущие offscreen captures; GIF display timing не
является измерением производительности. Итог:132+120+72+230+16=570 PNG матриц,
13 pointer replay/515 кадров,15 GIF (13 replay+2 новых последовательности).

## Активные CPU кадры

Приняты пять повторных прогонов после окончания компиляции/тестов/кодирования.
Первые прогоны конвейера пересеклись с отдельной компиляцией доктестов и отвергнуты
для timing acceptance; сохранены как active-during-doc-compile-*.log.
Полный UI1280×800,125%,без документа/GPU;600 измеренных кадров/фаза/прогон после40
warmup,9000 кадров суммарно. Медианы per-run percentiles,мс; max всех пяти:

| Фаза | p50 | p95 | p99 | max |
|---|---:|---:|---:|---:|
| idle | 2.373 | 3.426 | 3.846 | 10.357 |
| hover | 2.260 | 3.032 | 3.587 | 10.600 |
| drag | 2.475 | 3.561 | 4.999 | 9.480 |

Это текущий scoped CPU replay; нового before/after сравнения этого этапа нет.
Это не native GPU/FPS. Реальные GPU/OS stalls измерением не исключаются.

## Upstream и область PR

Объединён origin/main382b047c3: app-specific pretend versions/craft-update04aa1703,
CI/test runtime upstream. Shared UI92d392c и egui6d518fc не изменились. Только doc
conflicts объединены вручную; Rust conflicts не было. PR diff относительно main
не содержит CI,contributors,ATN/PSD/action-name/text или чужих изменений.
Vendor snapshot явный:6 изменённых Rust files относительно immutable92d392c,
остальная библиотека — исходный pin. Контракт ревизий, metrics boundary и fallback
добавляют контролируемую точку адаптации, а не обещают совместимость с любым API.
Нет неигнорируемых font binaries. Сохранены X half=5.0*scale+0.35, whole Tools,
обычный layer selection без Properties auto-open, adjustment/fill reveal.

Source-fingerprint.json подтверждает неизменность122 core files во время гейтов
и SHA текущего тестового exe; capture-manifest.json — SHA всех PNG/метаданных.
Свежий пакет/patch/описание и демонстрации собираются после этой приёмки, без
повторного использования старого proposal.zip. PR создаётся от @KotovGGG, без merge.
