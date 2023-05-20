# Top K Frequent Elements

## Link
https://leetcode.com/problems/top-k-frequent-elements/description/

## Solution
1. The first step is to build a hash map `element -> its frequency`. This step takes `O(N)` time where `N` is a number of elements in the list.
2. The second step is to build a heap of size `k` using `N` elements*. 
    - To add the first `k` elements takes a linear time `O(k)` in the average case, and `O(log1+log2+...+logk)=O(logk!)=O(klogk)` in the worst case. 
    - After the first `k` elements we start to push and pop at each step, `N - k` steps in total. The time complexity of heap push/pop is `O(logk)` and we do it `N - k` times that means `O((N−k)logk)` time complexity. Adding both parts up, we get `O(Nlogk)` time complexity for the second step.
3. The third and the last step is to convert the heap into an output array. That could be done in `O(klogk)` time.

## Code
```c++
vector<int> topKFrequent(vector<int>& nums, int k) {
    map<int, int> count;
    for(auto x: nums){
        count[x]++;
    }

    auto comp = [](pair<int, int> a, pair<int, int> b){return a.second > b.second;};
    priority_queue<pair<int, int>, vector<pair<int, int>>, decltype(comp)> pq(comp);

    for(auto &x: count){
        pq.push(x);
        if(pq.size() > k){
            pq.pop();
        }
    }

    vector<int> ans;
    while(pq.size() > 0){
        ans.push_back(pq.top().first);
        pq.pop();
    }
    return ans;
}
```

## Notes
1. While writing the custom comparator function, explicitly specifying data type of comp to `bool` gives a function signature error in the initialization of `priority_queue`.
