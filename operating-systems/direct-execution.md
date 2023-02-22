# Mechanism: Limited Direct Execution

## CPU virtualization

- We have one physical CPU and many jobs to run at the "same time".
- The solution is to run a little bit of a proccess, than switching
to another and go on until the processes are done. Time sharing the CPU.
- Really important to achieve such virtualization maintaining Performance
and Control, the OS needs to run multiple processes and switch between them 
but not overload the system and have total control of what is happening.

## Basic Technique: Limited Direct Execution

- Literally just running a program as fast as it is expected directly on CPU.

Create entry for process list
Allocate memory for program
Load program into memory
Set up stack with argc/argv
Clear registers
Execute call main()
Run main()
Execute return from main
Free memory of process
Remove from process list

- If the program is just executed like that, how the OS will have the control
of what is going on? How the above statement of switch process will work?

### Problem #1: Restricted Operations

- Direction Execution is fast, but provides zero control to the OS.
- In that case what do we do if the process needs access to I/O actions
or need access for more memory? We cant just give to the process full system
control.
- We have a processor mode called "user mode", code that runs on this mode
is restricted in what it can do. Like I/O requests results in OS exceptions.
- There's also "kernel mode" that is the mode that the OS runs in. Code that
runs in that mode has the privileges to do whatever is needed, I/O requests, etc.
- What should we do if our "user mode" process needs to read from disk or any other
privileged operation? Virtually modern hardware provides to user programs performs
system calls. System Calls allows the kernel to expose some essential functionality
to "user mode" programs allocate memory, read from disk, create processes, etc.
- To execute a system call the program execute a type of "trap" instruction. Thins
instruction goes to the kernel raises the privilege to "kernel mode", does what is needed
than when is finished the OS calls an "return-from-trap" instruction that downgrande the
privilege to "user mode" again.
- But how the trap instruction knows which code to run inside the OS?

"The kernel does so by setting up a trap table at boot time. When the
machine boots up, it does so in privileged (kernel) mode, and thus is free
to configure machine hardware as need be. One of the first things the OS
thus does is to tell the hardware what code to run when certain excep-
tional events occur. For example, what code should run when a hard-
disk interrupt takes place, when a keyboard interrupt occurs, or when
a program makes a system call? The OS informs the hardware of the"

### Problem #2: Switching Between Processes

- If a process is running on the CPU, that means that the OS is not
running on the CPU. If the OS is not running how can we switch process?

## A cooperative Approach: Wait For System Calls

- A process run on the CPU and if is running for too long, give up
the CPU so the OS can decide what to do.
- The process is always transfering control to the OS using system calls,
so basically there is like a "command" on systems like that to just pass
the control to the OS.
- When the application do something illegal like accessing memory that shouldn't
be accessed the control is passed to the OS by a trap call.

But what if the process get stuck on a infinite loop and not make a system call?
Well my friend, the machine will have to reboot :P.

## A Non-Cooperative Approach: The OS Takes Control

How can we regain control over the system if the process running on
the CPU does not help?

- The response is using a Timer Interrupt device!
- A timer device can be used to raise an interrupt action at certain times that calls
the active running process to stop and so the OS can regain the control over the CPU.
- The OS has to inform the hardware of which code to run when the interrupt is called.
This is done at boot time, like with the system calls.

"Note that the hardware has some responsibility when an interrupt oc-
curs, in particular to save enough of the state of the program that was
running when the interrupt occurred such that a subsequent return-from-
trap instruction will be able to resume the running program correctly.
This set of actions is quite similar to the behavior of the hardware during
an explicit system-call trap into the kernel, with various registers thus
getting saved (e.g., onto a kernel stack) and thus easily restored by the
return-from-trap instruction."


### Saving and Restoring Context

Now the OS has to made a decision, continue running the
currently process or switch to another?

- The scheduler is in charge of doing that kind of decision.
- If the decission is to switch, we call a "context switch"
operation. The system save some registers values for the currently
process (kernel stack) and restore some values to from the soon-to-be-executing
process. To save the context of the currently running process the OS saves
some registers, PC, and kernel stack pointer of the currently-running process. Also
switch to the kernel stack for the soon-to-be-executing process.
