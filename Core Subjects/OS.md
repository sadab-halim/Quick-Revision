# Operating Systems

<details>
  <summary>01: Basics</summary>

### Basics of Operating Systems

An Operating System (OS) is system software that acts as an interface between the computer hardware and the user. Its primary goals are to manage hardware resources efficiently, provide abstractions for complex hardware, and offer a user-friendly environment to execute programs.

### Operating System Introduction

The OS controls and coordinates the use of hardware among various applications and users.

* **Core Functions:**
  * **Process Management:** Creating, deleting, suspending, and resuming processes.
  * **Memory Management:** Allocating and deallocating memory space to programs.
  * **File System Management:** Organizing files and directories on storage devices.
  * **I/O Device Management:** Managing communication with hardware devices like keyboards, printers, and disk drives.
  * **Security:** Protecting system resources through user authentication and access control.
* **Dual-Mode Operation (IMP):** The OS operates in two modes to protect itself and system resources.
  * **User Mode:** The mode in which user applications run. It has limited access to hardware.
  * **Kernel Mode (Supervisor Mode):** The mode in which the OS kernel runs. It has privileged access to all hardware and memory. A **mode bit** (0 for kernel, 1 for user) in the hardware indicates the current mode. Transitions from user to kernel mode occur via system calls, interrupts, or exceptions.


### Process, Program, and Thread (IMP)

These terms describe different states of software on a computer system. Understanding their differences is crucial.


| Feature | Program | Process | Thread |
| :-- | :-- | :-- | :-- |
| **Nature** | Passive entity. A set of instructions. | Active entity. A program in execution. | A segment of a process. Basic unit of CPU execution. |
| **Location** | Stored on a secondary storage device (disk). | Resides in main memory (RAM). | Part of a process, sharing its memory space. |
| **Components** | Code and static data. | Code, data, stack, heap, and a Process Control Block (PCB). | Its own stack, registers, and program counter. Shares code, data, and files with other threads in the same process. |
| **Analogy** | A recipe written in a cookbook. | A chef actively cooking the recipe. | A single step in the recipe, like chopping vegetables. Multiple chefs (threads) can work on different steps of the same recipe (process) simultaneously. |

### Types of Operating Systems

Operating systems can be classified based on their processing capabilities and intended applications.

### Batch OS, Multiprogramming OS, and Multitasking OS

* **Batch OS:**
  * Jobs with similar needs were batched together and executed sequentially.
  * There was no direct user interaction. The CPU was often idle if a job needed to perform I/O.
  * **Real-world Example:** Early payroll systems or bank statement generation.
* **Multiprogramming OS:**
  * A refinement of batch systems that keeps multiple jobs in memory at once.
  * When one job waits for an I/O operation, the OS switches the CPU to another ready job, maximizing CPU utilization.
  * This is a foundational concept for all modern general-purpose operating systems.
* **Multitasking (Time-Sharing) OS (IMP):**
  * A logical extension of multiprogramming that allows interactive use.
  * The CPU switches between jobs so frequently (using a **time slice** or **quantum**) that users can interact with each program while it is running.
  * **Best Practice:** The time quantum must be carefully chosen. Too short, and context switching overhead becomes significant. Too long, and the system feels less responsive.
  * **Real-world OS:** Windows, macOS, and Linux are all multitasking systems.


### Multiprocessing OS and Real-time OS

* **Multiprocessing OS:**
  * Manages a system with two or more CPUs working in close communication.
  * **Symmetric Multiprocessing (SMP):** (IMP) Each processor runs an identical copy of the OS, and they communicate as needed. This is the standard in modern multi-core PCs.
  * **Asymmetric Multiprocessing (ASMP):** One processor acts as the master, controlling the system, while others are slaves.
  * **Benefit:** Increases throughput by executing more processes in parallel.
* **Real-time OS (RTOS) (IMP):**
  * Designed for systems where computations must be completed within strict time constraints.
  * **Hard Real-time:** Deadlines are absolute. Missing a deadline constitutes a system failure. **Analogy:** The control system for a car's airbag must deploy it within milliseconds of a crash.
  * **Soft Real-time:** Missing a deadline is undesirable but not catastrophic; it just degrades performance. **Analogy:** In live video streaming, a few dropped frames (missed deadlines) are acceptable.


### Distributed, Clustered, and Embedded OS

* **Distributed OS:**
  * Manages a collection of autonomous, networked computers and makes them appear as a single, coherent system.
  * Users are unaware of which machine is running their process or where their data is stored.
  * **Goal:** Provide resource sharing and high performance.
* **Clustered OS:**
  * A group of tightly-coupled computers that work together as a single system to provide high availability and/or load balancing.
  * If one node fails, another takes over its tasks (**failover**).
  * **Real-world Example:** A web server farm behind a major website like Google or Amazon.
* **Embedded OS:**
  * A specialized OS designed to perform a dedicated function for a device. They are highly optimized for size, power consumption, and reliability.
  * **Real-world OS:** FreeRTOS used in IoT devices, QNX in car infotainment systems, or the OS in your smart TV or digital watch.


</details>

---

<details>
  <summary>02: Process Management</summary>

### Section 2: Process Management

Process management is a fundamental function of the OS that involves creating, scheduling, and terminating processes, and providing mechanisms for synchronization and communication among them.

### Process and Its States (IMP)

A process is a program in execution. As it executes, it changes state. The main states of a process are :[^3_1][^3_2]

* **New:** The process is being created.[^3_3]
* **Ready:** The process is in main memory, waiting to be assigned to a CPU for execution.[^3_4][^3_3]
* **Running:** Instructions are being executed by the CPU.[^3_4]
* **Waiting (or Blocked):** The process is waiting for some event to occur, such as an I/O completion or receiving a signal.[^3_3]
* **Terminated:** The process has finished execution.[^3_3]

Some operating systems also use **Suspend Ready** and **Suspend Wait** states, where a process is swapped out of main memory to secondary storage to free up RAM, typically for higher-priority processes.[^3_3]

**State Transition Diagram Analogy:** Think of ordering a pizza.

* **New:** You've decided what to order.
* **Ready:** You've placed the order and are waiting for it to be cooked.
* **Running:** The chef is actively making your pizza.
* **Waiting:** The chef needs more cheese and has to wait for a new block to be delivered (I/O operation).
* **Terminated:** The pizza is ready and has been delivered to you.


### Process Control Block (PCB) (IMP)

