# retailpro-ea-agent

ИИ-агент архитектора предприятия на OpenCode (глава 10 учебника).
Строит и проверяет модели ArchiMate в PlantUML по текстовому описанию.

## Состав

    AGENTS.md              общие правила проекта
    opencode.json          модель, права доступа
    AI_USAGE_LOG.md        журнал использования ИИ (ведет агент)
    input/                 исходные документы (retailpro_case.md)
    model/                 артефакты этапов 01_ ... 08_
    diagrams/              PlantUML-модели; approved/ - утвержденные
    examples/              пример модели для проверки инструмента
    tools/                 сюда нужно положить plantuml.jar
    .opencode/agents/      ea-lead, ea-extractor, ea-modeler,
                           ea-reviewer, ea-analyst
    .opencode/skills/      archimate-extraction-rules,
                           archimate-plantuml-rules,
                           archimate-implementation-rules
    .opencode/commands/    extract, model, review, gap, roadmap,
                           explain, alternatives
    .opencode/tools/       archimate_check.ts и archimate_check.py
    .opencode/package.json зависимость @opencode-ai/plugin для tools/

## Требования

- OpenCode (https://opencode.ai), подключенный к LLM (`/connect`);
- Java (JRE 11+) и файл `tools/plantuml.jar` (см. tools/README.md);
- Python 3 (скрипт проверки модели).

## Быстрый старт

    export OPENCODE_MODEL=провайдер/модель   # см. opencode models
    python3 .opencode/tools/archimate_check.py \
      examples/retailpro_application_tobe.puml   # ожидается PASS
    opencode

В сессии выполняйте команды по порядку, после каждой проверяйте
результат и подтверждайте переход к следующему этапу:

    /extract retailpro_case.md
    /model
    /review
    /gap
    /roadmap
    /explain retailpro.puml top
    /alternatives

## Если агент сообщает, что не может запустить archimate_check

1. Проверьте, что есть `.opencode/package.json` и OpenCode установил
   зависимости (при запуске он выполняет `bun install`; нужен доступ
   в интернет). Перезапустите OpenCode; при необходимости выполните
   `bun install` в каталоге `.opencode/` вручную. Версию
   `@opencode-ai/plugin` лучше привести в соответствие с версией
   OpenCode (`opencode --version`).
2. Проверьте скрипт вручную (должен вернуть PASS):
   `python3 .opencode/tools/archimate_check.py examples/retailpro_application_tobe.puml`.
   В Windows команда может называться `python`; тогда замените
   `python3` в `archimate_check.ts`, `ea-modeler.md`, `ea-reviewer.md`.
3. Запасной путь: `ea-modeler` и `ea-reviewer` имеют право запускать
   только команду `python3 .opencode/tools/archimate_check.py *`
   (узкое правило `bash`). Если инструмент не загрузился, агент
   должен использовать ее.
4. Если и это недоступно, агент обязан остановиться и сообщить об
   этом; результат проверки имитировать нельзя.
5. Если у вас OpenCode v2, имена ключей прав в нем другие (например,
   `shell` вместо `bash`, `subagent` вместо `task`); сверьте
   конфигурацию с документацией v2.
6. Подробные журналы работы OpenCode см. в разделе Troubleshooting:
   https://opencode.ai/docs/troubleshooting/

## Важно

- Используйте только вымышленные или обезличенные данные. Облачная
  модель получает все, что попало в контекст.
- Права доступа заданы в opencode.json и в файлах агентов: по
  умолчанию все запрещено, агентам выданы минимальные права.
- Описание соответствует документации OpenCode на октябрь 2026 г.;
  имена параметров сверяйте с https://opencode.ai/docs.
- Инструмент archimate_check.ts написан по документации OpenCode и
  не запускался в среде разработки; скрипт archimate_check.py
  проверен отдельно.
