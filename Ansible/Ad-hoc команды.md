Ad-hoc команды - это единичные команды, вызываемые прямо из терминала: `ansible <команда>`

пример: `$ansible 192.168.100.1 -i myhosts.ini -c network_cli -e ansicle_network_os=ios -u user -k -m ios_command -a "commands='sh clock'"`, где:
`192.168.100.1` - адрес компьютера, к которому происходит подключение
`-i myhosts.ini` - название инвентарного файла
`-c network_cli` - тип соединения: выбрано соединение через сетевую
командную строку. Ещё варианты: `netconf`, `httpapi`, `local`
`-e ansicle_network_os=ios` - экстра параметры: сетевая операционная система ios, **это прописывать обязательно**
`-u user` - имя пользователя
`-k` - запрос пароля(?)
`-m ios_command` - модуль, который будет выполняться, в данном случае модуль ios_command
`-a "commands='sh clock'"` `` ``- передаваемые аргументы, в данном случае bash команда 

**важно**: по умолчанию ansible ориентирован на аутентификацию через ssh ключи
Часть этих команд можно заменить переменными в ini-файле:
```ini
[cisco_routers:vars]
ansible_connection=network_cli
ansible_network_os=ios
ansible_user=cisco
ansible_password=cisco
```
