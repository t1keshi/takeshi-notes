[Home](_opengl.md)

# The OpenGL Rendering Pipeline

A **pipeline de renderização** é uma sequência de estágios para a conversão de dados de vértices em uma imagem em pixels que será armazenada em um **framebuffer**. Normalmente, a pipeline gráfica é implementada no próprio hardware da **GPU** (_Unidade de Processamento Gráfico_).

Alguns estágios desta pipeline são programáveis. No caso de OpenGL, utilizamos a linguagem chamada **GLSL** (_OpenGL Shading Language_) para criar o bloco de código que será executado diretamente pela GPU. Estes blocos de código são chamados de **shader** e para cada estágio da pipeline de renderização existe um tipo de shader.

Os estágios da _pipeline_ de renderização de OpenGL são:

- **Vertex Shader** (obrigatório)
- **Tessellation Shader** (opcional)
- **Geometry Shader** (opcional)
- Clipping and Rasterization  (executado implicitamente pelo OpenGL)
- **Fragment Shader** (obrigatório)
- Per-fragment operations (executado implicitamente pelo OpenGL)
- **Compute Shader** (opcional)

O mesmo shader pode ser executado múltiplas vezes em diferentes dados de forma paralela. Por exemplo, para renderizar um cubo que possui oito vértices, **vertex shader** é executado de forma paralela oito vezes - uma execução para cada vértice. Outro exemplo é o **fragment shader** que é executado de forma paralela múltiplas vezes - uma execução para cada **fragmento** - que é um _candidato a se tornar um pixel_ no framebuffer.

O conjunto de shaders de cada estágio forma um programa de shader conhecido como **GLSL shader program**. Uma aplicação OpenGL pode conter diversos programas de shader mas apenas um programa pode estar ativo.

> **Nota:** Nas versões anteriores a OpenGL 2.0, a pipeline de renderização não era programável - conhecido como _Fixed-Function Pipeline_. A partir da versão 3.2, a utilização de shaders se tornou obrigatória. O advento da pipeline de renderização programável foi um marco na área da Computação Gráfica porque tornou a renderização mais flexível, eficiente e aumentou significativamente o desempenho da renderização.

A imagem final gerada pelo processo de renderização consiste em **pixels** (menor elemento visível de um monitor) armazenados em um **framebuffer** que é um bloco de memória gerenciado pelo hardware gráfico e enviado para o monitor.

# Referências

- KESSENICH, J. et al. OpenGL Programming Guide: the official guide to learning OpenGL, versions 4.5. 9th ed. Boston: Pearson Education, 2017.
- WOLFF, D. OpenGL 4 Shading Language Cookbook. 3rd ed. Birmingham: Packt Publishing, 2018.
- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.  
- Fixed Function Pipeline. Disponível em [https://www.khronos.org/opengl/wiki/Fixed_Function_Pipeline](https://www.khronos.org/opengl/wiki/Fixed_Function_Pipeline).
