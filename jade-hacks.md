# Jade (Pug) хаки и скрытые возможности

**Статус:** черновик.

## Введение

Подборка различных хаков или просто скрытых возможностей Jade (Pug)

## Передача аттрибутов в миксин

```jade
mixin test()
    a.test&attributes(attributes) test
    pre!= JSON.stringify(attributes)

+test(class="test2" href="#")
```

## Управление аттрибутами

```jade
mixin test(open)
  -
    var isOpen = attributes.open || false;
    var testAttrs = {};

    if (isOpen) {
      testAttrs["data-open"] = isOpen;
    }


  p&attributes(testAttrs)!= JSON.stringify(testAttrs)

+test()
+test(open="true")
+test(open="false")
```

## Передача данных в миксин

```jade
mixin test(data)
    a(href=data.url id="myid-#{data.id}").test= data.text

+test({"text": "test", "url": "#test", "id": "1"})
```

## Передача данных и атрибутов в миксин

```jade
mixin test(data)
    a(href=data.url id="myid-#{data.id}").test&attributes(attributes)= data.text

+test({"text": "test", "url": "#test", "id": "1"})(class="test2" href="#lol")
```

## Применение классов в зависимости от данных

```jade
mixin icon(data)
    - var classes = ['icon']
    if data.icon
        - classes.push(classes[0] + '_name_' + data.icon)
    if data.size
        - classes.push(classes[0] + '_size_' + data.size)

    i(class=classes)&attributes(attributes)

+icon({"icon": "share", "size": "big"})
```

## JavaScript в Jade (Pug)

```jade
//- Многострочный
-
    var uppercase = function(text) {
        return text.toUpperCase();
    }

//- Однострочный
- var test = uppercase('some text')

p= test
p= uppercase('Text')
```

## Значения по умолчанию у параметров миксинов

```jade
mixin price-tag(data)
    - currency = typeof data.currency != "undefined" ? data.currency : 'USD'

    .price-tag&attributes(attributes)
        span.price-tag__value= data.value
        span.price-tag__currency= currency

+price-tag({"value": "100"})
+price-tag({"value": "200", "currency": "RUB"})
```

## Динамическиое имя тега

```jade
mixin tag()
    if attributes.tag
        - var tag = attributes.tag
        - delete attributes.tag
        #{tag}&attributes(attributes).class Test


+tag()(tag="h1" class="test")
+tag()(tag="a" href="#" class="test2")
```

## Динамические аттрибуты

```pug
- var attrs = {}

if item.submenu
    - var tag = 'button'
    - customAttrs.type = "button"
else
    - var tag = 'a'
    - customAttrs.href = "#"

.main-menu
    #{tag}.main-menu__trigger&attributes(customAttrs)
    if item.submenu
        .main-menu__submenu
            | submenu
```

## Генерация элементов неизвестной вложенности (рекурсия)

```jade
mixin list(data)
    ul
        each item in data.items
            li= item.title
                if item.sublevel
                    +list(item)

- var data = {...}

+list(data)
```

```json
{
  "title": "Title text",
  "items": [
    {
      "title": "Item 1"
    },
    {
      "title": "Item 2",
      "sublevel": true,
      "items": [
        {
          "title": "Item 2.1"
        },
        {
          "title": "Item 2.2"
        },
        {
          "title": "Item 2.2",
          "sublevel": true,
          "items": [
            {
              "title": "Item 2.2.1",
              "sublevel": true,
              "items": [
                {
                  "title": "Item 2.2.2.1"
                },
                {
                  "title": "Item 2.2.2.2"
                },
                {
                  "title": "Item 2.2.2.3"
                }
              ]
            },
            {
              "title": "Item 2.2.2"
            },
            {
              "title": "Item 2.2.3"
            }
          ]
        }
      ]
    },
    {
      "title": "Item 3"
    }
  ]
}
```
