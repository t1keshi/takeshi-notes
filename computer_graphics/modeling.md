Previous: [Computer Graphics](_cg.md)

# Modeling

# Building Spheres

Considerando um círculo de raio R, conseguimos obter as coordenadas x e y do círculo através de funções seno e cosseno:

```
    x = R * cos(angleInRad);
    y = R * sen(angleInRad);
```

Para construir uma esfera, dividimos ele com N círculos horizontais (_slices_). Chamamos N de **precisão**.

Para cada círculo horizontal, subdividimos em N pontos. Estes pontos serão utilizados para criar triângulos que representam a superfície da esfera.

Quanto maior o número de circulos horizontais e pontos, maior a suavidade da esfera.

Os triângulos são criados percorrendo os pontos horizontais de baixo para cima. Para cada ponto encontrado, são construídos dois triângulos.

```
    for(size_t i = 0; i < slices; i++) {
        for(size_t j = 0; j < points; j++) {
            GLfloat y = cos(toRadian(180.0f - i * 180.0f / points));
            GLfloat x = -cos(toRadian(j * 360.0f / points)) * abs(cos(asin(y)));
            GLfloat z = sin(toRadian(j * 360.0f / points)) * abs(cos(asin(y)));
        }
    }
```

Vertices
Coordenadas de texturas
Normais


# References

- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.  
