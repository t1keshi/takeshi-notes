[Home](_opengl.md)  

# Método de Visualização 3D

O objetivo principal do **método de visualização** é projetar modelos geométricos em um espaço tridimensional para uma determinada área retangular bidimensional (_screen coordinates_) da tela.

O algoritmo de **rasterização** de OpenGL é responsável por gerar os pixels correspondentes aos modelos geométricos que serão exibidos na tela. Entretanto, este algoritmo precisa que todos os pontos (x, y) estejam no sistema de coordenadas bidimensional chamado de **NDC (Normalized Device Coordinates)**, onde o intervalo de valores para os eixos é de [-1, 1].

> **Nota:** Existem duas conveções para definir o intervalo de valores para o sistema de coordenadas NDC. OpenGL e Direct3D utilizam o intervalo de [-1, 1] e RenderMan utiliza o intervalo de [0, 1].

Quando estamos trabalhando com modelos geométricos em uma cena, precisamos de uma maior flexibilidade para especificar os vértices no espaço. Isto é, precisamos de um sistema de coordenadas que abranja um intervalo de valores diferentes de [-1, 1].

Portanto, antes da etapa de rasterização, precisamos de um meio para transformar os pontos que estão no sistema de coordenadas do usuário para o sistema de coordenadas NDC.

A solução para este problema é a aplicação de **transformações lineares** através de multiplicação de matrizes.

Além de transformar as coordenadas de um sistema de coordenadas para outro, as transformações lineares permitem:

- organização dos modelos geométricos em um espaço tridimensional (translação, rotação e escala)  
- a visulização da cena a partir de uma determinada localização, direção e orientação  
- aplicação dos efeitos de perspectiva  

# Transformações Lineares

# Referências

- KESSENICH, J. et al. OpenGL Programming Guide: the official guide to learning OpenGL, versions 4.5. 9th ed. Boston: Pearson Education, 2017.  
- WOLFF, D. OpenGL 4 Shading Language Cookbook. 3rd ed. Birmingham: Packt Publishing, 2018.  
- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.  
- Scratchapixel. The Perspective and Orthographic Projection Matrix. Disponível em: [link](https://www.scratchapixel.com/lessons/3d-basic-rendering/perspective-and-orthographic-projection-matrix/projection-matrix-introduction.html).  
