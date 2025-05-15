## Key Takeaways

* An interval is one such as [10, 20] seconds in a digital audio sequence sample.
* Merge intervals is a name given to a pattern of tasks that involve merging intersecting intervals, inserting new intervals into existing sets, or determining the minimum number of intervals needed to cover a range.
* Event scheduling, resource allocation, and time slot consideration are examples of merge intervals.
## Extra Notes

* Often these problems require tracking a previous intervals beginning and end in tuple format
* Often will have to append the first element to the output list prior to starting the algorithm
* Often will have to sort the intervals input
```python
# https://stackoverflow.com/questions/10695139/sort-a-list-of-tuples-by-2nd-item-integer-value
intervals = sorted(
    [(1, 2), (6, 7), (7, 9), (4, 5)], 
    key=lambda x: x[0] # for first element, for second element [1], etc.
)
```
## Does this solution fit the Problem?

* An array (or list, vector) of intervals as input
* Overlapping intervals. Does the problem require dealing with overlapping intervals, either to find unions, intersections, or gaps?
## Sample Problems

* Merge intervals: Given a sorted list of intervals, merge all overlapping intervals.
* Meeting rooms: Given an array of meeting time intervals consisting of start and end times, can a person attend all the meetings?
* Rideshare: Given an array or list of tuples indicating pickup and arrival time, determine if a driver can accommodate every ride in their queue
### Real-World

* Rideshare example already given
* Meeting or  scheduling
* Task scheduling in an operating system based on priority and schedule