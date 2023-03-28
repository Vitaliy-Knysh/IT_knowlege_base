[gitlab](https://gitlab.aq.ru/factorytesting/python/consul_interactions)

Служит для получения информации из консула.

Текущие функции:

*   **get\_zone\_id** - возвращает **zone\_id**, если прописан, иначе - **None**
*   **get\_pymssql\_connection\_data** - возвращает данные о подключении к **mssql** БД завода в формате

```json
{"server": "host",
"user": "login",
"port": "port",
"password": "password",
"database": "database",
"timeout": 3}
```

Возможные исключения - **KeyError**(&quot;Ошибка получения factory db, {e.\_\_repr\_\_()}&quot;), **ValueError**(f&quot;Unknown factory\_db: {factory\_db\_type}&quot;)

*   **get\_elastic\_connection\_data** - возвращает данные о подключение к **elasticsearch** в формате

```json
{"hosts": ["host"],
"basic_auth": ["local_elastic_login", "local_elastic_pwd"],
"verify_certs": false,
"ssl_show_warn": false}
```