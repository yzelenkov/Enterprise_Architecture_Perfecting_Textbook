# Отчет этапа 4: независимая проверка модели (review)
Источник: diagrams/retailpro_asis.puml, diagrams/retailpro_motivation_tobe.puml, diagrams/retailpro_application_tobe.puml, model/01_Elements.md, model/02_Relationships.md, model/03_PlantUML.md
Агент: ea-reviewer (модель nemotron-3.5-super-vl-free)

## Инструмент проверки

- `python3 .opencode/tools/archimate_check.py <файл>`
- Компиляция: `plantuml.jar` (в tools/), Java JRE 25.0.4.1 (Temurin)
- Линтер: проверка объявлений id, соответствия префиксов макросам, неописанных id в отношениях, подписей у Rel_Flow, Association вне Motivation, висячих элементов.

## Результаты проверки (запуск 1)

| Диаграмма | Результат | Ошибок | Предупреждений | Соответствие заявленному ea-modeler |
|---|---|---|---|---|
| diagrams/retailpro_asis.puml | PASS | 0 | 4 | Да (PASS, 0/4) |
| diagrams/retailpro_motivation_tobe.puml | PASS | 0 | 1 | Да (PASS, 0/1) |
| diagrams/retailpro_application_tobe.puml | PASS | 0 | 0 | Да (PASS, 0/0) |

### Предупреждения линтера (не блокируют PASS)

**retailpro_asis.puml (4 шт.):**
- элемент `st_retailpro` не имеет ни одной связи
- элемент `ass_client_data` не имеет ни одной связи
- элемент `ass_consent_sync` не имеет ни одной связи
- элемент `data_client_consent` не имеет ни одной связи

**retailpro_motivation_tobe.puml (1 шт.):**
- элемент `bs_personalized_offers` не имеет ни одной связи

**retailpro_application_tobe.puml:** предупреждений нет.

Все предупреждения совпадают со списком "элементов без связей" из `02_Relationships.md` (раздел "Элементы без связей") и ожидаемы.

## Сверка с моделью (01_Elements.md / 02_Relationships.md)

- Все id в .puml-файлах берутся из `01_Elements.md` без изменений.
- Префиксы идентификаторов соответствуют макросам PlantUML (проверка линтера не выдала ERROR по префиксам).
- Все id в отношениях объявлены; неописанных id не выявлено.
- У всех `Rel_Flow` есть подписи ("данные клиента", "автоматическая сегментация").
- Нет Grouping, Lay_*, вложенных блоков, многострочных макросов внутри скобок.
- Элементов и отношений, которых нет в `01_Elements.md` / `02_Relationships.md`, не добавлено.
- Состояния As-is и To-be разделены по файлам в соответствии с `01_Elements.md`.

## Спорные места (требуют проверки архитектором)

1. **R-01 `Rel_Association(st_retailpro, goal_repeat_sales)`** в `retailpro_motivation_tobe.puml`: оба элемента имеют состояние As-is в `01_Elements.md`, но отношение и повтор `st_retailpro` размещены в To-be-диаграмме. Связь stakeholder → цель через Association выбрана, так как иное выразить нельзя (уверенность low).
2. **Висячие элементы без связей:** `ass_client_data`, `ass_consent_sync`, `data_client_consent` (As-is) и `bs_personalized_offers` (To-be). Описаны в `02_Relationships.md` как без связей — оставить как есть или добавить отношения.
3. **`app_excel`** — Application_Component или инструмент конечного пользователя? (уверенность low).
4. **`bs_personalized_offers`** — бизнес-сервис выведен косвенно из цели, прямо в тексте не называется (уверенность medium).
5. **`cap_personalization`** — способность выведена косвенно из "персональных предложений" (уверенность medium).
6. **`st_retailpro`** — организация как заинтересованное лицо следует косвенно (уверенность low).
7. **R-08, R-09** `Rel_Flow` с подписью "данные клиента" — подпись не уточнена в тексте (уверенность low).
8. **R-13** `Rel_Serving(as_segmentation, bp_segment_manual)` — выведена косвенно (уверенность medium).

## Вердикт

Модель технически корректна: все три диаграммы прошли `archimate_check` с результатом **PASS**, 0 ошибок, предупреждения только о висячих элементах (задокументированы на этапах 1-3). Заявленные ea-modeler PASS независимо подтверждены.

Модель допускается к передаче на этапы 5-8 (gap-анализ, дорожная карта, объяснение, альтернативы) после утверждения списка спорных пунктов архитектором.
