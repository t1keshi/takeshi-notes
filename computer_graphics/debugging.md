Previous: [Computer Graphics](_cg.md)  

# Debugging

### Winding Issues

Para verificar se um modelo geométrico está com orientação de faces correta (_winding_), isto é, vértices em ordem anti horária ou horária, podemos utilizar a ideia de **two-sided rendering** em fragment shader:

```
    if(gl_FrontFacing) {
        fragmentColor = vec4(1.0, 0.0, 0.0, 1.0); // red
    } else {
        fragmentColor = vec4(0.0, 0.0, 1.0, 1.0); // blue
    }
```

Se o modelo renderizar a face da frente com cor diferente de vermelho ou a face traseira com cor diferente de azul há um problema na especificação dos vértices ou indíces do modelo.

# References

- WOLFF, D. OpenGL 4 Shading Language Cookbook. 3rd ed. Birmingham: Packt Publishing, 2018.  
