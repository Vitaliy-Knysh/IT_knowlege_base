### Документ с диаграммами
https://gist.github.com/ptmcg/3364c98081d6b544c13922584bf1352c

**textual** - это фреймворк, расширяющий возможности терминальных интерфейсов. Он позволяет создать интрфейс наравне с pyqt внутри терминала.

Пример пустого приложения:
```python
from textual.app import App


class MyApp(App):
    pass


if __name__ == "__main__":
    app = MyApp()
    app.run()
```

Всё приложение должно находиться в одном классе, который наследет класс App. Во время работы приложения нужно создать экземпляр этого класса и запустить его методом `run`.

### События
Textual может реагировать на такие события, как:
- нажатия клавиш
- действия мышкой
- изменения внутреннего состояния

Пример класса с обработчиками событий: 
```python
from textual import events


class EventApp(App):

    COLORS = [
        "white",
        "maroon",
        "red",
        "purple",
        "fuchsia",
        "olive",
        "yellow",
        "navy",
        "teal",
        "aqua",
    ]

    def on_mount(self) -> None:
        self.screen.styles.background = "darkblue"

    def on_key(self, event: events.Key) -> None:
        if event.key.isdecimal():
            self.screen.styles.background = self.COLORS[int(event.key)]
```
Обработчик `on_mount` вызывается, как только приложение запущено. Обработчик `on_key` заватывает и возвращает нажатую клавишу.

### Виджеты и метод compose()

**Виджеты** - компоненты, которые отвечают за генерацию вывода на части экрана. Виджеты отвечают на события так же, как `App`. Виджеты могт содержать как простые элементы(текст, кнопки), так и други виджеты. По сути, интерфейс состоит из виджетов. 

Чтобы добавить виджеты в приложение, используется метод compose(), который возвращает `iterable` объектов виждетов. Список годится для этого, но удобнее использовать `yield`, делая из метода генератор:
```python
from textual.app import App, ComposeResult


class WelcomeApp(App):
    def compose(self) -> ComposeResult:
        yield Welcome()

    def on_button_pressed(self) -> None:
        self.exit()
```
Внутри `compose` нужно прописать все используемые методы, прописав перд ними `yield`.

**Метод mount()** позволяет добавлять новые виджеты по событию:
```python
class WelcomeApp(App):
    def on_key(self) -> None:
        self.mount(Welcome())

    def on_button_pressed(self) -> None:
        self.exit()
```

### Контейнер
Действует по такому же принципу, как контейнер CSS. Нужен для группировки объектов. Пример:
```python
    def compose(self) -> ComposeResult:
        """Create child widgets for the app."""
        yield Header()
        yield Footer()
        yield Container(SomeClass(), SomeClass(), SomeClass())
```



# CSS 
**align и content-align**: разница в том, что align применяется к детским виждетам внутри контейнера, а content-align применяется к содержимому контейнера

# Фокус

На виджетах можно сфокусироваться, чтобы  события с клавиатуры и мыши(прокрутка, текствоый ввод итд) применялись к нужному виджету. Фокус переключается клавишей `Tab`. 
Чтобы сделать виждет доступным для фокуса, необходимо создать контейнер и задать параметр `can_focus=True`: 
```python
class FocusableScroll( VerticalScroll, can_focus=True ):  
	pass
```
Этот контейнер можно использовать как родительский для создания виждета, на котором можно сфокусироваться:
```python
def compose(self) -> ComposeResult:  
	with FocusableScroll():  
	for inp in input_log:  
		yield Label(inp, classes='inputs')
```
Чтобы при фокусировке виджет изменял свой стиль, необходимо прописать это в CSS:
```css
InputLog:focus-within {  
	border: dashed #368DFF;  
}
```

# Пользовательский ввод

## Кнопки
Когда кнопка нажата, соответствующее событие отправляется в приложение. Пример обработчика события:
```python
class InputApp(App):

    def on_key(self, event: events.Key) -> None:
        self.query_one(TextLog).write(event)
```