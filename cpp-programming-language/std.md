Previous: [C++ Programming Language](_cpp.md)  

# The C++ Standard Library

If the standard library provides a component that addresses a problem, it is almost always better to use that component than to build your own. Even if the standard component is arguably slightly inferior to a home-built component for a particular problem, the standard component is likely to be more widely applicable, more widely available, and more widely known. Over the longer term, the standard component (possibly accessed through a convenient custom interface) is likely to lower long-term maintenance, porting, tuning, and education costs.

Except for a few unfortunate and unimportant historical accidents, the C++ standard library is written in C++. Writing the C++ standard library in C++ is a crucial test of the C++ type system and abstraction mechanisms: they must be (and are) sufficiently powerful (expressive) and efficient (affordable) for the most demanding systems programming tasks. This ensures that they can be used in large systems that typically consist of layer upon layer of abstraction.

_"The standard library itself is also a fertile source of programming examples and design techniques."_ (Stroustrup, 2013).  
_"The standard library is the repository of much hard-earned knowledge of how to use C++ well."_ (Stroustrup, 2013).  

- Standard library headers  
- Standard Template Library (STL)  
    - Containers (hash tables)  
    - Iterators (reverse_iterator, move_iterator, function)  
    - Algorithms (find(), sort(), merge())  
- Strings (character traits that are basis for the use of different character sets)  
- Vectors  
- Map  
- Unordered Map  
- I/O streams: It describes formatted and unformatted input and output, error handling, and buffering.
- Memory and Resources (array, bitset, pair, tuple, unique_ptr, shared_ptr, allocators, garbage collector interface)  
- Utilities: time, type traits, and various type functions  
- Regular expressions: regular expression syntax and the various ways of using it for string matching, including regex_match() for matching a complete string, regex_search() for finding a pattern in a string, regex_replace() for simple replacement, and regex_iterator for general traversal of a stream of characters
- Locales describes class locale and its various facets that provide support for the handling of cultural differences in character sets, formatting of numeric values, formatting of date and time, and more.
- Numerics describes facilities for numerical computation (such as complex, valarray, random numbers, and generalized numerical algorithms).
- Concurrency presents the C++ basic memory model and the facilities offered for concurrent programming without locks.
- Threads and Tasks presents the classes providing threads-and-locks-style concurrent programming (such as thread, timed_mutex, lock_guard, and try_lock()) and the support for task-based concurrency (such as future and async()).
- The C Standard Library documents the C standard library (including printf() and clock()) as incorporated into the C++ standard library.


# References

- STROUSTRUP, B. The C++ programming language, 4th ed. Addison-Wesley, 2013.  
