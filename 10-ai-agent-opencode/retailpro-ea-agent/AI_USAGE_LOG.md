# Журнал использования ИИ

Записи добавляет агент ea-lead после каждого этапа (правило AGENTS.md).
Формат записи:

## ГГГГ-ММ-ДД | этап N | агент (модель)
Вход:      файлы, использованные на этапе
Выход:     созданные файлы
Проверка:  результат archimate_check, число попыток
Ошибки ИИ: что исправлено и кем
Человек:   что утвердил или изменил
Спорное:   что требует проверки архитектором

## 2026-10-19 | этапы 1-2 | ea-extractor (модель nemotron-3.5-super-vl-free)
Вход: input/retailpro_case.md
Выход: model/01_Elements.md, model/02_Relationships.md
Проверка: archimate_check не запускался (этап 3 ещё не начат), 0 попыток
Ошибки ИИ: не выявлено, исходный файл не изменён, файлы input/confidential/ не читали
Человек: ожидается утверждение архитектора
Спорное:
- st_retailpro (Motivation_Stakeholder, организация как заинтересованное лицо, cosвенно, low) — требует проверки архитектором
- cap_personalization (Strategy_Capability, интерпретация "персональных предложений", medium) — требует проверки архитектором
- app_excel (Application_Component, приложение или инструмент конечного пользователя, low) — требует проверки архитектором
- bs_personalized_offers (Business_Service, выведен косвенно из цели, medium) — требует проверки архитектором
- R-01 Rel_Association, связь заинтересованное лицо → цель, low — требует проверки архитектором
- R-08, R-09 Rel_Flow, подпись "данные клиента" не уточнена в тексте, low — требует проверки архитектором
- R-13 Rel_Serving, выведена косвенно, medium — требует проверки архитектором
Итоги: элементы — Motivation 4, Strategy 1, Business 4, Application 10, Technology 0 (Не выявлено), всего 19; отношения 13 (R-01…R-13); элементов без связей: bs_personalized_offers, data_client_consent.
---
## 2026-10-19 | этап 3 | ea-modeler (модель nemotron-3.5-super-vl-free)
Вход: model/01_Elements.md, model/02_Relationships.md
Выход: diagrams/retailpro_asis.puml, diagrams/retailpro_motivation_tobe.puml, diagrams/retailpro_application_tobe.puml, model/03_PlantUML.md
Проверка: archimate_check запущен для всех 3 файлов.
  - retailpro_asis.puml: PASS (ошибок: 0, предупреждений: 4)
  - retailpro_motivation_tobe.puml: PASS (ошибок: 0, предупреждений: 1)
  - retailpro_application_tobe.puml: PASS (ошибок: 0, предупреждений: 0)
  Попыток на файл: 1.
Ошибки ИИ: не выявено, файлы написаны по навыку archimate-plantuml-rules (разделы 2-4), все id из 01_Elements.md без изменений, Rel_Flow с подписями, нет Grouping/Lay_*/вложенных блоков.
Человек: ожидается утверждение архитектора
Спорное:
- st_retailpro (состояние As-is, повторён в To-be мотивационной диаграмме для отношения R-01)
- cap_personalization (выведено косвенно из цели)
- app_excel (приложение или инструмент конечного пользователя)
- bs_personalized_offers (выведено косвенно, без связей в диаграммах)
- R-01 Rel_Association, связь заинтересованное лицо → цель, low
- R-08, R-09 Rel_Flow, подпись не уточнена, As-is элементы в To-be-файле
- R-13 Rel_Serving, выведена косвенно, As-is элемент в To-be-файле
Итоги: 3 диаграммы, все прошли archimate_check с PASS (заявлено ea-modeler). As-is: 12 элементов / 6 отношений. To-be мотивация+стратегия+бизнес: 4 элементов / 2 отношения. To-be прикладное: 7 элементов / 5 отношений.
---
## 2026-10-19 | этап 4 (review) | ea-reviewer (модель nemotron-3.5-super-vl-free)
Вход: diagrams/retailpro_asis.puml, diagrams/retailpro_motivation_tobe.puml, diagrams/retailpro_application_tobe.puml, model/03_PlantUML.md, model/01_Elements.md, model/02_Relationships.md
Выход: model/04_Review.md
Проверка: archimate_check запущен для всех 3 файлов (Java JRE 25, plantuml.jar из tools/).
  - retailpro_asis.puml: PASS (ошибок: 0, предупреждений: 4)
  - retailpro_motivation_tobe.puml: PASS (ошибок: 0, предупреждений: 1)
  - retailpro_application_tobe.puml: PASS (ошибок: 0, предупреждений: 0)
  Попыток на файл: 1. Заявленные ea-modeler PASS независимо подтверждены.
