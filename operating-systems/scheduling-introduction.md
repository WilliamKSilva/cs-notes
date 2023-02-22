## Scheduling: Introduction

Schedulers employs high-level policies (called disciplines too)!

### Workload Assumptions

Workload are the processes running in the system!

- Some assumptions about the processes running on the system:

"Unrealistc assumptions"

1. Each job runs for the same amount of time.
2. All jobs arrive at the same time.
3. Once started, each job runs to completion.
4. All jobs only use the CPU (i.e., they perform no I/O)
5. The run-time of each job is known.

### Scheduling Metrics

Consist on ways of compare scheduling policies

- Turnaround Time: This metric consists on the time at which
the job completes minus the time at which the job arrived in
the system. There is also other metric called Fairness.

### Policies

- First In, First Out (FIFO)
- Shortest Job First (SJF)
- Shortest Time-to-Completion First (STCF)
- Round Robin

### A New Metric: Response Time

"We define response time as the time from when the job arrives in a
system to the first time it is scheduled."
