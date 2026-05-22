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


# References

- HALLINAN, C. Embedded Linux Primer: a practical, real-world approach. 2nd ed. Boston, MA: Prentice Hall, 2010.  