The **Process Control Block (PCB)** is a data structure maintained by the OS for every process. It acts as the process's passport, containing all the essential information the OS needs to manage it.[^3_5][^3_6]

**Key Information in a PCB :**[^3_5]

* **Process State:** The current state (e.g., ready, running, waiting).
* **Process ID (PID):** A unique identifier for the process.
* **Program Counter (PC):** The address of the next instruction to be executed.
* **CPU Registers:** A snapshot of all CPU registers (accumulators, index registers, stack pointers).
* **CPU Scheduling Information:** Process priority, pointers to scheduling queues.
* **Memory-Management Information:** Value of base and limit registers, page tables, or segment tables.
* **Accounting Information:** CPU time used, time limits, account numbers.
* **I/O Status Information:** List of I/O devices allocated to the process, open files.

**Best Practice:** The PCB is critical for context switching. Any corruption in a PCB could lead to system-wide instability.

### Context Switching (IMP)

**Context switching** is the mechanism the OS uses to switch the CPU from one process to another. It is a core feature of a multitasking operating system.[^3_7][^3_8]

**When does it happen?**

1. A high-priority process arrives.
2. An interrupt occurs (e.g., I/O completion).
3. The time slice for the current process expires.
4. The process makes a system call or voluntarily yields the CPU.

**The process involves :**[^3_7]

1. **Saving the context** of the current process (its state, PC, CPU registers) into its PCB.
2. **Loading the context** of the new process from its PCB.
3. Resuming execution of the new process.

* **Common Pitfall:** Context switching is pure overhead; the system does no useful work during the switch. Frequent switching can degrade performance.[^3_8]
* **Real-world Note:** Switching between **threads** of the same process is much faster than switching between processes because threads share the same memory space, so memory management information doesn't need to be reloaded.[^3_7]


### User Mode and Kernel Mode (IMP)

The OS uses two separate modes of operation to protect itself and system components from faulty user programs.[^3_9]


| Aspect | User Mode | Kernel Mode (System/Privileged Mode) |
| :-- | :-- | :-- |
| **Privilege Level** | Low. Restricted access. | High. Unrestricted access to all hardware and memory [^3_9]. |
| **What Runs Here?** | User applications (e.g., browser, text editor). | The OS kernel, device drivers, and system services [^3_10]. |
| **Hardware Access** | Indirect. Must use system calls to request services from the kernel [^3_9]. | Direct access to all hardware and memory addresses. |
| **Crash Impact** | A crash usually only affects the single application. | A crash is catastrophic and can bring down the entire system [^3_9]. |
| **Mode Bit** | `1` | `0` |

A **system call** is the mechanism used by an application to request a service from the OS kernel. This causes a trap, switching the CPU from user mode to kernel mode to fulfill the request.[^3_9]

### Scheduling Queues and Schedulers in OS

The OS maintains queues to manage processes at different stages.[^3_11][^3_12]

* **Job Queue:** Contains all processes in the system.
* **Ready Queue:** Contains all processes residing in main memory, ready and waiting to execute.
* **Device Queues:** A list of processes waiting for a particular I/O device.

**Schedulers** are special system software that handle process scheduling:

* **Long-Term Scheduler (or Job Scheduler):** Selects which processes should be brought from the job queue into the ready queue. It controls the degree of multiprogramming.
* **Short-Term Scheduler (or CPU Scheduler):** (IMP) Selects which process should be executed next and allocates the CPU. It is invoked very frequently (milliseconds) and must be fast.[^3_11]
* **Medium-Term Scheduler:** Handles swapping processes out of memory to reduce the degree of multiprogramming and later swapping them back in.


### Process Scheduling Algorithms, Preemptive vs. Non-Preemptive

Scheduling algorithms decide which of the processes in the ready queue is to be allocated the CPU.[^3_13]


| Scheduling Type | Description | Analogy | Examples |
| :-- | :-- | :-- | :-- |
| **Non-Preemptive** | Once the CPU has been allocated to a process, it keeps the CPU until it releases it, either by terminating or by switching to the waiting state [^3_14]. | A person at an ATM who uses it until their entire transaction is complete, no matter how long the line gets. | FCFS, SJF [^3_14]. |
| **Preemptive** | The CPU can be taken away from a process. A running process can be interrupted and moved to the ready queue by the OS [^3_14][^3_15]. | A doctor in an ER treating a patient with a minor injury might be interrupted to save a critical patient who just arrived. | SRTF, Round Robin, Priority [^3_16]. |

### Scheduling Algorithms (FCFS, SJF, SRTF)

* **First-Come, First-Serve (FCFS):** (Non-Preemptive)
  * The process that requests the CPU first is allocated the CPU first. It's implemented with a simple FIFO queue.[^3_17][^3_18]
  * **Common Pitfall (Convoy Effect) (IMP):** If one long process precedes many short processes, the short processes have to wait a long time, leading to poor average waiting time.
* **Shortest-Job-First (SJF):** (Non-Preemptive)
  * The CPU is allocated to the process with the smallest next CPU burst.
  * It is provably optimal, giving the minimum average waiting time for a given set of processes.
  * **Common Pitfall:** It's impossible to know the exact length of the next CPU burst. It's usually predicted (e.g., based on previous bursts). It can also lead to **starvation** for long processes.
* **Shortest-Remaining-Time-First (SRTF):** (Preemptive SJF)
  * If a new process arrives with a CPU burst length less than the remaining time of the current executing process, the CPU is preempted.
  * Like SJF, it can suffer from starvation of longer processes.


### Scheduling Algorithms (HRRN, RR, PBS, MLQ)

* **Highest Response Ratio Next (HRRN):** (Non-Preemptive)
  * A non-preemptive algorithm that corrects for the starvation in SJF. The priority of each job is calculated using the formula: `Priority = (Waiting Time + Burst Time) / Burst Time`.
  * Processes with shorter burst times get higher priority, but priority also increases as a process waits longer, preventing starvation.
* **Round Robin (RR):** (Preemptive) (IMP)
  * Designed for time-sharing systems. Each process gets a small unit of CPU time (a **time quantum** or **time slice**), usually 10-100 milliseconds. After this time has elapsed, the process is preempted and added to the end of the ready queue.
  * **Best Practice:** The quantum size is critical. Too large, and RR behaves like FCFS. Too small, and the overhead of context switching becomes too high.
