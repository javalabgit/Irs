# Operating Systems: Exam Quick Reference & Cheat Sheet

## UNIT-I: OS Overview - Quick Facts

### Core Definitions
- **OS**: Interface between hardware and users; manages resources efficiently
- **Program**: Passive entity (file on disk)
- **Process**: Active entity (running program in memory)

### Four Components of Computer System
1. **Hardware** - CPU, Memory, I/O devices
2. **Operating System** - Manager and controller
3. **Application Programs** - User-facing software
4. **Users** - People/machines using the system

### OS Core Functions - REMEMBER: P-M-S (Process, Memory, Storage)
1. **Process Management** - Create, delete, schedule, synchronize processes
2. **Memory Management** - Track, allocate, deallocate memory
3. **Storage Management** - Files, disks, caching

### Multiprogramming vs. Time-Sharing
| Aspect | Multiprogramming | Time-Sharing |
|--------|------------------|--------------|
| **Goal** | Max CPU utilization | Interactive computing |
| **Switching** | On I/O wait | On timer interrupt |
| **User Input** | No | Yes (real-time) |

### Dual-Mode Operation - CRITICAL CONCEPT
- **Mode Bit 0** = KERNEL MODE (Privileged, unlimited access)
- **Mode Bit 1** = USER MODE (Restricted, limited access)
- **Mode Switch Mechanism**: System call/Trap instruction
- **Timer**: Prevents process monopolizing CPU

### System Call Categories - REMEMBER: P-F-D-I-C
1. **Process Control** (end, abort, create, terminate, wait)
2. **File Management** (create, delete, open, close, read, write)
3. **Device Management** (request, release, read, write)
4. **Information Maintenance** (get/set time, date, system data)
5. **Communications** (send, receive, create connection)

### OS Structure Types
| Type | Pros | Cons |
|------|------|------|
| **Simple** | Easy, fast | Unsafe, unstructured |
| **Layered** | Modular, debug-friendly | Overhead, inefficient |
| **Microkernel** | Extensible, secure, reliable | Performance overhead |
| **Modular** | Flexible, maintainable | Complex to implement |

### Key Formulas (Unit I)
```
None - mostly conceptual, but understand mode bits and timer concepts
```

---

## UNIT-II: Processes & CPU Scheduling - Quick Facts

### Process Memory Layout - REMEMBER: T-D-H-S (Top Down)
```
HIGH ADDRESS â†’ Stack (grows down) â†“
             â†’ Heap (grows up) â†‘
             â†’ BSS (uninitialized data)
             â†’ Data (initialized globals)
             â†’ Text (code)
LOW ADDRESS
```

### Five Process States - REMEMBER: N-R-R-W-T
1. **New** â†’ Process created
2. **Ready** â†’ In memory, waiting for CPU
3. **Running** â†’ Executing on CPU
4. **Waiting** â†’ Waiting for I/O/event
5. **Terminated** â†’ Process finished

### Process Control Block (PCB) - What's Inside?
- Process state
- Program counter
- CPU registers
- CPU scheduling info (priority, queues)
- Memory management info (base/limit registers, page tables)
- Accounting info (CPU time used)
- I/O status info (devices, open files)

### Process Scheduling - Three Scheduler Types
| Scheduler | Frequency | Role |
|-----------|-----------|------|
| **Long-term** | Low (sec-min) | Job pool â†’ Memory (controls multiprogramming degree) |
| **Short-term** | High (ms) | Ready queue â†’ CPU (most impact on performance) |
| **Medium-term** | Medium | Memory â†” Disk (swap in/out) |

### Context Switch
- **Definition**: Save old process state (PCB) + load new process state
- **Overhead**: 1-1000 microseconds + cache misses + TLB misses
- **Impact**: Significant on system performance

### Key Concept: IPC Models
**Shared Memory**:
- Fast (memory speed)
- Less secure
- Requires explicit synchronization

**Message Passing**:
- Slower (system calls)
- More secure
- Synchronization built-in

