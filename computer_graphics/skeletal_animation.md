Previous: [Computer Graphics](_cg.md)  

# Skeletal Animation

**Skeletal Animation** é um método de animação para modelos 3D.

- Skin é o modelo geométrico
- Bones

Interpolação linear (lerp) para translação e escala

```
    a = a * (1 - t) + b * t
```

Para rotação (spherical interpolation ou slerp), é necessário utilizar ```quaternion```.

# Bones

**Bones** são representados através de uma estrutura de dados do tipo **hierarquia de nós** (_node hierarchy_), onde cada bone é representado por um nó.

Um vértice pode ser influenciado por N bones, isto é, sofrer transformações que correspondam a skeletal animation.

Um único bone pode influenciar um conjunto de vértices do mesh e o quanto ele deve influenciar é determinado por **weight**. Portanto, cada bone contém um array de vértices e um array de weights correspondentes.


# Keyframes

**Keyframes** representam as "poses" para cada tempo chave dentro de uma animação.

As poses são interpoladas de uma pose para outra para que a transição entre elas seja suave.


# Skinning
- Joints
- Inverse Bind Matrices

# Vertex attributes
- Joints
- Weights

# Animation Data
- Samplers
    - input
    - output
    - interpolation type

- Channels

# Interpolation

# References

- https://github.khronos.org/glTF-Tutorials/
- https://learnopengl.com/Guest-Articles/2020/Skeletal-Animation
- https://lisyarus.github.io/blog/posts/gltf-animation.html
