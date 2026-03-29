[Home](_opengl.md)  

# Método de Visualização 3D

O objetivo principal do **método de visualização** é projetar objetos tridimensionais em um plano bidimensional.

O algoritmo de **rasterização** de OpenGL é responsável por gerar os pixels correspondentes aos objetos que serão exibidos na tela. Entretanto, este algoritmo necessita que todos os vértices (x, y, z) dos objetos estejam no sistema de coordenadas bidimensional chamado de **Normalized Device Coordinates (NDC)**, onde o intervalo de valores dos eixos é de [-1, 1].

> **Nota:** Existem duas conveções para definir o intervalo de valores para o sistema de coordenadas NDC. Por exemplo, OpenGL e Direct3D utilizam o intervalo de [-1, 1] e RenderMan utiliza o intervalo de [0, 1].

Quando estamos trabalhando com modelos geométricos em uma cena, precisamos de uma maior flexibilidade para especificar os vértices no espaço. Isto é, precisamos de um sistema de coordenadas que abranja um intervalo de valores diferentes de [-1, 1].

Portanto, antes da etapa de rasterização, precisamos de um meio para transformar os vértices que estão no sistema de coordenadas do usuário para o sistema de coordenadas NDC.

A solução para este problema é a aplicação de **transformações lineares** e da **transformação projetiva** através de multiplicação de matrizes e da **divisão de perspectiva**.


# Transformações Lineares e Transformação Projetiva

O maior benefício do uso de transformações lineares e transformação projetiva é a sua simplicidade na aplicação. Estas transformações envolvem apenas multiplicação de matrizes. Apesar de sua simplicidade, estas transformações permitem:

- posicionar, rotacionar e alterar o tamanho dos objetos em uma cena (**model transform**)  
- posicionar o observador (_viewpoint_) e orientar a cena na frente do observador (**view transform**)  
- aplicar efeitos de perspectiva (**projection transform**)  
- compor diversas matrizes em apenas uma única matriz (propriedade associativa das matrizes)  
- organizar as transformações em forma de hierarquia para permitir animação (_skeletal animation_)  
- permitir operações de **culling** e **clipping**  
- permitir a **divisão de perspectiva** e transformar as coordenadas para NDC  

Um modelo geométrico tridimensional é descrito através de um conjunto de vértices definidos em um espaço conhecido como **local-space**, isto é, sem aplicação de nenhuma transformação.

Para posicionar os modelos geométricos em uma cena devemos transformar (_model transform_) seus vértices de **local-space** para **world-space** multiplicando os vértices pelas matrizes de transformação linear: translação, rotação e escala.

```
   vec4 vertexPosition = vec4(x, y, z, 1);
   uniform mat4 modelMatrix;

   vPosition = modelMatrix * vertexPosition;
```

Quando pensamos em transformação linear, devemos pensar nas coordenadas de um vértice como um vetor de quatro elementos. Dessa forma, conseguimos multiplicá-lo por uma matriz 4x4. A matriz precisa ser 4x4 para poder encapsular a operação de translação através da multiplicação de matrizes. Para que um vértice (x, y, z) possua 4 elementos basta incluir um novo componente **w** com valor 1, ficando (x, y, z, w).

```
    [a b c d] . (x)    (ax + by + cz + dw)
    [e f g h] . (y) -> (ex + fy + gz + hw)
    [i j k l] . (z)    (ix + jy + kz + lw)
    [m n p q] . (w)    (mx + ny + pz + qw)
```

Um ponto com 4 coordenadas (x, y, z, w) é chamado de **coordenada homogênea**. Nas operações de translação, escala e rotação, o valor de w do vértice deve ser sempre 1. Este componente será importante apenas quando OpenGL for transformar a coordenada homogênea de volta para a coordenada cartesiana (NDC) através da **divisão de perspectiva**: ```(x/w, y/w, z/w)```. Como verá em breve, o valor de w (diferente de 1) é produzido pela multiplicação de matriz projetiva.

Para posicionar o observador e orientar a cena na sua frente, transformamos os vértices que estão em **world-space** para **eye-space** ou **camera-space** (_view transform_) multiplicando os vértices pelas matrizes de transformação linear: translação, rotação e escala. É possível utilizar também uma matriz que encapsula estas operações chamada de **LookAt**.

```
   vec4 vertexPosition = vec4(x, y, z, 1);
   uniform mat4 modelMatrix;
   uniform mat4 viewMatrix;

   vPosition = viewMatrix * modelMatrix * vertexPosition;
```

> **Nota**: As duas transformações acima (_view transform_ e _model transform_) transformam os vértices da mesma forma mas em direções opostas. Elas podem ser encapsuladas em uma única transformação chamada **model-view transform**. Entretanto, deixar estas transformações separadas permite aplicar outros tipos de cálculos como iluminação e sombreamento.

