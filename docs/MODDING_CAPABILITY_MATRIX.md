# Карта возможностей моддинга — «Дети Эльтана»

Этот документ — технический фильтр проекта. Никакая механика не считается доступной в моде КР2/SRHD, пока способ её реализации не подтверждён документацией, известным инструментом, проверенным примером мода или воспроизводимым экспериментом.

## Статусы

- `verified-native` — используется базовая механика игры без изменения движка.
- `verified-moddable` — подтверждено, что возможность изменяется через моддинг.
- `verified-tool-assisted` — подтверждено через конкретный инструмент/конвертер.
- `researching` — есть признаки возможности, но нет завершённой проверки.
- `unverified` — пока только проектная гипотеза.
- `unsupported` — подтверждённое ограничение текущего пути моддинга.

## Матрица

| Область | Статус | Подтверждение / что ещё проверить | Реализация в «Детях Эльтана» |
|---|---|---|---|
| Файловый корень установки мода | `verified-moddable` | Пользовательские моды живут внутри каталога игры `Mods/`. При этом реальная SRHD-структура допускает вложенность `Mods/<Category>/<Mod>/ModuleInfo.txt`, а не только `Mods/<Mod>/`. Это подтверждается актуальным руководством MO2 для SRHD и файлами официального Steam depot. Источники: `https://www.nexusmods.com/spacerangersawarapart/mods/57`, `https://steamdb.info/depot/214731/`, `https://github.com/Xenomorphchyma/SRHD-XenoModKit` | релиз должен разворачиваться под `Space Rangers HD/Mods/`; финальный category path фиксируем только после smoke-test конкретного skeleton |
| Активация через `ModCFG.txt` | `researching` | Подтверждено, что игра читает `Mods/ModCFG.txt` как список включённых модов; XenoModKit и MO2 умеют анализировать effective load order. Но точный минимальный legally-clean текст записи для нового `ChildrenOfEltan` ещё не воспроизведён на установленной игре. | блокирует первый устанавливаемый пакет |
| Семантика порядка загрузки | `verified-moddable` | Порядок строк в `ModCFG.txt` влияет на load order только при одинаковом `Priority`; значение `Priority` берётся из `ModuleInfo.txt` и может изменить фактический порядок. Актуальный SRHD MO2-plugin нормализует `Priority=1`, чтобы порядок `ModCFG.txt` совпадал с видимым порядком модов. Источник: `https://www.nexusmods.com/spacerangersawarapart/mods/57` | для первого skeleton использовать один явно зафиксированный `Priority` после проверки допустимого минимального `ModuleInfo` |
| Структура папки мода / `ModuleInfo.txt` | `researching` | Наличие `ModuleInfo.txt` в корне конкретного модуля подтверждено XenoModKit и официальными файлами SRHD (`Mods/Tweaks/German/ModuleInfo.txt`, `Mods/Tweaks/LeoDomikShipsUpdate15/ModuleInfo.txt` и др.). XenoModKit требует `ModuleInfo.txt` для упаковки. Точный минимальный набор ключей/значений для нового пустого мода всё ещё требует воспроизводимого runtime-теста. | следующий шаг M1 — вывести минимальный оригинальный `ModuleInfo.txt` из проверенных полей и подтвердить его в игре |
| `ModuleInfo.txt` — `Section` + `SectionEng` coexistence | `verified-tool-assisted` | GPL-3.0 community tool `jaroslavknotek/SRHD-lang-dat-translate` preserves `Section` and adds `SectionEng=<parent category folder>` when translating real SRHD mod layouts; its test asserts exactly one `SectionEng` equal to the parent category. README reports use across large Evolution/Expansion/Revolution/ShusRangers/OtherMods/Tweaks sets. Evidence: `docs/evidence/2026-09-07-moduleinfo-sectioneng-semantics.md`. This does not resolve engine-required encoding/BOM or whether `SectionEng` is mandatory for a Russian-only module. | не удалять `Section` из research template; финальный `SectionEng` добавлять только после фиксации категории и byte-level/runtime проверки |
| Тексты/локализация | `researching` | XenoModKit подтверждает аудит кодировок и работу с языковыми DAT/TXT, но конкретная точка override для нашего пакета ещё не проверена в игре. | диалоги, новости, описания, лор |
| Квесты | `verified-tool-assisted` | SRHD XenoModKit читает QM 2/3/4 и QMM 6/7, экспортирует JSON, собирает QMM 7 и делает round-trip; игровой smoke-test конкретного квеста всё равно обязателен. | главная сюжетная кампания и побочные цепочки |
| Игровые таблицы/баланс | `verified-tool-assisted` | BlockPar DAT подтверждён через XenoModKit + BlockParEditor 2.1; конкретные таблицы и override-точки для предметов/баланса ещё требуют исследования. | оборудование, цены, награды, параметры |
| Изображения/иконки | `verified-tool-assisted` | XenoModKit нативно проверяет и преобразует GI↔PNG для подтверждённых режимов; точки подключения конкретных ассетов ещё проверяются отдельно. | оригинальные визуальные ресурсы |
| Контейнеры ресурсов PKG/GAI | `verified-tool-assisted` | XenoModKit читает/проверяет GAI/HAI/PKG и детерминированно собирает подтверждённые разновидности GAI/PKG; HAI остаётся read-only. | упаковка разрешённых оригинальных ресурсов там, где это требуется движком |
| Скрипты SCR/RSON/RSM | `verified-tool-assisted` | XenoModKit + RScript 4.15f + rsmc поддерживают аудит, декомпиляцию/сборку и runtime-lint; конкретные хуки кампании должны подтверждаться отдельно. | сценарные расширения только после проверки точки регистрации |
| Нативные DLL-плагины через XenoNativeLoader | `verified-tool-assisted` | XenoModKit 0.10.2 умеет создавать, собирать и статически валидировать x86 PE32 `*.XenoPlugin.dll` с Host API V1 (`XenoPlugin_Query` / `XenoPlugin_Initialize`). Публичная коллекция `Xenomorphchyma/XenoMods` документирует XenoNativeLoader 0.6.7 и реальные моды, использующие нативные плагины: `XenoBigGalaxy`, `XenoEquipmentInflation`, `XenoHangarPaging`, `XenoCoalitionSupplyLines`, `XenoDomRangers`. Loader проксируется через `dsound.dll`, читает активный `Mods/ModCFG.txt`, загружает DLL только включённых модов и проверяет сигнатуры перед хуками. Источники: `https://github.com/Xenomorphchyma/SRHD-XenoModKit`, `https://github.com/Xenomorphchyma/XenoMods`. Runtime-совместимость конкретного Children of Eltan plugin/версии EXE всё равно требует отдельного smoke-test. | допустимый расширенный путь только для механик, действительно недоступных DAT/RScript/QMM; не использовать как дефолт и не копировать XenoMods-код/контент без ясной лицензии |
| Звук/музыка | `researching` | форматы и точки подключения ещё не подтверждены для нашего пакета | оригинальный OST и звуковые события |
| Стартовые условия рейнджера | `unverified` | доступ к стартовым параметрам через мод | классы, отношения, стартовые ресурсы |
| Репутация/дипломатия | `unverified` | какие значения/события доступны модам | последствия выбора и фракционные ветки |
| Новое оборудование | `unverified` | таблицы, ID, ограничения движка | технологии эпохи «Детей Эльтана» |
| Новые NPC/события | `unverified` | форматы событий и генерации | сюжетные персонажи и динамические встречи |
| Новые системы/карта | `unverified` | можно ли безопасно менять галактику | новые регионы и аномальные зоны |
| Глубокий гипер | `unverified` | доступные механики/сценарные обходы | только после технической проверки |
| Новые UI-сценарии | `unverified` | степень модифицируемости интерфейса | не блокирует основную кампанию |
| Изменение бинарного движка | `unsupported` | не является базовым путём проекта; нативные loader-плагины рассматриваются отдельно как tool-assisted extension и не означают разрешение патчить `Rangers.exe` на диске | только отдельный эксперимент при явном решении |

