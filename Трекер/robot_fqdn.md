[gitlab](https://gitlab.aq.ru/factorytesting/python/robot_fqdn)

Служит для получения fqdn.

Основная функция - **get\_fqdn()**.

Процесс:

1.  Получение **zone\_id** с помощью [**consul\_interactions**](https://tracker.aq.ru/projects/python/wiki/consul-interactions).
2.  Поиск строки, начинающейся с &quot;**search**&quot; в файле &quot;**/etc/resolv.conf**&quot;, если строка не найдена - поднимается ошибка _ValueError(&quot;Couldn&#39;t find line starting with &#39;search&#39;&quot;)_
3.  Строка преобразуется в список, удаляется первый элемент (search)
4.  Поиск элемента без &quot;node&quot;, если такой строки нет - поднимается ошибка _ValueError(&quot;Couldn&#39;t find correct search, got line: {line}&quot;)_
5.  Если **zone\_id** было в консуле, отрезает зону из адреса. Если зоны не было найдено в строке, поднимается ошибка _ValueError(&quot;Couldn&#39;t find zone\_id ({zone\_id}) in search ({search})&quot;)_
6.  Возвращает полученную строку, пример: &quot;**r6.robots.aq.ru**&quot;