* **Priority-Based Scheduling (PBS):** (Can be Preemptive or Non-Preemptive)
  * A priority number (integer) is associated with each process. The CPU is allocated to the process with the highest priority.
  * **Common Pitfall (Starvation) (IMP):** Low-priority processes may never execute. This can be solved by **aging**, a technique of gradually increasing the priority of processes that wait in the system for a long time.
* **Multilevel Queue (MLQ) Scheduling:**
  * The ready queue is partitioned into several separate queues, e.g., a **foreground (interactive)** queue and a **background (batch)** queue. Each queue has its own scheduling algorithm (e.g., RR for foreground, FCFS for background).
  * Scheduling must be done between the queues, typically implemented as fixed-priority preemptive scheduling.


### Threads in Operating System

A thread is a lightweight process, a basic unit of CPU utilization. It comprises a thread ID, a program counter, a register set, and a stack. It shares with other threads of the same process its code section, data section, and other OS resources like open files.

### Multithreading Models: User-Level vs Kernel-Level

These models describe the relationship between user-level threads (managed by a thread library) and kernel-level threads (managed by the OS).

* **Many-to-One Model:** Maps many user-level threads to a single kernel thread.
  * **Pro:** Thread management is fast as it's done in user space.
  * **Con (IMP):** If one thread makes a blocking system call, the entire process blocks. True parallelism is not possible on a multicore system.
* **One-to-One Model:** Maps each user thread to a kernel thread.
  * **Pro:** A blocking call by one thread does not affect others. Allows for true parallelism.
  * **Con:** Creating a user thread requires creating a corresponding kernel thread, which carries overhead.
  * **Real-world OS:** Windows and modern Linux distributions use this model.
* **Many-to-Many Model:** Multiplexes many user-level threads to a smaller or equal number of kernel threads.
  * Offers a compromise, allowing both concurrency and parallelism without the high overhead of the one-to-one model.


</details>

---

<details>
  <summary>03: Synchronization & Concurrency</summary>

### Section 3: Synchronization \& Concurrency

When multiple processes or threads run concurrently, they often need to share data and resources. Process synchronization refers to the mechanisms used to manage access to shared resources and ensure the orderly execution of cooperating processes to maintain data consistency.

### Process Synchronization \& its Tools

Cooperating processes can be affected by each other's execution. Without control, this can lead to a **race condition**, where the final outcome depends on the particular order in which concurrent threads/processes access and modify shared data.

* **Real-world Example:** Imagine two people trying to withdraw money from the same bank account at the same time.

1. Initial Balance: \$500.
2. Person A reads the balance (\$500) and decides to withdraw \$100.
3. Before Person A can update the balance, the OS switches to Person B.
4. Person B reads the balance (still \$500) and withdraws \$200. Person B's transaction completes, setting the balance to \$300.
5. The OS switches back to Person A. Person A's operation continues from where it left off, calculating \$500 - \$100 = \$400 and updating the balance.
  * **Result:** The final balance is \$400, but it should be \$200. \$100 has been "lost" due to the race condition.


### Critical Section Problem (IMP)

The **critical section** is a segment of code in a process that accesses shared resources. The critical section problem is to design a protocol that cooperating processes can use to ensure that when one process is executing in its critical section, no other process is allowed to execute in its critical section.

* **Analogy (Single-Person Restroom):** A critical section is like a single-person restroom.
  * **Mutual Exclusion:** Only one person can be inside at a time. (The primary goal).
  * **Progress:** If the restroom is empty and someone is waiting, they must be allowed to enter eventually. The decision of who goes next cannot be postponed indefinitely.
  * **Bounded Waiting:** There must be a limit on the number of times other people can enter the restroom after you've started waiting. You shouldn't have to wait forever.


### Semaphores \& their Types (IMP)

A **semaphore** is a simple integer variable used to solve the critical section problem. It is accessed only through two standard atomic operations: `wait()` and `signal()`.

* `wait(S)` or `P(S)`: Decrements the semaphore value. If the value becomes negative, the process is blocked and placed in a waiting queue.

```
wait(S) {
    while (S <= 0)
        ; // busy wait or block
    S--;
}
```

* `signal(S)` or `V(S)`: Increments the semaphore value. If there are processes waiting, one is unblocked.

```
signal(S) {
    S++;
}
```

* **Analogy (Study Rooms):** Imagine a library with 5 identical study rooms. The semaphore `S` is initialized to 5.
  * When a student wants a room, they perform `wait(S)`. `S` becomes 4.
  * When 5 students are in rooms, `S` is 0. The 6th student calls `wait(S)` and must wait because `S` is not positive.
  * When a student leaves a room, they perform `signal(S)`, incrementing `S` to 1 and allowing a waiting student to enter.

| Type | Description | Initial Value | Use Case |
| :-- | :-- | :-- | :-- |
| **Counting Semaphore** | The integer value can range over an unrestricted domain. | Can be any integer `N >= 0`. | Controlling access to a resource with `N` instances (like the study rooms). |
| **Binary Semaphore (Mutex)** | The integer value can only be 0 or 1. | Initialized to 1. | Providing mutual exclusion for a critical section (a resource with only one instance). |

* **Real-world OS:** Linux provides a rich set of semaphore APIs (`sem_init`, `sem_wait`, `sem_post`) for synchronization in both kernel and user space.


### Producer-Consumer Problem (IMP)

This is a classic synchronization problem. One or more **producers** generate data and place it into a shared buffer, while a single **consumer** takes items out of the buffer.

* **The Problem:** Ensure the producer doesn't try to add data to a full buffer and the consumer doesn't try to remove data from an empty buffer.
* **Solution using Semaphores:**
  * `mutex`: A binary semaphore to ensure mutual exclusion when accessing the buffer (initialized to 1).
  * `empty`: A counting semaphore to count the number of empty slots in the buffer (initialized to `buffer_size`).
  * `full`: A counting semaphore to count the number of filled slots in the buffer (initialized to 0).


### Deadlock (IMP)

**Deadlock** is a situation where two or more processes are blocked forever, each waiting for a resource held by another process in the same set.

* **Analogy (Two People on a Narrow Staircase):** Two people meet in the middle of a narrow staircase. Neither can move forward because the other is blocking the way, and neither is willing to back up. Both are stuck.

**Four Necessary Conditions for Deadlock:**

1. **Mutual Exclusion:** At least one resource must be held in a non-sharable mode.
2. **Hold and Wait:** A process holding at least one resource is waiting to acquire additional resources held by other processes.
3. **No Preemption:** A resource can be released only voluntarily by the process holding it.
4. **Circular Wait:** There exists a set of waiting processes {P0, P1, ..., Pn} such that P0 is waiting for a resource held by P1, P1 is waiting for a resource held by P2, ..., Pn is waiting for a resource held by P0.

