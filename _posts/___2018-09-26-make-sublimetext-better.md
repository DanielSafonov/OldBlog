---
layout: post 
title: Как сделать Sublime Text 3 лучше
tags: [IDE]
image: better_sublime_text.png
---

Именно в этом текстовом редакторе были написны все статьи для этого блога (да и сам блог).

<!--more-->

Ссылка на загрузку Sumlime Text 3 https://www.sublimetext.com/3

Веб-интерфейс менеджера пакетов https://packagecontrol.io

Тема https://packagecontrol.io/packages/ayu
Моя прошлая тема https://packagecontrol.io/packages/Boxy%20Theme
Иконки для разных типов файлов https://packagecontrol.io/packages/A%20File%20Icon

ctrl/⌘+shift+p


Идем в пользовательские настройки кнопок: Preferences - Key Binding,  идем во вкладку User (вторая вкладка),  тыкаем в нее курсор, вставляем туда:
[
{ "keys": ["alt+shift+f"], "command": "reindent" },
]
Эта запись добавляет горячие клавиши alt+shift+f для команды reindent - форматирования выделенного кода (выравнивания отступов).

[
	{
		"keys": ["ctrl+command+f"], "command": "reindent", "args": {"single_line": false}
	},
	{ 
		"keys": ["option+space"], "command": "auto_complete" 
	}
]

Как вставить фрагмент Lorem Ipsum?
Набираем "lorem" в месте вставки и нажимаем Tab

Теперь, чтобы установить или удалить плагин для Sublime Text, жмем command+shift+p ( Ctrl+Shift+P), вводим install Package или remove Package, выбираем, пишем название плагина, выбираем его из списка, жмем Enter.

AutoFileName - автодополнение пути к файлу

AllAutocomplete
Классическое автодополнение в Sublime Text работает только с текущим файлом. AllAutocomplete осуществляет поиск по всем файлам открытым в текущем окне, что значительно упрощает процесс разработки. Также существует плагин CodeIntel, который воплощает в себе возможности IDE и помимо умного автокомплита привносит в Sublime «Code Intelligence» для ряда языков: JavaScript, Mason, XBL, XUL, RHTML, SCSS, Python, HTML, Ruby, Python3, XML, Sass, XSLT, Django, HTML5, Perl, CSS, Twig, Less, Smarty, Node.js, Tcl, TemplateToolkit, PHP.

DocBlockr
DocBlockr станет для вас эффективным помощником при документировании кода. После ввода /** и нажатия на клавишу Tab плагин автоматически распарсит любую функцию и подготовит соответствующий шаблон.

ColorPicker
Обычно, когда нам требуется цветовая палитра мы привыкли использовать Photoshop или Gimp. Но полноценный color picker может быть прямо в окне вашего редактора — Ctrl/Cmd + Shift + C. А еще есть замечательные GutterColor и ColorHighlighter, которые упрощают ориентирование в цветовых кодах: 

ColorHighlighter выделяет значения цвета. Он поддерживает hex, rgb, rgba, hsl, hsla, а также выделяет цветовые переменные Less и Sass.

MarkdownPreview или MarkdownEditing

Alignment — функциональное выравнивание фрагментов кода от автора Package Control.

SublimeLinter
Помогает находить синтаксические ошибки в коде подсвечивая их. На данный момент поддерживаются PHP, Javascript, Java, CSS, HTML, HAML, Python, Ruby, Json, CoffeeScript, Google Closure, XML, React.js, Slim, Markdown, Go, Perl, C, C++, SQL, Twig, Bootstrap, Jade, LESS, SASS.

Git
Этот плагин добавляет возможность пользоваться всеми необходимыми для разработки функциями Git: add, commit, доступ к логам – и все это не покидая Sublime!

Строки не должны заканчиваться пустыми символами.
Для этого используем плагин TrailingSpaces.
