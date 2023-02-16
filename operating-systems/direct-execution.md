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
