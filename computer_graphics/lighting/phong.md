Previous: [Lighting](lighting.md)  


# Phong Reflection Model

O modelo de reflexão **Phong**, criado pelo _Bui Tuong Phong_, modela a interação entre os raios de luz com a superfície com a soma de três componentes:

- **Ambiente**
- **Difusa**
- **Especular**

O componente ambiente modela a luz que é emanado uniformemente a partir de todas as direções - luz que provavelmente foi refletida múltiplas vezes na cena. Este componente ajuda a iluminar superfícies que não recebem luz direta. Sem o componente ambiente, estas superfícies seriam muito escuras ou completamente da cor preta.

```
    Ia = LaKa
```

O componente difusa representa a reflexão omnidirecional. Ele foi discutido no tópico [Reflexão Difusa](diffuse.md). 

```
    Id = LdKd(s . n)
```

O componente especular modela a reflexão do brilho da superfície em torno de uma determinada direção.

We model this so that the reflected light is strongest in the direction of perfect (mirror-like) reflection. The physics of the situation tells us that for perfect reflection, the angle of incidence is the same as the angle of reflection and that the vectors are coplanar with the surface normal.

In the preceding diagram, r represents the direction of pure reflection corresponding to the incoming light vector (-s), and n is the surface normal. We can compute r by using the following equation:

```
    r = -s + 2(s . n)n
```

To model specular reflection, we need to compute the following (normalized) vectors: the direction toward the light source (s), the vector of perfect reflection (r), the vector toward the viewer (v), and the surface normal (n).

We would like the reflection to be maximal when the viewer is aligned with the vector r, and to fall off quickly as the viewer moves farther away from alignment with r. This can be modeled using the cosine of the angle between v and r raised to some power (f).

```
    Is = LsKs(r . v)^f
```

The larger the power, the faster the value drops toward zero as the angle between v and r increases. Again, similar to the other components, we also introduce a specular light intensity term (Ls) and reflectivity term (Ks). It is common to set the Ks term to some grayscale value (for example, (0.8, 0.8, 0.8)), since glossy reflection is not (generally) wavelength dependent.

The specular component creates specular highlights (bright spots) that are typical of glossy surfaces. The larger the power of f in the equation, the smaller the specular highlight and the shinier the surface. The value for f is typically chosen to be somewhere between 1 and 200.

```
    I = Ia + Id + Is
```

# Nonlocal Viewer



# References

- WOLFF, D. OpenGL 4 Shading Language Cookbook. 3rd ed. Birmingham: Packt Publishing, 2018.  