---
author: "AJTL"
title: ThreeSum/三数之和
linktitle: "ThreeSum/三数之和"
weight: 10
date: 2019-06-18T10:37:56+08:00
draft: true
tags: [LeetCode,3Sum,C++]
topics: [LeetCode]
description: ""
---

## 题目

给定一个包含*n* 个整数的数组 `nums`，判断 `nums` 中是否存在三个元素*a* ，*b* ，*c* ，使得 *a + b + c = 0* ？找出所有满足条件且不重复的三元组。

注意：答案中不可以包含重复的三元组。

示例:

> 给定数组 nums = [-1, 0, 1, 2, -1, -4]，
>
> 满足要求的三元组集合为：
> [
> [-1, 0, 1],
> [-1, -1, 2]
> ]

## 题目链接

* CH: <https://leetcode-cn.com/problems/3sum/>
* EN: <https://leetcode.com/problems/3sum/>
  
## 解法一

```c++
vector<vector<int>> threeSum(vector<int> &nums)
{
  vector<vector<int>> vResult;
  for (size_t i = 0; i < nums.size()-2; i++)
  {
    for (size_t j = i+1; j < nums.size()-1; j++)
    {
      for (size_t k = j+1; k < nums.size(); k++)
      {
        if (nums[i]+nums[j]+nums[k] = 0)
        {
          vResult.emplace_back(vector<int>{nums[i],nums[j],nums[k]});
        }
      }
    }
  }
  return vResult;
}
```

## 解法二

固定第一个值，在用两个指针在剩余的队伍里查找匹配前值的数值。

```C++
vector<vector<int>> threeSum(vector<int> &nums)
{
        vector<vector<int>> vResult;
        sort(nums.begin(), nums.end());
        if (nums.size() < 3 || nums.front() > 0 || nums.back() < 0)
            return vResult;

        for (size_t i = 0; i < nums.size() - 2; i++)
        {
            if (nums[i] > 0)
                break;
            if (i >= 1 && nums[i] == nums[i - 1])
                continue;
            int r1 = 0 - nums[i];
            int j = i + 1;
            int k = nums.size() - 1;
            while (j < k)
            {
                if (nums[j] + nums[k] < r1)
                {
                    j++;
                    while (nums[j] == nums[j - 1] && j < k)
                        j++;
                }
                else if (nums[j] + nums[k] > r1)
                {
                    k--;
                    while (nums[k] == nums[k + 1] && j < k)
                        k--;
                }
                else
                {
                    vResult.emplace_back(vector<int>{nums[i],nums[j],nums[k]});
                    j++;
                    while (nums[j] == nums[j - 1] && j < k)
                        j++;
                    k--;
                    while (nums[k] == nums[k + 1] && j < k)
                        k--;
                }
            }
        }
        return vResult;
    }
```

## 总结

双指针 可以扩展到多数之和，并且多指针的使用 应该在这个题库中会经常用到。
