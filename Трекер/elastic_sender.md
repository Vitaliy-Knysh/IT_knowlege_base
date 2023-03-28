[**gitlab**](https://gitlab.aq.ru/factorytesting/python/elastic_sender)

Модуль используется для отправки данных на сервис [**elasticspec**](https://tracker.aq.ru/projects/python/wiki/elastic-spec).

Основная функция - **send\_data(schema, data)**.

*   **schema** - _название схемы, по которой проводится проверка данных и их дополнение_
*   **data** - _отправляемые данные в виде словаря_

Функция возвращает ответ от сервера в виде словаря вида

```json
{
  "result": "bool"
  "errors": "errors descriptions if result is False, list"
  "data": "processed data if result is True, dict"
}
```

Где, если **result** - **True**, отправленные данные записываются в **data** в виде _словаря_;

Если **result** - **False**, список ошибок записывается в **errors** в виде _списка_.

В случае неуспешного соединения с сервисом, либо в случае ответа сервера с кодом, не равным **200**, поднимается исключение **ConnectionError**.