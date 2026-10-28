# Глава 5. Назначение и логика языка ArchiMate 4.0

[← Предыдущая глава](../04-adm-method/README.md) · [К оглавлению](../README.md) · [Следующая глава →](../06-archimate-relationships/README.md)

**После изучения этой главы студент должен уметь:**

1. объяснять, зачем нужен язык архитектурного моделирования ArchiMate;
2. отличать ArchiMate от TOGAF, BPMN, UML и PlantUML;
3. понимать базовую структуру языка ArchiMate;
4. объяснять понятия слоя и аспекта в ArchiMate;
5. различать активную структуру, поведение и пассивную структуру;
6. объяснять роль мотивационных, стратегических, бизнес-, прикладных, технологических и миграционных элементов;
7. читать простую ArchiMate-модель;
8. создавать минимальную ArchiMate-диаграмму на PlantUML;
9. понимать типичные ошибки при первом знакомстве с ArchiMate.

## 5.1. Учебная ситуация: RetailPro нужна единая архитектурная нотация

Компания RetailPro работает над инициативой создания единой клиентской платформы. В процессе обсуждения участвуют разные специалисты:

- директор по маркетингу;
- ИТ-директор;
- бизнес-аналитик;
- архитектор предприятия;
- разработчики;
- специалист по данным;
- специалист по информационной безопасности;
- руководитель проекта;
- юридический отдел.

Каждый участник привык к своему способу описания проблемы (Таблица 5.1).

**Таблица 5.1.** Разные описания одной инициативы

| Участник | Как описывает ситуацию |
|---|---|
| Директор по маркетингу | Нужно увеличить повторные продажи и персонализировать предложения |
| Бизнес-аналитик | Нужно изменить процесс подготовки кампаний |
| Специалист по данным | Нужен единый профиль клиента и качество мастер-данных |
| ИТ-директор | Нужно интегрировать CRM, POS и интернет-магазин |
| Разработчик | Нужны API и события покупок |
| Инфраструктурный специалист | Нужны облачное хранилище и брокер сообщений |
| Юридический отдел | Нужно учитывать согласия клиентов |

Все говорят о реальной проблеме, но на разных языках. Если использовать только текстовые описания, легко потерять связи:

```text
Цель бизнеса → процесс → данные → приложения → технологии → проекты
```

Для того чтобы эти связи можно было формально и наглядно описывать, используется язык **ArchiMate**.

## 5.2. Что такое ArchiMate

**ArchiMate** — это открытый язык архитектурного моделирования, предназначенный для описания архитектуры предприятия через взаимосвязанные элементы бизнеса, данных, приложений, технологий, мотивации, стратегии и изменений.

```text
ArchiMate — это язык, с помощью которого можно моделировать архитектуру предприятия.
```

Он позволяет показать:

- зачем нужны изменения;
- какие бизнес-возможности требуются;
- какие процессы реализуют ценность;
- какие приложения поддерживают процессы;
- какие данные используются;
- какие технологии обеспечивают работу приложений;
- какие проекты переводят предприятие из текущего состояния в целевое.

ArchiMate нужен, чтобы:

1. создать общий язык для бизнеса и ИТ;
2. моделировать связи между слоями предприятия;
3. анализировать влияние изменений;
4. описывать текущую и целевую архитектуру;
5. выявлять архитектурные разрывы;
6. строить дорожные карты миграции;
7. документировать архитектурные решения;
8. поддерживать трассируемость от целей до реализации.

**Пример.** Что дает ArchiMate в кейсе RetailPro. Без ArchiMate:

```text
Нужно внедрить CDP, чтобы персонализировать предложения.
```

С ArchiMate можно показать отношения между различными элементами компании:

```text
Stakeholder: Директор по маркетингу
    ↓
Goal: увеличить повторные продажи
    ↓
Requirement: единый профиль клиента
    ↓
Business Process: сегментировать клиентов
    ↓
Application Service: управление профилем клиента
    ↓
Application Component: CDP
    ↓
Data Object: профиль клиента
    ↓
Technology Service: database hosting
```

Второе описание более архитектурное, потому что оно показывает смысловые связи.

## 5.3. ArchiMate, TOGAF, BPMN, UML и PlantUML: в чем различие

Начинающие часто путают разные методы, языки и инструменты. Важно понимать их назначение.

**Таблица 5.2.** Сравнение методов, языков и инструментов

| Инструмент / язык / метод | Основное назначение | Пример использования |
|---|---|---|
| TOGAF | метод и фреймворк архитектурной работы | пройти ADM-фазы |
| ArchiMate | язык моделирования архитектуры предприятия | описать связь цели, процесса, приложения и технологии |
| BPMN | язык моделирования бизнес-процессов | детально описать процесс обработки заказа |
| UML | язык моделирования программных систем | описать классы, компоненты, последовательности |
| PlantUML | текстовый способ описания диаграмм | сгенерировать ArchiMate-диаграмму из кода |
| EA-инструмент | среда хранения и анализа моделей | Archi, Bizzdesign, Sparx EA |

**TOGAF и ArchiMate.** TOGAF отвечает на вопрос «Как организовать работу по совершенствованию архитектуры предприятия?» ArchiMate предоставляет средства построения моделей. Например, на фазе B: `Business Architecture` TOGAF требует описать бизнес-архитектуру. Для этого ArchiMate предлагает элементы `Business Actor`, `Business Role`, `Business Process`, `Business Service`, `Business Object`.

**ArchiMate и BPMN.** BPMN лучше подходит для детального описания логики бизнес-процесса, поскольку включает такие элементы как событие (event), задача (task), ветвления по условию (gateway), сообщение (message), обработка исключений (exception handling) и инструменты для моделирования ролей (pool и lane). ArchiMate лучше подходит для архитектурной связи процесса с другими слоями.

| ArchiMate | BPMN |
|---|---|
| <img src="images/icon-01.png" alt="Иллюстрация" width="137"> | <img src="images/icon-02.png" alt="Иллюстрация" width="370"> |

То есть ArchiMate отвечает на архитектурный вопрос: `Как процесс связан с приложениями и данными?`

BPMN отвечает на процессный вопрос: `Как именно выполняется процесс?`

**ArchiMate и UML.** UML применяется преимущественно для проектирования программных систем: варианты использования (Use Case), диаграммы классов; диаграммы компонентов; диаграммы последовательности; диаграммы развертывания. На Рис. 5.1 представлена диаграмма классов, связывающая классы Клиент (Customer), Покупки (Purchase) и Маркетинговые кампании (MarketingCampaign). Эти данные будут использоваться в приложении CDP.

![Рис. 5.1. Диаграмма классов CDP.](images/fig-5-1.png)

Рис. 5.1. Диаграмма классов CDP.

UML показывает внутреннюю структуру программного решения. ArchiMate работает на более высоком архитектурном уровне. В примере выше ArchiMate показывает связь приложения «Аналитическая платформа» с бизнесом.

