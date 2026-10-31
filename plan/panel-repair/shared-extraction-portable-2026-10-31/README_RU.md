# Первый этап разделения PR

Создан https://github.com/storytold/craft-libs/pull/470 — 9 файлов, +341/-23. Ветка KotovGGG/craft-libs: codex/docking-host-geometry, commit dcd94c27e79e4795441339527df5bef64654b4f2. Текущая полная PhotoCraft-версия 7005992d2 сохранена; #10322 остаётся контрольной реализацией, со ссылкой на первый маленький PR в начале описания.

584 UI unit + 10 integration + 8 doctests passed (2 ignored); fmt и wasm passed. Общие гейты не зелёные: UI Clippy сообщает неизменённый preview.rs:120, workspace Clippy — неизменённый keymap/profiles.rs:474. Workspace test не завершился из-за internal compiler error Rust 1.95 в неизменённом craft-text linebreak/tests.rs:95. Подавления/посторонние исправления не добавлялись. Полный UI пакет прошёл; полный workspace — не объявлять успешным.

Следующий шаг — ревью/принятие shared API. Затем закрепить реальный принятый upstream SHA, убрать vendor snapshot и последовательно готовить меньшие PhotoCraft PR. До этого не подставлять несуществующую upstream ревизию. Не закрывать контрольный #10322 и не выполнять merge PR. Пользователь разрешил порядок с несколькими PR взамен старого требования одного PR. См. SPLIT_PLAN_RU.md.

Новый рабочий checkout: F:/photocraft-shared-ui. Исходный F:/photocraft и продуктовый EXE не менялись. Автор новых коммитов — только KotovGGG. Нельзя добавлять fonts, CI, сторонние ATN/PSD/action names/credits. Не пересылать старые результаты как проверку новых ревизий.
