# React basics

### JSX

`JSX` - это синтаксическое расширение для JavaScript \(функции **CreateElement**\)

```text
<MyButton color="blue" shadowSize={2} action={this.action}>
  Click Me
</MyButton>
```

```text
React.createElement(
  MyButton,
  { color: 'blue', shadowSize: 2 },
  'Click Me'
)
```

* `Babel` компилирует `JSX` в вызовы `React.createElement()`
* Теги начинаются с заглавной буквы \(чтобы отличить React-компоненты от html тегов\)
* т.к. неявно вызывается функция `React.createElement`, в файле должен быть `import React from 'react'`
* атрибуты: class === `className`, for === `htmlFor`
* встраивание пользовательского ввода в JSX является безопасным \(не допускает XSS-атак\) - потому что все преобразуется в строку, а не выполняется

### Presentation vs Container components

* `Container`
  * делают API запросы
  * подключены к Store,
  * часто созданы через `class`
  * используют lifecycle hooks
* `Presentation`
  * получают данные через `props` и отрисовывают
  * редко могут иметь свой локальный state, но это состояние UI, а не бизнес-данных \(например, выбран ли checkbox\)
  * часто созданны через `function`

### Lifecycle

![](../../.gitbook/assets/image%20%2823%29.png)

* Mounting
  * `constructor(props)` - \(не обязательный,, если не нужно инициализировать там state\)
  * static `getDerrivedStateFromProps(props, state)` \(возвращает объект, который и будет this.state\)
  * render\(\)
  * `componentDidMount()` \(хорошее место для API-запросов, подписок на события\)
* Updating
  * static `getDerrivedStateFromProps(props, state)`
  * `shouldComponentUpdate()` \(если вернет false, render и все нижние хуки не вызовутся\)
  * render\(\)
  * `getSnapshotBeforeUpdate()` - перед коммитом изменений в реальный DOM, возвращенное из метода значение станет 3-м аргументом
  * `componentDidUpdate(prevProps, prevState, snapshot)`
* Unmounting
  * `componentWillUnmount()` - \(отписаться от событий, удалить таймеры, ...\)
* Error Handling
  * static `getDerivedStateFromError(error)` - возвращает значение для изменения state \(тут не должно быть side-effects\)
  * `componentDidCatch(error, info)` - можно использовать для side-effects, например залогировать ошибку в логгер

### State vs Props

* Props

  * передаются в компонент из-вне
  * так ще компонент может иметь дефолтные props

  ```text
  static defaultProps = {
    theme: "secondary",
    label: "Button Text"
  };
  ```

  * props нельзя изменить \(однонаправленный поток данных, сверху-вниз\)

* State
  * хранит внутреннее состояние компонента
  * для того, чтобы хранить информацию между рендерами
  * при изменении состояния происходит render
  * setState\(\) асинхронный, иммутабельный, можно внутрь передавать функцию или объект \(если не зависим от прошлого состояния\)

### Refs

> Refs provide a way to access DOM nodes or React elements created in the render method.

```text
class Component extends React.Component {
  constructor() {
    this.inputRef = React.createRef();
  }

  handleSubmit = () => {
    this.inputWrapper.current.focus();
  }

  render() {
    return (
      <div onClick={this.handleSubmit}>
        <input type="text" ref={this.inputRef} />
      </div>
    )
  }
}
```

**\#forwarding Refs**

> Ref forwarding is a technique for automatically passing a ref through a component to one of its children

### Events

* React events are named using camelCase, rather than lowercase.
* with JSX you pass a function as the event handler, rather than a string.
* React uses a synthetic event. React defines these synthetic events according to the W3C spec, so you don’t need to worry about cross-browser compatibility

```text
function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }
```

**\#SyntheticEvent**

> SyntheticEvent, a cross-browser wrapper around the browser’s native event. It has the same interface as the browser’s native event, including `stopPropagation()` and `preventDefault()`, except the events work identically across all browsers.

### Forms

* uncontrolled input - will use `ref` to get the form values.

```text
submitFormHandler = event => {
  event.preventDefault();
  console.dir(this.refs.name.value); //will give us the name value
}

render() {
  return (
      <div>

        <form onSubmit={this.submitFormHandler}>
          <div>
            <input type="text" name="name" ref="name" />
          </div>
        </form>

      </div>
  );
}
```

* controlled input \(+ validation, notifications\)

```text
import React, { Component } from 'react';

class FormComponent extends Component {
  constructor () {
    this.state = {
      email: ''
    }
  }
  
  changeHandler = event => {
    this.setState({
      email: event.target.value
    });
  }

  render () {
    return (
      <form>
          <input type="email" 
                 name="email"   
                 value={this.state.email} 
                 onChange={this.changeHandler} 
          />
      </form>
    );        
  }
}

export default FormComponent;
```

### Data fetching

> React itself doesn’t have any allegiance to any particular way of fetching data.

* axios \(promises\)
* fetch \(browser api\)

```text
componentDidMount() {
    axios.get(`http://www.reddit.com/r/${this.props.subreddit}.json`)
      .then(res => {
        const posts = res.data.data.children.map(obj => obj.data);
        this.setState({ posts });
      });
  }
```

