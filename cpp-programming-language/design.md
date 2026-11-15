[Home](_cpp.md)  

# Design of C++

A linguagem C++ teve a sua origem no desenvolvimento do sistema operacional **UNIX** onde era necessário lidar diretamente com recursos de hardware, muitas vezes limitados e com alta demanda de desempenho. O uso eficiente de memória e operações de baixo nível são fundamentais para a programação de sistemas.  

Paralelamente, _Bjarne Stroustrup_, o criador de C++, buscava incorporar conceitos de alto nível por meio de mecanismos de abstração (_lightweight abstractions_), tendo a linguagem **Simula** como uma de suas grandes inspirações. A ideia era tornar possível expressar ideias diretamente através do código de forma simples e clara.

Utilizando a linguagem C como base e aplicando ideias de Simula, _Stroustrup_ conseguiu unir os dois ideais, resultando em uma linguagem de programação de propósito geral capaz de expressar ideias em código através do uso de **tipos definidos pelo usuário** sem comprometer a eficiência e o desempenho necessários para a programação de sistemas. A sua evolução ao longo dos anos permitiu que C++ fosse utilizado como uma síntese de diversos estilos de programação de forma elegante e eficiente.  

Hoje, C++ é utilizado desde sistemas embarcados até supercomputadores e disponível para a maioria dos sistemas operacionais.

Estes são as principais preocupações no design de C++:

- system programming  
- type system and compile-time checking  
- Abstraction Mechanism: user-defined types  
- mutability  
- resource management  
- expression of algorithms  
- error handling  
- modularity  

A linguagem C++ tem suporte direto a quatro tipos de estilos de programação:

- programação procedural  
- abstração de dados  
- programação orientada a objetos  
- programação genérica  

However, the emphasis is on the support of effective combinations of those. The best (most maintainable, most readable, smallest, fastest, etc.) solution to most nontrivial problems tends to be one that combines aspects of these styles.

**Classe** é o conceito chave para o mecanismo de abstração de C++. Todas as técnicas de programação como **abstração de dados (_data abstraction_)**, **programação orientada a objetos (_object-oriented programming_)** e **programação genérica** é possibilitada através do uso de classes. Just about anything that increases the flexibility or efficiency of classes improves the support of all of those styles. Thus, C++ could be (and has been) called class oriented.  

C++ has no built-in high-level data types and no high-level primitive operations. If a user wants such a type, it can be defined in the language itself. In fact, defining a new general-purpose or application-specific type is the most fundamental programming activity in C++. A well-designed user defined type differs from a built-in type only in the way it is defined, not in the way it is used. The C++ standard library provides many examples of such types and their uses. From a user's point of view, there is little difference between a built-in type and a type provided by the standard library.

Estes são os dois princípios importantes de C++:

> _"Leave no room for a lower-level language below C++ (except for assembly code in rare cases). If you can write more efficient code in a lower-level language, then that language will most likely become the systems programming language of choice."_ (Stroustrup, 2013).

> _"What you don't use you don't pay for. If programmers can hand-write reasonable code to simulate a language feature or a fundamental abstraction and provide even slightly better performance, someone will do so, and many will imitate. Therefore, a language feature and a fundamental abstraction must be designed not to waste a single byte, or a single processor cycle compared to equivalent alternatives. This is known as the zero-overhead principle."_ (Stroustrup, 2013).

> **Nota:** A partir da versão C++11, a linguagem ficou conhecida como **modern C++**. Foram introduzidos novos recursos que melhoraram a qualidade e desempenho de programas C++. Ainda é possível escrever código C++ de maneira antiga, mas estará perdendo uma oportunidade de criar código com mais qualidade.

C++ programming is based on strong static type checking, and most techniques aim at achieving a high level of abstraction and a direct representation of the programmer's ideas. This can usually be done without compromising run-time and space efficiency compared to lower-level techniques. To gain the benefits of C++, programmers coming to it from a different language must learn and internalize idiomatic C++ programming style and technique. The same applies to programmers used to earlier and less expressive versions of C++.

