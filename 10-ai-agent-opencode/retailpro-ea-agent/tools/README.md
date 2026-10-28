# Каталог tools

Здесь должен лежать файл `plantuml.jar` (его использует инструмент
archimate_check). В архив он не включен: это сторонняя программа
(лицензия GPL), ее нужно скачать самостоятельно.

    curl -L -o tools/plantuml.jar \
      https://github.com/plantuml/plantuml/releases/download/v1.2026.8/plantuml-1.2026.8.jar

Проект проверялся с версией 1.2026.8. Нужна Java (JRE 11 или новее).
