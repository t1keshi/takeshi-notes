[Home](_cpp.md)  


# C++ Design

A linguagem C++ teve a sua origem em programação de sistemas onde era fundamental lidar eficientemente com memória, mutabilidade, abstração, gerenciamento de recursos, expressão de algoritmos, tratamento de erros e modularidade. Estes fatores eram cruciais para programadores que trabalhavam em ambientes com recursos limitados e alta demanda de desempenho.

Ao mesmo tempo, _Stroustrup_ buscava incorporar conceitos de alto nível como mecanismos de abstração para a criação de **tipos definidos pelo usuário**. A linguagem **SIMULA** serviu de grande inspiração para cumprir este objetivo. Classe é o conceito-chave em C++ que permite ao usuário criar um novo tipo de dados.

A definição de um novo tipo pelo usuário permite utilizá-lo em expressões da mesma maneira como tipos predefinidos (_built-in types_) de forma eficiente e segura como, por exemplo, aproveitando o benefício de checagens de tipos em tempo de compilação.

Em C++, a classe possui diversos mecanismos que permitem a aplicação de diversas técnicas de programação de forma combinada:

- programação procedural  
- abstração de dados  
- programação orientada a objetos  
- programação genérica  


# C++ is statically typed language

Um dos pilares fundamental da linguagem C++ é ser uma linguagem estaticamente tipada.

- _compile-time checking_ - permite a checagem de tipos em tempo de compilação, detectando erros antes da execução do programa C++  
- evita comportamentos indefinidos que podem ocorrer como, por exemplo, em conversões indevidas de tipos durante a execução do programa C++  
- melhora o desempenho do programa C++ pois evita checagem de tipos em tempo de execução  
- permite otimizações do compiladores em tipos estáticos  
- aumenta a confiabilidade e segurança (_type-safe interface_) do programa C++  
- tipos estáticos é base para o uso de templates em C++  


# Referências

- STROUSTRUP, B. The C++ programming language, 4th ed. Addison-Wesley, 2013.  
