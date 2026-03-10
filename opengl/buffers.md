[OpenGL](_opengl.md)  

# OpenGL Buffers

A **buffer object** is memory that the OpenGL server allocates and owns, and almost all data passed into OpenGL is done by storing the data in a buffer object.

# Criando objetos

A partir da versão OpenGL 2.0, o comando ```glGenBuffers``` estava disponível para que 

```
    GLuint buffer;
    glGenBuffers(1, &buffer);
    glBindBuffer(GL_ARRAY_BUFFER, buffer);
```

# Referências

- KESSENICH, J. et al. OpenGL Programming Guide: the official guide to learning OpenGL, versions 4.5. 9th ed. Boston: Pearson Education, 2017.  