Previous: [OpenGL](_opengl.md)  

# Pixel Art

Se a imagem a ser renderizada for pixel art, o ideal é que a textura contenha a mesma resolução e razão de aspecto da superfície a ser texturizada.
Entretanto, na maioria das vezes, a textura é menor para economizar memória.

- Não gerar minimaps  
- Utilizar a opção de filtro GL_NEAREST para GL_TEXTURE_MIN_FILTER e GL_TEXTURE_MAG_FILTER  

```
	glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_NEAREST);
	glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_NEAREST);
```

# References  

- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.  
- Heartbest. How to Make an Action RPG. Available in youtube: https://www.youtube.com/watch?v=l_yTe50tHVg&list=PL9FzW-m48fn3H1URoqV6QorDpszCBIwt7.  
