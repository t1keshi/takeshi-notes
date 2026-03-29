Previous: [Computer Graphics](_cg.md)  

# Lighiting and Reflection


# Diffuse reflection model  

A **reflexão difusa** ou **reflexão Lambertiana** é um modelo de reflexão que assume que uma superfície puramente difusa irradia a luz incidente igualmente em todas as direções independentemente da direção. Há uma interação entre a luz incidente e a superfície antes que ela seja irradiada, fazendo com que os objetos apresentem superfícies totalmente ou parcialmente opacas.

O modelo matemático para a reflexão difusa envolve dois vetores: vetor **s** que representa a direção de um ponto da superfície (vértice) até a fonte de luz e o vetor **n** que representa uma direção perpendicular à superfície que receberá a luz incidente também conhecido como **vetor normal**.

A quantidade da luz incidente (**Ld**) que atinge a superfície depende da orientação do vetor **n** em relação ao vetor **s**. Caso o ângulo entre os dois vetores seja 0º, a superfície estará recebendo a quantidade máxima de luz e se o ângulo for 90º ou maior, a superfície não estará recebendo nada de luz. Dessa forma, podemos calcular a intensidade da luz atingida na superfície utilizando o cosseno do ângulo entre os vetores s e n ou o produto escalar entre eles (```s . n```).

```
    Ld = cos(a)
    Ld = s . n
```

> **Nota:** para utilizar o produto escalar, os vetores n e s precisam estar normalizados.

Para modelar a absorção da luz incidente na superfície, utilizamos o **coeficiente de reflexão (Kd) ou diffuse reflectivity** que representa a fração de luz incidente que é espalhada pela superfície. Este coeficiente é utilizado como fator de escala.

```
    L = KdLd(s . n)
```

> **Note:** Because this model depends only on the direction towards the light source and the normal to the surface, not on the direction towards the viewer, we have a model that represents uniform (omnidirectional) scattering.

Antes de realizar o cálculo da intensidade de luz, precisamos transformar os vetores **s** e **n** para _eye-space_ multiplicando pela matriz **model-view**.

Para transformar o vetor **n**, precisamos utilizar a inversa transposta da matriz **mode-view**.

```
    mat4 modelViewTransform = viewTransform * vModelTransform;
    mat3 normalTransform = transpose(inverse(mat3(modelViewTransform)));
    vec3 normal = normalize(normalTransform * vNormal);
```

Como o vetor **n** representa uma direção e não uma posição como o vértice, utilizamos uma matriz 3x3 para que ele não sofra translação.

Se a matriz **model-view** não contém escala não uniforme podemos utilizar diretamente a parte 3x3 da matriz **model-view**.

```
    mat3 normalTransform = mat3(modelViewTransform);
    vec3 n = normalize(normalTransform * vNormal);
```

> **Nota:** Se a matriz **mode-view** contiver escala uniforme, é necessário normalizar o resultado da transformação.

O próximo passo é encontrar o vetor **s** utilizando a posição do vértice (já transformado para _eye-space_) e a posição da fonte de luz.

```
    vec4 position = modelViewTransform * vec4(vPosition, 1.0);
    vec3 s = normalize(vec3(lightPosition - position.xyz));
```

Com os vetores **s** e **n** apropriadamente calculados, podemos realizar o cálculo de intensidade da luz:

```
    vec3 lightIntensity = Ld * Kd * max(dot(s, n), 0.0);
```

> **Nota:** Para evitar situações onde o ângulo entre os dois vetores seja maior que 90º graus (luz incidente que vem de dentro da superfície), utilizamos a função ```max``` para evitar valores negativos gerados pelo produto escalar.

Este modelo de reflexão possui algumas limitações dependendo do tipo de superfície. Ele é melhor utilizado para simular efeitos de superfícies opacas. Além disso, partes da superfície que não recebem luz incidente podem se tornam muito escuras ou com a cor completamente preta. Contudo, em outros modelos de reflexão como Phong, estas áreas são compensadas utilizando a reflexão Ambiente.


# Phong reflection model

# References

- WOLFF, D. OpenGL 4 Shading Language Cookbook. 3rd ed. Birmingham: Packt Publishing, 2018.  
