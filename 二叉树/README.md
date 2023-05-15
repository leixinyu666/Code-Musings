# 144.94.145 二叉树的前序中序后序遍历
op函数的数组参数以引用方式传递
# 102.二叉树的层序遍历
队列，出队再将其孩子入队，注意从开始1个的时候就记录s=qu.size()，用for记录每轮出多少
# 226.翻转二叉树
先交换左右，再递归翻左孩子和右孩子
# 101.对称二叉树
compare函数（2个点左右），判这2个空不空3种，判这2个等不等1种，递归判断左的左孩子compare右的右孩子，递归判断左的右孩子compare右的左孩子
# 104.二叉树的最大深度
op函数return max(op(左)，op(右))+1
# 111.二叉树的最小深度
和最大深度不同，要讨论左右空不空

都不空的时候再return min(op(左)，op(右))+1

有空的时候return 有值的一方+1
# 110.平衡二叉树
op函数对最大深度的op修改，-1代表不平衡，若左和右有-1则自己-1，若左右差值大于1则自己-1，若NULL则0，若其他则max(op(左)，op(右))+1
# 257.二叉树的所有路径
void op(TreeNode* root,string path,vector<string>& result)

op函数递归遇到非空节点后，path挂to_string(val),若是树叶则把path给push_back到result，若不是树叶，则把path挂上->再递归到两个子节点
# 112.路径总和
bool op(TreeNode* root,int sum,int targetSum)

op函数递归遇到非空节点后，sum+=val,若是树叶则判断相等true不等false，若不是树叶，则把sum递归到两个子节点，返回两者的并

op函数遇到空节点后返回false
# 113.路径总和2
void op(TreeNode* root,vector<int> arr,int sum,int targetSum,vector<vector<int>>& result)

op函数递归遇到非空节点后，sum+=val,val加入arr,若是树叶则判断相等则把arr加入resukt，不等则return，若不是树叶，则递归到两个子节点
