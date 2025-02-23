# Amortized Time Complexity

## What is Amortized Time Complexity?
Amortized time complexity is the **average time per operation** over a sequence of operations, even if some individual operations take longer. It helps analyze the overall efficiency of an algorithm when certain expensive operations **don't happen every time** but are spread out over multiple operations.

## Key Idea
Even if some operations are expensive (e.g., O(N)), they happen **infrequently**, making the **average cost per operation lower**.

## Example: Queue-Based `ping()` Function
```cpp
#include <queue>

class RecentCounter {
    std::queue<int> q;

public:
    int ping(int t) {
        int threshold = t - 3000;
        while (!q.empty() && q.front() < threshold) {
            q.pop();
        }
        q.push(t);
        return q.size();
    }
};
```
### **Why is it O(1) Amortized?**
- Each element is pushed **once** and popped **once**.
- Even if multiple elements are removed in one call, the total number of removals is at most **equal to insertions**.
- Hence, the **average cost per operation** remains **O(1) amortized**.

## Real-World Analogy
Imagine paying for a **yearly subscription**:
- You pay **once** for unlimited streaming.
- Some months you watch more, some months less.
- The **average cost per movie is low**, even if some days you watch many movies.

## Other Examples
1. **Dynamic Array Resizing (`std::vector`)**
   - When a `std::vector` grows beyond capacity, it **doubles in size**, taking O(N) time occasionally.
   - However, each element moves **only a few times**, so the **average insertion cost is O(1) amortized**.

## Conclusion
Amortized time complexity provides a more accurate analysis of algorithms that involve **occasional expensive operations** but maintain **efficient average performance** over time.