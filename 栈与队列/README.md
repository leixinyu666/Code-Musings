# 232.用栈实现队列
一个s2用来push，一个s1用来pop。

s1的如果空了就把s2的出栈到s1中
# 225.用队列实现栈
一个是主队列q1，一个是辅助队列q2。

q1要出栈就把前s-1个出队到q2，出最后元素，再把q2出队到q1
# 20.有效的括号
[{(:压栈

]}):弹栈
# 150.后缀表达式求值
数字压栈，符号弹栈，down op up

注意：将字符串转数字的函数是stoi()
# 239.滑动窗口最大值
单调队列，双端

push的元素比队尾元素大，则把队尾元素删掉直到遇到比他更大或者相等的再入队

pop的元素如果等于对头元素，则把队头元素删掉

注意：vector如果不事先声明大小不能直接用arr[i]=x索引，只能arr.push_back(x)
# 347.k个高频元素
# 42.接雨水
重点：sum+=min(leftmaxheight[i],rightmaxheight[i])-height[i];

求leftmaxheight和rightmaxheight（除开两个端点）：

leftmaxheight[i]=max(height[i],leftmaxheight[i-1]);

rightmaxheight[i]=max(height[i],rightmaxheight[i+1]);
