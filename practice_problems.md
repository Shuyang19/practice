target number: find the sum of two numbers in a num list is the target number:
1. Using two for loop: O($N^2$)
2. Using hash table: O(1):
```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> hashtable;
        for (int i = 0; i < nums.size(); ++i) {
            auto it = hashtable.find(target - nums[i]);
            if (it != hashtable.end()) {
                return {it->second, i};
            }
            hashtable[nums[i]] = i;
        }
        return {};
    }
};
```
[LeeCode](https://leetcode.cn/problems/two-sum/solutions/434597/liang-shu-zhi-he-by-leetcode-solution/)



## Greedy Algorithm:

给定一个长度为 `n` 的 `0` 索引整数数组 `nums`。初始位置为 `nums[0]`。

每个元素 `nums[i]` 表示从索引 `i` 向前跳转的最大长度。换句话说，如果你在 `nums[i]` 处，你可以跳转到任意 `nums[i + j]` 处:

`0 <= j <= nums[i]` 
`i + j < n`
返回到达 `nums[n - 1]` 的最小跳跃次数。生成的测试用例可以到达 `nums[n - 1`]。

```
class Solution {
public:
    int jump(vector<int>& nums) {
        int steps = 0;
        int start = 0;
        int end = 1;
        while(end < nums.size())
        {
            int maxPos = 0;
            for(int i = start; i < end; i++)
            {
                maxPos = std::max(maxPos, i + nums[i]);
            }
            start = end;//下次起跳起始点
            end = maxPos+1;//下次起跳能达到的最远距离
            steps++;
        }
        return steps;

    }
};
```
思路：[LeeCode](https://leetcode.cn/problems/jump-game-ii/solutions/36035/45-by-ikaruga)


优化：
```
int jump(vector<int>& nums)
{
    int ans = 0;
    int end = 0;
    int maxPos = 0;
    for (int i = 0; i < nums.size() - 1; i++)
    {
        maxPos = max(nums[i] + i, maxPos);
        if (i == end)
        {
            end = maxPos;
            ans++;
        }
    }
    return ans;
}

作者：Ikaruga
链接：https://leetcode.cn/problems/jump-game-ii/solutions/36035/45-by-ikaruga/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

```
