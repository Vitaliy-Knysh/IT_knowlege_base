BIOS передаёт управление загрузочному устройству, которое может быть жестким диском, флешкой, или другим носителем. сектор диска, на котором находится ОС (512 Б) содержит основной загрузчик(Master Boot Record) и таблицу разделов всех дисков, подключённых к системе. По умолчанию, в загрузочный раздел памяти загружается MBR, и ему передаётся управление. GRUB заменяет код MBR своим кодом.

Работа GRUB состоит из нескольких стадий:
**1.**    Размещение в MBR. Из-за малого объема MBR размещается только ссылка для перехода к стадии 2, которая содержит все требуемые данные.
**2.**    Переход к конфигурационному файлу, который содержит все компоненты пользовательского интерфейса и настройки, необходимые для работы GRUB.

Существует также стадия 1.5, которая используется, если загрузочная информация не может быть размещена непосредственно после MBR. (???)

![](file:///C:/Users/User/AppData/Local/Temp/msohtmlclip1/01/clip_image002.jpg)