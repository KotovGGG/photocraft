# Три оставшиеся части ремонта панелей — 2026-11-03

Код всех частей готов и отправлен в fork. Порядок принятия: #10908 → #10910 → миграция → compact/resize → Tools. Shared API #470 уже принят. Новые части пока сохранены как зависимые ветки с отдельными patch и описаниями PR; открывать их по очереди после принятия родителя, чтобы в main не отправлялся снова накопленный большой diff.

- codex/panel-layout-migration: старые Layout/колонки → один Workspace, скрытые возвраты, размеры, вкладки, безопасный fallback и личные view-параметры.
- codex/panel-compact-resize: компактные/раскрытые панели, docking и независимые размеры, реальный document-header, швы и hit targets.
- codex/panel-tools-floating: только whole-Tools drag, обе оси размеров, команды/lock/restore. Эта ветка содержит все предыдущие части и является итоговой для ручной проверки.

Точные SHA и родители — SOURCE.json. Отдельные изменения — migration.patch, compact.patch, tools.patch; описания для GitHub — *-pr.md. Рабочая папка итоговой ветки: F:/photocraft-panel-integration. F:/photocraft остаётся полной reference-веткой codex/panel-layout-upstream (69b370d2d). Не запускайте приложение из корня handoff-ветки: там историческое дерево. Основной EXE собирает пользователь.

Проверки каждой части указаны в её описании PR. Итоговая функциональная приёмка: 171 panel +31 dock +2 Tools command +8 toolbar +2 embedding +10 document tabs +9 workspace tests; engine panic_hunt отдельно прошёл. Свежие offscreen PNG: 444 compact, 444 итоговых, ещё 16 Tools. Ручные мониторы/mixed-DPI/native focus/IME/GPU latency не подтверждены. Полный UI suite не объявлен зелёным. Clippy блокируют зафиксированные неизменённые места upstream. Release-example perf --quick пока выполняется; окончательный результат будет добавлен перед завершением пакета.

Важная поправка к старым логам: общий Cargo target повторно использовал xtask, где CARGO_MANIFEST_DIR указывал на F:/photocraft. Поэтому прежние xtask-результаты не доказывают проверки отдельных review-веток. Все пять веток заново прошли layers/wasm с отдельным xtask, собранным в review checkout; точные данные — remaining-verified-gates.json. Для следующей машины соберите xtask заново с собственным --target-dir: скомпилированный xtask не переносим между каталогами. Прямые cargo check/test запускались в правильной review-папке.

Не выполнять merge PR и не force-push. Если родители приняты squash-merge, создать свежую ветку от актуального main и перенести только соответствующие собственные коммиты, не переписывая сохранённые ready-ветки. Для compact это a7df08d80 плюс последующие документационные коммиты; для Tools — accf5181a. Перед публикацией перечитать актуальные замечания/AGENTS и проверить конфликты. Сохранять новые возможности upstream и одобренное поведение панелей. Не менять CI, чужие credits, PSD/ATN или старый грязный D:/photocraft. Автор своих коммитов KotovGGG, About — @KotovGGG.
