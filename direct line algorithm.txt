#include <GL/glut.h>
#include <math.h>

void init(void)
{
    glClearColor(0.0, 0.0, 0.0, 0.0); // Set the background color to black
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();
    gluOrtho2D(0.0, 640.0, 0.0, 480.0); // Set the viewport to be the entire window
}

void display(void)
{
    glClear(GL_COLOR_BUFFER_BIT); // Clear the color buffer

    float x1 = 100.0, y1 = 100.0, x2 = 400.0, y2 = 400.0;
    float dx = x2 - x1;
    float dy = y2 - y1;
    float m = dy / dx;

    if (fabs(m) <= 1)
    {
        float y = y1;
        for (float x = x1; x <= x2; x++)
        {
            glColor3f(1.0, 1.0, 1.0); // Set the color to white
            glBegin(GL_POINTS); // Set the primitive type to points
            glVertex2f(round(x), round(y)); // Set the point on the line
            glEnd(); // End drawing the point
            y += m;
        }
    }
    else
    {
        float x = x1;
        for (float y = y1; y <= y2; y++)
        {
            glColor3f(1.0, 1.0, 1.0); // Set the color to white
            glBegin(GL_POINTS); // Set the primitive type to points
            glVertex2f(round(x), round(y)); // Set the point on the line
            glEnd(); // End drawing the point
            x += 1 / m;
        }
    }

    glFlush(); // Render the line to the screen
}

int main(int argc, char** argv)
{
    glutInit(&argc, argv);
    glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);
    glutInitWindowSize(640, 480); // Set the window size
    glutInitWindowPosition(100, 100); // Set the window position
    glutCreateWindow("Direct Line Drawing Algorithm using GLUT"); // Set the window title
    init();
    glutDisplayFunc(display); // Set the display callback function
    glutMainLoop(); // Enter the event processing loop
    return 0;
}