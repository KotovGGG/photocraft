# Продолжение ремонта панелей PhotoCraft v0.18.0

Код: `f8c0c4a7204bf499e906c2fd978bba06aa512636`.
Ветка кода в fork: https://github.com/KotovGGG/photocraft/tree/codex/panel-layout-v018-checkpoint
Ветка этого пакета: `codex/panel-layout-handoff-2026-10-31`.

Завершены исправления размещения панелей под строкой вкладок документов, нижнего resize составного плавающего блока и высоты раскрываемой компактной группы. Подробные результаты и ограничения находятся в `RESULTS_RU.md`; хеши кода и визуальных материалов — в JSON-манифестах и архиве.

PR #10322 и его удалённая ветка `codex/panel-layout-upstream` НЕ обновлялись: они остались на `1c53e40a853acdde3b367162f24c00cd8e650441`. Не создавать второй PR и не выполнять merge PR. Основной EXE собирает и проверяет пользователь. Тестовые/offscreen сборки разрешены.

## Восстановление на другом компьютере

Если checkout отсутствует:

```powershell
git clone --branch codex/panel-layout-v018-checkpoint https://github.com/KotovGGG/photocraft.git
Set-Location photocraft
git fetch origin codex/panel-layout-handoff-2026-10-31
git restore --source origin/codex/panel-layout-handoff-2026-10-31 --worktree -- plan/panel-repair/portable-2026-10-31
Expand-Archive -LiteralPath plan/panel-repair/portable-2026-10-31/native-followup-evidence.zip -DestinationPath plan/panel-repair/native-followup-2026-10-31
```

Если checkout уже существует, сначала проверить `git status`, ветку и remotes. Не сбрасывать незакоммиченные изменения и не распаковывать поверх существующих материалов без проверки.

На текущем компьютере код уже находится в `F:\photocraft`, локальная ветка называется `codex/panel-layout-upstream`. Не путать локальную ветку с пока не обновлённой одноимённой удалённой веткой PR.

Сборка пользователем:

```powershell
Set-Location F:\photocraft
& "$env:USERPROFILE\.cargo\bin\cargo.exe" build --release --locked -p photocraft -j 2
```

EXE: `F:\photocraft\target\release\photocraft.exe`.

Проверить на сохранённой пользовательской компоновке: вставку непосредственно под строкой документов и отдельно над ней; нижний край/оба нижних угла плавающей группы до изменения ширины; раскрытие двух панелей рядом и друг над другом; повторный collapse/expand после resize. Размеры самостоятельного редактора и размеры частей группы хранятся раздельно; расположение по-прежнему хранит единственный shared Workspace.

Остаются неподтверждёнными native focus/IME, реальные мониторы/mixed-DPI, GPU-задержки и приёмка пользовательского EXE. Сначала дождаться пользовательской проверки; план по PR отложен пользователем. Не выдавать старые матрицы v0.17.0 за приёмку нового кода.

Релизная основа: v0.18.0 (`8a87a457abb43ac344deeb3fdb67541b91a72ff1`), объединение с ремонтом — `621d9238b`. Более поздний main намеренно не включался. Исходный аудит и предыдущий полный пакет находятся в ветке `codex/panel-layout-handoff-2026-10-30`, коммит `23e0598346274c9de940dbadd3fe4e2f5998c044`.

Сохранять одобренное поведение и ограничения исходного задания; новые наши коммиты — только KotovGGG, без посторонних ATN/PSD, CI и credits. Перед изменениями прочитать AGENTS.md и docs/panel-docking-contract.md.
