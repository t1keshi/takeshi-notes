[Home](_cpp.md)  


# C++ Design

A linguagem de programação C++ teve a sua origem em programação de sistemas onde era essencial lidar com ambientes com recursos limitados e alta demanda de desempenho.

Ao mesmo tempo, _Stroustrup_ buscava incorporar conceitos de alto nível na linguagem através de implementação de mecanismos de abstração (_lightweight abstractions_). A linguagem **Simula** serviu de grande inspiração para cumprir este objetivo. O objetivo era poder representar conceitos e ideias diretamente através de código sem comprometer a eficiência e o desempenho necessário para trabalhar com programação de sistemas.  

**Classe** é o conceito chave para o mecanismo de abstração da linguagem C++. Todas as técnicas de programação como **abstração de dados**, **programação orientada a objetos** e **programação genérica** é possibilitada através do uso de classes.  

> **Nota:** _Stroustrup_ enfatiza que o conceito de classes em C++ não foi criada exclusivamente para a programação orientada a objetos. A linguagem C++ é uma síntese de diversos paradigmas de programação. Classe em C++ é o ponto central que suporta diversas técnicas de programação de forma combinada. A ideia é utilizar todo o potencial que a classe oferece em vez de utilizar apenas recursos específificos da linguagem de forma isolada.

Estes são os pontos fundamentais da linguagem C++:

- ser uma linguagem de programação de propósito geral  
- mapeamento direto de tipos de dados e operações de baixo nível utilizados pelo hardware (uso eficiente da memória e instruções de baixo nível)  
- possuir mecanismos de abstração (_lightweight abstractions_) como **tipos definidos pelo usuário** (_user-defined types_) 
- suporte a diversas técnicas de programação mas com objetivo de serem utilizados de forma combinada e não isoladamente  


# Abstraction Mechanisms

Abstraction Mechanisms presents the language features supporting data abstraction, object-oriented programming, and generic programming.

Tipos definidos pelo usuário (_user-defined types_) permite que os objetos destes tipos possam ser utilizados da mesma maneira que os tipos fundamentais (_built-in types_) de forma eficiente e segura como, por exemplo, aproveitando o benefício de verificação de tipos em tempo de compilação.


# C++ is statically typed language

The notion of static types and compile-time type checking is central to effective use of C++. The use of static types is key to expressiveness, maintainability, and performance.

The language features and the type system are provided for the programmer to precisely and concisely represent a design in code.

Following Simula, the design of user-defined types with interfaces that are checked at compile time is key to the expressiveness of C++. The C++ type system is extensible in nontrivial ways, aiming for equal support for built-in types and user-defined types.

C++ type-checking and data-hiding features rely on compile-time analysis of programs to prevent accidental corruption of data. They do not provide secrecy or protection against someone who is deliberately breaking the rules: C++ protects against accident, not against fraud. They can, however, be used freely without incurring run-time or space overheads. The idea is that to be useful, a language feature must not only be elegant, it must also be affordable in the context of a real-world program.

C++'s static type system is flexible, and the use of simple user-defined types implies little, if any overhead. The aim is to support a style of programming that represents distinct ideas as distinct types, rather than just using generalizations, such as integer, floating-point number, string, "raw memory," and "object," everywhere. A type-rich style of programming makes code more readable, maintainable, and analyzable. A trivial type system allows only trivial analysis, whereas a type-rich style of programming opens opportunities for nontrivial error detection and optimization. C++ compilers and development tools support such type-based analysis.

Maintaining most of C as a subset and preserving the direct mapping to hardware needed for the most demanding low-level systems programming tasks implies the ability to break the static type system.

- _compile-time checking_ - permite a checagem de tipos em tempo de compilação, detectando erros antes da execução do programa C++  
- verificação de tipos em tempo de compilação é a chave de expressividade em C++  
- evita comportamentos indefinidos que podem ocorrer como, por exemplo, em conversões indevidas de tipos durante a execução do programa C++  
- melhora o desempenho do programa C++ pois evita checagem de tipos em tempo de execução  
- permite otimizações do compiladores em tipos estáticos  
- aumenta a confiabilidade e segurança (_type-safe interface_) do programa C++  
- tipos estáticos é base para o uso de templates em C++  
- tipos definidos pelo usuário também possuem a segurança de verificação de tipos em tempo de compilação.  
- o sistema de tipos de C++ permite que tipos definidos pelo usuário sejam extensíveis e utilizados da mesma forma que tipos fundamentais  


# Conceito de move semantics

The fundamental object in C++ has identity; that is, it is located in a specific location in memory and can be distinguished from other objects with (potentially) the same value by comparing addresses. Expressions denoting such objects are called lvalues (§6.4). However, even from the earliest days of C++’s ancestors [Barron,1963] there have also been objects without identity (objects for which an address cannot be safely stored for later use). In C++11, this notion of rvalue has been developed into a notion of a value that can be moved around cheaply. Such objects are the basis of techniques that resemble what is found in functional programming (where the notion of objects with identity is viewed with horror). This nicely complements the techniques and language features (e.g., lambda expressions) developed primarily for generic programming. It also solves classical problems related to "simple abstract data types," such as how to elegantly and efficiently return a large matrix from an operation (e.g., a matrix +).


# Resouce Management

- Resource Acquisition is Initialization (RAII) technique  
- Construction, Cleanup, Copy, and Move
- simple, general, efficiente (zero-overhead principle), perfect (no leaks are acceptable), statically tyoe safe  


# Referências

- STROUSTRUP, B. The C++ programming language, 4th ed. Addison-Wesley, 2013.  
