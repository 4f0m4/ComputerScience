

FIFO (First-In, First-Out) is a simple page replacement algorithm used in operating systems to manage memory pages. The FIFO algorithm maintains a queue of pages in memory, and when a page fault occurs (i.e., a requested page is not in memory), the oldest page (the one that has been in memory the longest) is replaced with the new page.

### Characteristics of FIFO:

1. **Queue Structure**: Pages are organized in a queue. The page that has been in memory the longest is at the front, while the newest page is at the back.
2. **Simple Implementation**: The FIFO algorithm is easy to implement, as it requires minimal bookkeeping to manage the queue of pages.

### How It Works:
- When a page fault occurs, the algorithm removes the page at the front of the queue and adds the new page to the back.
- This process continues for each page fault until the desired page is in memory.

### Advantages:
- Easy to understand and implement, requiring straightforward data structures.
- Fair in terms of treating all pages equally based on their age in memory.

### Disadvantages:
- Can lead to poor performance, particularly in situations with a high number of page faults, as it may replace frequently used pages simply because they were loaded earlier. This is known as the "Belady's Anomaly," where increasing the number of page frames can lead to an increase in page faults.
- Lacks consideration for page usage patterns, which can lead to inefficient memory utilization.

Overall, while FIFO is simple and easy to implement, it may not be the most efficient choice for managing memory in systems with varying access patterns and workloads. More advanced algorithms, such as LRU (Least Recently Used) or optimal page replacement, can offer better performance in many scenarios.
# code in cpp

```
// C++ implementation of FIFO page replacement
// in Operating Systems.
#include<bits/stdc++.h>
using namespace std;

// Function to find page faults using FIFO
int pageFaults(int pages[], int n, int capacity)
{
	// To represent set of current pages. We use
	// an unordered_set so that we quickly check
	// if a page is present in set or not
	unordered_set<int> s;

	// To store the pages in FIFO manner
	queue<int> indexes;

	// Start from initial page
	int page_faults = 0;
	for (int i=0; i<n; i++)
	{
		// Check if the set can hold more pages
		if (s.size() < capacity)
		{
			// Insert it into set if not present
			// already which represents page fault
			if (s.find(pages[i])==s.end())
			{
				// Insert the current page into the set
				s.insert(pages[i]);

				// increment page fault
				page_faults++;

				// Push the current page into the queue
				indexes.push(pages[i]);
			}
		}

		// If the set is full then need to perform FIFO
		// i.e. remove the first page of the queue from
		// set and queue both and insert the current page
		else
		{
			// Check if current page is not already
			// present in the set
			if (s.find(pages[i]) == s.end())
			{
				// Store the first page in the
				// queue to be used to find and
				// erase the page from the set
				int val = indexes.front();

				// Pop the first page from the queue
				indexes.pop();

				// Remove the indexes page from the set
				s.erase(val);

				// insert the current page in the set
				s.insert(pages[i]);

				// push the current page into
				// the queue
				indexes.push(pages[i]);

				// Increment page faults
				page_faults++;
			}
		}
	}

	return page_faults;
}

// Driver code
int main()
{
	int n;
	cout<<"enter the number of pages : ";
	cin>>n;
	int pages[n];
	cout<<"Enter the reference string : ";
	for(int i=0;i<n;i++)
        cin>>pages[i];
	//int n = sizeof(pages)/sizeof(pages[0]);
	int capacity;
    cout<<"enter the number of frames : ";
	cin>>capacity;
	cout <<"Total Page fault : "<< pageFaults(pages, n, capacity);
	return 0;
}
// 7 0 1 2 0 3 0 4 2 3 0 3 2 1 2 0 1 7 0 1
```
