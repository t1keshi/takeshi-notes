[Home](_cpp.md)  


# C++ Design

A linguagem de programação C++ teve a sua origem em programação de sistemas onde era essencial lidar com noções fundamentais como memória, mutabilidade, abstração, gerenciamento de recursos, expressão de algoritmos, tratamento de erros e modularidade. Estes fatores são importantes para programadores que trabalham em ambientes com recursos limitados e alta demanda de desempenho.

Ao mesmo tempo, _Stroustrup_ buscava incorporar conceitos de alto nível como mecanismos de abstração (_lightweight abstractions_). A linguagem **Simula** serviu de grande inspiração para cumprir este objetivo.

Estes são os conceitos fundamentais da linguagem C++:

- ser uma linguagem de programação de propósito geral (suporte para uma grande variedade de usos)
- mapeamento direto de operações de baixo nível e tipos de dados utilizados pelo hardware (uso eficiente da memória e instruções de baixo nível)  
- possuir mecanismos de abstração como **tipos definidos pelo usuário** (_user-defined types_) 
- suporte a diversas técnicas de programação mas com objetivo de serem utilizadas de forma combinada e não isoladamente  

O conceito chave de C++ para alcançar estes objetivos é a **classe**. A classe é um tipo definido pelo usuário (_user-defined type_) que permite a aplicação de diversas técnicas de programação como:

- programação procedural  
- abstração de dados  
- programação orientada a objetos  
- programação genérica  

However, the emphasis is on the support of effective combinations of those. The best (most maintainable, most readable, smallest, fastest, etc.) solution to most nontrivial problems tends to be one that combines aspects of these styles. Each of these styles of design and programming has contributed to the synthesis that is C++.

Just about anything that increases the flexibility or efficiency of classes improves the support of all of those styles. Thus, C++ could be (and has been) called class oriented.

# Tipos definidos pelo usuário

Tipos definidos pelo usuário (_user-defined types_) permite que os objetos destes tipos possam ser utilizados da mesma maneira que os tipos fundamentais (_built-in types_) de forma eficiente e segura como, por exemplo, aproveitando o benefício de verificação de tipos em tempo de compilação.

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
