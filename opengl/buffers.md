[OpenGL](_opengl.md)  


# OpenGL Buffers

**Buffer object** é um objeto que representa uma área da memória no hardware gráfico e é gerenciado pelo OpenGL. Existem vários tipos de buffer objects para armazenar diferentes tipos de dados.

Quando um buffer object é criado, é necessário vinculá-lo ao contexto para que OpenGL possa utilizá-lo.

1. Criar buffer object  
2. Vincular (_binding_) ao contexto OpenGL  


# Criando buffer object

O comando ```glGenBuffers``` (disponível desde a versão 2.0) é utilizado para obter um "nome" disponível para que a aplicação possa referenciar o buffer object que está na memória do hardware gráfico.

Os nomes retornados por ```glGenBuffers``` só vão estar associados de fato a um buffer object após vincular o objeto ao contexto com ```glBindBuffer```.

```
    GLuint buffer;
    glGenBuffers(1, &buffer);

    glBindBuffer(GL_ARRAY_BUFFER, buffer);
```

A partir da versão 4.5, foi criado o conceito de **Direct State Access (DSA)**, onde não é mais necessário vincular o buffer object ao contexto para poder inicializá-lo. Foram criados comandos novos para obter nomes de buffer object já inicializados como se estivessem vinculados a um **target point** não especificado - ou seja, não é necessário realizar o _binding_ para inicializar este buffer object com dados.

```
    GLuint buffer;
    glCreateBuffers(1, &buffer);
```

Para verificar se um buffer object é válido ou deletar buffers objects, utilizar estes comandos:

```
    GLboolean glIsBuffer(GLuint buffer);
    void glDeleteBuffers(GLsizei n, const GLuint* buffers);
```


# Buffer binding targets

Existem diferentes tipos de **binding targets** onde os buffer objects podem ser vinculados. OpenGL utiliza cada um destes targets para própositos diferentes. Por exemplo, ao executar o comando ```glVertexAttribPinter```, OpenGL utiliza o buffer object que estiver vinculado ao target ```GL_ARRAY_BUFFER```.

```
    void glBindBuffer(GLenum target, GLuint buffer);
```

Quando um buffer object é vinculado, o buffer object que estava vinculado anteriormente é desvinculado.


# Alocando espaço para o buffer object


```
    glNamedBufferStorage()
```

# Referências

- KESSENICH, J. et al. OpenGL Programming Guide: the official guide to learning OpenGL, versions 4.5. 9th ed. Boston: Pearson Education, 2017.  