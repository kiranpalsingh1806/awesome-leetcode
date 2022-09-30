# Design and Implementation

## Implement Queue Using Stack

```cpp
class MyQueue {
public:
    stack<int> S1, S2;
    
    void push(int x) {
        while(S1.size()) {
            S2.push(S1.top());
            S1.pop();
        }
        
        S2.push(x);
        
        while(S2.size()) {
            S1.push(S2.top());
            S2.pop();
        }
    }
    
    int pop() {
        int x = S1.top();
        S1.pop();
        return x;
    }
    
    int peek() {
        return S1.top();
    }
    
    bool empty() {
        return S1.empty();
    }
};

```

## Implement Stack Using Queue

```cpp
class MyStack {
public:
    queue<int> q1, q2;
    
    void push(int x) {
        q2.push(x);
        while(q1.size()) {
            q2.push(q1.front());
            q1.pop();
        }
        while(q2.size()) {
            q1.push(q2.front());
            q2.pop();
        }
    }
    
    int pop() {
        int x = q1.front();
        q1.pop();
        return x;
    }
    
    int top() {
        return q1.front();
    }
    
    bool empty() {
        return q1.empty();
    }
};
```

## Stock Price Fluctuation

```cpp
class StockPrice {
    map<int, int> m;
    multiset<int> s;
public:
    StockPrice() {}
    void update(int t, int p) {
        if (m.count(t)) {
            s.erase(s.find(m[t]));
        }
        m[t] = p;
        s.insert(p);
    }
    int current() {
        return m.rbegin()->second;
    }
    int maximum() {
        return *s.rbegin();
    }
    int minimum() {
        return *s.begin();
    }
};
```

## Time based Key-Value Store

```cpp
class TimeMap {
public:
    unordered_map<string, map<int, string, greater<>>> M;
    
    void set(string key, string value, int timestamp) {
        M[key][timestamp] = value;
    }
    
    string get(string key, int timestamp) {
        if (M.count(key) == 0) return "";
        auto it = M[key].lower_bound(timestamp);
        if(it == M[key].end()) {
            return "";
        } else {
            return it->second;
        }
    }
};

```

## Design Circular Queue

```cpp
class MyCircularQueue {
private:
    vector<int> v;
    int start = 0, len = 0;
public:
    MyCircularQueue(int k): v(k) {}
    bool enQueue(int value) {
        if (isFull()) return false;
        v[(start + len++) % v.size()] = value;
        return true;
    }
    bool deQueue() {
        if (isEmpty()) return false;
        start = (start + 1) % v.size();
        --len;
        return true;
    }
    int Front() {
        if (isEmpty()) return -1;
        return v[start];
    }
    int Rear() {
        if (isEmpty()) return -1;
        return v[(start + len - 1) % v.size()];
    }
    bool isEmpty() {
        return !len;
    }
    bool isFull() {
        return len == v.size();
    }
};
```