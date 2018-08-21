---
layout: post 
title: Шаблонизатор для html
tags: [web, jekyll]
image: gulp.jpg
---

Аналог шаблонизатора liquid для сайтов без фреймворков/CMS.

<!--excerpt-->

Данный блог создан на статическом генераторе сайтов Jekyll. ([Об этом здесь]({{ site.baseurl }}/jekyll_how_to){:target="_blank"}

Jekyll использует написанный на Ruby язык шаблонов [liquid](https://shopify.github.io/liquid/){:target="_blank"}. Суть шаблонизации заключается в том, что в корне проекта есть директория `_layouts`, которая содержит в себе макеты страниц - стандартный макет и основанные на нем макеты страницы с постом и произвольной страницы. При сборке проекта Jekyll создает страницы путем подстановки Markdown в макеты страниц. Данная страница собрана на макете поста (`post.html`), страница About - на макете произвольной страницы. 

Все страницы сайта содержат в себе одинаковый блок `<head>..</head>`, поэтому в корне проекта имеется директория `_includes` с файлом `head.html`, содержащим весь блок `<head>..</head>`.

Получается, что при сборке проекта, Jekyll делает подстановку кода из директории `_includes` в соответствующие места шаблонов {% raw %}(например - `{% include head.html %}`){% endraw %}, а затем подстановку текстов страниц в Markdown в соответствующие им макеты страниц (например - `layout: post`). В итоге в директории `_site` мы имеем собранный статический сайт.

<h3 style="color: #4b86b4;">Так о чем вообще все это?</h3>

Хотелось перенести возможности liquid в формат небольшой утилиты для сборки html страничек из модулей: <header>, шапка, подвал, галерея или любой другой повторяющийся блок.

С задачами статической вставки фрагментов кода справится модуль [gulp-rigger](https://www.npmjs.com/package/gulp-rigger){:target="_blank"}, а для вставки с параметрами можно использовать шаблонизатор [Nunjucks.js](https://mozilla.github.io/nunjucks/){:target="_blank"}.
* [How to Modularize HTML Using Template Engines and Gulp](https://zellwk.com/blog/nunjucks-with-gulp/){:target="_blank"}
* [Four Killer Features of Nunjucks](https://css-tricks.com/killer-features-of-nunjucks/){:target="_blank"}

<h1 style="text-align: center;">...</h1>
