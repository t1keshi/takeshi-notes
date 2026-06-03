Previous: [Game Development](game_dev.md)  


# Entity Component System (ECS)

1. Resolve o problema de flexibilidade limitada da herança (programação orientada a objetos) no desenvolvimento de jogos.  
2. Resolve o uso indevido de memória cache.  

Na programação de jogos é muito comum iterar por um grupo de objetos de jogo a cada frame a fim de atualizar seus estados ou para processá-los de alguma maneira. Por exemplo, o sistema de física poderia iterar por uma parte deste grupo de objetos para atualizar informações como posiçãp, velocidade, etc enquanto que o sistema de renderização pooderia iterar por um grupo de objetos (que não precisa ser necessariamente o mesmo grupo de objetos) para desenhá-los na tela.

O problema do uso indevido de memória cache ocorre quando um objeto de jogo possui todos os dados possíveis contidos em si mesmo - uma classe com todos os dados declarados como membros. Ao iterar por um grupo de objetos desse tipo, muitos membros do objeto que não são necessários para o sistema que está processando no momento serão carregados na memória cache causando uma queda de desempenho. O problema pode ficar pior ainda se o grupo de objetos não estiverem armazenados de forma contígua na memória como, por exemplo, em estruturas do tipo lista vinculada ou árvores.


# Component System

Para evitar o mau uso da memória cache, os dados devem ser organizados como plain of data (POD) e armazenados de forma contígua na memória, por exemplo, em arrays.


# Entity

Uma entidade é simplemesnte um índice para o array de componentes. Os sistemas, como sistema de física, sistema de renderização, utilizam uma lista de entidades para acessar os elementos do array de componentes. Cada sistema referencia apenas o array de componentes de seu interesse. Dessa forma, tornamos mais eficiente o uso de memória cache.

O maior desafio para implementar um ECS é como os elementos dos arrays de componentes são reorganizados conforme as entidades são criadas/destruídas.


# Signature


# Ferramentas para checar memoria cache

- Intel VTune Profiler  
- AMD uProf  
- Visual Studio Profiler  
- Windows Performance Analyzer (WPA)  
- Tracy Profiler  
- Superluminal Profiler  
- Very Sleepy  
- Valgrind + Cachegrind  
- perf (Linux)  


# References

- ACTON, M. Data-oriented Design and C++. CppCon 2014. Available in [youtube](https://www.youtube.com/watch?v=rX0ItVEVjHc).  
- ROMEO, V. Implementation of a componented-based entity system in modern c++. CppCon 2015. Available in [youtube](https://www.youtube.com/watch?v=NTWSeQtHZ9M).  
- MORLAN, A. A simple entity component system (ecs). 2019. Available in https://austinmorlan.com/posts/entity_component_system/.  
- https://savas.ca/nomad
- https://tsprojectsblog.wordpress.com/portfolio/entity-component-system/
- https://github.com/skypjack/entt
- https://github.com/alecthomas/entityx
- https://www.youtube.com/watch?v=rX0ItVEVjHc
- https://people.freebsd.org/~lstewart/articles/cpumemory.pdf  
