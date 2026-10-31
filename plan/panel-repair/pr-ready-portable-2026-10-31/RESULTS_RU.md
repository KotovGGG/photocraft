# Отправка PR #10322 — 2026-10-31

Пользователь проверил свой исправленный v0.18.0 EXE и сообщил, что больше не видит крупных проблем. Подпись в About оставлена автоматической: @KotovGGG, без изменения contributors.

Проверенный код: 88da5a9142c9c55bbb9fb93abe8ddc5192f83929. Итоговый PR head d0e052e48434fa13f4ad60eebd20eb125bacac24 отличается от него документацией и изображениями. Включён актуальный main 422ca7beda90d927643bcd074646ebbd37706d75. После ручной приёмки main обновил updater dialog и craft-libs; эта последняя интеграция проверена автоматически, без повторной нативной приёмки пользователем.

Изменения main сохранены. Единственный конфликт Cargo.lock разрешён с сохранением явного vendor override. Ревизия craft-libs c5a1cbfb5f9049f9270955caffb5bee5997aebf7 согласована с зависимостями и контрактом. Четыре обновлённых файла скопированы без изменений; аудит подтвердил 76 исходных файлов, идентичных pinned upstream, и ровно шесть файлов локального docking-патча. Проверка cargo metadata --locked прошла.

164 панельных + 9 workspace integration тестов прошли. Полный shared UI suite: 579 passed, включая 346 docking. Desktop all-targets cargo check, fmt, layers (31 crate), wasm (24 + codecs/heif) прошли. Полный UI library suite: 4494 passed, 95 failed, 23 ignored. Имена всех 95 сбоев точно совпали с предыдущим исправленным v0.18.0 snapshot; новых нет. Это не зелёный suite и не независимо повторённый baseline чистого main.

Clippy остаётся незелёным: стандартный UI check останавливается на неизменённом text/src/psd_path.rs:157; UI --no-deps сообщает прежние пять расположений в strokes/vp_ui/text_field/color_picker tests. Standalone shared Clippy сообщает два nonminimal_bool на docking/render/preview.rs:120, идентичном pinned upstream. Suppressions, изменения CI и посторонние исправления не добавлены.

444 новых PNG, все четыре capture-теста и проверки швов прошли. 443 PNG побайтно совпали с предыдущей проверенной версией; оставшийся drag-preview просмотрен рядом с прежним, изменений геометрии не обнаружено. Обновлены две after PNG и три GIF. CPU kittest по 600 samples: p50 idle/hover/drag 2.273/2.268/2.473 ms, drag p95 2.982 ms. Это не native FPS/GPU latency. Новые engine/corpus/broad perf результаты не заявляются. Основной EXE агентом не собирался и не запускался.

Существующий PR https://github.com/storytold/photocraft/pull/10322 обновлён и переведён из Draft в Ready for review. GitHub подтвердил mergeable=true; main ещё НЕ получил эти изменения. Оба прежних замечания CodeRabbit решены. Новый обзор бота запрошен одним комментарием @coderabbitai review. Точные временные внешние статусы находятся в PR_STATUS.json; они могут измениться. Merge PR, второй PR и включение auto-merge не выполнялись.

Живые focus/IME, физические мониторы/mixed-DPI и GPU/input latency отдельно не сертифицированы. Подробная английская приёмка хранится в docs/panel-docking-validation.md итогового PR. Архив содержит raw logs, JSON-манифесты, кадры, GIF и точный текст описания PR.
