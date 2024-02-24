

``` python
class Node:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

def tree_height(root):
    if not root:
        return 0
    left_height = tree_height(root.left)
    right_height = tree_height(root.right)
    return max(left_height, right_height) + 1

# Example usage:
# Constructing a binary tree
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)
root.right.left = Node(6)
root.right.right = Node(7)

print("Height of the binary tree:", tree_height(root))

```


