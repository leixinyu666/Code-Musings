# 242.有效的字母异位词
arr：数组。
数组统计字母数即可，arr[26]
# 349.两个数组的交集
unordered_set:去重的集合。
把nums1放入unordered_set，对于每个nums2中的元素，在unordered_set中寻找有无此元素，有则插入另一个unordered_set——result（为了去重），输出数组形式的result
# 1.两数之和
unordered_map:去重的键值对，<key,value>。
本题中为<值，下标>
对于每个nums中的元素，在unordered_map里寻找auto iter=map.find(target-nums[i]):有则输出两个下标（iter->second和i），无则把此元素加入unordered_map，map[nums[i]]=i
# 454.四数相加2
分两组，AB双for把结果都放入unordered_map，second是出现的次数，CD双for对于每个值找map.find(target-c-d)！=map.end()则count+=map[target-c-d]
# 15.三数之和
双指针，先排序，定一个i遍历，left=i+1和right=nums.size()-1，大于则right--，小于则left++，等于则输出right--left++
注意去重：对于i，向前看i-1去重；对于left和right向中间看left+1和right-1去重
# 18.四数之和
同三数，多个for