**ArchiMate и PlantUML.** PlantUML не является языком архитектуры предприятия в строгом смысле. Это инструмент текстового описания диаграмм. Хотя изначально этот язык разработан для описания UML диаграмм, с его помощью можно записывать и ArchiMate-элементы в виде кода. Код для генерации диаграммы, приведенной выше:

```plantuml
@startuml
!include <archimate/Archimate>

title Трассируемость требования REQ-01

Business_Process(bp1, "Подготовить \n маркетинговую кампанию")
Application_Service(as1, "Сегментация клиентов")
Application_Component(ac1, "Аналитическая платформа")

Rel_Serving(as1, bp1)
Rel_Realization(ac1, as1)
@enduml
```

## 5.4. Архитектурная модель, элемент, отношение и представление

Перед изучением структуры ArchiMate нужно ввести несколько базовых понятий.

**Архитектурная модель** – это формальное описание выбранной части предприятия с помощью элементов и отношений.

Модель может включать любые объекты, которые уже обсуждались в предыдущих главах: цели, процессы, роли, приложения, данные, технологии, требования и т.д.

**Элемент** – это объект модели определенного типа.

**Отношение** показывает смысловую связь между элементами. В ArchiMate эти связи имеют формальные типы:

```text
Realization
Serving
Access
Flow
Influence
Triggering
Assignment
Composition
```

Отношения будут подробно изучаться в следующей главе.

**View** (или **представление**) – это конкретная диаграмма, показывающая часть модели для определенной аудитории и задачи. Одна и та же модель может иметь разные представления.

**Таблица 5.3.** Разные представления RetailPro

| View | Аудитория | Что показывает |
|---|---|---|
| Motivation View | руководство | зачем нужна клиентская платформа |
| Business View | маркетинг | как меняется процесс кампаний |
| Application View | ИТ | как интегрируются CRM, POS, CDP |
| Technology View | инфраструктурная команда | какие платформы нужны |
| Migration View | проектный офис | как будет выполняться переход |

## 5.5. Общая структура языка ArchiMate

> **Примечание о версиях.** В ArchiMate 4.0 термин «слой» (layer) заменен термином «домен» (domain), а часть элементов версии 3.x исключена: Constraint, Contract, Gap, Representation, Implementation Event и элементы Interaction (Business, Application, Technology Interaction). Их роль выполняют специализации более общих элементов (например, Constraint — специализация Requirement, Gap — специализация Assessment или Deliverable). В учебнике эти понятия описаны по терминологии версии 3.x, так как они удобны для обучения, а библиотека ArchiMate для PlantUML (проверено на версии 1.2026.8) по-прежнему содержит соответствующие макросы.

ArchiMate организован по слоям и аспектам. Можно выделить следующие группы элементов (Таблица 5.4).

**Таблица 5.4.** Группы элементов ArchiMate.

| Группа | Назначение |
|---|---|
| Motivation | цели, требования, принципы, ограничения |
| Strategy | возможности, ресурсы, направления действий |
| Business | бизнес-роли, процессы, услуги, объекты |
| Application | приложения, сервисы приложений, данные |
| Technology | инфраструктура и технологические сервисы |
| Physical | физические объекты, оборудование, материалы |
| Implementation & Migration | проекты, пакеты работ, разрывы, состояния |

Внутри основных слоев элементы часто можно понимать через три аспекта:

1. активная структура;
2. поведение;
3. пассивная структура.

Эта логика очень важна для понимания ArchiMate.

## 5.6. Три аспекта: активная структура, поведение, пассивная структура

При описании компании через три основных архитектурных слоя (бизнес, приложения и данные, технологии) всегда можно задать три вопроса:

```text
Кто или что действует?
Что выполняется?
Над чем выполняется действие?
```

Этим вопросам соответствуют три аспекта (Таблица 5.5)

**Таблица 5.5.** Аспекты ArchiMate

| Вопрос | Аспект | Примеры |
|---|---|---|
| Кто или что действует? | Active Structure | роль, приложение, сервер |
| Что выполняется? | Behavior | процесс, функция, сервис |
| Над чем выполняется действие? | Passive Structure | бизнес-объект, объект данных, артефакт |

**Таблица 5.6.** Пример для бизнес-слоя

| Аспект | Элемент RetailPro |
|---|---|
| Active Structure | Маркетолог |
| Behavior | Подготовить маркетинговую кампанию |
| Passive Structure | Маркетинговая кампания |

Смысл:

```text
Маркетолог выполняет процесс подготовки кампании, который работает с бизнес-объектом «Маркетинговая кампания».
```

**Таблица 5.7.** Пример для слоя приложений

| Аспект | Элемент RetailPro |
|---|---|
| Active Structure | CDP |
| Behavior | Управление профилем клиента |
| Passive Structure | Профиль клиента |

Смысл:

```text
CDP реализует сервис управления профилем клиента, который использует объект данных «Профиль клиента».
```

**Таблица 5.8.** Пример для технологического слоя

| Аспект | Элемент RetailPro |
|---|---|
| Active Structure | Cloud Platform |
| Behavior | Database Hosting |
| Passive Structure | customer_profile_table.sql |

**Смысл:**

```text
Облачная платформа предоставляет сервис размещения базы данных, на которой физически хранится артефакт customer_profile_table.sql.
```

**Таблица 5.9.** Сводная таблица аспектов

| Слой | Active Structure | Behavior | Passive Structure |
|---|---|---|---|
| Business | Business Actor, Business Role | Business Process, Business Service | Business Object |
| Application | Application Component | Application Function, Application Service | Data Object |
| Technology | Node, Device, System Software | Technology Function, Technology Service | Artifact |
| Physical | Equipment, Facility | Physical Process | Material |

## 5.7. Мотивационные элементы ArchiMate

Мотивационные элементы помогают объяснить, почему архитектура должна измениться.

**Таблица 5.10.** Мотивационные элементы

| Элемент | Смысл | ArchiMate | Пример RetailPro |
|---|---|---|---|
| Stakeholder | заинтересованное лицо | <img src="images/icon-04.png" alt="Иллюстрация" width="131"> | директор по маркетингу |
| Driver | фактор изменений | <img src="images/icon-05.png" alt="Иллюстрация" width="131"> | рост конкуренции |
| Assessment | оценка ситуации | <img src="images/icon-06.png" alt="Иллюстрация" width="133"> | разрозненные данные |
| Goal | желаемое состояние | <img src="images/icon-07.png" alt="Иллюстрация" width="133"> | увеличить повторные продажи |
| Outcome | измеримый результат | <img src="images/icon-08.png" alt="Иллюстрация" width="136"> | рост LTV |
| Requirement | необходимое свойство решения | <img src="images/icon-09.png" alt="Иллюстрация" width="136"> | единый профиль клиента |
| Principle | правило проектирования | <img src="images/icon-10.png" alt="Иллюстрация" width="142"> | API-first |

