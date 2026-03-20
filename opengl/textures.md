Previous: [OpenGL](_opengl.md)


# Textures

**Mapeamento de texturas** é uma técnica que permite aplicar uma imagem de textura em uma superfície de um modelo rasterizado. Ele é muito importante para adicionar realismo em cenas renderizadas.

**Textura** é uma image 


This technique allows you to look up values, like colors, from a shader in a special type of table. While access to texture maps is a ailable in all of OpenGL’s shading stages, we’ll first discuss it in the context of processing fragments, because that’s where it’s used most often.

Often, a texture map (or just "texture" for short) is an image captured by a camera or painted by an artist, but there’s no requirement that be the case — it’s possible that the image is procedurally generated (see Chapter 8, “Procedural Texturing”) or e en rendered by OpenGL targeting a texture instead of the display device.

Textures of this nature would be two dimensional, but OpenGL supports many other types of textures as well: one-, and three-dimensional textures, cube-map textures, and buffer textures. Array textures are also supported, which are treated as a set of slices of similar dimension and format wrapped up in a single texture object.

Textures are composed of texels, which will often contain color values. However, there’s a lot of utility in merely considering a texture as a table of alues that you can query in a shader and use for any purpose you desire.

??
Existem componentes de hardware gráfico específicos para ajudar no mapeamento de textura (sampling de textura, aplicação de filtros, LOD, mipmaps, etc). **Texture Units** é a interface para acessar esses componentes de hardware.

Para verificar a quantidade disponível de texture units em seu hardware verifique ```GL_MAX_VERTEX_TEXTURE_IMAGE_UNITS```. Por exemplo, se estiver disponível 16 texture units, o seu shader será capaz de utilizar 16 texture objects simultaneamente.


# Texture Objects

Em OpenGL, **texture object** é utilizado para armazenar uma imagem de textura.

```
    GLuint texture;
    glGenTextures(1, &texture);
    glBindTexture(GL_TEXTURE_2D, texture);

    glCreateTextures(1, &tex); // OpenGL 4.5+

    glTexParameter
```

Nas versões de OpenGL anteriores a 4.5, quando um **texture object** é criado, é necessário vinculá-lo a um **texture target** utilizando ```glBindTexture```. Com a introdução do conceito **Direct State Access (DSA)** na versão 4.5, foi criado um novo comando ```glCreateTextures``` que permite criar um texture object e manipulá-lo como se já estivesse vinculado à um target não especificado sem afetar o estado do contexto OpenGL.

```
    glTexImage2D
```


# Coordenadas de textura como vertex attribute

As **coordenadas de textura** são as coordenadas do eixo S (horizontal) e T (vertical) de uma imagem de textura. Estas coordenadas são utilizadas para mapear o vértice em alguma localização desta textura. Portanto, para cada vértice, associamos uma coordenada de textura. Em geral, fazemos isso declarando estas coordenadas como atributo de vértice.

> **Nota:** Em OpenGL, os nomes dos eixos de uma coordenada de textura é S e T. Mas fora de OpenGL, é muito comum utilizar também os nomes U e V.

```
    // vertex shader
    in vec2 textureCoordinate;

    void main() {
        ...
	    fragTexCoord = textureCoordinate;
    }
```

Quando passamos coordenadas de textura de vertex shader para fragment shader, elas são interpoladas pelo rasterizador da mesma forma que as posições do vértice. Com isso, conseguimos obter o pixel da textura (**texel**) para o determinado fragmento da primitiva.

```
    // fragment shader
    in vec2 fragTexCoord;
    uniform sampler2D tex;

    void main()
    {
        fragmentColor = texture(tex, fragTexCoord); // obtendo o texel da textura
    }
```

O intervalo de valores para as coordenadas de textura nos dois eixos são [0, 1] com a origem (0, 0) no canto inferior esquerdo.

> **Nota:** As imagens armazenadas em arquivos como PNG, JPEG, etc possuem a origem (0, 0) no canto superior esquerdo. Ao ler estas imagens de arquivos para memória, é necessário inverter verticalmente.

Exemplo de como mapear os vértices de um quad em uma textura.

```
```

Em modelos mais complexos que contém curvas ou muitos triângulos, as coordenadas de textuas precisam ser geradas matematicamente ou com algum algoritmo especializado. Alguns softares como Blender3D oferecem um recurso chamado "UV Mapping".


# Unfirom Sampler variable

Existe uma variável uniforme especial em shaders chamada **sampler** que utiliza texture unit para extrair texel ou "sample" do objeto de textura carregado.

```
    // fragment shader
    layout(binding=0) uniform sampler2D myTexture;
```

O qualificador ```layout binding``` especifica qual texture unit a variável sampler deve utilizar para extrair o texel.

Um texture object é associado ao texture unit pela aplicação da seguinte maneira:

```
    glActiveTexture(GL_TEXTURE0); // ativa o texture unit desejado
    glBindTexture(GL_TEXTURE_2D, tex);
```

