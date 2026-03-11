[OpenGL](_opengl.md)


# Drawing in OpenGL

The fundamental unit of rendering in OpenGL is known as the **primitive**.

Types of primitives supported of OpenGL:

- **Points**  
- **Lines**  
- **Triangle**
- **Patches** (input to tessellator)
- **adjancency primitives** (input to geometry sahder)  

> **Note:** Points, lines, and triangles are the _native_ primitive types supported by most graphics hardware. Isto significa que o hardware gráfico é capaz de rasterizar estas primitivas diretamente.

Primitives are made up of **vertices**. The vertices can come from a variety of sources - they can be read from files and then loaded into buffers by the C++/OpenGL application or they can be hardcoded in the C++ code or even in the GLSL code.

An **model** is constructed from these primitives.


# Points

Para renderizar pontos, OpenGL utiliza um conjunto de regras chamado **rasterization rules**.

Existem duas formas alterar o tamanho do ponto:

```
    void glPointSize(GLfloat size);
```

ou

```
    // in OpenGL application
    glEnable(GL_PROGRAM_POINT_SIZE);

    // in shader
    gl_PointSize = size;
```

> **Nota:** O comando ```glPointSize()``` só funcionará se ```GL_PROGRAM_POINT_SIZE``` estiver desabilitado.

Fragment shader disponibiliza a variável ```gl_PointCoord``` que contém as coordenadas do fragmento dentro do ponto. ```gl_PointCoord``` só está disponível em fragment shader e quando está renderizando pontos.


# Lines

As linhas são renderizadas pelo OpenGL através da regra **diamond exit rule**.

- Lines  
- Line loop  
- Line strip  

Para alterar a largura da linha:

```
    glLineWidth(GLfloat width);
```


# Triangles

- Triangles  
- Triangle loop  
- Triangle strip  

Quando dois triângulos compartilham a mesma aresta, OpenGL utiliza as seguintes regras:

- Nenhum pixel da aresta compartilha entre os dois triângulos devem ser deixados de renderizado.  
- Nenhum pixel da aresta compartilhada entre os dois triângulos devem ser renderizados mais de uma vez. 


# Rendering Polygons

Um polígono possui dois lados (_front_ e _back_) e eles podem ser renderizados diferentemente dependendo do lado que estiver de frente para o observador (_viewpoint_). Por padrão, as faces front e back são renderizadas da mesma forma.

Por convenção, polígonos cujo vértices são ordenados no sentido anti-horário são chamados de **front-facing**. Esta orientação é conhecida como **winding**. O comando ```glFrontFace``` permite alterar a orientação de anti-horário para horário e vice-versa.

```
    void glFrontFace(GLenum mode);
```

O comando ```glCullFace``` permite descartar a face frontal ou traseira (ou ambas).

```
    void glCullFace(GLenum mode);
```

O comando abaixo pode ser utilizado para especificar como o polígono deve ser renderizado: preenchido, somente linhas ou somente pontos.

```
    void glPolygonMode(GLenum face, GLenum mode);
```


# References

- KESSENICH, J. et al. OpenGL Programming Guide: the official guide to learning OpenGL, versions 4.5. 9th ed. Boston: Pearson Education, 2017.  