## Проверенный toolchain-кандидат

**SRHD XenoModKit** (`Xenomorphchyma/SRHD-XenoModKit`) — публичный headless-набор инструментов для Space Rangers HD. Для M1 он рассматривается как `verified-tool-assisted` источник по структуре/аудиту мода и поддерживаемым форматам, но не как доказательство конкретной игровой механики без smoke-test в SRHD.

Подтверждённые им области, полезные проекту: структура мода и `ModuleInfo.txt`, `ModCFG.txt`/load-order audit, DAT, SCR/RSON/RSM, QM/QMM, GI/GAI/HAI/PKG, кодировки, детерминированная release-сборка и deploy в заданный корень `Mods`.

Ключевая граница: статическая проверка и успешная сборка формата не заменяют запуск в игре. Любой новый контент получает окончательную совместимость только после smoke-test на явно зафиксированной версии Space Rangers HD.

## Новое подтверждение layout/load-order (2026-09-07)

Публичное руководство **Mod Organizer 2 for Space Rangers HD** (обновлено 17 августа 2026) документирует две важные особенности реального загрузчика SRHD:

1. Игра читает список включённых модов из `Mods/ModCFG.txt`.
2. Физический мод может находиться как `Mods/<Category>/<Mod>/ModuleInfo.txt`; следовательно правило «одна непосредственная подпапка `Mods` = один мод» для SRHD неверно.
3. `Priority` из `ModuleInfo.txt` участвует в фактическом load order; порядок строк `ModCFG.txt` сам по себе не гарантирует порядок загрузки при разных Priority.

