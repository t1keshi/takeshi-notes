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

O maior benefício do uso de transformações lineares para resolver o nosso problema é a sua simplicidade na aplicação. Todas as operações envolve apenas multiplicação de matrizes. Apesar dessa simplicidade, estas transformações permitem:

- Posicionar, rotacionar e alterar o tamanho dos modelos em uma cena através da multiplicação de matrizes 
- Orientar a cena na frente do visualizador através da multiplicação de matrizes
- Aplicar efeitos de perspectiva através da multiplicação de matrizes
- Compor múltiplas multiplicações de matrizes em apenas uma única matriz
- Transformar as coordenadas para NDC através da divisão de perspectiva

Um modelo geométrico tridimensional é descrito através de um conjunto de vértices (x, y, z) definidos em um espaço conhecido como **local-space**.

Para posicionar modelos geométricos em uma cena devemos transformar seus vértices (x, y, z) de **local-space** para **world-space** (_model transform_) multiplicando as coordenadas dos vértices pelas matrizes transformação linear: translação, rotação e escala.

```
   vec4 vertexPosition = vec4(x, y, z, 1);
   mat4 transformMatrix;
   ...
   vPosition = transformMatrix * vertexPosition;
```

Para aplicar a transformação linear nas coordenadas (x, y, z), é necessário que as matrizes sejam 4x4 para encapsular a operação de translação através da multiplicação de matrizes. Consequentemente, para que seja possível a=esta multiplicação, é necessário incluir uma **nova coordenada (w)** para as coordenadas formando um vetor 1x4:

```
 [a b c d] . (x)    (ax + by + cz + dw)
 [e f g h] . (y) -> (ex + fy + gz + hw)
 [i j k l] . (z)    (ix + jy + kz + lw)
 [m n p q] . (w)    (mx + ny + pz + qw)
```

Uma coordenada com 4 componentes (x, y, z, w) é chamado de **coordenada homogênea**. Para transformar uma coordenada cartesiana (x, y, z) basta acrescentar o **componente w** com o valor 1. Além de permitir a multiplicação pela matriz 4x4, o componente w será essencial para a **divisão de perspectiva**. OpenGL utilizará este valor para transformar a coordenada homogênea de volta para coordenada cartesiana (NDC) através da divisão ```(x/w, y/w, z/w)```. O valor de w será transformado após a multiplicação pela matriz de projeção.

Para posicionar e orientar a cena em frente ao observador (camera) transformamos os vértices que estão em **world-space** para **eye-space** (_view transform_) multiplicando as coordenadas dos vértices pelas matrizes de transformação linear: translação, rotação e escala. É possível utilizar também uma matriz que encapsula todas as operações chamada de **LookAt**.

> **Nota**: As duas transformações acima transformam as coordenadas da mesma forma mas em direções opostas. Elas podem ser encapsuladas em uma única transformação chamada **model-view transform**. Entretanto, deixar estas trasnformações separadas permite aplicar cálculos de iluminação e sombreamento.

Para aplicar efeito de perspectiva e definir o tamanho do frustrum, transformamos os vértices que estão em **eye-space** para **clip-coordinates space** (_projection transform_) multiplicando os vértices que estão em eye-space pelas matrizes de projeção. Novamente, é nesta transformação que produzirá o novo valor para a coordenada w que permitirá a divisão de perspectiva.

```
   vPostion = projectionMatrix * viewMatrix * modelMatrix * vertexPosition;
```

Após estas transformações, as coordenadas dos vértices dos modelos geométricos estarão prontos para a etapa de rasterização de OpenGL.

Antes de iniciar a rasterização, OpenGL realiza implicitamente a **divisão de perspectiva**, **clipping** e **viewport/depth-range** transform que serão discutidos em mais detalhes em breve.


# Projeção Perspectiva

**Projection transform** tem como objetivo definir o **volume de visualização** - um cone retangular conhecido como **frustum** - onde os objetos que estiverem dentro dele poderão ser exibidos na imagem final e, obviamente, os objetos que estiverem fora, serão descartados (processo também conhecido como **culling**). Dependendo do tipo de projeção, os objetos que estiverem mais próximos do visualizador (camera) serão maiores do que objetos que estiverem mais distantes, criando o efeito de perspectiva.

Esta etapa também irá produzir o valor de W (a quarta coordenada homogênea) necessária para que OpenGL possa transformar (_implicitamente_) as coordenadas homogêneas de volta para as coordenadas cartesianas em NDC chamada de **divisão de perspectiva**.

O frustum possui dois planos adicionais (**near plane** e **far plane**) que intersectam o frustum para eliminar objetos que estão muito próximo da ponta do cone (mais especificamente na frente de near plane) e que estão muito longe (mais especificamente atrás de far plane). Isto resolve vários problemas onde objetos ficam infinitamente grandes, precisão de profundidade (depth precision) e também em questão de desempenho.

A projeção ortográfica é um tipo de projeção onde o tamanho dos objetos não é alterado de acordo com a distância do observador. Em geral, é possível conseguir este efeito apenas ignorando um dos eixos x, y ou z utilizando transformações lineares. Entretanto, ainda precisamos do valor de W e do frustum para que OpenGL consiga realizar a divisão de perspectiva e clipping.


# Referências

- KESSENICH, J. et al. OpenGL Programming Guide: the official guide to learning OpenGL, versions 4.5. 9th ed. Boston: Pearson Education, 2017.  
- WOLFF, D. OpenGL 4 Shading Language Cookbook. 3rd ed. Birmingham: Packt Publishing, 2018.  
- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.  
- Scratchapixel. The Perspective and Orthographic Projection Matrix. Disponível em: [link](https://www.scratchapixel.com/lessons/3d-basic-rendering/perspective-and-orthographic-projection-matrix/projection-matrix-introduction.html).  
