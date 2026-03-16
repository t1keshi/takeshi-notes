Previous: [OpenGL](_opengl.md)


# Shader Plumbing

**Shader Plumbing** é um termo utilizado em OpenGL para o processo de conexão entre os **dados de vértice** armazenados em **vertex buffer objects (vbo)** e as **variáveis de entrada** declaradas em **Vertex Shader** - o primeiro estágio da pipeline de renderização.

Um vértice pode conter diversas informações como posição, cor, coordenadas de textura, vetor normal, etc e essas informações são conhecidas como **atributos de vértice**. De fato, podemos atribuir qualquer tipo de informação à um vértice.

Os atributos de vértice são organizados em forma de array (_vertex array_) na memória de OpenGL - cada atributo tem o seu array. Assim, cada vertex shader recebe um elemento destes arrays formando os dados do vértice.

Exemplo de um vértice com seus atributos:

```
	struct vertex {
		vec3 position;	// vertex attribute 1
		vec3 color;		// vertex attribute 2
		vec2 texture;	// vertex attribute 3
		vec3 normal;	// vertex attribute 4
	};
```

Exemplo de declaração de variáveis de entrada em um Vertex Shader que serão inicializados com os atributos de vértice acima:

``` 
	// variáveis de entrada em Vertex Shader
	layout(location=1) in vec3 position;	// vertex attribute 1
	layout(location=2) in vec3 color;		// vertex attribute 2
	layout(location=3) in vec3 texture;		// vertex attribute 3
	layout(location=4) in vec3 normal;		// vertex attribute 4
```

> **Nota:** In earlier versions of OpenGL (prior to 3.0), each piece of vertex information had a specific channel in the pipeline. It was provided to the shaders using functions such as glVertex, glTexCoord, and glNormal (or within client vertex arrays using glVertexPointer, glTexCoordPointer, or glNormalPointer). The shader would then access these values via built-in variables such as gl_Vertex and gl_Normal. This functionality was deprecated in OpenGL 3.0 and later removed. Instead, vertex information must now be provided using generic vertex attributes, usually in conjunction with (vertex) buffer objects. The programmer is now free to define an arbitrary set of pervertex attributes to provide as input to the vertex shader.

O objeto OpenGL responsável por essa conexão é o **vertex array object ou VAO**.

Uma outra maneira de uma aplicação passar informações para os shaders (além do Vertex Shader) é através de **variáveis uniforme**.


# Entrada de dados em Shaders

As variáveis de entrada em shaders são declaradas com o qualificador ```in```:

```
	layout (location=0) in vec3 vertexPosition;
	layout (location=1) in vec3 vertexColor;
```

No caso de um **Vertex Shader**, as variáveis de entrada são inicializadas com os atributos de vértice armazenados em **VBO**. Em outros tipos de shaders, estas variáveis são inicializadas com as variáveis de saída  ```out``` do estágio anterior.


# Vertex Array Object (VAO)

**Vertex Array Object (VAO)** é o objeto responsável por especificar o formado de dados do atributo de vértice e, de forma implícita, o vbo que contém o atributo de vértice para que quando for inicializado a pipeline de renderização, as variáveis de entrada de Vertex Shader possam ser inicializadas corretamente.

```
	GLuint vao;
	glGenVertexArrays(1, &vao);
	glBindVertexArray(vao);
```

# Referências

- KESSENICH, J. et al. OpenGL Programming Guide: the official guide to learning OpenGL, versions 4.5. 9th ed. Boston: Pearson Education, 2017.
- WOLFF, D. OpenGL 4 Shading Language Cookbook. 3rd ed. Birmingham: Packt Publishing, 2018.
- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.
