# 344.反转字符串
库函数reverse(s.begin(),s.end())
# 541.反转字符串2
for循环每次加2k

里面reverse(s.begin()+i,s.begin()+k+i)

再对最后的部分反转
# 151.反转字符串里的单词
## 去冗余的空格
双指针法，先去最前面的空格，在去单词间的连续空格，最后讨论最后面的空格，用resize(slow)操作
## 整体反转
reverse()
## 单词反转
双指针法，最后的情况单独反转
# 28.KMP
理解next数组，用s.find(t)即可
# 459.重复的子字符串
若是重复的子字符串，则两个拼到一起，掐头去尾，里面还能找到这个子字符串

用erase()删除字符，用find()查找
