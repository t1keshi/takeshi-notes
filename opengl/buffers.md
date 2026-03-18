[OpenGL](_opengl.md)  


# OpenGL Buffers

**Buffer object** é um objeto que representa uma área de armazenamento de dados (_data store_) do hardware gráfico e é gerenciado pelo OpenGL. Existem vários tipos de buffer objects para armazenar diferentes tipos de dados.

Quando um buffer object é criado, é necessário vinculá-lo (_binding_) ao contexto para que OpenGL possa utilizá-lo.


# Criando buffer object

O comando ```glGenBuffers``` (disponível desde a versão 2.0) é utilizado para obter "nomes" disponíveis para que a aplicação possa referenciar os buffer objects do hardware gráfico. Entretanto, os nomes retornados por ```glGenBuffers``` só vão estar associados de fato a um buffer object após vincular o buffer object a algum **binding target point** do contexto OpenGL com ```glBindBuffer```.

```
    GLuint buffer;
    glGenBuffers(1, &buffer);

    glBindBuffer(GL_ARRAY_BUFFER, buffer);
```

Existem diversos binding target points para diferentes tipos de buffer objects como ```GL_ARRAY_BUFFER```,```GL_ELEMENT_ARRAY_BUFFER```, etc. 

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

Na versão 4.4, também foi introduzido o conceito de **immutable data store** com o comando ```glBufferStorage```. Neste tipo de armazenamento não é possível alterar o tamanho do espaço criado. No caso do comando ```glBufferData```, é possível chamar novamente este comando para criar um novo espaço com um tamanho diferente. Criar armazenamento imutável é eficiente em hardwares gráficos modernos melhorando o desempenho da aplicação OpenGL. A versão DSA de ```glBufferStorage``` a partir da versão 4.5 é ```glNamedBufferStorage```.

```
    void glBufferStorage(GLenum target, GLsizeiptr size, const void* data, GLbitfield flags);
    void glNamedBufferStorage(GLuint buffer, GLsizeiptr size, const void* data, GLbitfield flags)
```

> **Nota:** Em todos os casos acima, escolher o valor correto para os parâmetros ```usage``` e ```flags``` é importante para otimização e obter o comportamento correto.


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

Na realidade, os comandos ```glMapBuffer``` e ```glMapNamedBuffer``` retornam um ponteiro para a memória que "representa" o armazenamento de dados do buffer object vinculado ao target e isso significa que esta memória pode não ser a memória que será utilizada pela GPU. A GPU pode mover os dados de um buffer object quando está em uso.

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

Existem algumas observações interessantes sobre as opções do parâmetro ```access```.

- ```GL_MAP_INVALIDATE_RANGE_BIT``` (invalida parte dos dados do buffer)  
- ```GL_MAP_INVALIDATE_BUFFER_BIT``` (invalida dados do buffer inteiro)  

Indica a OpenGL que os dados do buffer podem ser descartados para que a aplicação possa escrever. Se estas flags não for especificada e o buffer object estiver em uso, a GPU poderá esperar para copiar/mover os dados gerando **stall** na pipeline.

Quando os dados são invalidados, a GPU cria um buffer novo se estiver em uso para que a aplicação possa utilizá-la imediatamente.

Estas flags só podem ser especificadas junto com ```GL_MAP_WRITE_BIT```.

> **Nota:** Cuidado ao atualizar o buffer object em diversas chamadas com ```glMapBuferRange```. Se em alguma chamada posterior especificar ```GL_MAP_INVALIDATE_BUFFER_BIT```, as partes anteriores serão descartadas.


A flag ```GL_MAP_UNSYNCHRONIZED_BIT``` não espera a GPU transferir os dados que estiverem em uso para a região de memória acessível para aplicação. A aplicação deve garantir que a GPU não está utilizando o buffer object. Existem duas maneiras de garantir isso: ```glFnish()``` e **sync objects**.

Esta flag é interessa onde a GPU está utilizando uma parte do buffer object e você quer atualizar outras partes sem ocasionar stall da pipeline.

A flag ```GL_MAP_FLUSH_EXPLICIT_BIT``` indica que a aplicação irá indicar quais partes do buffer object foram realmente alteradas. Sem esta flag, a GPU irá mover toda a parte mapeada mesmo se aplicação atualizou uma pequena parte deste buffer. Esta flag evita o tráfego desnecessário e possível perda de desempenho. Para a aplicação informar exatamente quais partes foram alteradas, existem os comandos ```glFlushMappedBufferRange``` (disponível a partir da versão 3.0) e ```glFlushMappedNamedBufferRange``` (disponível a partir da versão 4.5).

Estes comandos precisam ser chamados antes de realizar o "unmap" do buffer object. Assim que o comando é chamado, a GPU inicia o tratamento destes dados de forma paralela antes mesmo da aplicação realizar o "unmap".

??
Mapeando o buffer object de forma assincrona:

A função glFlushMappedNamedBufferRange é usada para garantir que uma parte de um buffer mapeado na memória seja enviada para a GPU de forma assíncrona e eficiente. Ela é especialmente útil quando você está usando buffer mapeado para escrita dinâmica, como ao atualizar vértices, uniformes ou dados de computação.

O comando glFlushMappedNamedBufferRange pode ser chamado para garantir que apenas a região modificada seja enviada para a GPU. Assim, a GPU pode acessar os dados antes mesmo da chamada de glUnmapNamedBuffer, reduzindo a latência.

Este comando ajuda a manter a execução paralela entre CPU e GPU, evitando stalls desnecessários.

Precisa do flag GL_MAP_FLUSH_EXPLICIT_BIT ao mapear o buffer, caso contrário, glFlushMappedNamedBufferRange não terá efeito.


# Descartando dados do buffer object

Existem dois comandos ```glInvalidadeBufferData``` (disponível a partir da versão 4.3) e ```glInvalidadeBufferSubData``` (disponível a partir da versão 4.3) para "informar" a GPU que os dados de um buffer object pode ser invalidados e serem liberados para outro uso reduzindo stall da pipeline e fragmentação de memória.

O comando glInvalidateBufferData serve para invalidar os dados armazenados em um buffer da GPU, informando que seu conteúdo anterior não é mais necessário. Isso pode melhorar a performance ao evitar cópias desnecessárias de dados antigos na memória da GPU.

Quando um buffer já contém dados antigos que não serão reutilizados, a GPU pode tentar preservar esse conteúdo ao alocar espaço para novos dados. Isso pode causar cópias desnecessárias e impacto no desempenho.

??
Isso pode:

Evitar cópias desnecessárias, reduzindo overhead na GPU.
Melhorar o desempenho ao permitir que a GPU reutilize a memória do buffer imediatamente.
Ser mais eficiente do que glBufferData(NULL), pois não força a GPU a desalocar e realocar a memória do buffer.

# Referências

- KESSENICH, J. et al. OpenGL Programming Guide: the official guide to learning OpenGL, versions 4.5. 9th ed. Boston: Pearson Education, 2017.  