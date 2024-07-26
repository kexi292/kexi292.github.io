二分查找 确定查找区间

> 初始化`right`的时候是`nums.length`。nums.length是越界的，因此查找区间是`[left,rignt)`。当初始化`right`的时候是`nums.length - 1`。查找区间就是`[left,rignt]`。

两种二分算法的区别：
1. `[left,right]` 
循环结束判断使用` left <= right ` ,因为 `[2,2]` `有意义，查找空间不为空。`[left + 1, left] `查找空间才是空的。
`if (nums[middle] > target )`的时候，`right`需要更新为`middle - 1` ，查找空间更新为`[left,middle - 1]`。
3. `[left,right)`
循环结束判断使用` left < right` ，因为`[2,2)` 没有意义，查找空间已经是空的。
`if (nums[middle] > target ) `的时候，`right` 需要更新为 `middle` ,查找空间更新为`[left,middle)` ，因为middle是不在搜索区间里的。

扩展：
1）查找左侧边界：查找的数组中有重复数字，查找最左边的数字。
做法：使用左闭右闭的搜索空间,在查找到值的时候，压缩右侧的搜索空间。
`if (nums[middle] == target )` 的时候，`right = middle - 1` 。
返回的时候，返回的是left。
2）查找右侧边界：查找的数组中有重复数字，查找最右侧的数字。
做法：压缩左侧的搜索空间。
当使用左闭右闭的搜索空间的时候，在查找到值的时候。`if ((nums[middle] == target) ` ,`left = middle + 1` .
返回的时候，返回的是right。


参考链接1：[labuladong](https://labuladong.online/algo/essential-technique/binary-search-framework/)
参考链接2：[代码随想录](https://programmercarl.com/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.html#%E6%80%9D%E8%B7%AF)