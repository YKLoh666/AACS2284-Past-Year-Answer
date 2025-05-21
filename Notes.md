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
- [Memorization Tips](#memorization-tips)
  - [Components of System Software](#components-of-system-software)
  - [Functions of the Operating System](#functions-of-the-operating-system)
  - [Characteristics of the Operating System](#characteristics-of-the-operating-system)
  - [OS Managers/Subsystems](#os-managerssubsystems-1)
  - [Types of Operating Systems](#types-of-operating-systems-1)
  - [Categories of System Calls](#categories-of-system-calls)
  - [Classes of Interrupts](#classes-of-interrupts)
- [Processor Manager](#processor-manager)
  - [Key Terms](#key-terms)
  - [Submanagers of the Processor Manager](#submanagers-of-the-processor-manager)
  - [Process States](#process-states)
  - [Middle-Level Scheduler](#middle-level-scheduler)
  - [Process Control Block (PCB)](#process-control-block-pcb)
  - [Context Switching](#context-switching)
  - [Good Scheduling Policies](#good-scheduling-policies)

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

## Memorization Tips

### Components of System Software

**Concepts**:

- **Operating Systems (OS)**: Manages hardware and runs applications.
- **Utility Programs**: Maintains and optimizes the system.

**Memorization Tip**:  
Picture an **orchestra**. The **Operating System** is the _conductor_, directing all the instruments (hardware) to play together smoothly (run applications). The **Utility Programs** are the _maintenance crew_, tuning the instruments and keeping the stage ready.

---

### Functions of the Operating System

**Concepts**:

- Provides a user-friendly **interface**.
- Allocates **resources** (CPU, memory, I/O devices).
- Executes **application programs**.
- Controls **input/output** operations.

**Memorization Tip**:  
Imagine a **restaurant manager**:

- Offers a _menu_ (interface) for customers (users).
- Assigns _tables, staff, and kitchen resources_ (resource allocation).
- Ensures _chefs_ cook the meals (executes programs).
- Oversees _food delivery_ to tables (controls I/O).

---

### Characteristics of the Operating System

**Concepts**:

- **Concurrency**: Handles multiple tasks at once.
- **Sharing**: Allows resource and info sharing across processes/users.
- **Long-term Storage**: Stores data for later use.
- **Non-determinacy**: Manages unexpected events.

**Memorization Tip**:  
Visualize a **busy restaurant kitchen**:

- **Concurrency**: Picture multiple chefs in the kitchen, each cooking a different dish at the same time. One chef might be grilling steaks while another prepares desserts. This mirrors how the OS runs multiple processes simultaneously, keeping everything moving smoothly.

- **Sharing**: The chefs share resources like ovens, stovetops, and ingredients. For example, they might take turns using the oven or pass a bag of flour between them. Similarly, the OS ensures processes share resources like memory or CPU time efficiently and without clashes.

- **Long-term Storage**: The kitchen has a pantry or refrigerator where ingredients are kept for future use. Just as the pantry stores flour for tomorrow’s bread, the OS manages a file system to keep data accessible long after a task ends.

- **Non-determinacy**: Imagine a sudden rush of orders or a chef spilling a pot of soup. The kitchen staff adapts quickly to these surprises, just as the OS responds to unexpected events like a printer jamming or a user clicking a button.

---

### OS Managers/Subsystems

**Concepts**:

- **Processor Manager**: Assigns CPU time and tracks processes.
- **Memory Manager**: Manages memory allocation and protection.
- **Device Manager**: Controls devices and their operations.
- **File Manager**: Organizes and secures files.
- **Network Manager**: Oversees network resources.

**Memorization Tip**:  
Think of a **large corporation**:

- **Processor Manager**: _HR department_ assigning tasks to employees (processes).
- **Memory Manager**: _Facilities department_ managing office space (memory).
- **Device Manager**: _IT department_ handling computers (devices).
- **File Manager**: _Records department_ organizing documents (files).
- **Network Manager**: _Communications department_ managing connections.

---

### Types of Operating Systems

**Concepts**:

- **Batch Systems**: Process jobs in batches without interaction.
- **Time-Sharing Systems**: Allow multiple users to interact simultaneously.
- **Real-Time Systems**: Respond instantly to inputs.
- **Hybrid Systems**: Combine batch and interactive features.
- **Embedded Systems**: Built for specific devices.

**Memorization Tip**:  
Associate each with a **vehicle**:

- **Batch Systems**: _Cargo train_ hauling large loads in batches.
- **Time-Sharing Systems**: _Bus_ carrying multiple passengers (users).
- **Real-Time Systems**: _Ambulance_ racing to emergencies.
- **Hybrid Systems**: _Hybrid car_ blending power sources.
- **Embedded Systems**: _Car’s onboard computer_ for specific tasks.

---

### Categories of System Calls

**Concepts**:

- **Process Control**: Manages processes (e.g., start, end).
- **File Manipulation**: Handles files (e.g., open, read).
- **Device Manipulation**: Controls devices (e.g., printer access).
- **Information Maintenance**: Retrieves system info (e.g., time).
- **Communication**: Enables process interaction (e.g., messaging).
- **Protection**: Manages permissions (e.g., access control).

**Memorization Tip**:  
Picture a **library**:

- **Process Control**: Checking out/returning books (starting/ending processes).
- **File Manipulation**: Reading/writing in books (files).
- **Device Manipulation**: Using library computers (devices).
- **Information Maintenance**: Checking library hours (system info).
- **Communication**: Messaging between branches (process communication).
- **Protection**: Managing library card access (permissions).

---

### Classes of Interrupts

**Concepts**:

- **Program**: Errors like division by zero.
- **Timer**: Clock-based events.
- **I/O**: Input/output triggers (e.g., printer done).
- **Hardware Failure**: Device malfunctions.

**Memorization Tip**:  
Imagine a **classroom**:

- **Program**: A student asking a question (program interrupt).
- **Timer**: The bell ringing (timer interrupt).
- **I/O**: A student leaving for the restroom (I/O interrupt).
- **Hardware Failure**: The projector failing (hardware interrupt).

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

- File Request
- Database Locking
- Dedicated Devices
- Multiple Devices
- Spooling Deadlock
  - Deadlock in spooling occurs when the printing system faces a resource conflict. In this scenario:
  - The printer requires the complete output before printing can start.
  - However, the spooling system has enough space to hold only a part of the complete output.
  - As a result, neither the full document is available to initiate printing, nor can the spooling system clear space because it is blocked by the incomplete job.
  - This creates a deadlock where both the printer and the spooling system are waiting on each other, halting the process entirely.
- Disk Sharing
  - Conflicting commands causing deadlock
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
- **Mutual Exclusion**: Make resources shareable.
- **Hold and Wait**: Process should not hold resources while waiting for others.
- **No Preemption**: Allow preemption of resources from processes.
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
