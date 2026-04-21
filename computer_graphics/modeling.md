Previous: [Computer Graphics](_cg.md)

# Modeling

# Building Spheres

Podemos obter as coordenadas ```x``` e ```y``` de um ponto no círculo de raio ```R``` através de funções **seno** e **cosseno**:

```
    x = R * cos(angleInRad);
    y = R * sen(angleInRad);
```

> **Nota:** As funções seno e cosseno e a sua relação com o círculo são estudados em [Trigonometria](../mathematic/geometry/trigonometry.md).

Iniciamos a construção da esfera, subdividindo em  ```n``` círculos horizontais (_slices_).

Para cada círculo horizontal, subdividimos em ```n``` pontos (vértices).

Estes pontos serão utilizados para criar triângulos que representam a superfície da esfera. Quanto maior o número de circulos horizontais e pontos, maior a suavidade da esfera.

Algoritmo para criar os vértices da esfera de raio 1:

```
	for (size_t i = 0; i <= slices; i++) {
			float theta = M_PI - (M_PI * i / slices);
			float y = std::cos(theta);
			float r = std::sin(theta);

		for (size_t j = 0; j <= points; j++) {
			float phi = 2 * M_PI * j / points;
			float x = r * std::cos(phi);
			float z = r * std::sin(phi);
		}
	}
```

A ideia é utilizar o **ângulo vertical** (_theta_) de 0º a 180º para obter a altura de cada círculo horizontal e o **ângulo horizontal** (_phi_) de 0º a 360º ao redor do eixo y para obter os pontos do círculo horizontal.

A equação ```float y = M_PI - (M_PI * i / slices)``` define a altura de cada círculo horizontal. Quando ```i == 0``` (primeiro círculo horizontal), será calculado o cosseno de 180º (M_PI) que resulta em ```y == -1```. Quando ```i == slices```, será calculado o cosseno de 0º, resultado no valor ```y == 1```. Isto explica porque só precisamos percorrer pontos de 0º a 180º para a altura do ```y```.

> **Nota:** Observe que ```M_PI - (M_PI * i / slices)``` faz com que iniciemos do círculo horizontal inferior até o círculo horizontal superior. Isto é proposital para calcular os índices dos dois triângulos para cada vértice como verá em seguida.

O raio de cada círculo horizontal é calculado através do seno do ângulo (_theta_) utilizado na equação acima.

Com o raio obtido, basta calcular os pontos (x, z) de cada círculo horizontal utilizando ```x = cos(phi)``` e ```z = sen(z)```.

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
