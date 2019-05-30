# Operating System

## Timesharing/Threads

---

**Timesharing**: multiplexing use of CPU over time.

**Thread**: single sequential path of execution

* Independent of memory
  * Contrast to process: path of execution + memory
* A part of process
  * live in memory of process
  * Allow multiple threads in a process
* Kernel-level threads
  * Thread calls are system calls
  * Thread management functions are in kernel
    * Thread context switch/scheduling
  * Each thread requires user and kernel stacks
  * Kernel can schedule threads on separate CPUs
  *  Pros
    * True parallelism
  * Cons
    * Overhead: thread switch requires kernel call
* User-level threads
  * Can support threads at user level
  * included via thread library
  * Threads calls are at user level
  * Thread management at user level
  * Supports threads regardless of kernel support
    * Pros
      * works on any kernel
      * Thread-switching occurs in user space (efficient)
      * User can decide on scheduling policy
    * Cons
      * No true parallelism

Which of the following will benefit the **least** from **multiple** CPUs: 

(a) a single process with multiple user-level threads; 

(b) a single process with multiple kernel-level threads; 

(c) multiple processes, each with a single user-level thread; 

(d) multiple processes, each with a single kernel-level thread.

 

(a) If the kernel does not support threads (and so threads are implemented at user level), since the kernel is “unaware” of them, it cannot assign them to different CPUs.

