[Home](_opengl.md)  

# Método de Visualização 3D

O objetivo principal do **método de visualização** é projetar modelos geométricos de um espaço tridimensional para uma área retangular bidimensional (_screen coordinates_) da tela.

O algoritmo de **rasterização** de OpenGL é responsável por gerar os pixels correspondentes aos modelos geométricos que serão exibidos na tela. Entretanto, este algoritmo precisa que todos os pontos (x, y) estejam no sistema de coordenadas bidimensional chamado de **NDC (Normalized Device Coordinates)**, onde o intervalo de valores para os eixos é de [-1, 1].

> **Nota:** Na verdade, existem duas conveções para definir o intervalo de valores para o sistema de coordenadas NDC. OpenGL e Direct3D utilizam o intervalo de [-1, 1] e RenderMan utiliza o intervalo de [0, 1].

Quando estamos trabalhando com modelos geométricos em uma cena, precisamos de uma maior flexibilidade para especificar os vértices no espaço. Isto é, precisamos de um sistema de coordenadas que abranja um intervalo de valores diferentes de [-1, 1].

Portanto, antes da etapa de rasterização, precisamos de um meio para transformar os pontos que estão no sistema de coordenadas do usuário para o sistema de coordenadas NDC.

A solução para este problema é a aplicação de **transformações lineares** através de multiplicação de matrizes.

Além de transformar as coordenadas de um sistema de coordenadas para outro, as transformações lineares permitem:

- organizar os modelos geométricos em um espaço tridimensional (translação, rotação e escala)
- visualizar a cena a partir de uma determinada localização, direção e orientação
- aplicar efeitos de perspectiva


# Transformações Lineares

O maior benefício do uso de transformações lineares para resolver o nosso problema é a sua simplicidade na aplicação. Todas as operações envolve apenas multiplicação de matrizes 4x4. Apesar da simplicidade, estas transformações permitem:

- Posicionar, rotacionar e alterar o tamanho dos modelos em uma cena através da multiplicação de matrizes 
- Orientar a cena na frente do visualizador através da multiplicação de matrizes
- Aplicar efeitos de perspectivas através da multiplicação de matrizes
- Encapsular todas as operações de matrizes em apenas uma única matriz
- Transformar as coordenadas para NDC através da divisão de perspectiva

Um modelo geométrico tridimensional é descrito através de um conjunto de vértices (x, y, z) definidos em um espaço conhecido como **local-space**.

Para posicionar modelos geométricos em uma cena devemos transformar seus vértices (x, y, z) de **local-space** para **world-space** (_model transform_) multiplicando as coordenadas dos vértices pelas matrizes transformação linear: translação, rotação e escala.

Para posicionar e orientar a cena em frente ao visualizador (camera) transformamos os vértices que estão em **world-space** para **eye-space** (_view transform_) também multiplicando as coordenadas dos vértices pelas matrizes de transformação linear. É possível utilizar também uma matriz que encapsula todas as operações chamada de **LookAt**.

> **Nota**: As duas transformações acima transformam as coordenadas da mesma forma mas em direções opostas. Elas podem ser encapsuladas em uma única transformação chamada **model-view transform**. Entretanto, deixar estas trasnformações separadas permitem aplicar algoritimos de iluminação e sombreamento.

Para aplicar efeito de perspectiva e definir o tamanho do frustrum, transformamos os vértices que estão em **eye-space** para **clip-coordinates space** (_projection transform_) multiplicando os vértices que estão em eye-space pelas matrizes de projeção.

```
   vPostion = projectionMatrix * viewMatrix * modelMatrix * vertexPosition;
```

Após estas transformações, as coordenadas dos vértices dos modelos geométricos estarão prontos para a etapa de rasterização de OpenGL.

Antes de iniciar a rasterização, OpenGL realiza implicitamente a **divisão de perspectiva**, **clipping** e **viewport/depth-range** transform que serão discutidos em mais detalhes em breve.


# Projeção Perspectiva


# Referências

- KESSENICH, J. et al. OpenGL Programming Guide: the official guide to learning OpenGL, versions 4.5. 9th ed. Boston: Pearson Education, 2017.  
- WOLFF, D. OpenGL 4 Shading Language Cookbook. 3rd ed. Birmingham: Packt Publishing, 2018.  
- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.  
- Scratchapixel. The Perspective and Orthographic Projection Matrix. Disponível em: [link](https://www.scratchapixel.com/lessons/3d-basic-rendering/perspective-and-orthographic-projection-matrix/projection-matrix-introduction.html).  