### Methods for Handling Deadlock

1. **Deadlock Prevention:** Ensure that at least one of the four necessary conditions cannot hold. For example, break the "Hold and Wait" condition by requiring processes to request all their resources before execution begins.
2. **Deadlock Avoidance (IMP):** The OS is given advance information about which resources a process will need. It uses this to dynamically decide whether a request, if granted, could lead to a deadlock.
3. **Deadlock Detection and Recovery:** Allow the system to enter a deadlocked state, detect it, and then recover. Recovery might involve terminating one or more processes or preempting resources.

### Banker's Algorithm

This is the most famous **deadlock avoidance** algorithm.

* **Concept:** Before granting a resource request, the algorithm checks if granting it would leave the system in a **safe state**. A state is safe if there is at least one sequence of process executions that allows all processes to finish without causing a deadlock.
* **Analogy:** A banker with a fixed amount of cash only approves loans if they know that even if every customer requests their maximum credit line, there is an order in which they can be serviced. The banker won't grant a loan if it could lead to a situation where they can't fulfill their promises.
* **Common Pitfall:** Requires knowing the maximum resource needs of all processes in advance, which is often not practical in general-purpose operating systems.


### Starvation and Ageing

* **Starvation (Indefinite Blocking):** A process is ready to run but is perpetually overlooked by the scheduler. For example, in a priority-based scheduling system, a low-priority process might never get the CPU if there is a continuous stream of high-priority processes.
* **Ageing:** A solution to starvation. It is a technique of gradually increasing the priority of processes that have been waiting in the system for a long time. Eventually, the low-priority process will have its priority raised high enough to be scheduled.


</details>

---

<details>
  <summary>04: Memory Management</summary>

### Section 4: Memory Management

Memory management is the OS function responsible for managing the computer's primary memory (RAM). It keeps track of each memory location, determines how memory is allocated among competing processes, and deallocates memory when a process terminates.

### Memory Management Techniques: First Fit, Best Fit, Worst Fit

These are strategies for allocating memory from a list of free holes (partitions) in a **contiguous memory allocation** system.[^5_6]

* **Analogy (Parking Cars):** Imagine you are a valet trying to park cars of different lengths in various empty parking spots.
  * **First Fit:** You search the parking lot from the beginning and park the car in the *first* spot you find that is large enough. It's fast but can leave small, unusable holes.
  * **Best Fit:** You search the entire lot to find the *smallest* spot that is big enough for the car. This leaves the smallest possible leftover hole, but you have to search the whole list.
  * **Worst Fit:** You search the entire lot to find the *largest* spot and park the car there. The idea is that the leftover hole will be large enough to be useful. In practice, it's not a very effective strategy.

| Strategy | Description | Advantage | Disadvantage |
| :-- | :-- | :-- | :-- |
| **First Fit** | Allocate the first hole that is big enough. | Fast. | Tends to create small fragments at the beginning of memory. |
| **Best Fit** | Allocate the smallest hole that is big enough. | Tries to save large holes for large processes. | Can create tiny, unusable fragments. Slower due to exhaustive search. |
| **Worst Fit** | Allocate the largest hole. | Leftover hole is large and potentially more useful. | Tends to leave no large holes for future large processes. |

### Contiguous Allocation, Paging, and Segmentation (IMP)

These are the primary methods for mapping a process's logical address space to the physical address space of RAM.[^5_1]


| Technique | Description | Key Concept | Fragmentation | Analogy |
| :-- | :-- | :-- | :-- | :-- |
| **Contiguous Allocation** | Each process occupies a single, continuous block of memory [^5_6]. | Base and Limit registers define the process's address space. | Suffers from **external fragmentation** (unusable memory between allocated blocks). | A library where each book must be placed on a single, unbroken shelf long enough to hold it. Empty spaces between books on different shelves can't be combined. |
| **Paging** | Divides physical memory into fixed-size **frames** and logical memory into same-sized **pages**. A **page table** maps logical pages to physical frames. | The process's memory can be scattered across non-contiguous physical frames. | Suffers from **internal fragmentation** (unused space within the last allocated page/frame). | A book (process) is broken into fixed-size chapters (pages). These chapters can be stored on different shelves (frames) anywhere in the library. The table of contents (page table) tells you where each chapter is. |
| **Segmentation** | Divides a process's logical address space into variable-sized **segments** (e.g., code, data, stack). A **segment table** maps segments to physical memory locations. | The address space is a collection of logical segments, reflecting the programmer's view. | Suffers from **external fragmentation**, as segments are of variable sizes. | A book (process) is divided into logical parts like "Introduction," "Chapter 1," and "Appendix" (segments). Each part is kept whole but can be placed on different shelves. |

* **Paging vs. Segmentation:** Paging is transparent to the programmer, whereas segmentation is often visible. Many systems (like modern x86 processors) combine them into **paged segmentation**.


### Virtual Memory (IMP)

**Virtual Memory** is a memory management technique that provides a process with the illusion that it has a very large, private, contiguous main memory, when in fact its memory may be non-contiguous and partially held on secondary storage (like an SSD or HDD).[^5_5]

* **Key Idea:** Not all of a process needs to be in RAM at once. The OS can load only the necessary pages.
* **Implementation:** Usually implemented with **demand paging**, where a page is brought into memory only when it is needed (i.e., on "demand").
* **Analogy (A Large Desk and a Filing Cabinet):** Your desk (RAM) is small, but your filing cabinet (hard disk) is huge. You only keep the papers you're currently working on (active pages) on your desk. When you need a document from the cabinet (a non-resident page), you go get it and put it on your desk, possibly moving another document you're done with back to the cabinet.


### Page Fault

A **page fault** is a hardware interrupt (a trap) that occurs when a program tries to access a page that is mapped in its virtual address space but is not currently loaded in physical memory.

**Handling a Page Fault (IMP):**

1. The CPU traps to the OS.
2. The OS checks if the memory access was valid. If not, the process is terminated.
3. If valid, the OS finds a free frame in physical memory.
4. If there are no free frames, a **page replacement algorithm** is run to select a victim frame.
5. The OS schedules a disk operation to read the required page from disk into the (now free) frame.
6. The process's page table is updated.
7. The instruction that caused the fault is restarted.

### Page Replacement Algorithms (IMP)

