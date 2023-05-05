Download Link: https://assignmentchef.com/product/solved-ds-lab7-avl-tree
<br>
In the previous lab, we learned how to build up a BST. And in this tutorial, we continue to extend Binary Search Tree to the Balanced Binary Search Tree, one of them called AVL Tree.

<ol>

 <li><strong> What is AVL Tree?</strong></li>

</ol>

AVL is the abbreviation of the Russian authors Adelson-Velskii and Landis (1962) who defined the balanced tree.

An AVL tree is the same as a binary search tree, except that for every node, the height of the left and right subtrees can differ only by 1 (and an empty tree has a height of -1)<sup>1</sup>. This difference is called Balance Factor. When the Balance Factor &gt; 1, the tree will be rebalanced.

Figure 1: AVL tree

<h1>2.      Node of a AVL tree</h1>

In this lab, we add one more attribute which is called <em>height </em>to the Node class (same with BST). This attribute will help us access the height of the node faster.

<sup>1</sup>https://web.stanford.edu/class/archive/cs/cs106b/cs106b.1176/lectures/20-BinarySearchTrees/20BinarySearchTrees.pptx                                                                                                            <strong>1</strong>

<table width="529">

 <tbody>

  <tr>

   <td width="529">public class Node{ Integer key; Node left,right; int height;public Node(Integer key){ this.key = key; this.height = 0;this.left = this.right = null;}}</td>

  </tr>

 </tbody>

</table>

1

2

3

4

5

6

7

8

9

10

11

In AVL class:

<table width="529">

 <tbody>

  <tr>

   <td width="529">public int height(Node node){ if (node == null) return -1;return node.height; }</td>

  </tr>

 </tbody>

</table>

1

2

3

4

5

<h1>3.      Check balance factor</h1>

A Balance Factor of a AVL tree is defined by the height difference of the left subtree and the right subtree.

<table width="529">

 <tbody>

  <tr>

   <td width="529">private int checkBalance(Node x) { return height(x.left) – height(x.right); }</td>

  </tr>

 </tbody>

</table>

1

2

3

<h1>4.      Rotation</h1>

The insert or delete operation may make the AVL tree come to imbalance. A simple modification of the tree, called <strong>rotation</strong>, can restore the AVL property. We have 4 types of rotation corresponding to 4 violation cases that make the tree imbalance.

<h2>4.1.      Left rotation</h2>

When a new node is inserted into a AVL tree and makes it a right-right-unbalancedtree. The tree can be re-balanced using left rotation as following:

Figure 2: Left rotation

This is the code of left rotation:

<table width="529">

 <tbody>

  <tr>

   <td width="529">private Node rotateLeft(Node x) {Node y = x.right; x.right = y.left;y.left = x;x.height = 1 + Math.max(height(x.left), height(x.right));y.height = 1 + Math.max(height(y.left), height(y.right)); return y;}</td>

  </tr>

 </tbody>

</table>

1

2

3

4

5

6

7

8

<h2>4.2.      Right rotation</h2>

When a new node is inserted into a AVL tree and make it a left-left-unbalanced-tree. The tree can be re-balanced using right rotation as following:

Figure 3: Right rotation

<table width="529">

 <tbody>

  <tr>

   <td width="529">private Node rotateRight(Node x) {//your turn }</td>

  </tr>

 </tbody>

</table>

1

2

3

<h2>4.3.      Left-Right rotation</h2>

When a new node is inserted into a AVL tree and make it a left-right-unbalancedtree. The tree can be re-balanced using left-right rotation.

Figure 4: Left-Right rotation

First, we perform a <strong>left rotation </strong>on node A (the left subtree of C).

Figure 5: Left-Right rotation

This makes A come to the left subtree of B. And B replaces A to become the left subtree of C.

Figure 6: Left-Right rotation

Now, node C is remaining unbalanced but it has become case left-left-unbalancedtree and <strong>right rotation </strong>can be used to balance the tree.

<h2>4.4.      Right-Left rotation</h2>

When a new node is inserted into a AVL tree and make it a right-left-unbalancedtree. The tree can be re-balanced using right-left rotation.

Figure 7: Right-Left rotation

First, we perform a <strong>right rotation </strong>on node C (the left subtree of A).

Figure 8: Right-Left rotation

This makes C come to the right subtree of B. And B replaces C to become the right subtree of A.

Figure 9: Right-Left rotation

Now, node A is remaining unbalanced but it has become case right-right-unbalancedtree and <strong>left rotation </strong>can be used to balance the tree.

<h1>5.      Balance</h1>

This is the code to re-balance the tree:

<table width="529">

 <tbody>

  <tr>

   <td width="529">private Node balance(Node x) { if (checkBalance(x) &lt; -1) { if (checkBalance(x.right) &gt; 0) {x.right = rotateRight(x.right); }x = rotateLeft(x);}else if (checkBalance(x) &gt; 1) { if (checkBalance(x.left) &lt; 0) {x.left = rotateLeft(x.left); }x = rotateRight(x);} return x;}</td>

  </tr>

 </tbody>

</table>

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

<ol start="6">

 <li><strong> Exercise</strong></li>

</ol>

<h1>Exercise 1</h1>

Complete the class to build the AVL tree. You can re-use the BST code in the previous lab (insertion, deletion).

THE END