[Game Development](README.md)

# Game Animation


# Animação contínua com seno e cosseno

Podemos utilizar a propriedade periódica das funções seno e cosseno para criar uma animação contínua.

Sabendo que os intervalos de valores das funções seno e cosseno são [-1, 1] e elas são funções periódicas, podemos utilizá-los para criar uma animação onde um objeto "vai e vem" continuamente.

```
    void update() {
        float currentTime = getCurrentTime();

        float tX = sin(0.35f * currentTime) * 2.0f;
        float tY = cos(0.52f * currentTime) * 2.0f;
        float tZ = sin(0.70f * currentTime) * 2.0f;

        matrix newPosition = translate(tX, tY, tZ);
    }
```


# Referências

- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.  