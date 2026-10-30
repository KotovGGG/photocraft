# PhotoCraft: продолжение дома, 2026-10-30

Исходники восстановлены в `F:/photocraft`, ветка `codex/panel-layout-upstream`.
В неё объединён upstream `b1cfff9d30298eea4f446a8f6a5e4285cb43c6e7`.
Пять конфликтов разрешены с сохранением обеих сторон; checkpoint `a95714647`
отправлен в fork. Итоговый source commit: `1c53e40a853acdde3b367162f24c00cd8e650441`. Единственный PR: https://github.com/storytold/photocraft/pull/10322
Он остаётся draft до ручной desktop-приёмки и учёта незелёных upstream-гейтов.

Первоначальный пакет `portable-2026-10-30` и его SHA-манифест не изменялись.
Все 23 записи его манифеста проверены; original audit распакован, PLAN прочитан,
исходные пользовательские PNG просмотрены. Старые результаты относятся к
`cd571efe4` / `382b047c3`. Новые результаты находятся в этом пакете.

## Сборка основного EXE пользователем

Установлен Rust MSVC 1.95.0, доступны Visual Studio C++ tools и wasm target.
Команды PowerShell из корня восстановленного репозитория:

```powershell
Set-Location F:\photocraft
$env:Path = "$env:USERPROFILE\.cargo\bin;$env:Path"
$env:CARGO_BUILD_JOBS = '2'
$env:CARGO_TARGET_DIR = "$PWD\target"
cargo build --release --locked -p photocraft
```

После успешной сборки:

```powershell
.\target\release\photocraft.exe
```

Основной продуктовый EXE агент не собирал и не запускал. Опциональный HEIF не включён в эту базовую команду; для него добавляется
`--features heif`, как в документации проекта.

## Ручная приёмка

- Большой Color присоединяется к короткой мини-панели и сохраняет высоту после отрыва.
- Свёрнутые top/bottom группы остаются прикреплёнными строками вкладок; проверить
  раскрытие и вставку вкладки до/между/после существующих.
- Tools переносится целиком, изменяется по обеим осям; соседние компактные части
  раскрываются/сворачиваются независимо, без перекрытия.
- Обычный выбор слоя не открывает Properties; создание adjustment/fill открывает её.
- Проверить собственные мониторы и масштабирование, перенос между разными DPI,
  клавиатурный focus/IME и задержки GPU в обычной desktop-сборке.

Профили пользователя и старый `D:/photocraft` не менялись. Новых ATN/PSD,
action-name/text, CI и чужих credits в diff относительно upstream нет.
Новые коммиты принадлежат KotovGGG. Второй PR не создавался; merge PR не выполнялся.

## Проверки

136 панельных тестов прошли, два opt-in benchmark проигнорированы штатно.
Прошли относящиеся к панели фильтры, 2762 engine и 9 workspace integration тестов.
Свежая offscreen-матрица: 570 PNG, 72 pixel seam assertions, 515 replay PNG и 15 GIF.
Хеши 1267 исходных файлов совпали до/после этих прогонов.

Полный UI library run: **4460 passed, 95 failed, 23 ignored**. 92 имени сбоев
совпали с историческим списком; нового независимого полного baseline текущего
upstream не заявляется. Три остальных — неизменённые upstream font Probe tests:
ArrowDown+Enter выбирает установленный `Inter Hewn` вместо ожидаемого `Inter`.
Этот harness рисует Character/options, без docking. Шрифты и текстовый код не менялись.

Прогоны завершены. fmt/layers/wasm/parity/scorecard, doctest checks, shared docking
и shared Clippy прошли. Строгий UI/engine Clippy не прошёл: семь диагностических
точек в шести неизменённых upstream-файлах. Подробности — `ACCEPTANCE_RU.md`,
`results.json` и логи. Native-проверка остаётся за пользователем.

Не push в main и не merge PR автоматически. После ручной приёмки обновить этот же
PR #10322 для ревью, учитывая отдельно документированные сбои полного UI.