When a page fault occurs and there are no free frames, the OS must decide which page in memory to swap out to disk to make room for the new page.


| Algorithm | Description | Analogy (Revising for an Exam) |
| :-- | :-- | :-- |
| **FIFO (First-In, First-Out)** | Replaces the page that has been in memory the longest. | You forget the first topic you studied, regardless of how recently you reviewed it. |
| **Optimal (OPT)** | Replaces the page that will not be used for the longest period of time in the future. | You have psychic powers and forget the topic you know you won't be tested on for the longest time. |
| **LRU (Least Recently Used)** | Replaces the page that has not been used for the longest period of time. | You forget the topic you haven't thought about in the longest time. |

* **Best Practice:** LRU is a good approximation of OPT and is widely used. It can be implemented with a stack or counters. FIFO is simple but performs poorly.


### Belady's Anomaly, Thrashing, Dynamic Binding

* **Belady's Anomaly (IMP):** A phenomenon where increasing the number of allocated page frames results in an *increase* in the number of page faults for certain page access sequences when using the FIFO page replacement algorithm. **This is a hot interview question.**
* **Thrashing (IMP):** A state where the system spends an excessive amount of time paging (swapping pages between memory and disk) instead of doing useful work. It occurs when a process does not have enough frames to hold its **working set** (the set of pages it is actively using).
  * **Symptom:** High page fault rate and low CPU utilization. The OS might mistakenly think it needs to increase the degree of multiprogramming, making the problem even worse.
  * **Solution:** Use a local page replacement algorithm (don't steal frames from other processes) and provide processes with enough frames for their working set.
* **Dynamic Binding:** The mapping from a logical address to a physical address is delayed until run time. This is essential for virtual memory, as the physical location of a page can change.


</details>

---

<details>
  <summary>05: File Systems</summary>

### Section 5: File Systems

A **File System** provides a structured way for the operating system to store, organize, and manage files on storage devices like hard drives and SSDs. It acts as an interface between the OS and the physical storage hardware, allowing users and applications to handle files efficiently.

### File Systems \& its Components

A file is a logical storage unit, a collection of related information. The file system manages files and directories.[^6_4]

**Layered Architecture (IMP):**

1. **Application Programs:** User-level programs that request file operations.
2. **Logical File System:** Manages metadata information, such as file names, directory structures, and access permissions. It handles the symbolic file names and maps them to their logical block numbers.[^6_5]
3. **Virtual File System (VFS):** (IMP) An abstraction layer that provides a common interface for multiple different file systems. This allows the OS to support various file system types (e.g., NTFS, ext4, APFS) seamlessly. In Linux, for example, the VFS allows you to mount different file systems into a single directory hierarchy.
4. **Physical File System:** Translates logical block addresses to physical block addresses and issues commands to the device driver to read/write those blocks on the storage device.[^6_5]

### Types of File Systems

Different operating systems use different file systems, each with unique features.[^6_1]


| File System | Primary OS | Key Features |
| :-- | :-- | :-- |
| **FAT (FAT16/FAT32)** | Older Windows, MS-DOS, many USB drives | Simple, widely compatible, but lacks modern features like permissions and journaling [^6_1]. |
| **NTFS** | Modern Windows (XP and later) | Supports large files, access control lists (permissions), file compression, and encryption. It is a journaling file system [^6_1]. |
| **ext (ext2/ext3/ext4)** | Linux | **ext4** is the default for most Linux distributions. It is a journaling file system with support for large volumes and files [^6_1]. |
| **APFS (Apple File System)** | macOS, iOS | Optimized for SSDs. Features strong encryption, space sharing, and crash protection [^6_1]. |

### File Allocation \& Deallocation (IMP)

This determines how disk blocks are allocated to files.

* **Contiguous Allocation:** Each file occupies a set of contiguous blocks on the disk.
  * **Pro:** Fast sequential access.
  * **Con:** Suffers from **external fragmentation**. It's difficult to find space for a new file and to grow an existing one.
* **Linked Allocation:** Each file is a linked list of disk blocks, which may be scattered anywhere on the disk. The directory contains a pointer to the first and last blocks.
  * **Pro:** No external fragmentation.
  * **Con:** Only efficient for sequential access. Random access is slow as one must traverse the list. Pointers also consume disk space.
* **Indexed Allocation:** Brings all pointers for a file together into one location: the **index block**. Each file has its own index block, which is an array of disk block addresses.
  * **Pro:** Solves the fragmentation and random access problems.
  * **Con:** Wastes space if the index block is too large for small files. For very large files, a single index block may not be enough (requiring linked schemes or multilevel indexes).
  * **Real-world OS:** The inode used in Unix-like systems is a form of indexed allocation.[^6_6]


### File Control Blocks (FCB) (IMP)

A **File Control Block (FCB)** is a data structure containing metadata about a file, such as ownership, permissions, size, and location of the data blocks.[^6_6]

* **In Unix-like systems, the FCB is called an inode.** It contains all metadata *except* the filename, which is stored in the directory entry.
* **Key information in an FCB/inode :**[^6_6]
  * File permissions (read, write, execute).
  * File ownership (owner, group).
  * File size.
  * Timestamps (creation, last access, last modification).
  * Pointers to the data blocks on disk.


### Access Control Lists (ACLs)

**ACLs** provide a more fine-grained way to control file access than standard Unix-style permissions (owner, group, other). An ACL is a list of permissions attached to an object (like a file). Each entry in the ACL, called an Access Control Entry (ACE), specifies a user or group and the permissions they have.

* **Example:** You could grant read/write access to `user_A`, read-only access to `group_B`, and deny access to everyone else for a specific file.
* **Real-world OS:** Windows NTFS is heavily based on ACLs. Linux also supports ACLs as an extension to its standard permission model.


### User Authentication Mechanisms

This is the process of verifying the identity of a user trying to access the system. Common methods include:

* **Passwords:** The most common method. The OS should store salted hashes of passwords, not the plaintext passwords themselves.
* **Biometrics:** Using unique physical characteristics like fingerprints, retina scans, or face recognition.
* **Smart Cards/Security Keys:** Physical tokens that a user must possess.
* **Multi-Factor Authentication (MFA):** Requires two or more verification methods (e.g., a password and a code from a mobile app).


### Encryption Techniques in File Systems

Encryption protects file confidentiality by making data unreadable without the correct key.

* **File-Level Encryption:** Individual files or folders are encrypted. The user often provides a password to decrypt them.
* **Full Disk Encryption (FDE):** The entire disk partition is encrypted. The key is typically required at boot time.
  * **Real-world Examples:** **BitLocker** on Windows, **FileVault** on macOS, and **LUKS** on Linux. This is a best practice for protecting data on laptops and portable devices.


### Backup and Recovery Mechanisms

These are essential for protecting against data loss due to hardware failure, software bugs, or user error.

* **Backup:** Creating a copy of data on a separate storage medium. Backups can be **full** (copying everything) or **incremental** (copying only what has changed since the last backup).
* **Journaling (IMP):** A technique used by modern file systems (NTFS, ext4, APFS) to improve reliability. Before making changes to the disk, the file system writes a description of what it is about to do to a special log, or **journal**. If the system crashes mid-operation, it can look at the journal upon reboot and either complete or undo the partial operations, bringing the file system back to a consistent state.


</details>

---

<details>
  <summary>06: Disk Management \& Scheduling</summary>

### Section 6: Disk Management \& Scheduling

Disk management involves initializing physical disks, partitioning them into logical volumes, and managing the space on those volumes. Disk scheduling is the process of deciding which pending I/O request to service next to optimize performance.

### Disk Scheduling and Algorithms (IMP)

On a multiprogramming system, multiple processes may have pending I/O requests for the same disk. The OS must choose an order to service these requests to improve efficiency. The primary goals are to minimize **seek time** (time for the disk arm to move to the correct cylinder) and **rotational latency** (time for the desired sector to rotate under the head). Seek time is the most significant component.

* **Analogy (Elevator Algorithm):** Think of the disk head as an elevator and the I/O requests as people on different floors waiting to be picked up. The goal is to service all the requests efficiently without moving the elevator randomly up and down.

**Common Disk Scheduling Algorithms:**


| Algorithm | Description | Pro | Con |
| :-- | :-- | :-- | :-- |
| **FCFS (First-Come, First-Served)** | Services requests in the order they arrive. | Fair; no starvation. | Inefficient. Can result in wild head swings, causing high seek times. |
| **SSTF (Shortest Seek Time First)** | Selects the request with the minimum seek time from the current head position. | Improves performance significantly over FCFS. | Can cause **starvation** for requests far from the current head position. |
| **SCAN (Elevator Algorithm)** | The disk arm starts at one end and moves toward the other end, servicing requests as it goes. When it reaches the end, it reverses direction. | Good performance. No starvation. | Favors requests in the middle cylinders over those at the ends. |
| **C-SCAN (Circular SCAN)** | Like SCAN, but when the head reaches the end, it immediately returns to the beginning of the disk without servicing any requests on the return trip. | Provides a more uniform wait time than SCAN because it treats all cylinders the same. |  |
| **LOOK \& C-LOOK** | A variation of SCAN/C-SCAN where the arm only goes as far as the last request in each direction, then reverses. It doesn't travel to the very end of the disk. | Avoids unnecessary travel to the ends of the disk, slightly improving efficiency. |  |

* **Best Practice:** LOOK and C-LOOK are the most common algorithms in practice as they provide good performance without starvation and are relatively simple to implement.


### RAID (Redundant Array of Independent Disks) (IMP)

RAID is a technology that combines multiple physical disk drives into a single logical unit to improve performance, provide data redundancy, or both.

**Common RAID Levels:**


| Level | Name | Description | Min. Disks | Redundancy? | Performance | Use Case |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| **RAID 0** | **Striping** | Data is split ("striped") across multiple disks. | 2 | No | **Excellent read/write.** Highest performance. | Video editing, caching. Any application where speed is critical and data loss is acceptable. |
| **RAID 1** | **Mirroring** | Data is duplicated ("mirrored") onto two or more disks. | 2 | Yes | **Excellent read**, normal write. | OS boot drives, critical databases. Applications needing high fault tolerance. |
| **RAID 5** | **Striping with Parity** | Data is striped across multiple disks, and a **parity** block is distributed among them. This parity information can be used to reconstruct data if one disk fails. | 3 | Yes | **Good read**, slower write (due to parity calculation). | General file servers, application servers. Good balance of performance, storage, and protection. |
| **RAID 6** | **Striping with Double Parity** | Similar to RAID 5 but uses two parity blocks, allowing it to survive the failure of **two** disks simultaneously. | 4 | Yes (High) | Good read, **very slow write** (due to dual parity). | Archival systems, large-scale storage where data integrity is paramount. |
| **RAID 10 (1+0)** | **Stripe of Mirrors** | Combines mirroring and striping. It creates two mirrored sets (RAID 1) and then stripes data across them (RAID 0). | 4 | Yes | **Excellent read/write.** Best of both worlds. | High-performance databases, enterprise applications needing both speed and redundancy. |

* **Common Pitfall:** RAID is **not a backup**. It protects against hardware failure, not against accidental deletion, file corruption, or malware. You still need a separate backup strategy.
* **Real-world Note:** RAID can be implemented in **hardware** (via a dedicated RAID controller card, which is faster and more reliable) or **software** (managed by the OS, which is cheaper but uses CPU cycles).


</details>

---

<details>
  <summary>07: Inter-Process Communication</summary>

### Section 7: Inter-Process Communication

**Inter-Process Communication (IPC)** is a set of mechanisms provided by the operating system that allow different processes to communicate with each other and synchronize their actions. This is essential for coordinating activities in a system with multiple concurrent processes.[^8_2]

### Inter-Process Communication Mechanisms (IMP)

There are two fundamental models for IPC.


| Feature | Shared Memory | Message Passing |
| :-- | :-- | :-- |
| **Concept** | Processes communicate via a region of memory shared between them [^8_5]. The OS establishes the shared region, but all further control is up to the processes. | Processes communicate by sending and receiving messages through the kernel. No shared address space is required [^8_1]. |
| **Speed** | **Fast**. Communication happens at memory speed, as the kernel is not involved in the data exchange itself [^8_2]. | **Slow**. Involves system calls for every send/receive operation, adding overhead from kernel intervention [^8_2]. |
| **Synchronization** | The processes themselves are responsible for ensuring synchronization (e.g., using semaphores) to prevent conflicts [^8_1]. | Easier to implement and manage. Synchronization is often handled by the `send()` and `receive()` primitives themselves [^8_1]. |
| **Security** | Prone to conflicts if not implemented carefully. One process can corrupt another's data. | Safer, as the kernel acts as an intermediary, preventing direct, uncontrolled access to another process's space [^8_1]. |
| **Analogy** | **A shared whiteboard.** Anyone in the room can read or write on it instantly. But they need to coordinate to avoid writing over each other's work. | **A postal service.** You write a letter and give it to the post office (kernel). The post office delivers it. The process is slower and more formal but ensures the message gets to the right person without interference. |

**Real-world Implementations:**

* **Shared Memory:** POSIX Shared Memory (`shm_open`), Windows memory-mapped files.
* **Message Passing:** Sockets, Pipes, Message Queues.[^8_2]


### Other IPC Mechanisms

* **Pipes:**
  * A simple, one-way (half-duplex) communication channel between two related processes (e.g., a parent and child).[^8_5]
  * **Analogy:** A simple water pipe. Water flows in one direction only.
  * **Real-world Example:** In a Unix shell, the command `ls -l | grep "Sept"` uses a pipe. The standard output of `ls -l` is "piped" to become the standard input of `grep`.
  * **Named Pipes (FIFO):** A variation that has a name in the file system and can be used by unrelated processes.[^8_5]
* **Sockets:**
  * An endpoint for communication, typically used for sending and receiving data between processes over a network. Sockets can also be used for communication on the same machine.[^8_2]
  * This is the fundamental mechanism behind all network communication (e.g., your web browser communicating with a web server).
* **Message Queues:**
  * A linked list of messages stored in the kernel. Processes can add and remove messages from the queue.[^8_2]
  * It allows for many-to-many communication and doesn't require the sender and receiver to be active at the same time.


### Signals and Signal Handling

A **signal** is a software interrupt delivered to a process to notify it of an event. It's a lightweight, asynchronous form of IPC.

* **Common Signals in Unix/Linux:**
  * `SIGINT`: Interrupt signal (e.g., sent when you press `Ctrl+C`).
  * `SIGKILL`: The "kill" signal, which terminates a process immediately and cannot be caught or ignored.
  * `SIGSEGV`: Segmentation fault, sent when a process makes an invalid memory access.
  * `SIGHUP`: Hangup signal, often used to tell a daemon to re-read its configuration files.
* **Signal Handling:** When a process receives a signal, it can:

1. **Perform the default action** (e.g., terminate for `SIGINT`).
2. **Ignore the signal.**
3. **Catch the signal** with a custom function called a **signal handler**. This allows the process to perform a specific action in response to the signal.


</details>

---

<details>
  <summary>08: System and Performance</summary>

### Section 8: System and Performance

This section covers the core interactions between user applications and the OS kernel, how the system starts, and how its performance is measured and optimized.

### System Calls and their Categories (IMP)

A **system call** is the programmatic way a user-level process requests a service from the kernel. It's the primary interface between an application and the operating system. When a system call is made, it causes a trap, switching the processor from user mode to kernel mode.

* **Analogy (Ordering at a Restaurant):** You (a user process) cannot go into the kitchen (kernel) yourself. You must ask the waiter (the system call interface) to get something for you. The waiter takes your request, goes to the kitchen, gets it done, and brings the result back to you.

**Common Categories of System Calls:**

* **Process Control:** `fork()` (create a new process), `exit()` (terminate), `wait()` (wait for a child to terminate).
* **File Management:** `open()`, `read()`, `write()`, `close()`.
* **Device Management:** `ioctl()` (to configure device parameters), `read()`, `write()`.
* **Information Maintenance:** `getpid()` (get process ID), `gettimeofday()` (get current time).
* **Communication:** `pipe()`, `socket()`, `shmget()` (for shared memory).


### System Boot Process (IMP)

The boot process is the sequence of operations the computer performs when it is first turned on, culminating in the loading of the operating system.

**Typical Boot Sequence for a PC:**

1. **BIOS/UEFI:** When the computer is powered on, the processor executes code stored in a firmware chip on the motherboard, either the Basic Input/Output System (BIOS) or the more modern Unified Extensible Firmware Interface (UEFI).
2. **POST (Power-On Self-Test):** The firmware runs a self-test to check that basic hardware components (like memory, keyboard) are functional.
3. **Bootloader Identification:** The firmware looks for a bootable device (like an HDD, SSD, or USB drive) in a pre-configured order. It finds the **bootloader** (e.g., GRUB in Linux, Windows Boot Manager) in the first sector of the disk (the Master Boot Record or MBR).
4. **Bootloader Execution:** The firmware loads the bootloader into memory and transfers control to it.
5. **Kernel Loading:** The bootloader's job is to load the OS **kernel** (e.g., `ntoskrnl.exe` in Windows, `vmlinuz` in Linux) and an initial RAM disk (`initrd`) into memory.
6. **Kernel Initialization:** The bootloader hands over control to the kernel. The kernel initializes itself, sets up device drivers, mounts the root file system, and starts the initial user-space process (e.g., `init` or `systemd` in Linux).
7. **User Space:** The initial process starts other system daemons and services, eventually leading to the login prompt or graphical user interface.

### Software and Hardware Interrupts

An **interrupt** is a signal that prompts the OS to stop its current work and handle a specific event.


| Type | Description | Trigger | Analogy |
| :-- | :-- | :-- | :-- |
| **Hardware Interrupt** | A signal generated by a hardware device. | An I/O device finishing an operation, a key press, a mouse click, a timer expiring. | The doorbell ringing. You must stop what you're doing to answer it. |
| **Software Interrupt (Trap)** | An interrupt generated by a software instruction. | A system call, an illegal memory access (segmentation fault), division by zero. | Intentionally pausing your work to make a phone call (system call). |

### Resource Management

The OS is responsible for managing all system resources (CPU, memory, I/O devices) and allocating them to various processes and users. Effective resource management aims to be:

* **Efficient:** Maximize resource utilization and system throughput.
* **Fair:** Ensure all processes get a fair share of resources.
* **Conflict-free:** Prevent processes from interfering with each other.


### Priority Inversion (IMP)

**Priority inversion** is a scheduling problem that occurs when a high-priority task is indirectly preempted by a lower-priority task, effectively "inverting" their relative priorities.

* **Classic Scenario:**

1. A **low-priority task (L)** acquires a resource (e.g., a mutex).
2. A **high-priority task (H)** preempts L and tries to acquire the same resource. H blocks, as L holds the resource.
3. A **medium-priority task (M)**, which does not need the resource, becomes runnable. Since M has higher priority than L, it preempts L.
  * **Result:** H is now waiting for L, but L is being prevented from running by M. The high-priority task is effectively blocked by a medium-priority task.
* **Solution (Priority Inheritance):** A common solution is **priority inheritance**, where the low-priority task (L) temporarily inherits the priority of the high-priority task (H) that is waiting for it. This allows L to run, finish its critical section, release the resource, and let H proceed.


### Load Balancing in Operating Systems

In a multiprocessor (multi-core) system, **load balancing** is the process of distributing the workload evenly across all available CPUs.

* **Push Migration:** A specific task periodically checks the load on each processor and, if it finds an imbalance, "pushes" tasks from an overloaded CPU to a less-busy one.
* **Pull Migration:** An idle processor "pulls" a waiting task from a busy processor's ready queue.
* **Best Practice:** Load balancing must be balanced with the cost of migrating processes, which can be high due to cache invalidation (processor affinity).


### Performance Measurement and Tuning

This involves monitoring system performance, identifying bottlenecks, and making adjustments.

**Key Performance Metrics (IMP):**

* **CPU Utilization:** The percentage of time the CPU is busy doing useful work.
* **Throughput:** The number of processes or transactions completed per unit of time.
* **Response Time:** The time from a request's submission until the first response is produced.
* **Memory Usage:** The amount of RAM being used, including page fault rates.
* **I/O Performance:** Data transfer rates and latency for disk and network operations.

**Common Monitoring Tools:**

* **Linux:** `top`, `htop` (for real-time process monitoring), `vmstat` (virtual memory statistics), `iostat` (I/O statistics), `sar` (system activity reporter).[^9_5]
* **Windows:** Task Manager, Resource Monitor, Performance Monitor.


</details>

---

<details>
  <summary>09: Advanced Topics</summary>

### Section 9: Advanced Topics

These topics represent sophisticated techniques and modern trends in OS design, focusing on performance, virtualization, security, and future architectures.

### Cache: Direct Mapping and Associative Mapping

Cache is a small, fast memory that sits between the CPU and main memory (RAM). It stores frequently accessed data to reduce the average time to access memory. **Cache mapping** defines how memory blocks are placed in the cache.

* **Direct Mapping:** Each block from main memory can only be placed in one specific line in the cache. The mapping is usually determined by `(Block address) MOD (Number of cache lines)`.
  * **Pro:** Simple and fast to implement.
  * **Con:** Can lead to **conflict misses**. If two frequently used memory blocks map to the same cache line, they will continuously evict each other, even if the rest of the cache is empty.
* **Associative Mapping (Fully Associative):** A block from main memory can be placed in any line of the cache. The CPU must search the entire cache in parallel to find the data.
  * **Pro:** Most flexible; avoids conflict misses.
  * **Con:** Very expensive to implement due to the hardware needed for parallel comparison.
* **Set-Associative Mapping (IMP):** A compromise between the two. The cache is divided into sets, and each memory block can be placed in any of the lines within a specific set. It is the most common approach used in modern CPUs.


### Virtual Machines and Hypervisors (IMP)

**Virtualization** allows a single physical machine to run multiple "guest" operating systems simultaneously.

* **Virtual Machine (VM):** A software-based emulation of a computer system. It provides the functionality of a physical computer, running its own OS and applications.
* **Hypervisor (or Virtual Machine Monitor, VMM):** The software layer that creates and runs virtual machines. It sits between the hardware and the guest OSs, managing the allocation of physical resources (CPU, memory, storage) to each VM.

| Type | Description | Analogy | Real-world Examples |
| :-- | :-- | :-- | :-- |
| **Type 1 (Bare-metal)** | The hypervisor runs directly on the host's hardware. | A landlord who owns a building and rents out individual, unfurnished apartments directly to tenants. | VMware ESXi, Microsoft Hyper-V, Xen. |
| **Type 2 (Hosted)** | The hypervisor runs as an application on top of a conventional host operating system. | A tenant who rents a large apartment and then sublets individual rooms to others. | VMware Workstation, Oracle VirtualBox, Parallels. |

### Spooling

**Spooling (Simultaneous Peripheral Operations On-Line)** is a technique where data for a slow I/O device (like a printer) is temporarily held in a buffer on a faster device (like a disk). The OS then copies the data from the disk buffer to the device at its own pace.

* **Benefit:** It allows the CPU to continue with other tasks without having to wait for the slow device to complete its operation, thus increasing system efficiency.
* **Real-world Example:** When you print multiple documents, they are added to a **print queue** (a spool), and the printer processes them one by one in the background.


### Network File Systems (NFS)

An **NFS** is a distributed file system protocol that allows a user on a client computer to access files over a computer network as if they were on their local storage. This enables centralized file storage and sharing among multiple machines.

### Thread Safety and Reentrancy (IMP)

These are important concepts in concurrent programming.

* **Thread Safety:** A piece of code is **thread-safe** if it functions correctly even when executed by multiple threads simultaneously. This usually means protecting shared data with synchronization mechanisms like mutexes.
* **Reentrancy:** A function is **reentrant** if it can be interrupted in the middle of its execution, then safely called again ("re-entered") before the first call completes, and both calls will still give the correct result. Reentrant functions cannot use static or global non-constant data.
  * **Key Difference:** A reentrant function is always thread-safe, but a thread-safe function is not necessarily reentrant. A thread-safe function might use a global lock, which would prevent it from being re-entrant.


### Operating System Security Mechanisms

These are features designed to protect the OS and user data from unauthorized access and malicious activity.

* **Authentication:** Verifying user identity (passwords, biometrics).
* **Access Control:** Limiting what authenticated users can do (permissions, ACLs).
* **Intrusion Detection:** Monitoring for and alerting on suspicious activity.
* **Sandboxing:** A security mechanism for separating running programs, usually to execute untrusted code in a highly restricted environment. Web browsers often run tabs in separate sandboxed processes.


### Future Trends in Operating Systems

* **Microkernels:** A design philosophy where the kernel is kept as small as possible, containing only the most fundamental functions like process scheduling, memory management, and IPC. Other services (like device drivers, file systems) run as user-space processes.
  * **Pro:** More secure and stable (a crash in a driver doesn't bring down the whole system).
  * **Con:** Can have higher overhead due to increased IPC between services.
* **Containers (e.g., Docker) (IMP):** A form of OS-level virtualization. Containers share the host system's kernel but have their own isolated user space, file system, and network stack.
  * **Containers vs. VMs:** Containers are much more lightweight and faster to start than VMs because they don't need to boot a full guest OS. They are ideal for packaging and deploying applications in a consistent environment.


</details>

---
