# Компонентная архитектура
<!-- Состав и взаимосвязи компонентов системы между собой и внешними системами с указанием протоколов, ключевые технологии, используемые для реализации компонентов.
Диаграмма контейнеров C4 и текстовое описание. 
Подробнее: https://confluence.mts.ru/pages/viewpage.action?pageId=375783368
-->
## Компонентная диаграмма

```plantuml
@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml

AddElementTag("microService", $shape=EightSidedShape(), $bgColor="CornflowerBlue", $fontColor="white", $legendText="microservice")
AddElementTag("storage", $shape=RoundedBoxShape(), $bgColor="lightSkyBlue", $fontColor="white")

Person(speaker, "Докладчик", "Докладчик на конференции")

System_Boundary(c, "Сайт конференции") {
   Container(app, "Клиентское веб-приложение", "html, JavaScript, Angular", "Портал конференции")
   Container(client_service, "Сервис авторизации", "C++", "Сервис управления докладчиками", $tags = "microService")    
   Container(scheduling_service, "Сервис расписаний", "C++", "Сервис управления расписанием", $tags = "microService")      
   ContainerDb(scheduling_db, "Данные конференции", "MySQL", "Хранение данных конференции", $tags = "storage")
   
}

Rel(speaker, app, "Регистрация спикера", "HTTPS","/person")
Rel(speaker, app, "Регистрация доклада", "HTTPS","/schedule")

Rel(app, client_service, "Сохранение данных регистрации докладчика", "JSON, HTTPS")
Rel(app, scheduling_service, "Сохранение данных доклада", "JSON, HTTPS")
Rel(client_service, scheduling_db, "Сохранение/чтение данных докладчика", "JDBC, SQL")
Rel(scheduling_service, scheduling_db, "Сохранение/чтение данных доклада", "JDBC, SQL")


SHOW_LEGEND()
@enduml
```
## Список компонентов
### Сервис авторизации
Приложение должно содержать следующие данные:
- Пользователь
- Доклад
- Конференция

**API**:
-	Создание нового пользователя
-	Поиск пользователя по логину
-	Поиск пользователя по маске имя и фамилии

### Сервис расписаний
Приложение должно содержать следующие данные:
- Доклад
- Конференция

**API**:
-	Создание доклада
-	Получение списка всех докладов
-	Добавление доклада в конференцию
-	Получение списка докладов в конференции
