<h3> Problem </h3>
The median is the middle value in a sorted list of integers. For lists of even length, there is no middle value, so the median is the mean of the two middle values.

For example:

For arr = [1,2,3], the median is 2.
For arr = [1,2], the median is (1 + 2) / 2 = 1.5
Implement the MedianFinder class:

MedianFinder() initializes the MedianFinder object.
void addNum(int num) adds the integer num from the data stream to the data structure.
double findMedian() returns the median of all elements so far.

Example 1:

<pre>
    Input: ["MedianFinder", "addNum", "1", "findMedian", "addNum", "3" "findMedian", "addNum", "2", "findMedian"]

    Output: [null, null, 1.0, null, 2.0, null, 2.0]

    Explanation:
    MedianFinder medianFinder = new MedianFinder();
    medianFinder.addNum(1);    // arr = [1]
    medianFinder.findMedian(); // return 1.0
    medianFinder.addNum(3);    // arr = [1, 3]
    medianFinder.findMedian(); // return 2.0
    medianFinder.addNum(2);    // arr[1, 2, 3]
    medianFinder.findMedian(); // return 2.0
</pre>

<h3> Algorithm </h3>

<pre>

Step 1: To solve this problem, make two priority queues
Step 2: In one priority queue, store elements in ascending order and and ther other in descending order.
Step 3: Trick to this question is that whateven we put in descending ques should go in ascending queue, and when ascending queue get bigger that descending queue, transfer the lowest element from ascending to descending queue.
Step 4: for example we have encountered 1, then add it to descending que then pop it and add to ascending queue, but as the ascending queue is more in size so it'll go back in descending queue -: so it becomes -: asc queue = [], desc queue = [1]
        -> now we encountered 3, then again add it to descending que then pop it and add to ascending queue, now as the ascending queue is equal in size so there's no going back in descending queue -: so it becomes -: asc queue = [3], desc queue = [1]
        -> now we encountered 2, then again add it to descending que then pop it and add to ascending queue, now as the ascending queue is more in size so it'll go back in descending queue -: so it becomes -: asc queue = [3], desc queue = [2, 1]
Step 5: now suppose we have to find median, we can check if ascending is smaller than descending queue that means, there were odd number of elements, so we can take the first element of desc queue, we got our median -: 2 for [1,2,3]
Step 6: now suppose we have to find median when elements were [1,3], we can check if ascending is smaller than descending queue, that'll return false that means, there were even number of elements, so we can take the first element of desc and asc queue, and average it to get our median -: 1+3/2 = 1.5 for [1,3].


**Note: 
Time Complexity = O(n) (n is no of nodes of tree)
Space Complexity = O(n) 
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class MedianFinder {
    Queue< Integer> ascendingQueue;
    Queue< Integer> descendingQueue;

    public MedianFinder() {
        ascendingQueue = new PriorityQueue<>((a,b) -> (a-b));
        descendingQueue = new PriorityQueue<>((a,b) -> (b-a));
    }
    
    public void addNum(int num) {
        descendingQueue.add(num);
        ascendingQueue.add(descendingQueue.poll());

        if(descendingQueue.size() < ascendingQueue.size()){
            descendingQueue.add(ascendingQueue.poll());
        }
    }
    
    public double findMedian() {
        double numRet;
        if(descendingQueue.size() == ascendingQueue.size()){
            numRet = (double)(descendingQueue.peek() + ascendingQueue.peek())/2;
        }
        else{
            numRet = (double) descendingQueue.peek(); 
            }
        return numRet;
    }
}
``` </pre>