Наличие именно такой вложенной структуры независимо видно в официальном Steam depot SRHD: `Mods/Tweaks/German/ModuleInfo.txt`, `Mods/Tweaks/LeoDomikShipsUpdate15/ModuleInfo.txt`, `Mods/Tweaks/LeoDomikShipsUpdate30/ModuleInfo.txt` и другие штатно поставляемые модули.

Это повышает **семантику load order** до `verified-moddable`, но **не** повышает саму активацию нашего нового мода до verified: ещё нужны точная запись `ModCFG.txt`, минимальные поля `ModuleInfo.txt`, версия игры и чистый runtime smoke-test.

## Новое подтверждение `Section` / `SectionEng` (2026-09-07)

Публичный GPL-3.0 инструмент **`jaroslavknotek/SRHD-lang-dat-translate`** даёт независимое community-toolchain подтверждение семантики локализованной категории модуля. В `python/app.py` исходный `Section` сохраняется, а `SectionEng` добавляется как имя родительской category-папки (`module_info_path.parent.parent.name`). Тест `tests/test_app.py` воспроизводит `ModSection/TestMod/ModuleInfo.txt` и требует ровно один `SectionEng=ModSection`.

README инструмента сообщает практическое применение на крупном наборе модов Evolution, Expansion, Revolution, ShusRangers, OtherMods и Tweaks. Это переводит именно **coexistence/derivation pattern `Section` + `SectionEng`** в `verified-tool-assisted`, но не доказывает release-safe byte encoding и не делает `SectionEng` engine-required для любого языкового набора.

Источник и границы доказательства зафиксированы в `docs/evidence/2026-09-07-moduleinfo-sectioneng-semantics.md`.

## Новое подтверждение native-extension path (2026-09-07)

Актуальный **SRHD XenoModKit 0.10.2** добавляет статически проверяемый путь нативного расширения через **XenoNativeLoader Host API V1**: шаблон проекта, MSVC x86 build, PE32/ABI validation, manifest/config discovery и проверку точных экспортов `XenoPlugin_Query` / `XenoPlugin_Initialize`.

Публичная коллекция **XenoMods** показывает этот путь на реальных SRHD-модах. XenoNativeLoader 0.6.7 не изменяет `Rangers.exe` на диске: `dsound.dll` проксирует DirectSound, `XenoCore.dll` читает активный `Mods/ModCFG.txt`, а DLL модов находятся в их собственных `Native/` каталогах и загружаются только для включённых модов. Плагины проверяют сигнатуры исполняемого кода и пропускают неизвестные сборки вместо слепой установки hook-патчей.

Это подтверждает существование профессионального native-extension механизма и повышает сам **toolchain path** до `verified-tool-assisted`; однако ни один конкретный hook «Детей Эльтана» пока не подтверждён. Репозиторий XenoMods имеет неясный SPDX (`NOASSERTION`), поэтому его код и контент используются только как поведенческое/архитектурное доказательство, пока лицензия на повторное использование явно не установлена.

## Правило обновления

Каждое изменение статуса должно содержать источник или воспроизводимый тест: ссылку/название инструмента, целевую версию КР2/SRHD, пример входных файлов, результат запуска и известные ограничения. Не переносить предположения из legacy WebGL в колонку подтверждённых возможностей.

## Следующая цель

Получить **byte-level первичный артефакт реального shipped/installed SRHD `ModuleInfo.txt`**: BOM/encoding, `Section`, `SectionEng`, `Name`, `Priority` и затем провести smoke-test оригинального Children of Eltan skeleton на зафиксированной версии SRHD.
