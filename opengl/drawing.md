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


# References

- KESSENICH, J. et al. OpenGL Programming Guide: the official guide to learning OpenGL, versions 4.5. 9th ed. Boston: Pearson Education, 2017.  