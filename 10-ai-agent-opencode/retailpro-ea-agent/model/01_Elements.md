# Элементы ArchiMate
Источник: input/retailpro_case.md
Агент: ea-extractor

## Motivation
| ID | Название | Тип ArchiMate | Состояние | Цитата | Уверенность | Примечание |
|---|---|---|---|---|---|---|
| st_retailpro | RetailPro (компания) | Motivation_Stakeholder | As-is | "Компания RetailPro хочет увеличить повторные продажи" | low | Организация как заинтересованное лицо — косвенно следует из текста. Требует проверки архитектором. |
| goal_repeat_sales | Увеличить повторные продажи | Motivation_Goal | To-be | "Компания RetailPro хочет увеличить повторные продажи за счет персональных предложений" | high | |
| ass_client_data | Данные клиентов в CRM, POS и интернет-магазине | Motivation_Assessment | As-is | "Сейчас данные о клиентах хранятся в CRM, POS и интернет-магазине." | high | |
| ass_consent_sync | Согласия клиентов не синхронизированы | Motivation_Assessment | As-is | "Согласия клиентов не синхронизированы." | high | |

## Strategy
| ID | Название | Тип ArchiMate | Состояние | Цитата | Уверенность | Примечание |
|---|---|---|---|---|---|---|
| cap_personalization | Персонализация предложений | Strategy_Capability | To-be | "увеличить повторные продажи за счет персональных предложений" | medium | Выведено из фразы "за счет персональных предложений". Требует проверки архитектором. |

## Business
| ID | Название | Тип ArchiMate | Состояние | Цитата | Уверенность | Примечание |
|---|---|---|---|---|---|---|
| ba_marketers | Маркетологи | Business_Actor | As-is | "Маркетологи формируют сегменты вручную в Excel." | high | |
| bp_segment_manual | Формировать сегменты клиентов | Business_Process | As-is | "Маркетологи формируют сегменты вручную в Excel." | high | Название по правилу: глагол в неопределенной форме. |
| bo_client_segment | Сегмент клиентов | Business_Object | As-is | "формируют сегменты" | medium | Бизнес-понятие предметной области. |
| bs_personalized_offers | Персональные предложения клиентам | Business_Service | To-be | "увеличить повторные продажи за счет персональных предложений" | medium | Выведено косвенно из цели. Требует проверки архитектором. |

## Application
| ID | Название | Тип ArchiMate | Состояние | Цитата | Уверенность | Примечание |
|---|---|---|---|---|---|---|
| app_crm | CRM | Application_Component | As-is | "данные о клиентах хранятся в CRM" | high | |
| app_pos | POS | Application_Component | As-is | "хранятся в CRM, POS и интернет-магазине" | high | |
| app_eshop | Интернет-магазин | Application_Component | As-is | "хранятся в CRM, POS и интернет-магазине" | high | |
| app_excel | Excel | Application_Component | As-is | "формируют сегменты вручную в Excel" | low | Приложение или инструмент конечного пользователя? Требует проверки архитектором. |
| app_cdp | CDP | Application_Component | To-be | "планирует внедрить CDP" | high | Элемент приложения с состоянием To-be, не Work Package. |
| ai_customer_api | Customer API | Application_Interface | To-be | "создать Customer API" | high | |
| app_analytics | Аналитическая платформа | Application_Component | To-be | "использовать аналитическую платформу" | high | |
| as_segmentation | Автоматическая сегментация клиентов | Application_Service | To-be | "аналитическую платформу для автоматической сегментации клиентов" | high | |
| data_client_data | Данные о клиентах | Application_DataObject | As-is | "данные о клиентах хранятся в CRM, POS и интернет-магазине" | high | |
| data_client_consent | Согласия клиентов | Application_DataObject | As-is | "Согласия клиентов не синхронизированы." | high | Данные как хранимая информация в системах. |

## Technology
Не выявлено

## Спорные решения
- st_retailpro: организация "RetailPro" как заинтересованное лицо — косвенно следует из текста ("Компания RetailPro хочет..."), уверенность low. Требует проверки архитектором.
- cap_personalization: "персональные предложения" интерпретированы как способность организации (Capability), а не как бизнес-сервис. Требует проверки архитектором.
- app_excel: Excel — приложение или инструмент конечного пользователя? Требует проверки архитектором.
- bs_personalized_offers: бизнес-сервис выведен косвенно из цели, прямо в тексте не называется. Требует проверки архитектором.

## Подозрительные фрагменты
- нет
