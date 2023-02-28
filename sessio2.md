# GLSL

Lenguatge d'alt nivell (basat en C) per programar shaders. **Multiplataforma**

### VERTEX SHADER
El VS és l'unic que pot llegir els VBOs

``` glsl
#version 330 core

int vec3 vertex;    // inVar

void main() {
    gl_Position = vec4(vertex, 1.0); // Guardem les coordenades de Clipping
}
```
> Aquest programa no fa cap TG (Transformació Geometrica)
---
### FRAGMENT SHADER

``` glsl
#version 330 core

out vec4 FragColor;

void main() {
    FragColor = vec4(1.);
}
```
> Retorna el color en negre
---
### TIPUS DE DADES

- **TIPUS BASICS**
	- **Escalars**: void, int, uint, float, bool...
	- **Vectorials**: vec2, vec3, mat2, mat4, mat2x3, ivec3, bvec4...
- **ALTRES**
	- **Arrays**: mat2, mat[3];
	- **Structs**
	``` glsl
	struct Light {
	    vec3 color;
	    vec3 pos;
	};
	light l1(col, p);
	```
	> _Els structs generen constructors implicitament_
---
---
La multiplicació de vectors es fa component a component
> vec1*vec2 = (x1·x2, y1·y2..)
---
---
Existeixen variables predefinides

``` glsl
1. out vec4 gl_position;    // Vertex Shader

1. in vec4 gl_FragCoord;    // Fragment Shader
2. out float gl_FragDepth;  // Fragment Shader
```
A _GLSL_ existeix la instrucció especial ```discard``` pel fragment shader que actua
com un ```return``` i descarta el fragment

# ESQUELET COMPLET

Existeixen dues classes Qt que usarem pels shaders
- **QOpenGLShader**
- **QOpenGLShaderProgram**

``` glsl
QOpenGLShader fs (QOpenGLShader::Fragment, this);
QOpenGLShader vs (QOpensGLShader::Vertex, this);    // Creen els FS i VS

fs.compileSourceFile("shaders/fragshad.frag");    // Carreguen el codi dels
vs.compileSourceFile("shaders/vertshad.vert");    // fitxers i els compila

program = new QOpenGLShaderProgram(this);    // Creem el program

program->addSahder(&fs);
program->addSahder(&vs);    // Afegim els shaders creats

program->link();

program->bind();
```

Cal indicar com passar la informació al shader. \
S'han d'enllaçar els atributs del shader a la nostra classe, obtenir la posició de l'atribut
a través del nom. \

``` glsl
vertexLoc = glGetAttribLocation (program->programID(), "vertex");

// glGetAttribLocation(GLuint program, const GLchar *name)
```
> program: Identificador del programa \
> name: nom de l'atribut en el VS

