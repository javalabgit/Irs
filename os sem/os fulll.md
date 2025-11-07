# Comprehensive Study Notes: Foundational Concepts of Operating Systems
## Enhanced for Exam Preparation with Detailed Diagrams and Visual Aids

---

## 1.0 UNIT-I: Operating Systems Overview and System Structures

### 1.1 Introduction

An **Operating System (OS)** is a foundational program that serves as a critical intermediary between a computer's hardware and its users and their applications. The primary goals of an OS are twofold: to create a convenient and user-friendly computing environment and to manage the computer's hardware resources in an efficient and controlled manner. The OS acts as a central control program, coordinating the use of hardware among various application programs for different users. It is the software that brings the physical components of a computer to life, providing the essential services and structures upon which all other software depends.

### 1.2 Learning Outcomes

After studying this unit, you will be able to:

* Define an Operating System and explain its primary goals
* Describe the core functions of an OS, including process, memory, and storage management
* Differentiate between multiprogramming and time-sharing systems
* Explain the concept of dual-mode operation (user mode vs. kernel mode) and its importance for system protection
* Categorize and describe the main types of system calls
* Compare and contrast different OS structures like layered, microkernel, and modular approaches

### 1.3 Detailed Notes with Examples

#### 1.3.1 Core Operating System Concepts

**OS Goals and Components**

An Operating System is a program that controls and coordinates the use of hardware among various applications and users. Its primary goals are to:

* Execute user programs and simplify problem-solving
* Make the computer system convenient to use
* Utilize computer hardware efficiently

A computer system is comprised of four essential components:

1. **Hardware**: Provides the basic computing resources (CPU, memory, I/O devices)
2. **Operating System**: Manages and controls the hardware
3. **Application Programs**: Use system resources to solve user computing problems (e.g., word processors, browsers)
4. **Users**: The people, machines, or other computers interacting with the system

**OS Architecture Overview**

[Image shows the layered architecture with users, software, and OS managing hardware resources]

**Core OS Functions**

An OS performs several fundamental management activities to ensure the smooth and efficient operation of the computer.

**Process Management**

A **process** is a program in execution. It is an active entity that requires resources like CPU time, memory, and I/O devices to complete its task. The OS is responsible for:

* Creating and deleting both user and system processes
* Suspending and resuming processes
* Providing mechanisms for process synchronization and communication
* Providing mechanisms for deadlock handling

**Memory Management**

Main memory is a large, volatile array of bytes where the CPU can directly access data and instructions. The OS is responsible for:

* Keeping track of which parts of memory are currently being used and by which process
* Deciding which processes and data to move into and out of memory
* Allocating and deallocating memory space as needed

**Memory Layout of a Process**

[Image: Process Memory Layout showing Text Segment (Code), Data Section (Global Variables), Heap (Dynamic Memory), and Stack (Temporary Data)]

The typical memory layout of a process includes:
- **Text Section**: Contains the executable code
- **Data Section**: Contains initialized global variables
- **BSS (Block Started by Symbol)**: Contains uninitialized global variables
- **Heap**: Dynamically allocated memory (grows upward)
- **Stack**: Temporary storage for function parameters, return addresses, local variables (grows downward)

**Storage Management**

The OS provides a logical, uniform view of information storage, abstracting the physical properties of storage devices. This includes:

* **File-System Management**: A file is a collection of related information. The OS manages:
  * Creating and deleting files and directories
  * Supporting operations to manipulate files and directories
  * Mapping files onto secondary storage
  * Backing up files to stable, non-volatile media

* **Mass-Storage Management**: Disks are the primary medium for long-term program and data storage. The OS handles:
  * Free-space management
  * Storage allocation
  * Disk scheduling to optimize performance

* **Caching**: Information is temporarily copied from a slower storage system to a faster one (the cache). When information is needed, the OS first checks the cache. If it's present, access is fast; if not, the information is retrieved from the source and a copy is placed in the cache for future use.

#### 1.3.2 Operating System Structure and Operations

**Multiprogramming and Time-Sharing**

**Multiprogramming** is a technique that increases CPU utilization by ensuring the CPU always has a job to execute. The OS keeps several jobs in a job pool on disk. When the currently running job has to wait (e.g., for an I/O operation), the OS switches the CPU to another job in memory.

**Time-sharing** (or **multitasking**) is a logical extension of multiprogramming. In a time-sharing system, the CPU switches between jobs so frequently that users can interact with each running program, creating the illusion of simultaneous execution. This requires an interactive system where users can provide input and receive immediate responses.

| Aspect | Multiprogramming | Time-Sharing |
|--------|------------------|--------------|
| **Purpose** | Maximize CPU utilization | Provide interactive computing |
| **Context Switching** | Occurs on I/O wait | Occurs on timer interrupt |
| **User Interaction** | No interaction during execution | Real-time user interaction |
| **Response Time** | Not a priority | Critical requirement |

**Dual-Mode Operation**

To protect the OS and system components from user programs, the hardware provides two separate modes of operation:

* **Kernel Mode (Mode Bit = 0)**: 
  * The OS executes in this privileged mode
  * Has full access to all hardware
  * Can execute any instruction, including privileged instructions
  * Used for critical OS operations

* **User Mode (Mode Bit = 1)**: 
  * User applications execute in this mode
  * Access to hardware is restricted
  * Privileged instructions cannot be executed
  * Protects system integrity

**Dual-Mode Operation Flow**

When a user application needs to perform a privileged action, such as an I/O operation, it must make a **system call**. This causes a **trap** to the OS, and the hardware switches from user mode to kernel mode. After the OS completes the requested service, it switches the mode back to user mode before returning control to the application.

**Step-by-Step Transition Process:**

1. **User Mode**: Application requests privileged operation
2. **Trap Instruction**: Special hardware instruction triggers mode switch
3. **Hardware Response**: CPU changes mode bit from 1 to 0 (User â†’ Kernel)
4. **Kernel Mode**: OS handles the request with full privileges
5. **Completion**: OS performs the requested operation
6. **Return Instruction**: OS executes return from trap instruction
7. **Mode Switch Back**: Hardware changes mode bit from 0 to 1 (Kernel â†’ User)
8. **Resumed Execution**: User application continues from where it left off

**Timers**

A **timer** is a hardware mechanism that can be set to interrupt the computer after a specified period. This ensures that:

* The OS maintains control over the system
* User programs cannot monopolize the CPU
* Infinite loops in user programs don't crash the system
* Fair resource allocation among processes

When the timer goes off, an interrupt is generated, transferring control back to the OS. The OS can then decide whether to:
* Continue the current process
* Switch to another process
* Terminate the current process if it exceeds its time limit

#### 1.3.3 System Calls and OS Services

**Operating-System Services**

The OS provides a set of services to programs and users to make tasks easier:

* **User Interface (UI)**: Provides a way for users to interact with the system, such as a Command-Line Interface (CLI), Graphical User Interface (GUI), or batch interface

* **Program Execution**: The system can load a program into memory and run it

* **I/O Operations**: A running program may need to perform I/O with a file or a device, which the OS manages

* **File-System Manipulation**: Programs can create, delete, read, write, and search for files and directories

* **Communications**: The OS facilitates information exchange between processes, either on the same computer or across a network

* **Error Detection**: The OS constantly monitors for errors in hardware, I/O devices, and user programs

* **Resource Allocation**: When multiple jobs run concurrently, the OS allocates resources like CPU cycles, memory, and devices among them

* **Accounting**: The OS tracks resource usage for billing or statistics

* **Protection and Security**: The OS controls access to system resources and authenticates users to secure the system

**User and OS Interface**

* **Command-Line Interface (CLI)**: Users type text commands which are interpreted by a program called a shell. The shell gets and executes the next user-specified command. Examples include the Bourne shell in UNIX and the command prompt in Windows.

* **Graphical User Interface (GUI)**: A user-friendly interface based on a desktop metaphor. Users interact with the system using a mouse to click on icons, select from menus, and manage windows. Mobile devices often use a touch-screen GUI.

**System Calls**

A **system call** is the programmatic interface to the services provided by the operating system. When an application needs an OS service, it invokes a system call.

Parameters can be passed to the OS during a system call in three ways:

1. **In registers**: The simplest method, but limited by the number of available CPU registers
2. **In a memory block**: Parameters are stored in a block of memory, and the address of the block is passed as a parameter in a register
3. **On the stack**: The program pushes the parameters onto the stack, and the OS pops them off

**Types of System Calls**

