[Home](_opengl.md)

# OpenGL History

# Versão 1.0

A primeira versão de OpenGL 1.0 foi lançada em 30 de junho de 1992 pela **Silicon Graphics Computer Systems**.

- A pipeline de renderização não era programável nesta versão (fixed-function pipeline).  
- Suporte para especificação de matrizes de transformação (```GL_MODELVIEW``` e ```GL_PROJECTION```).  

# Versão 2.0

A versão 2.0 foi lançada em 7 de setembro de 2004.

- Introdução de shaders programáveis e da linguagem de programação de shaders GLSL (OpenGL Shading Language).  
- OpenGL Architecture Review Board (ARB) foi transferido para Khronos Group (2006).  
- Each of piece of vertex information had a specific channel in the pipeline (```glVertex```, ```glTexCoord```, and ```glNormal```) or client vertex arrays using ```glVertexPointer```, glTexCoordPointer```, or ```glNormal```.  
- The shader would then access these value via built-in variables such as ```gl_Vertex``` and ```gl_Normal```.

# Versão 3.0

A versão 3.0 foi lançada em 11 de agosto de 2008.

- Introdução de modelo de depreciação (_deprecation model_).  
- Introdução de um novo mecanismo de criação de contextos.  
- A abordagem "immediate mode" foi marcada como deprecado.
- Comandos como ```glVertex```, ```glTexCoord```, ```glVertexPointer```, etc foram marcados como deprecados.  
- Inclusão da extensão ```ARB_compatibility```.  

# Versão 3.1

A versão 3.1 foi lançada em 24 de março de 2009.

- Remoção de funcionalidades que foram marcadas como deprecados na versão 3.0.  
- Remoção da abordagem "immediate mode".  


# Versão 4.0

A versão 4.0 foi lançada em 11 de março de 2010.

- Introdução do estágio **tesselation** na pipeline de renderização.  
- Introdução de **Transform Feedback Objects**


# Referências

- KESSENICH, J. et al. OpenGL Programming Guide: the official guide to learning OpenGL, versions 4.5. 9th ed. Boston: Pearson Education, 2017.
- WOLFF, D. OpenGL 4 Shading Language Cookbook. 3rd ed. Birmingham: Packt Publishing, 2018.
- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.  
- Fixed Function Pipeline. Disponível em [https://www.khronos.org/opengl/wiki/Fixed_Function_Pipeline](https://www.khronos.org/opengl/wiki/Fixed_Function_Pipeline).
