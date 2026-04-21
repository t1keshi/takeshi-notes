Previous: [Computer Graphics](_cg.md)

# Modeling

# Building Spheres

Podemos obter as coordenadas ```x``` e ```y``` de um ponto no círculo de raio ```R``` através de funções **seno** e **cosseno**:

```
    x = R * cos(angleInRad);
    y = R * sen(angleInRad);
```

> **Nota:** As funções seno e cosseno e a sua relação com o círculo são estudados em [Trigonometria](../mathematic/geometry/trigonometry.md).

Para construir uma esfera, dividimos ele com ```n``` círculos horizontais (_slices_).

Para cada círculo horizontal, subdividimos em ```n``` pontos (vértices).

Estes pontos serão utilizados para criar triângulos que representam a superfície da esfera. Quanto maior o número de circulos horizontais e pontos, maior a suavidade da esfera.

Algoritmo para criar os vértices da esfera:

```
    for(size_t i = 0; i < slices; i++) {
        for(size_t j = 0; j < points; j++) {

            float y = cos(M_PI - (i * M_PI / slices));
            float x = -cos(toRadian(j * 360.0f / points)) * abs(cos(asin(y)));
            float z = sin(toRadian(j * 360.0f / points)) * abs(cos(asin(y)));
        }
    }
```

A ideia é utilizar o **ângulo vertical** (theta) de 0º a 180º (polo sul) e o **ângulo horizontal** (phi) que gira 360º ao redor do eixo y para percorrer a superfície da esfera.

A equação ```float y = M_PI - (i * M_PI / points)``` define a altura de cada círculo horizontal. Quando ```i == 0``` (primeiro círculo horizontal), será calculado o cosseno de 180º ou M_PI que resulta no valor ```-1``` para ```y```. Quando ```i == slices```, será calculado o cosseno de 0º, resultado no valor ```1``` para ```y```. Isto explica porque só precisamos percorrer pontos de 0º a 180º (M_PI).

Para calcular o raio de cada círculo horizontal, basta utilizar a identidade trigonométrica onde se ```y = sin(a)```, então o raio no plano XZ é ```cos(a)```.


Os vértices são listados a partir do círculo horizontal mais inferior e são percorridos de forma circular.

O vetor normal de cada vértice da esfera é simplesmente um vetor que aponta da origem (centro da esfera) até o vértice. Não é necessário normalizar o vetor normal porque o algoritmo acima cria uma esfera com o raio de tamanho 1.

Com os vértices da esfera criados, os triângulos são construídos através de índices para esses vértices.

Iniciando com o círculo horizontal inferior, para cada vértice percorrido especificamos os 6 índices dos vértices formando dois triângulos. Os triângulos são construídos de acordo com o padrão CCW (_couter clock winding_) da seguinte forma:

1. vértice atual (```i * (n + 1) + j)```)  
2. vértice à direta do vértice atual (```i * (n + 1) + j + 1```)  
3. vértice à cima do vértice atual (```(i + 1) * (n + 1) + j```)  

> **Nota:** ```n + 1``` está cosiderando o vértice adicional (coincidente) que fecha o círculo.

```
    for (int i = 0; i < slices; i++) {
        for (int j = 0; j < points; j++) {
            // first triangle
            indices[6 * (i * points + j) + 0] = i * (points + 1) + j;
            indices[6 * (i * points + j) + 1] = i * (points + 1) + j + 1;
            indices[6 * (i * points + j) + 2] = (i + 1) * (points + 1) + j;
            // second triangle
            indices[6 * (i * points + j) + 3] = i * (points + 1) + j + 1;
            indices[6 * (i * points + j) + 4] = (i + 1) * (points + 1) + j + 1;
            indices[6 * (i * points + j) + 5] = (i + 1) * (points + 1) + j;
        }
    }
```

# References

- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.  
