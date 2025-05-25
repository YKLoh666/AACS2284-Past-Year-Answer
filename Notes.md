# Table of Contents

- [System Software](#system-software)
- [Operating System (OS)](#operating-system-os)
  - [OS Managers/Subsystems](#os-managerssubsystems)
  - [Types of Operating Systems](#types-of-operating-systems)
  - [Bootstrap Program](#bootstrap-program)
  - [Services Provided by the OS](#services-provided-by-the-os)
  - [System Calls](#system-calls)
  - [Kernel and Interrupts](#kernel-and-interrupts)
  - [Utility Programs](#utility-programs)
- [Processor Manager](#processor-manager)
  - [Key Terms](#key-terms)
  - [Submanagers of the Processor Manager](#submanagers-of-the-processor-manager)
  - [Process States](#process-states)
  - [Middle-Level Scheduler](#middle-level-scheduler)
  - [Process Control Block (PCB)](#process-control-block-pcb)
  - [Context Switching](#context-switching)
  - [Good Scheduling Policies](#good-scheduling-policies)
- [Deadlock](#deadlock)
  - [Cases of Deadlock](#cases-of-deadlock)
  - [Deadlock Conditions](#deadlock-conditions)
  - [Deadlock Prevention](#deadlock-prevention)
  - [Deadlock Avoidance](#deadlock-avoidance)
  - [Deadlock Detection](#deadlock-detection)
  - [Deadlock Recovery](#deadlock-recovery)
  - [Starvation](#starvation)

## System Software

**System Software** is computer software that operates the **computer hardware** and provides a platform for running **application software**. It includes two main categories:

- **Operating Systems (OS)**: Manages **hardware resources** and controls the execution of **application software**.
- **Utility Programs**: Analyzes, configures, optimizes, and maintains the **computer system**.

---

## Operating System (OS)

The **Operating System (OS)** is the intermediary between **computer hardware** and **application software**. It manages **hardware components** such as **I/O devices**, **CPU**, **memory**, and **storage**, and controls all running **software**. The **OS** remains active as long as the computer is powered on.

- **Interaction Layers**:  
  User ↔ **Application Program** ↔ **OS** ↔ **Hardware**

- **OS Functions**:

  - Provides an **interface** to make the **computer system** user-friendly.
  - Allocates **resources** like **CPU time**, **memory**, and **I/O devices**.
  - Executes **application programs**.
  - Controls **I/O Devices**

- **OS Characteristics**:
  - **Concurrency**: Manages multiple **processes** simultaneously to support parallel activities.
  - **Sharing**: Enables **resources** and **information** to be shared across **processes** and **users**.
  - **Long-term Storage**: Maintains **data** for processing and future use.
  - **Non-determinacy**: Handles unpredictable events, such as **I/O interrupts**.

---

### OS Managers/Subsystems

The **OS** includes specialized subsystems, referred to as **managers**, to handle different **resources**. These are:

- **Processor Manager**:

  - Allocates and releases **CPU time**.
  - Provides **registers** for processing.
  - Tracks the status of each **process**.

- **Memory Manager**:

  - Allocates, deallocates, and reallocates **memory space** for **programs**.
  - Ensures **memory protection** and **sharing**.
  - Monitors **memory usage**.

- **Device Manager**:

  - Allocates and deallocates **devices**.
  - Oversees **devices**, **channels**, and **control units**.

- **File Manager**:

  - Allocates and deallocates **files**.
  - Tracks all **files** in the system.
  - Manages **security** through **access policies**.

- **Network Manager**:
  - Monitors **resource sharing** over **networks**.
  - Controls access to **network resources**.

---

### Types of Operating Systems

Different **Operating Systems** are designed for specific purposes. These types include:

- **Batch Systems**:

  - Execute a series of **jobs** in batches without **user interaction**.
  - Ideal for processing large volumes of **data**.

- **Time-Sharing Systems** (also called **Interactive Systems**):

  - Allow multiple **users** to interact with the system at the same time.
  - Provide immediate feedback and reduce **response time**.

- **Real-Time Systems**:

  - Respond to **input** instantly, often in time-sensitive environments.
  - Use **priority-based pre-emptive scheduling** for urgent **tasks**.

- **Hybrid Systems**:

  - Combine features of **batch systems** and **interactive systems**.
  - Support **user interaction** while running **batch programs** in the background.

- **Embedded Systems**:
  - Built for specific purposes within **devices** (e.g., smartphones, appliances).
  - Not designed for general use or interchangeable across **systems**.

---

### Bootstrap Program

The **Bootstrap Program** is the initial program that runs when the **system** starts. It initializes the **system**, loads the **OS kernel**, and starts **system daemons**. The **kernel** operates in an **interrupt-driven** mode, responding to **hardware interrupts** and **software interrupts**.

---

### Services Provided by the OS

The **OS** offers services divided into two categories:

- **Services Outside the Kernel**:

  - **Print services**.
  - **Graphical User Interface (GUI)**.
  - **Daemons** (background processes).
  - **Device drivers**.

- **Services Provided by the Kernel**:
  - **Resource management** via the **Processor Manager**, **Memory Manager**, **Device Manager**, **File Manager**, and **Network Manager**.
  - **System Calls**: Enable **user-space applications** to request services from the **OS** and interact with **hardware**.

---

### System Calls

**System Calls** are requests from **applications** to the **OS kernel** for low-level operations, such as accessing **hardware**. They ensure secure and controlled access to **system resources**. Categories include:

- **Process Control**: Manages **processes** (e.g., fork, exit, wait).
- **File Manipulation**: Handles **files** (e.g., open, read, write).
- **Device Manipulation**: Controls **devices** (e.g., read, write, ioctl).
- **Information Maintenance**: Retrieves **system information** (e.g., alarm, sleep, getpid).
- **Communication**: Supports **inter-process communication** (e.g., pipe, mmap, shmget).
- **Protection**: Manages **permissions** and **security** (e.g., chmod, chown, umask).

---

### Kernel and Interrupts

The **Kernel** is the core component of the **OS** that manages **system resources** and handles **interrupts**. It operates in an **interrupt-driven** manner, responding to:

- **Hardware Interrupts**: Triggered by **hardware devices** (e.g., keyboard input).
- **Software Interrupts**: Triggered by **software events** (e.g., division by zero, **system calls**).

- **Dual Mode Operation**:

  - **User Mode**: Restricted mode for **application execution**.
  - **Kernel Mode**: Privileged mode for **OS operations** with full **hardware** access.
  - Transitions occur when a **user application** requests a service, shifting from **User Mode** to **Kernel Mode**.
  - **Privileged instructions** are restricted in **User Mode** for security.

- **Interrupts**:
  - Enable the **CPU** to pause normal processing for urgent **tasks**.
  - Types of **Interrupts**:
    - **Program**: Errors like **division by zero**.
    - **Timer**: **System clock** events.
    - **I/O**: **Input/output** events (e.g., printer completion).
    - **Hardware Failure**: **Hardware** malfunctions.
  - **Trap**: A **software interrupt** from a **user program** to invoke **OS functions** (e.g., **system calls**).
  - **Hardware Interrupt**: Triggered by **hardware** to execute an **Interrupt Service Routine (ISR)**.
  - **Interrupt Service Routine (ISR)**: A routine handling specific **interrupt** types.

---

### Utility Programs

**Utility Programs** are a type of **system software** that assists in analyzing, configuring, optimizing, and maintaining the **computer**. They require technical expertise to use effectively.

---

## Processor Manager

The **Processor Manager** is a critical component of the **Operating System (OS)** responsible for managing **CPU time** and scheduling **jobs** and **processes**. It coordinates the execution of multiple tasks using **active multiprogramming** and **passive multiprogramming** techniques.

- **Active Multiprogramming**: Each program is given a **preset time slice** of CPU time. When the time slice expires, the job is interrupted, and another new job begins execution.
- **Passive Multiprogramming**: Each program is **serviced in turn**, one after another. An interrupt signal is generated when a program completes, allowing the next program to continue.

---

### Key Terms

- **Job**: A **program** submitted to the system for execution.
- **Process**: An active **job** that has been loaded into **RAM** and is either running or waiting to run.

---

### Submanagers of the Processor Manager

The Processor Manager includes two primary submanagers: the **Job Scheduler** and the **Process Scheduler**.

#### Job Scheduler (Long-Term Scheduler)

The **Job Scheduler**, also called the **Long-Term Scheduler**, selects **jobs** from incoming requests and prepares them for execution.

- **Responsibilities**:
  - Selects **jobs** from the incoming job request queue.
  - Arranges **jobs** to fully utilize system **resources**.
  - Balances **I/O-bound** and **CPU-bound processes** for optimal performance.
  - Places selected **jobs** into the **Ready Queue**, where they await the **Process Scheduler**.
- **I/O-bound Process**: A **job** with short **CPU cycles** and long **I/O cycles**, resulting in low **CPU usage** (e.g., frequent disk reads).
- **CPU-bound Process**: A **job** with high **CPU cycles** and short **I/O cycles**, resulting in high **CPU usage** (e.g., intensive computations).

#### Process Scheduler (Short-Term Scheduler)

The **Process Scheduler**, also known as the **Short-Term Scheduler**, assigns the **CPU** to execute **processes** from the **Ready Queue**.

- **Responsibilities**:
  - Assigns the **CPU** to execute **processes** from the **Ready Queue**.
  - Determines the **time slice** allocated to each **process**.
  - Decides when to **interrupt** a **process** (e.g., when its time slice expires).
  - Manages how **jobs** move during execution (e.g., from running to waiting).
  - Recognizes when a **job** has concluded and terminates it.

---

### Process States

A **process** transitions through several states during its lifecycle:

- **Hold**: The **job** has been accepted by the system but is not yet ready to run.
- **Ready**: The **process** is loaded into memory and ready to run on the **CPU**.
- **Waiting**: The **process** is paused, waiting for **I/O resources** or another event to complete.
- **Running**: The **process** is currently being executed by the **CPU**.
- **Finished**: The **process** has completed execution.

**Diagram**:

```

        +------+        Admitted       +---------+
        | Hold |---------------------->| Ready   |<-----------------+
        +------+                       +---------+                  |
                                          |  ^                      |
                       Scheduler dispatch |  | Interrupt            |
                                          v  |                      |
        +----------+        Exit       +---------+                  |
        | Finished |<------------------| Running |                  | I/O or event completion
        +----------+                   +---------+                  |
                                          |                         |
                                          | I/O or event wait       |
                                          v                         |
                                       +---------+                  |
                                       | Waiting |------------------+
                                       +---------+
```

---

### Middle-Level Scheduler

The **Middle-Level Scheduler** is employed in highly interactive environments to enhance **memory** management.

- **Function**: Temporarily swaps **active jobs** in and out of **memory** to allow other **jobs** to complete faster, often leveraging **virtual memory**.
- **Thrashing**: A situation where excessive swapping of pages in and out of memory causes performance degradation or system halting.

---

### Process Control Block (PCB)

The **Process Control Block (PCB)** is a data structure containing vital information about each **process**. It is created when a **job** enters the **Hold** state and updated as the **process** progresses.

- **Contents of PCB**:
  - **Process Identification**: A unique ID for the **process**.
  - **Process Status**: The current state of the **process** (e.g., Ready, Running).
  - **Process States**: Details about **register content**, **main memory**, and **resources** used.
  - **Accounting**: Tracks **CPU time**, **main storage occupancy**, and **system programs** utilized.
- **Queue**: A linked list of **PCBs** indicating the order in which **jobs** or **processes** are serviced (not the job itself).

---

### Context Switching

**Context Switching** occurs when the **CPU** switches execution from one **process** to another.

- **Process**:
  - The current **job** is halted, and its state is stored in its **PCB**.
  - The **PCB** of the preempting **job** is loaded into the **CPU registers**.
  - Once the preempting **job** completes or is interrupted, the previous **job** resumes by reloading its **PCB**.

---

### Good Scheduling Policies

Effective scheduling policies aim to optimize system performance with the following objectives:

- **Maximize Throughput**: Complete as many **jobs** as possible within a given time frame.
- **Minimize Response Time**: Reduce the delay between a user’s request and the system’s response.
- **Minimize Turnaround Time**: Shorten the duration from **job** submission to completion.
- **Minimize Waiting Time**: Decrease the time **processes** spend in queues.
- **Maximize Efficiency**: Optimize the use of the **CPU** and other **resources**.
- **Fairness**: Ensure all **jobs** receive equitable **CPU time** and resource access.

---

## Deadlock

- **Deadlock**: A situation where two or more processes are unable to proceed because each is waiting for the other to release resources. This can occur in systems with limited resources and can lead to system halting. Resolving deadlocks through external intervention.

---

### Cases of Deadlock

- File Request: Need 2 files, but one is held by another process.
- Database Locking: Need to access two tables, but one is locked by another process.
- Dedicated Devices: Need two tapes, but one is held by another process.
- Multiple Devices: Circular wait for multiple devices, where each process holds one device and waits for another.
- Spooling Deadlock
  - Deadlock in spooling occurs when the printing system faces a resource conflict. In this scenario:
  - The printer requires the complete output before printing can start.
  - However, the spooling system has enough space to hold only a part of the complete output.
  - As a result, neither the full document is available to initiate printing, nor can the spooling system clear space because it is blocked by the incomplete job.
  - This creates a deadlock where both the printer and the spooling system are waiting on each other, halting the process entirely.
- Disk Sharing
  - Conflicting I/O commands causing deadlock
- Network Deadlock
  - Nodes buffer are full and waiting for each other to release resources.

---

### Deadlock Conditions

- **Mutual Exclusion**: At least one resource must be held in a non-shareable mode.
- **Hold and Wait**: A process holding at least one resource is waiting to acquire additional resources.
- **No Preemption**: Resources cannot be forcibly taken from a process holding them.
- **Circular Wait**: A set of processes are waiting for each other in a circular chain.

---

### Deadlock Prevention

- Design the system to prevent one of the four conditions from occurring.
- **Mutual Exclusion**: Make resources shareable. (But this is not always feasible, e.g., printers).
- **Hold and Wait**: Process should not hold resources while waiting for others.
- **No Preemption**: Allow preemption of resources from waiting processes.
- **Circular Wait**: Impose a strict ordering on resource allocation to prevent circular wait conditions.

---

### Deadlock Avoidance

- Use algorithms to ensure that the system never enters a deadlock state.
- **Banker’s Algorithm**: A resource allocation and deadlock avoidance algorithm that tests for safe states before granting resource requests.
- **Safe State**: A state where the system can allocate resources to each process in some order and still avoid deadlock.
- **Problems**:
  - Jobs must state their maximum resource needs in advance.
  - Number of total resources must be constant.
  - Overhead of maintaining the resource allocation table.

---

### Deadlock Detection

- Reducing the Directed Resource Graph (DRG) to find cycles.

---

### Deadlock Recovery

- Terminate one or more processes to break the deadlock.
- Preempt resources from one or more processes to break the deadlock.
- Rollback processes to a safe state and restart them.

---

### Starvation

- **Starvation**: Result of conservative resource allocation policies, where a process is perpetually denied the resources it needs to proceed. This can occur in systems with high contention for limited resources, leading to some processes being indefinitely delayed while others are serviced.
- **Avoiding Starvation**: Aging techniques can be used to gradually increase the priority of waiting processes, ensuring that all processes eventually receive the resources they need.
- **Aging**: Gradually increasing the priority of waiting processes to ensure they eventually receive the resources they need.

---

## Memory Management

---

### Memory Partitioning

- **Fixed Partitioning**:
  - Fixed-size partitions are created in memory
  - Static allocation of memory
  - If too small, large processes may not fit
  - If too large, **internal fragmentation** occurs (wastage)
  - Same program stored contiguously
  - **Deallocation**: Set memory partition to free when process terminates.
- **Dynamic Partitioning**:
  - Jobs given exactly the amount of memory they need
  - Performance degrades over time due to **external fragmentation**
  - **Deallocation**
    - Maintain a free list of available memory blocks.
    - When a process terminates, merge adjacent free blocks to reduce fragmentation.
    - When merging more than 3 blocks, the list will have null entries.
    - Null entries are to be filled later with free blocks.
  - **Compaction/Defragmentation**:
    - Rearranging memory to eliminate fragmentation.
    - **Relocation**: Update currently used memory blocks to point to the new locations.
    - Has high overhead, only done when necessary.
      - Memory almost full (e.g., 75% used)
      - Programs waiting too long
      - Fixed time intervals (e.g., every 10 minutes)
- **First Fit** vs **Best Fit**

| First Fit                                                    | Best Fit                                                        |
| ------------------------------------------------------------ | --------------------------------------------------------------- |
| Allocates the first available partition that is large enough | Allocates the smallest available partition that is large enough |
| Faster allocation as it scans memory linearly                | Slower allocation as it searches for the best fit               |
| Algorithm less complex                                       | Algorithm more complex                                          |
| Memory list sorted by location                               | Memory list sorted by size                                      |

---

### New Memory Management Scheme

- The old scheme issues
  - Program needs to be loaded entirely into memory.
  - Fragmentation issues.
  - Overhead of compaction.
- **Paged Memory Allocation**
  - Divides memory into fixed-size pages.
  - Steps:
    1. Divide program into pages.
    2. Allocate enough empty frames in memory.
    3. Load pages into frames all at once.
  - Tables
    - **Job Table (JT)**: Size of the job and memory location of Page Map Table (PMT).
    - **Page Map Table (PMT)**: Maps pages to frames.
    - **Memory Map Table (MMT)**: Location and free/busy status.
  - Pros
    - Non-contiguous allocation.
  - Cons
    - Determine size of pages.
    - Increased overhead
    - Internal fragmentation still exists, but reduced.
  - TL;DR
    - Still fitting whole program into memory, just not in one contiguous block.
- **Demand Paging**
  - Only loads pages into memory when they are needed.
  - Thrashing: Excessive paging leading to performance degradation.
    - Caused when a page is removed from memory and then immediately needed again.
    - Can occur across jobs, large number of jobs vying limited memory.
    - Can occur within a job, such as cross page loops.
  - Page Fault: Occurs when a page is not in memory and needs to be loaded.
  - Tables
    - **Job Table (JT)**
    - **Page Map Table (PMT)** - extra fields:
      - Determines if page is in memory.
      - Determines if page is dirty (modified).
      - Determines if page is recently used (for replacement algorithms).
    - **Memory Map Table (MMT)**
  - Page Replacement Algorithms
    - **Least Recently Used (LRU)**: Replaces the page that has not been used for the longest time.
    - **First In First Out (FIFO)**: Replaces the oldest page in memory.
    - **Optimal Page Replacement**: Replaces the page that will not be used for the longest time in the future.
  - Pros
    - Not constrained by memory size.
    - More efficient, as only needed pages are loaded.
  - Cons
    - More overhead, table and page interrupt.
  - TL;DR
    - Program is divided into pages, and only the needed pages are loaded into memory.
- **Segmented Memory Allocation**
  - **Segments**: Logical divisions of a program (e.g., functions, data structures).
  - Segments can vary in size, allowing for more flexible memory allocation.
  - Tables
    - **Job Table (JT)**: Job and memory location of Segment Map Table (SMT).
    - **Segment Map Table (SMT)**
      - Segment number.
      - Size
      - Status (Inside memory or not)
      - Access rights (read, write, execute).
      - Memory location of the segment.
    - **Memory Map Table (MMT)**: Location and free/busy status.
  - Pros
    - Non-contiguous allocation.
    - More efficient memory usage, as segments can vary in size.
  - Cons
    - Compaction due to external fragmentation.
  - TL;DR
    - Demand paging but dynamically sized pages.
- **Segmented/Demand Paged Memory Allocation**
  - Pages segments into fixed-size pages.
  - Combines the benefits of both segmented and paged memory allocation.
  - Tables
    - **Job Table (JT)**: Job and memory location of Segment Map Table (SMT).
    - **Segment Map Table (SMT)**: Maps segments to pages.
    - **Page Map Table (PMT)**: Maps pages to frames.
    - **Memory Map Table (MMT)**: Location and free/busy status.
  - Pros
    - Non-contiguous allocation.
    - More efficient memory usage, as segments can vary in size and pages are fixed-size.
  - Cons
    - More overhead, as multiple tables are used.

---

### Virtual Memory

- Implemented using **demand paging** and **segmentation schemes**.

| Demand Paging                                  | Segmentation                                      |
| ---------------------------------------------- | ------------------------------------------------- |
| Internal fragmentation allowed                 | External fragmentation allowed                    |
| Pages are equal size                           | Segments are variable size                        |
| Address calculated from page number and offset | Address calculated from segment number and offset |
| Use Page Map Table (PMT)                       | Use Segment Map Table (SMT)                       |

- Advantages
  - Multiprogramming
  - Not restricted by physical main memory size.
  - Efficient memory usage, as only needed pages are loaded.
  - Eliminates either fragmentation or reduces it significantly.
- Disadvantages
  - Increased processor hardware costs.
  - Overhead of handling paging interrupts.
  - Software complexity to prevent thrashing.

---

## Concurrent Processes

- **Parallel processing**: Multiprocessing with multiple CPUs.
- **Process Synchronization**:
  - Resolve conflicts between processors in multiprocessing environments.
  - Ensure events occur in the correct order.
- Why Multiprocessing?
  - Increased throughput and computing power.
  - Reliability through redundancy.
  - Faster response time.
- Challenges
  - Orchestrating multiple processes.

---

### Process Synchronization

- **Critical Region**: A part of program that must complete execution without interruption towards a shared resource.
- **Lock-and-Key**: A mechanism to ensure that only process with the key can access the critical region.
- **Semaphore**: A variable used to control access to a common resource by multiple processes.
  - **Binary Semaphore**: Can be either 0 or 1, used for mutual exclusion.
  - **Counting Semaphore**: Can take any non-negative integer value, used for resource counting.
- **Operations on Semaphores**:
  - **Wait (P)**: Decrement the semaphore value. If the value is negative, block the process.
  - **Signal (V)**: Increment the semaphore value. If the value is non-negative, unblock a waiting process.
- **Mutex**: A mutual exclusion object that allows only one thread to access a resource at a time.
  - Implemented using binary semaphores.

> How it works:
>
> 1. A process requests access to a critical region by calling the **Wait (P)** operation on a semaphore. The semaphore can be think as the number of key available to use the critical region.
> 2. If the semaphore value is greater than 0, then **Wait (P)** will take the key, semaphore value will -1, and the process can enter the critical region.
> 3. If the semaphore value is 0, means no key is available, the **Wait (P)** operation will pause (blocked) until a key is available.
> 4. When the process inside the critical region completes its task, it calls the **Signal (V)** operation on the semaphore, which can be thought as returning the key.
> 5. The **Signal (V)** operation increments the semaphore value, and if there are any processes waiting for the key, one of them will be unblocked and allowed to enter the critical region.
>
> TL;DR
>
> - Wait(P) wait for a key, if key available, take it and enter critical region. If not, wait until key is available.
> - Signal(V) return the key, increment the semaphore value, and let waiting processes know that a key is available.

---

### Process Cooperation

---

#### Producer-Consumer Problem

- In simple,
  - The producer creates data and the consumer consumes it.
  - The producer produces data and places it in a buffer.
  - The consumer takes data from the buffer and processes it.
  - The buffer has a limited size, and the producer must wait if the buffer is full.
  - The consumer must wait if the buffer is empty.
- **Solution**: Use semaphores to synchronize access to the buffer.
  - Producer Semaphore: Indicates the total empty slots in the buffer.
  - Consumer Semaphore: Indicates the total filled slots in the buffer.
  - Mutex Semaphore: Ensures mutual exclusion when accessing the buffer.
- Producer Workflow:
  1. Wait on the Producer Semaphore (P) until it can produce data.
  2. Wait on the Mutex Semaphore (P).
  3. Add data to the buffer.
  4. Signal the Mutex Semaphore (V) to release the buffer.
  5. Signal the Consumer Semaphore (V) to indicate that data is available.
- Consumer Workflow:
  1. Wait on the Consumer Semaphore (P) until data is available.
  2. Wait on the Mutex Semaphore (P).
  3. Remove data from the buffer.
  4. Signal the Mutex Semaphore (V) to release the buffer.
  5. Signal the Producer Semaphore (V) to indicate that space is available in the buffer.

---

#### Reader-Writer Problem

- In simple,
  - Multiple readers can read data simultaneously.
  - Only one writer can write data at a time.
  - If a writer is writing, no readers can read.
- **Solution**: Use semaphores to synchronize access to the shared data.
  - Reader Semaphore: Indicates the number of readers currently reading.
  - Writer Semaphore: Indicates that a writer is writing.
- Reader Workflow:
  1. Verify if no writer is writing (Writer Semaphore is not 0), otherwise wait.
  2. Wait on the Reader Semaphore (P). (This increments the count of readers).
  3. Read data.
  4. Signal the Reader Semaphore (V) to indicate that reading is complete. (This decrements the count of readers).
- Writer Workflow:
  1. Verify if no readers are reading (Reader Semaphore is 0), otherwise wait.
  2. Wait on the Writer Semaphore (P).
  3. Write data.
  4. Signal the Writer Semaphore (V) to indicate that writing is complete.
- Issues:
  - Reader or Writer Starvation depending who is prioritized.

---

### Application of Concurrent Programming

- Arithmetic operations
- **Explicit Parallelism**: Concurrent programming where the programmer explicitly defines the parallel tasks.
- **Implicit Parallelism**: Concurrent programming where the compiler or runtime system automatically identifies parallel tasks.

---

## I/O Devices Management

- Functions:
  - Track status of each device.
  - Preseet policies to determine which process gets access to a device for how long.
  - Allocate devices
  - Deallocate devices
    - **Process Level**: I/O commands executed and device temporarily released.
    - **Job Level**: Device permanently released when job terminates.

| Aspect             | Variation                                |
| ------------------ | ---------------------------------------- |
| Data Transfer Mode | Character Mode, Block Mode               |
| Access Method      | Sequential Access, Random Access         |
| Transfer Schedule  | Synchronous, Asynchronous                |
| Sharing            | Dedicated, Shared                        |
| Device Speed       | Latency, Seek Time, Transfer Rate, Delay |
| I/O direction      | Read, Write, Read-Write                  |

---

### Access Time

- Seek Time: Time taken to move the read/write head to the correct track. (Arm Movement)
- Search Time: Time taken to find the correct sector on the track. (Rotational Latency)
- Transfer Time: Time taken to transfer data from the disk to memory.
- Total Access Time: Seek Time + Search Time + Transfer Time.

---

### I/O Modules

- Manage communication between CPU and I/O devices.
- Accept I/O requests from the CPU.
- Transfer data between the CPU and I/O devices.
- Send interrupts to the CPU when I/O operations are complete.

---

### I/O Techniques

- Test flag in Channel Status Word (CSW)
- **Programmed I/O**:
  - **Polling**: CPU continuously checks the status of the I/O device.
  - If too frequent, CPU time is wasted in checking the status.
  - If too seldom, I/O operations may take longer to complete.
- **Interrupt**:
  - I/O device sends an interrupt signal to the CPU when it is ready for data transfer.
  - Control transferred to **interrupt handler**.
  - Interrupt handler processes the I/O request and returns control to the CPU.
- **Direct Memory Access (DMA)**:
  - Allows I/O devices to transfer data directly to/from memory without CPU intervention.
  - CPU send information to DMA controller about accessing memory.

---

### Buffering

- Temporary storage area for data being transferred between the CPU and I/O devices.
- Synchronizes data transfer between devices with different speeds.
- Double buffering: Two buffers used to allow one buffer to be filled while the other is being emptied. (Solve mutual exclusion problem)

---

### Submanagers of Device Manager

- **I/O Traffic Controller**: Watch status of all devices and channels
- **I/O Scheduler**: Determines which process gets access to which device and for how long.
- **I/O Device Handler**: Handles data transfer and interrupts for each device.

---

### Seek Time Algorithms

| Algorithm                       | Advantages          | Disadvantages                      |
| ------------------------------- | ------------------- | ---------------------------------- |
| First Come First Serve (FCFS)   | Simple, fair        | Low throughput, high seek time     |
| Shortest Seek Time First (SSTF) | Reduces seek time   | Starvation for distant requests    |
| SCAN, LOOK                      | No starvation, fair | More complex, need directional bit |

---

## File Management

- Efficiency depends on
  - How files organised (e.g., sequential, direct, indexed sequential)
  - How files stored (e.g., contiguous, linked, indexed)
  - How records structured (e.g., fixed-length, variable-length)
  - Access control (e.g., read, write, execute permissions)
- Responsibilities
  - Allocate and deallocate files.
  - Track where each file stored
  - Determine how files will be stored

---

### File Organization

- Depends on
  - Volatility of data (addition, deletion, modification)
  - Activity of file (number of records processed in a given time)
  - Size of file (number of records)
  - Response time (time taken to access a record)
- **Sequential Record Organization**:
  - Records stored in a sequential order.
  - Accessed sequentially, one after another.
  - Can be optimized by sorting with key fields.
  - Batch applications.
- **Direct Record Organization**
  - Use direct access files instead of sequential files.
  - Flexibility to access records in any order. (Not from start to end)
  - Identified by relative address, which is the hash of the key field.
  - Logical address translated to physical address
  - Fast access to records.
  - But collisions can occur, where two records hash to the same address, leading to the need for collision resolution techniques.
- **Indexed Sequential Record Organization**
  - Combines sequential and direct access.
  - Index file contains key fields and their corresponding addresses.
  - Only the index file is stored in memory.
  - Sequential access to the index file, and direct access to the data file.

---

### Physical Storage Allocation

- Different from file organization.
  - File organization is about how files are structured and accessed.
  - Physical storage allocation is about how files are stored on disk.
- **Contiguous Allocation**:
  - Files stored in contiguous blocks on disk.
  - Fast access to specific records, given the starting address and size of the record.
  - Easily direct accessed.
  - Hard to expand unless there is enough space available.
  - Fragmentation can occur, leading to wasted space.
- **Linked Allocation**:
  - Files stored in non-contiguous blocks, linked together using pointers.
  - Each block contains a pointer to the next block.
  - Flexible, as files can grow dynamically.
  - Slower access, as each block must be traversed to access a specific record.
- **Indexed Allocation**:
  - Index blocks store pointers to data blocks.
  - Each file has its own index block.
  - Supports direct access to records.
  - Slower than contiguous allocation due to index lookup.
  - Flexible, as files can grow dynamically.

### Free Space Management

- **Bit Vector**: A bitmap where each bit represents a block of memory. A bit is set to 1 if the block is free, and 0 if it is allocated.
  - Easy to retrieve contiguous free blocks.
  - Requires significant memory overhead for large files.
- **Linked List**: A linked list of free blocks, where each block contains a pointer to the next free block.
  - More efficient in terms of memory usage.
  - Slower to retrieve contiguous free blocks, as the list must be traversed.
- **Grouping**: Store addresses of neighboring free blocks in a single block.
  - Reduces the overhead of maintaining a linked list.
  - Faster retrieval of contiguous free blocks.
- **Counting**: Store the length of a contiguous free block instead of individual addresses.
  - Reduces overhead further.
  - Faster retrieval of contiguous free blocks, as the length is known.

---

## System Management

- Balances strength and weaknesses of various components.

---

### Roles

- Memory Management
  - Tradeoff between memory use and CPU overhead.
- Processor Management
  - Tradeoff between CPU utilization and response time, overhead, and throughput.
- Device Management
  - Tradeoff between device utilization and response time, overhead, and throughput.
  - CPU manage blocking, buffering, and rescheduling of I/O operations.
- File Management
  - Tradeoff between file flexibility and CPU overhead.

---

### Measurement

- **Throughput** - Number of jobs completed in a given time.
- **Capacity** - Maximum number of jobs that can be processed in a given time.
- **Response Time** - Time taken to respond to a request.
- **Turnaround Time** - Time taken to complete a job from submission to completion.
- **Resource Utilization** - Percentage of time a resource is busy.
- **Availability** - Percentage of time a resource is available for use.
- **Reliability** - Probability that a resource will perform its intended function without failure.
  - Mean Time Between Failures (MTBF) - Average time between failures of a resource.
  - Mean Time To Repair (MTTR) - Average time taken to repair a resource after a failure.
  - Uptime = MTBF / (MTBF + MTTR) - Percentage of time a resource is operational.

---

### Feedback Loop

- Used in paged virtual memory systems to manage the arrival rate of processes based on system load.
- **Negative Feedback Loop**

  - Slow down arrival rate of processes when system is overloaded.

  ```
  +---------------------+
  | Monitor System Load |<--------------+
  +---------------------+               |
            |                           |
            v                           |
  +-----------------------+     No      |
  | Is System Overloaded? |-------------|
  +-----------------------+             |
            | Yes                       |
            v                           |
  +-----------------------------+       |
  | Slow Down Arrival Rate of   |-------+
  | Processes                   |
  +-----------------------------+

  ```

- **Positive Feedback Loop**

  - Speed up arrival rate of processes when system is underloaded.

  ```
  +---------------------+
  | Monitor System Load |<--------------+
  +---------------------+               |
            |                           |
            v                           |
  +------------------------+     No     |
  | Is System Underloaded? |------------|
  +------------------------+            |
            | Yes                       |
            v                           |
  +-----------------------------+       |
  | Speed Up Arrival Rate of    |-------+
  | Processes                   |
  +-----------------------------+

  ```

- Negative feedback loop is more common, as underutilization is less of a concern than overloading the system.

---

### Technique to Protect Hardware and Software

- User Authentication and Authorization
- Firewalls
- Antivirus Software
- File Permissions
- Data Encryption
- Backup and Recovery
- Regular Software Updates