Thoughtlessly applying techniques effective in one language to another typically leads to awkward, poorly performing, and hard-to-maintain code. Such code is also most frustrating to write because every line of code and every compiler error message reminds the programmer that the language used differs from "the old language." You can write in the style of Fortran, C, Lisp, Java, etc., in any language, but doing so is neither pleasant nor economical in a language with a different
philosophy. Every language can be a fertile source of ideas about how to write C++ programs. However, ideas must be transformed into something that fits with the general structure and type system of C++ in order to be effective in C++. Over the basic type system of a language, only Pyrrhic victories are possible.


# System programming

The C++ fundamental (built-in) types, operators, and statements are those that computer hardware deals with directly: numbers, characters, and addresses. 

Thus, C++ is based on the idea of providing both
- direct mappings of built-in operations and types to hardware to provide efficient memory use and efficient low-level operations, and
- affordable and flexible abstraction mechanisms to provide user-defined types with the same notational support, range of uses, and performance as built-in types.

The design of C++ has focused on programming techniques dealing with fundamental notions such as memory, mutability, abstraction, resource management, expression of algorithms, error handling, and modularity. Those are the most important concerns of a systems programmer and more generally of programmers of resource-constrained and high-performance systems.

By systems programming I mean writing code that directly uses hardware resources, has serious resource constraints, or closely interacts with code that does. In particular, the implementation of software infrastructure (e.g., device drivers, communications stacks, virtual machines, operating systems, operations systems, programming environments, and foundation libraries) is mostly systems programming. The importance of the ‘‘bias toward systems programming’’ qualification in my long-standing characterization of C++ is that C++ has not been simplified (compromised) by ejecting the facilities aimed at the expert-level use of hardware and systems resources in the hope of making it more suitable for other application areas.

C++ was developed from the C programming language and, with few exceptions, retains C as a subset. The main reasons for relying on C were to build on a proven set of low-level language facilities and to be part of a technical community.

C++ is now more compatible with C than it was originally.

The definition of C++ has been revised to ensure that a construct that is both legal C and legal C++ has the same meaning in both languages.

One of the original aims for C was to replace assembly coding for the most demanding systems programming tasks. When C++ was designed, care was taken not to compromise the gains in this area. The difference between C and C++ is primarily in the degree of emphasis on types and structure. C is expressive and permissive. Through extensive use of the type system, C++ is even more expressive without loss of performance.

Programming in C encourages many techniques and tricks that are rendered unnecessary by C++ language features. For example, explicit type conversion (casting) is less frequently needed in C++ than it is in C (§1.3.3). However, good C programs tend to be C++ programs. For example, every program in Kernighan and Ritchie, The C Pro gramming Language, Second Edition [Kernighan,1988], is a C++ program. Experience with any statically typed language will be a help when learning C++.

C++ and its standard libraries are designed for portability. The current implementation will run on most systems that support C. C libraries can be used from a C++ program, and most tools that support programming in C can be used with C++.

C++’s support comes in the form of the built-in types, operators, statements, functions, structs, unions, etc. With minor exceptions, C is a subset of C++. Compared to C, C++ provides further support for procedural programming in the form of many additional language constructs and a stricter, more flexible, and more supportiv e type system.

C++ was designed to be used in a traditional compilation and run-time environment: the C programming environment on the UNIX system [UNIX,1985]. Fortunately, C++ was never restricted to UNIX; it simply used UNIX and C as a model for the relationships among language, libraries, compilers, linkers, execution environments, etc. That minimal model helped C++ to be successful on essentially every computing platform. There are, however, good reasons for using C++ in environments that provide significantly more run-time support. Facilities such as dynamic loading, incremental compilation, and a database of type definitions can be put to good use without affecting the language.

C++ supports systems programming. This implies that C++ code is able to effectively interoperate with software written in other languages on a system. The idea of writing all software in a single language is a fantasy. From the beginning, C++ was designed to interoperate simply and efficiently with C, assembler, and Fortran. By that, I meant that a C++, C, assembler, or Fortran function could call functions in the other languages without extra overhead or conversion of data structures passed among them.

Features that would incur run-time or memory overhead even when not used were avoided. For example, constructs that would make it necessary to store "housekeeping information" in every object were rejected, so if a user declares a structure consisting of two 16-bit quantities, that structure will fit into a 32-bit register. Except for the new, delete, typeid, dynamic_cast, and throw operators, and the try-block, individual C++ expressions and statements need no run-time support. This can be essential for embedded and high-performance applications. In particular, this implies that the C++ abstraction mechanisms are usable for embedded, high-performance, high-reliability, and real-time applications. So, programmers of such applications don’t have to work with a low-level (error-prone,   impoverished, and unproductive) set of language features.

