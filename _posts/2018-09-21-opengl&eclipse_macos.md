---
layout: post 
title: Работа с OpenGL и GLUT в Eclipse на MacOS
tags: [opengl, cpp, IDE, eclipse, macos]
image: opengl_setup_macos.png
---

3 строки в IDE и вы великолепны!

<!--excerpt-->

*Да, в MacOS Mojave больше нет полноценной поддержки OpenGL в связи с тем, что Apple признала их устаревшими (ведь нужно продвигать нативный API Metal), но на данный момент я использую High Sierra, да и в дальнейшем приложения с OpenGL будут работать, но за их стабильность Apple не отвечает.*

Итак, мы хотим **запустить проект на C++ и OpenGL в MacOS с Eclipse**. Для этого необходимо выполнить всего 3 действия:

1. В созданном проекте переходим в настройки:  <br/>
`Project>Properties>C/C++ Build>Settings>Tool Settings>MacOS X Linker>Miscellaneous`. <br/>
Зетем добавляем флаги линковщику: <br/>
`Linker flags: -framework GLUT -framework openGL -framework Cocoa`

2. Добавляем в пути к библиотекам <br/>
`Project>Properties>C/C++ General>Paths and Symbols>Includes>GNU C++>Add` <br/>
Вот это: <br/>
`/System/Library/Frameworks/OpenGL.framework/Versions/A/Libraries/` <br/>
`/System/Library/Frameworks/GLUT.framework/Versions/A/Libraries/`

3. Подключаем GLUT и OpenGL в созданном проекте: <br/>
`#include <GLUT/glut.h>` <br/>
`#include <OpenGL/gl.h>`

4. **Вы великолепны:** библиотеки подключены и работоспособность проекта можно проверить следующим кодом (визуализация кода - на обложке поста):

```cpp
#include <GLUT/glut.h>
#include <OpenGL/gl.h>

char title[] = "Rotating Pyramid";
GLfloat anglePyramid = 0.0f;  // Rotational angle for pyramid
int refreshMills = 15;        // refresh interval in milliseconds

void initGL() {
	glClearColor(0.0f, 0.0f, 0.0f, 1.0f); // Set background color to black and opaque
	glClearDepth(1.0f);                   // Set background depth to farthest
	glEnable(GL_DEPTH_TEST);   // Enable depth testing for z-culling
	glDepthFunc(GL_LEQUAL);    // Set the type of depth-test
	glShadeModel(GL_SMOOTH);   // Enable smooth shading
	glHint(GL_PERSPECTIVE_CORRECTION_HINT, GL_NICEST); // Nice perspective corrections
}


void display() {
	glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT); // Clear color and depth buffers
	glMatrixMode(GL_MODELVIEW);     // To operate on model-view matrix

	glTranslatef(0.0f, -1.0f, 0.0f);


	glDisable(GL_LIGHTING);
	// OZ GREEN
	glBegin(GL_LINES);
	glColor3f(0.0f, 1.0f, 0.0f);
	glVertex3f(0.0f, 0.0f, 0.0f);
	glVertex3f(0.0f, 30.0f, 0.0f);
	glEnd();


	glLoadIdentity();                  // Reset the model-view matrix
	glTranslatef(.0f, 0.0f, -7.0f);  // Move center and into the screen
	glRotatef(anglePyramid, 0.0f, 1.0f, .0f);  // Rotate about the Z-axis

	glBegin(GL_TRIANGLES);         // Begin drawing the pyramid with 4 triangles
	// Front
	glColor3f(1.0f, 0.0f, 0.0f);     // Red
	glVertex3f(0.0f, 1.0f, 0.0f);
	glColor3f(0.0f, 1.0f, 0.0f);     // Green
	glVertex3f(-1.0f, -1.0f, 1.0f);
	glColor3f(0.0f, 0.0f, 1.0f);     // Blue
	glVertex3f(1.0f, -1.0f, 1.0f);

	// Right
	glColor3f(1.0f, 0.0f, 0.0f);     // Red
	glVertex3f(0.0f, 1.0f, 0.0f);
	glColor3f(0.0f, 0.0f, 1.0f);     // Blue
	glVertex3f(1.0f, -1.0f, 1.0f);
	glColor3f(0.0f, 1.0f, 0.0f);     // Green
	glVertex3f(1.0f, -1.0f, -1.0f);

	// Back
	glColor3f(1.0f, 0.0f, 0.0f);     // Red
	glVertex3f(0.0f, 1.0f, 0.0f);
	glColor3f(0.0f, 1.0f, 0.0f);     // Green
	glVertex3f(1.0f, -1.0f, -1.0f);
	glColor3f(0.0f, 0.0f, 1.0f);     // Blue
	glVertex3f(-1.0f, -1.0f, -1.0f);

	// Left
	glColor3f(1.0f, 0.0f, 0.0f);       // Red
	glVertex3f(0.0f, 1.0f, 0.0f);
	glColor3f(0.0f, 0.0f, 1.0f);       // Blue
	glVertex3f(-1.0f, -1.0f, -1.0f);
	glColor3f(0.0f, 1.0f, 0.0f);       // Green
	glVertex3f(-1.0f, -1.0f, 1.0f);
	glEnd();   // Done drawing the pyramid


	glTranslatef(0.0f, 0.0f, 0.0f);

	glutSwapBuffers(); // Swap the front and back frame buffers (double buffering)

	anglePyramid += 0.5f; // Update the rotational angle after each refresh
}


void timer(int value) {
	glutPostRedisplay();      // Post re-paint request to activate display()
	glutTimerFunc(refreshMills, timer, 0); // next timer call milliseconds later
}


void reshape(GLsizei width, GLsizei height) { // GLsizei for non-negative integer
	// Compute aspect ratio of the new window
	if (height == 0)
		height = 1;                // To prevent divide by 0
	GLfloat aspect = (GLfloat) width / (GLfloat) height;

	// Set the viewport to cover the new window
	glViewport(0, 0, width, height);

	// Set the aspect ratio of the clipping volume to match the viewport
	glMatrixMode(GL_PROJECTION);  // To operate on the Projection matrix
	glLoadIdentity();             // Reset
	// Enable perspective projection with fovy, aspect, zNear and zFar
	gluPerspective(45.0f, aspect, 0.1f, 100.0f);
}


int main(int argc, char** argv) {
	glutInit(&argc, argv);            // Initialize GLUT
	glutInitDisplayMode(GLUT_DOUBLE); // Enable double buffered mode
	glutInitWindowSize(640, 480);   // Set the window's initial width & height
	glutInitWindowPosition(100, 100); // Position the window's initial top-left corner
	glutCreateWindow(title);          // Create window with the given title
	glutDisplayFunc(display); // Register callback handler for window re- apaint event
	glutReshapeFunc(reshape); // Register callback handler for window re-size event
	initGL();                       // Our own OpenGL initialization
	glutTimerFunc(0, timer, 0);     // First timer call immediately
	glutMainLoop();                 // Enter the infinite event-processing loop
	return 0;
}
```