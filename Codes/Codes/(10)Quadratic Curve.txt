#include <windows.h>
#include <GL/glut.h>
GLfloat ctrlPoints[3][2] = { {-4.0, -2.0}, {0.0, 4.0}, {4.0, -2.0} };
GLfloat resolution = 0.01;  // Resolution of the curve

void drawQuadraticBezierCurve() {
    glClear(GL_COLOR_BUFFER_BIT);
    glColor3f(1.0, 0.0, 0.0); // Set color to red

    glBegin(GL_LINE_STRIP);
    for (GLfloat t = 0; t <= 1; t += resolution) {
        GLfloat x = (1 - t) * (1 - t) * ctrlPoints[0][0] + 2 * (1 - t) * t * ctrlPoints[1][0] + t * t * ctrlPoints[2][0];
        GLfloat y = (1 - t) * (1 - t) * ctrlPoints[0][1] + 2 * (1 - t) * t * ctrlPoints[1][1] + t * t * ctrlPoints[2][1];
        glVertex2f(x, y);
    }
    glEnd();

    glPointSize(5.0);
    glColor3f(0.0, 0.0, 1.0); // Set color to blue
    glBegin(GL_POINTS);
    for (int i = 0; i < 3; ++i) {
        glVertex2f(ctrlPoints[i][0], ctrlPoints[i][1]);
    }
    glEnd();

    glFlush();
}

void init() {
    glClearColor(1.0, 1.0, 1.0, 1.0);
    glMatrixMode(GL_PROJECTION);
    gluOrtho2D(-5.0, 5.0, -5.0, 5.0);
}

int main(int argc, char** argv) {
    glutInit(&argc, argv);
    glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);
    glutCreateWindow("OpenGL Quadratic Bezier Curve");
    glutDisplayFunc(drawQuadraticBezierCurve);

    init();

    glutMainLoop();
    return 0;
}
