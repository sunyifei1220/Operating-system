# Operating System

## process

---

**Process** : Abstraction of a running program

**Context of a process**: 

* CPU: value of registers
  * PC (Program counter)
  	 SP (stack pointer),	FP (frame pointer),	GP (general)	
* Memory: pointers to memory areas
  * Code, static variables, heap, shared..
  * stack of activation records 
* Other (kernel-related state,..)

**Process Stack**

* Stack of activation records : one per pending procedure
* Activation record *stores*
  * return address
  * link to previous record 
  * local variables
  * other(e.g. register values)
* Stack pointer points to top (SP)

**(\*)Context Switching**

- Occurs when **process makes system call or interrupt occurs**

* Done  in software
  * Allocating CPU from one process to another
    * First save context of currently running process
    * Next restore context of next process
  * Loading the context
    * Load general registers, SP, etc.
    * Load PC (*must be last instruction*)
* Done in hardware
  * switch from user to kernel mode: amplify power

**Yield**

* yield(p)

  * Let process p run (voluntarily give up CPU to p)
  * context switch

* The magic of yield


  ```pseudocode
  magic = 0; // local variable 
  save A’s context: // current process 
  	asm save GP; // general purpose registers; 
  	asm save SP; // stack pointer 
  	asm save PC; // program counter, note value! 
  if (magic == 1) return; 
  else magic = 1; 
  restore B’s context: // process being yielded to 
  	asm restore GP; 
  	asm restore SP;   
  	asm restore PC; // must be last! 
  /* magic is allocated on stack, won't be changed when restoring*/
  ```

**Kernel**: 

* code that supports processes.
  * System calls: fork(), exit(), read(), etc.
  * Management: context switch, scheduling
*  Runs as an extension of current process
* Kernel runs when *system call* or *hardware interrupts* occurs.
* Kernel maintains list of process: unique ids, states and other info.
* Kernel can get control by:
  * Process give up control voluntarily
    * System call
  * Preemption: forcibly take away CPU
    * Interrupt generated when hardware timer expires. Rest timer while kernel running. 

**Process states**

* Running: actually making progress, using CPU
* Ready: able to make process, not using CPU
* Blocked: not able to make process, cannot use CPU

```sequence
Ready->Running:dispatch
Running->Ready:preempt
Blocked->Ready:wake up
Running->Blocked:sleep
```

| Physical\Logical  | Able to execute | Not Able to execute |
| ----------------- | --------------- | ------------------- |
| **Executing**     | Run             | X                   |
| **Not Executing** | Ready           | Blocked             |