Para aplicar efeito de perspectiva, transformamos os vértices que estão em **eye-space** para **clip-space** (_projection transform_) multiplicando os vértices pela **matriz de projeção**. É nesta transformação que produzirá o novo valor (diferente de 1) para a coordenada w e que permitirá a divisão de perspectiva.

```
   vec4 vertexPosition = vec4(x, y, z, 1);
   uniform mat4 modelMatrix;
   uniform mat4 viewMatrix;
   uniform mat4 projectionTransform;

   vPostion = projectionMatrix * viewMatrix * modelMatrix * vertexPosition;
```

Estas transformações devem ser realizadas pela aplicação, normalmente nos shaders para aproveitar o desempenho da GPU e permitir outros tipos de processamento. Após estas transformações, as coordenadas dos vértices dos modelos geométricos estarão prontos para a etapa de rasterização de OpenGL.

> **Nota:** Antes de iniciar a rasterização, OpenGL realiza implicitamente a **divisão de perspectiva** para transformar as coordenadas de clip-space para NDC. Com os vértices transformados, OpenGL realiza o **clipping** e **viewport/depth-range transform** que serão discutidos em mais detalhes em breve.


# Regra da mão direita vs regra da mão esquerda

Na Computação Gráfica, existem duas formas de orientar os eixos x, y e z: **regra da mão direita** e **regra da mão esquerda**:

Na regra da mão direita, o eixo x aponta para a direita, o eixo y aponta para cima e o eixo z aponta para o observador.

Na regra da mão esquerda, o eixo x aponta para a direita, o eixo y aponta para cima e o eixo z aponta para a mesma direção onde observador está olhando.

Escolher a orientação correta influencia nos cálculos de transformações lineares. OpenGL utiliza a regra da mão direita e DirectX utiliza a regra da mão esquerda.


# Projeção Perspectiva

A **transformação projetiva** é responsável por transformar os pontos tridimensionais que estão em _eye-space_ para _homogeneous clip-space_ através da multipicação do vértice pela **matriz de projeção**. OpenGL utilizará estes pontos transformados para realizar a **divisão de perspectiva**, **clipping** e **rasterização**. 

Conceitualmente, a **transformação projetiva** cria um volume de visualização - um cone retangular dividido em seis planos conhecido como **frustum** - onde os objetos que estiverem dentro dele são exibidos na imagem final e os objetos que estiverem fora serão descartados - processo também conhecido como **culling**. A criação dos planos de frustum é importante também para o processo de **clipping** que será realizado depois.

[imagem do frustum]

O plano **near plane** é o plano de projeção bidimensional onde os pontos 3D serão projetados. Este plano intersercta o frustum e é paralelo aos eixos x e y do observador. Em OpenGL, o observador (_viewpoint_) está sempre na origem (0, 0, 0) e "olhando" para a direção negativa do eixo z (regra da mão direita). Dessa forma, conseguimos definir o tamanho do frustum e a distância entre o observador através das seguintes variáveis:

- **left** (valor do lado esquerdo de near plane no eixo x)
- **right** (valor do lado direito de near plane no eixo x)  
- **top** (valor do lado de cima de near plane no eixo y)  
- **bottom** (valor do lado de baixo de near plane no eixo y)
- **near** (distância do observador até o plano de projeção no eixo z )
- **far** (distância do observador até o far plane no eixo z)  

> **Nota:** Os planos **near plane** e **far plane** eliminam objetos que estão muito próximo da ponta do cone (mais especificamente na frente de near plane) e que estão muito longe (mais especificamente atrás de far plane). Isto resolve vários problemas onde objetos ficam infinitamente grandes, precisão de profundidade (depth precision) e também questões de desempenho.

> **Nota:** Os valores de x e y dos parâmetros ```left```, ```right```, ```bottom``` e ```top``` podem ser calculados através do ângulo **field of view** e **razão de aspecto**.

Dependendo do tipo de projeção, os objetos que estiverem mais próximos do observador serão maiores do que objetos que estiverem mais distantes, criando o **efeito de perspectiva**. Este efeito é obtido através da **divisão de perspectiva**, onde as coordenadas ```x```, ```y``` e ```z``` são divididos pela coordenada ```w```.

Outra operação importante é o remapeamento dos valores das coordenadas x, y e z para o intervalo de valores [-1, 1] de NDC.

Como é o OpenGL que faz essa divisão de perspectiva, a matriz de projeção deve gerar o valor de ```w``` para que, após a divisão, crie este efeito de perspectiva e transforme as coordenadas para NDC. Todas as equações serão discutidos no tópico _"Construindo Matriz de Projeção"_.

