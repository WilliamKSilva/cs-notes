# The Abstraction: The Process

What is a Process? Let's dig that out!

## The Abstraction: A process

- A running program on your OS is actually a process. The process
on his execution affects other parts of the system.
- A process is based on Machine State: What can the program access
in his life time? Memory for example, the process relies on his own
memory (address space), to read and write data. Registers are also
part of the process Machine State, examples of registeres are the program
counter (responsible for telling wich instruction will be called), a stack
pointer and a frame pointer, respectively responsible of dealing with function
parameters, local variables and return addresses. Also the process can have
access to a list of I/O information as well.

## Process API

Basically every OS nowadays will have some sort of API like
the described below to deal with process.

- Create: You need a way to create new process, like the one
that is executed when you double click an App icon.
- Destroy: Some process quit by themselves without you need to do nothing,
but sometimes you maybe will need to quit the program by yourself,
so a command for that is pretty good.
- Wait: Maybe you will need to wait a process to stop running.
- Other: A resume command, to stop and than comeback to a process is also
a avaiable command.
- Status: Information about a process that is running.

## Process Creation: A Little More Detail

How process start running? What magic the OS really makes for that?

- The OS needs to load the code and all of its static data (initialized variables)
to the memory, inside the address space of the process.
- The program actually is first stored on the disk in a format that can be executed.
Than the OS reads that chunk of bytes of the program and put all that on memory.
- Some of that memory goes to the stack (C programs use the stack memory for local
variables, function parameters, return addresses), OS allocate that memory and dedicate
to the running process. The OS also allocate some of that memory to the heap, the memory
on the heap is avaiable for the developer to request, using malloc and free. Data structes
like Linked Lists, Trees, Hash Tables, etc are allocated on the heap.
- The OS also do other tasks destinated to I/O settings, for input, output and errors,
so the programs can read from the terminal and write to the screen.

## Process State

A process can have different states:

- Running: the process is running on the processor, executing instructions.
- Ready: the process is ready to run but the OS not chosed to run the process
at the moment.
- Blocked: in this process the process has initialized some sort of process that
take a time to be done, like an I/O operation to the disk or a network package call.
So this process become blocked and give the CPU space to another process to run.

## Data Structures

- The OS needs an way to track that kind of information, like the state of each process.
For that kind of thing the OS uses some Data Structures like a process list to keep track
of each process that is running or a blocked process for example.
- OS has an register context for example, that is responsible of keep tracking of stopped
processes CPU registers content. Saving that kind of information provides a way to restore
this content on the physical register again and resume running the process that was blocked.
This is called Context Switch.



