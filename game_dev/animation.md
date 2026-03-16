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

```CurrentTime``` é um exemplo de um valor que pode ser utilizado como valores de ```sin``` e ```cos```. Estas funções trigonométricas aceitam valores que "crescem"/"decrescem" continuamente mas o resultado será sempre um valor entre [-1, 1] e que variam de acordo a função a matemática e se repetem após competar um período.

Podemos utilizar um valor constante para ajustar o valor que passamos para ```sin``` e ```cos```.

O valor que é multiplicado após o cálculo do seno e cosseno aumenta o intervalo de valores de [-1, 1] para o valor multiplicado. Neste caso, aumentamos o intervalo para [-2, 2].


# Referências

- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.  