# Продолжение ремонта PhotoCraft дома

Исходники уже отправлены в fork @KotovGGG. Рабочая ветка: `codex/panel-layout-upstream`.
Коммит исходников/демонстраций: `cd571efe41c556347b1851ac208e3388acc3002e`. PR: https://github.com/storytold/photocraft/pull/10322
Эта отдельная ветка `codex/panel-layout-handoff-2026-10-30` сохраняет большие материалы; они не входят в upstream PR.

## Важно: после checkpoint появился новый большой upstream

Проверенный код остаётся cd571efe4 на базе382b047c3. После открытия PR в main вошёл
b1cfff9d3 (PR10204):380 файлов,включая UI/engine. Он НЕ объединён с проверенным
snapshot. Read-only merge-tree обнаружил5 конфликтов:

- crates/ui-egui/src/lib.rs
- crates/ui-egui/src/panels/toolbar.rs
- docs/control-protocol.md
- docs/scorecard.md
- docs/ui-parity.md

PR10322 переведён в draft. На текущем рабочем дереве реальный merge не начинался,
никаких конфликтных маркеров в исходниках нет. Сначала дома объедините актуальный
upstream с codex/panel-layout-upstream, сохранив обе стороны нужных правок; затем
повторите относящиеся к панелям гейты и визуальную матрицу на объединённой версии.
Дальше выполните живую native проверку. Старые136/346/2711 и570+515 кадров относятся
к cd571efe4/382b047c3 и НЕ доказывают корректность ещё не объединённого b1cfff9d3.
Пины craft-ui92d392c/egui6d518fc в новом main не сменились,но этого недостаточно
для заявления о совместимости нового UI. Большой upstream нельзя переносить из
старого грязного D:/photocraft или выдавать за наши ATN/PSD/CI изменения.

## Получить на другом компьютере

```powershell
git clone --branch codex/panel-layout-upstream https://github.com/KotovGGG/photocraft.git
cd photocraft
git restore --source origin/codex/panel-layout-handoff-2026-10-30 --worktree -- plan/panel-repair/portable-2026-10-30
```

Последняя команда восстанавливает материалы в локальную gitignored папку `plan/`,
не меняет рабочую ветку и не добавляет архивы в индекс PR. Можно также скачать
нужные ZIP прямо из этой папки на GitHub через Download raw file.

Распакуйте PR-пакет `photocraft-panel-repair-2026-10-30-final.zip`: там описание,
полный binary patch относительно upstream382b047c3, приёмка, логи, четыре before/after
PNG,15 GIF (13 pointer replay +2 последних перехода),132 финальных PNG с fitted JSON,
лицензии и SHA manifest. Остальные архивы содержат ВСЕ исходные кадры этого прогона:
570 PNG матриц и515 replay PNG. ZIP по семействам нужно распаковать в одну папку;
пути совпадут с `capture-manifest.json`. Manifest этого checkpoint проверяет ZIP-файлы.
Original-audit ZIP сохраняет исходный PLAN,7 картинок,problem layout и последующие UI
скриншоты пользователя. Старые указания об отсрочке PR в аудите исторические: пользователь
разрешил PR и push; PR уже создан. Исправления не переносятся из старого D:/photocraft.

## Текущее состояние

Два последних дефекта исправлены: full float не сжимается до высоты короткой mini при
соединении и сохраняет размер после отрыва; top/bottom collapsed группа остаётся
прикреплённой строкой вкладок, корректно раскрывается/сворачивается и принимает вкладки
до/между/после существующих. Предыдущие одобренные исправления сохранены.

136 panel +346 shared docking tests прошли;2711 engine tests и panic_hunt прошли;
Clippy UI/engine all-targets/shared,fmt,layers31,wasm24+heif,parity/scorecard,doc checks
прошли.9 workspace integration tests прошли отдельно. Полный UI:4303 passed,92 failed,
21 ignored. Все92 совпали с независимо зафиксированными историческими baseline failures;
нового полного baseline нынешнего main нет. Полный UI suite не объявлен зелёным.
570 matrix PNG,72 pixel seam assertions,515 replay frames; новые снимки просмотрены.
CPU scoped benchmark приведён в ACCEPTANCE_RU.md, без обещаний native FPS/GPU latency.

## Что остаётся дома

Основной EXE собирает пользователь. Живой Windows capture ранее дал timeout,
поэтому physical monitor/mixed-DPI/IME и реальные GPU stalls остаются непроверенными.
Соберите эту ветку и проверьте текущую desktop-версию на своей раскладке. При новом
дефекте добавьте точное воспроизведение/pointer regression и обновите кадры. Все новые
исправления коммитьте и push в `codex/panel-layout-upstream`: существующий PR обновится.
Не merge PR автоматически. Не считайте старый proposal.zip актуальным пакетом.

Не менять старый грязный fork/профиль D:/photocraft, ATN/PSD/action names/texts,CI или
чужие изменения. Авторство только @KotovGGG. X half=5.0*scale+0.35; обычный layer selection
не открывает Properties, adjustment/fill reveal сохраняется. Tools отделяется целиком.
Независимые компактные части не сворачивают соседей; левая часть раскрывается наружу.

## Проверки на новом компьютере

Прочитайте репозиторный AGENTS.md, docs/panel-docking-contract.md и ACCEPTANCE_RU.md.
Установите обычный Rust/native toolchain по docs/development.md. Не копируйте старые
target-каталоги. Локальный shared craft-ui snapshot уже в Git; font binaries не добавлялись.

```powershell
$env:CARGO_BUILD_JOBS='1'
$env:CARGO_TARGET_DIR="$PWD/target"
cargo test -p photocraft-ui-egui --lib panel_docking -- --nocapture
$env:PHOTOCRAFT_FINAL_REVIEW_CAPTURES="$PWD/plan/final-review-captures"
cargo test -p photocraft-ui-egui --lib capture_final_review_transitions -- --nocapture
```

Полные необходимые гейты — по AGENTS.md. Optional shared-crate test fonts/fixtures
восстанавливаются из immutable92d392c по vendor/craft-ui/PATCH.md, они не коммитятся.
Служебный xtask при shared target между checkout должен иметь отдельный target:
его compile-time root важен. Скрипты в отдельном ZIP — материалы предыдущего прогона;
в finish-pr.py/summarize-pr.py есть пути C:/Users/pavel и D:/photocraft, на другом ПК
их нужно адаптировать перед запуском. Обычные Cargo-команды выше переносимы.

## Запрос следующему агенту

Продолжи ремонт панелей PhotoCraft0.17.0 в ветке codex/panel-layout-upstream.
Сначала прочитай AGENTS.md, текущий ACCEPTANCE_RU.md, docs/panel-docking-contract.md,
original-audit/PLAN_RU.md из архива и evidence. Исправления и визуальная матрица уже
сделаны; PR10322 открыт. Не начинай перенос старого форка заново. Сначала объедини новый main b1cfff9d3 и разреши5 перечисленных конфликтов; повтори
гейты/матрицу, затем проведи живую native проверку, которая оставалась недоступна из-за
Windows capture timeout. Сохрани все ограничения выше; если новых дефектов нет,
не переписывай готовую реализацию ради нового плана.
