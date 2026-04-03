# LeetCode 单维动态规划 (1D DP)

单维动态规划通常可以转化成递归解法，但递归在大规模输入下会消耗大量时间和空间，因此推荐使用 DP。

---

## 动态规划基本步骤

1. **初始化**  
   创建一个列表（数组）保存历史状态信息。

2. **设置初始条件**  
   例如长度为 1 或 2 的情况。

3. **设计状态转移条件**  
   - 两个元素不相邻的约束  
   - 只考虑完全平方数等特殊条件  

4. **计算 DP 值**  
   使用 `min` 或 `max` 函数更新状态。

---

## 示例：单词拆分（LeetCode 139）

**题目描述**：

给定一个字符串 `s` 和一个字符串列表 `wordDict`，判断 `s` 是否可以由字典中的单词拼接而成。

**注意事项**：

- 字典中的单词可以重复使用  
- 不要求字典中出现的所有单词都必须使用  

---

### 示例 1

```text
输入: s = "leetcode", wordDict = ["leet", "code"]
输出: true
解释: "leetcode" 可以由 "leet" 和 "code" 拼接成

class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        wordSet = set(wordDict)  # 转集合加速查找
        dp = [False] * (len(s) + 1)
        dp[0] = True  # 空字符串可以拆分
        
        for i in range(1, len(s)+1):
            for j in range(i):
                if dp[j] and s[j:i] in wordSet:
                    dp[i] = True
                    break
        
        return dp[len(s)]
