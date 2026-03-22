[Home](_cpp.md)  

# Smart Pointer [under construction]

# ```std::unique_ptr<TYPE>```

```
    #include <memory>
    std::unique_ptr<TYPE> myPtr = std::make_unique<TYPE>();
```

- chama o delete implicitamente quando é destruído
- chama o delete explicitamente com o método ```reset```
- std::unique_ptr não deve ser utilizado caso não quer que o ponteiro seja destruído

# std::unique_ptr para substituir arrays []

```
    std::unique_ptr<float[]> myArray;
    myArray = std::make_unique<float[]>(1000);
```

# Referências