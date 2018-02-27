Build a tree from a postorder array.



The solutions is

for a single node

Input: array\[\], index point to this node, min, max

output: This Node

Logic:

  Base Case:

    1 reaches end which means index &lt; 0, return null

    2 not valid, which means the val of current node is exceed the \(min, max\)

  Process:

    for RightChild, update the min to val

    for LeftChild, update the max to val

  Return

    return the Node which with current val, helper\(left, val, max\) as left child, helper\(right, min, val\) as right child



### Notice

  We should do right child process first then left child.

  Cause it's a post order array, we go from end to start. The last element is the root. Which means part of the front elements besides is root's right children, then the left part is the root's left children. Always, goes like root, right child, left. 

  So we processed right child first then left.





```
const postOrder = [2, 5, 3, 13, 17, 11, 7, 31, 29, 41, 37, 23, 53, 47, 43, 19];

function rebuild(arr) {
    let index = postOrder.length - 1;
    return (function recurse(min, max) {
        // base
        if (index < 0) {
            return null;
        }

        const val = arr[index];

        if (!(min <= val && val <= max)) {
            return null;
        }

        index--;

        return {
            val,
            right: recurse(val, max),
            left: recurse(min, val)
        };
    })(-Infinity, Infinity);
}

```



