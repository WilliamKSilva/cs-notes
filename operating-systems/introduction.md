# Operating Systems

This notes are being taken based on "Operating Systems: Three Easy Pieces" book

## Introdution to Operating Systems

A basic introduction for some essential topics of an OS

### Virtualization Concept 

- Operating Systems use a concept called virtualization, that consists of getting real
physical elements like memory, CPU, etc and transform that in a virtual process that
turns on to be much easier to use.
- For that concept OS provides a lot of native API's to let us developers handle with
this kind of resource in a simpler way.

### Memory Virtualization 
    
- A program is based on memory usage, data structures are saved on memory
- To read memory you need the memory address, to write on memory you need a value
- Each process has his own virtual memory (address space), you can run a process that uses the memory address
0x200000, but they are not sharing the same physical piece of memory.
- Physical memory however is actually a shared resource.

### Concurrency

- A concept used when we need to work on manny things at once on a program.
- Use different threads (a function that runs on the same memory space of other functions, with more than one of them active at a time).
- How the instructions of a concurrently program are executed is crucial to how the program itself will work, if the program don't run
some instructions at the same time for example odd things can happen at the final output.

### Persistence 

- Data can be easily lost on memory, DRAM for example has an volatile behavior,
not been used to persist long lived information. For that kind of thing we often
use I/O devices like hard drives, SSD's.
- On software side File System is the program that is used to save user system information
in a optimized and good way.
- Different from CPU and memory the OS does not have a virtual layer for disk data. Sometimes
we need to share that information between process.

### Others

- An OS needs to provide protection between apps, running manny programs has to be a safe process.
- Reliability is not a big point on OS, since all process are very connected to OS core functions,
so if our OS fails probably everything will fall a part.
