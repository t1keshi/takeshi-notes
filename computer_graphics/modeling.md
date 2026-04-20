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

Para cada círculo horizontal, subdividimos em ```n``` pontos (vértices). Estes pontos serão utilizados para criar triângulos que representam a superfície da esfera.

Quanto maior o número de circulos horizontais e pontos, maior a suavidade da esfera.

Algoritmo para criar os vértices da esfera:

```
    for(size_t i = 0; i < slices; i++) {
        for(size_t j = 0; j < points; j++) {

            GLfloat y = cos(toRadian(180.0f - i * 180.0f / points));
            GLfloat x = -cos(toRadian(j * 360.0f / points)) * abs(cos(asin(y)));
            GLfloat z = sin(toRadian(j * 360.0f / points)) * abs(cos(asin(y)));
        }
    }
```

The vertices are stored in a one-dimensional array, starting with the vertices in the bottommost horizontal slice. 

O vetor normal de cada vértice da esfera é simplesmente um vetor que aponta da origem (centro da esfera) até o vértice. Não é necessário normalizar o vetor normal porque o algoritmo acima cria uma esfera com o raio de tamanho 1.

Com os vértices da esfera criados, os triângulos são construídos através de índices para esses vértices.

Iniciando com o círculo horizontal inferior, para cada vértice percorrido especificamos os 6 índices dos vértices formando dois triângulos.

```
    for (int i = 0; i < slices; i++) {
        for (int j = 0; j < points; j++) {
            indices[6 * (i * points + j) + 0] = i * (points + 1) + j;
            indices[6 * (i * points + j) + 1] = i * (points + 1) + j + 1;
            indices[6 * (i * points + j) + 2] = (i + 1) * (points + 1) + j;
            indices[6 * (i * points + j) + 3] = i * (points + 1) + j + 1;
            indices[6 * (i * points + j) + 4] = (i + 1) * (points + 1) + j + 1;
            indices[6 * (i * points + j) + 5] = (i + 1) * (points + 1) + j;
        }
    }
```

# References

- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.  
