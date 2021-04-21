---
author: "AJTL"
title: TwoSum/两数之和
linktitle: "TwoSum/两数之和"
weight: 10
date: 2019-06-17T11:08:34+08:00
draft: true
tags: [LeetCode,TwoSum,C++]
topics: [LeetCode]
description: ""
---

## 题目

给定一个整数数组 `nums` 和一个目标值 `target`，请你在该数组中找出和为目标值的那 **两个** 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

示例:

> 给定 nums = [2, 7, 11, 15], target = 9
>
> 因为 nums[0] + nums[1] = 2 + 7 = 9
> 所以返回 [0, 1]

## 题目链接

* CH: <https://leetcode-cn.com/problems/two-sum/>
* EN: <https://leetcode.com/problems/two-sum/>
  
## 解法一

双重循环，时间复杂度是O(n^2)

```C++
    vector<int> twoSum(vector<int> &nums, int target)
    {
        vector<int> vRes;
        for (size_t i = 0; i < nums.size() - 1; i++)
        {
            for (size_t j = i + 1; j < nums.size(); j++)
            {
                if (nums[i] + nums[j] == target)
                {
                    vRes.emplace_back(i);
                    vRes.emplace_back(j);
                    break;
                }
            }
        }
        return vRes;
    }
```

## 解法二

使用`map`将数值及其的位置存储起来，再去遍历元数组，每遍历一次就去map查找匹配值是否存在。注意判断相同值。时间复杂度是O(n)

```c++
    vector<int> twoSum(vector<int> &nums, int target)
    {
        vector<int> vRes;
        map<int, int> mNums;
        for (size_t i = 0; i < nums.size(); i++)
        {
            mNums.try_emplace(nums[i], i);
        }

        auto it = nums.begin();
        while (it != nums.end())
        {
            int temp = target - *it;
            if (mNums.count(temp) && mNums[temp] != (it - nums.begin()))
            {
                vRes.emplace_back(it - nums.begin());
                vRes.emplace_back(mNums[temp]);
                break;
            }
            it++;
        }
        return vRes;
    }
```

## 总结

LeetCode 第一题 ，难度easy，固定思维比较常引向第一种解法。

在解法二中使用到了[`map`](https://en.cppreference.com/w/cpp/container/map/)中的[`count()`](https://en.cppreference.com/w/cpp/container/map/count)方法,你也可以使用[`contains()`](https://en.cppreference.com/w/cpp/container/map/contains)方法。一般如果对`map`或者是对这两种方法不熟悉，那也有可能想不到第二种解法。

## 引申

在很多解答中，都使用了[`unordered_map`](https://en.cppreference.com/w/cpp/container/unordered_map)~~，在做少量的测试用例之后，本题情况下无太大差别~~。

这里列出一些两者的特点。

|          map           |             unordered_map              |
| :--------------------: | :------------------------------------: |
|          有序          |                  无序                  |
|  内部实现了一个红黑树  |          内部实现了一个哈希表          |
|      空间占用率高      |        哈希表的建立比较消耗时间        |
| 适用于有顺序要求的问题 |             适用于查找问题             |
| **需要重载operator<**  | **需要自定义Hash函数并重载operator==** |