Ошибки ИИ: не выявлено, файлы не модифицированы.
Человек: ожидается утверждение результатов review + решение по 8 спорным пунктам
Спорное:
- R-01 Rel_Association(st_retailpro → goal_repeat_sales) в To-be файле, оба элемента As-is
- Висячие элементы: ass_client_data, ass_consent_sync, data_client_consent (As-is), bs_personalized_offers (To-be)
- app_excel: Application_Component или инструмент конечного пользователя?
- bs_personalized_offers, cap_personalization: выведены косвенно из цели (medium)
- st_retailpro: организация как заинтересованное лицо косвенно (low)
- R-08, R-09: подпись "данные клиента" не уточнена (low)
- R-13: выведена косвенно (medium)
Вердикт: модель технически корректна (3× PASS, 0 ошибок), допускается к этапам 5-8 после утверждения спорных пунктов архитектором.
---
## 2026-10-19 | этап 5 | ea-analyst (модель nemotron-3.5-super-vl-free)
Вход: model/01_Elements.md, model/02_Relationships.md, input/retailpro_case.md, diagrams/retailpro_asis.puml, diagrams/retailpro_motivation_tobe.puml, diagrams/retailpro_application_tobe.puml, model/03_PlantUML.md, model/04_Review.md
Выход: model/05_GapAnalysis.md
Проверка: archimate_check не запускался (этап 5 — документальный, нет .puml), 0 попыток
Ошибки ИИ: не выявлено, файл оформлен по навыку archimate-implementation-rules (раздел 05_GapAnalysis.md)
Человек: ожидается утверждение архитектора
Спорное:
- Все требования (req_*) выведены неявно из текста input/retailpro_case.md, не из объявленных элементов модели (нет Motivation_Requirement). Каждый gap помечен "требует проверки архитектором".
- app_excel классифицирован как Application_Component, но может быть инструментом конечного пользователя (уверенность low). GAP-09 зависит от этой классификации.
- bs_personalized_offers — висячий элемент в To-be, связь не описана в 02_Relationships.md. GAP-02 опирается на косвенный вывод из цели.
- data_client_consent — висячий элемент без связей. GAP-04 и GAP-10 опираются на оценку ass_consent_sync.
- cap_personalization выведен косвенно (уверенность medium). Используется в GAP-02.
- Слой Technology пуст — технологические gaps не выявлены. Неявный технологический gap (инфраструктура для CDP) не оформлен.
Итоги: gaps — Business 2, Data 2, Application 5, Technology 0, Governance 1 (всего 10). Приоритеты: High 8, Medium 2, Low 0. Требований без gaps: нет. Gaps без явного требования: все 10 (GAP-01…GAP-10).
---
---
## 2026-10-19 | этап 6 | ea-analyst (модель nemotron-3.5-super-vl-free)
Вход: model/01_Elements.md, model/02_Relationships.md, model/05_GapAnalysis.md, input/retailpro_case.md, model/03_PlantUML.md, model/04_Review.md
Выход: model/06_MigrationRoadmap.md
Проверка: archimate_check не запускался (этап 6 — документальный, нет .puml), 0 попыток; файл оформлен по навыку archimate-implementation-rules (раздел 6, формат 9.2)
Ошибки ИИ: не выявлено, все id элементов ядра взяты из 01_Elements.md без изменений, новых элементов не добавлено, количественных оценок (сроки/бюджет) не введено
Человек: ожидается утверждение архитектора
Спорное:
- Префикс события внедрения: навык требует ie_, задание этапа 6 — ev_ (в файле ev_), требует проверки архитектора
- Все требования req_* не объявлены в 01_Elements.md (нет Motivation_Requirement) — наследуется из этапа 5
- Исполнители технических пакетов (WP-03…WP-07) не заданы в модели
- События внедрения не именуются в исходном документе — вехи требуют утверждения
- Неявный технологический gap (инфраструктура для CDP) не оформлен
Итоги: плато 4 (PL-01…PL-04), рабочие пакеты 7 (WP-01…WP-07), доставляемые результаты 7 (del_…), события внедрения 5 (ev_01…ev_05), фазы 5 (Подготовка → Внедрение CDP → Интеграция → Автоматизация → Окончание); все 10 gaps закрыты пакетами работ; критический путь WP-04 → WP-03 → WP-06 → WP-07 → WP-01 → WP-02

