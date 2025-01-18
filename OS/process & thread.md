
## Process

**A process is a computer program under execution**
**Linux processes are isolated and do not interrupt each other’s execution**
**With a PID, we can identify any process in Linux**
The process of switching between two executing processes on the CPU is called process context switching. **Process context switching is expensive because the kernel has to save old registers and load current registers, memory maps, and other resources**.

## Thread
**A thread is a lightweight process**
- PID: Unique process identifier
- LWP: Unique thread identifier inside a process
- NLWP: Number of threads for a given process
Similar to process context switch, there is a concept of a thread context switch. A thread context switch is faster as the thread records only its stack values before the switch happens.
Since the threads share the same memory, they can become slow if the process does many concurrent tasks.