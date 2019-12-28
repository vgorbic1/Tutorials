## Operating Systems

### Single-user Machines (Elevator operator)
- Hardware executes a single program, which has access to all hardware resources
in the machine. 
- The instruction set architecture (ISA) is the interface between software and
hardware.

### Computer Systems (Laptop)
- Multiple executing programs running on the same machine, which do hot have
direct access to all hardware resources.
- Operating system (OS) interposes between programs and hardware.
- OS talks to hardware through ISA
- OS talks to programs through application binary interface (ABI).

### Nomenclature
- **Program** is the code or collection of instructions.
- **Process** is a program that is being executed.
- **OS Kernel** is a process with special privileges.

### Goals of OS
- **Protection** and privacy. Processes cannot access each other's data.
- **Abstraction** OS hides details of underlying hardware.
- **Resource Management** OS controls how processes share hardware. 

### The Big Picture (Most abstract level)
- **Private address space** in memory provided to each process by OS.
- **Scheduling** processes in CPU by OS, giving a fraction of CPU time to
each process.
- **System calls** allowed to processes by OS to invoke system services: acess files
or network sockets.

### Virtual Machines (VM)
The OS Kernel gives a **virtual machine* to each process, so the process "believes" that it runs
on its own (physical) hardware, but VS is just an abstraction.
