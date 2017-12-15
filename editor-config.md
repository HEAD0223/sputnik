# Настройки редактора кода

## Введение

EditorConfig это конфигурационный файл и набор расширений, к большому количеству редакторов кода и IDE (Далее просто IDE).
Editor Config
Его задача — создать единый формат настроек, и, раз и навсегда, решить вопросы вроде “табы или пробелы” для всех IDE и всех языков программирования. Такой файл может храниться в системе контроля версий проекта, что позволит всем его разработчикам использовать одну и ту же конфигурацию.

Файлы .editorconfig можно найти в таких проектах, как jQuery, Ruby, WordPress, и многих других.

Плагины доступны для большого количество IDE

## Настройки

Если для вашего любимого редактора нет такого плагина (что маловероятно) то
установите в вашем редакторе следующие настройки, которые помогут избежать распространенных несогласованностей в коде и грязи:

* Использовать семантичную табуляцию вместо четырёх пробелов.
* Обрезать конечные пробелы при сохранении.
* Кодировка файлов utf-8.
* Добавлять новую строку в конец файлов.

Файл должен находится в корне проекта и иметь имя `.editorconfig`

Плагины для большнства редактров можно найти здесь [http://editorconfig.org/#download](http://editorconfig.org/#download)

**Пример: файла `.editorconfig`**

```ini
# EditorConfig is awesome: http://EditorConfig.org

# top-most EditorConfig file
root = true

# Unix-style newlines with a newline ending every file
[*]
end_of_line = LF
indent_style = tab
indent_size = 4
charset = utf-8
trim_trailing_whitespace = all
insert_final_newline = true

[*.jade]
trim_trailing_whitespace = false

[{package.json,.travis.yml}]
indent_style = space
indent_size = 2
```

## Ссылки

* [![habr]EditorConfig — Одни Настройки для всех Редакторов/IDE](https://habrahabr.ru/post/220131/)

[habr]: https://habrahabr.ru/images/favicons/favicon-16x16.png
