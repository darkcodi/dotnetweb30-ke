# Promise

> Объект Promise служит хранилищем для результата асинхронной операции это специальный объект, который хранит своё состояние, текущий результат \(если есть\) и коллбэки.

A promise can be:

* **fulfilled** - The action relating to the promise succeeded
* **rejected** - The action relating to the promise failed
* **pending** - Hasn't fulfilled or rejected yet
* **settled** - Has fulfilled or rejected



* до промисов:
  * модель события \(addEventListener\)
  * функции обратного вызова \(callback\)
* внутренние состояния: `pending`, `fulfilled`, `rejected`
* методы `then`, `catch`
* new Promise\(\)

  ```text
  let fs = require('fs');

  function readFile(filename) {
    return new Promise((resolve, reject) => {
      fs.readFile(filename, { encoding: 'utf8' }, (err, content) => {
        if(err) {
          reject(err);
        }
        resolve(content);
      })
    });
  }
  ```

* Promise.resolve\(\)

Сразу возвращает объект Promise в состоянии "выполнено"

```text
let promise = Promise.resolve(42);

promise
  .then(value => console.log(value)); // 42
```

* Promise.reject\(\)

Сразу возвращает объект Promise в состоянии "отклонено"

```text
let promise = Promise.reject(42);

promise
  .catch(value => console.log(value)); // 42
```

* `Promise.all()`

  > Вызов Promise.all\(iterable\) получает массив \(или другой итерируемый объект\) промисов и возвращает промис, который ждёт, пока все переданные промисы завершатся, и переходит в состояние «выполнено» с массивом их результатов.

* `Promise.race()`

Gереходит в `fullfiled` сразу после первого удачного выполнения

* Global ErrorHandler

{% hint style="info" %}
в спецификации нет глобальной обработки rejected Promises

* nodeJS: `unhandledRejection()`, `rejectionHandler()`
* браузеры: `window.unhandledrejection`, `window.onrejecthandled`
{% endhint %}

