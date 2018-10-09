---
layout: post 
title: OpenGL HowTo 2 - GLUT, GLFW, GLEW, etc.
tags: [opengl, cpp]
---

OpenGL повсеместно упоминается с какой-то из дополнительных библиотек. Что есть что и для чего все это?

<!--more-->

>Creating an OpenGL context usually requires writing platform-specific code to create a window. It also requires loading OpenGL functions manually from that context. These tools simplify these tasks greatly, in most cases providing cross-platform solutions. **-[Khronos](https://www.khronos.org/opengl/wiki/Related_toolkits_and_APIs){:target="_blank"}**

То есть, для работы с OpenGL требуется код для конкретной OS, который обеспечит взаимодействие с системой и создание окон, а также некоторые другие возможности. OpenGL - платформонезависимый интерфейс, поэтому и "оконная" библиотека должна быть кроссплатформенна. Рассмотрим наиболее популярные из них.

* **GLUT** - Open**GL** **U**tility **T**oolkit - стандартная библиотека для работы с окнами в OpenGL, но не входящая в состав OpenGL. Существенно не обновлялась с 1998 года. Устарела, но использовать можно. 
* **FreeGLUT** - открытая альтернатива GLUT - полная замена с небольшими отличиями.
* **GLFW** - актуальная и поддерживаемая замена GLUT для работы с современным OpenGL (OpenGL 3.2+).
* **SDL** - мультимедийная библиотека, реализующая единый программный интерфейс к графической подсистеме, звуковым устройствам и средствам ввода для широкого спектра платформ. Используется в основном для разработки игр, написана на C. 
* **SFML** - объектно-ориентированный аналог SDL на C++.
* **GLEW** - Open**GL** **E**xtension **W**rangler Library, **GLEE**, **gl3w** - библиотеки расширений OpenGL. Рекомендуется использовать GLEW.

**В итоге:** рекомендуется использовать GLFW & GLEW (или GLUT & GLEW для начала) или SFML & GLEW.

[Установка OpenGL с C++ в Eclipse]({{ site.baseurl }}/opengl&eclipse_macos){:target="_blank"}<br/>
[Учебные материалы по OpenGL]({{ site.baseurl }}/opengl&c++-howto){:target="_blank"}
