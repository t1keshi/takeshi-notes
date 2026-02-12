[Home](_cpp.md)  

# Function Objects (Functor)

Function objects (functor) é um objeto que pode ser utilizado como função:

```
    template<typename T>
    class LessThan {
    public:
        LessThan(const T& v) : value(v)  {}
        bool operator()(const T& x) const { return x < val; }

    private:
        const T value;
    }
```

Exemplos de uso:

```
    // 1. Em escopo local
    LessThan<double> a{ 50.0 };
    if(a(100.0)) // compara 100.0 < 50.0

    // 2. Em funções
    template<typename T>
    bool foo(T func) {
        return func(100);
    }

    foo(LessThan<int>{100});
```

Functors são bastante utilizados como argumentos em algoritmos de Standard Library.

Vantagens:

- Functor podem ter membros de dados  
- Generalizados com templates  
- O operador() pode ser **inline**  eliminado overhead de chamada de função   

# Lambda expression

A notação [](){} chamada **lambda expression** gera um functor sem a necessodade de declarar uma classe e sobrecarga de operador().

```
    // expressão anterior
    foo(LessThan<int>{100});

    // expressão lambda
    int val = 50;
    foo([=](int x){ return x < val>});
```

[] é um **capture list** que passa as variáveis locais para as expressões.

- [=] passa as variáveis locais por cópia  
- [&] passa as variáveis locais por referência  
- [] não passa variáveis locais  
- [=val] passa somente a variável ```val``` por cópia   
- [&val] passa somente a variável ```val``` por referência     


# Referências

- STROUSTRUP, B. The C++ programming language, 4th ed. Addison-Wesley, 2013.  
