Previous: [Linux](linux.md)  


# The Linux Programming Interface

In this book, I describe the Linux programming interface—the system calls, library functions, and other low-level interfaces provided by Linux, a free implementation of the UNIX operating system. These interfaces are used, directly or indirectly, by every program that runs on Linux. They allow applications to perform tasks such as file I/O, creating and deleting files and directories, creating new processes, executing programs, setting timers, communicating between processes and threads on the same computer, and communicating between processes residing on different computers connected via a network. This set of low-level interfaces is sometimes also known as the system programming interface.


# Portable Operationg System Interface (POSIX)

POSIX é um padrão que define uma interface comum para sistemas Unix e Unix-like. Um programa POSIX deve funcionar tanto em um Unix, MacOS (baseado em Unix) e em Linux (Unix-like).

Padrões de POSIX:

- processos
- threads
- arquivos
- sinais
- shell
- permissões
- chamadas de sistema
- APIs em C


# Programming features that are specific to Linux

- epoll, a mechanism for obtaining notification of file I/O events;
- inotify, a mechanism for monitoring changes in files and directories;
- capabilities, a mechanism for granting a process a subset of the powers of the superuser;
- extended attributes;
- i-node flags;
- the clone() system call;
- the /proc file system; and
- Linux-specific details of the implementation of file I/O, signals, timers, threads, shared libraries, interprocess communication, and sockets.


# Reference  

- KERRISK, M. The Linux programming interface: a linux and UNIX system programming handbook. San Francisco: no starch press, 2010.
