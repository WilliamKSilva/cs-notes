## Scheduling: The Multi-Level Feedback Queue

In this chapter of the book we will have a look on MLFQ 
a common way to deal with scheduling.

We will understand how to optmize "turnoround time" running
shorter jobs first.

We will also have a look on how to optmize "response time"
of our jobs.

### MLQF: Basic Rules

- What are the base algorithms from MLDF?
- The MLQF have multiple queues with different priorities levels
- MLQF decide which job to run based on the priority of the job itself
- A queue can have multiple jobs, so all the jobs on this specific queue
have the same priority

• Rule 1: If Priority(A) > Priority(B), A runs (B doesn’t).
• Rule 2: If Priority(A) = Priority(B), A & B run in RR (Round-Robin, run a process for a given time, than another).

"If, for example, a job
repeatedly relinquishes the CPU while waiting for input from the key-
board, MLFQ will keep its priority high, as this is how an interactive
process might behave. If, instead, a job uses the CPU intensively for long
periods of time, MLFQ will reduce its priority. In this way, MLFQ will try
to learn about processes as they run, and thus use the history of the job to
predict its future behavior."


### Attempt #1: How To Change Priority

- Rule 3: When a job enter the system is automatically placed on the top priority queue.
- Rule 4a: If the jobs uses all of the time slice provided to it, its priority 
is reduced one level
- Rule 4b: "If a job gives up the CPU before the time slice is up, it stays
at the same priority level"

### Problems With Our Current MLFQ

- The Starvation problem: What if there is multiple interactive jobs? Well the bottom level jobs will never
have CPU time.
- The Gaming problem: What if a high interactive job like an I/O is constantly using
the CPU and relinquishing it before its time slice ends? The priority level of this job will remain on the top level
and the lower level jobs will never be run.
- Behavior changes: What if a CPU bound job change his behavior to an interactive approach? Well, since
this job is listed as low priority he will be treated different from the other interactive jobs.

### Attempt #2: The Priority Boost

- To deal with CPU starvation we can "boost" the priority of all
the jobs at certain time, so all the jobs can run. Also, since
the jobs are all on high priority level, the scheduler also can
deal with a CPU bond job that has become a interactive one.

"• Rule 5: After some time period S, move all the jobs in the system
to the topmost queue."

### Attempt #3: Better Accounting

- Now how do we deal with the Gaming problem?

"The solution here is to perform better accounting of CPU time at each
level of the MLFQ. Instead of forgetting how much of a time slice a pro-
cess used at a given level, the scheduler should keep track; once a process
has used its allotment, it is demoted to the next priority queue. Whether
it uses the time slice in one long burst or many small ones does not matter.
We thus rewrite Rules 4a and 4b to the following single rule:
• Rule 4: Once a job uses up its time allotment at a given level (re-
gardless of how many times it has given up the CPU), its priority is
reduced (i.e., it moves down one queue)."
