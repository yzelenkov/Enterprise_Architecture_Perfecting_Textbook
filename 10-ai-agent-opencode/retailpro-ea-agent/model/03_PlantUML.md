# Отчет этапа 3: PlantUML
Источник: model/01_Elements.md, model/02_Relationships.md
Агент: ea-modeler

| Диаграмма | Представление | Состояние | Элементов | Отношений | Попыток | Результат |
|---|---|---|---|---|---|---|
| diagrams/retailpro_asis.puml | Мотивационное + Бизнес + Прикладное | As-is | 12 | 6 | 1 | PASS |
| diagrams/retailpro_motivation_tobe.puml | Мотивационное + Стратегическое + Бизнес | To-be | 4 | 2 | 1 | PASS |
| diagrams/retailpro_application_tobe.puml | Бизнес-процесс + Прикладное | To-be | 7 | 5 | 1 | PASS |

## Инструмент проверки archimate_check

Запускался для всех трёх файлов. Инструмент: `python3 .opencode/tools/archimate_check.py <файл>`.

- `diagrams/retailpro_asis.puml`: PASS (ошибок: 0, предупреждений: 4)
- `diagrams/retailpro_motivation_tobe.puml`: PASS (ошибок: 0, предупреждений: 1)
- `diagrams/retailpro_application_tobe.puml`: PASS (ошибок: 0, предупреждений: 0)

## Исправления по результатам проверки

Исправления не требулись — все три файла прошли проверку с первой попытки.

Внесены изменения относительно существующих файлов перед первой проверкой:

1. **retailpro_asis.puml**: удалён элемент `goal_repeat_sales` (состояние To-be, не belongs в As-is) и отношение `R-01` (ссылается на To-be элемент). Оставлены только As-is элементы и отношения между ними.

2. **retailpro_motivation_tobe.puml**: добавлен элемент `st_retailpro` (повторён из As-is, требуется для отношения R-01) и отношение `R-01` (`Rel_Association(st_retailpro, goal_repeat_sales)`).

3. **retailpro_application_tobe.puml**: файл оставлен без изменений (уже соответствовал правилам).

## Спорные решения (требует проверки архитектором)

- `st_retailpro` повторён в диаграмме `retailpro_motivation_tobe.puml`, хотя его состояние — As-is. Требуется для отношения R-01 (Assocation stakeholder → goal, состояние отношения As-is, но цель — To-be).
- Элементы `ass_client_data`, `ass_consent_sync`, `data_client_consent` в As-is диаграмме не имеют связей (предупреждения линтера). Связи для них не описаны в `02_Relationships.md` — оставить как есть или добавить отношения — требует проверки архитектором.
- Элемент `bs_personalized_offers` в To-be мотивационной диаграмме не имеет связей. Связь не описана в исходнике — требует проверки архитектором.
- `app_excel` классифицирован как Application_Component — неясно, приложение это или инструмент конечного пользователя (уже отмечено в `01_Elements.md`).
- `bs_personalized_offers` выведен косвенно из цели, прямо в тексте не называется (уже отмечено в `01_Elements.md`).

## Примечания

- Предупреждения об элементах без связей ожидаемы: `02_Relationships.md` явно перечисляет `bs_personalized_offers` и `data_client_consent` как элементы без связей.
- Предупреждение об `Rel_Association` внутри слоя Motivation (para `st_retailpro` → `goal_repeat_sales`) ожидаемо по правилам навыка и не требует исправления.
- Все id взяты из `01_Elements.md` без изменений. Префиксы идентификаторов соответствуют макросам PlantUML.
- Нет Grouping, Lay_*, вложенных блоков и многострочных макросов.
- Элементы, общие для нескольких диаграмм (`st_retailpro`, `bp_segment_manual`, `app_pos`, `app_eshop`), повторены с теми же id и названиями.
