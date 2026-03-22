# Hierarchical Transformation

Em uma hierarquia de transformações, todos os objetos desta hierarquia precisam ser transformados no seu espaço local primeiro e depois transformar com a transformação do pai. Na Computação Gráfica, a convenção na multiplicação de matrizes é sempre da direita para a esquerda.

```
    mat4 transform = parentTransform * localTransform;
```


# References

- 