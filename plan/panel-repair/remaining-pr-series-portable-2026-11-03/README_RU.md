# Три оставшиеся части ремонта панелей — 2026-11-03

Код всех частей готов и отправлен в fork. Порядок принятия: #10908 → #10910 → миграция → compact/resize → Tools. Shared API #470 уже принят. Новые части пока сохранены как зависимые ветки с отдельными patch и описаниями PR; открывать их по очереди после принятия родителя, чтобы в main не отправлялся снова накопленный большой diff.

- codex/panel-layout-migration: старые Layout/колонки → один Workspace, скрытые возвраты, размеры, вкладки, безопасный fallback и личные view-параметры.
- codex/panel-compact-resize: компактные/раскрытые панели, docking и независимые размеры, реальный document-header, швы и hit targets.
- codex/panel-tools-floating: только whole-Tools drag, обе оси размеров, команды/lock/restore. Эта ветка содержит все предыдущие части и является итоговой для ручной проверки.

Точные SHA и родители — SOURCE.json. Отдельные изменения — migration.patch, compact.patch, tools.patch; описания для GitHub — *-pr.md. Рабочая папка итоговой ветки: F:/photocraft-panel-integration. F:/photocraft остаётся полной reference-веткой codex/panel-layout-upstream (69b370d2d). Не запускайте приложение из корня handoff-ветки: там историческое дерево. Основной EXE собирает пользователь.

Проверки каждой части указаны в её описании PR. Итоговая функциональная приёмка: 171 panel +35 dock +3 Tools command +8 toolbar +2 embedding +10 document tabs +9 workspace tests; engine panic_hunt отдельно прошёл. Offscreen PNG до follow-up восстановления: 444 compact, 444 Tools, ещё 16 палитры Tools. Их исходные SHA сохранены, это не повтор матрицы после review-fix. Два новых PNG проверяют notice при скрытом status bar и fullscreen. Ручные мониторы/mixed-DPI/native focus/IME/GPU latency не подтверждены. Полный UI suite не объявлен зелёным. Clippy блокируют зафиксированные неизменённые места upstream. Performance: окончательный результат и ограничения находятся в PERFORMANCE_STATUS.md, perf-summary.md и perf-results.json; зелёный performance gate не заявлен.

Важная поправка к старым логам: общий Cargo target повторно использовал xtask, где CARGO_MANIFEST_DIR указывал на F:/photocraft. Поэтому прежние xtask-результаты не доказывают проверки отдельных review-веток. Все пять веток заново прошли layers/wasm с отдельным xtask, собранным в review checkout; точные данные — remaining-verified-gates.json. Для следующей машины соберите xtask заново с собственным --target-dir: скомпилированный xtask не переносим между каталогами. Прямые cargo check/test запускались в правильной review-папке.

Не выполнять merge PR и не force-push. Если родители приняты squash-merge, создать свежую ветку от актуального main и перенести только соответствующий incremental patch через git apply --3way либо собственные коммиты из SOURCE.json, не переписывая сохранённые ready-ветки. Patch уже содержит разрешённые пересечения с родительскими review-fix; при конфликтах сохранять и родительское восстановление/notice, и новую функциональность. После переноса повторить проверки. Список собственных коммитов каждой части хранится в own_non_merge_commits в SOURCE.json. Перед публикацией перечитать актуальные замечания/AGENTS и проверить конфликты. Сохранять новые возможности upstream и одобренное поведение панелей. Не менять CI, чужие credits, PSD/ATN или старый грязный D:/photocraft. Автор своих коммитов KotovGGG, About — @KotovGGG.

Дополнительно исправлены пять замечаний CodeRabbit к #10910: явная правка native fallback заменяет сохранённую нечитаемую раскладку читаемым Workspace; noop/theme/chrome сохраняют исходные данные; успешная загрузка/сброс убирают только собственное предупреждение. Non-blocking notice виден без строки состояния, в том числе fullscreen. Старый reset не фиксирует прежнюю native-раскладку вместо выбранного preset. Изменения переданы зависимым веткам; для них есть новые *-review-* логи.

Текущий main при последней проверке — 24d4f4db9; review-серия намеренно остаётся на 289dd0a87 с открытыми родителями #10908/#10910. Перед публикацией каждой следующей части нужно заново проверить main, принятие родителей и incremental diff. Подготовка ветки не означает одобрение или merge PR.

Если нужно повторно собрать итоговую версию самостоятельно (PowerShell):
```powershell
Set-Location F:\photocraft-panel-integration
$env:CARGO_TARGET_DIR = 'F:\photocraft\target'
cargo build --release -p photocraft
```
Результат — F:/photocraft/target/release/photocraft.exe. Этот продуктовый build агент не запускал.

Read-only merge-tree с main 24d4f4db9fea590ed7dde65db6592938359c2c2e выполнен для трёх веток; результат — UPSTREAM_MERGE_PREVIEW.json. Это проверка текстового объединения, а не компиляция/приёмка объединённого дерева. Сам main не добавлялся в review-ветки.

На main 24d4f4db9 миграция текстово объединяется чисто; compact/Tools имеют один документальный конфликт в docs/gaps.md после большого upstream ATN update. Решать его по существу при публикации compact после принятия родителей; исходники в read-only preview объединились без текстовых конфликтов. Это не подтверждает их компиляционную/поведенческую совместимость с новым main.
