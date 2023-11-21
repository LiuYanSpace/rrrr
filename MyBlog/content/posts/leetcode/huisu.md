---
title: "39.组合总和"
date: 2023-11-09T18:27:43+08:00
lastmod: 2023-11-09T18:27:43+08:00
author: ["Yan Yan"]
categories:
- 分类1
- 分类2
tags:
- 回溯
- 组合 
summary: ""
description: ""
# weight:  # 如果不需要使用 weight 字段，可以将它删除或注释掉
slug: ""
draft: false
comments: true
showToc: true
TocOpen: true
hidemeta: false
disableShare: true
showbreadcrumbs: true
cover:
image: ""
caption: ""
alt: ""
relative: false
---
一、给定一个无重复元素的数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。candidates 中的数字可以无限制重复被选取。
说明：

所有数字（包括 target）都是正整数。
解集不能包含重复的组合。

示例 1：

输入：candidates = [2,3,6,7], target = 7,
所求解集为： [ [7], [2,2,3] ]

示例 2：

输入：candidates = [2,3,5], target = 8,
所求解集为： [ [2,2,2,2], [2,3,3], [3,5] ]
```
class Solution {
List<List<Integer>> res = new LinkedList<>();

public List<List<Integer>> combinationSum(int[] candidates, int target) {
        if (candidates.length == 0) {
            return res;
        }
        backtrack(candidates, 0, target, 0);
        return res;
    }

// 记录回溯的路径
    LinkedList<Integer> track = new LinkedList<>();

// 回溯算法主函数
    void backtrack(int[] candidates, int start, int target, int sum) {
        if (sum == target) {
            // 找到目标和
            res.add(new LinkedList<>(track));
            return;
        }

        if (sum > target) {
// 超过目标和，直接结束
            return;
        }

// 回溯算法框架
        for (int i = start; i < candidates.length; i++) {
            // 选择 candidates[i]
            track.add(candidates[i]);
            sum += candidates[i];
            // 递归遍历下一层回溯树
            backtrack(candidates, i, target, sum);
            // 撤销选择 candidates[i]
            sum -= candidates[i];
            track.removeLast();
        }
    }
}
```
这段代码是一个Java实现的回溯算法，用于找到给定整数数组 candidates 中的组合，使得这些组合的元素之和等于给定的目标整数 target。代码中使用了递归和回溯的方法来实现这个目标。
具体来说，代码的主要结构如下：

定义了一个类 Solution，其中包含了一个成员变量 res，它是一个列表，用于存储找到的符合条件的组合列表。

combinationSum 方法是入口方法，接受两个参数：candidates 数组和 target 目标值。首先检查如果 candidates 为空，直接返回空的结果列表 res。否则，调用 backtrack 方法来进行回溯搜索。

backtrack 方法是回溯算法的主要函数。它接受四个参数：candidates 数组，当前搜索的起始位置 start，目标值 target，以及当前累计的和 sum。在这个方法中，通过不断选择和撤销选择数组中的元素，以满足和等于目标值的条件。具体过程如下：

如果 sum 等于 target，表示找到了一个符合条件的组合，将这个组合添加到 res 中。

如果 sum 大于 target，表示累计的和超过了目标值，直接返回，不再继续搜索。

否则，使用一个循环遍历 candidates 数组，从当前位置 start 开始。在循环中，依次选择 candidates 中的元素，更新 sum 和 track，然后递归调用 backtrack 方法继续搜索下一层的可能性。

每次递归结束后，要撤销选择，即将当前选择的元素从 track 中移除，同时减去对 sum 的累加。

这种方法通过不断选择和撤销选择，逐渐构建出符合条件的组合，最终得到所有满足条件的组合列表，存储在 res 中，并返回给调用者。这是一种典型的回溯算法的实现方式，用于解决组合类的问题。
让我们逐行解读给出的代码：
```
List<List<Integer>> res = new LinkedList<>(); 
```
- 创建一个列表 res，用于存储最终的组合结果，这里使用了泛型，表示它是一个包含整数列表的列表。

```
public List<List<Integer>> combinationSum(int[] candidates, int target) 
```
 - 定义了一个公有方法 combinationSum，接受两参数 candidates 和 target，表示要在 candidates 数组中查找和为 target 的组合。

```
if (candidates.length == 0) { return res; } 
```
- 如果 candidates 数组为空，直接返回空的结果列表 res。

