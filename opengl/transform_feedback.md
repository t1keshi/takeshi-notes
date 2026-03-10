[OpenGL](_opengl.md)


# Transform Feedback

**Transform Feedback** é um estágio da pipeline de renderização relacionada a _primitive assembly_ onde os dados das primitivas são gravados em buffer object do usuário.


# Transform Feedback Objects

Este objeto guarda os seguintes estados:

- buffer object que está vinculado (_bound_) ao **transform feedback buffer binding points**  
- contadores indicando o quão cheio está o buffer  
- se este objeto está ativo  

```
    GLuint tfo;
    glGenTransformFeedbacks(1, &tfo);
    glBindTransformFeedback(GL_TRANSFORM_FEEDBACK, tfo);
    ...
    glIsTransformFeedback(tfo);
    glDeleteTransformFeedbacks(1, &tfo);
```

Se nenhum transform feedback object for vinculado ao contexto pela aplicação, existe um transform feedback object padrão com o _name_ 0. Isso significa que ao chamar ```glBindTransformFeedback(GL_TRANSFORM_FEEDBACK, 0)```, estamos ativando o transform feedback object padrão e desvinculando o objeto que estava vinculado anteriormente.


# Vinculando buffer object em Transform Feedback Object

- Múltiplos buffer objects podem ser vinculados ao transform feedback buffer binding points  
- Sub-seções de um buffer object podem ser vinculados ao transform feedback buffer binding points  
- Sub-seções de um mesmo buffer object podem ser vinculados a diferentes transform feedback buffer binding points simultaneamente  

```
    GLuint buffer;
    glGenBuffer(1, &buffer);
    glBindBuffer(GL_ARRAY_BUFFER, buffer);
    glBufferData(GL_ARRAY_BUFFER, 1024 * 1024, nullptr, 0);

    glTransformFeedbackBufferBase(tfo, GLuint index, buffer);
    glTransformFeedbackBufferRange(tfo, 0, buffer, 0, 0);
```

O indíce 0 para ```GLuint index``` é onde o transform feedback object padrão está vinculado.

> **Nota:** Utilizar 0 para ```GLenum usage``` em ```glBufferData``` significa que o buffer não será alterado pela CPU e que o driver de OpenGL irá otimizar para este uso.


# Exemplo de uso

```
```


# Referências

- KESSENICH, J. et al. OpenGL Programming Guide: the official guide to learning OpenGL, versions 4.5. 9th ed. Boston: Pearson Education, 2017.  
