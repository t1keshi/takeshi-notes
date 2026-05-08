Previous: [Computer Graphics](../_cg.md)  

# Lighiting and Reflection

- [Diffuse Reflection Model](diffuse.md)  
- [Phong Reflection Model](phong.md)  

Quando um modelo de reflexão é calculado no vertex shader (por vértice) é chamado de **Gouraud Shading**. Isto reduz a quantidade de cálculos por draw call em comparação se fosse calculado por fragmento. Entretanto, o resultado visual perde qualidade. Por exemplo, o efeito de brilho especular pode se perder no centro do polígono, quando o componente especular fica com valor próximo do zero para o vértice. Outro efeito indesejável que pode ocorrer quando a cor interpolada não combinar com o resultado do modelo de reflexão produzindo arestas nos polígonos (_edge of polygons effect_).

Quando movemos o cálculo de modelo de reflexão para a etapa de fragment shader, conseguimos um resultado visual muito melhor já que estariamos utilizando valores de posição e normal interpolado por fragmento. Esta técnica é chamada de **Phong shading** ou **Interpolação Phong**. A sua grande desvantagem é que irá reduzir o desempenho em comparação com Gouraud shading, entretanto, cada vez mais as placas gráficas estão evoluindo melhorando o seu desempenho.

# Directional Lights

Modelos de reflexão que utilizam a posição da fonte de luz para determinar a sua direção ```s``` podem ser substituídos com **fonte de luz direcional** eliminando a necessidade de calcular a direção ```s``` porque a direção deste tipo de fonte é sempre a mesma. Este tipo de fonte de luz é ideal para modelar iluminação como a luz do sol.

# Two-side Shading

Quando um modelo contém "buracos" como, por exemplo, uma caixa aberta, as faces internas da caixa são consideradas como faces traseiras e não são iluminadas porque o vetor normal está invertido. Para esta situação, é necessário calcular novamente o modelo de reflexão mas com o vetor normal invertido.

Para descobrir se a face deve ser considerada como uma face traseira, basta calcular o produto escalar entre o vetor v que tem a direção do observador e o vetor n. Se o resultado for negativo, então a normal está apontando para outro lado do observador. Isto significa que o observador está visualizando a face traseira.

```
  float vDotN = dot(v, n);

  if(vDotN >= 0)
    // face fronteira
    color = phongModel(v, n);
  else
    // face traseira
    color  = phongModel(v, -n)
```

> **Nota:** API como OpenGL fornece outros meios para descobrir se a superfície é front ou back como a variável ``gl_FrontFacing`` disponível em fragment shader.

# Flat Shading

Flat shading é uma tonalização onde cada face do polígono tem uma única cor. Ou seja, não há variação de cor ao longo da face fazendo com que o polígono tenha uma aparência flat diferente de Gouraud shading. Em geral, este método é útil em situações de depuração de modelos geométricos complexos ou para criar outros efeitos flat.

Para criar este tipo de tonalização basta não interpolar as cores na fase de fragment shader. Basta calcular o modelo de reflexão na etapa de vertex shader e utilizar a cor do vértice sem interpolar na etapa de rasterização.

```
    // vertex shader
    flat out vec3 outColor;

    // fragment shader
    flat in vec3 inColor;
```


# References

- WOLFF, D. OpenGL 4 Shading Language Cookbook. 3rd ed. Birmingham: Packt Publishing, 2018.  
