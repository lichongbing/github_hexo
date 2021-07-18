title: AVL树
categories:
  - 数据结构
date: 2021-04-26 13:40:36
---
AVL树本质上是一棵自平衡的二叉排序树。
<!--more-->
AVL树具有以下特点：

（1）AVL树是一棵空树或它的左右两棵子树的高度差的绝对值不超过1。

（2）AVL树每个结点的左右两棵子树都是一棵平衡二叉树。

平衡二叉树和非平衡二叉树对比如图2-49所示。

￼![IMG_2870](https://image.lichongbing.com/IMG_2870.JPG)

图2-49　平衡二叉树和非平衡二叉树对比示意图

AVL树中有一个重要的概念叫作平衡因子。平衡因子指左子树与右子树高度差的绝对值。计算公式如下：

平衡因子=|左子树高度-右子树高度|

AVL树的平衡因子的取值范围是：-1≤平衡因子≤1。

普通的二叉排序树在一些极端的情况下可能会退化成链式结构，例如图2-50所示的结点1～5组成的二叉排序树。
![IMG_2871](https://image.lichongbing.com/IMG_2871.JPG)
图2-50　退化成链式结构的二叉排序树示意图
当二叉排序树退化成为链表时，此时访问其中的元素的时间复杂度从O(log2n)退化为O(n)。即便是在构建二叉排序树时尽量避免如图2-50所示的情况，但是随着在使用过程中不断地对二叉排序树进行添加和删除操作，还是会造成二叉排序树向左倾斜或者向右倾斜，造成二叉排序树的平衡性被破坏。

1．AVL树的基本操作

AVL树的插入和删除可能会破坏AVL树的平衡性。在插入或删除元素后，从变更的结点开始向根结点回溯，遇到的第一个不平衡的结点称为“最低失衡根结点”。从最低失衡根结点向下分析，不平衡的情况可以分为4种情况：

（1）导致失衡的结点出现在最低失衡根结点的左子树的左子树中。

（2）导致失衡的结点出现在最低失衡根结点的左子树的右子树中。

（3）导致失衡的结点出现在最低失衡根结点的右子树的右子树中。

（4）导致失衡的结点出现在最低失衡根结点的右子树的左子树中。

分析解决不平衡的情况之前，先介绍两种调整AVL树使之平衡的基本操作。

①左旋转

当向AVL树插入元素后，右子树的高度减去左子树的高度大于1，此时发生左旋转，即AVL树向左旋转，如图2-51所示。
￼![IMG_2872](https://image.lichongbing.com/IMG_2872.JPG)

图2-51　左旋转示意图

②右旋转

当向AVL树插入元素后，左子树的高度减去右子树的高度大于1，此时发生右旋转，即AVL树向右旋转，如图2-52所示。

￼![IMG_2873](https://image.lichongbing.com/IMG_2873.JPG)

图2-52　右旋转示意图

下面分别对各种不平衡的情况进行分析。

（1）LL情况旋转

LL（Left-Left）旋转即导致失衡的结点出现在最低失衡根结点的左子树的左子树中而发生结点旋转的情况。旋转方式是找到最低失衡根结点，将最低失衡根结点右旋转，如图2-53所示。

![IMG_2874](https://image.lichongbing.com/IMG_2874.JPG)

图2-53　导致失衡的结点出现在最低失衡根结点的左子树的左子树中示意图

如图2-53所示，最低失衡根结点是结点5，失衡是因为结点1的存在，而结点1位于结点5左子树的左子树中，需要一次右旋转即可达到平衡。具体的方法是：LL旋转的对象是最低失衡根结点（结点5），找到结点5的左孩子（结点3），将结点3的右孩子结点4变成结点5的左孩子，最后将结点5变成结点3的右孩子，调整后的AVL树如图2-54所示。

￼![IMG_2875](https://image.lichongbing.com/IMG_2875.JPG)

图2-54　LL情况旋转示意图

（2）LR情况旋转

LR（Left-Right）旋转即导致失衡的结点出现在最低失衡根结点的左子树的右子树中而发生旋转的情况。旋转方式是找到最低失衡根结点，先对最低失衡根结点的左孩子进行左旋转，然后对最低失衡根结点进行右旋转，如图2-55所示。

￼![IMG_2876](https://image.lichongbing.com/IMG_2876.JPG)

图2-55　导致失衡的结点出现在最低失衡根结点的左子树的右子树中示意图

图2-55的情况的调整过程：首先对最低失衡根结点5的左孩子结点2进行左旋转，然后对最低失衡根结点5进行右旋转。调整过程如图2-56所示。

￼![IMG_2877](https://image.lichongbing.com/IMG_2877.JPG)

图2-56　LR情况旋转示意图

（3）RR情况旋转

RR（Right-Right）旋转即导致失衡的结点出现在最低失衡根结点的右子树的右子树中而发生旋转的情况。旋转方式是找到最低失衡根结点，将最低失衡根结点左旋转，如图2-57所示。

￼![IMG_2878](https://image.lichongbing.com/IMG_2878.JPG)

图2-57　导致失衡的结点出现在最低失衡根结点的右子树的右子树中示意图

如图2-57所示，最低失衡根结点是结点2，失衡是结点6导致的，而结点6位于结点2右子树的右子树，需要一次左旋转即可达到平衡。旋转的对象是最低失衡根结点（结点2），找到结点2的右孩子结点4，将结点4的左孩子结点3变成结点2的右孩子，最后将结点2变成结点4的左孩子，旋转后的结果如图5-58所示。

![IMG_2882](https://image.lichongbing.com/IMG_2882.JPG)

图2-58　RR情况旋转示意图
（4）RL情况旋转

RL（Right-Left）旋转即导致失衡的结点出现在最低失衡根结点的右子树的左子树中而发生旋转的情况。旋转方式是找到最低失衡根结点，先对最低失衡根结点的右孩子进行右旋转，然后对最低失衡根结点进行左旋转，如图2-59所示。

￼图2-59　导致失衡的结点出现在最低失衡根结点的右子树的左子树中示意图

2-59的情况的调整过程：首先对最低失衡根结点2的右孩子结点5进行右旋转，然后对最低失衡根结点2进行左旋转。调整过程如图2-60所示。

![IMG_2881](https://image.lichongbing.com/IMG_2881.JPG)

图2-60　RL情况旋转示意图

2．AVL树的实现

AVL树的代码实现如下
```java

/**
 * @Author : zhouguanya
 * @Project : java-interview-guide
 * @Date : 2019-05-05 20:33
 * @Version : V1.0
 * @Description : AVL树实现
 */
public class AvlTree {
    /**
     * 根结点
     */
    private Node root;

    /**
     * 内部类
     */
    public class Node {
        /**
         * 结点元素值
         */
        private int key;
        /**
         * 高度
         */
        private int height;
        /**
         * 左子结点
         */
        private Node left;
        /**
         * 右子结点
         */
        private Node right;
        /**
         * 父结点
         */
        private Node parent;
        /**
         * 内部类构造器
         *
         * @param key       元素值
         * @param left      左子结点
         * @param right     右子结点
         * @param parent    父结点
         */
        Node(int key, Node left, Node right, Node parent) {
            this.key = key;
            this.left = left;
            this.right = right;
            this.height = 0;
            this.parent = parent;
        }
    }

    /**
     * AVL树构造器
     */
    public AvlTree() {

    }

    /**
     * 添加key到AVL树
     *
     * @param key
     */
    public void insert(int key) {
        root = insert(root, key);
        root.parent = null;
    }

    /**
     * 将结点插入到AVL树中，并返回根结点
     *
     * @param root      父结点
     * @param key       元素值
     * @return          插入结果
     */
    private Node insert(Node root, int key) {
        // 创建结点
        if (root == null) {
            root = new Node(key, null, null, null);
        } else if (key < root.key) {
            // 插入左子树
            root.left = insert(root.left, key);
            root.left.parent = root;
            // 二叉树失衡
            if (height(root.left) - height(root.right) == 2) {
                // 进行LL旋转
                if (key < root.left.key) {
                    root = leftLeftRotate(root);
                } else {
                    // 进行LR旋转
                    root = leftRightRotate(root);
                }
            }
        } else if (key > root.key) {
            // 插入右子树
            root.right = insert(root.right, key);
            root.right.parent = root;
            // 二叉树失衡
            if (height(root.right) - height(root.left) == 2) {
                if (key > root.right.key) {
                    // 进行RR旋转
                    root = rightRightRotate(root);
                } else {
                    // 进行RL旋转
                    root = rightLeftRotate(root);
                }
            }
        }
        root.height = max(height(root.left), height(root.right)) + 1;
        return root;
    }

    /**
     * LL旋转(右旋转)
     *
     * @param root    失衡AVL树根结点
     * @return        调整后的AVL树根结点
     */
    private Node leftLeftRotate(Node root) {
        // 失衡AVL树根结点的左子结点——也是调整后的AVL树的根结点
        Node leftChild = root.left;
        // 失衡AVL树根结点的左子结点 = 失衡AVL树根结点的左子结点的右子结点
        root.left = leftChild.right;
        if (root.left != null) {
            root.left.parent = root;
        }
        // 失衡AVL树根结点的左子结点的右结点 = 原AVL树的根结点
        leftChild.right = root;
        leftChild.right.parent = leftChild;
        // 调整leftChild的高度 = max(左子树的高度，右子树的高度) + 1
        leftChild.height = max(height(leftChild.left), height(leftChild.right)) + 1;
        // 调整root的高度 = max(左子树的高度，右子树的高度) + 1
        root.height = max(height(root.left), height(root.right)) + 1;
        return leftChild;
    }

    /**
     * RR旋转(左旋转)
     *
     * @param root    失衡AVL树根结点
     * @return        调整后的AVL树根结点
     */
    private Node rightRightRotate(Node root) {
        // 失衡AVL树根结点的右子结点——也是调整后的AVL树的根结点
        Node rightChild = root.right;
        // 失衡AVL树根结点的右子结点 = 失衡AVL树根结点的右子结点的左子结点
        root.right = rightChild.left;
        if (root.right != null) {
            root.right.parent = root;
        }
        // 失衡AVL树根结点的右子结点的左结点 = 原AVL树的根结点
        rightChild.left = root;
        rightChild.left.parent = rightChild;
        // 调整leftChild的高度 = max(左子树的高度，右子树的高度) + 1
        rightChild.height = max(height(rightChild.left), height(rightChild.right)) + 1;
        // 调整root的高度 = max(左子树的高度，右子树的高度) + 1
        root.height = max(height(root.left), height(root.right)) + 1;
        return rightChild;
    }

    /**
     * LR旋转(左右旋转)
     *
     * @param root    失衡AVL树根结点
     * @return        调整后的AVL树根结点
     */
    private Node leftRightRotate(Node root) {
        // 对左子树进行RR旋转
        root.left = rightRightRotate(root.left);
        // 对失衡AVL树最低失衡根结点进行LL旋转
        return leftLeftRotate(root);
    }

    /**
     * RL旋转(右左旋转)
     *
     * @param root    失衡AVL树根结点
     * @return        调整后的AVL树根结点
     */
    private Node rightLeftRotate(Node root) {
        // 对左子树进行LL旋转
        root.right = leftLeftRotate(root.right);
        // 对失衡AVL树最低失衡根结点进行RR旋转
        return rightRightRotate(root);
    }

    /**
     * 比较两个子树的最大高度
     *
     * @param a     子树a的高度
     * @param b     子树b的高度
     * @return      子树a和子树b的最大高度
     */
    private int max (int a, int b) {
        return a > b ? a : b;
    }

    /**
     * 获取树的高度
     *
     * @param node      结点
     * @return          树高
     */
    private int height(Node node) {
        if (node != null) {
            return node.height;
        }
        return 0;
    }

    /**
     * 先序遍历AVL树
     */
    public void preOrder() {
        preOrder(this.root);
    }

    /**
     * 先序遍历AVL树
     *
     * @param parent    父结点
     */
    private void preOrder(Node parent) {
        if (parent != null) {
            System.out.print(parent.key + " ");
            preOrder(parent.left);
            preOrder(parent.right);
        }
    }

    /**
     * 中序遍历AVL树
     */
    public void inOrder() {
        inOrder(root);
    }

    /**
     * 中序遍历AVL树
     *
     * @param parent    父结点
     */
    private void inOrder(Node parent) {
        if (parent != null) {
            inOrder(parent.left);
            System.out.print(parent.key + " ");
            inOrder(parent.right);
        }
    }

    /**
     * 后序遍历AVL树
     */
    public void postOrder() {
        postOrder(root);
    }

    /**
     * 后序遍历AVL树
     *
     * @param parent    父结点
     */
    private void postOrder(Node parent) {
        if (parent != null) {
            postOrder(parent.left);
            postOrder(parent.right);
            System.out.print(parent.key + " ");
        }
    }

    /**
     * 查找key
     *
     * @param key   待查找的key
     * @return      查找的key
     */
    public int search(int key) {
        Node node = search(root, key);
        if (node != null) {
            return node.key;
        }
        return -1;
    }

    /**
     * 查找AVL树中值为key的结点
     *
     * @param root  父结点
     * @param key   查找的key
     * @return      查找到的结点
     */
    private Node search(Node root, int key) {
        if (root == null) {
            return null;
        }
        if (key < root.key) {
            return search(root.left, key);
        } else if (key > root.key) {
            return search(root.right, key);
        } else {
            return root;
        }
    }

    /**
     * 从二叉查找树上删除指定元素
     *
     *
     * @param value     待删除元素
     * @return          删除结果
     */
    public boolean remove(int value) {
        Node deleteNode = search(root, value);
        if (deleteNode == null) {
            return false;
        }
        remove(root, deleteNode);
        return true;
    }

    /**
     * 删除结点
     *
     * @param root          父结点
     * @param deleteNode    待删除结点
     * @return              删除后的根结点
     */
    private Node remove(Node root, Node deleteNode) {
        if (root == null || deleteNode == null) {
            return null;
        }
        // 待删除结点值 - 父结点值
        int compare = deleteNode.key - root.key;
        // 待删除的结点在左子树中
        if (compare < 0) {
            root.left = remove(root.left, deleteNode);
            root.left.parent = root;
            // 删除结点后，若AVL树失去平衡，则进行相应的调节
            if (height(root.right) - height(root.left) == 2) {
                // 右子结点
                Node rightChild = root.right;
                if (height(rightChild.left) > height(rightChild.right)) {
                    // RL旋转
                    root = rightLeftRotate(root);
                } else {
                    // RR旋转
                    root = rightRightRotate(root);
                }
            }
            // 待删除的结点在右子树中
        } else if (compare > 0) {
            root.right = remove(root.right, deleteNode);
            if (height(root.left) - height(root.right) == 2) {
                Node leftChild = root.left;
                if (height(leftChild.left) > height(leftChild.right)) {
                    // LL旋转
                    root = leftLeftRotate(root);
                } else {
                    // LR旋转
                    root = leftRightRotate(root);
                }
            }
        } else {
            //root是当前需要删除的结点
            if (root.left != null && root.right != null) {
                // 如果tree的左子树比右子树高，则执行以下：
                if (height(root.left) > height(root.right)) {
                    // (01)找出root的左子树中的最大结点
                    // (02)将该最大结点的值赋值给root
                    // (03)删除该最大结点
                    // 采用这种方式的好处是：删除左子树中最大结点之后，AVL树仍然是平衡的
                    Node max = findMax(root.left);
                    root.key = max.key;
                    root.left = remove(root.left, max);
                    root.left.parent = root;
                } else {
                    // 如果tree的右子树比左子树高，则执行以下：
                    // (01)找出root的右子树中的最小结点
                    // (02)将该最小结点的值赋值给root
                    // (03)删除该最小结点
                    // 采用这种方式的好处是：删除右子树中最小结点之后，AVL树仍然是平衡的
                    Node min = findMin(root.right);
                    root.key = min.key;
                    root.right = remove(root.right, min);
                    root.right.parent = root;
                }
            } else {
                Node temp = root;
                root = root.left != null ? root.left : root.right;
                if (root != null) {
                    root.parent = root.parent.parent;
                }
                temp = null;
            }
        }
        return root;
    }

    /**
     * 查找最小结点：返回node为根结点的AVL树的最小结点
     *
     * @param node      AVL树的父结点
     * @return          最小结点
     */
    private Node findMin(Node node) {
        if (node == null) {
            return null;
        }
        while (node.left != null) {
            node = node.left;
        }
        return node;
    }

    /**
     * 查找最大结点：返回node为根结点的AVL树的最大结点
     *
     * @param node      AVL树父结点
     * @return          最大结点
     */
    private Node findMax(Node node) {
        if (node == null) {
            return null;
        }
        while (node.right != null) {
            node = node.right;
        }
        return node;
    }

}


```
创建AVL树的测试类，验证AVL树的功能。在测试代码中，通过数组中的1～16共16个数字创建了一个如图2-61所示的AVL树。

￼![IMG_2883](https://image.lichongbing.com/IMG_2883.JPG)

图2-61　测试类创建的AVL树示意图

AVL树的测试类代码如下：

```java

/**
 * @Author : zhouguanya
 * @Project : java-interview-guide
 * @Date : 2019-05-06 20:47
 * @Version : V1.0
 * @Description :   AVL树测试
 */
public class AvlTreeDemo {
    public static void main(String[] args) {
        AvlTree avlTree = new AvlTree();
        int[]array = { 3,2,1,4,5,6,7,16,15,14,13,12,11,10,8,9 };
        for (int i = 0; i < array.length; i++) {
            // 添加元素到AVL树
            avlTree.insert(array[i]);
        }
        print(avlTree);
        System.out.println();
        System.out.println("--------在AVL树查找元素12--------");
        System.out.println(avlTree.search(12));
        System.out.println("--------在AVL树查找元素20--------");
        System.out.println(avlTree.search(20));
        System.out.println("--------在AVL树删除元素12--------");
        avlTree.remove(12);
        System.out.println("--------删除元素12后遍历AVL树--------");
        print(avlTree);
    }
    public static void print(AvlTree avlTree) {
        System.out.println("----------中序遍历AVL树----------");
        avlTree.inOrder();
        System.out.println();
        System.out.println("----------先序遍历AVL树----------");
        avlTree.preOrder();
        System.out.println();
        System.out.println("----------后序遍历AVL树----------");
        avlTree.postOrder();
    }
}


```
执行测试代码，执行结果如下：

```
----------中序遍历AVL树----------
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 
----------先序遍历AVL树----------
7 4 2 1 3 6 5 13 11 9 8 10 12 15 14 16 
----------后序遍历AVL树----------
1 3 2 5 6 4 8 10 9 12 11 14 16 15 13 7 
--------在AVL树查找元素12--------
12
--------在AVL树查找元素20--------
-1
--------在AVL树删除元素12--------
--------删除元素12后遍历AVL树--------
----------中序遍历AVL树----------
1 2 3 4 5 6 7 8 9 10 11 13 14 15 16 
----------先序遍历AVL树----------
7 4 2 1 3 6 5 13 10 9 8 11 15 14 16 
----------后序遍历AVL树----------
1 3 2 5 6 4 8 9 11 10 14 16 15 13 7 
```
