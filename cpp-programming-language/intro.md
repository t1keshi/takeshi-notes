Previous: [Table of Contents](_cpp.md)

# Introduction

Este texto tem como objetivo ser uma referência completa sobre a linguagem de programação C++. Todo conteúdo foi escrito com base na minha experiência com o uso da linguagem, especificação C++, livros, artigos e materiais acadêmicos relacionados à C++.

Segundo o seu criador, [_Bjarne Stroustrup_](https://www.stroustrup.com/), a linguagem C++ é definida da seguinte forma:

> _"C++ is a general-purpose programming language providing a direct and efficient model of hardware combined with facilities for defining lightweight abstractions."_ (Stroustrup, 2013).

E ela atende a dois princípios importantes:

> _"Leave no room for a lower-level language below C++ (except for assembly code in rare cases). If you can write more efficient code in a lower-level language, then that language will most likely become the systems programming language of choice."_ (Stroustrup, 2013).

> _"What you don't use you don't pay for. If programmers can hand-write reasonable code to simulate a language feature or a fundamental abstraction and provide even slightly better performance, someone will do so, and many will imitate. Therefore, a language feature and a fundamental abstraction must be designed not to waste a single byte, or a single processor cycle compared to equivalent alternatives. This is known as the zero-overhead principle."_ (Stroustrup, 2013).

A linguagem é padronizada pela *International Organization for Standardization* (ISO) e a sua versão atual é a **C++23 (ISO/IEC 14882:2024(E))**. A especificação pode ser encontrada em [https://webstore.ansi.org/](https://webstore.ansi.org/).

A especificação é utilizada por implementadores de compiladores para garantir que o mesmo código C++ funcione em diferentes plataformas. Entretanto, devido a variedade de hardwares e sistemas operacionais, o comportamento pode variar dependendo do tipo da plataforma. A existência da especificação também significa estabilidade - o código escrito hoje funcionará por várias décadas.

Para obter mais informações a respeito do desenvolvimento da especificação da linguagem C++, basta acessar: [https://isocpp.org](https://isocpp.org).

> **Nota**: Até o momento da escrita deste texto, a versão C++26 está em desenvolvimento.

Segue a lista de versões da especificação de C++:

- INCITS/ISO/IEC 14882:1998 (C++98)
- INCITS/ISO/IEC 14882-2003 (C++03)
- ISO/IEC 14882:2011 (C++11 ou C++0x)
- INCITS/ISO/IEC 14882:2014 (C++14 ou C++1y)
- INCITS/ISO/IEC 14882:2017 (C++17 ou C++1z)
- ISO/IEC 14882:2020 (C++20 ou C++2a)
- ISO/IEC 14882:2024(E)

> **Nota:**  A linguagem **C++03** é essencialmente a mesmo que **C++98**. Ela contém apenas "bug fixes".

Outro recurso online muito útil para referência pode ser encontrado em [https://en.cppreference.com/w/cpp](https://en.cppreference.com/w/cpp).

A melhor forma de aprender a linguagem é realizar os seus próprios experimentos. Consulte com frequência a documentação, faça alterações nos exemplos e veja os efeitos destas alterações. Além disso, configure as opções do compilador para exibir todos os avisos. Estude cada mensagem gerada pelo compilador e elimine os avisos. Testar o seu código em múltiplas plataformas e compiladores também é uma boa prática para melhorar a portabilidade do seu código e aprender as diferenças entre diversas plataformas.

> _"C++ rewards the programmer who takes the time to master techniques for writing quality code."_ (Stroustrup, 2013).

# Referências

- STROUSTRUP, B. The C++ programming language, 4th ed. Addison-Wesley, 2013.