You might suspect that specifying a program by using a more detailed type structure would increase the size of the program source text (or even the size of the generated code). With C++, this is not so. A C++ program declaring function argument types, using classes, etc., is typically a bit shorter than the equivalent C program not using these facilities. Where libraries are used, a C++ program will appear much shorter than its C equivalent, assuming, of course, that a functioning C equivalent could have been built.

C++ was designed to operate within a single address space. The use of multiple processes and multiple address spaces relied on (extralinguistic) operating system support. In particular, I assumed that a C++ programmer would have the operating systems command language available for composing processes into a system. Initially, I relied on the UNIX Shell for that, but just about any ‘‘scripting language’’ will do. Thus, C++ provided no support for multiple address spaces and no support for multiple processes, but it was used for systems relying on those features from the earliest days. C++ was designed to be part of large, concurrent, multilanguage systems.


# C++ type system and compile-time type checking

The language features and the type system are provided for the programmer to precisely and concisely represent a design in code.

The notion of **static types** and **compile-time type checking** is central to effective use of C++. The use of static types is key to expressiveness, maintainability, and performance. Following Simula, the design of **user-defined types** with interfaces that are checked at compile time is key to the expressiveness of C++. The C++ type system is extensible in nontrivial ways, aiming for equal support for built-in types and user-defined types.

C++ type-checking and data-hiding features rely on compile-time analysis of programs to prevent accidental corruption of data. They do not provide secrecy or protection against someone who is deliberately breaking the rules: C++ protects against accident, not against fraud. They can, however, be used freely without incurring run-time or space overheads. The idea is that to be useful, a language feature must not only be elegant, it must also be affordable in the context of a real-world program.

C++'s static type system is flexible, and the use of simple user-defined types implies little, if any overhead. The aim is to support a style of programming that represents distinct ideas as distinct types, rather than just using generalizations, such as integer, floating-point number, string, "raw memory," and "object," everywhere. A type-rich style of programming makes code more readable, maintainable, and analyzable. A trivial type system allows only trivial analysis, whereas a type-rich style of programming opens opportunities for nontrivial error detection and optimization. C++ compilers and development tools support such type-based analysis.

C++ provides much better facilities for type checking and for expressing modularity than C does.

Maintaining most of C as a subset and preserving the direct mapping to hardware needed for the most demanding low-level systems programming tasks implies the ability to break the static type system.

Tipos definidos pelo usuário (_user-defined types_) permite expressar conceitos e ideias diretamente no código que vão além de tipos fundamentais como ```int```, ```double```, etc. Por exemplo, uma declaração de uma variável do tipo ```double value;``` pode representar muitas coisas como distância, temperatura, etc. Agora o tipo definido pelo usuário como ```struct Meters { double value };``` torna o código mais expressivo.

A verificação de tipos em tempo de compilação (**compile-time type checking**) permite detectar diversos erros antes da execução do programa como:

- comportamentos indefinidos em conversão implícita de tipos (_type casting_)  
- chamadas de função com tipos de argumentos incompatíveis  
- verificação de tipos em templates  
- erros de interface de classes  
- tentativas de modificação de objetos com qualificador ```const```  
- permite chamadas de ```static_assert``` em tempo de compilação  
- concepts (C++20)  

Encontrar erros em tempo de compilação reduz o tempo de depuração do programa, torna o código mais confiável (_type-safe interface_) e mais fácil de manter.

O desempenho do programa também melhora pois evita verificação de tipos estáticos (incluindo tipos definidos pelo usuário) em tempo de execução - já que foi verificado em tempo de compilação. Além disso, os compiladores C++ possuem otimizações para tipos estáticos. Os tipos estáticos também são a base para o uso de templates em C++.


# Abstraction Mechanisms

**Classe** é o conceito chave para o mecanismo de abstração de C++. Uma classe é um **tipo definido pelo usuário (_user-defined type_)**.  