**Примечание:** В версиях ArchiMate 3.X присутствовал элемент constraint (ограничение), однако он исключен из версии 4.0, поскольку все ограничения можно описать как requirement.

Ниже приводятся более формальные определения элементов ArchiMate, предназначенных для описания мотивации:

**Stakeholder** – это лицо, группа, подразделение или организация, имеющие интерес к архитектуре или затрагиваемые архитектурными изменениями.

**Driver** – это внутренний или внешний фактор, который мотивирует организацию изменяться.

**Assessment** – это результат оценки влияния drivers на организацию. Assessment может описывать проблему, риск, возможность или слабое место.

Driver и Assessment: Driver – фактор. Assessment – оценка состояния компании относительно этого фактора.

Одной из практик идентификации Assessments является SWOT анализ, суждения о сильных и слабых сторонах компании, угрозах и возможностях можно включать в модель мотивации. Но при этом важно, что эти суждения должны быть ассоциированы с конкретными заинтересованными лицами и их драйверами.

**Goal** – это желаемое состояние или результат, которого хочет достичь организация.

**Outcome** – это конкретный, обычно измеримый результат достижения цели.

Outcome и Goal: Goal описывает желаемое направление, а outcome — наблюдаемый эффект.

**Requirement** – это необходимое свойство архитектуры, системы, процесса или решения, которое должно быть реализовано для достижения целей. Этот элемент отвечает на вопрос «что необходимо обеспечить?».

**Constraint** – это ограничение, которое должно соблюдаться при проектировании или реализации архитектуры. Этот элемент исключен из версии ArchiMate 4.0, предлагается описывать ограничения как требования.

**Principle** – это общее правило или руководство, которое должно направлять архитектурные решения.

Пример мотивационной модели

```plantuml
@startuml
!include <archimate/Archimate>
Left to right direction

title Motivation View: RetailPro

Motivation_Stakeholder(st_cmo, "Директор по маркетингу")
Motivation_Driver(drv_competition, "Рост конкуренции")
Motivation_Assessment(ass_fragmented_data, "Разрозненные\nклиентские данные")
Motivation_Goal(goal_repeat_sales, "Увеличить повторные\nпродажи")
Motivation_Outcome(out_ltv_growth, "Рост LTV")
Motivation_Requirement(req_single_profile, "Единый профиль клиента")
Motivation_Principle(pr_privacy, "Privacy by design")

Rel_Association(st_cmo, drv_competition)
Rel_Influence(drv_competition, ass_fragmented_data)
Rel_Influence(ass_fragmented_data, goal_repeat_sales)
Rel_Realization(goal_repeat_sales, out_ltv_growth)
Rel_Influence(req_single_profile, goal_repeat_sales)
Rel_Influence(pr_privacy, req_single_profile)

@enduml
```

![Рис. 5.2. Мотивационное представление RetailPro.](images/fig-5-2.png)

Рис. 5.2. Мотивационное представление RetailPro.

Как читать эту модель:

```text
Директор по маркетингу заинтересован в реакции на рост конкуренции.
Рост конкуренции выявляет проблему разрозненных клиентских данных.
Эта проблема влияет на цель увеличения повторных продаж.
Измеримым результатом достижения этой цели будет рост LTV.
Для достижения цели требуется единый профиль клиента.
Принцип Privacy by design влияет на реализацию этого требования.
```

## 5.8. Стратегические элементы ArchiMate

Стратегический слой показывает, какие способности и ресурсы нужны организации для достижения целей.

**Таблица 5.11.** Стратегические элементы

| Элемент | Смысл | ArchiMate | Пример RetailPro |
|---|---|---|---|
| Capability | способность организации | <img src="images/icon-12.png" alt="Иллюстрация" width="146"> | клиентская аналитика |
| Resource | актив или ресурс | <img src="images/icon-13.png" alt="Иллюстрация" width="146"> | клиентские данные |
| Course of Action | направление действий | <img src="images/icon-14.png" alt="Иллюстрация" width="146"> | развить омниканальную персонализацию |
| Value Stream | поток создания ценности | <img src="images/icon-15.png" alt="Иллюстрация" width="146"> | персонализировать клиентское взаимодействие |

Определения и комментарии:

**Capability** – это способность организации выполнять определенный вид деятельности или достигать определенного результата.

**Resource** – это актив, которым располагает организация и который используется для реализации capabilities.

Важно различать стратегический ресурс и объект данных. Resource идентифицируется и обсуждается на стратегическом уровне, Data Object – на прикладном уровне.

**Course of Action** – это выбранный подход или направление действий, с помощью которого организация намерена достичь целей или развить capabilities.

Course of Action и Work Package: Course of Action – стратегическое направление. Work Package – конкретная работа или проект.

**Value Stream** — это последовательность этапов, через которые создается ценность для заинтересованного лица.

Value Stream и Business Process: Value Stream показывает этапы создания ценности, а процесс показывает конкретную операционную логику.

Пример стратегической модели

```plantuml
@startuml
!include <archimate/Archimate>

title Strategy View: RetailPro

Motivation_Goal(goal_repeat_sales, "Увеличить повторные\nпродажи")

Strategy_Capability(cap_customer_data, "Управление\nклиентскими данными")
Strategy_Capability(cap_customer_analytics, "Клиентская аналитика")
Strategy_Capability(cap_campaign_management, "Управление кампаниями")
Strategy_CourseOfAction(coa_omnichannel, "Развить омниканальную\nперсонализацию")
Strategy_Resource(res_customer_data, "Клиентские данные")

Rel_Influence(cap_customer_analytics, goal_repeat_sales)
Rel_Influence(cap_campaign_management, goal_repeat_sales)
Rel_Influence(coa_omnichannel, cap_customer_analytics)
Rel_Influence(cap_customer_data, goal_repeat_sales)
Rel_Association(res_customer_data, cap_customer_data)

@enduml
```

![Рис. 5.3. Стратегическое представление RetailPro](images/fig-5-3.png)

Рис. 5.3. Стратегическое представление RetailPro

Как читать модель:

```text
Для увеличения повторных продаж RetailPro должна развивать клиентскую аналитику и управление кампаниями. Направление действий — омниканальная персонализация. Ключевой ресурс — клиентские данные.
```

**Связь мотивационных и стратегических моделей**

Модель мотивации показывает, **зачем** нужны изменения. Стратегическая модель показывает, **какие способности и направления действий** нужны для достижения целей.

Типовая цепочка моделирования:

```text
Stakeholder
↓
Driver
↓
Assessment
↓
Goal
↓
Outcome
↓
Requirement
↓
Course of Action
↓
Capability
↓
Resource
```

Пример RetailPro

```text
Stakeholder: Директор по маркетингу

Driver: Ожидание персональных предложений

Assessment: Низкая персонализация предложений

Goal: Увеличить повторные продажи

Outcome: Повторные продажи +15%

Requirement: Единый профиль клиента

Course of Action: Централизовать клиентские данные

Capability: Управление клиентскими данными

Resource: Клиентские данные
```

