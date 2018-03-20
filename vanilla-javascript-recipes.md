# Рецепты «ванильного» JavasScript

**Статус:** черновик.

## Оглавление

* [Работа с DOM](#work-with-dom)
  * [Выборка элементов](#elements-selection)
  * [Поиск элементов среди потомков](#decendants-elements-find)
  * [Перебор элементов](#elements-iterate)
    * [Array.prototype.forEach()](#array-prototype-foreach)
    * [[].forEach()](#array.foreach)
    * [Конвертация в массив](#convert-to-array)
    * [Цикл `for`](#for-loop)
    * [Цикл `for-of`](#for-of-loop)
* [События](#events)
  * [Несколько событий с одним обработчиком](#mulitple-events-with-single-handler)
  * [Симуляция события](#event-simulation)
  * [Document Ready](#document-ready)
* [Данные](#data)
  * [Данные привязанные к DOM элементу](#data-linked-to-dom-elment)
* [Структуры](#structures)
  * [Плагин](#plugin)
* [Ссылки](#links)

<a name="work-with-dom"></a>

## Работа с DOM

<a name="elements-selection"></a>

### Выборка элементов

```js
// Один элемент
const article = document.querySelector("article");

// Несколько элементов
const articles = document.querySelectorAll("article");
```

Чтобы не писать каждый раз `document.querySelector...`, можно использовать следующие хелперы.

```js
// Один элемент
const $ = selector => document.querySelector(selector);
$("article");

// Несколько элементов
const $$ = selector => document.querySelectorAll(selector);
$$("article");

// Более продвинутый вариант
const isString = value => toString.call(value) === "[object String]";

const $ = (element, selector) => {
  const elements = !isString(element)
    ? element.querySelectorAll(selector)
    : document.querySelectorAll(element);

  const elementsArray = elements.length > 0 ? [].slice.call(elements) : [];

  return elementsArray.length === 1 ? elementsArray[0] : elementsArray;
};

const article = $('article.post'); // 'document > article.post', <article class="post">...</article>
const h1 = $(article, 'h1'); // 'article.post > h1', <h1>...</h1>
const parpagraphs = $(article, 'p'); // 'article.post > p', [<p>, <p> ....]
```

<a name="decendants-elements-find"></a>

### Поиск элементов среди потомков

```js
const page = document.querySelector(".page");
const header = page.querySelector(".header");
const headerMenu = header.querySelector(".menu");
const sidebar = page.querySelector(".sidebar");
```

<a name="elements-iterate"></a>

### Перебор элементов

```js
const articles = document.querySelectorAll("article");
```

При выборке элементов через `querySelectorAll` возвращяется `NodeList` а не `Array`

<a name="array-prototype-foreach"></a>

#### Array.prototype.forEach()

```js
Array.prototype.forEach.call(articles, article => {
  console.log(article);
});
```

<a name="array.foreach"></a>

#### [].forEach()

```js
[].forEach.call(articles, article => {
  console.log(article);
});
```

<a name="convert-to-array"></a>

#### Конвертация в массив

```js
const articles = [].slice.call(document.querySelectorAll("article"));
const articles = [...document.querySelectorAll("article")];
const articles = Array.from(document.querySelectorAll("article"));
```

<a name="for-loop"></a>

#### Цикл `for`

```js
for (let i = 0; i < articles.length; i++) {
  console.log(articles[i]);
}
```

<a name="for-of-loop"></a>

#### Цикл `for-of`

```js
for (let article of articles) {
  console.log(article);
}
```

<a name="events"></a>

## События

<a name="mulitple-events-with-single-handler"></a>

### Несколько событий с одним обработчиком

```js
const input = document.querySelector("#input");
["focus", "blur", "keyup"].forEach(eventName => {
  input.addEventListener(eventName, event => {
    console.log(event);
  });
});
```

Можно использовать следующий хелпер

```js
const input = document.querySelector("#input");
const on = (element, events, cb) => {
  let eventsList = [];

  if (Array.isArray(events)) {
    eventsList = events;
  } else if (typeof events === "string") {
    eventsList = events.split(",").map(item => item.trim());
  } else {
    throw new Error(
      "The second parameter must be an array or comma separeted string"
    );
  }

  eventsList.forEach(eventName => {
    element.addEventListener(eventName, cb);
  });
};

on(input, "focus, blur, keyup", event => {
  console.log(event.type);
});
```

<a name="event-simulation"></a>

### Симуляция события

```js
const trigger = (element, eventName, data) => {
  if (typeof eventName === "string" && eventName.length > 0) {
    const event = new Event(eventName);

    if (data) {
      event.data = data;
    }

    element.dispatchEvent(event);
  }
};

window.addEventListener("click", e => console.log(e));
window.addEventListener("resize", e => console.log(e));

trigger(window, "click", { test: true });
trigger(window, "resize");
```

<a name="document-ready"></a>

### Document Ready

```js
function ready(fn) {
  if (
    document.attachEvent
      ? document.readyState === "complete"
      : document.readyState !== "loading"
  ) {
    fn();
  } else {
    document.addEventListener("DOMContentLoaded", fn);
  }
}

ready(function() {
  console.log("ready");
});
```

<a name="data"></a>

## Данные

<a name="data-linked-to-dom-elment"></a>

### Данные привязанные к DOM элементу

```js
// based on code from page
// https://j11y.io/javascript/element-datastorage/

let cache = [0];
const expando = "data" + (new Date() + Math.random()).replace(/\D/g, "");

function data(element) {
  if (!element) {
    throw new Error("Element not set");
  }

  let cacheIndex = element[expando];
  const nextCacheIndex = cache.length;

  if (!cacheIndex) {
    cacheIndex = element[expando] = nextCacheIndex;
    cache[cacheIndex] = {};
  }

  return cache[cacheIndex];
}

const element = document.querySelector("#element");
data(element).someData = "test"; // set
data(element).someData; // get
```

<a name="structures"></a>

## Структуры

<a name="plugin"></a>

### Плагин

```js
// plugin.js
// Plugin init helper
function Plugin(Instance) {
  return function(selector = document.documentElement, options = {}) {
    const elements = document.querySelectorAll(selector);

    return Array.prototype.map.call(elements, element => {
      return new Instance(element, options);
    });
  };
}

export default Plugin;
```

```js
// helloWorld.js
import Plugin from "./plugin";

class HelloWorld {
  constructor(element, _options) {
    this.element = element;
    this._options = _options;
    this._defaults = {
      text: "Hello world!"
    };
    this.options = Object.assign({}, this._defaults, this._options);

    this.init();
  }

  init() {
    this.renderText();
  }

  renderText() {
    this.element.innerHTML = this.options.text;
  }
}

// export wrapped class
export default Plugin(HelloWorld);
```

```js
// app.js
import HelloWorld from "./helloWorld";

HelloWorld(".hello-world");
HelloWorld(".test2", { text: "Text from `text` param" });
```

<a name="links"></a>

## Ссылки

* [YOU MIGHT NOT NEED JQUERY](http://youmightnotneedjquery.com/)
* [ECMAScript compatibility table](http://kangax.github.io/compat-table/es6)
* [Bliss.js (если все равно больно)](http://blissfuljs.com/)
