Previous: [Computer Graphics](_cg.md)  

# Lighiting and Reflection


# Diffuse reflection model  

A **reflexão difusa** ou **reflexão Lambertiana** é um modelo de reflexão que assume que uma superfície puramente difusa irradia a luz incidente igualmente em todas as direções independentemente da direção. Há uma interação entre a luz incidente e a superfície antes que ela seja irradiada, fazendo com que os objetos apresentem superfícies totalmente ou parcialmente opacas.

O modelo matemático para a reflexão difusa envolve dois vetores: vetor **s** que representa a direção de um ponto da superfície (vértice) até a fonte de luz e o vetor **n** que representa uma direção perpendicular à superfície que receberá a luz incidente também conhecido como **vetor normal**.

A quantidade da luz incidente que atinge a superfície depende da orientação do vetor **n** em relação ao vetor **s**. Caso o ângulo entre os dois vetores seja 0º, a superfície estará recebendo a quantidade máxima de luz e se o ângulo for 90º ou maior, a superfície não estará recebendo nada de luz. Dessa forma, podemos calcular a quantidade de radiação atingida na superfície multplicando o cosseno do ângulo entre os vetores s e n ou o produto escalar entre eles (```s . n```) pela intensidade da fonte de luz **Ld**.

```
    Ld * cos(a)
    Ld * (s . n)
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

O próximo passo é encontrar o vetor **s** utilizando a posição do vértice (já transformado para _eye-space_) e a posição da fonte de luz que também deve estar em _eye-space_.

```
    vec4 lightPos = viewTransform * vec4(lightPosition, 1.0);
    vec4 position = modelViewTransform * vec4(vPosition, 1.0);
    vec3 s = normalize(vec3(lightPos - position.xyz));
```

Com os vetores **s** e **n** apropriadamente calculados, podemos realizar o cálculo de intensidade da luz:

```
    vec3 lightIntensity = Ld * Kd * max(dot(s, n), 0.0);
```

> **Nota:** Para evitar situações onde o ângulo entre os dois vetores seja maior que 90º graus (luz incidente que vem de dentro da superfície), utilizamos a função ```max``` para evitar valores negativos gerados pelo produto escalar.

Este modelo de reflexão possui algumas limitações dependendo do tipo de superfície. Ele é melhor utilizado para simular efeitos de superfícies opacas. Além disso, partes da superfície que não recebem luz incidente podem se tornam muito escuras ou com a cor completamente preta. Contudo, em outros modelos de reflexão como Phong, estas áreas são compensadas utilizando a reflexão Ambiente.


# Phong reflection model (Phong shading model)

O modelo de reflexão **Phong**, criado pelo pesquisador _Bui Tuong Phong_, modela a interação entre os raios de luz com a superfície com a soma de três componentes:

- **Ambiente**
- **Difusa**
- **Especular**

O componente ambiente modela a luz que é emanado uniformemente a partir de todas as direções - luz que provavelmente foi refletida múltiplas vezes na cena. Este componente ajuda a iluminar superfícies que não recebem luz direta (calculado a partir da fonte de luz e o vetor normal). Sem o componente ambiente, estas superfícies seriam da cor preta.

```
    Ia = LaKa
```

O componente difusa represent a reflexão omnidirecional. Ele foi discutido no tópico anterior.

```
    Id = LdKd(s . n)
```

The specular component models the shininess of the surface and represents glossy reflection around a preferred direction.
The specular component is used for modeling the shininess of a surface. When a surface has a glossy shine to it, the light is reflected off of the surface, scattered around some preferred direction. We model this so that the reflected light is strongest in the direction of perfect (mirror-like) reflection. The physics of the situation tells us that for perfect reflection, the angle of incidence is the same as the angle of reflection and that the vectors are coplanar with the surface normal.

In the preceding diagram, r represents the direction of pure reflection corresponding to the incoming light vector (-s), and n is the surface normal. We can compute r by using the following equation:

```
    r = -s + 2(s . n)n
```

To model specular reflection, we need to compute the following (normalized) vectors: the direction toward the light source (s), the vector of perfect reflection (r), the vector toward the viewer (v), and the surface normal (n).

We would like the reflection to be maximal when the viewer is aligned with the vector r, and to fall off quickly as the viewer moves farther away from alignment with r. This can be modeled using the cosine of the angle between v and r raised to some power (f).

```
    Is = LsKs(r . v)^f
```

The larger the power, the faster the value drops toward zero as the angle between v and r increases. Again, similar to the other components, we also introduce a
specular light intensity term (Ls) and reflectivity term (Ks). It is common to set the Ks term to some grayscale value (for example, (0.8, 0.8, 0.8)), since glossy reflection is not (generally) wavelength dependent.

The specular component creates specular highlights (bright spots) that are typical of glossy surfaces. The larger the power of f in the equation, the smaller the specular highlight and the shinier the surface. The value for f is typically chosen to be somewhere between 1 and 200.

```
    I = Ia + Id + Is
```


# References

- WOLFF, D. OpenGL 4 Shading Language Cookbook. 3rd ed. Birmingham: Packt Publishing, 2018.  
