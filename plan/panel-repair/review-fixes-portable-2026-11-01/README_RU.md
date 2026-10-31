# Ревью панелей — 2026-11-01

Не запускайте проект из корня handoff-ветки: её дерево историческое. Код восстановления — `codex/panel-layout-upstream` (a175b27c1), он также сохранён в `codex/panel-layout-v018-checkpoint`. Runtime проверен на a4077cb15; позднее обновлены только документы/PNG. Точные SHA — SOURCE.json.

Shared PR: https://github.com/storytold/craft-libs/pull/470 — восемь замечаний исправлены (235fffbd, 4f263ed и 9a97555; дополнительно3685bae отключает хвостовую зону под host-owned свёрнутой группой), исходные review threads разрешены. 591 unit +10 integration +8 doctests прошли. Snapshot consumer остаётся235fffbd: дополнительный shared-only фикс относится к docked custom-group, а PhotoCraft эксклюзивно рисует только floating-группы. См. SOURCE.json и VALIDATION.md. PR открыт, не слит. Полное workspace-тестирование/Clippy не зелёные: причины и исходные файлы указаны в логах и приёмке.

PhotoCraft: пять замечаний обработаны в b73eecb8a, текущий main 799e12962 объединён как a4077cb15. Конфликты трёх документов разрешены, scorecard перегенерирован (11 из 183 настроек ничего не делают). 167 панельных и 9 workspace integration тестов прошли; fmt/layers/wasm/desktop check прошли. 444 новых PNG и seam assertions прошли. Центральная ROI всех 444 кадров совпадает с прошлой матрицей; полный кадр отличается внешним chrome. Это не проверка native EXE.

Полный UI последовательным запуском: 4640 passed,97 failed,23 ignored. Все прежние95 ошибок сохранились, плюс два новых теста upstream (см. ui-failure-comparison.json); чистый main независимо не прогонялся. Первый параллельный запуск завершился без полного отчёта. Нельзя называть suite зелёным. Clippy также не зелёный.

perf --quick: завершён, exit 0. Не выдавать промежуточный CPU benchmark, шедший одновременно с capture, за контролируемое сравнение производительности. Итоговые результаты и границы проверки — VALIDATION.md и perf-summary.md.

Продуктовый EXE агент не собирал/не запускал. Ручная приёмка пользователя предшествует этому merge. Физические мониторы/mixed-DPI, native IME/focus и GPU-задержки остаются отдельной проверкой. 13 GIF сохраняют источник7005992d2; текущая приёмка опирается на новые 444 PNG.

Дальше: дождаться принятия shared API в craft-libs, закрепить реальный immutable upstream SHA, убрать vendor и подготовить зависимые малые PR интеграции/persistence, compact/resize и Tools. Большой PR10322 сохраняется как полная reference-реализация, не сливать его автоматически. Credits остаются @KotovGGG, CI/чужие credits не менять.
