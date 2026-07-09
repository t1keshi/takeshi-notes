[Home](_cpp.md)

# Classes

- Classes: The notion of a user-defined type, a class, is the foundation of all C++ abstraction mechanisms.  
- Construction, Cleanup, Copy, and Move shows how a programmer can define the meaning of creation and initialization of objects of a class. Further, the meaning of copy, move, and destruction can be specified  
- Operator Overloading presents the rules for giving meaning to operators for user-defined types with an emphasis on conventional arithmetic and logical operators, such as +, ∗, and &.  
-  Special Operators discusses the use of user-defined operator for non-arithmetic purposes, such as [] for subscripting, () for function objects, and −> for "smart
pointers."  
- Derived Classes presents the basic language facilities for building hierarchies out of classes and the fundamental ways of using them. We can provide complete
separation between an interface (an abstract class) and its implementations (derived classes); the connection between them is provided by virtual functions. The C++ model for access control (public, protected, and private) is presented.  
- Class Hierarchies discusses ways of using class hierarchies effectively. It also presents the notion of multiple inheritance, that is, a class having more than one direct base class.  
- Run-Time Type Information presents ways to navigate class hierarchies using data stored in objects. We can use dynamic_cast to inquire whether an object of a base class was defined as an object of a derived class and use the typeid to gain minimal information from an object (such as the name of its class).  

??
"A class is a user-defined type provided to represent a concept in the code of a program."

# Classes concretas

Uma **classe concreta** possui a sua representação como parte de sua definição. Ela pode ser utilizada em expressões da mesma maneira como objetos de tipos predefinido (_built-in type_) de forma eficiente e segura.

Objetos de classes concretas podem:

- ser instaciados na stack, memória estática e em outros objetos  
- ser utilizados diretamente sem ponteiros e referências   
- ser copiados  
- podem ser inicializados imediamtamente e de forma completa (construtores) 

"The representation can be private (as it is for Vector; §2.3.2) and accessible only through the member functions, but it is present."

"To increase flexibility, a concrete type can keep major parts of its representation on the free store (dynamic memory, heap) and access them through the part stored in the class object itself."


# Referências

- STROUSTRUP, B. The C++ programming language, 4th ed. Addison-Wesley, 2013.  
