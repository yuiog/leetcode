# [2588. Count the Number of Beautiful Subarrays](https://leetcode.com/problems/count-the-number-of-beautiful-subarrays)

[中文文档](/solution/2500-2599/2588.Count%20the%20Number%20of%20Beautiful%20Subarrays/README.md)

## Description

<p>You are given a <strong>0-indexed</strong> integer array <code>nums</code>. In one operation, you can:</p>

<ul>
	<li>Choose two different indices <code>i</code> and <code>j</code> such that <code>0 &lt;= i, j &lt; nums.length</code>.</li>
	<li>Choose a non-negative integer <code>k</code> such that the <code>k<sup>th</sup></code> bit (<strong>0-indexed</strong>) in the binary representation of <code>nums[i]</code> and <code>nums[j]</code> is <code>1</code>.</li>
	<li>Subtract <code>2<sup>k</sup></code> from <code>nums[i]</code> and <code>nums[j]</code>.</li>
</ul>

<p>A subarray is <strong>beautiful</strong> if it is possible to make all of its elements equal to <code>0</code> after applying the above operation any number of times.</p>

<p>Return <em>the number of <strong>beautiful subarrays</strong> in the array</em> <code>nums</code>.</p>

<p>A subarray is a contiguous <strong>non-empty</strong> sequence of elements within an array.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [4,3,1,2,4]
<strong>Output:</strong> 2
<strong>Explanation:</strong> There are 2 beautiful subarrays in nums: [4,<u>3,1,2</u>,4] and [<u>4,3,1,2,4</u>].
- We can make all elements in the subarray [3,1,2] equal to 0 in the following way:
  - Choose [<u>3</u>, 1, <u>2</u>] and k = 1. Subtract 2<sup>1</sup> from both numbers. The subarray becomes [1, 1, 0].
  - Choose [<u>1</u>, <u>1</u>, 0] and k = 0. Subtract 2<sup>0</sup> from both numbers. The subarray becomes [0, 0, 0].
- We can make all elements in the subarray [4,3,1,2,4] equal to 0 in the following way:
  - Choose [<u>4</u>, 3, 1, 2, <u>4</u>] and k = 2. Subtract 2<sup>2</sup> from both numbers. The subarray becomes [0, 3, 1, 2, 0].
  - Choose [0, <u>3</u>, <u>1</u>, 2, 0] and k = 0. Subtract 2<sup>0</sup> from both numbers. The subarray becomes [0, 2, 0, 2, 0].
  - Choose [0, <u>2</u>, 0, <u>2</u>, 0] and k = 1. Subtract 2<sup>1</sup> from both numbers. The subarray becomes [0, 0, 0, 0, 0].
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,10,4]
<strong>Output:</strong> 0
<strong>Explanation:</strong> There are no beautiful subarrays in nums.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= nums[i] &lt;= 10<sup>6</sup></code></li>
</ul>

## Solutions

<!-- tabs:start -->

### **Python3**

```python
class Solution:
    def beautifulSubarrays(self, nums: List[int]) -> int:
        cnt = Counter({0: 1})
        ans = mask = 0
        for x in nums:
            mask ^= x
            ans += cnt[mask]
            cnt[mask] += 1
        return ans
```

### **Java**

```java
class Solution {
    public long beautifulSubarrays(int[] nums) {
        Map<Integer, Integer> cnt = new HashMap<>();
        cnt.put(0, 1);
        long ans = 0;
        int mask = 0;
        for (int x : nums) {
            mask ^= x;
            ans += cnt.getOrDefault(mask, 0);
            cnt.merge(mask, 1, Integer::sum);
        }
        return ans;
    }
}
```

### **C++**

```cpp
class Solution {
public:
    long long beautifulSubarrays(vector<int>& nums) {
        unordered_map<int, int> cnt{{0, 1}};
        long long ans = 0;
        int mask = 0;
        for (int x : nums) {
            mask ^= x;
            ans += cnt[mask];
            ++cnt[mask];
        }
        return ans;
    }
};
```

### **Go**

```go
func beautifulSubarrays(nums []int) (ans int64) {
	cnt := map[int]int{0: 1}
	mask := 0
	for _, x := range nums {
		mask ^= x
		ans += int64(cnt[mask])
		cnt[mask]++
	}
	return
}
```

### **...**

```

```

<!-- tabs:end -->