| Category | Examples of System Calls |
|----------|--------------------------|
| **Process Control** | end, abort, load, execute, create process, terminate process, wait, signal event, allocate/free memory |
| **File Management** | create file, delete file, open, close, read, write, reposition, get/set file attributes |
| **Device Management** | request device, release device, read, write, reposition, get/set device attributes, logically attach/detach devices |
| **Information Maintenance** | get/set time or date, get/set system data, get/set process, file, or device attributes |
| **Communications** | create/delete communication connection, send/receive messages, transfer status information, attach/detach remote devices |

#### 1.3.4 OS Design and Implementation

**OS Structures**

* **Simple Structure (e.g., MS-DOS)**: 
  * Not designed with a well-defined structure
  * Functionality is not well separated
  * Applications can often access hardware directly
  * Offers little protection

* **Layered Approach**: 
  * The OS is broken into a number of layers, each built on top of lower layers
  * Layer 0 is the hardware
  * The highest layer is the user interface
  * Each layer only uses services from the layers below it
  * Simplifies construction and debugging
  * Less efficient due to overhead of passing through multiple layers

**[Image: Layered OS Architecture showing concentric circles from Hardware (Layer 0) to User Interface (Layer N)]**

* **Microkernel**: 
  * Removes all nonessential components from the kernel
  * Implements them as user-level programs
  * The microkernel's main function is to provide communication between the client program and the various services running in user space
  * Easier to extend, more reliable, and more secure
  * Performance overhead from user-space to kernel-space communication

* **Modules**: 
  * The kernel has a set of core components
  * Can dynamically link in additional services via loadable modules
  * Modules can be loaded at boot time or during run time
  * Common in modern OSs like Linux and Solaris

**Comparison of OS Structures**

| Approach | Advantages | Disadvantages |
|----------|-----------|-----------------|
| **Layered** | Simplicity of construction and debugging | Less efficient due to overhead of passing through multiple layers |
| **Microkernel** | Easier to extend, more reliable, more secure | Performance overhead from user-space to kernel-space communication |
| **Modular** | Flexibility, easy to maintain, suitable for modern systems | Complex implementation, potential performance issues |

### 1.4 Solved Problems

**Problem 1: File Copy Operation**

**Question**: Describe the sequence of system calls a simple command-line program would use to copy a file from a source location to a destination location. Explain the purpose of each system call in the sequence.

**Answer**: A program to copy a file (source.txt to destination.txt) would use the following sequence of system calls:

1. **open("source.txt", O_RDONLY)**: The program first opens the source file. It requests read-only access. The operating system finds the file, verifies permissions, and returns a small integer called a file descriptor, which is used for all subsequent operations on that file.

2. **open("destination.txt", O_WRONLY | O_CREAT)**: Next, the program opens the destination file. It requests write-only access. The O_CREAT flag tells the OS to create the file if it does not exist. The OS returns a second, unique file descriptor for this file.

3. **read(source_fd, buffer, n_bytes)**: The program enters a loop. In each iteration, it calls read() to read a chunk of data (e.g., 4096 bytes) from the source file into a temporary memory location called a buffer. The call returns the number of bytes actually read.

4. **write(dest_fd, buffer, n_bytes_read)**: The program then calls write() to write the data from the buffer into the destination file. This step is repeated until the read() call returns 0, indicating the end of the source file has been reached.

5. **close(source_fd)**: Once the loop is finished, the program calls close() on the source file's descriptor. This tells the OS to release any resources associated with the open file.

6. **close(dest_fd)**: Finally, the program calls close() on the destination file's descriptor to ensure all written data is saved to disk and resources are released.

**Key Exam Points**: 
- Remember the order of operations: open â†’ read â†’ write â†’ close
- Each system call transitions from user mode to kernel mode
- The file descriptor is crucial for all subsequent file operations
- Proper file closure ensures data integrity and resource cleanup

**Problem 2: User to Kernel Mode Transition**

**Question**: Explain, step-by-step, what happens when a running application needs to read data from a file, focusing on the transition from user mode to kernel mode and back.

**Answer**: The transition from user mode to kernel mode and back is a fundamental protection mechanism. When an application reads from a file, the following steps occur:

1. **User Mode Operation**: The running application, executing in user mode (mode bit = 1), makes a call to a standard library function, such as read(), to get data from a file.

2. **System Call Invocation**: The read() library function is a wrapper. Its job is to set up the necessary parameters (e.g., file descriptor, buffer address, number of bytes) in the appropriate CPU registers and then execute a special hardware instruction called a trap (or software interrupt).

3. **Trap and Mode Switch to Kernel**: The trap instruction causes the CPU to switch from user mode to kernel mode by changing the mode bit from 1 to 0. The CPU then jumps to a fixed location in an interrupt vector table, which contains the address of the operating system's system call handler.

4. **Kernel Mode Operation**: The OS's system call handler executes in kernel mode. It verifies the parameters passed from the user program and performs the actual I/O operation to read the data from the disk into the user's buffer. Because it is in kernel mode, it can execute the privileged instructions required to interact with the disk controller hardware.

5. **Return and Mode Switch to User**: Once the I/O operation is complete, the OS's system call handler prepares to return control. It places a return value in a register and executes a special "return from interrupt" instruction. This instruction causes the hardware to switch the mode bit back to 1, returning the CPU to user mode.

6. **User Mode Resumption**: Control is returned to the standard library function (read()), which then returns the result to the application program. The application continues its execution in user mode, now with the data it requested from the file.

**Detailed Transition Diagram**:

```
USER APPLICATION (Mode Bit = 1)
        â†“
    read() call
        â†“
Set up parameters in registers
        â†“
Execute TRAP instruction
        â†“
    [MODE BIT = 0]
        â†“
CPU jumps to interrupt vector handler
        â†“
KERNEL MODE OPERATION
        â†“
Verify parameters and perform I/O
        â†“
Execute RETURN FROM TRAP instruction
        â†“
    [MODE BIT = 1]
        â†“
Return control to read()
        â†“
USER APPLICATION RESUMES
```

**Key Exam Points**:
- The trap instruction is the key mechanism for mode switching
- Mode bit = 0 for kernel mode, Mode bit = 1 for user mode
- The OS cannot be bypassed; all privileged operations must go through system calls
- This mechanism is essential for system security and stability

### 1.5 Exam Tips & Important Questions

**Key Concepts to Memorize**:

* **System Call**: The programmatic interface to OS services
* **Dual-Mode Operation**: The mechanism (user mode and kernel mode) that protects the OS from user programs
* **Multiprogramming**: Keeping multiple jobs in memory to maximize CPU utilization
* **Time-Sharing**: A logical extension of multiprogramming that allows for interactive use
* **Trap**: A special instruction that switches from user mode to kernel mode
* **Timer**: Hardware mechanism that prevents a process from monopolizing the CPU

**Common Mistakes**:

* Confusing a program (a passive file on disk) with a process (an active program in execution)
* Misunderstanding that a system call is the only legitimate way for a user program to request a privileged operation. A user program cannot simply switch to kernel mode on its own.
* Forgetting that context switching has overhead and impacts system performance
* Not understanding that the mode bit is checked by the CPU hardware before executing privileged instructions

**Key Connections**:

* The Dual-Mode Operation discussed in this unit is the fundamental protection mechanism that makes Process Management (Unit II) and Process Synchronization (Unit III) possible
* Without the distinction between user and kernel mode, the OS could not safely manage processes or enforce mutual exclusion
* The timer mechanism is essential for implementing preemptive scheduling

**Potential Exam Questions**:

* "What is the purpose of the mode bit in dual-mode operation, and why is it essential for protecting the operating system?"
* "Compare and contrast the layered approach and the microkernel approach to OS design. What are the trade-offs of each?"
* "List and describe five major categories of system calls."
* "Explain the complete sequence of events that occurs when a user program calls read() to read from a file. Include the mode transitions."
* "Why is the timer interrupt important in a time-sharing system?"

---

## 2.0 UNIT-II: Processes, Threads, and CPU Scheduling

### 2.1 Introduction

A **process** is a program in execution and represents the fundamental unit of work in a modern operating system. Managing the lifecycle of numerous processesâ€”from creation to terminationâ€”and scheduling their access to the CPU efficiently is one of the most critical and complex tasks an OS performs. This unit delves into the core concepts of process management, including process states, scheduling queues, and interprocess communication (IPC). We will also explore threads, a lighter-weight unit of execution that allows for concurrency within a single process, and analyze the various algorithms that operating systems use to decide which process should run on the CPU next.

### 2.2 Learning Outcomes

After studying this unit, you will be able to:

