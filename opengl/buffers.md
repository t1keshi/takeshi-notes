[OpenGL](_opengl.md)  


# OpenGL Buffers

**Buffer object** é um objeto que representa uma área da memória no hardware gráfico e é gerenciado pelo OpenGL. Existem vários tipos de buffer objects para armazenar diferentes tipos de dados.

Quando um buffer object é criado, é necessário vinculá-lo (_binding_) ao contexto para que OpenGL possa utilizá-lo.


# Criando buffer object

O comando ```glGenBuffers``` (disponível desde a versão 2.0) é utilizado para obter "nomes" disponíveis para que a aplicação possa referenciar o buffer object na memória do hardware gráfico.

Os nomes retornados por ```glGenBuffers``` só vão estar associados de fato a um buffer object após vincular o objeto ao contexto OpenGL com ```glBindBuffer```.

```
    GLuint buffer;
    glGenBuffers(1, &buffer);

    glBindBuffer(GL_ARRAY_BUFFER, buffer);
```

A partir da versão 4.5, foi criado o conceito de **Direct State Access (DSA)**, onde não é mais necessário vincular o buffer object ao contexto para poder inicializá-lo. Foram criados comandos novos para obter nomes de buffer object que são inicializados como se estivessem vinculados a um **target point** não especificado - ou seja, não é mais necessário realizar o _binding_ para inicializar o buffer object com dados.

```
    GLuint buffer;
    glCreateBuffers(1, &buffer);
```

Para verificar se um buffer object é válido ou deletar buffers objects, basta utilizar estes comandos:

```
    GLboolean glIsBuffer(GLuint buffer);
    void glDeleteBuffers(GLsizei n, const GLuint* buffers);
```


# Buffer binding targets

Existem diferentes tipos de **binding targets** onde os buffer objects podem ser vinculados ao contexto. OpenGL utiliza cada um destes targets para própositos diferentes. Por exemplo, ao executar o comando ```glVertexAttribPinter```, OpenGL utiliza o buffer object que estiver vinculado ao target ```GL_ARRAY_BUFFER```.

Quando um buffer object é vinculado, o buffer object que estava vinculado anteriormente é desvinculado.


# Populando dados em buffer objects

O comando ```glBufferData``` (disponível desde a versão 2.0) cria um novo armazenamento para o buffer object (qualquer pré-armazenamento criado anteriormente será deletado). OpenGL irá utilizar o buffer object que estiver vinculado ao _binding target_. Se o parâmetro ```data``` for ```NULL```, o espaço para armazenamento ainda é criado mas o seu conteúdo não será inicializado (_undefined_).

```
    void glBufferData(GLenum target, GLsizeiptr size, const void* data, GLenum usage);
```

Na versão 4.5, foi disponibilizado o comando ```glNamedBufferData``` que também cria um novo armazenamento mas para o buffer object especificado no parâmetro ```bufferName``` e não o buffer object que estiver vinculado ao _binding target_. Este comando está de acordo com o conceito de **Direct State Access (DSA)**.

```
    void glNamedBufferData(GLuint bufferName, GLsizeiptr size, const void* data, GLenum usage);
```

Na versão 4.4, também foi introduzido o conceito de **immutable data store** com o comando ```glBufferStorage```. Neste tipo de armazenamento não é possível alterar o tamanho do espaço criado. No caso do comando ```glBufferData```, é possível chamar novamente este comando para criar um novo espaço com um tamanho diferente. Criar armazenamento imutável é eficiente em hardwares gráficos modernos melhorando o desempenho da aplicação OpenGL. Existem também a versão DSA de ```glBufferStorage``` a partir da versão 4.5: ```glNamedBufferStorage```.

```
    void glBufferStorage(GLenum target, GLsizeiptr size, const void* data, GLbitfield flags);
    void glNamedBufferStorage(GLuint buffer, GLsizeiptr size, const void* data, GLbitfield flags)
```

> **Nota:** Em todos os casos acima, escolher o valor correto para os parâmetros ```usage``` e ```flags``` é importante para otimizar o desempenho e obter o comportamento correto.


# Populando apenas uma parte do buffer object

Os comandos ```glBufferSubData``` (disponível a partir de 2.0) e ```glNamedBufferSubData``` (disponível a partir de 4.5) permitem redefinir uma parte (ou inteiramente) o conteúdo de um buffer object com espaço de armazenamento alocado anteriormente.

```
void glBufferSubData(GLenum target, GLintptr offset, GLsizeiptr size, const void * data);
void glNamedBufferSubData(	GLuint buffer, GLintptr offset,  GLsizeiptr size, const void *data);
```


# Preenchendo o conteúdo de buffer object com dados da aplicação

