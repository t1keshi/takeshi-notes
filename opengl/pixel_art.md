Previous: [OpenGL](_opengl.md)  

# Pixel Art

Se a imagem a ser renderizada for pixel art, o ideal é que a textura contenha a mesma resolução e razão de aspecto da superfície a ser texturizada.
Entretanto, na maioria das vezes, uma textura pode ser menor para economizar memória.

A ideia é o seguinte:

Se a janela de visualização (matriz de projeção ortográfica 2D) for 320x180 e a janela de aplicação (viewport) for 1280x720, teremos:

```
    1 unidade = 4 pixels (1280 / 320 e 720 / 180)
```

Isso significa que o tamanho do sprite original se tornará 4 vezes maior:

```
    Antes: 64x64
    Depois: 256x256
```

Além disso, é necessário configurar o filtro da textura em OpenGL da seguinte forma:

```
	glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_NEAREST);
	glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_NEAREST);
```


# References  

- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.  
- Heartbest. How to Make an Action RPG. Available in youtube: https://www.youtube.com/watch?v=l_yTe50tHVg&list=PL9FzW-m48fn3H1URoqV6QorDpszCBIwt7.  
