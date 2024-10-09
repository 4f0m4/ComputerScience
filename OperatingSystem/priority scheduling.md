Priority scheduling is a method used by operating systems to manage processes based on their priority levels. Each process is assigned a priority, and the scheduler selects processes for execution based on their priority, with higher-priority processes being executed before lower-priority ones.

### Characteristics of Priority Scheduling:

1. **Preemptive and Non-preemptive**: In preemptive priority scheduling, if a new process arrives with a higher priority than the currently running process, the scheduler may interrupt the current process. In non-preemptive priority scheduling, a running process will not be interrupted until it completes or voluntarily yields control.
2. **Static and Dynamic Priorities**: Priorities can be static (fixed for the lifetime of the process) or dynamic (changing based on certain criteria, such as aging to prevent starvation).

### Advantages:
- Allows important tasks to be processed quickly, making it suitable for real-time systems where certain tasks are more critical.
- Flexibility in defining priorities based on various factors, such as resource needs or user requirements.

### Disadvantages:
- Potential for starvation, where lower-priority processes may wait indefinitely if higher-priority processes continually arrive.
- Complexity in determining the appropriate priority levels and managing changes.

Overall, priority scheduling is effective for scenarios requiring task prioritization but must be managed carefully to mitigate issues like starvation and ensure fairness among processes.

# Code in cpp

## without arrival time
![image](https://github.com/user-attachments/assets/a8d4b72b-f632-4f0b-a5f6-87f33c5be597)

```
#include<iostream>
using namespace std;
int main()
{
    int n;
    cout<<"Enter the number of process : ";
    cin>>n;
    int p[n],b[n],pr[n],sum=0;
    cout<<"Enter the Burst Time for the processes recpectively: "<<endl;
    cout<<"process\tBrust Time\tPriority"<<endl;
    for(int i=1; i<=n; i++)
    {
        cout<<"P"<<i<<"\t";
        cin>>b[i];
        cin>>pr[i];
        p[i]=i;
    }

    for(int i=1; i<n; i++)
    {
        for(int j=1; j<n; j++)
        {
            if(pr[j+1]>pr[j])
            {
                swap(pr[j],pr[j+1]);
                swap(b[j],b[j+1]);
              swap(p[j],p[j+1]);
            }
        }
    }
    cout<<"\nAfter sorting according to priority: "<<endl;
    cout<<"process\t\tBrust Time\t\tPriority"<<endl;
    for(int i=1; i<=n; i++)
    {
       // cout<<b[i]<<endl;
        cout<<"P"<<p[i]<<"\t\t"<<b[i]<<"\t\t\t"<<pr[i]<<endl;

    }

    int avgS=b[1],w=0;
    cout<<"process\t\tWaiting Time"<<endl;
    cout<<"P"<<p[1]<<"\t\t"<<0<<endl;
    for(int i=2; i<=n; i++)
    {
        w+=avgS;

        cout<<"P"<<p[i]<<"\t\t"<<avgS<<endl;

        avgS+=b[i];


       // cout<<w<<endl;
    }
    cout<<"\nAverage Waiting Time : "<<(double)w/(double)n<<endl;




    return 0;
}

```
![image](https://github.com/user-attachments/assets/be400877-473f-413e-a753-817224352569)


## With arrival time

```
//high number highest priority

#include<iostream>

 using namespace std;
int main()
{
    int a[10],b[10],x[10];
    int waiting[10],turnaround[10],completion[10],p[10];
    int i,j,smallest,count=0,time,n;
    double avg=0,tt=0,end;

   cout<<"\nEnter the number of Processes: ";
    cin>>n;
    for(i=0;i<n;i++)
    {
      cout<<"\nEnter arrival time of process: ";
      cin>>a[i];
    }
    for(i=0;i<n;i++)
    {
      cout<<"\nEnter burst time of process: ";
      cin>>b[i];
    }
    for(i=0;i<n;i++)
    {
      cout<<"\nEnter priority of process: ";
      cin>>p[i];
    }
    for(i=0; i<n; i++)
        x[i]=b[i];

    p[9]=-1;
    for(time=0; count!=n; time++)
    {
        smallest=9;
        for(i=0; i<n; i++)
        {
            if(a[i]<=time && p[i]>p[smallest] && b[i]>0 )
                smallest=i;
        }
        b[smallest]--;

        if(b[smallest]==0)
        {
            count++;
            end=time+1;
            completion[smallest] = end;
            waiting[smallest] = end - a[smallest] - x[smallest];
            turnaround[smallest] = end - a[smallest];
        }
    }
     cout<<"Process"<<"\t"<< "burst-time"<<"\t"<<"arrival-time" <<"\t"<<"waiting-time" <<"\t"<<"turnaround-time"<< "\t"<<"completion-time"<<"\t"<<"Priority"<<endl;
    for(i=0; i<n; i++)
    {
         cout<<"p"<<i+1<<"\t\t"<<x[i]<<"\t\t"<<a[i]<<"\t\t"<<waiting[i]<<"\t\t"<<turnaround[i]<<"\t\t"<<completion[i]<<"\t\t"<<p[i]<<endl;
        avg = avg + waiting[i];
        tt = tt + turnaround[i];
    }
   cout<<"\n\nAverage waiting time ="<<avg/n;
    cout<<"  Average Turnaround time ="<<tt/n<<endl;
}

```