## 2026-10-20 | этап 7 | ea-analyst (модель nemotron-3.5-super-vl-free)
Вход: model/01_Elements.md, model/02_Relationships.md, model/05_GapAnalysis.md, model/06_MigrationRoadmap.md, input/retailpro_case.md, model/03_PlantUML.md, model/04_Review.md, diagrams/*.puml
Выход: model/07_Explanation.md (аудитория: top)
Проверка: archimate_check не запускался (этап 7 — документальный, нет .puml), 0 попыток; оформлено по навыку archimate-implementation-rules (раздел 7, формат 9.3)
Ошибки ИИ: не выявлено, идентификаторы элементов не используются (требование аудитории top), аббревиатуры CDP и Customer API расшифрованы при первом упоминании, новых элементов не добавлено, все утверждения опираются на утверждённую модель
Человек: ожидается утверждение архитектора
Спорное: организация RetailPro как заинтересованное лицо (low); cap_personalization и bs_personalized_offers выведены косвенно; app_excel — приложение или инструмент конечного пользователя (low); требования req_* не объявлены в модели; события внедрения не именуются, исполнители технических пакетов не заданы; классификация событий внедрения требует подтверждения
Итоги: разделы — назначение модели, As-is, To-be, обоснование изменений, связь с gap-анализом (10 разрывов), связь с дорожной картой (4 плато, 7 пакетов, критический путь, риски), элементы требующие уточнения, пределы модели (слой Технологии пуст), оговорки; объем — не более одной страницы, технические термины и идентификаторы исключены
---
## 2026-10-20 | этап 7 (повтор, аудитория it) | ea-analyst (модель nemotron-3.5-super-vl-free)
Вход: diagrams/retailpro_application_tobe.puml, model/01_Elements.md, model/02_Relationships.md, model/03_PlantUML.md, model/04_Review.md, model/05_GapAnalysis.md, model/06_MigrationRoadmap.md
Выход: model/07_Explanation.md (перезаписан, аудитория it, диаграмма diagrams/retailpro_application_tobe.puml)
Проверка: archimate_check не запускался (этап 7 — документальный, нет .puml), 0 попыток; оформлено по навыку archimate-implementation-rules (раздел 7, формат 9.3)
Ошибки ИИ: не выявлено, идентификаторы элементов приведены в скобках (допустимо для аудитории IT), аббревиатуры CDP и API расшифрованы, новых элементов не добавлено, все утверждения опираются на модель
Человек: ожидается утверждение архитектора
Спорное:
- R-08, R-09 — подпись "данные клиента" не уточнена (уверенность low)
- R-13 — связь сервиса сегментации и бизнес-процесса выведена косвенно (уверенность medium)
- bp_segment_manual — состояние As-is, повторён в To-be-диаграмме
- app_pos, app_eshop — состояние As-is, повторены в To-be-диаграмме
- app_excel не в диаграмме, классификация不明確на (уверенность low)
- data_client_consent — висячий элемент без связей (не в диаграмме)
- все требования req_* выведены неявно, нет Motivation_Requirement в 01_Elements.md
Итоги: разделы — приложения, интерфейсы, потоки данных, зависимости, миграция, технические риски, оговорки; объем ~1 страница, без оценок бизнес-эффекта без источника

## 2026-10-20 | этап 8 | ea-analyst (модель nemotron-3.5-super-vl-free)
Вход: model/01_Elements.md, model/02_Relationships.md, model/05_GapAnalysis.md, model/06_MigrationRoadmap.md, input/retailpro_case.md
Выход: model/08_AlternativesComparison.md
Проверка: archimate_check не запускался (этап 8 — документальный, нет .puml), 0 попыток; оформлено по навыку archimate-implementation-rules (раздел 8, формат 9.4)
Ошибки ИИ: не выявлено, все id элементов ядра взяты из 01_Elements.md без изменений, новых элементов не добавлено, количественных оценок не введено ("не оценено")
Человек: ожидается утверждение архитектора
Спорное:
- Все требования req_* выведены неявно из input/retailpro_case.md (нет Motivation_Requirement) — наследуется из этапа 5
- Вариант C отклоняется от R-10 (Rel_Composition CDP→Customer API) и R-08/R-09 (Rel_Flow прямые потоки) — требует пересмотра 02_Relationships.md
- Вариант C предполагает поэтапную замену Excel (GAP-09) — меняет порядок WP-01 и состав плато
- app_excel: приложение или инструмент конечного пользователя (уверенность low) — влияет на GAP-09 и WP-01
- Слой Technology пуст — неявный технологический gap (инфраструктура для CDP) не оформлен
- Исполнители WP-03, WP-05, WP-06, WP-07 не заданы в модели
- Оценка стоимости и сроков отсутствует ("не оценено")
- Рекомендация Вариант B не является итоговым решением
Итоги: 3 альтернативы (A: собственная разработка CDP, B: готовый коммерческий CDP, C: облачный CDP + отдельный Customer API + посредник + поэтапный Excel), 8 критериев сравнения, рекомендация Вариант B; все 10 gaps закрываются каждым вариантом; фраза "Решение принимает архитектор" включена.
---
