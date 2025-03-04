# Operating System Questions and Answers

## Chapter 1: Introduction

### 1.1 What are the three main purposes of an operating system?
1. **Resource Management**: Efficiently manages hardware and software resources (CPU, memory, I/O devices).
2. **Process Management**: Schedules and executes processes smoothly.
3. **User Interface**: Provides an interface for users to interact with the computer.

### 1.2 When is it appropriate for an OS to "waste" resources?
- To improve user experience, multitasking, and responsiveness.
- Example: GUI-based systems use more memory but enhance usability and productivity.

### 1.3 Main challenge in real-time OS
- Ensuring tasks meet strict timing constraints.
- Delays can cause failures in critical applications like medical devices and automotive control.

### 1.4 Should an OS include applications like browsers and mail programs?
- **Yes**: Simplifies user experience, ensures compatibility.
- **No**: Makes the OS bulky, increases security risks, limits user choice.

### 1.5 Kernel mode vs User mode (Security)
- **Kernel Mode**: Has full access to system resources.
- **User Mode**: Restricts direct access to critical system components for security.

### 1.6 Privileged Instructions
✅ Privileged:
- Set timer
- Clear memory
- Turn off interrupts
- Modify device-status table
- Switch to kernel mode

❌ Non-Privileged:
- Read clock
- Issue a trap instruction
- Access I/O device

### 1.7 Difficulties in protecting OS with memory partitioning
1. OS updates and bug fixes become impossible.
2. If an error occurs, the OS cannot modify itself to recover.

### 1.8 Uses of multiple modes in CPUs
1. **Virtualization**: Different access levels for virtual machines.
2. **Security**: Different privilege levels for system components.

### 1.9 How to use timers for computing the current time
- Timers count clock ticks.
- OS reads timer values and calculates time based on clock frequency.

### 1.10 Cache benefits, issues, and limitations
#### Benefits:
1. **Speed**: Reduces access time for frequently used data.
2. **Efficiency**: Lowers the load on main memory.

#### Issues:
- Can cause inconsistency.
- Complex management is needed.

#### Why not make caches as large as the device?
- Expensive and hardware-inefficient.

### 1.11 Client-Server vs Peer-to-Peer Models
- **Client-Server**: Central server provides services to multiple clients.
- **Peer-to-Peer**: Each node acts as both client and server, distributing workloads.

---


**Contributors:** [Khoirul Yardan Mauluddin Zhorif 3124521022]
