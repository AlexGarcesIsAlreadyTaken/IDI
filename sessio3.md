# UNFIORMS
Variables globals que poden anar des del _GLWidget_ al shader
 - De lectura
 - Constants
 - Es creen i inicialitzen a l'aplicació
 - No van vertex a vertes, són globals

``` GLSL
#version 330 core

in vec3 vertex;
uniform float escalat;

void main {
  gl_position =  vec4 (vertex * escalat, 1.0);
}
```
> El valor assignat a _escalat_ a GLWidget serà compartit per tots els vertexs

``` GLSL
valLoc = glGetUniformLocation(program->programId(), "escalat"); //Obtenir direccio de 'escalat'
glUniform1f(valLoc, scl); //Enviem a 'escalat' el valor scl
```
> glGetUniformLocation amb una sola trucada és suficient \
> glUniform1f la podem cridar tants cops com vulguem modificar el valor d'escalat

    glUniform{1|2|3|4}{f|i|ui}{v}
    glUniformMatrix4fv(localització a shader, Nº matrius, transposada?, posició matriu);

# INTERACCIÓ AMB Qt

``` GLSL
#include <QkeyEvent>

virtual void mousePressEvent (QMouse Event *e)
virtual void mouseReleaseEvent (QMouse Event *e)
virtual void mouseMoveEvent (QMouse Event *e)
virtual void keyPressEvent (QKey Event *e)
```
> S'ha de declarar la funció al .h

``` GLSL
void MyGLWidget::keyPressEvent(QekyEvent *e) {
  makeCurrent();  //Necessari per activar el context OpenGL
  switch (e->key()) {
    case Qt::Key_S:
      scl += 0.1;
      glUniform1f(valLoc, scl);
      break;
    case Qt:Key_D:
      scl -= 0.1;
      glUniform1f(valLoc, scl);
      break;
    default: e->ignore();
  }
}
```

# TRANSFORMACIONS GEOMETRIQUES
```GLSL
void myGlWidget::modelTransform() {
  glm::mat4 TG (1.0);
  TG = glm::translate (TG, glm::vec3 (-0.5, 0.5, 0.0));
  glUniformMatrix4fv(transLoc, 1, GL_FALSE, &TG[0][0]);
}
```
> S'ha de cridar un cop just abans de cridar a PintarObjecte

```GLSL
 #define GLM_FORCE_RADIANS
```
Les transformaciosn geometriques s'apliquen dreta a esquerra (escriure de baix a dalt)
