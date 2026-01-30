[Home](_opengl.md)  


# Introdução

**OpenGL** (Open Graphics Library) é uma interface de software (API) para o hardware gráfico que possibilita escrever programas interativos capazes de **renderizar** modelos geométricos e imagens em tempo real através de diversos métodos de Computação Gráfica.

OpenGL é uma especificação independente de hardware mantida pelo grupo **KHRONOS** ([_The Khronos Group, Inc._](https://en.wikipedia.org/wiki/Khronos_Group)) que é um consórcio aberto sem fins lucrativos constituído por diversas organizações. Este grupo é responsável pela aprovação de novas funcionalidades, versões e extensões de OpenGL. Anteriormente, este grupo era conhecido como **OpenGL ARB** ([*OpenGL Architecture Review Board*](https://en.wikipedia.org/wiki/OpenGL_Architecture_Review_Board)).

As implementações de OpenGL em cada plataforma de hardware podem variar em questões de desempenho ou funcionalidades adicionais. OpenGL pode até mesmo ser implementado inteiramente como software (por exemplo, em máquinas virtuais). Consulte a documentação da implementação que estiver utilizando para obter mais detalhes – você pode encontrar exemplos de código otimizados para o seu sistema. Além disso, o fornecedor da implementação pode oferecer ferramentas como depuradores de _gpus_, ferramentas de análise de desempenho, etc.

A NVidia, por exemplo, oferece as seguintes ferramentas para ajudar na depuração e análise de desempenho:

- NVIDIA Nsight Vistual Studio Edition ([https://developer.nvidia.com/nsight-visual-studio-edition](https://developer.nvidia.com/nsight-visual-studio-edition))
- NVIDIA PerfKit ([https://developer.nvidia.com/nvidia-perfkit](https://developer.nvidia.com/nvidia-perfkit))
- NVIDIA Nsight Graphics ([https://developer.nvidia.com/nsight-graphics](https://developer.nvidia.com/nsight-graphics))

Segue uma lista de links onde poderá encontrar mais informações sobre ferremantas de depuração:

- [https://www.khronos.org/opengl/wiki/Getting_Started](https://www.khronos.org/opengl/wiki/Getting_Started).
- [https://www.khronos.org/opengl/wiki/Debugging_Tools](https://www.khronos.org/opengl/wiki/Debugging_Tools)

A última versão de OpenGL é **4.6**. É possível obter a sua especificação em [https://www.khronos.org/registry/OpenGL/index_gl.php](https://www.khronos.org/registry/OpenGL/index_gl.php).

> **Nota:** A especificação de OpenGL não está mais em desenvolvimento. A última versão publicada foi em 5 de Maio de 2022. O grupo está focado agora no desenvolvimento de [Vulkan](https://www.vulkan.org/).

OpenGL é independente de sistema operacional e, portanto, independente de inteface gráfica do usuário ou sistema de janelas. A sua especificação não inclui funções para gerenciamento de janelas de aplicação, tratamento de eventos do sistema operacional, processamento de entrada de dados do usuário, operações para leitura de arquivos de imagens e nem mesmo estruturas de dados ou abstrações para descrever modelos geométricos. Cada sistema operacional como **Microsoft Windows**, **Apple Mac OS** e **Linux** oferece extensões que incluem funcionalidades adicionais para que você possa utilizar OpenGL em seus respectivos sistemas de janelas:

- **WGL** (extensão OpenGL para sistema de janelas do Microsoft Windows)
- **GLX** (extensão OpenGL para sistema de janelas X-Window em plataformas baseado em Linux)
- **AGL** (extensão para sistema de janelas da Apple)

> **Nota:** A Apple descontinuou o uso de OpenGL em seus sistemas. A última versão de OpenGL disponível em um MacOS foi 4.1.

Para obter mais detalhes sobre OpenGL, consulte: [https://www.opengl.org](https://www.opengl.org/). Este website contém especificação de OpenGL, documentação, exemplos, fórum de discussão e novidades sobre OpenGL.

Outras fontes úteis sobre OpenGL:

- [https://www.khronos.org/opengl/wiki/Main_Page](https://www.khronos.org/opengl/wiki/Main_Page)
- [https://learnopengl.com/](https://learnopengl.com/)


# OpenGL e as linguagens de programação

A linguagem de programação nativa de OpenGL é C. Entretanto, existem também "bindings" para outras linguagens de programação como Java, Perl, Python, C#, Visual Basic, Delphi, Haskell, Lisp, Ruby, etc com desempenho virtualmente equivalente.


# Variações de OpenGL

- **OpenGL ES** (OpenGL Embedded Systems)  
- **WebGL** (based on OpenGL ES)  


# OpenGL como um sistema cliente-servidor

Originalmente, OpenGL foi implementado como um sistema cliente-servidor, onde a aplicação OpenGL é o "cliente" e a implementação da API OpenGL pelas fabricantes é o "servidor". Este tipo de arquitetura é bem parecido com o de **X Window System**. Isto significa que existem implementações OpenGL onde uma máquina pode enviar comandos OpenGL através da rede para uma outra máquina realizar a renderização. Nas implementações modernas, o hardware gráfico que implementa a API OpenGL é considerado como "servidor" e a aplicação OpenGL que é executada pela CPU é considerado o "cliente".


# Renderização baseada em Rasterização

OpenGL é um sistema baseado em **rasterização**. Entretanto, nas versões mais rencentes de OpenGL, nada impede a aplicação de otros algoritmos como **ray-tracing**, **photon mapping**, **path tracing** e **image-based rendering**.


# Referências

- KESSENICH, J. et al. OpenGL Programming Guide: the official guide to learning OpenGL, versions 4.5. 9th ed. Boston: Pearson Education, 2017.
- WOLFF, D. OpenGL 4 Shading Language Cookbook. 3rd ed. Birmingham: Packt Publishing, 2018.
- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.
- WIKIPEDIA. Khronos Group. Disponível em [https://en.wikipedia.org/wiki/Khronos_Group](https://en.wikipedia.org/wiki/Khronos_Group).
- WIKIPEDIA. OpenGL Architecture Review Board. Disponível em [https://en.wikipedia.org/wiki/OpenGL_Architecture_Review_Board](https://en.wikipedia.org/wiki/OpenGL_Architecture_Review_Board).