A **projeção ortográfica** é um tipo de projeção onde o tamanho dos objetos não é alterado de acordo com a distância do observador. Em geral, é possível conseguir este efeito apenas ignorando um dos eixos x, y ou z utilizando transformações lineares. Entretanto, ainda precisamos do valor de w e do frustum para que OpenGL consiga realizar a divisão de perspectiva e clipping.


# OpenGL Clipping

Se apenas uma parte do objeto estiver fora do volume de visulização, OpenGL realiza o processo de **clipping**, isto é, geração de uma nova geometria a partir do cálculo de intersecção do objeto com os planos do frustum.

Quando os vértices são transformados para _clip-space_ onde o intervalo de valores é [-1, 1], facilita a operação de clipping.

"The remapping of P's x- and y-coordinates, as well as its z-coordinate to the ranges [-1,1] and [0,1] (or [-1,1]), signifies that the projection matrix transformation alters the viewing frustum's volume into a 2x2x1 (or 2x2x2) dimensional cube, commonly known as the unit cube or canonical view volume. This transformation can be viewed as normalizing the viewing frustum. This operation simplifies further operations on points by converting the viewing frustum, defined by the near and far clipping planes and screen dimensions, into a much more manageable geometric shape."


# Construindo as matrizes de transformações lineares

Todas as matrizes abaixo estão em colum-major order que é o padrão em OpenGL. Isto significa que quando multiplicamos uma matriz pelo vetor, o vetor deve estar sempre a direita.

Translação

```
  [ 1.0 ][ 0.0 ][ 0.0 ][ 0.0 ]
  [ 0.0 ][ 1.0 ][ 0.0 ][ 0.0 ]
  [ 0.0 ][ 0.0 ][ 1.0 ][ 0.0 ]
  [ Tx  ][ Ty  ][ Tz  ][ 1.0 ]
```

Escala

```
  [ Sx  ][ 0.0 ][ 0.0 ][ 0.0 ]
  [ 0.0 ][ Sy  ][ 0.0 ][ 0.0 ]
  [ 0.0 ][ 0.0 ][ Sz  ][ 0.0 ]
  [ 0.0 ][ 0.0 ][ 0.0 ][ 1.0 ]
```

Rotação

Rotation counterclock around the z axis:

```
  [ cosA ][ -sinA ][ 0 ][ 0 ] (x)    (cosA . x - sinA . y) = (x)
  [ sinA ][  cosA ][ 0 ][ 0 ] (y) -> (sinA . x + cosA . y) = (y)
  [   0  ][   0   ][ 1 ][ 0 ] (z)    (1 . z)               = (z)
  [   0  ][   0   ][ 0 ][ 1 ] (w)    (1 . w)               = (w)
```

Rotation counterclock around the x axis:

```
  [ 1 ][  0   ][   0   ][ 0 ] (x)    (1 . y)               = (x)
  [ 0 ][ cosA ][ -sinA ][ 0 ] (y) -> (cosA . y - sinA . z) = (y)
  [ 0 ][ sinA ][  cosA ][ 0 ] (z)    (sinA . y + cosA . z) = (z)
  [ 0 ][  0   ][   0   ][ 1 ] (w)    (1 . w)               = (w)
```

Rotation counterclock around the y axis:

```
  [  cosA ][ 0 ][ sinA ][ 0 ] (x)    (cosA . x + sinA . z)  = (x)
  [   0   ][ 1 ][  0   ][ 0 ] (y) -> (1 . y)                = (y)
  [ -sinA ][ 0 ][ cosA ][ 0 ] (z)    (-sinA . x + cosA . z) = (z)
  [   0   ][ 0 ][  0   ][ 1 ] (w)    (1 . w)                = (w)
```

In all cases, the rotation is in the direction of the first axis toward the second axis — that is, from the row with the cos –sin pattern to the row with the sin cos pattern, for the positive axes corresponding to these rows.


# Referências

- KESSENICH, J. et al. OpenGL Programming Guide: the official guide to learning OpenGL, versions 4.5. 9th ed. Boston: Pearson Education, 2017.  
- WOLFF, D. OpenGL 4 Shading Language Cookbook. 3rd ed. Birmingham: Packt Publishing, 2018.  
- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.  
- Scratchapixel. The Perspective and Orthographic Projection Matrix. Disponível em: [link](https://www.scratchapixel.com/lessons/3d-basic-rendering/perspective-and-orthographic-projection-matrix/projection-matrix-introduction.html).  
- LearnOpenGL - Cmaera. Available in [https://learnopengl.com/Getting-started/Camera](https://learnopengl.com/Getting-started/Camera).  