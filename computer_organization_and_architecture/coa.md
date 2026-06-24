Previous: [Home](../README.md)  


# Computer Organization and Architecture

The study of computer organization focuses on this hierarchy and the issues involved with how to partition the levels and how each level is implemented.  

We must become familiar with how various circuits and components fit together to create working computer systems. We do this through the study of computer organization. Computer organization addresses issues such as control signals (how the computer is controlled), signaling methods, and memory types. It encompasses all physical aspects of computer systems. It helps us to answer the question: How does a computer work?  

The study of computer architecture focuses on the interface between hardware and software, and emphasizes the structure and behaviour of the system.  

The study of computer architecture focuses on the structure and behavior of the computer system and refers to the logical and abstract aspects of system implementation as seen by the programmer. Computer architecture includes many elements, such as instruction sets and formats, operation codes, data types, the number and types of registers, addressing modes, main memory access methods, and various I/O mechanisms. The architecture of a system directly affects the logical execution of programs. Studying computer architecture helps us to answer the question: How do I design a computer?  

#### Por que estudar Organização e Arquitetura de Computadores?

There is a fundamental relationship between the computer hardware and the many aspects of programming and software components in computer systems. In order to write good software, it is very important to understand the computer system as a whole.

- Program optmization and system tuning  
- Entender erros misteriosos como "segmentation fault" ou "bus error"  
- Writing compilers (you must understand the particular hardware which you are compiling - e.g. pipelining can be adapted to compilation techniques)  
- To model large, complex, real-world systems (you must understand how floating-point arithmetc should work and how it does work)  
- To write device drivers for video, disks, or other I/O devices (you need a good understanding of I/O interfacing and computer architecture in general)  
- If you want to work on embedded systems (you must understand all of the time, space, and price trade-offs)  
- Benchmarking and how to present perfomance results adequately  


# Pre-requistes

- Programming Language  
- Calculus or Discrete Mathematics  

A computer organization and architecture class is customarily a prerequisite for an undergraduate operating sustems class, compilers, networking, advanced architecture class.

# Computer System

Principle of equivalence of hardware and software: Any task done by software can also be done using hardware, and any operation performed directly by hardware can be done using software. What this principle does not address is the speed with which the equivalent tasks are carried out. Hardware implementations are almost always faster.

The principle of equivalence of hardware and software tells us that we have a choice; any task performed directly in hardware can be done using software, and anything done using hardware can be simulated using software. Our knowledge of computer organization and architecture will help us to make the best choice and allow us to minimize cost and size while maximizing performance, resulting in a perfect combination of hardware and software.

At the most basic level, a computer is a device consisting of three pieces:

1. A processor (CPU, or central processing unit) to interpret and execute programs
2. A memory to store both data and programs
3. A mechanism for transferring data to and from the outside world

A processor consists of an arithmetic logic unit (ALU, to perform computations and make decisions) and a control unit (to act as a "traffic police officer" directing data to correct locations). It also contains very special storage locations called registers; these registers hold data that the CPU needs to access very quickly.

When a program is running, the CPU executes instructions found in memory. Memory is used to store anything that the computer needs. There are two types of memory: (1) long-term memory, such as disk drives and flash drives, which stores data even when the power is off; and (2) temporary memory, which loses data when it loses power, and includes registers and RAM.

Typically, memory is "hierarchical," meaning that there are different levels of memory, varying in size and speed. The goal of this memory hierarchy is to give the best performance at the lowest cost. For example, a hard drive provides a large, inexpensive place to store long-term data, whereas cache is a small, but fast and expensive type of memory that stores data being used most often. By accessing the cache, the CPU can read and write data quickly without bogging down the entire system.

The ALU must be connected to the registers, and both must be connected to the memory; this is done by a special pathway called a bus. The collection of ALU, registers, and bus is called a datapath, an extremely important component of any computer, because it is the hardware that is ultimately responsible for running programs.

A computer would do us no good if we couldn't give it information and get results in return. Input/output components, such as keyboards, mice, monitors, printers, web cameras, scanners, graphics tablets, and thumb drives, are all examples of devices that allow us to communicate with the computer.

# Hierarchy of Virtual Machines

- low-level hardware  
- higher-level software (assemblers and operating systems)


# Instruction Set Architecture (ISA)

The computer architecture for a given machine is the combination of its hardware components plus its instruction set architecture (ISA). The ISA is the agreed-upon interface between all the software that runs on the machine and the hardware that executes it. The ISA allows you to talk to the machine.  


# References

- NULL, L. The essentials of computer organization and architecture. 6th ed. Burlington, Massachusetts: Jones & Bartlett Learning, 2024.  