### Threading Models - REMEMBER: M-O-M (Many-One, One-One, Many-Many)
| Model | User Threads | Kernel Threads | Parallelism | Pros | Cons |
|-------|-------------|----------------|------------|------|------|
| **Many-to-One** | Many | 1 | No | Cheap | Blocking blocks all |
| **One-to-One** | N | N | Yes | True concurrency | Expensive |
| **Many-to-Many** | Many | Fewer | Yes | Best balance | Complex |

### CPU Scheduling Metrics - REMEMBER: U-T-T-W-R
1. **Utilization** - % time CPU busy (higher better)
2. **Throughput** - Processes/time (higher better)
3. **Turnaround Time** - Submission to completion (lower better)
4. **Waiting Time** - Time in ready queue (lower better)
5. **Response Time** - Submission to first response (lower better)

### CPU Scheduling Algorithms - REMEMBER: F-S-P-R-M-M

#### 1. **FCFS** (First-Come, First-Served)
- Non-preemptive
- Simple but poor avg WT (convoy effect)
- Formula: FCFS usually worst WT

#### 2. **SJF** (Shortest-Job-First)
- Non-preemptive version: Optimal WT
- Preemptive version: SRTF (Shortest-Remaining-Time-First)
- SRTF < Non-preemptive SJF < FCFS (in terms of WT)
- Problem: Need to know/predict burst time

#### 3. **Priority Scheduling**
- Can be preemptive or non-preemptive
- Problem: Starvation (low priority never runs)
- Solution: Aging (gradually increase waiting process priority)

#### 4. **Round Robin** (RR)
- Preemptive
- Each process gets time quantum q
- Fair but not optimal WT
- Small q: more context switches (overhead)
- Large q: approaches FCFS

#### 5. **Multilevel Queue**
- Separate queues for different process types
- Each queue has own algorithm
- Scheduling among queues (fixed priority or time-share)

#### 6. **Multilevel Feedback Queue** (Most Complex)
- Processes can move between queues
- Separates short/long CPU burst processes
- Implements aging to prevent starvation
- Most flexible but complex

### Key Scheduling Formulas - MUST KNOW
```
Turnaround Time (TAT) = Completion Time - Arrival Time
Waiting Time (WT) = Turnaround Time - Burst Time
= Completion Time - Arrival Time - Burst Time

Average WT = Î£(All WT) / Number of Processes
Average TAT = Î£(All TAT) / Number of Processes

Optimal for WT: SRTF < SJF < Priority (if set well) < RR < FCFS
```

### Exam Problem-Solving Approach for Scheduling
1. **Draw timeline** (0 to completion of last process)
2. **Mark arrival times** on timeline
3. **Follow algorithm rules** for process selection
4. **Calculate completion times** from Gantt chart
5. **Calculate TAT** (Completion - Arrival)
6. **Calculate WT** (TAT - Burst)
7. **Calculate averages**

### Common Scheduling Mistakes to Avoid
- âŒ Forgetting arrival times in calculations
- âŒ Confusing SJF (non-preemptive) with SRTF (preemptive)
- âŒ Not updating queue order in RR
- âŒ Confusing burst time with waiting time
- âŒ Allowing invalid process moves between queues

---

## UNIT-III: Synchronization & Deadlocks - Quick Facts

### The Critical Section Problem - Three Requirements

1. **Mutual Exclusion**: 
   - Only ONE process in critical section at a time
   - If Pi in CS, then no other Pj can be in CS

2. **Progress**: 
   - If no process in CS and some want to enter
   - Only processes NOT in remainder section decide
   - Decision cannot be indefinitely postponed

3. **Bounded Waiting**: 
   - Limit on times OTHER processes enter after request
   - Prevents starvation
   - No process waits forever

### Process Structure with Critical Section
```
do {
    ENTRY SECTION          // Acquire lock/semaphore
    CRITICAL SECTION       // Access shared data
    EXIT SECTION           // Release lock/semaphore
    REMAINDER SECTION      // Other work
} while(TRUE);
```

### Synchronization Tools

