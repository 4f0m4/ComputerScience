
SJF is a process scheduling algorithm that selects the process with the shortest execution time to run next. This method aims to minimize the average waiting time and turnaround time for a set of processes.

### Characteristics of SJF:

1. **Preemptive and Non-preemptive**: In its non-preemptive form, once a process starts executing, it runs to completion. In the preemptive version, if a new process arrives with a shorter execution time than the currently running process, the scheduler can interrupt the current process and run the shorter one.
2. **Optimal for Average Waiting Time**: SJF minimizes the average waiting time for a set of processes, making it efficient in terms of resource utilization.

### Advantages:
- Reduces average waiting and turnaround times compared to FCFS and other scheduling algorithms.
- Suitable for batch processing systems where job lengths are known in advance.

### Disadvantages:
- Difficulty in knowing the length of the next job in a general-purpose system.
- Can lead to starvation, where longer processes may wait indefinitely if shorter processes keep arriving.

Overall, SJF is effective in specific contexts, particularly where job lengths can be predicted, but it may not be suitable for all environments due to its potential for starvation and complexity in implementation.

# Code in cpp
## without arrival
![image](https://github.com/user-attachments/assets/474692e1-93c6-4545-8ec5-30ce806c0ca4)

```
#include<iostream>
using namespace std;
int main()
{
    int n;
    cout<<"Enter the number of process : ";
    cin>>n;
    int p[n],b[n],sum=0;
    cout<<"Enter the Burst Time for the processes recpectively: "<<endl;
    cout<<"process\t\tBrust Time"<<endl;
    for(int i=1; i<=n; i++)
    {
        cout<<"P"<<i<<"\t\t";
        cin>>b[i];
        p[i]=i;
    }

    for(int i=1; i<n; i++)
    {
        for(int j=1; j<n; j++)
        {
            if(b[j+1]<b[j])
            {
                swap(b[j],b[j+1]);
                swap(p[j],p[j+1]);
            }
        }
    }
    cout<<"After sorting according to shortest job first : "<<endl;
for(int i=1; i<=n; i++)
    {
       // cout<<b[i]<<endl;
        cout<<"P"<<p[i]<<"\t\t"<<b[i]<<endl;

    }

    int avgS=b[1],w=0,ta,tas=0;
    cout<<"process\t\tWaiting Time\t\tturn around time"<<endl;
    cout<<"P"<<p[1]<<"\t\t"<<0<<"\t\t\t"<<b[1]<<endl;
    for(int i=2; i<=n; i++)
    {
        w+=avgS;
        ta = avgS+b[i];

        cout<<"P"<<p[i]<<"\t\t"<<avgS<<"\t\t\t"<<ta<<endl;

        avgS+=b[i];
        tas+=ta;


       // cout<<w<<endl;
    }
    cout<<"\nAverage Waiting Time : "<<(double)w/(double)n<<endl;
 cout<<"\nAverage turn around Time : "<<(double)tas/(double)n<<endl;




    return 0;
}

```
![image](https://github.com/user-attachments/assets/29c57b1f-db15-4e71-b2c3-4230dc7e6486)

## with arrival
![image](https://github.com/user-attachments/assets/9df03ec3-69c4-4b31-b6aa-d75a166f2be3)

```
#include<iostream>
using namespace std;

int main() {
    int n, time_tracker = 0, mini_arrival, d, i, j;
    float awt = 0;

    cout << "Enter no of process: ";
    cin >> n;
    int a[n], b[n], e[n], wt[n], p[n];

    // Input arrival times and burst times for each process
    for (i = 0; i < n; i++) {
        p[i] = i + 1;
        cout << "Enter arrival time and burst time for P" << p[i] << ": ";
        cin >> a[i] >> b[i];
    }

    // Sort processes by burst time in ascending order
    for (i = 0; i < n; i++) {
        for (j = i + 1; j < n; j++) {
            if (b[i] > b[j]) {
                swap(a[i], a[j]);
                swap(p[i], p[j]);
                swap(b[i], b[j]);
            }
        }
    }

    // Find the process with the mini_arrivalimum arrival time
    mini_arrival = a[0];
    for (i = 0; i < n; i++) {
        if (mini_arrival > a[i]) {
            mini_arrival = a[i];
            d = i;
        }
    }

    time_tracker = mini_arrival;
    e[d] = time_tracker + b[d];
    time_tracker = e[d];

    // Calculate completion times for the rest of the processes
    for (i = 0; i < n; i++) {
        if (a[i] != mini_arrival) {
            e[i] = b[i] + time_tracker;
            time_tracker = e[i];
        }
    }

    // Calculate waiting times and average waiting time
    for (i = 0; i < n; i++) {
        wt[i] = e[i] - a[i] - b[i];
        awt += wt[i];
    }

    awt /= n;

    // Print waiting times and average waiting time
    cout << "Process\tWaiting-time(s)" << endl;
    for (i = 0; i < n; i++) {
        cout << "P" << p[i] << "\t" << wt[i] << endl;
    }
    cout << "Average Waiting Time=" << awt << endl;

    return 0;
}

```
![image](https://github.com/user-attachments/assets/1bc8b619-7fbc-4091-85b5-5a3f42f4ca85)

