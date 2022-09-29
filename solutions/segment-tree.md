# Segment Tree

- [Segment Tree](#segment-tree)
  - [Sum of Even Numbers After Queries](#sum-of-even-numbers-after-queries)
  - [Range Sum Query Mutable](#range-sum-query-mutable)
  - [Longest Increasing Subsequence - II](#longest-increasing-subsequence---ii)
  - [Shifting Letters - II](#shifting-letters---ii)
  - [Falling Squares](#falling-squares)

## Sum of Even Numbers After Queries

```cpp
struct segtree {
    int size;
    vector<int> sums;

    void init(int n) {
        size = 1;
        while (size < n) size *= 2;
        sums.assign(2 * size, 0);
    }

    void set(int i, int v, int x, int lx, int rx) {
        if (rx - lx == 1){
            sums[x] = v % 2 == 0 ? v : 0;
            return;
        }
        int m = (lx + rx) / 2;
        if (i < m) set(i, v, 2 * x + 1, lx, m);
        else set(i, v, 2 * x + 2, m, rx);
        sums[x] = sums[2 * x + 1] + sums[2 * x + 2];
    }

    void set(int i, int v) {
        set(i, v, 0, 0, size);
    }

    int sum(int l, int r, int x, int lx, int rx) {
        if (lx >= r || l >= rx) return 0;
        if (lx >= l && rx <= r) return sums[x];
        int m = (lx + rx) / 2;
        int s1 = sum(l, r, 2 * x + 1, lx, m);
        int s2 = sum(l, r, 2 * x + 2, m, rx);
        return s1 + s2;
    }

    int sum(int l, int r) {
        return sum(l, r, 0, 0, size);
    }
};

class Solution {
public:
    vector<int> sumEvenAfterQueries(vector<int>& nums, vector<vector<int>>& queries) {
        int n = nums.size();
        segtree st;
        st.init(n);
        for (int i = 0; i < n; i++) st.set(i, nums[i]);
        vector<int> ans;
        for (auto q : queries) {
            int val = q[0], idx = q[1];
            st.set(idx, nums[idx] += val);
            ans.push_back(st.sum(0, n));
        }
        return ans;
    }
};
```

## Range Sum Query Mutable

```cpp
struct segtree {
    vector<long long> sums;
    int size;
    
    void init(int n) {
        size = 1;
        while (size < n) size *= 2;
        sums.assign(size * 2, 0LL);
    }
    
    void set(int i, int v, int x, int lx, int rx) {
        if (rx - lx == 1) {
            sums[x] = v;
            return;
        }
        int m = (lx + rx) / 2;
        if (i < m) {
            set(i, v, 2 * x + 1, lx, m);
        } else {
            set(i, v, 2 * x + 2, m, rx);
        }
        sums[x] = sums[2 * x + 1] + sums[2 * x + 2];
    }
    
    void set(int i, int v) {
        set(i, v, 0, 0, size);
    }
    
    long long sum(int l, int r, int x, int lx, int rx) {
        if (lx >= r || l >= rx) return 0;
        if (lx >= l && rx <= r) return sums[x];
        int m = (lx + rx) / 2;
        long long s1 = sum(l, r, 2 * x + 1, lx, m);
        long long s2 = sum(l, r, 2 * x + 2, m, rx);
        return s1 + s2;
    }
    
    
    long long sum(int l, int r) {
        return sum(l, r, 0, 0, size);
    }
};

class NumArray {
public:
    NumArray(vector<int>& nums) {
        n = nums.size();
        st.init(n);
        for (int i = 0; i < n; i++) {
            st.set(i, nums[i]);
        }
    }
    
    void update(int index, int val) {
        st.set(index, val);
    }
    
    int sumRange(int left, int right) {
        return st.sum(left, right + 1);
    }

private: 
    segtree st;
    int n;
};
```

## Longest Increasing Subsequence - II

```cpp
struct segtree {
    vector<long long> a;
    int size;
    
    void init(int n) {
        size = 1;
        while (size < n) size *= 2;
        a.assign(size * 2, 0LL);
    }
    
    void set(int i, int v, int x, int lx, int rx) {
        if (rx - lx == 1) {
            a[x] = v;
            return;
        }
        int m = (lx + rx) / 2;
        if (i < m) set(i, v, 2 * x + 1, lx, m);
        else set(i, v, 2 * x + 2, m, rx);
        a[x] = max(a[2 * x + 1], a[2 * x + 2]);
    }
    
    void set(int i, int v) {
        set(i, v, 0, 0, size);
    }
    
    long long op(int l, int r, int x, int lx, int rx) {
        if (lx >= r || l >= rx) return 0;
        if (lx >= l && rx <= r) return a[x];
        int m = (lx + rx) / 2;
        return max(op(l, r, 2 * x + 1, lx, m), op(l, r, 2 * x + 2, m, rx));
    }
    
    long long op(int l, int r) {
        return op(l, r, 0, 0, size);
    }
};

class Solution {
public:
    int lengthOfLIS(vector<int>& nums, int k) {
        segtree st;
        int n = nums.size(), ans = 0;
        st.init(1e5 + 5);
        for (auto x : nums) {
            // look for max of LIS from [x - k, x]
            int mx = st.op(max(0, x - k), x);
            ans = max(ans, mx + 1);
            st.set(x, mx + 1);
        }
        return ans;
    }
};
```

## Shifting Letters - II

```cpp
class Solution {
public:
    vector<int> seg;

    void upd(int l, int r, int v, int x, int lx, int rx) {
        if(lx > r or rx < l) return;
        if(lx >= l and rx <= r) {
            seg[x] += v;
            return;
        }
        int mid = (lx + rx) / 2;
        upd(l, r, v, 2 * x + 1, lx, mid);
        upd(l, r, v, 2 * x + 2, mid + 1, rx);
    }

    int query(int i, int x, int lx, int rx) {
        if(lx == rx) return seg[x];

        int mid = (lx + rx) / 2;

        if(i <= mid)
            return seg[x] + query(i, 2 * x + 1, lx, mid);

        return seg[x] + query(i, 2 * x + 2, mid + 1, rx);
    }
    
    string shiftingLetters(string s, vector<vector<int>>& shifts) {
        long x = 1;
        while(x <= s.length()) x <<= 1;
        seg.resize(2 * x, 0);
        
        for(int i = 0; i < shifts.size(); ++i) {
            int l = shifts[i][0], r = shifts[i][1], dir;
            if(shifts[i][2] == 0) dir = -1;
            else dir = 1;
            upd(l, r, dir, 0, 0, x - 1);
        }
        
        for(int i = 0; i < s.length(); ++i) {
            int shift = query(i, 0, 0, x - 1);
            int dir = (shift > 0) ? 1 : -1;
            shift = abs(shift) % 26; 
            
            shift *= dir;
            int cur = s[i] - 'a';
            cur = (cur + shift + 26) % 26;
            s[i] = char(cur + 'a');
        }
        return s;
    }
};
```

## Falling Squares

```cpp
class Solution {
    vector<int> tree;
    int N = 0;
    void updateAt(int i, int val) {
        i += N;
        tree[i] = val;
        while (i > 0) {
            i /= 2;
            tree[i] = max(tree[2 * i], tree[2 * i + 1]);
        }
    }
    void update(int begin, int end, int val) {
        for (int i = begin; i < end; ++i) updateAt(i, val);
    }
    int maxRange(int i, int j) {
        i += N;
        j += N;
        int ans = 0;
        while (i <= j) {
            if (i % 2) ans = max(ans, tree[i++]);
            if (j % 2 == 0) ans = max(ans, tree[j--]);
            i /= 2;
            j /= 2;
        }
        return ans;
    }
public:
    vector<int> fallingSquares(vector<vector<int>> & positions) {
	    vector<int> a;

	    for (auto& p : positions) {
	      a.push_back(p[0]);
	      a.push_back(p[0] + p[1]);
	    }

	    sort(a.begin(), a.end());
	    N = unique(a.begin(), a.end()) - a.begin();
	    a.resize(N);
        
	    tree.resize(2 * N + 1);

	    vector<int> res;

	    for (auto& p : positions) {
	      int l = lower_bound(a.begin(), a.end(), p[0]) - a.begin();
	      int r = lower_bound(a.begin(), a.end(), p[0] + p[1]) - a.begin();
	      int maxh = maxRange(l, r - 1);
	      update(l, r, maxh + p[1]);
	      res.push_back(maxRange(0, N));
	    }
	    return res;
	}
};
```

```cpp
struct segtree {
    vector<long long> a;
    int size;
    
    void init(int n) {
        size = 1;
        while (size < n) size *= 2;
        a.assign(size * 2, 0LL);
    }
    
    void set(int i, int v, int x, int lx, int rx) {
        if (rx - lx == 1) {
            a[x] = v;
            return;
        }
        int m = (lx + rx) / 2;
        if (i < m) set(i, v, 2 * x + 1, lx, m);
        else set(i, v, 2 * x + 2, m, rx);
        a[x] = max(a[2 * x + 1], a[2 * x + 2]);
    }
    
    void set(int i, int v) {
        set(i, v, 0, 0, size);
    }
    
    long long op(int l, int r, int x, int lx, int rx) {
        if (lx >= r || l >= rx) return 0;
        if (lx >= l && rx <= r) return a[x];
        int m = (lx + rx) / 2;
        return max(op(l, r, 2 * x + 1, lx, m), op(l, r, 2 * x + 2, m, rx));
    }
    
    long long op(int l, int r) {
        return op(l, r, 0, 0, size);
    }
};

class Solution {
public:
    
    vector<int> fallingSquares(vector<vector<int>>& positions) {
        
        int N;
        
        vector<int> a;
	    for (auto& p : positions) {
	      a.push_back(p[0]);
	      a.push_back(p[0] + p[1]);
	    }

	    sort(a.begin(), a.end());
	    N = unique(a.begin(), a.end()) - a.begin();
	    a.resize(N);
        
        
        segtree st;
        st.init(2 * N + 1);
	    // tree.resize(2 * N + 1);

	    vector<int> res;

	    for (auto& p : positions) {
	      int l = lower_bound(a.begin(), a.end(), p[0]) - a.begin();
	      int r = lower_bound(a.begin(), a.end(), p[0] + p[1]) - a.begin();
	      int maxh = st.op(l, r);
            
          for (int i = l; i < r; i++) {
              st.set(i, maxh + p[1]);
          }; 
            
	      res.push_back(st.op(0, N + 1));
	    }
	    return res;
    }
};
```