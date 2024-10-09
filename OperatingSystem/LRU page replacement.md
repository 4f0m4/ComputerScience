

LRU is a popular page replacement algorithm that keeps track of page usage over time. It replaces the page that has not been used for the longest period, under the assumption that pages used recently will likely be used again soon. This method aims to minimize page faults and improve overall system performance.

### Characteristics of LRU:

1. **Recent Usage Tracking**: LRU maintains a record of page access history to determine which pages are least recently used.
2. **Dynamic Decision Making**: It makes page replacement decisions based on actual usage patterns, adapting to varying workloads.

### How It Works:
- When a page fault occurs and a replacement is needed, the algorithm identifies the page that has not been accessed for the longest time.
- That page is then replaced with the new page being requested.

### Advantages:
- Generally provides better performance than simpler algorithms like FIFO and optimal page replacement, as it reflects actual usage patterns.
- Reduces the number of page faults by keeping frequently used pages in memory longer.

### Disadvantages:
- Requires additional overhead to maintain the usage history, which can complicate implementation.
- Can be resource-intensive in terms of time and space, especially if implemented using a naive approach (e.g., maintaining a list of page accesses).
- Not immune to the "Belady's Anomaly," although it typically performs better than FIFO in practical scenarios.

Overall, LRU is widely used in modern operating systems due to its effectiveness in minimizing page faults and optimizing memory usage, making it suitable for a variety of applications with dynamic access patterns.

```
// C++ program for page replacement algorithms
#include <iostream>
#include<bits/stdc++.h>
using namespace std;

int main()
{
    int n;
    cout<<"enter the number of pages : ";
    cin>>n;
    int pages[n];
    cout<<"Enter the reference string : ";
    for(int i=0; i<n; i++)
        cin>>pages[i];
    //int n = sizeof(pages)/sizeof(pages[0]);
    int capacity;
    cout<<"enter the number of frames : ";
    cin>>capacity;



    deque<int> q(capacity);
   // int count=0;
    int page_faults=0;
    deque<int>::iterator itr;
    q.clear();
    for(int i:pages)
    {

        // Insert it into set if not present
        // already which represents page fault
        itr = find(q.begin(),q.end(),i);
        if(!(itr != q.end()))
        {

            ++page_faults;

            // Check if the set can hold equal pages
            if(q.size() == capacity)
            {
                q.erase(q.begin());
                q.push_back(i);
            }
            else
            {
                q.push_back(i);

            }
        }
        else
        {
            // Remove the indexes page
            q.erase(itr);

            // insert the current page
            q.push_back(i);
        }

    }
    cout<<page_faults;
}


```