Модель PlantUML

```plantuml
@startuml
!include <archimate/Archimate>

title Связь мотивационного и стратегического слоя RetailPro

' === Motivation ===
Motivation_Stakeholder(stk_cmo, “Директор\nпо маркетингу”)
Motivation_Driver(drv_customer_expectations, "Ожидание персональных\nпредложений")
Motivation_Assessment(ass_low_personalization, "Низкая персонализация\nпредложений")
Motivation_Goal(goal_repeat_sales, "Увеличить повторные\nпродажи")
Motivation_Outcome(out_repeat_sales_15, "Повторные продажи\n+15%")
Motivation_Requirement(req_single_profile, "Единый профиль клиента")

' === Strategy ===
Strategy_CourseOfAction(coa_centralize_data, "Централизовать\nклиентские данные")
Strategy_Capability(cap_customer_data, "Управление\nклиентскими данными")
Strategy_Capability(cap_customer_analytics, "Клиентская аналитика")
Strategy_Resource(res_customer_data, "Клиентские данные")

' === Relations ===
Rel_Association(stk_cmo,drv_customer_expectations)
Rel_Association(stk_cmo, ass_low_personalization)

Rel_Influence(drv_customer_expectations, ass_low_personalization)
Rel_Influence(ass_low_personalization, goal_repeat_sales)
Rel_Realization(goal_repeat_sales, out_repeat_sales_15)
Rel_Influence(req_single_profile, goal_repeat_sales)

Rel_Influence(coa_centralize_data, req_single_profile)
Rel_Influence(coa_centralize_data, cap_customer_data)
Rel_Realization(cap_customer_data, goal_repeat_sales)
Rel_Realization(cap_customer_analytics, goal_repeat_sales)

Rel_Association(res_customer_data, cap_customer_data)
Rel_Association(res_customer_data, cap_customer_analytics)

@enduml
```

![Рис. 5.4. Мотивационно-стратегическая модель RetailPro](images/fig-5-4.png)

Рис. 5.4. Мотивационно-стратегическая модель RetailPro

## 5.9. Бизнес-элементы ArchiMate

Бизнес-слой ArchiMate описывает организацию, ее деятельность, участников, бизнес-процессы, бизнес-объекты и бизнес-услуги.

**Таблица 5.12.** Элементы бизнес-слоя

| Элемент | Смысл | ArchiMate | Пример RetailPro |
|---|---|---|---|
| Business Actor | Подразделение или участник | <img src="images/icon-18.png" alt="Иллюстрация" width="126"> | Отдел маркетинга |
| Business Role | Роль | <img src="images/icon-19.png" alt="Иллюстрация" width="126"> | Маркетолог |
| Business Process | Процесс | <img src="images/icon-20.png" alt="Иллюстрация" width="126"> | Подготовить кампанию |
| Business Function | Функция | <img src="images/icon-21.png" alt="Иллюстрация" width="126"> | Маркетинг |
| Business Event | Событие | <img src="images/icon-22.png" alt="Иллюстрация" width="126"> | Начало сезонной акции |
| Business Service | Услуга | <img src="images/icon-23.png" alt="Иллюстрация" width="132"> | Персональное предложение |
| Business Object | Бизнес-понятие | <img src="images/icon-24.png" alt="Иллюстрация" width="132"> | Клиент, кампания, договор |
| Business Collaboration | Объединение ролей или акторов | <img src="images/icon-25.png" alt="Иллюстрация" width="126"> | Команда из маркетолога, аналитика и юриста |
| Business Interaction | Поведение business collaboration | <img src="images/icon-26.png" alt="Иллюстрация" width="132"> | Согласовать параметры компании |
| Product | Продукт | <img src="images/icon-27.png" alt="Иллюстрация" width="136"> | Программа лояльности |

Определения и комментарии:

**Business Actor** — это организационная единица, человек, группа людей или внешний участник, который способен выполнять бизнес-роли или участвовать в бизнес-поведении.

**Business Role** – это роль или ответственность, которую выполняет Business Actor. Один актор может выполнять несколько ролей. Одна роль может выполняться разными акторами.

**Business Process** – это последовательность бизнес-действий, направленная на достижение определенного результата.

**Business Function** – это устойчивая область бизнес-деятельности, объединяющая сходное поведение.

**Таблица 5.13.** Примеры бизнес-функций и бизнес-процессов

| Business Function | Business Process |
|---|---|
| Маркетинг | Подготовить кампанию |
| Продажи | Оформить покупку |
| Клиентская поддержка | Обработать обращение |
| Управление данными | Обновить профиль клиента |
| Управление лояльностью | Начислить бонусы |

Business function и Capability: Capability отвечает на вопрос «что организация должна уметь», Business Function определяет «какая деятельность выполняется».

**Business Event** – это событие, значимое для бизнеса, которое может запускать процесс или быть результатом процесса.

**Business Object** – это пассивный объект или сущность предметной области, с которыми работают бизнес-процессы и бизнес-функции.

Business Object – понятие бизнеса. Data Object – цифровое представление в приложении. Data Object, как правило, является реализацией бизнес-объекта.

**Business Service** – это поведение, которое бизнес предоставляет внешнему или внутреннему потребителю и которое имеет ценность для него.

Когда нужно показать совместную работу нескольких ролей или акторов, используются элементы:

**Business Collaboration** – это объединение двух или более бизнес-ролей или акторов, работающих совместно.

**Business Interaction** – это поведение, выполняемое Business Collaboration.

Иногда для более точного описания бизнеса используются элементы:

**Business Interface** – это точка доступа к бизнес-услуге. Это аналогия Application Interface, который показывает канал взаимодействия с Application Component (например, API). Business Interface описывает каналы взаимодействия с Business Service. В случае RetailPro доступ к сервису «Предоставление персонального предложения» может осуществляться через интерфейсы Web-канал или POS-канал.

**Representation** – это форма представления бизнес-объекта. Например, бизнес-объект «Персональное предложение» может быть представлен как «Email- предложение» или «Электронный купон».

Пример модели бизнеса

```plantuml
@startuml
!include <archimate/Archimate>

left to right direction

title Business View: RetailPro

Business_Actor(ba_marketing, "Отдел маркетинга")
Business_Role(br_marketer, "Маркетолог")
Business_Role(br_analyst, "Аналитик данных")

Business_Event(be_season_start, "Начало сезонной акции")

Business_Process(bp_prepare_campaign, "Подготовить кампанию")
Business_Process(bp_segment_customers, "Сегментировать клиентов")
Business_Process(bp_send_offer, "Отправить предложение")

Business_Object(bo_campaign, "Кампания")
Business_Object(bo_customer_segment, "Клиентский сегмент")
Business_Object(bo_offer, "Персональное предложение")

Business_Service(bs_personal_offer, "Предоставление\nперсонального предложения")

Rel_Assignment(ba_marketing, br_marketer)
Rel_Assignment(ba_marketing, br_analyst)

Rel_Assignment(br_marketer, bp_prepare_campaign)
Rel_Assignment(br_analyst, bp_segment_customers)
Rel_Assignment(br_marketer, bp_send_offer)

Rel_Triggering(be_season_start, bp_prepare_campaign)
Rel_Triggering(bp_prepare_campaign, bp_segment_customers)
Rel_Triggering(bp_segment_customers, bp_send_offer)

Rel_Access(bp_prepare_campaign, bo_campaign)
Rel_Access(bp_segment_customers, bo_customer_segment)
Rel_Access(bp_send_offer, bo_offer)

Rel_Realization(bp_send_offer, bs_personal_offer)

@enduml
```

