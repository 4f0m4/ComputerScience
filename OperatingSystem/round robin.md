Round Robin (RR) is a time-sharing scheduling algorithm designed to allocate CPU time to processes in a fair and cyclic manner. Each process is assigned a fixed time slice, or quantum, during which it can execute. If a process does not complete within its allotted time, it is paused and moved to the back of the queue, allowing the next process to execute.

### Characteristics of Round Robin:

1. **Preemptive**: The algorithm is inherently preemptive, as processes are interrupted after their time slice expires, ensuring that all processes receive CPU time.
2. **Time Quantum**: The choice of time quantum significantly affects the performance; a very short quantum can lead to high context switching overhead, while a very long quantum can degrade responsiveness.

### Advantages:
- Fairness: Every process gets an equal opportunity to execute, making it suitable for time-sharing systems.
- Simple and easy to implement, providing good responsiveness for interactive applications.

### Disadvantages:
- Can lead to high context-switching overhead if the time quantum is too short.
- Average turnaround and waiting times may be higher compared to other algorithms like SJF, particularly for processes with varying execution times.

Overall, Round Robin is an effective scheduling algorithm for multi-user and time-sharing systems, balancing responsiveness and fairness, though care must be taken in selecting an appropriate time quantum to optimize performance.


# code in cpp

```
#include<iostream>
using namespace std;

int main()
{
    int bt[20], wt[20], at[20], rt[20], p[20], tq, time, remain, i, j, done, n;
    float wtavg = 0;
    cout << "Enter the number of processes: ";
    cin >> n;
    cout << "Enter the arrival time of processes: ";
    for (i = 0; i < n; i++)
        cin >> at[i];
    cout << "Enter the burst time of processes: ";
    for (i = 0; i < n; i++)
    {
        cin >> bt[i];
        rt[i] = bt[i];       // Initially the entire burst time is remaining
        p[i] = i + 1;
    }
    cout << "Enter the time quantum: ";
    cin >> tq;




    for (i = 0; i < n; i++)   // Bubble sort
    {
        for (j = 0; j < n - 1; j++)
        {
            if (at[j] > at[j + 1]) // Smaller arrival time are moved to the front
            {
                swap(at[j], at[j + 1]);
                swap(bt[j], bt[j + 1]);
                swap(rt[j], rt[j + 1]);
                swap(p[j], p[j + 1]);
            }
        }
    }

    cout << "\nProcess \t Arrival Time \t Burst Time\t Waiting Time";
    i = 0, time = at[0], remain = n; // Current time is 0 and all processes are remaining
    while (remain != 0)
    {
        if (rt[i] <= tq && rt[i] > 0) // Remaining burst time of the process is less than time quantum but not less than zero
        {
            time += rt[i]; // Only remaining burst time is given and current time is increased
            rt[i] = 0;      // This process has no remaining burst time
            done = 1;       // This process is done now
        }
        else if (rt[i] > 0) // Remaining burst time is not less than time quantum
        {
            rt[i] -= tq;     // Remaining burst time decreased
            time += tq;      // Current time increased
        }
        if (rt[i] == 0 && done == 1) // Process has no remaining burst time and has been done
        {
            remain--; // Remaining processes are decreased because this process is finished
            wt[i] = time - at[i] - bt[i]; // Waiting time calculated from finish time
            cout << "\n" << p[i] << "\t\t" << at[i] << "\t\t" << bt[i] << "\t\t" << wt[i];
            done = 0;  // Done is set to 0, so this process won't be considered again
            wtavg += wt[i];
        }

        for (j = i; j < n - 1; j++) // Bringing processes that arrived in the current time to the front
        {
            if (at[j + 1] <= time) // Placing the current process at the end of them
            {
                swap(at[j], at[j + 1]);
                swap(bt[j], bt[j + 1]);
                swap(rt[j], rt[j + 1]);
                swap(p[j], p[j + 1]);
            }
        }
    }

    cout << "\n\nAverage waiting time = " << wtavg / n << endl;
    return 0;
}


```
