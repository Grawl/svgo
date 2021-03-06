[english](https://github.com/svg/svgo/blob/master/README.md) | **русский**
- - -

<img src="http://soulshine.in/svgo/logo.svg?v3" width="200" height="200" alt="logo"/>

## SVGO v0.2.0 [![Build Status](https://secure.travis-ci.org/svg/svgo.png)](http://travis-ci.org/svg/svgo)

**SVG** **O**ptimizer – это инструмент для оптимизации векторной графики в формате SVG, написанный на Node.js.
![](//mc.yandex.ru/watch/18431326)

## Зачем?

SVG файлы, особенно экспортированные из различных редакторов, содержат много избыточной и бесполезной информации, комментариев, скрытых элементов, неоптимальные или дефолтные значения и другой мусор, удаление которого безопасно и не влияет на конечный результат рендеринга.

## Возможности

SVGO имеет плагинную архитектуру, в которой практически каждая оптимизация является отдельным плагином.

Сегодня у нас есть:

* [ [>](https://github.com/svg/svgo/blob/master/plugins/cleanupAttrs.js) ] удаление переносов строк и лишних пробелов
* [ [>](https://github.com/svg/svgo/blob/master/plugins/removeDoctype.js) ] удаление doctype
* [ [>](https://github.com/svg/svgo/blob/master/plugins/removeXMLProcInst.js) ] удаление XML-инструкций
* [ [>](https://github.com/svg/svgo/blob/master/plugins/removeComments.js) ] удаление комментариев
* [ [>](https://github.com/svg/svgo/blob/master/plugins/removeMetadata.js) ] удаление `<metadata>`
* [ [>](https://github.com/svg/svgo/blob/master/plugins/removeEditorsNSData.js) ] удаление пространств имён различных редакторов, их элементов и атрибутов
* [ [>](https://github.com/svg/svgo/blob/master/plugins/removeEmptyAttrs.js) ] удаление пустых атрибутов
* [ [>](https://github.com/svg/svgo/blob/master/plugins/removeHiddenElems.js) ] удаление скрытых элементов
* [ [>](https://github.com/svg/svgo/blob/master/plugins/removeEmptyText.js) ] удаление пустых текстовых элементов
* [ [>](https://github.com/svg/svgo/blob/master/plugins/removeEmptyContainers.js) ] удаление пустых элементов-контейнеров
* [ [>](https://github.com/svg/svgo/blob/master/plugins/removeViewBox.js) ] удаление атрибута `viewBox` когда это возможно
* [ [>](https://github.com/svg/svgo/blob/master/plugins/cleanupEnableBackground.js) ] удаление или оптимизация атрибута `enable-background` когда это возможно
* [ [>](https://github.com/svg/svgo/blob/master/plugins/convertStyleToAttrs.js) ] конвертирование стилей в атрибуте `style` в отдельные svg-атрибуты
* [ [>](https://github.com/svg/svgo/blob/master/plugins/convertColors.js) ] конвертирование цветовых значений (из `rgb()` в `#rrggbb`, из `#rrggbb` в `#rgb`)
* [ [>](https://github.com/svg/svgo/blob/master/plugins/convertPathData.js) ] конвертирование данных в Path в относительные координаты, конвертирование одних типов сегментов в другие, удаление ненужных разделителей и многое другое
* [ [>](https://github.com/svg/svgo/blob/master/plugins/convertTransform.js) ] схлопывание нескольких трансформаций в одну, конвертирование матриц в короткие алиасы и многое другое
* [ [>](https://github.com/svg/svgo/blob/master/plugins/removeUnknownsAndDefaults.js) ] удаление неизвестных элементов, контента и атрибутов
* [ [>](https://github.com/svg/svgo/blob/master/plugins/removeUnusedNS.js) ] удаление  деклараций неиспользуемых пространств имён
* [ [>](https://github.com/svg/svgo/blob/master/plugins/cleanupIDs.js) ] удаление неиспользуемых и сокращение используемых ID
* [ [>](https://github.com/svg/svgo/blob/master/plugins/cleanupNumericValues.js) ] округление дробных чисел до заданной точности, удаление `px` как единицы измерения по умолчанию
* [ [>](https://github.com/svg/svgo/blob/master/plugins/moveElemsAttrsToGroup.js) ] перемещение совпадающих атрибутов у всех элементов внутри группы `<g>`
* [ [>](https://github.com/svg/svgo/blob/master/plugins/collapseGroups.js) ] схлопывание бесполезных групп `<g>`

Хотите узнать, как это работает и как написать свой плагин? [Конечно же да](https://github.com/svg/svgo/blob/master/docs/how-it-works/ru.md).


## Как использовать

```sh
$ [sudo] npm install -g svgo
```

```
Usage:
  svgo [OPTIONS] [ARGS]

Options:
  -h, --help : Help
  -v, --version : Version
  -i INPUT, --input=INPUT : Input file, "-" for STDIN
  -s STRING, --string=STRING : Input SVG data string
  -f FOLDER, --folder=FOLDER : Input folder, optimize and rewrite all *.svg files
  -o OUTPUT, --output=OUTPUT : Output file (by default the same as the input), "-" for STDOUT
  -c CONFIG, --config=CONFIG : Local config file to extend default
  --disable=DISABLE : Disable plugin by name
  --enable=ENABLE : Enable plugin by name
  --datauri : Output as Data URI base64 string
  --pretty : Make SVG pretty printed

Arguments:
  INPUT : Alias to --input
  OUTPUT : Alias to --output
```

* с файлами:

        $ svgo test.svg

    или:

        $ svgo test.svg test.min.svg

* с STDIN / STDOUT:

        $ cat test.svg | svgo -i - -o - > test.min.svg

* с папками

        $ svgo -f ../path/to/folder/with/svg/files

* со строками:

        $ svgo -s '<svg version="1.1">test</svg>' -o test.min.svg

    или даже с Data URI base64:

        $ svgo -s 'data:image/svg+xml;base64,…' -o test.min.svg

* с SVGZ:

    из `.svgz` в `.svg`:

        $ gunzip -c test.svgz | svgo -i - -o test.min.svg

    из `.svg` в `.svgz`:

        $ svgo test.svg -o - | gzip -cfq9 > test.svgz

* с помощью GUI – [svgo-gui](https://github.com/svg/svgo-gui)
* как модуль Node.js – [examples](https://github.com/svg/svgo/tree/master/examples)
* как таск для Grunt – [svgo-grunt](https://github.com/svg/svgo-grunt)
* как действие папки в OSX – [svgo-osx-folder-action](https://github.com/svg/svgo-osx-folder-action)

## TODO

* [v0.2.x](https://github.com/svg/svgo/issues?milestone=7&state=open)


## Лицензия и копирайты

Данное программное обеспечение выпускается под [лицензией MIT](https://github.com/svg/svgo/blob/master/LICENSE).

Логотип – [Егор Большаков](http://xizzzy.ru/).