Classes provide data hiding, guaranteed initialization of data, implicit type conversion for user-defined types, dynamic typing, user-controlled memory management, and mechanisms for overloading operators.

Tipos definido pelo usuário bem projetados são utilizados da mesma maneira que tipos fundamentais (_built-in types_). Isto é, com a mesma notação, eficiência e segurança (verificação de tipos em tempo de compilação) de tipos fundamentais.

C++ fornece **abstração de dados** através do uso classes concretas e abstratas. Detalhes de implementação podem ser ocultos (_data hiding_) através do [controle de acesso] ```public``` e ```private```. Funções membros, construtores, destrutores e operadores sobrecarregados fornecem uma interface limpa para os objetos. E as classes abstratas fornecem interfaces que ocultam totalmente os dados da classe.

C++ oferece **programação orientada a objetos** atraves da hierarquia de classes (base and derived classes) e polimorfismo. C++ também oferece múltiplas heranças.

A **programação genérica** em C++ é alcanda através do uso de **template de função** e **template de classes**. Os tipos de templates são verificados em tempo de compilação.

Function declarations provide specific statically checked interfaces to member functions as well as freestanding functions, so they support all of the mentioned styles. They are necessary for overloading.

Inlining made the use of these facilities affordable in systems programming and for building run-time and space efficient libraries.

> **Nota:** _Stroustrup_ enfatiza que o conceito de classes em C++ não foi criada exclusivamente para a programação orientada a objetos. A linguagem C++ é uma síntese de diversos paradigmas de programação. Classe em C++ é o ponto central que suporta diversas técnicas de programação de forma combinada. A ideia é utilizar todo o potencial que a classe oferece em vez de utilizar apenas recursos específificos da linguagem de forma isolada.


# Move Semantics

The fundamental object in C++ has identity; that is, it is located in a specific location in memory and can be distinguished from other objects with (potentially) the same value by comparing addresses. Expressions denoting such objects are called lvalues (§6.4). However, even from the earliest days of C++’s ancestors [Barron,1963] there have also been objects without identity (objects for which an address cannot be safely stored for later use). In C++11, this notion of rvalue has been developed into a notion of a value that can be moved around cheaply. Such objects are the basis of techniques that resemble what is found in functional programming (where the notion of objects with identity is viewed with horror). This nicely complements the techniques and language features (e.g., lambda expressions) developed primarily for generic programming. It also solves classical problems related to "simple abstract data types," such as how to elegantly and efficiently return a large matrix from an operation (e.g., a matrix +).


# Modularity

C++'s emphasis on modularity, strongly typed interfaces, and flexibility pays off here. However, as programs get larger, the problems associated with their development and maintenance shift from being language problems to being more global problems of tools and management.  


# Resource Management

From the very earliest days, C++ programs and the design of C++ itself have been concerned about resource management. The ideal was (and is) for resource management to be

- simple (for implementers and especially for users),  
- general (a resource is anything that has to be acquired from somewhere and later released),  
- efficient (obey the zero-overhead principle; §1.2),  
- perfect (no leaks are acceptable), and  
- statically type-safe  

Many important C++ classes, such as the standard library’s vector, string, thread, mutex, unique_ptr, fstream, and regex, are resource handles. Foundation and application libraries beyond the standard provided many more examples, such as Matrix and Widget. The initial step in supporting the notion of resource handles was taken with the provision of constructors and destructors in the very first "C with Classes" draft. This was soon backed with the ability to control copy by defining assignment as well as copy constructors. The introduction of move constructors and move assignments (§3.3) in C++11 completes this line of thinking by allowing cheap movement of potentially large objects from scope to scope (§3.3.2) and to simply control the lifetime of polymorphic or shared objects (§5.2.1).

The facilities supporting resource management also benefit abstractions that are not resource handles. Any class that establishes and maintains an invariant relies on a subset of those features.

O princípio fundamental de C++ para lidar com gerenciamento de recursos é chamado de **Resource Acquisition Is Initialization (RAII)**.


# Effective C++

However, the emphasis is on the support of effective combinations of those. The best (most maintainable, most readable, smallest, fastest, etc.) solution to most nontrivial problems tends to be one that combines aspects of these styles.  


# Referências

- STROUSTRUP, B. The C++ programming language, 4th ed. Addison-Wesley, 2013.  
