# Inorder Traversal

## Definition

Inorder traversal is to traverse the left subtree first. Then visit the root. Finally, traverse the right subtree.

[94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

## Recursive Solution

```c#
public class Solution
{
    private List<int> result = new List<int>();

    private void Recursive(TreeNode node)
    {
        if(node == null) return;
        Recursive(node.left);
        result.Add(node.val);
        Recursive(node.right);
        return;
    }

    // main function
    public IList<int> InorderTraversal(TreeNode root)
    {
        Recursive(root);
        return result;
    }
}

```

## Iterative Solution

```c#
public class Solution
{
    private List<int> result = new List<int>();

    private Stack<TreeNode> stk = new Stack<TreeNode>();

    public IList<int> InorderTraversal(TreeNode root)
    {
        if (root == null) return result;

        TreeNode node = root;

        while (node != null || stk.Count > 0)
        {
            while (node != null)
            {
                stk.Push(node);
                node = node.left;
            }

            node = stk.Pop();
            result.Add(node.val);
            node = node.right;
        }

        return result;
    }
}

```
