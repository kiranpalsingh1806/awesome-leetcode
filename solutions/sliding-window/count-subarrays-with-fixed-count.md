## Count Subarrays With Fixed Count

```cpp
long long countSubarrays(vector<int>& A, int minK, int maxK) {
    long res = 0, jbad = -1, jmin = -1, jmax = -1, n = A.size();
    for (int i = 0; i < n; ++i) {
        if (A[i] < minK || A[i] > maxK) jbad = i;
        if (A[i] == minK) jmin = i;
        if (A[i] == maxK) jmax = i;
        res += max(0L, min(jmin, jmax) - jbad);
    }
    return res;
}
```