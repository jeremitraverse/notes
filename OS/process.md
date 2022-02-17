
In a *time sharing* OS, a process is a job/program loaded in memory 
from the job pool. If there's not enough space in memory for all the
jobs in the job pool, the system, job scheduling, has to take a decision.

Timer is used to prevent a user program from running too long.


## Operating System Structure (Chapt 2)

### Dual mode
Kernel vs user mode is simply a bit set at the hardware level.

### System calls
System calls provides the means for a user program to ask the OS to 
perform tasks reserved for the OS on the user program's behalf.

#### Command Interpreter
Piece of software that enable the user to directly enter commands to
be performed by the OS

#### API's
API that invokes the actual system call on behalf of the programmer used
within a System Call Interface
Pros:
  1. Program protability. Dev can expect the program to compile and run 
  on each on any system that support the same API.
  2. System calls can often be more difficult to work with then the API

### Design
Must define goals, specifications and requirements.
Must take in consideration the choice of hardware and type of system.

#### Layered approach
OS is broken into multiple layers making it modular and easier to debug
Needs a lot of planning ahead and less efficient

### Microkernel
Removing non-essential components from the kernel and implementing them
as system and user-level program.
- Provides minimal process and memory management 
- Kernal acts as a communication facility between the client program and
various services running on the user space.

### Interrupts
CPU hardware has a wire called the interrupt-request line that the CPU
senses after executing every instruction. When CPU detects that a
controller has asserted a signal on the interrupt-request line, the CPU
the CPU perform a state save and jumps to the interrupt-handler routine.

Two request lines:
1. nonmaskable interrupts
2. maskable interrupts

An interrupts cause the OS to change a CPU from its current task and to
run a kernel routine. The previous current task's context is saved into 
the PCB


# Processes
A process is a program in executing state. Only one process can be
*running* on a processor core at the same time if they are single 
threaded.

Objective of multiprogramming is to have some process running at all
time to maximize CPU utilization hence the need of a Process Scheduler.

#### Schedulers
1. Long-term scheduler:
  - Loads processes from the job pool into memory (from New to Ready)
  - Controls the degree of multiprogramming (nb of processes in memory)
  - Doesn't care much about the speed
  - CPU-bound process makes high I/O and low amount of calculation
  - In time sharing systems long-term scheduler doesn't exists or minimal
  every processes are put in memory
2. Short-term scheduler:
  - Change status from Ready to Running
  - Must be fast 
  - CPU-bound process makes low I/O and high amount of calculation
3. Medium-term scheduler
  - Can be avantageous to remove processes from the memory by swaping
  it. Process can be later reintroduced into memory and it execution
  can be continued where it left off.

Context switch caused by interrupts/scheduler is pure overhead (saving
the current process context, copying registeries etc..).
  f
