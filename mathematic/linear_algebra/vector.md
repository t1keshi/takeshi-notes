[Linear Algebra](README.md)

# Vetores

Um vetor é um elemento de um conjunto chamado **espaço vetorial** - uma estrutura que possui certas propriedades matemáticas relacionadas à adição e à multiplicação por escalar.

O **espaço vetorial euclidiano** lida com espaços bidimensionais e tridimensionais, utilizados para representar posição, velocidade, direção, etc por meio de vetores.

# Produto Escalar (a . b)

Cálculo do produto escalar:

```
    a . b = a.x * b.x + a.y * b.y + a.z * b.z
```

Produto escalar permite encontrar o ângulo entre dois vetores normalizados.

```
    cos(x) = a . b
```

Se dois vetores são perpendiculares.

```
    a . b = 0
```

Se dois vetores são paralelos.

```
    a . b = |a| * |b|
```

Se dois vetores são paralelos mas apontando para direções opostas.

```
    a . b = -|a| * |b|
```

Se o ângulo entre dois vetores estão no intervalo [-90º, 90º]

```
    a . b > 0
```

Encontrar a distância mínima de um ponto P (x, y, z) até o plano S (a, b, c, d). O sinal indica o lado do plano S onde o ponto se encontra.

```
    S = (a, b, c, d)
    
        (a / sqrt(a*a + b*b + c*c))
    n = (b / sqrt(a*a + b*b + c*c))
        (c / sqrt(a*a + b*b + c*c))
    
    D = d / sqrt(a*a + b*b + c*C)

    distância mínima entre P e S = (n . P) + D
```

# Produto Vetorial (a x b)

O produto vetorial produz um vetor normal perpencidular ao plano formado por vetores a e b não colineares.

```
            a.y * b.z - a.z * b.y
    a x b = a.z * b.x - a.x * b.z
            a.x * b.y - a.y * b.x
```

Alterar a ordem dos vetores produz um vetor normal que aponta para a direção oposta.

# References

- MILLINGTON, I. Game Physics Engine Development, 2nd ed. Morgan Kaufmann Publishers, 2010.  