![Рис. 5.5. Бизнес-представление RetailPro](images/fig-5-5.png)

Рис. 5.5. Бизнес-представление RetailPro

**Связь между бизнес-процессами и бизнес-функциями**

Выше уже обсуждалось различие между бизнес-функциями и бизнес-процессами, а также степень детализации, которая необходима и достаточна для моделирования бизнеса.

На практике бизнес-процессы часто пересекают несколько функциональных областей, причем каждая функция выполняется отдельным подразделением предприятия. В таком случае на уровне архитектурной моделей достаточно показать общий процесс, а его шаги смоделировать как функции, выполняемые разными ролями. Это тем более справедливо, что разные подразделения используют собственные прикладные функции.

Пример RetailPro

```text
Заявка на закупку создается департаментом логистики и проходит согласование планового и финансового отделов. Каждое подразделение использует специализированные функции единой ERP системы.
```

Пример PlantUML

```plantuml
@startuml
!include <archimate/Archimate>

left to right direction

title Согласование заявки на закупку в ERP (ArchiMate)

' --- БИЗНЕС-СЛОЙ (Business Layer) ---
Business_Actor(log_dept, "Департамент\nлогистики")
Business_Actor(plan_dept, "Плановый\nотдел")
Business_Actor(fin_dept, "Финансовый\nотдел")

Business_Process(proc_po, "Согласование заявки на закупку")  {
  Business_Function(fn_create, "Создание заявки\nна закупку")
  Business_Function(fn_plan_appr, "Согласование\nлимитов")
  Business_Function(fn_fin_appr, "Финансовое\nутверждение")
}

' --- СЛОЙ ПРИЛОЖЕНИЙ (Application Layer) ---
Application_Component(erp_system, "Единая ERP-система")  {
   Application_Function(mod_log, "Модуль\nлогистики")
   Application_Function(mod_plan, "Модуль\nпланирования")
   Application_Function(mod_fin, "Финансовый\nмодуль")
  }

' --- СВЯЗИ И СТРУКТУРА ---

' Закрепление процессов за отделами (Назначение / Assignment)
Rel_Assignment(log_dept, fn_create)
Rel_Assignment(plan_dept, fn_plan_appr)
Rel_Assignment(fin_dept, fn_fin_appr)

' Последовательность бизнес-процессов (Flow)
Rel_Triggering(fn_create, fn_plan_appr)
Rel_Triggering(fn_plan_appr, fn_fin_appr)

' Использование функций ERP-системы (Serving / Использование)
Rel_Serving(mod_log, fn_create)
Rel_Serving(mod_plan, fn_plan_appr)
Rel_Serving(mod_fin, fn_fin_appr)
@enduml
```

![Рис. 5.6. Модель связи бизнес-процесса и бизнес-функций](images/fig-5-6.png)

Рис. 5.6. Модель связи бизнес-процесса и бизнес-функций

Для детального моделирования бизнес-процесса и участвующих в его реализации функциональных подразделений лучше использовать BPMN.

**Связь бизнес-слоя с мотивационным и стратегическим слоями**

Бизнес-слой не существует отдельно. Он должен быть связан с мотивацией и стратегией.

Типовая цепочка:

```text
Goal
↓
Capability
↓
Business Process
↓
Business Service
```

Пример RetailPro

```text
Goal: Увеличить повторные продажи

Capability: Клиентская аналитика

Business Process: Сегментировать клиентов

Business Service: Предоставление персонального предложения
```

## 5.10. Прикладные элементы ArchiMate

Прикладной слой описывает информационные системы, их сервисы, функции, интерфейсы, данные и взаимодействия. Прикладной слой должен показывать, как приложения поддерживают бизнес.

**Таблица 5.14.** Элементы слоя приложений и данных

| Элемент | Смысл | ArchiMate | Пример RetailPro |
|---|---|---|---|
| Application Component | приложение или модуль | <img src="images/icon-30.png" alt="Иллюстрация" width="143"> | CDP |
| Application Service | сервис, предоставляемый приложением | <img src="images/icon-31.png" alt="Иллюстрация" width="143"> | управление профилем клиента |
| Application Function | функция внутри приложения | <img src="images/icon-32.png" alt="Иллюстрация" width="143"> | расчет сегмента |
| Application Process | прикладной процесс | <img src="images/icon-33.png" alt="Иллюстрация" width="143"> | обновить профиль клиента |
| Application Interface | интерфейс | <img src="images/icon-34.png" alt="Иллюстрация" width="143"> | Customer API |
| Data Object | данные приложения | <img src="images/icon-35.png" alt="Иллюстрация" width="148"> | профиль клиента |

Определения:

**Application Component** – это модульная, развертываемая или логически выделенная часть информационной системы, которая предоставляет прикладное поведение.

**Application Service** – это функциональность, которую приложение предоставляет пользователям, бизнес-процессам или другим приложениям.

**Application Function** – это внутреннее поведение приложения, сгруппированное по назначению.

**Application Process** – это последовательность прикладного поведения, выполняемая приложением.

**Application Event** – это событие, значимое на прикладном уровне, которое может запускать прикладной процесс или быть результатом прикладного процесса.

**Application Interface** – это точка доступа, через которую прикладной сервис становится доступен пользователям или другим приложениям.

Когда нужно показать совместную работу нескольких приложений, используются элементы:

**Application Collaboration** – это объединение нескольких приложений, совместно выполняющих поведение.

**Application Interaction** – это поведение, выполняемое несколькими приложениями совместно.

Пример прикладной модели

```plantuml
@startuml
!include <archimate/Archimate>

title Application View: RetailPro

Application_Component(app_crm, "CRM")
Application_Component(app_pos, "POS")
Application_Component(app_webshop, "Интернет-магазин")
Application_Component(app_cdp, "CDP")
Application_Component(app_analytics, "Аналитическая платформа")
Application_Component(app_email, "Система рассылок")

Application_Service(as_customer_profile, "Управление\nпрофилем клиента")
Application_Service(as_segmentation, "Сегментация клиентов")
Application_Service(as_email_delivery, "Доставка email")

Application_Interface(ai_customer_api, "Customer API")

Application_DataObject(data_customer_profile, "Профиль клиента")
Application_DataObject(data_purchase_history, "История покупок")
Application_DataObject(data_segment, "Клиентский сегмент")

Rel_Realization(app_cdp, as_customer_profile)
Rel_Realization(app_analytics, as_segmentation)
Rel_Realization(app_email, as_email_delivery)

Rel_Assignment(app_cdp, ai_customer_api)

Rel_Access(app_cdp, data_customer_profile)
Rel_Access(app_cdp, data_purchase_history)
Rel_Access(app_analytics, data_segment)

Rel_Flow(app_crm, app_cdp, "данные клиента")
Rel_Flow(app_pos, app_cdp, "покупки")
Rel_Flow(app_webshop, app_cdp, "онлайн-заказы")
Rel_Flow(app_cdp, app_analytics, "профиль и покупки")
Rel_Flow(app_analytics, app_email, "сегменты")

@enduml
```

