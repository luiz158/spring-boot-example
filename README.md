# spring-boot example
some spring boot examples:
* prop-test
* boot-security
* actuator-default
* h2-default


## prop-test

## actuator-default example
1. приложение доступно по следующему url: [http://localhost:8092](http://localhost:8092)
2. доступные конечные точки актуатора:
 - `/autoconfig`
 - `/beans`
 - `/configprops`
 - `/env`
 - `/info`
 - `/metrics`
 - `/logfile`
 - `/trace`

## h2-default example
Spring boot по умолчанию настраивает h2 на работу из памяти
```properties
# h2 data source
spring.datasource.url=jdbc:h2:mem:testdb;DB_CLOSE_ON_EXIT=FALSE;DB_CLOSE_DELAY=-1
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.user=sa
spring.datasource.password=
```

В примере используются настройки по умолчанию. Генерим схему БД по Entity и подгружаем начальные данные из скрипта `data.sql`.
```properties
# generate db scheme
spring.jpa.generate-ddl=true
spring.jpa.hibernate.ddl-auto=create

# load data.sql
spring.datasource.initialize=true
```

Разрешаем в приложении работу с h2 консолью:
```
spring.h2.console.enabled=true
```
Путь к консоли стандартный: `http://localhost:8090/h2-console`

Для простоты реализации пример доступен по REST. 
Примеры http запросов:

* простотреть все записи
 ```http
 GET localhost:8090/items
 ```

* создать третью запись
 ```http
 POST localhost:8090/items 
 Content-Type: application/json
 { 
  "name": "new item",
  "description": "short descr"
 }
 ```

* показать третью запись
 ```http
 GET localhost:8090/items/3
 ```

* запросить доступные функции для поиска
 ```http
 GET localhost:8090/items/search
 ```

* поиск записей по функции
 ```http
 GET localhost:8090/items/search/findByName?name=new%20item
 ```

* отредактировать запись используя PUT, PATCH или DELETE
 ```http
 PUT localhost:8090/items/3
 Content-Type: application/json
 {
   "name": "Item3",
   "description": "long description"
 }
 ```

* удалить запись
 ```http
 DELETE localhost:8090/items/3
 ```
