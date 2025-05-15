# AACS2204 OCT 2024 Answers

[Link to the paper](https://eprints.tarc.edu.my/30256/1/QP-AACS2284.pdf)

- [Question 1](#question-1)
- [Question 2](#question-2)
- [Question 3](#question-3)
- [Question 4](#question-4)

## Answers

### Question 1

a)

- Active Multiprogramming is a time-sharing system allows each program to use a preset slice of CPU time. When the time slice expires, the job is interrupted and another job is given the CPU time. Example: A web browser which downloads a file and playing videos in different tabs are given CPU time in a round-robin fashion to allow them to run concurrently.
  > Basically round-robin scheduling.
- Passive Multiprogramming allows each program to be serviced in turn. The other jobs need to wait until the current job is completed before they can be serviced.
  > Basically first-come-first-serve scheduling, or any non-preemptive scheduling. Example: A printing system requires the other documents to wait until the current document is printed before the next document can be printed.

b)

- If the time quantum of a round-robin scheduling algorithm is too small, context switching will increase, which will spend more CPU time on the overhead of switching and reduces throughput.
- If the time quantum of a round-robin scheduling algorithm is too large, the waiting time of the jobs will increase, which will reduce the responsiveness of the system.
- The right amount of time quantum is the one that balances the CPU throughput and the waiting time of the jobs.

c)

i) SRTF (Preemptive)

```

|-----|-----|-----|-----|-----|-----|-----|
|  A  |  C  |  D  |  E  |  B  |  F  |  A  |
|-----|-----|-----|-----|-----|-----|-----|
0     3     5     8     9    13    17    22

```

| Process     | Arrival Time | CPU Cycle | Finish Time | Turnaround Time | Waiting Time |
| ----------- | ------------ | --------- | ----------- | --------------- | ------------ |
| A           | 0            | 8         | 22          | 22              | 14           |
| B           | 3            | 4         | 13          | 10              | 6            |
| C           | 3            | 2         | 5           | 2               | 0            |
| D           | 5            | 3         | 8           | 3               | 0            |
| E           | 7            | 1         | 9           | 2               | 1            |
| F           | 7            | 4         | 17          | 10              | 6            |
| **Average** |              |           |             | `49/6 = 8.1667` | `27/6 = 4.5` |

ii) SJN (Non-Preemptive)

```

|-----|-----|-----|-----|-----|-----|
|  A  |  E  |  C  |  D  |  B  |  F  |
|-----|-----|-----|-----|-----|-----|
0     8     9    11    14    18    22

```

| Process     | Arrival Time | CPU Cycle | Finish Time | Turnaround Time | Waiting Time    |
| ----------- | ------------ | --------- | ----------- | --------------- | --------------- |
| A           | 0            | 8         | 8           | 8               | 0               |
| B           | 3            | 4         | 18          | 15              | 11              |
| C           | 3            | 2         | 11          | 8               | 6               |
| D           | 5            | 3         | 14          | 9               | 6               |
| E           | 7            | 1         | 9           | 2               | 1               |
| F           | 7            | 4         | 22          | 15              | 11              |
| **Average** |              |           |             | `57/6 = 9.5`    | `35/6 = 5.8333` |

iii) Round Robin (3ms)

```

|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
|  A  |  B  |  C  |  A  |  D  |  B  |  E  |  F  |  A  |  F  |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
0     3     6     8    11    14    15    16    19    21    22

```

| Process     | Arrival Time | CPU Cycle | Finish Time | Turnaround Time  | Waiting Time    |
| ----------- | ------------ | --------- | ----------- | ---------------- | --------------- |
| A           | 0            | 8         | 21          | 21               | 13              |
| B           | 3            | 4         | 15          | 12               | 8               |
| C           | 3            | 2         | 8           | 5                | 3               |
| D           | 5            | 3         | 14          | 9                | 6               |
| E           | 7            | 1         | 16          | 9                | 8               |
| F           | 7            | 4         | 22          | 15               | 11              |
| **Average** |              |           |             | `71/6 = 11.8333` | `49/6 = 8.1667` |

iv) Preemptive Priority

```

|-----|-----|-----|-----|-----|-----|-----|
|  A  |  B  |  F  |  D  |  C  |  A  |  E  |
|-----|-----|-----|-----|-----|-----|-----|
0     3     7    11    14    16    21    22

```

| Process     | Arrival Time | CPU Cycle | Finish Time | Turnaround Time | Waiting Time    |
| ----------- | ------------ | --------- | ----------- | --------------- | --------------- |
| A           | 0            | 8         | 21          | 21              | 13              |
| B           | 3            | 4         | 7           | 4               | 0               |
| C           | 3            | 2         | 16          | 13              | 11              |
| D           | 5            | 3         | 14          | 9               | 6               |
| E           | 7            | 1         | 22          | 15              | 14              |
| F           | 7            | 4         | 11          | 4               | 0               |
| **Average** |              |           |             | `66/6 = 11`     | `44/6 = 7.3333` |