![Рис. 5.7. Прикладное представление RetailPro](images/fig-5-7.png)

Рис. 5.7. Прикладное представление RetailPro

## 5.11. Технологические элементы ArchiMate

Технологический слой ArchiMate описывает инфраструктуру, платформы, системное программное обеспечение, сети, устройства, технологические сервисы и физические артефакты, которые поддерживают прикладный слой.

**Таблица 5.15.** Элементы технологического слоя

| Элемент | Смысл | ArchiMate | Пример RetailPro |
|---|---|---|---|
| Node | вычислительный узел | <img src="images/icon-37.png" alt="Иллюстрация" width="128"> | Cloud Platform |
| Device | физическое устройство | <img src="images/icon-38.png" alt="Иллюстрация" width="128"> | POS-терминал |
| System Software | системное ПО | <img src="images/icon-39.png" alt="Иллюстрация" width="128"> | Kubernetes, PostgreSQL |
| Technology Service | технологический сервис | <img src="images/icon-40.png" alt="Иллюстрация" width="128"> | Database Hosting |
| Technology Interface | технологический интерфейс | <img src="images/icon-41.png" alt="Иллюстрация" width="128"> | HTTPS endpoint |
| Artifact | физический файл или компонент | <img src="images/icon-42.png" alt="Иллюстрация" width="128"> | customer-service.jar |
| Communication Network | сеть | <img src="images/icon-43.png" alt="Иллюстрация" width="133"> | корпоративная сеть |

Определения:

**Node** — это вычислительный или инфраструктурный ресурс, на котором могут размещаться системное ПО, приложения или артефакты.

**Device** — это физический ИТ-ресурс, который выполняет вычисления, хранение, ввод-вывод или коммуникации.

**System Software** — это программное обеспечение, которое предоставляет технологическую среду для приложений и технологических сервисов.

**Technology Service** — это технологическая функциональность, предоставляемая инфраструктурой, платформой или системным ПО приложениям или другим технологическим элементам.

**Technology Interface** — это точка доступа к технологическому сервису.

**Artifact** — это физический или развертываемый объект, например файл, исполняемый компонент, конфигурация, схема базы данных или контейнерный образ.

Data Object — логический объект данных. Artifact — физическая реализация или файл.

**Communication Network** — это коммуникационная сеть, обеспечивающая связь между устройствами и узлами.

Пример технологической модели

```plantuml
@startuml
!include <archimate/Archimate>

title Technology View: RetailPro

Technology_Node(node_cloud, "Cloud Platform")
Technology_Node(node_store, "Магазин")

Technology_Device(dev_pos_terminal, "POS-терминал")

Technology_SystemSoftware(sw_api_gateway, "API Gateway")
Technology_SystemSoftware(sw_message_broker, "Message Broker")
Technology_SystemSoftware(sw_dwh, "Cloud Data Warehouse")
Technology_SystemSoftware(sw_monitoring, "Monitoring Platform")

Technology_Service(ts_api_management, "API Management")
Technology_Service(ts_event_delivery, "Event Delivery")
Technology_Service(ts_data_storage, "Data Storage")
Technology_Service(ts_monitoring, "Monitoring")

Rel_Composition(node_cloud, sw_api_gateway)
Rel_Composition(node_cloud, sw_message_broker)
Rel_Composition(node_cloud, sw_dwh)
Rel_Composition(node_cloud, sw_monitoring)
Rel_Composition(node_store, dev_pos_terminal)

Rel_Realization(sw_api_gateway, ts_api_management)
Rel_Realization(sw_message_broker, ts_event_delivery)
Rel_Realization(sw_dwh, ts_data_storage)
Rel_Realization(sw_monitoring, ts_monitoring)

Rel_Flow(dev_pos_terminal, sw_api_gateway, "purchase event")
Rel_Flow(sw_api_gateway, sw_message_broker, "validated event")

@enduml
```

![Рис. 5.8. Технологическое представление RetailPro](images/fig-5-8.png)

Рис. 5.8. Технологическое представление RetailPro

## 5.12. Элементы для описания реализации и миграции

Эти элементы помогают описывать переход от текущей архитектуры к целевой.

**Таблица 5.16.** Элементы реализации и миграции

| Элемент | Смысл | ArchiMate | Пример RetailPro |
|---|---|---|---|
| Work Package | пакет работ или проект | <img src="images/icon-45.png" alt="Иллюстрация" width="116"> | внедрить CDP |
| Deliverable | результат работы | <img src="images/icon-46.png" alt="Иллюстрация" width="116"> | Customer API |
| Implementation Event | событие реализации | <img src="images/icon-47.png" alt="Иллюстрация" width="116"> | запуск CDP |
| Plateau | устойчивое состояние архитектуры | <img src="images/icon-48.png" alt="Иллюстрация" width="116"> | целевая архитектура |
| Gap | разрыв между состояниями | <img src="images/icon-49.png" alt="Иллюстрация" width="116"> | нет единого профиля клиента |

Определения:

**Gap** — это разрыв между двумя архитектурными состояниями. Этот элемент отвечает на вопрос: чего не хватает в текущем состоянии для достижения целевого состояния?

**Gap-анализ** — это метод сравнения текущей архитектуры с целевой архитектурой для выявления разрывов, которые необходимо устранить, чтобы перейти к желаемому состоянию.

Разрывы удобно классифицировать по слоям архитектуры:

- **Business gap** — разрыв в бизнес-процессах, ролях, услугах или способностях.
- **Data gap** — разрыв в данных, их качестве, структуре, владении или доступности.
- **Application gap** — разрыв в приложениях, сервисах, интерфейсах или интеграциях.
- **Technology gap** — разрыв в инфраструктуре, платформах, системном ПО или технологических сервисах.
- **Governance gap** — разрыв в правилах управления, ответственности и контроле.

**Work Package** — это набор работ, проект, программа, инициатива или задача, направленные на реализацию изменений архитектуры.

**Deliverable** — это конкретный результат, создаваемый work package.

**Implementation Event** — это событие, связанное с реализацией, запуском или завершением архитектурного изменения.

**Plateau** — это относительно устойчивое состояние архитектуры в определенный момент времени.

Пример миграционной модели

