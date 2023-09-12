# Inorder Traversal

## Definition

Inorder traversal is to traverse the left subtree first. Then visit the root. Finally, traverse the right subtree.


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

