[OpenGL](_opengl.md)  

# Instancing Rendering

**Instancing Rendering** em OpenGL é um método bastante eficiente de realizar múltiplas chamadas de _draw calls_ utilizando uma única chamada.

Sempre que um comando de _draw call_ é executado, a GPU precisa realizar uma preparação dos dados para enviá-los na pipeline de renderização. Quando utilizamos instancing rendering, evitamos o overhead de preparação de dados para realizar múltiplas chamadas de _draw calls_.

Cada chamada de draw call em instancing rendering é chamada de **instância**.

```
    void glDrawArraysInstanced(	GLenum mode, GLint first, GLsizei count, GLsizei instancecount);
    void glDrawElementsInstanced(GLenum mode, GLsizei count, GLenum type, const void * indices, GLsizei instancecount);
```

Existem dois mecanismos para diferenciar as chamadas de desenho a partir do shader:

1. Permitir que atributos de vértice sejam passados por instância em vez de por vérice.  
2. Disponibilidade do índice (```gl_InstanceID```) da instância atual no shader.  

Quando é utilizado este tipo de _draw call_, vertex shader tem acesso a uma variável chamada ```gl_InstanceID``` que indica a instância que está sendo renderizada.


# ```glVertexAttribDivisor```

O comando ```glVertexAttribDivisor()``` especifica a frequência com que os atributos de vértice devem ser enviados na pipeline de renderização.

Por padrão, um novo valor do vertex array é enviado para cada vértice. Com o comando ```glVertexAttribDivisor()``` podemos especificar que um novo valor do vertex array seja enviado a cada N instâncias - todos os vértices da instância receberam o mesmo valor.


# Referências

- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.  
- KESSENICH, J. et al. OpenGL Programming Guide: the official guide to learning OpenGL, versions 4.5. 9th ed. Boston: Pearson Education, 2017.  