#### Mutex Lock (Mutual Exclusion)
```
acquire() { while (!available); available = FALSE; }
release() { available = TRUE; }
```
- Binary: locked (1) or unlocked (0)
- Simple but can cause busy waiting

#### Semaphore - CRITICAL UNDERSTANDING
```
wait(S) { S--; if (S<0) block this process; }
signal(S) { S++; if (Sâ‰¤0) wakeup(P); }
```

**Binary Semaphore** (S = 0 or 1): Like mutex, provides mutual exclusion
**Counting Semaphore** (S â‰¥ 0): Controls access to multiple resource instances

Example:
```
S = 3 means 3 resources available
Each wait(S) decrements (process claims resource)
Each signal(S) increments (process releases resource)
If S < 0, processes wait in queue
```

#### Monitor
- High-level synchronization construct
- Automatically provides mutual exclusion
- Encapsulates shared data and operations
- Uses condition variables (wait/signal)

### Four Necessary Conditions for Deadlock - ALL MUST HOLD

1. **Mutual Exclusion**:
   - At least one resource is non-sharable
   - Only one process can use it at a time

2. **Hold and Wait**:
   - Process holds resource AND waits for another
   - Can accumulate resources while waiting

3. **No Preemption**:
   - Resource released only voluntarily by holder
   - OS cannot forcibly take resources

4. **Circular Wait**:
   - Cycle in resource request/allocation
   - P0 â†’ R0 â†’ P1 â†’ R1 â†’ ... â†’ P0

**CRITICAL**: ALL FOUR must be true for deadlock!

### Classic Synchronization Problems

#### Producer-Consumer (Bounded Buffer)
- Producer creates items â†’ Buffer â†’ Consumer uses items
- Semaphores: empty (free slots), full (filled slots), mutex
- âŒ Producer on full buffer
- âŒ Consumer on empty buffer

#### Readers-Writers
- Multiple readers can access simultaneously
- Writers need exclusive access
- Track readcount + mutex
- Issue: Writer starvation possible

#### Dining Philosophers
- 5 philosophers, 5 chopsticks
- Each needs both chopsticks to eat
- âŒ Deadlock if all grab left chopstick first
- Solution: Asymmetric (some grab right first) or resource ordering

### Deadlock Handling Methods

#### 1. Prevention (Make at least ONE condition false)
- **Prevent Mutual Exclusion**: Make resources sharable (not always possible)
- **Prevent Hold-and-Wait**: Require all resources upfront OR release before requesting new
- **Prevent No Preemption**: Allow preemption (difficult for most resources)
- **Prevent Circular Wait**: Total ordering of resources (request in order)

**Trade-off**: Low resource utilization, reduced throughput

#### 2. Avoidance (Don't enter unsafe state)
- Requires knowing max resource needs in advance
- **Safe State**: Exists sequence to complete all processes
- **Unsafe State**: No guaranteed sequence (deadlock possible)

**Banker's Algorithm**: 
```
Before granting request:
1. Check if Need[i] â‰¤ Available for some process i
2. Simulate allocation and free that process
3. If all can finish: SAFE, grant request
4. Else: UNSAFE, process waits
```

#### 3. Detection (Allow deadlock, then detect)
- Run detection algorithm periodically
- Build Wait-For graph (P â†’ Q if P waits for resource held by Q)
- Deadlock exists âŸº Cycle in graph

#### 4. Recovery (Remove from deadlock)
- **Process termination**: Abort all or one by one until cycle broken
- **Resource preemption**: Take resources and rollback process

**Best approach**: Combination of methods based on system requirements

### Resource Allocation Graph
- **Nodes**: Processes (circles), Resources (squares)
- **Edges**:
  - P â†’ R (request edge): Process waiting for resource
  - R â†’ P (allocation edge): Resource allocated to process
- **Deadlock**: Cycle exists in graph

### Key Deadlock Formulas
```
Safe State = âˆƒ sequence where all processes can complete
Deadlock Detection = Cycle exists in Wait-For graph
```

