# Контекст решения
<!-- Окружение системы (роли, участники, внешние системы) и связи системы с ним. Диаграмма контекста C4 и текстовое описание. 
Подробнее: https://confluence.mts.ru/pages/viewpage.action?pageId=375783261
-->
```plantuml
@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml

LAYOUT_WITH_LEGEND()

Person(speaker, "Докладчик", "Докладчик на конференции")
Person(client, "Слушатель", "Посетитель конференции")
Person(moderator, "Программный комитет", "Модераторы докладов")

System(cnf, "Сайт конференции", "Позволяет публиковать доклады, проводить модерацию, осуществлять трансляцию докладов.")
System_Ext(es, "E-mail system", "The internal Microsoft Exchange e-mail system.")


Rel(speaker, cnf, "Uses")
Rel(client, cnf, "Uses")
Rel(moderator, cnf, "Uses")
Rel(es, client, "Sends e-mails to")
Rel(cnf, es, "Sends e-mails", "SMTP")

@enduml
```
## Назначение систем
