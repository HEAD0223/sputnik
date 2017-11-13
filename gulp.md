# [Gulp](https://gulpjs.com/)
Стриминговая система сборки, с очень маленьким API 

**Статус:** черновик.

## Установка
Для работы нужен [Node.js](http://nodejs.org/download/), включающий в себя NPM (или другой пакетный менеджер).

1. Установить один раз глобально Gulp CLI (интерфейс командной строки) `npm install gulp-cli -g`<br>
После этого следует закрыть и заново открыть окно терминала (Bash/Git-Bash).
2. Установить локально в проект `npm install gulp -D`
3. Создать в проекте конфигурационный файл `touch gulpfile.js`


## Философия

У gulp очень простое API, основных методов всего четыре:

* `gulp.src(globs[, options])` - указывает откуда прочитать файлы
* `gulp.dest(path[, options])` - куда записать файлы
* `gulp.task(name [, deps] [, fn])` - группирует задачи по имени
* `gulp.watch(globs[, opts][, fn])` - запускает слежение за определенными файлами

После чтения файлов через метод `src()` они попадают в поток т.н. трубу (pipe).
Файлы "текут" от `src()` к `dest()`, между этими точками они могут трансформироватся различными плагинами.


```js
gulp.task('templates', function() {
  return gulp.src('client/templates/*.jade') // читаем файлы
    .pipe(jade()) // плагины
    .pipe(minify())
    .pipe(gulp.dest('build/templates')) // записываем на диск
});

gulp.watch('client/templates/*.jade', function(event) {
  console.log('File ' + event.path + ' was ' + event.type + ', running tasks...');
}));
```

У Gulp версии 4 есть дополнительные методы: 

* `gulp.parallel`- запускеает задачи в паралельном режиме
* `gulp.series` - запускеает задачи в последовательном режиме
* `gulp.symlink` - записывает файлы в симлинки
* `gulp.lastRun` - хранит метку времени последненго успешного запуска 
* `gulp.tree` - используется в терминале для получения "дерева задач"
* `gulp.registry` - управление регистром

Наиболее востребованными являются `parallel()` и `series()`. Они предназначены для контроля выполнения задач. `series()` используется когда для следующей задачи нужен результат работы предидущей задачи. Остальные зачачи следует запускать паралельно используя `parallel()`.


## Ссылки
[Cheatsheet по gulp](https://github.com/osscafe/gulp-cheatsheet)
[Документация Gulp API](https://github.com/gulpjs/gulp/blob/4.0/docs/API.md)
[Рецепты](https://github.com/gulpjs/gulp/blob/4.0/docs/recipes/README.md)
[Gulp Awesome](https://github.com/alferov/awesome-gulp)