```
backtrack(candidates, 0, target, 0); 
```
- 否则，调用 backtrack 方法开始回溯搜索，起始位置为 0，目标值为 target，当前累计和为 0。

```
LinkedList<Integer> track = new LinkedList<>(); 
```
- 创建一个整数链表 track，用于记录回溯的路径，即当前正在考虑的组合。

```
void backtrack(int[] candidates, int start, int target, int sum) { 
```
- 定义了一个回溯算法的主要函数 backtrack，接受四个参数：candidates 数组，当前搜索的起始位置 start，目标值 target，以及当前累计的和 sum。

```
if (sum == target) { res.add(new LinkedList<>(track)); return; } 
```
- 如果当前累计和 sum 等于目标值 target，表示找到了一个符合条件的组合，将当前 track 中的元素复制一份并添加到 res 中，然后返回，结束本次搜索。

```
if (sum > target) { return; } 
```
- 如果当前累计和 sum 超过了目标值 target，直接返回，不再继续搜索，因为这条路径无法得到符合条件的组合。


接下来是回溯算法的核心部分，在循环中遍历 candidates 数组，从当前位置 start 开始。

```
track.add(candidates[i]); 
```
- 选择当前循环中的元素 candidates[i]，将其添加到 track 中，表示当前正在考虑这个元素。

```
sum += candidates[i]; 
```
- 更新累计和 sum，将当前选择的元素的值累加到 sum 上。

```
backtrack(candidates, i, target, sum); 
```
- 递归调用 backtrack 方法，继续搜索下一层的可能性，传入参数为 candidates 数组，起始位置 i，目标值 target，和累计和 sum。

```
sum -= candidates[i];
``` 
- 递归返回后，撤销选择，即从 sum 中减去当前选择的元素的值。

```
track.removeLast(); 
```
- 同样，从 track 中移除最后一个元素，表示当前不再考虑这个元素。


这样，代码通过不断选择和撤销选择，递归搜索所有可能的组合，找到和为 target 的组合并存储在 res 中。最终，res 包含了所有满足条件的组合。
三、
输入: candidates = [2,3,5], target = 8。
对于输入 candidates = [2,3,5] 和 target = 8，让我们看看以上代码如何运行：


combinationSum 方法被调用，传入 candidates 数组 [2, 3, 5] 和 target 值 8。


首先检查 candidates 数组不为空，所以继续执行。


backtrack 方法被调用，起始位置 start 为 0，目标值 target 为 8，当前累计和 sum 为 0。


在 backtrack 方法内部：

回溯搜索开始。
开始循环，首先选择 candidates[0]，即 2。
track 变为 [2]，sum 更新为 2。
递归调用 backtrack，传入 candidates 数组，起始位置 0，目标值 8，累计和 2。



在递归调用内部：

继续回溯搜索，开始循环。
选择 candidates[0]，即 2。
track 变为 [2, 2]，sum 更新为 4。
递归调用 backtrack，传入 candidates 数组，起始位置 0，目标值 8，累计和 4。



在递归调用内部：
继续回溯搜索，开始循环。
选择 candidates[0]，即 2。
track 变为 [2, 2, 2]，sum 更新为 6。
递归调用 backtrack，传入 candidates 数组，起始位置 0，目标值 8，累计和 6。

在递归调用内部：
继续回溯搜索，开始循环。
选择 candidates[0]，即 2。
track 变为 [2, 2, 2, 2]，sum 更新为 8。
此时 sum 等于 target，所以找到一个符合条件的组合 [2, 2, 2, 2]，将其添加到结果列表 res。

返回上一层递归，继续循环，选择下一个元素 candidates[1]，即 3。

track 变为 [2, 2, 2, 3]，sum 更新为 11。

由于 sum 大于 target，直接返回，不再继续搜索这个分支。

返回上一层递归，继续循环，选择下一个元素 candidates[2]，即 5。

track 变为 [2, 2, 2, 5]，sum 更新为 13。

由于 sum 大于 target，直接返回，不再继续搜索这个分支。

返回上一层递归，继续循环，选择下一个元素 candidates[1]，即 3。

track 变为 [2, 2, 3]，sum 更新为 6。

递归搜索下一层，类似上述过程。

最终，所有的搜索完成后，res 中包含了所有满足条件的组合。

结果 res 包含以下组合：

[2, 2, 2, 2]
[2, 3, 3]
[3, 5]
