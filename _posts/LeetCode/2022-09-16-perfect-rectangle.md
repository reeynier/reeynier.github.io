---
layout: post
title: "Perfect Rectangle Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Line Sweep ]
similar: [ Line Sweep ]
featured: false
hidden: false
excerpt: LeetCode 391. Given an array rectangles where rectangles[i] = [x_i, y_i, a_i, b_i] represents an axis-aligned rectangle. The bottom-left point of the rectangle is (x_i, y_i) and the top-right point of it is (a_i, b_i).

---

<br />

## Description

LeetCode Problem 391.

Given an array rectangles where rectangles[i] = [x_i, y_i, a_i, b_i] represents an axis-aligned rectangle. The bottom-left point of the rectangle is (x_i, y_i) and the top-right point of it is (a_i, b_i).

Return true if all the rectangles together form an exact cover of a rectangular region.

Example 1:
```
Input: rectangles = [[1,1,3,3],[3,1,4,2],[3,2,4,4],[1,3,2,4],[2,3,3,4]]
Output: true
Explanation: All 5 rectangles together form an exact cover of a rectangular region.
```

Example 2:
```
Input: rectangles = [[1,1,2,3],[1,3,2,4],[3,1,4,2],[3,2,4,4]]
Output: false
Explanation: Because there is a gap between the two rectangular regions.
```

Example 3:
```
Input: rectangles = [[1,1,3,3],[3,1,4,2],[1,3,2,4],[3,2,4,4]]
Output: false
Explanation: Because there is a gap in the top center.
```

Example 4:
```
Input: rectangles = [[1,1,3,3],[3,1,4,2],[1,3,2,4],[2,2,4,4]]
Output: false
Explanation: Because two of the rectangles overlap with each other.
```

Constraints:
* 1 <= rectangles.length <= 2 * 10^4
* rectangles[i].length == 4
* -10^5 <= x_i, y_i, a_i, b_i <= 10^5

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isRectangleCover(vector<vector<int>>& rectangles) {
        long long int X1 = INT_MAX;
        long long int Y1 = INT_MAX;
        long long int X2 = INT_MIN;
        long long int Y2 = INT_MIN;
        
        unordered_set<string> points;
        long long int actualAreas = 0;
        for (auto & rectangle : rectangles){
            long long int x1 = rectangle[0];
            long long int y1 = rectangle[1];
            long long int x2 = rectangle[2];
            long long int y2 = rectangle[3];
            X1 = min(X1, x1); 
            Y1 = min(Y1, y1);
            X2 = max(X2, x2);
            Y2 = max(Y2, y2);
            actualAreas += abs(x1 - x2) * abs(y1 - y2);
            
            if(!points.erase(to_string(x1)+"#"+to_string(y1)))
                points.insert(to_string(x1)+"#"+to_string(y1));
            if(!points.erase(to_string(x1)+"#"+to_string(y2)))
                points.insert(to_string(x1)+"#"+to_string(y2));
            if(!points.erase(to_string(x2)+"#"+to_string(y1)))
                points.insert(to_string(x2)+"#"+to_string(y1));
            if(!points.erase(to_string(x2)+"#"+to_string(y2)))
                points.insert(to_string(x2)+"#"+to_string(y2));
        }
        
        long long int expectedAreas = abs(X1 - X2) * abs(Y1- Y2);
        if (actualAreas != expectedAreas) return false;
        if (points.size() != 4 ) return false;
        
        if (points.find (to_string(X1)+"#"+to_string(Y1)) == points.end()) return false;
        if (!points.count (to_string(X1)+"#"+to_string(Y2))) return false;
        if (!points.count (to_string(X2)+"#"+to_string(Y1))) return false;
        if (!points.count (to_string(X2)+"#"+to_string(Y2))) return false;
        
        return true;
    }
};
```


