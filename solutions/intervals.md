# Intervals

## Merge Intervals

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& A) {
        
        sort(A.begin(), A.end());
        vector<vector<int>> ans;
        
        for(auto &a : A) {
            if(ans.empty() || a[0] > ans.back()[1]) {
                ans.push_back(a);
            } else {
                ans.back()[1] = max(a[1], ans.back()[1]);
            }
        }
        
        return ans;
    }
};
```

</details>

## Insert Interval

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        int start = newInterval[0], end = newInterval[1];
        
        vector<vector<int>> ans;
        
        for(auto &intv : intervals) {
            // Four cases
            
            if(start > end) {
                ans.push_back(intv);
            } else if(end < intv[0]) {
                ans.push_back({start, end});
                start = end + 1;
                ans.push_back(intv);
            } else if(start > intv[1]) {
                ans.push_back(intv);
            } else {
                // Update start and end
                start = min(start, intv[0]);
                end = max(end, intv[1]);
            }
        }
        
        if(start <= end) {
            ans.push_back({start, end});
        }
        
        return ans;
    }
};
```

</details>

## Non Overlapping Interval

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    int eraseOverlapIntervals(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end(), [](auto &a, auto &b) {
            return a[1] < b[1];
        });
        
        int overlapCnt = 0;
        int end = INT_MIN;
        
        for(auto &e : intervals) {
            if(e[0] >= end) {
                end = e[1];
            } else {
                overlapCnt++;
            }
        }
        
        return overlapCnt;
    }
};
```

</details>

## Minimum Number of Arrows To Burst Balloons

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    int findMinArrowShots(vector<vector<int>>& points) {
        sort(points.begin(), points.end(), [](auto &a, auto &b) {
            return a[1] < b[1];
        });
        
        long end = LONG_MIN;
        long answer = points.size();
        
        for(auto &p : points) {
            if(p[0] <= end) {
                answer--;
            } else {
                end = p[1];
            }
        }
        
        return answer;
    }
};
```

</details>

## My Calendar I

<details>
<summary> View Code </summary>

```cpp
class MyCalendar {
public:
    MyCalendar() {
        
    }

    map<int, int> M;
    
    bool book(int start, int end) {
        
        if(M.empty()) {
            M[start] = end;
            return true;
        }
        
        // Conditions 
        
        auto it = M.upper_bound(start);
        
        // Check the later intersection
        if(it != M.end() && it->first < end) return false;
        
        // Check the starting intersection
        if(it != M.begin() && prev(it)->second > start) return false;
        
        
        // After checking conditions
        M[start] = end;
        return true;
    }
};
```

</details>

## Video Stitching

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    int videoStitching(vector<vector<int>>& clips, int time) {
        sort(clips.begin(), clips.end());
        int N = clips.size();
        int ans = 0;
        for(int i = 0, st = 0, end = 0; st < time; st = end, ans++) {
            while(i < N && clips[i][0] <= st) {
                end = max(end, clips[i++][1]);
            }
            if(st == end) {
                return -1;
            }
        }
        return ans;
    }
};
```

</details>