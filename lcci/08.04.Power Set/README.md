# [面试题 08.04. 幂集](https://leetcode-cn.com/problems/power-set-lcci)

[English Version](/lcci/08.04.Power%20Set/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->
<p>幂集。编写一种方法，返回某集合的所有子集。集合中<strong>不包含重复的元素</strong>。</p>

<p>说明：解集不能包含重复的子集。</p>

<p><strong>示例:</strong></p>

<pre><strong> 输入</strong>： nums = [1,2,3]
<strong> 输出</strong>：
[
  [3],
&nbsp; [1],
&nbsp; [2],
&nbsp; [1,2,3],
&nbsp; [1,3],
&nbsp; [2,3],
&nbsp; [1,2],
&nbsp; []
]
</pre>

## 解法

<!-- 这里可写通用的实现逻辑 -->

回溯法

<!-- tabs:start -->

### **Python3**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        def dfs(u, t):
            if u == len(nums):
                ans.append(t[:])
                return
            t.append(nums[u])
            dfs(u + 1, t)
            t.pop()
            dfs(u + 1, t)

        ans = []
        dfs(0, [])
        return ans
```

### **Java**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```java
class Solution {
    private List<List<Integer>> ans;
    private int[] nums;

    public List<List<Integer>> subsets(int[] nums) {
        ans = new ArrayList<>();
        this.nums = nums;
        dfs(0, new ArrayList<>());
        return ans;
    }

    private void dfs(int u, List<Integer> t) {
        if (u == nums.length) {
            ans.add(new ArrayList<>(t));
            return;
        }
        t.add(nums[u]);
        dfs(u + 1, t);
        t.remove(t.size() - 1);
        dfs(u + 1, t);
    }
}
```

### **JavaScript**

```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var subsets = function (nums) {
    let prev = [];
    let res = [];
    dfs(nums, 0, prev, res);
    return res;
};

function dfs(nums, depth, prev, res) {
    res.push(prev.slice());
    for (let i = depth; i < nums.length; i++) {
        prev.push(nums[i]);
        depth++;
        dfs(nums, depth, prev, res);
        prev.pop();
    }
}
```

### **TypeScript**

```ts
function subsets(nums: number[]): number[][] {
    const res = [[]];
    nums.forEach(num => {
        res.forEach(item => {
            res.push(item.concat(num));
        });
    });
    return res;
}
```

```rust
function subsets(nums: number[]): number[][] {
    const n = nums.length;
    const res = [];
    const list = [];
    const dfs = (i: number) => {
        if (i === n) {
            res.push([...list]);
            return;
        }
        list.push(nums[i]);
        dfs(i + 1);
        list.pop();
        dfs(i + 1);
    };
    dfs(0);
    return res;
}
```

### **Rust**

```rust
impl Solution {
    pub fn subsets(nums: Vec<i32>) -> Vec<Vec<i32>> {
        let n = nums.len();
        let mut res: Vec<Vec<i32>> = vec![vec![]];
        for i in 0..n {
            for j in 0..res.len() {
                res.push(vec![..res[j].clone(), vec![nums[i]]].concat());
            }
        }
        res
    }
}
```

```rust
impl Solution {
    fn dfs(nums: &Vec<i32>, i: usize, res: &mut Vec<Vec<i32>>, list: &mut Vec<i32>) {
        if i == nums.len() {
            res.push(list.clone());
            return;
        }
        list.push(nums[i]);
        Self::dfs(nums, i + 1, res, list);
        list.pop();
        Self::dfs(nums, i + 1, res, list);
    }

    pub fn subsets(nums: Vec<i32>) -> Vec<Vec<i32>> {
        let mut res = vec![];
        Self::dfs(&nums, 0, &mut res, &mut vec![]);
        res
    }
}
```

### **C++**

```cpp
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<int> t;
        vector<vector<int>> ans;
        dfs(0, t, nums, ans);
        return ans;
    }

    void dfs(int u, vector<int>& t, vector<int>& nums, vector<vector<int>>& ans) {
        if (u == nums.size())
        {
            ans.push_back(t);
            return;
        }
        t.push_back(nums[u]);
        dfs(u + 1, t, nums, ans);
        t.pop_back();
        dfs(u + 1, t, nums, ans);
    }
};
```

### **Go**

```go
func subsets(nums []int) [][]int {
	var ans [][]int
	var dfs func(u int, t []int)
	dfs = func(u int, t []int) {
		if u == len(nums) {
			cp := make([]int, len(t))
			copy(cp, t)
			ans = append(ans, cp)
			return
		}
		t = append(t, nums[u])
		dfs(u+1, t)
		t = t[:len(t)-1]
		dfs(u+1, t)

	}
	var t []int
	dfs(0, t)
	return ans
}
```

### **...**

```

```

<!-- tabs:end -->
