# 3.N叉树的层序遍历

>题目描述：给定一个 N 叉树，返回其节点值的层序遍历。 (即从左到右，逐层遍历)。



![示例](images\N叉树_3.png)
## 说明:
+ 树的深度不会超过 1000。
+ 树的节点总数不会超过 5000。

## 代码（c++版本）

```c++
/*
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> children;

    Node() {}

    Node(int _val) {
        val = _val;
    }

    Node(int _val, vector<Node*> _children) {
        val = _val;
        children = _children;
    }
};
*/
//两个队列求解
class Solution {
public:
    vector<vector<int>> levelOrder(Node* root) {
        vector<vector<int>> ret;
        vector<int> temp_ret;
        if(root == NULL)
        {
            return ret;
        }
        queue<Node*> q1;
        queue<Node*> q2;
        Node* temp;
        q1.push(root);
        while(!q1.empty() || !q2.empty())
        {
            temp_ret.clear();
            while(!q1.empty())
            {
                temp = q1.front();
                temp_ret.push_back(temp->val);
                q1.pop();
                int len = temp->children.size();
                for(int i=0;i<len;i++)
                {
                    q2.push(temp->children[i]);
                }
                
            }
            if(temp_ret.size() != 0)
            {
                ret.push_back(temp_ret);
            }
            
            temp_ret.clear();
            while(!q2.empty())
            {
                temp = q2.front();
                temp_ret.push_back(temp->val);
                q2.pop();
                int len = temp->children.size();
                for(int i=0;i<len;i++)
                {
                    q1.push(temp->children[i]);
                }
                
            }
            if(temp_ret.size() != 0)
            {
                ret.push_back(temp_ret);
            }
            
        }
        
        return ret;
    }
};
```
