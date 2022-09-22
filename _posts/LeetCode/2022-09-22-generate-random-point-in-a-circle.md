---
layout: post
title: "Generate Random Point In A Circle Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Geometry, Rejection Sampling, Randomized ]
similar: [ Geometry ]
featured: false
hidden: false
excerpt: LeetCode 478. Given the radius and the position of the center of a circle, implement the function randPoint which generates a uniform random point inside the circle.

---

<br />

## Description

LeetCode Problem 478.

Given the radius and the position of the center of a circle, implement the function randPoint which generates a uniform random point inside the circle.

Implement the Solution class:
* Solution(double radius, double x_center, double y_center) initializes the object with the radius of the circle radius and the position of the center (x_center, y_center).
* randPoint() returns a random point inside the circle. A point on the circumference of the circle is considered to be in the circle. The answer is returned as an array [x, y].

Example 1:
```
Input
["Solution", "randPoint", "randPoint", "randPoint"]
[[1.0, 0.0, 0.0], [], [], []]
Output
[null, [-0.02493, -0.38077], [0.82314, 0.38945], [0.36572, 0.17248]]
Explanation
Solution solution = new Solution(1.0, 0.0, 0.0);
solution.randPoint(); // return [-0.02493, -0.38077]
solution.randPoint(); // return [0.82314, 0.38945]
solution.randPoint(); // return [0.36572, 0.17248]
```

Constraints:
* 0 < radius <= 10^8
* -10^7 <= x_center, y_center <= 10^7
* At most 3 * 10^4 calls will be made to randPoint.

<br />

## Sample C++ Code


```c
class Solution {
public:
    Solution(double radius, double x_center, double y_center) : 
    m_x_center(x_center), m_y_center(y_center), m_radius(radius) {}
    
    vector<double> randPoint() {
        double x, y;
        while (!isInCircle(x, y)) {
            x = (double)rand()/RAND_MAX * (m_radius + m_radius) + m_x_center - m_radius;
            y = (double)rand()/RAND_MAX * (m_radius + m_radius) + m_y_center - m_radius;
        }
        return {x, y};
    }
    
    bool isInCircle(double x, double y) { 
        return ((x - m_x_center) * (x - m_x_center) + 
            (y - m_y_center) * (y - m_y_center) <= m_radius * m_radius);
    } 
    
private:
    double m_x_center;
    double m_y_center;
    double m_radius;
};

/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(radius, x_center, y_center);
 * vector<double> param_1 = obj->randPoint();
 */
```


