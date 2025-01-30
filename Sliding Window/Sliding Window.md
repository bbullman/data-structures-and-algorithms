## Key Takeaways

* The sliding window pattern is used to process sequential data, strings, arrays, vectors, etc.*
* Can be viewed as a variation of two pointers, as there are two pointers used to indicate the edges of the window.
* Commonly used for substring and subarray problems as well as time series questions.
* Generally you want a time complexity of O(n) here.
* Generally the computation step when recalculating the window or some data within the window should be O(1) or a very slow growing funciton like O(logN) where N is small.
* Often you'll iterate from 0 to n-k+1 where n is the length of the sequence, k is the kernel, and +1 is the offset.

## Extra Notes

* You'll often iterate from 0 to N-K+1 where N is the length of the sequence, K is the subsequence.
* You can sometimes use a deque instead of two pointers. 
## Does this solution fit the Problem?

* Contiguous or linear data structure input. Sequences are key.
* Processing subsets of elements. If the problem requires repeated computation on a subset of data such as a subarray or substring, it's likely a sliding window candidate.
* Efficient computation time complexity if the window calculation is easy to calculate.
* Time intervals being mentioned is sometimes a good indicator.
## Sample Problems

* Maximum sum subarray of size K
* Longest substring without repeating characters

### Real-World

* **Telecommunications**: Number of users connected to a cellular network station in every k-time window
* **Video Streaming**: Given a stream of numbers representing buffering events in a user session, calculate the median number of events in an interval.
* **Social Media Content Mining:** Given lists of topics that two users have posted about, find the shortest sequence of posts by one user that includes all topics rom the other user.

