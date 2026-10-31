# PR #10322 готов к ревью

PR: https://github.com/storytold/photocraft/pull/10322
Код: d0e052e48434fa13f4ad60eebd20eb125bacac24, ветка origin/codex/panel-layout-upstream.
Последний проверенный code commit: 88da5a9142c9c55bbb9fb93abe8ddc5192f83929 (после него только docs/assets).

Сначала прочитать RESULTS_RU.md, PR_STATUS.json и docs/panel-docking-validation.md. Полный UI suite и строгий Clippy НЕ зелёные, ограничения явно раскрыты. Пользователь сообщил об успешной проверке своего исправленного EXE до последнего main/shared-widget merge. Новое объединение покрыто автоматическими проверками; отдельная native/IME/mixed-DPI/GPU сертификация не заявляется.

Восстановление:

```powershell
git clone --branch codex/panel-layout-upstream https://github.com/KotovGGG/photocraft.git
Set-Location photocraft
git restore --source origin/codex/panel-layout-handoff-2026-10-31 --worktree -- plan/panel-repair/pr-ready-portable-2026-10-31
Expand-Archive -LiteralPath plan/panel-repair/pr-ready-portable-2026-10-31/pr-ready-evidence.zip -DestinationPath plan/panel-repair/pr-ready-2026-10-31
```

Если checkout уже существует, сначала проверить git status, ветку и remotes. Не сбрасывать изменения или профиль. Не распаковывать поверх своих материалов без проверки. Основной EXE собирает пользователь; тестовые/offscreen сборки разрешены. Новые коммиты только KotovGGG, подпись About только @KotovGGG. Не трогать посторонние ATN/PSD, action names/text, CI и чужие credits. Не создавать второй PR и не выполнять merge PR без новой прямой инструкции.

Следующий шаг — дождаться ревью/проверок существующего PR, проверить замечания по текущему коду и исправлять только подтверждённые проблемы. Не скрывать исходные незелёные гейты и не менять CI ради feature/fix PR. Не повторять команду CodeRabbit, пока текущий обзор выполняется.

Предыдущий пакет f8c0c4a72 остаётся в portable-2026-10-31 на этой же handoff-ветке. Исходный аудит находится в handoff-ветке 2026-10-30. Старые матрицы и результаты не считать приёмкой будущего main.
