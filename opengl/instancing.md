[OpenGL](_opengl.md)  

# Instancing Rendering

**Instancing Rendering** em OpenGL é uma maneira de realizar múltiplas chamadas de _draw calls_ utilizando uma única chamada.

```
    void glDrawArraysInstanced(	GLenum mode, GLint first, GLsizei count, GLsizei instancecount);
    void glDrawElementsInstanced(GLenum mode, GLsizei count, GLenum type, const void * indices, GLsizei instancecount);
```

Quando é utilizado este tipo de _draw call_, vertex shader tem acesso a uma variável chamada ```gl_InstanceID``` que indica a instância que está sendo renderizada.


# Referências

- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.  