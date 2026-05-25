Previous: [Linux](linux.md)  


# Embedded Linux

- Linux supports a vast variety of hardware devices, probably more than any other OS
- Linux supports a huge variety of applications and networking protocols
- Linux is scalable, from small consumer-oriented devices to large, heavy-iron, carrier-class switches and routers
- Linux can be deployed without the royalties required by traditional proprietart embedded operating systems
- Linux has attracted a huge number of active developers, enabling rapid support of new hardware architectures, platforms, and devices
- An increasing number of hardware and software vendors, including virtually all the top-tier chip manufacturers and independent software vendors (ISV), now support Linux

Characteristics of an embedded system:

- Contains a processing engine, such as a general-purpose microprocessor.  
- Typically designed for a specific application or purpose.  
- Includes a simple (or no) user interface, such as an automotive engine ignition controller.  
- Often is resource-limited. For example, it might have a small memory footprint and no hard drive.  
- Might have power limitations, such as a requirement to operate from batteries.  
- Not typically used as a general-purpose computing platform.  
- Generally has application software built in, not user-selected.  
- Ships with all intended application hardware and software preintegrated.  
- Often is intended for applications without human intervention.   
- Frequently, the only user interface is a serial port and some LEDs.


# BIOS vs Bootloader

The BIOS first gains control of the processor when power is applied. Its primary responsibility is to initialize the hardware, especially the memory subsystem, and load an operating system from the PC's hard drive.

In a typical embedded system (assuming that it is not based on an industry standard x86 PC hardware platform), a bootloader is the software program that performs the equivalent functions. In your own custom embedded system, part of your development plan must include the development of a bootloader specific to your board. Luckily, several good open source bootloaders are available that you can customize for your project.

Here are some of the more important tasks your bootloader performs on power-up:

- Initializes critical hardware components, such as the SDRAM controller, I/O controllers, and graphics controllers.
- Initializes system memory in preparation for passing control to the operating system.
- Allocates system resources such as memory and interrupt circuits to peripheral controllers, as necessary.
- Provides a mechanism for locating and loading your operating system image.
- Loads and passes control to the operating system, passing any required startup information. This can include total memory size, clock rates, serial port speeds, and other low-level hardware-specific configuration data.


# Typical Anatomy of Embedded System

- processor (e.g. 32-bit RISC)
- flash memory for non volatile program and data storage
- main memory (e.g. SDRAM)
- real time clock module often backed up by battery keeps  the time of the day
- ethernet and usb interface
- serial port for console access via RS-232
- many processors contain integrated peripherals. Sometimes they are referred to as system on chip (SOC). 


# Typical Embedded Linux Setup

- host development system.  
- Embedded Linux target board is connected to the development host via an RS-232 serial cable.  
- Embedded Linux target board and development host system are connected to network via ethernet.  
- The development host contains your development tools and utilities along with target files, which normally are obtained from an embedded Linux distribution.  

Serial terminal program is used to communicate  with the target board:

- Minicom  
- screen  

When power is first applied, a bootloader supplied with your target board takes immediate control of the processor. It performs some very low-level hardware initialization, including processor and memory setup, initialization of the UART controlling the serial port, and initialization of the Ethernet controller. Example of bootloader: U-Boot. After initialization, bootloader waits for input from the console over the serial port.

All bootloaders have a command to load and execute an operating system image. Example of how to load Linux Kernel using U-Boot:

```
    => tftp 600000 uImage
    => tftp c00000 dtb
    => bootm 600000 - c00000
```

The tftp command instructs U-Boot to load the kernel image uImage into memory over the network using the TFTP protocol.
The kernel image, in this case, is located on the development workstation (usually the same machine that has the serial port connected to the target board).
The tftp command is passed an address that is the physical address in the target board's memory where the kernel image will be loaded.

The second invocation of the tftp command loads a board configuration file called a device tree. It is referred to by other names, including fl at device tree and device tree binary or dtb.
This file contains board-specific information that the kernel requires in order to boot the board. This includes things such as memory size, clock speeds, onboard devices, buses, and Flash layout.

Next, the bootm (boot from memory image) command is issued, to instruct U-Boot to boot the kernel we just loaded from the address specified by the tftp command.
In this example of using the bootm command, we instruct U-Boot to load the kernel that we put at 0x600000 and pass the device tree binary (dtb) we loaded at 0xc00000 to the kernel.
This command transfers control to the Linux kernel. 

Note that the bootm command is the death knell for U-Boot. This is an important concept. Unlike the BIOS in a desktop PC, most embedded systems are architected in such a way that when the Linux kernel takes control, the bootloader ceases to exist. The kernel claims any memory and system resources that the bootloader previously used. The only way to pass control back to the bootloader is to reboot the board.


# Kernel Initialization

Linux mounts a root file system (contains the application program, system libraries and utilities that make up a Linux system). Linux requires a file system.

A file system consists of a predefined set of system directories and files in a specific layout on a hard drive or other medium that the Linux kernel mounts as its root file system.

Note that Linux can mount a root file system from other devices. The most common, of course, is to mount a partition from a hard drive as the root file system, as is done on your Linux laptop or workstation. Indeed, NFS is pretty useless when you ship your embedded Linux widget out the door and away from your development environment. However, as you progress through this book, you will come to appreciate the power and flexibility of NFS root mounting as a development environment.

Until this point, the kernel itself was executing code, performing the numerous initialization steps in a context known as kernel context. In this operational state, the kernel owns all system memory and operates with full authority over all system resources. The kernel has access to all physical memory and to all I/O subsystems. It executes code in kernel virtual address space, using a stack created and owned by the kernel itself. When the Linux kernel has completed its internal initialization and mounted its root file system, the default behavior is to spawn an application program called init. When the kernel starts init, it is said to be running in user space or user space context. In this operational mode, the user space process has restricted access to the system and must use kernel system calls to request kernel services such as device and file I/O. These user space processes, or programs, operate in a virtual memory space picked at random and managed by the kernel. The kernel, in cooperation with specialized memorymanagement hardware in the processor, performs virtual-to-physical address translation for the user space process. The single biggest benefit of this architecture is that an error in one process can’t trash the memory space of another. This is a common pitfall in legacy embedded OSs that can lead to bugs that are some of the most difficult to
track down.


# References

- HALLINAN, C. Embedded Linux Primer: a practical, real-world approach. 2nd ed. Boston, MA: Prentice Hall, 2010.  
