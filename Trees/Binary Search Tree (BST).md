| **Access** | **Search** | **Insertion** | **Deletion** | **Space** |
| ---------- | ---------- | ------------- | :----------: | --------- |
| O(log(n))  | O(log(n))  | O(log(n))     |  O(log(n))   | O(n)      |

## TreeNode or Node Stub in CSharp

```csharp
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
```

# Recursion

* Most BST methods can be done recursively.
1. Check a base case
2. (Optional) Do some calculation
3. Recursive case(s). Usually operating on both the left and right subtree.
4. (Optional) Do some calculation
5. Return a base value or the calculated result

### Invert Tree (Flip around Root)

Base case
```csharp
public TreeNode InvertTree(TreeNode root)
{
        if (root == null)
            return null;

        TreeNode tmp = root.left;
        root.left = root.right;
        root.right = tmp;

        InvertTree(root.left);
        InvertTree(root.right);
        return root;
}
```

## Maximum Depth (using Recursion)

```csharp
    public int MaxDepth(TreeNode root) {
          if(root == null)
          {
              return 0;
          }
          int ldepth = MaxDepth(root.left);
          int rdepth = MaxDepth(root.right);
          if (ldepth > rdepth)
              return (ldepth + 1);
          else
              return (rdepth + 1);
    }
```

## Is Same Tree (Recursion)

```csharp
    public bool IsSameTree(TreeNode p, TreeNode q) {
        if(p == null && q == null)
        {
            return true;
        }
        else if (p != null && q != null)
        {
            return (p.val == q.val && IsSameTree(p.left, q.left) && IsSameTree(p.right, q.right));
        }
        return false;
    }
```

## Subtree of another Tree
```

```