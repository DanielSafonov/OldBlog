---
layout: post 
title: Аналитика для Jekyll
tags: [jekyll, web, seo]
image: google_analitics_jekyll.png
---
Как получить аналитику с блога на Jekyll?

<!--excerpt-->
{% raw %}
1. Создадим новый ресурст типа веб-сайт в [Google Analitics](https://analytics.google.com){:target="_blank"}
2. Создадим новый файл `_includes/analytics.html` и вставим туда сгенерированный Global Site Tag
3. Для того, чтобы скрипт аналитики при сборке автоматически был добавлен на каждую страницу блога, сделаем {% include %} в страндартный макет: вставим строку `{% include analytics.html %}` перед закрывающимся тэгом body в файл `_layouts/default.html`.
4. Вы великолепны: после сборки и выгрузки сайта на сервер, аналитика будет доступна в личном кабинете Google Analitics.
{% endraw %}