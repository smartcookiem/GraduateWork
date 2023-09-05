# Дипломный проект по курсу «Тестировщик ПО»

Автоматизировано тестирование комплексного сервиса покупки тура, взаимодействующего с СУБД и API Банка.

Покупка тура возможна двумя способами:

- Оплата по дебетовой карте;
- Кредит по данным банковской карты.

Сервис обрабатывает только специальные номера карт, которые предоставлены для тестирования:

- APPROVED карта - 4444 4444 4444 4441
- DECLINED карта - 4444 4444 4444 4442.

Приложение должно в собственной СУБД сохранять информацию о том, каким способом был совершён платёж, и успешно ли он был совершён (при этом данные карт сохранять не допускается).

### В процессе работы над данным проектом были созданы следующие документы:
1. [План автоматизации тестирования](https://github.com/smartcookiem/GraduateWork/blob/main/documentation/Plan.md)
2. [Отчет по итогам тестирования](https://github.com/smartcookiem/GraduateWork/blob/main/documentation/Report.md)
3. [Отчет по итогам автоматизации](https://github.com/smartcookiem/GraduateWork/blob/main/documentation/Summary.md)

## Запуск
**Необходимое окружение:**

- установленный Docker Desktop;
- Проверить порты 8080, 9999 и 5432 или 3306 (в зависимости от выбранной базы данных) на то, что они не заняты;
- открыть проект в IntelliJ IDEA.

**Инструкция по установке:**

1. Скачайте архив;

2. Запустите контейнер, в котором разворачивается база данных (далее БД) docker-compose up -d --force-recreate

3. Убедитесь в том, что БД готова к работе (логи смотреть через docker-compose logs -f <applicationName> (mysql или postgres)

4. Запустить SUT во вкладке Terminal Intellij IDEA командой:
    
для mysql: java "-Dspring.datasource.url=jdbc:mysql://localhost:3306/app" -jar artifacts/aqa-shop.jar

для postgresql: java "-Dspring.datasource.url=jdbc:postgresql://localhost:5432/app" -jar artifacts/aqa-shop.jar

5. Для запуска авто-тестов в Terminal Intellij IDEA открыть новую сессию и ввести команду:

для mysql: ./gradlew clean test allureReport "-Ddb.url=jdbc:mysql://localhost:3306/app"

для postgresql: ./gradlew clean test allureReport "-Ddb.url=jdbc:postgresql://localhost:5432/app"

6. Для просмотра отчета Allure в терминале ввести команду: ./gradlew allureServe