### Exam Problem-Solving for Synchronization
1. **Identify shared resources**
2. **Identify critical sections**
3. **Determine correct synchronization tool**
4. **Verify mutual exclusion, progress, bounded waiting**
5. **Check for potential deadlock**

### Exam Problem-Solving for Deadlock
1. **Check if ALL FOUR conditions present**
2. **Draw resource allocation graph**
3. **Identify cycles**
4. **Choose handling method appropriate to scenario**
5. **Explain trade-offs**

### Common Mistakes to Avoid
- âŒ Saying deadlock can occur if only 3 of 4 conditions hold
- âŒ Confusing semaphore wait/signal
- âŒ Forgetting to initialize semaphores correctly
- âŒ Not recognizing when processes can deadlock
- âŒ Incorrect resource allocation graph

---

## Master Study Summary Table

| Concept | Key Formula/Definition | Where It Appears | Exam Frequency |
|---------|----------------------|------------------|----------------|
| **Process States** | Newâ†’Readyâ†’Runningâ†’Waitingâ†’Terminated | Unit II | Very High |
| **Turnaround Time** | Completion - Arrival | Unit II | Very High |
| **Waiting Time** | TAT - Burst Time | Unit II | Very High |
| **Context Switch** | Time to save/restore state | Unit II | High |
| **Mode Bit** | 0=Kernel, 1=User | Unit I | High |
| **System Call** | Interface to OS services | Unit I | High |
| **Mutual Exclusion** | Only one process in CS | Unit III | Very High |
| **Deadlock** | ALL FOUR conditions | Unit III | Very High |
| **Safe State** | All processes can complete | Unit III | High |
| **PCB** | Data structure for process info | Unit II | High |

---

## Final Exam Tips

### Time Management
- **Conceptual Questions** (5 mins each): Define, explain, compare
- **Problem-Solving** (10-15 mins each): Gantt charts, calculations, graphs
- **Total**: Budget accordingly based on question distribution

### Answer Organization
1. State what you're about to do
2. Show all intermediate steps
3. Clearly mark final answer
4. Explain your reasoning

### Common Exam Question Types

**Type 1: "Define and Explain"**
- Use definition + real example + why it matters

**Type 2: "Compare/Contrast"**
- Use table format for clarity
- Highlight key differences

**Type 3: "Draw and Label"**
- Use clear labels
- Show all components
- Explain what diagram represents

**Type 4: "Calculate"**
- Show all work step-by-step
- Include units
- Verify reasonableness

**Type 5: "Solve Problem"**
- Draw visual representation
- Apply algorithm systematically
- Double-check calculations

### What to Do If Stuck
1. **Stuck on definition?** â†’ Describe what you know + real-world example
2. **Stuck on calculation?** â†’ Show your work, partial credit likely
3. **Stuck on concept?** â†’ Explain related concepts, show understanding
4. **Stuck on choice?** â†’ Explain trade-offs, choose and justify

### Last-Minute Review (30 mins before exam)
- [ ] Review all process states
- [ ] Review all scheduling algorithms names
- [ ] Review four deadlock conditions
- [ ] Review three critical section requirements
- [ ] Verify all formulas
- [ ] Mental rehearsal of 2-3 problem types

---

## Formulas Quick Reference Card

```
UNIT-II CALCULATIONS:
TAT = Completion Time - Arrival Time
WT = TAT - Burst Time
Avg WT = Î£ WT / n
Avg TAT = Î£ TAT / n

UNIT-III CONCEPTS (Not formulas, but key understanding):
Deadlock âŸº ALL FOUR conditions + Circular Wait
Safe State âŸº Process sequence to complete all without deadlock
Banker's Algorithm: Check Need[i] â‰¤ Available
```

---

## Best of Luck! 

**Remember**:
1. Read questions carefully - they often have tricks
2. Draw diagrams when asked - never skip this
3. Show work - partial credit is better than no credit
4. Double-check calculations - easy mistakes lose points
5. Manage time - don't spend 20 mins on 5-point question
6. Answer what's asked - don't add unnecessary info

**You got this! ðŸ’ª**