```plantuml
@startuml
!include <archimate/Archimate>

title Migration View: RetailPro

Implementation_Plateau(pl_baseline, "Baseline:\nразрозненные данные")
Implementation_Plateau(pl_transition, "Transition:\nCDP внедрена")
Implementation_Plateau(pl_target, "Target:\nперсонализация\nво всех каналах")

Implementation_Gap(gap_no_single_profile, "Нет единого\nпрофиля клиента")
Implementation_Gap(gap_manual_campaigns, "Ручные кампании")

Implementation_WorkPackage(wp_data_audit, "Аудит данных")
Implementation_WorkPackage(wp_implement_cdp, "Внедрить CDP")
Implementation_WorkPackage(wp_campaign_automation, "Автоматизировать\nкампании")

Implementation_Deliverable(del_customer_api, "Customer API")
Implementation_Deliverable(del_segment_model, "Модель сегментации")

Rel_Triggering(pl_baseline, pl_transition)
Rel_Triggering(pl_transition, pl_target)

Rel_Association(pl_baseline, gap_no_single_profile)
Rel_Association(pl_transition, gap_manual_campaigns)

Rel_Association(wp_data_audit, gap_no_single_profile)
Rel_Association(wp_implement_cdp, gap_no_single_profile)
Rel_Association(wp_campaign_automation, gap_manual_campaigns)

Rel_Realization(wp_implement_cdp, del_customer_api)
Rel_Realization(wp_campaign_automation, del_segment_model)

@enduml
```

![Рис. 5.9. Миграционное представление RetailPro](images/fig-5-9.png)

Рис. 5.9. Миграционное представление RetailPro

**Связь Work Package, Gap, Requirement и Target Element**

Модель миграции становится полезной, когда показывает не просто список проектов, а архитектурную логику:

```text
Requirement
↓
Gap
↓
Work Package
↓
Deliverable
↓
Target Architecture Element
```

Пример RetailPro

```text
Requirement: Единый профиль клиента

Gap: Нет единого профиля клиента

Work Package: Внедрить CDP

Deliverable: Настроенная CDP

Target Element: Application Component - CDP, Data Object - Customer Profile
```

Модель PlantUML

```plantuml
@startuml
!include <archimate/Archimate>

title Связь Requirement, Gap, Work Package и Target Element

Motivation_Requirement(req_single_profile, "REQ-01:\nЕдиный профиль клиента")

Implementation_Gap(gap_no_single_profile, "GAP-01:\nНет единого\nпрофиля клиента")

Implementation_WorkPackage(wp_implement_cdp, "WP:\nВнедрить CDP")
Implementation_Deliverable(del_configured_cdp, "Настроенная CDP")

Application_Component(app_cdp, "CDP")
Application_DataObject(data_customer_profile, "Customer Profile")
Application_Service(as_customer_profile, "Управление профилем клиента")

Rel_Association(gap_no_single_profile, req_single_profile)
Rel_Association(wp_implement_cdp, gap_no_single_profile)

Rel_Realization(wp_implement_cdp, del_configured_cdp)
Rel_Realization(wp_implement_cdp, app_cdp)

Rel_Realization(app_cdp, as_customer_profile)
Rel_Access(app_cdp, data_customer_profile)

@enduml
```

![Рис. 5.10. Связь требований, разрывов, пакетов работ и целевых элементов](images/fig-5-10.png)

Рис. 5.10. Связь требований, разрывов, пакетов работ и целевых элементов

## 5.13. Сквозная ArchiMate-модель

Теперь объединим несколько слоев в одну простую модель.

**Модель должна показать цепочку:**

```text
Stakeholder
↓
Goal
↓
Requirement
↓
Business Process
↓
Application Service
↓
Application Component
↓
Data Object
↓
Technology Service
↓
Node
↓
Work Package
```

PlantUML-код сквозной модели

```plantuml
@startuml
!include <archimate/Archimate>

title Первая сквозная ArchiMate-модель RetailPro

' === Motivation ===
Motivation_Stakeholder(st_cmo, "Директор по маркетингу")
Motivation_Goal(goal_repeat_sales, "Увеличить повторные продажи")
Motivation_Requirement(req_single_profile, "Единый профиль клиента")

' === Business ===
Business_Process(bp_segment_customers, "Сегментировать клиентов")
Business_Service(bs_personal_offer, "Персональное предложение")

' === Application ===
Application_Service(as_customer_profile, "Управление профилем клиента")
Application_Component(app_cdp, "CDP")
Application_DataObject(data_customer_profile, "Профиль клиента")

' === Technology ===
Technology_Service(ts_database_hosting, "Database Hosting")
Technology_Node(node_cloud, "Cloud Platform")

' === Implementation ===
Implementation_WorkPackage(wp_implement_cdp, "Внедрить CDP")

' === Relations ===
Rel_Association(st_cmo, goal_repeat_sales)
Rel_Influence(req_single_profile, goal_repeat_sales)

Rel_Realization(bp_segment_customers, bs_personal_offer)
Rel_Serving(as_customer_profile, bp_segment_customers)

Rel_Realization(app_cdp, as_customer_profile)
Rel_Access(app_cdp, data_customer_profile)

Rel_Serving(ts_database_hosting, app_cdp)
Rel_Realization(node_cloud, ts_database_hosting)

Rel_Realization(wp_implement_cdp, app_cdp)
Rel_Association(wp_implement_cdp, req_single_profile)

@enduml
```

![Рис. 5.11. Сквозное представление RetailPro](images/fig-5-11.png)

Рис. 5.11. Сквозное представление RetailPro

Как читать эту модель:

```text
Директор по маркетингу заинтересован в увеличении повторных продаж.
Для достижения этой цели требуется единый профиль клиента.
Бизнес-процесс сегментации клиентов участвует в предоставлении персонального предложения.
Процесс использует прикладной сервис управления профилем клиента.
Этот сервис реализуется CDP.
CDP работает с объектом данных «Профиль клиента».
CDP поддерживается технологическим сервисом Database Hosting.
Этот сервис реализуется облачной платформой.
Пакет работ «Внедрить CDP» реализует соответствующий прикладной компонент.
```

## 5.14. Как именовать элементы ArchiMate

Качество модели сильно зависит от названий элементов.

**Таблица 5.17.** Общие правила именования элементов

| Тип элемента | Хорошее название | Плохое название |
|---|---|---|
| Goal | Увеличить повторные продажи | CDP |
| Requirement | Единый профиль клиента | Сделать красиво |
| Business Process | Сегментировать клиентов | Сегментация |
| Application Component | CDP | Сегментация клиентов |
| Application Service | Управление профилем клиента | CDP |
| Data Object | Профиль клиента | Управлять клиентом |
| Technology Service | Database Hosting | PostgreSQL |
| Node | Cloud Platform | Аналитика |

Рекомендации:

1. **Цели** формулируйте как желаемые бизнес-результаты:

