## 代码随想录day37

## ● 738.单调递增的数字 

```c++
class Solution {
public:
    int monotoneIncreasingDigits(int n) {
        string strNum = to_string(n);
        //flag 用来标记赋值9从哪里开始
        //设置为这个默认值，为了防止第二个for循环循环在flag没有赋值的情况下执行
        //332 -> 329 -> 299
        int flag = strNum.size();
        for(int i = strNum.size() - 1; i > 0;i--){
            if(strNum[i - 1] > strNum[i]){
                flag = i;
                strNum[i - 1] --;
            }
        }
        for(int i = flag; i<strNum.size();i++){
            strNum[i] = '9';
        }
        return stoi(strNum);
    }
};
```



## ● 968.监控二叉树 

```c++
class Solution {
// 0:未覆盖 1：有摄像头 2：有覆盖
// 我们使用后序遍历，在叶子节点的父节点按摄像头
// left == 0 || right == 0 指的是如果左右孩子没有覆盖，则return 1 ，覆盖摄像头且result++
// right == 2 && left == 2 说明左右孩子有覆盖，此时父节点没有覆盖
// 其他情况为有覆盖 情况
// 空节点设置为2，可以保证不在叶子节点按摄像头
// if(traversal(root) == 0) 判断根节点是否覆盖，没覆盖需要加摄像头
private:
    int result = 0;
    int traversal(TreeNode* cur){
        if(cur == nullptr) return 2;
        int left = traversal(cur->left);
        int right = traversal(cur->right);
        if(left == 2 && right == 2) return 0;
        else if(left == 0 || right == 0){
            result++;
            return 1;
        }else return 2;
    }
public:
    int minCameraCover(TreeNode* root) {
        if(traversal(root) == 0){
            result++;
        } 
        return result;
    }
};
```

