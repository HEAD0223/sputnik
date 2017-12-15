# Pug (jade) - HTML препроцессор

**Статус:** актуально.

## Ссылки

* [Документация](https://pugjs.org/)

## 1. Подключение частиц в страницы

* `include header` - используется для подключения частиц страницы, например, для шапок и подвалов.
* `extends partials/default` - используется для внедрения контент в расширяемый шаблон. `layouts/default`.
* `block content` - используется для добавления строк кода в определённое место другого шаблона

Во всех случаях через пробел указывается путь от текущего расположения до шаблона без расширения `*.pug, *.jade`.

## 2. Теги, классы и идентификаторы

* Классы и идентификаторы пишутся в начале, а не в атрибутах. Указывать тег `div` не нужно, т.к. он используется по умолчанию.

  ```pug
  //- Плохо
  div(class='carousel' id="carousel")
  nav(class='nav nav_pos_left')
  div(id="carousel")

  //- Хорошо
  .carousel
  nav.nav.nav_pos_left
  #carousel
  ```

* Идентификатор ставится после классов.

  ```pug
  //- Плохо
  .carousel#carousel.carousel_theme_dark
  #carousel.carousel

  //- Хорошо
  .carousel.carousel_theme_dark#carousel
  .carousel#carousel
  ```

## 3. Атрибуты элемента и их значения

* Для нескольких атрибутов запятая не нужна.

  ```pug
  //- Плохо
  input.input-text(type='text', name='project', value='csssr', required)

  //- Хорошо
  input.input-text(type='text' name='project' value='csssr' required)
  ```

* Используйте одинарные кавычки для текстовых значений.

  ```pug
  //- Плохо
  input.input-text(type="text" name="project" value="csssr" required)

  //- Хорошо
  input.input-text(type='text' name='project' value='csssr' required)
  ```

* Не давайте необязательные значения атрибутам.

  ```pug
  //- Плохо
  input.input-checkbox(type='checkbox' name='browser[]' value='chrome' checked='checked')

  //- Хорошо
  input.input-checkbox(type='checkbox' name='browser[]' value='chrome' checked)
  ```

* Распологайте одиночные атрибуты в последнюю очередь.

  ```pug
  //- Плохо
  input.input-checkbox(type='checkbox' checked name='browser[]' value='chrome')

  //- Хорошо
  input.input-checkbox(type='checkbox' name='browser[]' value='chrome' checked)
  ```

* Для числовых значений кавычки не нужны.

  ```pug
  //- Плохо
  input.input-text(type="text" name="price" value="24999")

  //- Хорошо
  input.input-text(type='text' name='price' value=24999)
  ```

* Переносите атрибуты новую строку, если их много и/или значения длинные.

  ```pug
  //- Плохо
  input.input-text(type='text' name='project' value='csssr' data-required='Это поле обязательно для заполнения!'  data-hint='Допустимы только символы латинского алфавита `[a-z-A-Z]` и числа `[0-9]`.' required)

  //- Хорошо
  input.input-text(
      type='text'
      name='project'
      value='csssr'
      data-required='Это поле обязательно для заполнения!'
      data-hint='Допустимы только символы латинского алфавита `[a-z-A-Z]` и числа `[0-9]`.'
      required
  )
  ```

## 4. Переносы строк

* Добавляйте перенос строки для однотипных блоков с множественным вложением элементов. В лучшем случае используйте [примесь (mixin)](http://jade-lang.com/reference/#mixins).

  ```pug
  //- Плохо
  .project
  .project__name Lorem
  .project__desc
      | Lorem ipsum dolor sit amet, consectetur adipisicing elit.
      | Unde doloremque neque facilis sed repudiandae tempore ipsum provident officia eaque quas.
  .project
  .project__name Ipsum.
  .project__desc
      | Lorem ipsum dolor sit amet, consectetur adipisicing elit.
      | Unde doloremque neque facilis sed repudiandae tempore ipsum provident officia eaque quas.

  //- Хорошо
  .project
  .project__name Lorem
  .project__desc
      | Lorem ipsum dolor sit amet, consectetur adipisicing elit.
      | Unde doloremque neque facilis sed repudiandae tempore ipsum provident officia eaque quas.

  .project
  .project__name Ipsum.
  .project__desc
      | Lorem ipsum dolor sit amet, consectetur adipisicing elit.
      | Unde doloremque neque facilis sed repudiandae tempore ipsum provident officia eaque quas.
  ```

* Строчные элементы можно записывать на одной строке через двоеточие `:`.<br>Не злоупотреблять с длинными классами.

  ```pug
  //- Хорошо
  ul.nav
  li.nav__item
      a.nav__link(href='/') Главная
  li.nav__item
      a.nav__link(href='/projects') Проекты
  li.nav__item
      a.nav__link(href='/contacts') Контакты

  //- Лучше
  ul.nav
      li.nav__item: a.nav__link(href='/') Главная
      li.nav__item: a.nav__link(href='/projects') Проекты
      li.nav__item: a.nav__link(href='/contacts') Контакты
  ```

## 5. Комментарии

* Комментарии в Jade, которые не должны попасть в HTML записываются через `//-`.

  ```pug
  // Этот комментарий попадёт в HTML.

  //- Этот комментарий не попадёт в HTML.
  ```

* Простые или условные комментарии можно записывать прямо в HTML-формате.

  ```html
  <!--[if IE]>
  meta(name='imagetoolbar' content='no')
  meta(name='msthemecompatible' content='no')
  <![endif]-->

  <!--noindex-->
  Это содержимое не будет индексироваться поисковиком.
  <!--/noindex-->
  ```

## 6. Пиши меньше, делай больше или используйте примеси!

Для однотипных и повторяющихся строк кода имеет смысл использовать [примеси (mixins)](http://jade-lang.com/reference/#mixins) и указать только данные.

```jade
mixin tools(list)
    ul.list
        each item in list
            li.list__item
                span.mark= item[0]
                = ' - ' + item[1]

+tools([
    ['spritesmith', 'генератор спрайтов и CSS переменных'],
    ['imagemin', 'сжатие картинок']
])
```

Скомпилирует в

```html
<ul class="list">
    <li class="list__item">
        <span class="mark">spritesmith</span> - генератор спрайтов и CSS переменных
    </li>
    <li class="list__item">
        <span class="mark">imagemin</span> - сжатие картинок
    </li>
</ul>
```

## 7. Выделение активного пункта в меню навигации

### 7.1. Идентификаторы

На каждой странице в самом начале добавляем по идентфикатору страницы.

**pages/main.jade**

```javascript
- var pageId = 0;
```

**news.jade**

```javascript
- var pageId = 1;
```

**projects.jade**

```javascript
- var pageId = 2;
```

**about.jade**

```javascript
- var pageId = 3;
```

**contacts.jade**

```javascript
- var pageId = 4;
```

### 7.2. Активация пункта навигации

Активируем текущий пункт навигации в зависимости от идентификатора страницы.

**partials/header.pug**

```pug
//- Добавляем примесь для активации пункта навигации текущей страницы
mixin nav(items)
    ul.nav
        each item, i in items
            li.nav-item
                if i === pageId
                    span.nav-item__name.nav-item__name_state_active= item.name
                else
                    a.nav-item__name(href=item.href)= item.name

//- Используем примесь и добавляем в него данные навигации
+nav([{
    name: 'Главная',
    href: '/'
}, {
    name: 'Новости',
    href: '/news.html'
}, {
    name: 'Проекты',
    href: '/projects.html'
}, {
    name: 'О нас',
    href: '/about-us.html'
}, {
    name: 'Контакты',
    href: '/contacts.html'
}])
```

### 7.3. Результат

В итоге, если у нас текущая страница "Новости", то результат будет таким:

```html
<ul class="nav">
    <li class="nav-item">
        <a class="nav-item__name" href="/">Главная</a>
    </li>
    <li class="nav-item">
        <span class="nav-item__name nav-item__name_state_active">Новости</span>
    </li>
    <li class="nav-item">
        <a class="nav-item__name" href="/projects.html">Проекты</a>
    </li>
    <li class="nav-item">
        <a class="nav-item__name" href="/about-us.html">О нас</a>
    </li>
    <li class="nav-item">
        <a class="nav-item__name" href="/contacts.html">Контакты</a>
    </li>
</ul>
```
