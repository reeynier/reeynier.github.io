---
layout: post
title: "Data Stream As Disjoint Intervals Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Binary Search, Design, Ordered Set ]
similar: [ Binary Search ]
featured: false
hidden: false
excerpt: LeetCode 352. Given a data stream input of non-negative integers a_1, a_2, ..., a_n, summarize the numbers seen so far as a list of disjoint intervals.

---

<br />

## Description

LeetCode Problem 352.

Given a data stream input of non-negative integers a_1, a_2, ..., a_n, summarize the numbers seen so far as a list of disjoint intervals.

Implement the SummaryRanges class:
* SummaryRanges() Initializes the object with an empty stream.
* void addNum(int val) Adds the integer val to the stream.
* int[][] getIntervals() Returns a summary of the integers in the stream currently as a list of disjoint intervals [start_i, end_i].

Example 1:
```
Input
["SummaryRanges", "addNum", "getIntervals", "addNum", "getIntervals", "addNum", "getIntervals", "addNum", "getIntervals", "addNum", "getIntervals"]
[[], [1], [], [3], [], [7], [], [2], [], [6], []]
Output
[null, null, [[1, 1]], null, [[1, 1], [3, 3]], null, [[1, 1], [3, 3], [7, 7]], null, [[1, 3], [7, 7]], null, [[1, 3], [6, 7]]]
Explanation
SummaryRanges summaryRanges = new SummaryRanges();
summaryRanges.addNum(1);      // arr = [1]
summaryRanges.getIntervals(); // return [[1, 1]]
summaryRanges.addNum(3);      // arr = [1, 3]
summaryRanges.getIntervals(); // return [[1, 1], [3, 3]]
summaryRanges.addNum(7);      // arr = [1, 3, 7]
summaryRanges.getIntervals(); // return [[1, 1], [3, 3], [7, 7]]
summaryRanges.addNum(2);      // arr = [1, 2, 3, 7]
summaryRanges.getIntervals(); // return [[1, 3], [7, 7]]
summaryRanges.addNum(6);      // arr = [1, 2, 3, 6, 7]
summaryRanges.getIntervals(); // return [[1, 3], [6, 7]]
```

Constraints:
* 0 <= val <= 10^4
* At most 3 * 10^4 calls will be made to addNum and getIntervals.

<br />

## Sample C++ Code

For a new number n, find and return the index of interval [s, t] such that s is the largest 'start' that is smaller than n. If no such interval exists, return -1. This is done using binary search.

For example,
* new number 5, intervals [[1,1], [4,6], [8,8]], binary search returns 1.
* new number 0, intervals [[1,1], [4,6], [8,8]], binary search returns -1.

After we find this 'index', there are three circumstances:
* intervals[index] already contains val. Do nothing.
* val can be merged into intervals[index+1]. Modify intervals[index+1].start to val.
* val can be merged into intervals[index]. Modify intervals[index].end to val.
* val can't be merged into either interval. Insert Interval( val, val).

Finally, after inserting val, we need to check whether intervals[index] and intervals[index+1] can be merged.

```c
class SummaryRanges {
private:
    vector<Interval> intervals = vector<Interval>();
    
    int binarySearch(vector<Interval> intervals, int val) {
        return binarySearchHelper(intervals, 0, intervals.size(), val);
    }
    
    int binarySearchHelper(vector<Interval> intervals, int start, int end, int val) {
        if (start == end) return -1;
        if (start+1 == end && intervals[start].start < val) return start;
        
        int mid = (start + end)/2;
        if (intervals[mid].start == val) {
            return mid;
        } else if (intervals[mid].start < val) {
            return binarySearchHelper(intervals, mid, end, val);
        } else { //intervals[mid] > val
            return binarySearchHelper(intervals, start, mid, val);
        }
    }
    
public:
    /** Initialize your data structure here. */
    SummaryRanges() {
        
    }
    
    /** For a new number n, find the last(biggest) interval
     *  [s,t], such that s < n. If no such interval exists, 
     *  return -1.
     */
    void addNum(int val) {
        int index = binarySearch(intervals, val);
        
        // intervals[index] contains val
        if (index != -1 && intervals[index].end >= val) {
            return;
        }
        
        if (index != intervals.size()-1 && val + 1 == intervals[index+1].start) {
            intervals[index+1].start = val;
        } else if (index != -1 && val - 1 == intervals[index].end) {
            intervals[index].end = val;
        } else {
            intervals.insert(intervals.begin() + index + 1, Interval(val, val));
        }
        
        //merge intervals[index] with intervals[index+1]
        if (index != -1 && intervals[index].end + 1 == intervals[index+1].start) {
            intervals[index].end = intervals[index+1].end;
            intervals.erase(intervals.begin()+index+1);
        }
        
        return;
    }
    
    vector<Interval> getIntervals() {
        return this->intervals;
    }
};
```


