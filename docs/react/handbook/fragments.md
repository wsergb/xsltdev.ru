# Фрагменты

Возврат нескольких элементов из компонента является распространённой практикой в React. Фрагменты позволяют формировать список дочерних элементов, не создавая лишних узлов в DOM.

```js
render() {
  return (
    <React.Fragment>
      <ChildA />
      <ChildB />
      <ChildC />
    </React.Fragment>
  );
}
```

Также существует [сокращённая запись](#short-syntax), однако не все популярные инструменты поддерживают её.

## Мотивация {#motivation}

Возврат списка дочерних элементов из компонента – распространённая практика. Рассмотрим пример на React:

```js
class Table extends React.Component {
  render() {
    return (
      <table>
        <tr>
          <Columns />
        </tr>
      </table>
    )
  }
}
```

`<Columns />` должен вернуть несколько элементов `<td>`, чтобы HTML получился валидным. Если использовать div как родительский элемент внутри метода `render()` компонента `<Columns />`, то HTML окажется невалидным.

```js
class Columns extends React.Component {
  render() {
    return (
      <div>
        <td>Привет</td>
        <td>Мир</td>
      </div>
    )
  }
}
```

Результатом вывода `<Table />` будет:

```js
<table>
  <tr>
    <div>
      <td>Привет</td>
      <td>Мир</td>
    </div>
  </tr>
</table>
```

Фрагменты решают эту проблему.

## Использование {#usage}

```js
class Columns extends React.Component {
  render() {
    return (
      <React.Fragment>
        <td>Привет</td>
        <td>Мир</td>
      </React.Fragment>
    )
  }
}
```

Результатом будет правильный вывод `<Table />`:

```js
<table>
  <tr>
    <td>Привет</td>
    <td>Мир</td>
  </tr>
</table>
```

### Сокращённая запись {#short-syntax}

Существует сокращённая запись объявления фрагментов. Она выглядит как пустые теги:

```js
class Columns extends React.Component {
  render() {
    return (
      <>
        <td>Привет</td>
        <td>Мир</td>
      </>
    )
  }
}
```

Можно использовать `<></>` так же, как используется любой другой элемент. Однако такая запись не поддерживает ключи или атрибуты.

Обратите внимание, что **большинство инструментов ещё не поддерживают сокращённую запись**, поэтому можно явно указывать `<React.Fragment>`, пока не появится поддержка.

### Фрагменты с ключами {#keyed-fragments}

Фрагменты, объявленные с помощью `<React.Fragment>`, могут иметь ключи. Например, их можно использовать при создании списка определений, преобразовав коллекцию в массив фрагментов.

```js
function Glossary(props) {
  return (
    <dl>
      {props.items.map((item) => (
        // Без указания атрибута `key`, React выдаст предупреждение об его отсутствии
        <React.Fragment key={item.id}>
          <dt>{item.term}</dt>
          <dd>{item.description}</dd>
        </React.Fragment>
      ))}
    </dl>
  )
}
```

`key` – это единственный атрибут, допустимый у `Fragment`. В будущем мы планируем добавить поддержку дополнительных атрибутов, например, обработчиков событий.

### Живой пример {#live-demo}

Новый синтаксис JSX фрагментов можно попробовать на [CodePen](https://codepen.io/reactjs/pen/VrEbjE?editors=1000).
