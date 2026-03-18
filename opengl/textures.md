Previous: [OpenGL](_opengl.md)


# Textures

**Mapeamento de texturas** é uma técnica que permite aplicar uma imagem em uma superfície de um modelo rasterizado. Ele é muito importante para adicionar realismo em cenas renderizadas.

Existem componentes de hardware gráfico específicos para ajudar no mapeamento de textura (sampling de textura, aplicação de filtros, LOD, mipmaps, etc). **Texture Units** é a interface para acessar esse componente de hardware.

Para verificar a quantidade disponível de texture units em seu hardware verifique ```GL_MAX_VERTEX_TEXTURE_IMAGE_UNITS```.


# Texture Objects

Em OpenGL, **texture object** é utilizado para armazenar uma imagem de textura.

```

    GLuint texture;
    glGenTextures(1, &texture);
    glBindTexture(GL_TEXTURE_2D, texture);

    glTexParameter
```


# Coordenadas de textura como vertex attribute

As **coordenadas de textura** são as coordenadas do eixo S e T de uma imagem de textura. Estas coordenadas são utilizadas para mapear o vértice em alguma localização desta textura. Portanto, para cada vértice, associamos uma coordenada de textura. Em geral, fazemos isso declarando estas coordenadas como atributo de vértice.

> **Nota:** Em OpenGL, os nomes dos eixos de uma coordenada de textura é S e T. Mas fora de OpenGL, é muito comum utilizar também os nomes U e V.


```
    // vertex shader
    in vec2 textureCoordinate;
    out vec2 fragTexCoord;

    void main() {
        ...
	    fragTexCoord = textureCoordinate;
    }
```

Quando passamos estas coordenadas de vertex shader para fragment shader, elas são interpoladas pelo rasterizador da mesma forma que as posições do vértice. Com isso, conseguimos obter o pixel da textura (**texel**) para o determinado fragmento da primitiva que está sendo renderizada.

```
    // fragment shader
    in vec2 fragTexCoord;
    out vec4 fragmentColor;

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
    uniform sampler2D myTexture;
```

# Referências

- KESSENICH, J. et al. OpenGL Programming Guide: the official guide to learning OpenGL, versions 4.5. 9th ed. Boston: Pearson Education, 2017.  
- WOLFF, D. OpenGL 4 Shading Language Cookbook. 3rd ed. Birmingham: Packt Publishing, 2018.  
- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.  
