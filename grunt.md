# Grunt - сборщик проектов

**Статус:** черновик.

## Ссылки

* [gruntjs.com](https://gruntjs.com/) - официальный сайт Grunt.
* [Grunt для тех, кто считает штуки вроде него странными и сложными](http://frontender.info/grunt-is-not-weird-and-hard/).
* [Сборка сайтов на независимых блоках из Jade и Stylus с использованием Grunt.js](http://oleggromov.com/slides/independent-blocks-assemble/).
* [Grunt: система сборки для фронтенд-разработчиков](http://sapegin.ru/pres/grunt/).

## Установка

1. Устанавливаем [Node.js](http://nodejs.org/download/), включающий в себя NPM (Node Packet Manager).
2. `npm i -g grunt-cli` - устанавливаем Grunt CLI (интерфейс командной строки).<br>
   После этого следует закрыть и заново открыть окно терминала (Bash/Git-Bash).<br>
   Если при вызове команды `grunt` пишет ошибку `Command Not Found`, то нужно перезагрузиться или выйти из системы и зайти снова.
3. Устанавливаем [Git](http://git-scm.com/book/ru/Введение-Установка-Git) под Вашу ОС, если ещё не установлен.

Эти 3 шага выполняются один раз.

## Пакеты NPM

Для повседневных задач нам достаточно:

* [`bump`](https://www.npmjs.org/package/grunt-bump) - обновление версии проекта.
* [`clean`](https://www.npmjs.org/package/grunt-contrib-clean) - очистка папки от файлов.
* [`spritesmith`](https://www.npmjs.org/package/grunt-spritesmith) - генератор спрайтов и CSS переменных.
* [`imagemin`](https://www.npmjs.org/package/grunt-contrib-imagemin) - сжатие картинок.
* [`stylus`](https://www.npmjs.org/package/grunt-contrib-stylus) - препроцессор CSS.
* [`autoprefixer`](https://www.npmjs.org/package/grunt-autoprefixer) - подстановка префиксов для заданных браузеров.
* [`combine-media-queries`](https://www.npmjs.org/package/grunt-combine-media-queries) - комбинирование медиа-запросов в CSS.
* [`csscomb`](https://www.npmjs.org/package/grunt-csscomb) - форматирование CSS.
* [`jade`](https://www.npmjs.org/package/grunt-contrib-jade) - препроцессор HTML.
* [`prettify`](https://www.npmjs.org/package/grunt-prettify) - форматирование HTML.
* [`jshint`](https://www.npmjs.org/package/grunt-contrib-jshint) - проверка JavaScript на качество кода с подсказками.
* [`copy`](https://www.npmjs.org/package/grunt-contrib-copy) - создание копий файлов.
* [`uglify`](https://www.npmjs.org/package/grunt-contrib-uglify) - минифицирование и обфускация скриптов.
* [`replace`](https://www.npmjs.org/package/grunt-replace) автозамена паттернов на заданные значения.
* [`newer`](https://www.npmjs.org/package/grunt-newer) - выполнение задач только с новыми файлами.
* [`browser-sync`](https://www.npmjs.org/package/grunt-browser-sync) - локальный сервер и автоперезагрузка страницы с уведомлениями.
* [`watch`](https://www.npmjs.org/package/grunt-contrib-watch) - отслеживание изменений файлов и их компиляция.

В зависимости от проекта дополнительно могут пригодиться такие пакеты:

* Для объединения и минификации:

  * [`cssmin`](https://www.npmjs.org/package/grunt-contrib-cssmin) - минификация CSS.
  * [`concat`](https://www.npmjs.org/package/grunt-contrib-concat) - объединение скриптов в один файл.<br>
    _Если возникают ошибки при конкатенации скриптов, то нужно установить порядку их зависисмости_.
  * [`uglify`](https://www.npmjs.org/package/grunt-contrib-uglify) - обфускация скриптов.

* Препроцессоры:

  * [`coffee`](https://www.npmjs.org/package/grunt-contrib-coffee) - CoffeeScript препроцессор JavaScript.
  * [`less`](https://www.npmjs.org/package/grunt-contrib-less) - Less препроцессор CSS.
  * [`sass`](https://www.npmjs.org/package/grunt-contrib-sass)/[`compass`](https://www.npmjs.org/package/grunt-contrib-compass) - Sass препроцессор CSS.

* Если этого будет недостаточно, можно поискать подходящие по ссылкам:
  * [gruntjs.com/plugins](https://gruntjs.com/plugins)
  * [npmjs.org](https://www.npmjs.org/)
