# [885. 螺旋矩阵 III](https://leetcode.cn/problems/spiral-matrix-iii)

[English Version](/solution/0800-0899/0885.Spiral%20Matrix%20III/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->

<p>在&nbsp;<code>R</code>&nbsp;行&nbsp;<code>C</code>&nbsp;列的矩阵上，我们从&nbsp;<code>(r0, c0)</code>&nbsp;面朝东面开始</p>

<p>这里，网格的西北角位于第一行第一列，网格的东南角位于最后一行最后一列。</p>

<p>现在，我们以顺时针按螺旋状行走，访问此网格中的每个位置。</p>

<p>每当我们移动到网格的边界之外时，我们会继续在网格之外行走（但稍后可能会返回到网格边界）。</p>

<p>最终，我们到过网格的所有&nbsp;<code>R * C</code>&nbsp;个空间。</p>

<p>按照访问顺序返回表示网格位置的坐标列表。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>R = 1, C = 4, r0 = 0, c0 = 0
<strong>输出：</strong>[[0,0],[0,1],[0,2],[0,3]]

<img alt="" src="https://fastly.jsdelivr.net/gh/doocs/leetcode@main/solution/0800-0899/0885.Spiral%20Matrix%20III/images/example_1.png" style="height: 99px; width: 174px;">
</pre>

<p>&nbsp;</p>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>R = 5, C = 6, r0 = 1, c0 = 4
<strong>输出：</strong>[[1,4],[1,5],[2,5],[2,4],[2,3],[1,3],[0,3],[0,4],[0,5],[3,5],[3,4],[3,3],[3,2],[2,2],[1,2],[0,2],[4,5],[4,4],[4,3],[4,2],[4,1],[3,1],[2,1],[1,1],[0,1],[4,0],[3,0],[2,0],[1,0],[0,0]]

<img alt="" src="https://fastly.jsdelivr.net/gh/doocs/leetcode@main/solution/0800-0899/0885.Spiral%20Matrix%20III/images/example_2.png" style="height: 142px; width: 202px;">
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ol>
	<li><code>1 &lt;= R &lt;= 100</code></li>
	<li><code>1 &lt;= C &lt;= 100</code></li>
	<li><code>0 &lt;= r0 &lt; R</code></li>
	<li><code>0 &lt;= c0 &lt; C</code></li>
</ol>

## 解法

<!-- 这里可写通用的实现逻辑 -->

<!-- tabs:start -->

### **Python3**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```python
class Solution:
    def spiralMatrixIII(
        self, rows: int, cols: int, rStart: int, cStart: int
    ) -> List[List[int]]:
        ans = [[rStart, cStart]]
        if rows * cols == 1:
            return ans
        k = 1
        while True:
            for dr, dc, dk in [[0, 1, k], [1, 0, k], [0, -1, k + 1], [-1, 0, k + 1]]:
                for _ in range(dk):
                    rStart += dr
                    cStart += dc
                    if 0 <= rStart < rows and 0 <= cStart < cols:
                        ans.append([rStart, cStart])
                        if len(ans) == rows * cols:
                            return ans
            k += 2
```

### **Java**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```java
class Solution {
    public int[][] spiralMatrixIII(int rows, int cols, int rStart, int cStart) {
        int cnt = rows * cols;
        int[][] ans = new int[cnt][2];
        ans[0] = new int[] {rStart, cStart};
        if (cnt == 1) {
            return ans;
        }
        for (int k = 1, idx = 1;; k += 2) {
            int[][] dirs = new int[][] {{0, 1, k}, {1, 0, k}, {0, -1, k + 1}, {-1, 0, k + 1}};
            for (int[] dir : dirs) {
                int r = dir[0], c = dir[1], dk = dir[2];
                while (dk-- > 0) {
                    rStart += r;
                    cStart += c;
                    if (rStart >= 0 && rStart < rows && cStart >= 0 && cStart < cols) {
                        ans[idx++] = new int[] {rStart, cStart};
                        if (idx == cnt) {
                            return ans;
                        }
                    }
                }
            }
        }
    }
}
```

### **C++**

```cpp
class Solution {
public:
    vector<vector<int>> spiralMatrixIII(int rows, int cols, int rStart, int cStart) {
        int cnt = rows * cols;
        vector<vector<int>> ans;
        ans.push_back({rStart, cStart});
        if (cnt == 1) return ans;
        for (int k = 1;; k += 2) {
            vector<vector<int>> dirs = {{0, 1, k}, {1, 0, k}, {0, -1, k + 1}, {-1, 0, k + 1}};
            for (auto& dir : dirs) {
                int r = dir[0], c = dir[1], dk = dir[2];
                while (dk-- > 0) {
                    rStart += r;
                    cStart += c;
                    if (rStart >= 0 && rStart < rows && cStart >= 0 && cStart < cols) {
                        ans.push_back({rStart, cStart});
                        if (ans.size() == cnt) return ans;
                    }
                }
            }
        }
    }
};
```

### **Go**

```go
func spiralMatrixIII(rows int, cols int, rStart int, cStart int) [][]int {
	cnt := rows * cols
	ans := [][]int{[]int{rStart, cStart}}
	if cnt == 1 {
		return ans
	}
	for k := 1; ; k += 2 {
		dirs := [][]int{{0, 1, k}, {1, 0, k}, {0, -1, k + 1}, {-1, 0, k + 1}}
		for _, dir := range dirs {
			r, c, dk := dir[0], dir[1], dir[2]
			for dk > 0 {
				rStart += r
				cStart += c
				if rStart >= 0 && rStart < rows && cStart >= 0 && cStart < cols {
					ans = append(ans, []int{rStart, cStart})
					if len(ans) == cnt {
						return ans
					}
				}
				dk--
			}
		}
	}
}
```

### **...**

```

```

<!-- tabs:end -->