* Describe the states of a process and the contents of a Process Control Block (PCB)
* Differentiate between the shared memory and message passing models of Interprocess Communication (IPC)
* Explain the benefits of multithreading and compare the many-to-one, one-to-one, and many-to-many multithreading models
* Define scheduling criteria like throughput, turnaround time, and waiting time
* Calculate average waiting time and turnaround time for various scheduling algorithms
* Compare and contrast FCFS, SJF, Priority, and Round Robin scheduling algorithms

### 2.3 Detailed Notes with Examples

#### 2.3.1 Process Management

**The Process Concept**

A **program** is a passive entity, like an executable file on a disk. A **process** is an active entity, representing a program that has been loaded into memory and is executing.

**Key Distinction**:
- **Program**: Passive, static entity on disk
- **Process**: Active, dynamic entity in memory

The memory layout of a process typically includes:

* **Text Section**: The executable code
* **Data Section**: Global variables (initialized)
* **BSS Section**: Uninitialized global variables
* **Heap**: Memory that is dynamically allocated during runtime (grows upward)
* **Stack**: Temporary data storage for function parameters, return addresses, and local variables (grows downward)

**[Image: Process Memory Layout showing all sections with address directions]**

**Process State**

As a process executes, it transitions between several states:

1. **New**: The process is being created
2. **Ready**: The process is in main memory, waiting to be assigned to a CPU
3. **Running**: The process's instructions are being executed on the CPU
4. **Waiting**: The process is waiting for some event to occur (e.g., an I/O completion)
5. **Terminated**: The process has finished execution

**[Image: Process State Transition Diagram showing arrows between states]**

| State | Meaning | Transitions |
|-------|---------|------------|
| **New** | Process created but not yet admitted to ready queue | â†’ Ready (by long-term scheduler) |
| **Ready** | Process is in memory, ready to run | â†’ Running (by short-term scheduler) |
| **Running** | Process is executing on CPU | â†’ Waiting (on I/O), â†’ Ready (on timer), â†’ Terminated |
| **Waiting** | Process waiting for I/O or event | â†’ Ready (event occurs) |
| **Terminated** | Process has finished execution | (End) |

**Process Control Block (PCB)**

Each process is represented in the OS by a **Process Control Block (PCB)**, which stores all information associated with that specific process.

**Key Information in a PCB**:

* **Process State**: Current state (e.g., new, ready, running, waiting, terminated)
* **Process ID (PID)**: Unique identifier for the process
* **Program Counter**: The address of the next instruction to execute
* **CPU Registers**: Values of accumulators, index registers, stack pointers, general-purpose registers, etc.
* **CPU-Scheduling Information**: Process priority, pointers to scheduling queues, scheduling parameters
* **Memory-Management Information**: Base and limit registers, page tables, segment tables
* **Accounting Information**: CPU time used, elapsed real time, time limits, etc.
* **I/O Status Information**: List of I/O devices allocated to the process, list of open files, I/O requests pending
* **Protection Information**: Access permissions, privilege level

**Why PCB is Important for Exams**:
- The PCB is what the OS saves during a context switch
- Understanding PCB content helps explain how the OS manages processes
- Questions often ask what information is saved in a PCB

**Process Scheduling**

The OS manages multiple queues for organizing processes:

* **Job Queue**: All processes in the system (on disk and in memory)
* **Ready Queue**: All processes residing in main memory, ready to execute
* **Device Queues**: Processes waiting for a specific I/O device (there can be multiple device queues)

**[Image: Process Scheduling Queues showing job pool, ready queue, device queues, and schedulers]**

**Different Schedulers Manage Process Movement**:

* **Long-Term Scheduler (Job Scheduler)**: 
  * Selects processes from the job pool and loads them into memory
  * Controls the degree of multiprogramming (how many processes are in memory)
  * Executes infrequently (seconds to minutes)
  * Important in batch systems

* **Short-Term Scheduler (CPU Scheduler)**: 
  * Selects a process from the ready queue and allocates the CPU to it
  * Must execute frequently (milliseconds)
  * Has the most impact on system performance

* **Medium-Term Scheduler**: 
  * Can be used to temporarily remove a process from memory (swap it out)
  * Later reintroduce it (swap it in) to reduce the degree of multiprogramming
  * Useful for improving memory utilization

**Context Switch**

A **context switch** is the task of:

1. Saving the state of the old process (in its PCB)
2. Loading the saved state of the new process (from its PCB)

**During Context Switch**:
- The OS saves CPU registers, program counter, and other state information
- The CPU state is switched to the new process
- This process introduces overhead, as the system does no useful work during the switch
- Modern systems try to minimize context switch time

**Context Switch Overhead Considerations**:
- Pure switching time (typically 1-1000 microseconds)
- Cache miss penalties (can be significant on modern systems)
- TLB (Translation Lookaside Buffer) miss penalties
- Memory bandwidth consumed

**Operations on Processes**

* **Process Creation**: 
  * A running process (a parent) can create new processes (children)
  * Forms a tree structure (process hierarchy)
  * In UNIX-like systems, the fork() system call creates a new process by duplicating the address space of the parent
  * The child process inherits file descriptors and environment from the parent
  * Child and parent execute concurrently

* **Process Termination**: 
  * A process terminates when it finishes its last statement and calls the exit() system call
  * Its resources are then deallocated by the OS
  * A parent may also terminate a child process
  * Parent process may wait for child to terminate using wait() system call

#### 2.3.2 Interprocess Communication (IPC)

**Cooperating Processes**

Processes that can affect or be affected by other executing processes are called **cooperating processes**. They are allowed to cooperate for:

* **Information Sharing**: Processes exchange data and information
* **Computation Speedup**: Dividing a task among multiple processes
* **Modularity**: Implementing system functionality as separate processes
* **Convenience**: Working on multiple tasks simultaneously

**IPC Models**

**1. Shared Memory Model**:

* A region of memory is established as shared space between two or more processes
* Processes can exchange information at memory speed by reading and writing to this area
* The OS is responsible for establishing the shared memory region
* After shared memory is established, the OS is no longer involved in communications
* Faster communication (at memory speed)
* Requires synchronization to prevent race conditions

**Example**: Producer-Consumer Problem
- A producer process places items into a shared bounded buffer
- A consumer process removes them from the buffer
- Need semaphores or locks to ensure consistency
- Producer cannot add to a full buffer
- Consumer cannot remove from an empty buffer

**2. Message Passing Model**:

* Processes communicate by exchanging messages without sharing the same address space
* More secure (processes cannot accidentally access each other's memory)
* Relies on two primary operations: send(message) and receive(message)

**Communication Types**:
* **Direct**: Explicitly naming the recipient (send(P, message))
* **Indirect**: Using a shared mailbox or port (messages go to intermediate entity)

**Synchronization Types**:
* **Blocking (Synchronous)**: Sender/receiver waits until message is received/sent
  * Sender blocks until receiver receives the message
  * Provides natural rendezvous point
  * Simpler semantics

* **Non-blocking (Asynchronous)**: Sender/receiver continues its operation
  * Sender sends and continues immediately
  * Receiver receives if message is available, otherwise continues
  * More flexible but harder to program

**Comparison**:

| Aspect | Shared Memory | Message Passing |
|--------|---------------|-----------------|
| **Speed** | Fast (memory access) | Slower (involves system calls) |
| **Security** | Less secure | More secure (no shared address space) |
| **Implementation** | User-level | Kernel-level (system calls required) |
| **Synchronization** | Complex (race conditions possible) | Built into communication mechanism |
| **Suitable For** | Shared data, speed critical | Distributed systems, security critical |

#### 2.3.3 Threads and Concurrency

**Overview of Threads**

A **thread** is a lightweight process or a basic unit of CPU utilization. 

**Thread Components**:
* Thread ID
* Program counter
* Register set
* Stack

**Threads belonging to the same process share**:
* Code section (text segment)
* Data section (global variables)
* OS resources (file descriptors, signals, etc.)

**Key Benefits of Multithreading**:

* **Responsiveness**: An application can remain responsive to the user even if one part is blocked (e.g., downloading a file while typing)
* **Resource Sharing**: Threads share memory and resources by default, which is more efficient than sharing between separate processes
* **Economy**: It is cheaper to create and switch between threads than between processes
  * Thread creation: microseconds
  * Process creation: milliseconds
  * Context switching between threads: less overhead than between processes
* **Utilization of Multiprocessor Architectures**: Multiple threads can run in parallel on different processor cores, providing true parallelism

**Multithreading Models**

These models describe the relationship between user-level threads (managed by a thread library) and kernel-level threads (managed by the OS).

**1. Many-to-One Model**:

* Maps many user threads to a single kernel thread
* Implemented in user space (thread library)
* The OS is unaware of user-level threads
* **Advantage**: Efficient thread management in user space, low overhead
* **Disadvantage**: 
  * The entire process blocks if one thread makes a blocking system call
  * Cannot take advantage of multiprocessor systems (only one kernel thread)
  * Poor scalability

**[Image: Many-to-One Thread Model showing multiple user threads mapping to single kernel thread]**

**2. One-to-One Model**:

* Maps each user thread to a dedicated kernel thread
* Each thread is independently scheduled by the kernel
* **Advantage**: 
  * Provides true concurrency
  * A blocking call in one thread doesn't affect others
  * Can use multiple processors effectively
* **Disadvantage**: 
  * Creating a user thread requires creating a kernel thread, adding overhead
  * Too many threads can overwhelm the OS
  * Kernel threads are limited resources

**[Image: One-to-One Thread Model showing individual mapping]**

**3. Many-to-Many Model**:

* Multiplexes many user threads to a smaller or equal number of kernel threads
* Also called "Two-Level Model"
* Scheduler entities do the virtual CPU scheduling
* **Advantage**: 
  * A balance between the other two models
  * Provides concurrency without excessive overhead
  * Efficient use of kernel threads
* **Disadvantage**: 
  * More complex to implement
  * Difficult to debug
  * Need additional scheduling at user level

**[Image: Many-to-Many Thread Model showing multiple users mapping to multiple kernels]**

**Comparison of Threading Models**:

| Model | Concurrency | Performance | Scalability | Complexity |
|-------|-----------|-------------|------------|-----------|
| **Many-to-One** | No | Good | Poor | Simple |
| **One-to-One** | Yes | Good | Limited | Simple |
| **Many-to-Many** | Yes | Excellent | Good | Complex |

#### 2.3.4 CPU Scheduling

**Basic Concepts**

Process execution is a cycle of CPU execution and I/O wait, known as the **CPUâ€“I/O Burst Cycle**.

* Each process alternates between CPU execution and I/O operations
* CPU burst: Time spent executing in CPU
* I/O burst: Time spent waiting for I/O to complete
* Eventually process terminates with a final CPU burst

**Scheduling Types**:

* **Nonpreemptive (Cooperative) Scheduling**: 
  * Once the CPU is allocated to a process, it keeps it until it either terminates or switches to a waiting state (I/O)
  * Used in older systems and some real-time systems
  * Simple to implement
  * Less responsive

* **Preemptive Scheduling**: 
  * The CPU can be taken away from a running process
  * Occurs when: higher-priority process arrives, time slice expires, or I/O interrupt occurs
  * More responsive
  * More complex to implement
  * Need to save/restore process state (context switch overhead)

**Scheduling Criteria** (Metrics for Evaluating Scheduling Algorithms)

* **CPU Utilization**: Percentage of time the CPU is busy (higher is better; target: 40-90%)
* **Throughput**: Number of processes completed per unit of time (higher is better)
* **Turnaround Time**: Total time from submission to completion = Completion Time - Arrival Time (lower is better)
* **Waiting Time**: Total time a process spends waiting in the ready queue (lower is better) = Turnaround Time - Burst Time
* **Response Time**: Time from submission until the first response is produced (lower is better; important for interactive systems)

**Important Formulas**:

```
Turnaround Time (TAT) = Completion Time - Arrival Time
Waiting Time (WT) = Turnaround Time - Burst Time
Average Waiting Time = Î£(Waiting Times) / Number of Processes
Average Turnaround Time = Î£(Turnaround Times) / Number of Processes
```

**Scheduling Algorithms**

**1. First-Come, First-Served (FCFS)**

* A nonpreemptive algorithm where the process that requests the CPU first gets it first
* Simple but can have long average waiting times
* Suffers from the "convoy effect": if a long process arrives first, all subsequent shorter processes must wait

**Characteristics**:
- **Average WT**: Often poor
- **Fair**: Yes (in order)
- **Starvation**: No
- **Implementation**: Simple (use queue)

**Example Gantt Chart**:
```
P1(8)  | P2(4)  | P3(9)  | P4(5)  |
|------|--------|--------|--------|
0      8       12       21       26
```

**2. Shortest-Job-First (SJF)**

The CPU is allocated to the process with the smallest next CPU burst.

**Non-Preemptive SJF**:
* Once a process starts, it runs to completion
* Provably optimal for average waiting time (minimizes average WT)
* Difficult to implement (requires knowing burst time in advance)

**Preemptive SJF (Shortest-Remaining-Time-First - SRTF)**:
* If a new process arrives with a shorter burst than the remaining time of the current process, the current process is preempted
* Even more optimal than non-preemptive SJF
* More overhead due to preemption

**Characteristics**:
- **Average WT**: Optimal
- **Fair**: No (shorter jobs get priority)
- **Starvation**: Yes (long jobs may never run)
- **Implementation**: Difficult (need to predict burst time)

**Problem**: How to predict burst time? Typically use exponential averaging:
```
Ï„_{n+1} = Î± * t_n + (1-Î±) * Ï„_n
where:
Ï„_n = predicted burst time for nth process
t_n = actual burst time for nth process
Î± = weight (typically 0.5)
```

**3. Priority Scheduling**

A priority is associated with each process, and the CPU is allocated to the process with the highest priority.

**Characteristics**:
* Can be preemptive or nonpreemptive
* **Priority**: Can be internal (CPU/IO ratio) or external (importance)
* **Problem**: Starvation (low-priority processes never run)
* **Solution**: Aging (gradually increase priority of waiting processes over time)

**Starvation Example**:
- If high-priority processes keep arriving, low-priority processes may never execute
- Solution: After a process waits for time T, increase its priority

**Preemptive vs. Non-Preemptive**:
- **Non-Preemptive**: Running process keeps CPU until it yields (I/O or termination)
- **Preemptive**: New higher-priority process can interrupt running process

**4. Round Robin (RR)**

A preemptive algorithm designed for time-sharing systems.

**Key Concept**:
* Each process gets a small unit of CPU time called a **time quantum** (or time slice)
* If the process is still running after its quantum expires, it is preempted and placed at the end of the ready queue
* Typically 10-100 milliseconds

**Characteristics**:
- **Average WT**: Fair but not optimal
- **Fair**: Yes (each process gets equal CPU time)
- **Starvation**: No
- **Responsiveness**: Good (no process waits more than (n-1)q time units)
- **Context Switch Overhead**: Important consideration

**Quantum Selection**:
* Small quantum (q): More responsive but more context switches (overhead)
* Large quantum (q â†’ âˆž): Approaches FCFS, fewer context switches
* Typically choose based on desired response time vs. overhead

**[Image: Round Robin Scheduling with Ready Queue showing time slices]**

**5. Multilevel Queue Scheduling**

The ready queue is partitioned into separate queues (e.g., for foreground and background processes).

**Characteristics**:
* Each queue has its own scheduling algorithm
* There is scheduling among the queues (e.g., fixed-priority or time-sharing)
* Useful for different process types (system, interactive, batch)

**Example Queue Structure**:
```
Foreground (Interactive) - Round Robin (80% CPU)
                â†“
Background (Batch) - FCFS (20% CPU)
```

**6. Multilevel Feedback-Queue Scheduling**

Similar to multilevel queue, but processes can move between queues.

**Characteristics**:
* Most complex and most flexible algorithm
* Can separate processes based on CPU burst characteristics
* Implements aging by moving processes between queues
* Prevents starvation

**Typical Structure**:
```
Queue 0 (RR, q=8ms):     [Most Priority]
Queue 1 (RR, q=16ms):    [Medium Priority]
Queue 2 (FCFS):          [Low Priority]
```

**Process Movement Rules**:
- New process starts in Queue 0
- If completes before quantum, goes to next queue (lower priority)
- If I/O request, returns to Queue 0
- After waiting long time, process promoted (aging)

**Advantages of Feedback Queues**:
- Separates short and long CPU-bound processes
- Good response time for short processes
- Starvation avoided through aging
- Efficient I/O scheduling

### 2.4 Solved Problems

**Problem 1: First-Come, First-Served (FCFS)**

**Question**: Given the following processes, calculate the average waiting time and average turnaround time using the FCFS scheduling algorithm.

| Process | Arrival Time | Burst Time |
|---------|-------------|-----------|
| P1 | 0 | 8 |
| P2 | 1 | 4 |
| P3 | 2 | 9 |
| P4 | 3 | 5 |

**Solution**: Processes are served in the order they arrive: P1 â†’ P2 â†’ P3 â†’ P4.

**Gantt Chart**: 
```
P1(8)  | P2(4)  | P3(9)  | P4(5)
|------|--------|--------|--------|
0      8       12       21       26
```

**Calculations**:

* Turnaround Time (TAT) = Completion Time - Arrival Time
* Waiting Time (WT) = Turnaround Time - Burst Time

| Process | Arrival Time | Burst Time | Completion Time | Turnaround Time | Waiting Time |
|---------|-------------|-----------|-----------------|-----------------|-------------|
| P1 | 0 | 8 | 8 | 8 - 0 = 8 | 8 - 8 = 0 |
| P2 | 1 | 4 | 12 | 12 - 1 = 11 | 11 - 4 = 7 |
| P3 | 2 | 9 | 21 | 21 - 2 = 19 | 19 - 9 = 10 |
| P4 | 3 | 5 | 26 | 26 - 3 = 23 | 23 - 5 = 18 |

**Average Times**:
* Average Waiting Time: (0 + 7 + 10 + 18) / 4 = **8.75 ms**
* Average Turnaround Time: (8 + 11 + 19 + 23) / 4 = **15.25 ms**

**Exam Analysis**: FCFS is simple but note the high waiting time, especially for P4. This demonstrates the "convoy effect."

---

**Problem 2: Shortest-Job-First (SJF) - Non-Preemptive**

**Question**: Using the same set of processes, calculate the average waiting time and average turnaround time for the non-preemptive SJF algorithm.

**Solution**: SJF selects the shortest job from the ready queue at each decision point.

**Gantt Chart**:
```
P1(8)  | P2(4)  | P4(5)  | P3(9)
|------|--------|--------|--------|
0      8       12       17       26
```

**Decision Points Explanation**:
* At T=0: Only P1 available â†’ Execute P1
* At T=8: Ready queue = {P2(4), P3(9), P4(5)} â†’ Pick shortest: P2
* At T=12: Ready queue = {P3(9), P4(5)} â†’ Pick shortest: P4
* At T=17: Ready queue = {P3(9)} â†’ Execute P3

**Calculations**:

| Process | Arrival Time | Burst Time | Completion Time | Turnaround Time | Waiting Time |
|---------|-------------|-----------|-----------------|-----------------|-------------|
| P1 | 0 | 8 | 8 | 8 - 0 = 8 | 8 - 8 = 0 |
| P2 | 1 | 4 | 12 | 12 - 1 = 11 | 11 - 4 = 7 |
| P3 | 2 | 9 | 26 | 26 - 2 = 24 | 24 - 9 = 15 |
| P4 | 3 | 5 | 17 | 17 - 3 = 14 | 14 - 5 = 9 |

**Average Times**:
* Average Waiting Time: (0 + 7 + 15 + 9) / 4 = **7.75 ms**
* Average Turnaround Time: (8 + 11 + 24 + 14) / 4 = **14.25 ms**

**Comparison with FCFS**:
- SJF AWT: 7.75 ms vs FCFS AWT: 8.75 ms (improvement of 1 ms)
- SJF is optimal for minimizing average waiting time
- Note: P3 has higher waiting time in SJF compared to FCFS

---

**Problem 3: Shortest-Remaining-Time-First (SRTF) - Preemptive SJF**

**Question**: Using the same set of processes, calculate results for the preemptive SJF (SRTF) algorithm.

**Solution**: SRTF preempts the current process if a new process arrives with a shorter burst time.

**Gantt Chart**:
```
P1(1) | P2(4) | P4(5) | P1(7) | P3(9)
|-----|-------|-------|-------|-------|
0     1       5      10      17      26
```

**Timeline Explanation**:
* T=0: P1 starts (burst=8)
* T=1: P2 arrives (burst=4). P1 has 7 remaining > P2's 4 â†’ P2 preempts P1
* T=2: P3 arrives (burst=9). P2 has 3 remaining < P3's 9 â†’ P2 continues
* T=3: P4 arrives (burst=5). P2 has 2 remaining < P4's 5 â†’ P2 continues
* T=5: P2 finishes. Ready = {P1(7), P3(9), P4(5)} â†’ P4 shortest
* T=10: P4 finishes. Ready = {P1(7), P3(9)} â†’ P1 shortest
* T=17: P1 finishes. Ready = {P3(9)} â†’ Execute P3
* T=26: P3 finishes

**Calculations**:

| Process | Arrival Time | Burst Time | Completion Time | Turnaround Time | Waiting Time |
|---------|-------------|-----------|-----------------|-----------------|-------------|
| P1 | 0 | 8 | 17 | 17 - 0 = 17 | 17 - 8 = 9 |
| P2 | 1 | 4 | 5 | 5 - 1 = 4 | 4 - 4 = 0 |
| P3 | 2 | 9 | 26 | 26 - 2 = 24 | 24 - 9 = 15 |
| P4 | 3 | 5 | 10 | 10 - 3 = 7 | 7 - 5 = 2 |

**Average Times**:
* Average Waiting Time: (9 + 0 + 15 + 2) / 4 = **6.5 ms**
* Average Turnaround Time: (17 + 4 + 24 + 7) / 4 = **13.0 ms**

**Comparison**:
- SRTF (6.5 ms) < Non-Preemptive SJF (7.75 ms) < FCFS (8.75 ms)
- SRTF gives best average waiting time
- Note: P1 suffers higher waiting time due to preemptions

---

**Problem 4: Priority Scheduling (Non-Preemptive)**

**Question**: Given the following processes with priorities (lower number = higher priority), calculate results for non-preemptive Priority scheduling. Assume all processes arrive at T=0.

| Process | Burst Time | Priority |
|---------|-----------|----------|
| P1 | 10 | 3 |
| P2 | 1 | 1 |
| P3 | 2 | 4 |
| P4 | 1 | 5 |
| P5 | 5 | 2 |

**Solution**: Processes are served in order of priority: P2 (priority 1) â†’ P5 (priority 2) â†’ P1 (priority 3) â†’ P3 (priority 4) â†’ P4 (priority 5)

**Gantt Chart**:
```
P2(1)  | P5(5)  | P1(10) | P3(2)  | P4(1)
|------|--------|--------|--------|--------|
0      1        6       16       18       19
```

**Calculations**:

| Process | Burst Time | Priority | Completion Time | Turnaround Time | Waiting Time |
|---------|-----------|----------|-----------------|-----------------|-------------|
| P1 | 10 | 3 | 16 | 16 | 6 |
| P2 | 1 | 1 | 1 | 1 | 0 |
| P3 | 2 | 4 | 18 | 18 | 16 |
| P4 | 1 | 5 | 19 | 19 | 18 |
| P5 | 5 | 2 | 6 | 6 | 1 |

**Average Times**:
* Average Waiting Time: (6 + 0 + 16 + 18 + 1) / 5 = **8.2 ms**
* Average Turnaround Time: (16 + 1 + 18 + 19 + 6) / 5 = **12.0 ms**

**Key Observation**: P4 has very high waiting time despite short burst - it has lowest priority.

---

**Problem 5: Round Robin (RR) Scheduling**

**Question**: Using the first set of processes, calculate results for Round Robin scheduling with a time quantum of 4 ms.

| Process | Arrival Time | Burst Time |
|---------|-------------|-----------|
| P1 | 0 | 8 |
| P2 | 1 | 4 |
| P3 | 2 | 9 |
| P4 | 3 | 5 |

**Solution**: Processes get 4ms of CPU time before being moved to the back of the ready queue.

**Gantt Chart**:
```
P1(4)  | P2(4)  | P3(4)  | P4(4)  | P1(4)  | P3(4)  | P4(1)  | P3(1)
|------|--------|--------|--------|--------|--------|--------|--------|
0      4        8       12       16       20       24       25       26
```

**Timeline Explanation**:
* T=0: P1 starts (8ms), runs 4ms â†’ Remaining: P1(4)
* T=4: P1 preempted, Queue: P2, P3, P4, P1. Run P2 (4ms) â†’ Completes
* T=8: Queue: P3, P4, P1. Run P3 (4ms out of 9) â†’ Remaining: P3(5)
* T=12: Queue: P4, P1, P3. Run P4 (4ms out of 5) â†’ Remaining: P4(1)
* T=16: Queue: P1, P3, P4. Run P1 (4ms) â†’ Completes
* T=20: Queue: P3, P4. Run P3 (4ms out of 5) â†’ Remaining: P3(1)
* T=24: Queue: P4, P3. Run P4 (1ms) â†’ Completes
* T=25: Queue: P3. Run P3 (1ms) â†’ Completes

**Calculations**:

| Process | Arrival Time | Burst Time | Completion Time | Turnaround Time | Waiting Time |
|---------|-------------|-----------|-----------------|-----------------|-------------|
| P1 | 0 | 8 | 20 | 20 - 0 = 20 | 20 - 8 = 12 |
| P2 | 1 | 4 | 8 | 8 - 1 = 7 | 7 - 4 = 3 |
| P3 | 2 | 9 | 26 | 26 - 2 = 24 | 24 - 9 = 15 |
| P4 | 3 | 5 | 25 | 25 - 3 = 22 | 22 - 5 = 17 |

**Average Times**:
* Average Waiting Time: (12 + 3 + 15 + 17) / 4 = **11.75 ms**
* Average Turnaround Time: (20 + 7 + 24 + 22) / 4 = **18.25 ms**

**Comparison Summary**:

| Algorithm | Avg WT | Avg TAT | Notes |
|-----------|--------|---------|-------|
| FCFS | 8.75 | 15.25 | Simple, high waiting time |
| SJF | 7.75 | 14.25 | Optimal but requires burst prediction |
| SRTF | 6.5 | 13.0 | Best but impractical |
| Priority | 8.2 | 12.0 | Specific to priorities |
| RR (q=4) | 11.75 | 18.25 | Fair but not optimal |

### 2.5 Exam Tips & Important Questions

**Key Concepts to Memorize**:

* **PCB (Process Control Block)**: The data structure that stores all information about a process
* **Context Switch**: The mechanism to save the state of one process and restore the state of another
* **Preemption**: The act of temporarily interrupting a running task, with the intention of resuming it at a later time
* **Time Quantum**: The fixed time slice given to a process in Round Robin scheduling
* **Burst Time**: Time period during which a process uses the CPU continuously
* **The names and basic logic of all scheduling algorithms**: FCFS, SJF, Priority, RR

**Common Exam Mistakes**:

* Forgetting to account for arrival times when calculating waiting times, especially in preemptive algorithms
* Confusing the preemptive (SRTF) and non-preemptive versions of SJF
* Incorrectly updating the ready queue order in Round Robin scheduling
* Writing arrival time when calculating turnaround time (should be completion time - arrival time)
* Forgetting to move processes to the back of the queue in Round Robin
* Confusing priority (high number vs. low number being higher priority)

**Key Connections**:

* A Context Switch is the mechanism that enables preemptive scheduling algorithms like Round Robin (RR)
* The overhead of a context switch is a critical factor in determining an effective time quantum for RR scheduling
* Process states determine when context switches occur
* The PCB is what gets saved/restored during context switches

**Potential Exam Questions**:

* "For a given set of processes, calculate the average waiting time using both FCFS and SJF scheduling. Which is better and why?"
* "Explain the difference between preemptive and non-preemptive scheduling. Give an example of each."
* "What is the convoy effect in FCFS scheduling?"
* "Why is SJF optimal for minimizing average waiting time?"
* "Explain how Round Robin scheduling provides fairness. What is the trade-off?"
* "How does the time quantum affect Round Robin performance?"
* "Explain how a multilevel feedback-queue scheduler prevents starvation while still prioritizing short jobs."
* "What are the benefits of multithreading over using multiple processes? Describe a situation where using multiple processes would be preferable."
* "Compare one-to-one and many-to-many thread models. When would you use each?"
* "Draw a state transition diagram for a process and explain each state."
* "Describe the contents of a PCB and explain why each field is necessary."

**Formula Quick Reference**:

```
Turnaround Time (TAT) = Completion Time - Arrival Time
Waiting Time (WT) = Turnaround Time - Burst Time
Context Switch Time = Small compared to burst times but significant in modern systems
```

---

## 3.0 UNIT-III: Process Synchronization and Deadlocks

### 3.1 Introduction

When multiple cooperating processes execute concurrently and share data, their unsynchronized access can lead to data inconsistency. This unit introduces the concept of process synchronization, which refers to the mechanisms used to coordinate the execution of processes that share logical address space or resources. We will explore the "critical-section problem" and examine various toolsâ€”such as mutex locks, semaphores, and monitorsâ€”designed to enforce controlled access to shared data. Furthermore, we will investigate deadlock, a critical problem in multiprogramming systems where two or more processes become permanently blocked, each waiting for a resource held by another process in the set.

### 3.2 Learning Outcomes

After studying this unit, you will be able to:

* Define the critical-section problem and its three requirements: mutual exclusion, progress, and bounded waiting
* Explain how synchronization tools like mutex locks, semaphores, and monitors are used to solve the critical-section problem
* Describe the classic synchronization problems: Bounded-Buffer, Readers-Writers, and Dining-Philosophers
* Identify the four necessary conditions for a deadlock to occur
* Differentiate between deadlock prevention, avoidance, detection, and recovery
* Apply the Banker's algorithm to determine if a system is in a safe state

### 3.3 Detailed Notes with Examples

#### 3.3.1 Synchronization Tools

**The Critical-Section Problem**

A **race condition** occurs when several processes access and manipulate the same data concurrently, and the outcome depends on the particular order of access.

**Example of Race Condition**:
```
Shared Variable: count = 5

Process A:
  read count         // reads 5
  count = count + 1  // count = 6
  write count        // writes 6

Process B:
  read count         // reads 5
  count = count - 1  // count = 4
  write count        // writes 4

Expected Result: count = 5 (one increment, one decrement)
Possible Result: count = 4 or 6 (depending on execution order)
```

To prevent race conditions, we must ensure that only one process at a time can manipulate the shared data. The part of a program where shared data is accessed is called the **critical section**.

**Solution to Critical-Section Problem** must satisfy three requirements:

1. **Mutual Exclusion**: 
   * If a process is executing in its critical section, no other process can be executing in its critical section
   * Only one process at a time in the critical section

2. **Progress**: 
   * If no process is in its critical section and some processes want to enter, only those not in their remainder sections can participate in the decision of who enters next
   * If critical section is empty and process wants to enter, it should be allowed (no unnecessary delays)
   * This decision cannot be postponed indefinitely

3. **Bounded Waiting**: 
   * There must be a limit on the number of times other processes are allowed to enter their critical sections after a process has made a request to enter its critical section
   * Prevents starvation
   * No process waits indefinitely

**Process Structure with Critical Section**:

```
do {
    ENTRY SECTION      â† Acquire lock/semaphore
    CRITICAL SECTION   â† Access shared resource
    EXIT SECTION       â† Release lock/semaphore
    REMAINDER SECTION  â† Do other work
} while(TRUE);
```

**Peterson's Solution**

This is a classic software-based solution that works for two processes.

```c
// Shared variables
int turn;
boolean flag[2];

// Process i:
do {
    flag[i] = TRUE;           // Signal interest
    turn = j;                 // Set turn to other process
    while (flag[j] && turn == j);  // Wait if other has interest and it's their turn
    
    // CRITICAL SECTION
    
    flag[i] = FALSE;          // Release critical section
    // REMAINDER SECTION
} while(TRUE);
```

**How It Works**:
* Each process sets its flag to TRUE (indicating interest)
* Each process sets turn to the other process
* Each waits while the other wants to go AND it's their turn
* When conditions are met, the process can enter critical section

**Limitations**:
* Only works for two processes
* Not guaranteed on modern computer architectures due to instruction reordering
* Now mainly of historical/educational interest

**Mutex Locks and Semaphores**

**Mutex Lock (Mutual Exclusion Lock)**:

A simple tool to provide mutual exclusion.

```c
acquire() {
    while (!available);  // Busy waiting
    available = FALSE;
}

release() {
    available = TRUE;
}
```

**Usage**:
```c
do {
    acquire lock
    // CRITICAL SECTION
    release lock
    // REMAINDER SECTION
} while(TRUE);
```

**Characteristics**:
* Binary lock (two states: locked/unlocked)
* Simple to understand and use
* Busy waiting wastes CPU cycles (spinlock)
* Modern implementations use blocking rather than busy waiting

**Semaphore**:

A more general synchronization tool than mutex. A semaphore is an integer variable S that is accessed only through two atomic operations: **wait(S)** (or P) and **signal(S)** (or V).

**Operations**:

```c
wait(S) {
    S--;
    if (S < 0)
        block this process;  // Add to waiting queue
}

signal(S) {
    S++;
    if (S <= 0)
        wakeup(P);  // Wake up a waiting process from queue
}
```

**Types of Semaphores**:

* **Counting Semaphore**: 
  * Can range over an unrestricted domain (0, 1, 2, ...)
  * Used to control access to a resource with a finite number of instances
  * Initial value = number of resources available

* **Binary Semaphore**: 
  * Can only have a value of 0 or 1
  * On many systems, it is known as a mutex lock
  * Provides mutual exclusion

**Example: Counting Semaphore for Resource Pool**

```c
Semaphore S = 3;  // 3 identical resources available

Process 1:
    wait(S);       // S becomes 2
    use resource
    signal(S);     // S becomes 3

Process 2:
    wait(S);       // S becomes 2 (or blocks if S=0)
    use resource
    signal(S);
```

**Implementation**:

* **Busy Waiting (Spinlock)**: Process repeatedly checks condition
  * Simple but wastes CPU cycles
  * Only suitable for very short wait times

* **Blocking**: Process blocks and is placed in waiting queue
  * Better approach
  * Wakes up only when resource is available
  * More efficient for long waits

**Monitors**

A **monitor** is a high-level synchronization construct that simplifies concurrent programming.

**Characteristics**:
* An abstract data type that encapsulates shared data
* Encapsulates operations (procedures) that can be performed on shared data
* Ensures only one process can be active within the monitor at a time
* Automatically provides mutual exclusion
* Programmers do not need to explicitly code synchronization constraints

**Structure**:

```
MONITOR MonitorName {
    // Shared Data
    private int shared_data;
    
    // Condition Variables
    condition cv;
    
    // Public Methods
    public void method1() {
        // CRITICAL SECTION
        // Automatically protected by monitor
    }
    
    public void method2() {
        // Can use wait(cv) and signal(cv)
    }
}
```

**Condition Variables**:
* Used with monitors for more complex synchronization
* `wait(cv)`: Process waits on condition and releases monitor lock
* `signal(cv)`: Wake up one waiting process and re-acquire lock

**Advantages of Monitors**:
* Simpler than semaphores or locks
* Less error-prone
* Automatic mutual exclusion
* Compiler enforces proper usage

#### 3.3.2 Classic Synchronization Problems

**1. The Bounded-Buffer Problem (Producer-Consumer)**

**Problem Setup**:
* A producer process creates items and places them in a shared bounded buffer
* A consumer process removes items from the buffer
* Buffer has maximum capacity N

**Constraints**:
* Producer cannot add to a full buffer (must wait)
* Consumer cannot remove from an empty buffer (must wait)
* Only one producer/consumer can access buffer at a time (mutual exclusion)

**Solution Using Semaphores**:

```c
Semaphore mutex = 1;      // Binary semaphore for mutual exclusion
Semaphore empty = N;      // Counting semaphore (initially N empty slots)
Semaphore full = 0;       // Counting semaphore (initially 0 full slots)

Producer:
do {
    produce item
    wait(empty);           // Wait if buffer full
    wait(mutex);           // Acquire lock
    add item to buffer
    signal(mutex);         // Release lock
    signal(full);          // Signal that buffer has item
} while(TRUE);

Consumer:
do {
    wait(full);            // Wait if buffer empty
    wait(mutex);           // Acquire lock
    remove item from buffer
    signal(mutex);         // Release lock
    signal(empty);         // Signal that buffer has empty space
    consume item
} while(TRUE);
```

**Key Points**:
* If buffer is full, producer blocks on wait(empty)
* If buffer is empty, consumer blocks on wait(full)
* Mutual exclusion protected by mutex semaphore
* Efficient signaling without busy waiting

**2. The Readers-Writers Problem**

**Problem Setup**:
* A database is shared among multiple processes
* Some processes are **readers** (only read data, no modification)
* Some processes are **writers** (read and write data)

**Constraints**:
* Multiple readers can access the database concurrently
* A writer must have exclusive access (no other readers or writers)
* A writer cannot access if readers are present
* A reader cannot access if a writer is present or waiting

**Readers-Preferring Solution**:

```c
Semaphore mutex = 1;           // Protects readcount
Semaphore write_mutex = 1;    // Protects database from writers

int readcount = 0;             // Number of active readers

Reader:
do {
    wait(mutex);               // Acquire lock
    readcount++;
    if (readcount == 1)
        wait(write_mutex);     // First reader blocks writers
    signal(mutex);             // Release lock
    
    // READ DATABASE
    
    wait(mutex);               // Acquire lock
    readcount--;
    if (readcount == 0)
        signal(write_mutex);   // Last reader allows writers
    signal(mutex);             // Release lock
} while(TRUE);

Writer:
do {
    wait(write_mutex);         // Acquire exclusive access
    // WRITE DATABASE
    signal(write_mutex);       // Release database
} while(TRUE);
```

**Problem**: Writers can starve if readers keep arriving

**Alternative: Writers-Preferring Solution** prioritizes writers but may starve readers

**3. The Dining-Philosophers Problem**

**Problem Setup**:
* Five philosophers sit at a circular table
* Five chopsticks (one between each pair of philosophers)
* Each philosopher thinks or eats
* To eat, a philosopher needs both the left and right chopstick
* To think, a philosopher doesn't need chopsticks

**[Image: Circular arrangement showing philosophers and chopsticks]**

**Naive Solution (DEADLOCK)**:

```c
Semaphore chopstick[5];  // Each initialized to 1

Philosopher i:
do {
    think();
    wait(chopstick[i]);             // Get left chopstick
    wait(chopstick[(i+1)%5]);      // Get right chopstick
    eat();
    signal(chopstick[i]);           // Put down left
    signal(chopstick[(i+1)%5]);    // Put down right
} while(TRUE);
```

**Problem**: If all philosophers pick up left chopstick simultaneously, they all wait for right chopstick â†’ DEADLOCK

**Solution 1: Asymmetric Approach**

```c
Philosopher i:
do {
    think();
    if (i is even) {
        wait(chopstick[i]);
        wait(chopstick[(i+1)%5]);
    } else {
        wait(chopstick[(i+1)%5]);   // Reverse order for odd philosophers
        wait(chopstick[i]);
    }
    eat();
    signal(chopstick[i]);
    signal(chopstick[(i+1)%5]);
} while(TRUE);
```

**Solution 2: Monitor-Based Approach**

```c
MONITOR DiningPhilosophers {
    condition self[5];
    int state[5] = {thinking, thinking, ...};  // thinking, hungry, eating
    
    public void pickup(int i) {
        state[i] = hungry;
        test(i);
        if (state[i] != eating)
            wait(self[i]);
    }
    
    public void putdown(int i) {
        state[i] = thinking;
        test((i+4)%5);
        test((i+1)%5);
    }
    
    private void test(int i) {
        if (state[(i+4)%5] != eating &&
            state[i] == hungry &&
            state[(i+1)%5] != eating) {
            state[i] = eating;
            signal(self[i]);
        }
    }
}
```

**Key Insight**: A philosopher can only eat if both neighbors are not eating

#### 3.3.3 Deadlocks

**Deadlock Characterization**

A **deadlock** is a situation where two or more processes become permanently blocked, each waiting for a resource held by another process in the set.

A deadlock can arise if **four conditions hold simultaneously**:

1. **Mutual Exclusion**: 
   * At least one resource must be held in a non-sharable mode
   * Only one process can use the resource at a time

2. **Hold and Wait**: 
   * A process is holding at least one resource and is waiting to acquire additional resources held by other processes
   * A process can hold a resource while waiting for another

3. **No Preemption**: 
   * A resource can be released only voluntarily by the process holding it
   * The OS cannot forcibly take away resources

4. **Circular Wait**: 
   * A set of waiting processes {Pâ‚€, Pâ‚, ..., Pâ‚™} exists such that:
   * Pâ‚€ is waiting for a resource held by Pâ‚
   * Pâ‚ is waiting for a resource held by Pâ‚‚
   * ...
   * Pâ‚™ is waiting for a resource held by Pâ‚€
   * Forms a cycle in resource allocation graph

**[Image: Deadlock scenario with circular wait involving P1, P2 holding and requesting R1, R2]**

**Resource Allocation Graph**:
* Nodes: Processes (circles) and Resources (squares)
* Edges:
  * P â†’ R: Process requesting resource
  * R â†’ P: Resource allocated to process
* Deadlock exists if and only if the graph contains a cycle

**Example**: If graph shows P1 â†’ R1 â†’ P2 â†’ R2 â†’ P1, this is a cycle indicating deadlock

**Methods for Handling Deadlocks**

**1. Deadlock Prevention**

This method ensures that at least one of the four necessary conditions for deadlock can never hold.

**Prevention Strategies**:

* **Prevent Mutual Exclusion**: 
  * Make resources shareable (not always possible)
  * Example: Read-only files can be shared

* **Prevent Hold-and-Wait**: 
  * **Option A**: Require process to request all resources at once
    * Problem: May waste resources if not all needed immediately
  * **Option B**: Require process to release all current resources before requesting new ones
    * Problem: May need to re-acquire resources

* **Prevent No Preemption**: 
  * Allow preemption of resources
  * When process waiting for resource held by another, preempt holding process
  * Problem: Only practical for certain resource types (CPU, memory)

* **Prevent Circular Wait**: 
  * Impose total ordering on all resources
  * Require processes to request resources in increasing order
  * If process needs R_i and R_j where i < j, must request R_i first
  * Problem: Difficult to maintain globally

**Trade-offs**: Prevention often leads to low resource utilization and reduced system throughput

**2. Deadlock Avoidance**

This method dynamically avoids deadlock by examining each resource allocation request.

**Key Idea**: Before granting a resource request, check if granting would lead to an unsafe state. If so, delay the request.

**Safe vs. Unsafe States**:

* **Safe State**: There exists a sequence of process executions that allows all processes to finish without deadlocking
  * Even if processes act maliciously (request maximum resources)
  
* **Unsafe State**: No guaranteed sequence; deadlock is possible

**Banker's Algorithm** (Dijkstra)

A classic deadlock avoidance algorithm.

**Data Structures**:
* `Available[m]`: Available resources of each type
* `Max[n][m]`: Maximum demand of each process for each resource type
* `Allocation[n][m]`: Currently allocated resources to each process
* `Need[n][m]`: Remaining resources needed by each process = Max - Allocation

**Safety Algorithm** (checks if state is safe):

```
1. Work = Available
2. Finish[i] = FALSE for all i
3. Find index i such that:
   - Finish[i] == FALSE
   - Need[i] â‰¤ Work
   If found, go to step 4; otherwise go to step 5
4. Work = Work + Allocation[i]
   Finish[i] = TRUE
   Go to step 3
5. If Finish[i] == TRUE for all i, then system is in safe state
   Otherwise, system is in unsafe state
```

**Resource Request Algorithm**:

```
If Request[i] > Need[i]:
    Error (exceeded maximum claim)

If Request[i] > Available:
    Process waits

Otherwise:
    Tentatively allocate resources
    Run Safety Algorithm
    If safe state:
        Allocate resources permanently
    Else:
        Restore old state and process waits
```

**Example**: 
```
System State:
Available: [3, 3, 2]
Max:       [[7,5,3], [3,2,2], [9,0,2], [2,2,2], [4,3,3]]
Allocation: [[0,1,0], [2,0,0], [3,0,2], [2,1,1], [0,0,2]]
Need:      [[7,4,3], [1,2,2], [6,0,0], [0,1,1], [4,3,1]]

Process P1 requests [0,2,0]
Can grant? Check if system remains safe after allocation
```

**Limitations**:
* Requires knowledge of maximum resource needs in advance
* Processes rarely know maximum needs
* Too restrictive (may delay requests unnecessarily)

**3. Deadlock Detection**

This approach allows the system to enter a deadlock state but detects and recovers from it.

**Detection Algorithm**:

Similar to Safety Algorithm but uses current Allocation and Wait states:
* Create a Wait-For graph where processes are nodes
* Edge P â†’ Q if P is waiting for a resource held by Q
* Deadlock exists if and only if Wait-For graph has a cycle

**Implementation**:

```
Every T time units:
1. Run deadlock detection algorithm
2. If cycle found in resource allocation graph:
   - System is in deadlock
   - Invoke recovery procedure
```

**Trade-offs**:
* Allows more processes to run and complete
* Recovery can be expensive
* Detection frequency affects overhead vs. detection delay

**4. Deadlock Recovery**

If deadlock is detected, several recovery options exist:

**Option A: Process Termination**
* **Terminate all deadlocked processes**: Simple but expensive
* **Terminate processes one at a time until cycle is broken**: Better but need abort order
  * Terminate process requiring least rollback
  * Terminate process with least priority
  * Terminate process with least resources allocated

**Option B: Resource Preemption**
* Preempt resources from a deadlocked process
* Rollback process to state before resource allocation
* Restart process
* Problem: Determining which process to preempt and how far to rollback

**Choice of Method**:

| Method | When to Use | Pros | Cons |
|--------|-----------|------|------|
| **Prevention** | Simple systems | No detection needed | Low resource utilization |
| **Avoidance** | Small systems | Good utilization | Need advance knowledge |
| **Detection** | Complex systems | Allows concurrency | Expensive recovery |

**Practical Approaches**:
* Most modern OSs use **combination** of approaches
* Use prevention for resources like tape drives (mutual exclusive)
* Use avoidance for memory allocation
* Use detection + recovery in extreme cases

### 3.4 Exam Tips & Important Questions

**Key Concepts to Memorize**:

* **Critical Section**: Code segment where shared data is accessed
* **Race Condition**: Non-deterministic outcome due to unsynchronized concurrent access
* **Mutual Exclusion**: Only one process in critical section at a time
* **Deadlock**: Permanent blocking due to circular wait
* **Safe State**: System guarantees no deadlock
* **Semaphore**: Integer variable for synchronization
  * Binary semaphore: 0 or 1 (like mutex)
  * Counting semaphore: unrestricted domain
* **Banker's Algorithm**: Deadlock avoidance using safety checking

**Common Exam Mistakes**:

* Confusing deadlock conditions - need ALL FOUR
* Forgetting that bankers algorithm is avoidance, not detection
* Not understanding that deadlock prevention causes low efficiency
* Mixing up wait() and signal() operations on semaphores
* Not drawing resource allocation graphs correctly
* Forgetting bounded waiting requirement in critical section solution

**Key Connections**:

* Synchronization is fundamental to Process Management (Unit II)
* Without proper synchronization, concurrent processes cannot share data safely
* Deadlock is an extreme manifestation of synchronization problems
* All four deadlock conditions must hold for deadlock to occur

**Potential Exam Questions**:

* "Define the critical-section problem and list its three requirements."
* "Compare mutex locks and semaphores. When would you use each?"
* "Explain Peterson's solution to the critical-section problem. What are its limitations?"
* "What are the four necessary conditions for deadlock? Explain each."
* "Explain the difference between deadlock prevention and deadlock avoidance."
* "Describe the Banker's algorithm and explain how it prevents deadlock."
* "Draw a resource allocation graph showing a deadlock scenario."
* "Solve a producer-consumer problem using semaphores."
* "Solve the dining philosophers problem and explain the solution."
* "How would you detect and recover from deadlock?"
* "What is the purpose of monitors in synchronization?"
* "Explain bounded waiting and why it's important."

**Calculation Quick Tips**:

For Banker's Algorithm:
```
Need[i] = Max[i] - Allocation[i]
Check if Need[i] â‰¤ Work for any process
If yes, simulate resource allocation and check if all can finish
```

---

## Summary of Important Formulas and Key Points

### UNIT-I

* **System Call**: Programmatic interface to OS services; causes mode switch
* **Dual Mode**: Mode bit = 0 (kernel), Mode bit = 1 (user)
* **Timer Interrupt**: Ensures OS maintains control
* **OS Structures**: Simple, Layered, Microkernel, Modular

### UNIT-II

```
Turnaround Time = Completion Time - Arrival Time
Waiting Time = Turnaround Time - Burst Time
Average WT = Î£(Waiting Times) / Number of Processes
Average TAT = Î£(Turnaround Times) / Number of Processes

Process States: New â†’ Ready â†’ Running â†’ Waiting â†’ Terminated

Scheduling Optimality:
SRTF < Non-preemptive SJF < FCFS (in terms of average waiting time)
```

### UNIT-III

* **Four Deadlock Conditions**: Mutual Exclusion, Hold and Wait, No Preemption, Circular Wait
* **Critical Section Requirements**: Mutual Exclusion, Progress, Bounded Waiting
* **Banker's Algorithm**: Avoidance technique using safety checking
* **Semaphores**: wait() decrements, signal() increments

---

## Revision Checklist for Exam

- [ ] Can I explain what an OS is and its four main components?
- [ ] Do I understand dual-mode operation and mode switching?
- [ ] Can I list and explain 5 types of system calls?
- [ ] Do I understand the difference between multiprogram and time-sharing?
- [ ] Can I describe all process states and transitions?
- [ ] Can I explain what a PCB contains and why each field matters?
- [ ] Can I solve CPU scheduling problems (FCFS, SJF, SRTF, Priority, RR)?
- [ ] Do I understand context switches and their overhead?
- [ ] Can I compare different threading models?
- [ ] Do I understand IPC (shared memory vs. message passing)?
- [ ] Can I explain the critical section problem and its solutions?
- [ ] Can I solve producer-consumer and dining philosopher problems?
- [ ] Can I list the four deadlock conditions?
- [ ] Do I understand deadlock prevention vs. avoidance?
- [ ] Can I apply Banker's algorithm?
- [ ] Can I identify deadlocks in resource allocation graphs?

---

**End of Comprehensive Study Notes**

*Use this document for comprehensive exam preparation. Focus on understanding concepts rather than just memorization. Practice solving problems multiple times to build confidence.*
