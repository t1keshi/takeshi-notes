Previous: [Home](../README.md)  


# Computer Organization and Architecture
  
The study of computer organization focuses on this hierarchy and the issues involved with how to partition the levels and how each level is implemented.  

We must become familiar with how various circuits and components fit together to create working computer systems. We do this through the study of computer organization. Computer organization addresses issues such as control signals (how the computer is controlled), signaling methods, and memory types. It encompasses all physical aspects of computer systems. It helps us to answer the question: How does a computer work?  

The study of computer architecture focuses on the interface between hardware and software, and emphasizes the structure and behaviour of the system.  

The study of computer architecture focuses on the structure and behavior of the computer system and refers to the logical and abstract aspects of system implementation as seen by the programmer. Computer architecture includes many elements, such as instruction sets and formats, operation codes, data types, the number and types of registers, addressing modes, main memory access methods, and various I/O mechanisms. The architecture of a system directly affects the logical execution of programs. Studying computer architecture helps us to answer the question: How do I design a computer?  

# Pre-requistes

- Programming Language  
- Calculus or Discrete Mathematics  

A computer organization and architecture class is customarily a prerequisite for an undergraduate operating sustems class, compilers, networking, advanced architecture class.

# Por que estudar Organização e Arquitetura de Computadores?

There is a fundamental relationship between the computer hardware and the many aspects of programming and software components in computer systems. In order to write good software, it is very important to understand the computer system as a whole.

- Program optmization and system tuning  
- Entender erros misteriosos como "segmentation fault" ou "bus error"  
- Writing compilers (you must understand the particular hardware which you are compiling - e.g. pipelining can be adapted to compilation techniques)  
- To model large, complex, real-world systems (you must understand how floating-point arithmetc should work and how it does work)  
- To write device drivers for video, disks, or other I/O devices (you need a good understanding of I/O interfacing and computer architecture in general)  
- If you want to work on embedded systems (you must understand all of the time, space, and price trade-offs)  
- Benchmarking and how to present perfomance results adequately  

# Computer System

> **Principle of equivalence of hardware and software**: Any task done by software can also be done using hardware, and any operation performed directly by hardware can be done using software. What this principle does not address is the speed with which the equivalent tasks are carried out. Hardware implementations are almost always faster.

Um computador consiste em:

- Processor - Central Processing Unit (CPU)  
- Memory  
- Input and Output (I/O)   

### Processor - Central Processing Unit (CPU)

Um processador consiste em:

- Arithmetic Logic Unit (ALU)  
- Control Unit  
- Registers  

ALU é responsável pelos cálculos aritméticos e tomadas de decisão.  
Control Unit é responsável pelo direcionamento dos dados.  
Registrador é um armazenamento de dados especiais utilizado diretamente pela CPU.  

### Memory

A memória é responsável por armazenar dados e instruções de programas. Existem tipos diferentes de memória:

- long-term memory: disk drives and flash drivers (armazena dados até mesmo quando o computador está desligado)  
- temorary memory: registers and RAM (perde os dados quando o computador está desligado)  

Existe uma hierarquia entre os tipos de memória. O objetivo é conseguir o melhor desempenho pelo menor custo: memórias como SSD costumam ter uma capacidade maior de armazenamento e são mais baratos comparados a memória cache que tem uma capacidade menor de armazenamento. Entretanto, a CPU consegue acessar e gravar dados muito mais rapidamente em memória cache do que em memória do tipo SSD.

### System Bus

System Bus é responsável por conectar a unidade ALU, registradores e a memória através de um _pathway_ especial. The collection of ALU, registers, and bus is called a **datapath**, an extremely important component of any computer, because it is the hardware that is ultimately responsible for running programs.

### Input and Output (I/O)

Os componentes de entrada como teclado, mouse, camera, etc são responsáveis por obter dados externos para o computador.

Os componentes de saida como monitores, impressoras, caixa de som, etc são responsáveis por enviar os dados do computador para estes dispositivos externos.  


# Hierarchy of Virtual Machines

- low-level hardware  
- higher-level software (assemblers and operating systems)


# Instruction Set Architecture (ISA)

The computer architecture for a given machine is the combination of its hardware components plus its instruction set architecture (ISA). The ISA is the agreed-upon interface between all the software that runs on the machine and the hardware that executes it. The ISA allows you to talk to the machine.  


# References

- NULL, L. The essentials of computer organization and architecture. 6th ed. Burlington, Massachusetts: Jones & Bartlett Learning, 2024.  