Para extrair o texel em fragment shader, basta passar as coordenadas de texturas interpolada para o sampler:

```
    color = texture(myTexture, textureCoordinates);
```


# Mipmapping

O mapeamento de texturas pode provocar artefatos indesejáveis quando a resolução da textura ou aspecto de razão não coincide com a superfície do modelo a ser renderizada. Isto pode ocorrer por dois motivos:

1. A resolução da textura é menor que a superfície do modelo provocando blurry e distorção da imagem

Neste caso, utilizar uma textura com uma resolução maior resolve o problema.

2. a resolução da textura é muito maior do que a superfície do modelo provocando aliasing ou efeitos "shimmering" em objetos que se movem

Aliasing é causa por erros de _sampling_. Este tipo de erro é frequentemente associado a processamento de sinais onde a amostra (_sample_) tem menos sinais que o original.

Este problema podem ser resolvido com a técnica chamada **mipmapping**, onde diferentes resoluções da textura são criadas a partir do original e a mais apropriadada é escolhida durante a renderização.

Em OpenGL, existem diversos parâmetros de mipmapping:

Para **minification** onde a superfície é menor que a textura, basta utilizar o comando ```glTexParameteri``` com o parâmetro ```GL_TEXTURE_MIN_FILTER```:

```
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_NEAREST_MIPMAP_NEAREST);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR_MIPMAP_NEAREST);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_NEAREST_MIPMAP_LINEAR);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR_MIPMAP_LINEAR);
```

- ```GL_NEAREST_MIPMAP_NEAREST``` - escolhe o mipmap mais próximo do tamanho da superfície e obtém o texel mais próximo  
- ```GL_LINEAR_MIPMAP_NEAREST``` - escolhe o mipmap mais próximo do tamanho da superfície e interpola os 4 texels mais próximos (linear filtering)  
- ```GL_NEAREST_MIPMAP_LINEAR``` - escolhe os dois mipmaps mais próximos e interpola o texel dos dois mipmaps (bilinear filtering)  
- ```GL_LINEAR_MIPMAP_LINEAR``` - escolhe os dois mipmaps mais próximos e interpola os 4 texels de cada mipmap e depois interpola os dois resultados (trilinear filtering)  

Trilinear filtering é o mais preferível mas tem o custo de desempenho maior entre eles.

Mipmaps podem ser criados pelo próprio usuário ou pelo OpenGL:

```
    glBindTexture(GL_TEXTURE_2D, textureID);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR_MIPMAP_LINEAR);
    glGenerateMipmap(GL_TEXTURE_2D);
```

Para criar manualmente os mipmaps, basta chamar repetidamente o comando ```glTexImage2D``` com diferentes valores para ```level```.

> **Nota:** É possível utilizar ```GL_NEAREST``` ou ```GL_LINEAR``` para desativar o mipmapping.


# Wrapping and Tiling

Além de mipmapping, é possível especificar comportamentos para coordenadas de texturas com valores diferentes de [0, 1] utilizando os parâmetros ```GL_TEXTURE_WRAP_S``` e ```GL_TEXTURE_WRAP_T```.

```
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_CLAMP_TO_EDGE);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_CLAMP_TO_EDGE);
```

- ```GL_REPEAT```  
- ```GL_MIRRORED_REPEAT```  
- ```GL_CLAMP_TO_EDGE```  
- ```GL_CLAMP_TO_BORDER```  

Para que ```GL_CLAMP_TO_BORDER``` funcione, é necessário especificar também a cor da borda limite:

```
    float redColor[4] = { 1.0f, 0.0f, 0.0f, 1.0f };
    glTexParameterfv(GL_TEXTURE_2D, GL_TEXTURE_BORDER_COLOR, redColor);
```


# Anisotropic filtering (AF)

Para verificar se o filtro **anistropic** está disponível no hardware gráfico:

```
    GLint numExtensions;
    glGetIntegerv(GL_NUM_EXTENSIONS, &numExtensions);

    for (GLint i = 0; i < numExtensions; i++) {
        extension = glGetStringi(GL_EXTENSIONS, static_cast<GLuint>(i));

        if(extension == "GL_EXT_texture_filter_anisotropic") {
            // this hardware has anisotropic filtering
        }
    }

    // setting anisotropic filtering
    GLfloat	anisoSetting = 0.0f;
    glGetFloatv(GL_MAX_TEXTURE_MAX_ANISOTROPY_EXT, &anisoSetting);
    glTexParameterf(GL_TEXTURE_2D, GL_TEXTURE_MAX_ANISOTROPY_EXT, anisoSetting);
```

# Referências

- KESSENICH, J. et al. OpenGL Programming Guide: the official guide to learning OpenGL, versions 4.5. 9th ed. Boston: Pearson Education, 2017.  
- WOLFF, D. OpenGL 4 Shading Language Cookbook. 3rd ed. Birmingham: Packt Publishing, 2018.  
- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.  
