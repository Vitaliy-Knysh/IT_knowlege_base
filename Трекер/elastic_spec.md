[gitlab](https://gitlab.aq.ru/factorytesting/python/elastic_spec/)

Посредник для отправки данных в эластик, проводит валидацию и дополнение данных.

_**Схема** - здесь и далее имеется в виду схема по проверке и дополнению данных, отправляемых в эластик._

Основной функционал - **post**\-запрос по адресу _**service\_address/send/**_ с параметрами _schema\_name_ и _data._

*   **schema\_name** - название используемой схемы для отправки данных, _строка_
*   **data** - данные, пересылаемые для отправки, _словарь_

В случае успеха возвращает код **200** со следующей информацией:

```json
{
  "result": "bool"
  "errors": "errors descriptions if result is False, list"
  "data": "processed data if result is True, dict"
}
```

Где, если **result** - **True**, отправленные данные записываются в **data** в виде _словаря_;

Если **result** - **False**, список ошибок записывается в **errors** в виде _списка_.

[Процесс валидации и формирования данных для отправки](https://tracker.aq.ru/projects/python/wiki/protsiess-validatsii-i-formirovaniia-dannykh-dlia-otpravki).

[Список возможных ошибок](https://tracker.aq.ru/projects/python/wiki/spisok-vozmozhnykh-oshibok).

Также возможны следующие запросы:

*   **get**\-запрос _**/schemas\_names**_ - возвращает список сохраненных схем
*   **get**\-запрос _**/refresh**_ - заново собирает схемы и поля из эластика, автоматически выполняется один раз, если схема не была найдена