
FCFS is one of the simplest scheduling algorithms used in operating systems for managing processes in a queue. As the name suggests, it processes requests in the order they arrive, meaning the first process that arrives is the first one to be executed. This approach is straightforward and easy to implement, making it suitable for environments where simplicity is prioritized.

### Characteristics of FCFS:

1. **Non-preemptive**: Once a process starts executing, it runs to completion before any other process can take over.
2. **Fairness**: Every process gets a chance to run based on its arrival time, ensuring no starvation.
3. **Performance**: While easy to understand, FCFS can lead to inefficiencies, especially with longer processes arriving before shorter ones. This phenomenon is known as the "convoy effect," where short processes wait for long processes to complete.

### Advantages:
- Simple and easy to implement.
- No complex data structures are needed.

### Disadvantages:
- Poor average turnaround time and waiting time, particularly in mixed workloads.
- Long waiting times for short processes if they arrive after long ones.

Overall, FCFS is suitable for certain applications but may not be the best choice for systems requiring high efficiency and responsiveness.

# Code in cpp
## without arrival time
```
#include<iostream>
using namespace std;
int main(){
    int n;
    cout<<"Enter the number of process : ";
    cin>>n;
    int wt[n],b[n],ta[n],sum=0;
    cout<<"Enter the Burst Time for the processes recpectively: "<<endl;
    cout<<"process\t\tBurst Time"<<endl;
    for(int i=1; i<=n; i++)
    {
        cout<<"P"<<i<<"\t\t";
        cin>>b[i];

        wt[i]=sum;
        sum+=b[i];
        ta[i]=sum;
    }
int avgS=0;

cout<<"process\t\tWaiting Time\t\tturn around time"<<endl;
for(int i=1;i<=n;i++){

        cout<<"P"<<i<<"\t\t"<<wt[i]<<"\t\t\t"<<ta[i]<<endl;
        avgS+=wt[i];

}
cout<<"\nAverage Waiting Time : "<<(double)avgS/(double)n<<endl;

return 0;
}


```
![image](https://github.com/user-attachments/assets/4e55f05c-b26a-4147-bf64-0d8e08b7db0d)

## with arrival time

```
#include<iostream>
using namespace std;
int main(){
    int n;
    cout<<"Enter the number of process : ";
    cin>>n;
    int p[n],wt[n],b[n],sum=0,arrival[n];
    cout<<"Enter the Burst Time and Arrival Time for the processes recpectively: "<<endl;
    cout<<"process\t\tBurst Time\tArrival Time"<<endl;
    for(int i=1; i<=n; i++)
    {
        cout<<"P"<<i<<"\t\t";
        cin>>b[i]>>arrival[i];
        p[i]=i;

    }
    for(int i=1; i<n; i++)
    {
        for(int j=1; j<n; j++)
        {
            if(arrival[j+1]<arrival[j])
            {
                swap(arrival[j],arrival[j+1]);
                swap(b[j],b[j+1]);
                 swap(p[j],p[j+1]);

            }
        }
    }

    for(int i=1;i<=n;i++)
    {
        wt[i]=sum-arrival[i];
        sum+=b[i];

    }
int sumForAvg=0;

cout<<"process\t\tWaiting Time"<<endl;
for(int i=1;i<=n;i++){

        cout<<"P"<<p[i]<<"\t\t"<<wt[i]<<endl;
        sumForAvg+=wt[i];

}
cout<<"\nAverage Waiting Time : "<<(double)sumForAvg/(double)n<<endl;




return 0;
}


```

![image](https://github.com/user-attachments/assets/c6fcb116-41bd-4c8f-bb85-15e59e2e26bb)