```text
Увеличить повторные продажи
Снизить время обработки заказа
Повысить качество клиентских данных
```

2. **Процессы** формулируйте глаголами:

```text
Сегментировать клиентов
Обработать заказ
Проверить согласие клиента
```

3. **Объекты данных** формулируйте существительными:

```text
Профиль клиента
История покупок
Запись согласия
```

4. **Сервисы** формулируйте как предоставляемую способность:

```text
Управление профилем клиента
Сегментация клиентов
Доставка email-предложений
```

## 5.15. Типичные ошибки при первом знакомстве с ArchiMate

**Ошибка 1. Считать ArchiMate просто набором иконок.** ArchiMate — это не просто визуальная нотация. Важно не только как выглядит элемент, но и что он означает.

**Ошибка 2. Путать слои**

Неверно:

```text
Business Process: CDP
```

Правильно:

```text
Application Component: CDP
```

**Ошибка 3. Путать поведение и структуру**

Неверно:

```text
Application Component: Управление профилем клиента
```

Лучше:

```text
Application Service: Управление профилем клиента
Application Component: CDP
```

**Ошибка 4. Путать объект данных и бизнес-объект**

```text
Business Object: Клиент
Data Object: Профиль клиента
```

**Ошибка 5. Не показывать отношения.** Модель из одних элементов почти бесполезна.

**Ошибка 6. Строить слишком большую диаграмму.** Новички часто пытаются поместить всю архитектуру на одну диаграмму. Лучше создавать несколько представлений.

**Ошибка 7. Использовать ArchiMate вместо BPMN для детального процесса.** ArchiMate хорошо показывает архитектурную роль процесса. Для детального сценария процесса лучше использовать BPMN.

## 5.16. Практикум: распознавание элементов ArchiMate

Исходное описание

```text
RetailPro хочет увеличить повторные продажи.
Для этого директор по маркетингу требует персонализировать предложения.
Проблема состоит в том, что данные о клиентах разрознены между CRM, POS и интернет-магазином.
Компания планирует внедрить CDP, которая будет формировать единый профиль клиента.
Аналитическая платформа будет использовать профиль клиента и историю покупок для сегментации.
Система рассылок будет доставлять персональные предложения клиентам.
Интеграция должна выполняться через API Gateway.
```

**Задание 1.** Выделите элементы и заполните таблицу.

| Фрагмент | Тип ArchiMate | Слой |
|---|---|---|
| RetailPro хочет увеличить повторные продажи | | |
| директор по маркетингу | | |
| персонализировать предложения | | |
| данные о клиентах разрознены | | |
| CRM | | |
| POS | | |
| интернет-магазин | | |
| CDP | | |
| единый профиль клиента | | |
| аналитическая платформа | | |
| история покупок | | |
| система рассылок | | |
| API Gateway | | |

**Задание 2.** Постройте связи, сформулируйте минимум 8 отношений:

**Пример:**

```text
CDP реализует сервис управления профилем клиента.
CDP использует профиль клиента.
POS передает историю покупок в CDP.
```

**Задание 3.** Постройте PlantUML-модель. Используйте заготовку:

```plantuml
@startuml
!include <archimate/Archimate>

title Практикум: первая модель ArchiMate

' Motivation
Motivation_Stakeholder(st_1, "Stakeholder")
Motivation_Goal(goal_1, "Goal")
Motivation_Requirement(req_1, "Requirement")

' Strategy
Strategy_Capability(cap_1, "Capability")

' Business
Business_Process(bp_1, "Business Process")

' Application
Application_Component(app_1, "Application Component")
Application_Service(as_1, "Applicatipn Service")
Application_DataObject(data_1, "Data Object")

' Technology
Technology_SystemSoftware(sw_1, "System Software")

' Relations
Rel_Association(st_1, goal_1)
Rel_Influence(req_1, goal_1)
Rel_Realization(cap_1, goal_1)
Rel_Realization(bp_1, cap_1)
Rel_Serving(as_1, bp_1)
Rel_Realization(app_1, as_1)
Rel_Access(app_1, data_1)
Rel_Serving(sw_1, app_1)

@enduml
```

## 5.17. Практическое задание: создать три представления RetailPro

Создайте три ArchiMate-представления для инициативы RetailPro.

**Представление 1. Motivation View.** Должно включать:

- stakeholder;
- driver;
- assessment;
- goal;
- requirement;
- principle.

**Представление 2. Application View.** Должно включать:

- CRM;
- POS;
- интернет-магазин;
- CDP;
- аналитическую платформу;
- систему рассылок;
- профиль клиента;
- историю покупок;
- потоки данных.

**Представление 3. Migration View.** Должно включать:

- baseline plateau;
- target plateau;
- минимум 2 gaps;
- минимум 3 work packages;
- минимум 2 deliverables.

## 5.18. Контрольные вопросы

1. Что такое ArchiMate?
2. Зачем нужен язык архитектурного моделирования?
3. Чем ArchiMate отличается от TOGAF?
4. Чем ArchiMate отличается от BPMN?
5. Чем ArchiMate отличается от UML?
6. Как PlantUML связан с ArchiMate?
7. Что такое архитектурная модель?
8. Что такое элемент ArchiMate?
9. Что такое отношение ArchiMate?
10. Что такое view?
11. Какие основные группы элементов есть в ArchiMate?
12. Что такое активная структура?
13. Что такое поведение?
14. Что такое пассивная структура?
15. Как отличить Business Object от Data Object?
16. Как отличить Application Component от Application Service?
17. Зачем нужны Implementation & Migration элементы?
18. Какие типичные ошибки возникают при первом моделировании на ArchiMate?

## 5.19. Краткие выводы главы

1. ArchiMate — это язык моделирования архитектуры предприятия.
2. Он нужен для формального описания связей между целями, бизнесом, данными, приложениями, технологиями и изменениями.
3. TOGAF задает процесс архитектурной работы, а ArchiMate помогает моделировать результаты этой работы.
4. BPMN лучше подходит для детального описания процессов, UML — для проектирования программных систем.
5. PlantUML позволяет описывать ArchiMate-диаграммы текстом.
6. ArchiMate организован по слоям и аспектам.
7. Три базовых аспекта — активная структура, поведение и пассивная структура.
8. В бизнес-слое активными элементами являются акторы и роли, поведением — процессы и сервисы, пассивными элементами — бизнес-объекты.
9. В прикладном слое активными элементами являются компоненты приложений, поведением — прикладные сервисы и функции, пассивными элементами — объекты данных.
10. В технологическом слое активными элементами являются узлы и системное ПО, поведением — технологические сервисы, пассивными элементами — артефакты.
11. Implementation & Migration элементы позволяют описывать переход от текущей архитектуры к целевой.
12. Главная ценность ArchiMate — не в отдельных символах, а в смысловых связях между элементами архитектуры.

---

[← Предыдущая глава](../04-adm-method/README.md) · [К оглавлению](../README.md) · [Следующая глава →](../06-archimate-relationships/README.md)
