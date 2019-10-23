# click()

Метод **`.click()`** привязывает JavaScript обработчик событий `click` (клик левой кнопкой мыши), или запускает это событие на выбранный элемент.

Следующие условия обязательно должны быть выполнены, чтобы событие `click` сработало:

- Левая кнопка мыши нажата, когда курсор находился внутри элемента.
- Левая кнопка мыши отпущена пока курсор находится внутри элемента.

## Синтаксис

Синтаксис 1.0:

```js
$(selector).click() // метод используется без параметров
$(selector).click(handler)
```

- `handler` - `Function( Event eventObject )`

Синтаксис 1.4.3:

```js
$(selector).click(eventData, handler)
```

- `eventData` - `Anything`
- `handler` - `Function( Event eventObject )`

Метод `.click()`, используемый вместе с функцией, переданной в качестве параметра (handler) является, короткой записью метода `.on()`, а без параметра является короткой записью метода `.trigger()`:

```js
$(selector).on('click', handler)
$(selector).trigger('click')
```

Добавлен в версии jQuery 1.0 (синтаксис обновлен в версии 1.4.3)

## Параметры

`eventData`
: Объект, содержащий данные, которые будут переданы в обработчик событий.

`handler`
: Функция, которая будет выполнена каждый раз, когда событие срабатывает. Функция в качестве параметра может принимать объект `Event`.

## Пример 1

```html
<!DOCTYPE html>
<html>
  <head>
    <title>
      Использование jQuery метода .click() (без параметров и с функцией)
    </title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
    <script>
      $(document).ready(function() {
        $('button').click(function() {
          // задаем функцию при нажатиии на элемент <button>
          $('div').click() // вызываем событие click на элементе <div>
        })
        $('div').click(function() {
          // задаем функцию при нажатиии на элемент <div>
          $('div').toggle() // отображаем, или скрываем элемент
        })
      })
    </script>
  </head>
  <body>
    <button>Клик</button>
    <div style="border:1px solid red">Элемент div</div>
  </body>
</html>
```

В этом примере с использованием метода `.click()` мы при нажатии на элемент `<button>` (кнопка) вызываем событие `click` на элементе `<div>`. Самому элементу `<div>` задаем, что при срабатывании события `click` на элементе выполнить функцию, которая с использованием метода `.toggle()` отобразит, или скроет элемент.

Обратите внимание, что если мы вызываем напрямую событие `click` на элемент `<div>`, то мы его можем только скрыть, по той причине, что напрямую кликнуть по скрытому элементу нельзя, но мы можем опять отобразить этот элемент кликнув по кнопке, которая симулирует щелчок по этому элементу.

Результат:

![Пример использования](854.png)

Пример использования метода `.click()` (без параметров и с функцией)