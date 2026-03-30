Previous: [win32 programming](win32.md)

# Debugging with Visual Studio

Execute em modo Debug:

```
    #define _CRTDBG_MAP_ALLOC
    #include <cstdlib>
    #include <crtdbg.h>

    ...

    int main() {
        _CrtSetDbgFlag(_CRTDBG_ALLOC_MEM_DF | _CRTDBG_LEAK_CHECK_DF);
        return 0;
    }
```

Forçar o dump em algum ponto específico.

```
    _CrtDumpMemoryLeaks();
```


# References

- https://learn.microsoft.com/en-us/cpp/c-runtime-library/reference/crtsetdbgflag?view=msvc-170  
- https://learn.microsoft.com/pt-br/cpp/c-runtime-library/reference/crtdumpmemoryleaks?view=msvc-170  
