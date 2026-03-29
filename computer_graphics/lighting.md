Previous: [Computer Graphics](_cg.md)  

# Lighiting and Reflection


# Diffuse reflection model  

A **reflexão difusa** ou **reflexão Lambertiana** é um modelo de reflexão que assume que uma superfície puramente difusa irradia a luz incidente igualmente em todas as direções independentemente da direção. Há uma interação entre a luz incidente e a superfície antes que ela seja irradiada, fazendo com que os objetos apresentem superfícies totalmente ou parcialmente opacas.

O modelo matemático para a reflexão difusa envolve dois vetores: vetor **s** que representa a direção de um ponto da superfície (vértice) até a fonte de luz e o vetor **n** que representa uma direção perpendicular a suerfície que receberá a luz incidente também conhecido como **vetor normal**.

A quantidade da luz incidente (**Ld**) que atinge a superfície depende da orientação do vetor **n** em relação ao vetor **s**. Caso o ângulo entre os dois vetores seja 0º, a superfície estará recebendo a quantidade máxima de luz e se o ângulo for 90º ou maior, a superfície não estará recebendo nada de luz. Dessa forma, podemos calcular a intensidade da luz atingida na superfície utilizando o cosseno do ângulo entre os vetores s e n ou produto escalar entre eles (```s . n```).

```
    Ld = cos(a)
    Ld = s . n
```

> **Nota:** para utilizar o produto escalar, os vetores n e s precisam estar normalizados.

Para modelar a absorção da luz incidente na superfície, utilizamos o **coeficiente de reflexão (Kd) ou diffuse reflectivity** que representa a fração de luz incidente que é espalhada pela superfície. The diffuse reflectivity becomes a scaling factor, so the intensity of the outgoing light can be expressed as follows:

```
    L = KdLd(s . n)
```

> **Note:** Because this model depends only on the direction towards the light source and the normal to the surface, not on the direction towards the viewer, we have a model that represents uniform (omnidirectional) scattering.


# Phong reflection model

# References

- WOLFF, D. OpenGL 4 Shading Language Cookbook. 3rd ed. Birmingham: Packt Publishing, 2018.  
