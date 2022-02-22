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

#### APIs
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

Initially, the child process copies the adress space of it's parent. Typically,
we execute an exec command that copies a binary file into the new process's memory
destroying it's memory image.

A child process life cycle ends when it finishes executing its last statement 
and ask the OS to be deleted by the exit() sys call. All of it's memory is 
deallocated.

#### Schedulers
1. *Long-term scheduler*:
  - Loads processes from the job pool into memory (from New to Ready)
  - Controls the degree of multiprogramming (nb of processes in memory)
  - Doesn't care much about the speed
  - CPU-bound process makes high I/O and low amount of calculation
  - In time sharing systems long-term scheduler doesn't exists or minimal
  every processes are put in memory
2. *Short-term scheduler*:
  - Change status from Ready to Running
  - Must be fast 
  - CPU-bound process makes low I/O and high amount of calculation
3. *Medium-term scheduler*
  - Can be avantageous to remove processes from the memory by swaping
  it. Process can be later reintroduced into memory and it execution
  can be continued where it left off.

Context switch caused by interrupts/scheduler is pure overhead (saving
the current process context, copying registeries etc..).

#### Interprocess Communication
Two types of process:
1. *Independant*:
  - Cannot affect or be affected by other processes 
2. *Cooperating*:
  - Can affect or be affected by other processes 

Two types of communication:
1. *Shared Memory*:
  - Region of memory that is shared by cooperating processes is established
  - Shared memory region resides in the address space of the process creating
  the shared-memory segment. Other processes that wish to communicate using 
  this shared memory must attach this memory to their address space
  - Usage of a fixed (bounded) or unfixed (unbounded) buffer
2. *Message passing*:
  - Communication take place by means of messages exchanged between processes
  - Usefull when the communicating processes may reside on different computers
  connected by a network
  - Can use:
    - Direct or indirect communication (indirect is favorable -> less hardcoding)
      - Direct: The two processes must know the name of the other one
      - Indirect: Communiation through ports/mailboxes
      - Can have blocking or nonblocking communication
    - Sync or async communication
    - Automatic or explicit buffer 
      - Zero capacity buffer : queue max size = 0, so no waiting messages
      - Bounded capacity buffer : queue has finite length n, at most n messages
      - Unbounded capacity : queue's length is potentially infinite

##### Pipes
Two types of pipes:
1. *Ordinary Pipes*:
  - Takes the form of a special kind of file
  - Allows two processes to communicate in standard producer-consumer fashion
  - Unidirectional. If two ways communication is required, needs 2 pipes
  - Parent child relationship is required
  - Ordinary pipes cease to exist when the communication is over
2. *Named Pipes*:
  - Takes the form of regular file in the file system (file manipulation sys calls)
  - Bidirectional
  - No parent-child relationship required 
  - Continues to exist after communication


# Threads 
- Basic unit of CPU utilization
Two types of threads:
1. *User threads*
  - Supported without the kernel
  - Used above kernel level
  - Kernel is unawared of user threads cause they are managed by a thread library
2. *Kernel threads*
  - Managed by the system scheduler
  - Runs within a process, but can be referenced bu any other thread in the system
  - Programmer has no direct control over these threads

### Signals
- Used to notify a process that a particular event has occured. Can be sync or async
- Every signal has a default signal handler and can be overridden

# CPU Scheduling
In a monoCPU computer, only 1 process can run at the time (only 1 process is running and
the other ones are ready)

Process execution consists of cycle between CPU burst (time that the process consum ressources
from the CPU) and I/O Burst (idle time when waiting for I/O)

When CPU becomes idle, the CPU scheduler (short-term scheduler) selects a process pre-loaded in
memory (from the ready queue) and allocates CPU ressources to it.

### Nonpreemptive scheduling
Can't deallocate CPU ressources from a running process until it releases the CPU by termininates or waiting.

Can only if process :
1. Passes from Running to Waiting (awaiting I/O, or wait() syscall)
2. Passes from Running to Terminated (when process is done or killed)


### Preemptive scheduling
Can deallocate CPU from a running process.


### Scheduling algorithms

1. *First In First Out*:
  - Simplest algo
  - Often resulting in suffering from the convoy effect
    - When a CPU bound process holds the CPU for a long time, the I/O
    bound processes wait for a long time in the ready queue
2. *Shortest Job First*
  - Prioritizing the job that has the shortest next CPU burst
3. *Priority Scheduling*
  - 
