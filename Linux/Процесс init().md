**init()** - подсистема инициализации, которая запускает процессы, обеспечивающие взаимодействие с пользователем. Имеет PID 1.
В реализации init в стиле System V используется понятие уровня выполнения — степени загрузки операционной системы; в этом случае стартовые сценарии для каждого уровня разложены по каталогам от /etc/rc0.d до /etc/rc6.d, где цифра после rc соответствует номеру уровня инициализации
#### Пример init-файла 
```
id:5:initdefault:
si::sysinit:/etc/rc.d/rc.sysinit
l0:0:wait:/etc/rc.d/rc 0
l1:1:wait:/etc/rc.d/rc 1
l2:2:wait:/etc/rc.d/rc 2
l3:3:wait:/etc/rc.d/rc 3
l4:4:wait:/etc/rc.d/rc 4
l5:5:wait:/etc/rc.d/rc 5
l6:6:wait:/etc/rc.d/rc 6
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6
x:5:respawn:/etc/X11/prefdm -nodaemon
```
#### Уровни выполнения
0. Halt
1. Однопользовательсктй(безопасный) режим
6. Перезагрузка