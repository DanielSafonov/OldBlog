---
layout: post 
title: OpenGL HowTo 0.2 - Mojave Fix
tags: [opengl, cpp, macos]
---

>Да, в MacOS Mojave больше нет полноценной поддержки OpenGL в связи с тем, что Apple признала их устаревшими (ведь нужно продвигать нативный API Metal), но на данный момент я использую High Sierra, да и в дальнейшем приложения с OpenGL будут работать, но за их стабильность Apple не отвечает. — [OpenGL HowTo 0 - работа в Eclipse на MacOS]({{ site.baseurl }}/opengl&eclipse-macos){:target="_blank"}

Все таки, в Mojave все сломалось, но есть рабочий костыль!

<!--more-->

```cpp
/*
* Задача 2: вывести треугольник красного цвета
*/

//Отключение сообщения об отсутствии поддержки OpenGL в MacOS Mojave (Eclipse)
#define GL_SILENCE_DEPRECATION silence

//Подключение библиотек
#ifdef __APPLE__
#include <GLUT/glut.h> //GLUT
#include <OpenGL/gl.h> //OpenGL
#else
#include <GL/glut.h> //GLUT
#include <OpenGL/gl.h> //OpenGL
#endif

//Глобальные переменные
bool MojaveWorkAround = true; //Костыль для Mojave
int size = 480; //Размер окна

//Функция отрисовки
void display(void) {
	//Костыль для Mojave
	if (MojaveWorkAround) {
		glutReshapeWindow(size + 1, size + 1);
		MojaveWorkAround = false;
	}

	//Очистка экрана
	glClear(GL_COLOR_BUFFER_BIT);

	//Отрисовка треугольника
	glBegin(GL_TRIANGLES);
	glColor3f(0.7, 0, 0); //Установка цвета отрисовки
	glVertex3f(-0.5, -0.5, 0); //Левая вершина
	glVertex3f(0.5, -0.5, 0); //Правая вершина
	glVertex3f(0, 0.5, 0); //Верхняя вершина
	glEnd();

	//Выгрузка кадра из буфера на экран
	glutSwapBuffers();

	//Костыль для Mojave
	glutPostRedisplay();
}

//Функция обработки события изменения размера окна
void reshape(int w, int h) {
	glViewport(0, 0, size + 1, size + 1); //Установка области видимости равным изначальному размеру окна
}

//Главная функция
int main(int argc, char **argv) {
	//Инициализация окна
	glutInit(&argc, argv); //Инициализация GLUT
	glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGBA | GLUT_DEPTH); //Режим отображения
	glutInitWindowSize(size, size); //Размер окна
	glutInitWindowPosition(100, 100); //Позиция окна на экране
	glutCreateWindow("Part 2"); //Title окна
	glClearColor(1.0, 1.0, 1.0, 1.0); //Задание цвета очистки экрана
	glClear(GL_COLOR_BUFFER_BIT); //Очистка экрана

	//Функция отрисовки окна
	glutDisplayFunc(display);

	//Функция обработки события изменения размера окна
	glutReshapeFunc(reshape);

	//Основной цикл GLUT
	glutMainLoop();

	return 0;
}
```