Os comandos ```glClearBufferData``` (disponível a partir de 4.3) e ```glClearNamedBufferData``` (disponível a partir de 4.5) preenchem todo conteúdo de um buffer object com um valor conhecido.

```
    void glClearBufferData(GLenum target, GLenum internalFormat, GLenum format, GLenum type, const void* data);
    void glClearNamedBufferData(GLuint buffer, GLenum internalFormat, GLenum format, GLenum type, const void* data);
```

Existem também os comandos ```glClearBufferSubData``` (disponível a partir de 4.3) e ```glClearNamedBufferSubData``` (disponível a partir de 4.5) para preencher partes de um buffer object.

```
void glClearBufferSubData(GLenum target, GLenum internalformat, GLintptr offset, GLsizeiptr size, GLenum format, GLenum type, const void * data);
 
void glClearNamedBufferSubData(	GLuint buffer, GLenum internalformat, GLintptr offset, GLsizeiptr size, GLenum format, GLenum type, const void *data);
```

Utilizar estes comandos permite preencher os dados (_data store_) de um buffer object de forma otimizada sem a necessidade de reservar e limpar a região de memória.


# Copiando dados de um buffer object para outro

Para copiar parte dos dados de um buffer object em outro buffer object, existem os comandos ```glCopyBufferSubData``` (disponível a partir de 3.1) e ```glCopyNamedBufferSubData``` (disponível a partir de 4.5).

```
void glCopyBufferSubData(GLenum readTarget, GLenum writeTarget, GLintptr readOffset, GLintptr writeOffset, GLsizeiptr size);

void glCopyNamedBufferSubData(GLuint readBuffer, GLuint writeBuffer, GLintptr readOffset, GLintptr writeOffset, GLsizeiptr size);
```

No caso de ```glCopyBufferSubData```, é necessário utilizar ```GL_COPY_READ_BUFFER``` e ```GL_COPY_WRITE_BUFFER``` binding targets para copiar dados sem afetar outras operações de OpenGL.


# Lendo os dados de um buffer object

Para obter os dados de um buffer object, existem dois comandos: ```glGetBufferSubData``` (disponível a partir de 2.0) e ```glGetNamedBufferSubData``` (disponível a partir de 4.5).


# Acessando o conteúdo com ```glMapBuffer```

Todos os comandos acima envolvem cópias de dados, seja da memória da aplicação para buffer object, de um buffer object para outro buffer object ou de um buffer object para memória da aplicação.

Dependendo da configuração de hardware, é possível utilizar os comandos ```glMapBuffer```(disponível a partir da versão 2.0) e ```glMapNamedBuffer``` (disponível a partir da versão 4.5) para obter acesso a memória alocada pelo OpenGL através de um ponteiro.

```
    void* glMapBuffer(GLenum target, GLenum access);
    void* glMapNamedBuffer(GLuint buffer, GLenum access);
```

O comando ```glMapBuffer``` retorna um ponteiro para a memória que "representa" o armazenamento de dados do buffer object vinculado ao target. Isso significa que esta memória pode não ser a memória que será utilizada pela GPU.

Após a utilização da memória, a aplicação abdica do ponteiro através do comando ```glUnmapBuffer``` (disponível a partir da versão 2.0) e ```glUnmapNamedBuffer``` (disponível a partir da versão 4.5).

```
    GLboolean glUnmapBuffer(GLenum target);
    GLboolean glUnmapNamedBuffer(GLuint buffer);
```

> **Nota:** Se os dados do buffer object estiver inacessível para a aplicação na chamada de ```glMapBuffer```, OpenGL poderá mover estes dados para tornar acessível. Da mesma forma, após a aplicação utilizar a memória, OpenGL poderá mover os dados para uma área acessível para a GPU. Este processo tem um custo de desempenho alto.

Exemplo de uso:

```
    GLuint buffer;
    glGenBuffers(1, &buffer);
    glBindBuffer(GL_COPY_WRITE_BUFFER, buffer);
    glBufferData(GL_COPY_WRITE_BUFFER, size, NULL, GL_STATIC_DRAW);

    void* dataFromGPU = glMapBuffer(GL_COPY_WRITE_BUFFER, GL_WRITE_ONLY);

    copy(data, dataFromGPU);

    glUnmapBuffer(GL_COPY_WRITE_BUFFER);
```

O exemplo acima mostra que, uma vez mapeado, não há cópia da aplicação para a GPU e nem cópia da GPU para a aplicação.


# Referências

- KESSENICH, J. et al. OpenGL Programming Guide: the official guide to learning OpenGL, versions 4.5. 9th ed. Boston: Pearson Education, 2017.  