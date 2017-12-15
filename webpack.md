# [Webpack](https://webpack.js.org/)

Мощная и гибкая система сборки для frontend

**Статус:** черновик.

## Установка

Для работы нужен [Node.js](http://nodejs.org/download/), включающий в себя NPM (или другой пакетный менеджер).

1. Установить `npm install webpack --save-dev`
2. Создать в проекте конфигурационный файл `touch webpack.config.js`
3. Добавить в `package.json` в секцию "scripts"


```js
"scripts": {
  "start": "webpack --config webpack.config.js"
}
```

## Философия

Основная цель webpack собрать все ваши `*.js` файлы в любое нужное вам количество пакетов (bundles), а также убедиться, что в собранном пакете есть все `*.js` файлы вашего проекта в правильном порядке.

Для того чтобы это работало нужно в каждом модуле (файле) явно указывать все зависимости.

Существует 3 системы модулей:

1. CommonJS
2. AMD modules
3. ES6 modules

Webpack может разобрать все эти зависимости, но ему нужно еще указать точку входа, и куда вернуть собранный бандл.

Webpack очень популярен не только из-за большого числа разработчиков, активно поддерживающих его, но и из-за количества дополнительных функциональных возможностей, доступных для него, таких как загрузчики (loaders) и плагины. С их помощью вы можете легко запускать различные процессы до и после того, как Webpack собрал ваши файлы. Это позволяет легко построить статический конвейер активов (assets)

Благодаря системе лоадеров бандл webpack может включать в себя не только javascript код, а так же любое содержимое. Например css, svg, jpg и тд.

Обычно эти файлы не оставляют в бандле, а выносят в отдельные файлы, с помощбью других лоадеров (file-loader, css-loader и тд.)

Для настройки webpack можно сконфигурировать с помощью параметров коммандной строки, но гораздо удобней это делать при помощи отдельного конфигурационного файла - webpack.config.js.

## Конфиг

Простейший конфиг для webpack выглядит примерно так:

```js
const path = require("path");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname, "dist")
  }
};
```

Более подробно по конфигу webpack можно посмотреть в документации.

Для постоянной пересборки проекта создатели webpack рекомендуют использовать [webpack-dev-server](https://github.com/webpack/webpack-dev-server/).
Так же можно использовать [webpack-dev-middleware](https://github.com/webpack/webpack-dev-middleware) для реализации собственного сервера.

## Ссылки

* [Документация Webpack Config](https://webpack.js.org/configuration/)
* [Рецепты и примеры](https://github.com/webpack/webpack/blob/master/examples/README.md)
* [Awesome Webpack](https://github.com/webpack-contrib/awesome-webpack)
