# 如何优雅的旋转平衡二叉树

*文章来自[知乎](https://zhuanlan.zhihu.com/p/438604092)*

![LL Rotate](https://pic2.zhimg.com/v2-d444cbe0b2f2ed0d74547a7ec38f1d51_r.jpg)

![RR Rotate](https://pic3.zhimg.com/v2-9811412ad54dce2c0d6abaa840187d6a_r.jpg)

平衡二叉树 是 二叉搜索树 的一种。之所以平衡，是因为它的每一个结点的 左子树的高度 和 右子树的高度 差至多为 1。

我们将二叉树上的结点的 左子树高度 减去 右子树高度 的值称为 平衡因子，即 BF（Balance Factor）。 根据平衡二叉树的定义，树上所有结点的平衡因子只可能是 -1、0 和 1。即只要二叉树上有一个结点的平衡因子的绝对值大于 1，则该二叉树就是不平衡的。如图所示，图中每个结点左上角的数值就是它的平衡因子。

## AVL 存储结构

AVL树也是一种**二叉树**，所以左右孩子结点，一定是要存储的，不然无法快速进行树的遍历。其次，它是**二叉搜索树**，所以数据域也是必须的。必须满足左子树的根结点的数据域小于根结点的数据域，右子树的根结点的数据域大于根结点的数据域。每个结点的平衡因子不需要存储。

```cpp
typedef struct KeyValue {           // (1)
    int key;
    int value;
}KeyValue;

typedef KeyValue DataType;          // (2)

typedef struct TreeNode {
    DataType data;                  // (3)
    int height;                     // (4) 
    struct TreeNode* left, * right; // (5) 
}TreeNode;                          // (6)
```

- (1) 树结点的 数据域 设计成一个键值对，其中 key 用来作为二叉搜索树的排序依据，value 作为实际的数据存储域；
- (2) DataType作为键值对KeyValue的别名，作为TreeNode数据域的类型；
- (3) data为 AVL 树的数据域，数据类型要求能够比较大小，下文会实现一个对DataType这种类型进行关系运算的接口；
- (4) height存储树的高度；
- (5) left和right分别表示当前结点的左、右孩子结点的指针；
- (6) 这里的目的是为了能将TreeNode替代struct TreeNode，定义结点类型时，可以少写一个struct字段；

## API

创建节点

```cpp
TreeNode* AVLCreateNode(DataType data) {
    TreeNode* node = (TreeNode*)malloc(sizeof(TreeNode));
    node->data = data;
    node->height = 1;
    node->left = node->right = NULL;
    return node;
}
```

递归获取高度

```cpp
int AVLGetHeight(TreeNode* node) {
    if (node == NULL)
        return 0;
    return node->height;
}
```

## 旋转操作

- 1）LL，根结点的平衡因子 +2，左子树根结点平衡因子 +1；
- 2）RR，根结点的平衡因子 -2，右子树根结点平衡因子 -1；
- 3）LR，根结点的平衡因子 +2，左子树根结点平衡因子 -1；
- 4）RL，根结点的平衡因子 -2，右子树根结点平衡因子 +1；

LL，即往**左子树的左子树插入一个结点**。这种情况下，如果树出现了不平衡的情况，根结点的当前平衡因子一定是 +2。

![](https://pic2.zhimg.com/v2-d444cbe0b2f2ed0d74547a7ec38f1d51_r.jpg)

- 1）结点 T 和 L 交换了父子关系，参见图中的 「 绿色箭头 」；
- 2）T3 的父结点从原先的 L 变成了 T ，参见图中的「 橙色箭头 」；
- 3）树的根结点，从原先的 T ，变成了 L ；

```cpp
PTreeNode RRotate(PTreeNode T) {
    PTreeNode L = T->left;  // (1) 
    T->left = L->right;     // (2) 
    L->right = T;           // (3) 
    AVLCalcHeight(T);       // (4) 
    AVLCalcHeight(L);       // (5) 
    return L;               // (6) 
}
```

RR，即往右子树的右子树插入一个结点。这种情况下，如果树出现了不平衡的情况，根结点的当前平衡因子一定是 -2。

![](https://pic3.zhimg.com/v2-9811412ad54dce2c0d6abaa840187d6a_r.jpg)

- 1）结点 T 和 R 交换了父子关系，参见图中的 「 绿色箭头 」；
- 2）T2 的父结点从原先的 R 变成了 T ，参见图中的「 橙色箭头 」；
- 3）树的根结点，从原先的 T ，变成了 R ；


```cpp
TreeNode* LRotate(TreeNode *T) { 
    TreeNode* R = T->right; // (1)
    T->right = R->left;     // (2) 
    R->left = T;            // (3)
    AVLCalcHeight(T);       // (4) 
    AVLCalcHeight(R);       // (5)  
    return R;               // (6)
}
```

LR，即往左子树的右子树插入一个结点。这种情况下，如果树出现了不平衡的情况的话，根结点的当前平衡因子一定是 +2。

![](https://pic3.zhimg.com/v2-8e34a49bc79e3161baf92408cc3a4fa6_r.jpg)

- 1）将树 T 的左子树 进行左旋；
- 2）将树 T 进行右旋；

```cpp
TreeNode* AVLTreeLR(TreeNode *T) {
    T->left = LRotate(T->left);   // (1)
    return RRotate(T);            // (2)
}
```

RL，即往右子树的左子树插入一个结点。这种情况下，如果树出现了不平衡的情况的话，根结点的当前平衡因子一定是 -2。

![](https://pic4.zhimg.com/v2-df74e089f93ee47b6afde3203f0aef3b_r.jpg)

- 1）将树 T 的右子树 进行右旋；
- 2）将树 T 进行左旋；

```cpp
TreeNode* AVLTreeRL(TreeNode *T) {
    T->right = RRotate(T->right);    // (1)
    return LRotate(T);               // (2)
}
```

AVL 的四种旋转操作（左旋、右旋、两个双旋），代码其实很短，都没有超过三行代码，理解以后很简单。

```c
// LL 型 
TreeNode* AVLTreeLL(TreeNode* T) {
    return RRotate(T);
}

// RR 型 
TreeNode* AVLTreeRR(TreeNode* T) {
    return LRotate(T);
}

// LR 型 
TreeNode* AVLTreeLR(TreeNode* T) {
    T->left = LRotate(T->left);
    return RRotate(T);
}

// RL 型
TreeNode* AVLTreeRL(TreeNode* T) {
    T->right = RRotate(T->right);
    return LRotate(T);
}
```

## 算法

### 查找

```c
bool AVLFind(TreeNode* T, DataType data) {
    int cmpResult;
    if (T == NULL) {
        return false;                        // (1)
    }
    cmpResult = CompareData(&data, &T->data);// (2)
    if (cmpResult < 0) {
        return AVLFind(T->left, data);       // (3)
    }
    else if (cmpResult > 0) {
        return AVLFind(T->right, data);      // (4)
    }
    return true;                             // (5)
}
```

(1) 若为空树，直接返回false；

(2) 这是一个比较的三值函数，cmpResult为比较结果，只有三种情况 -1、0、1；

(3) data小于 树根结点的数据域，说明data对应的结点不在根结点，也不在右子树上，则递归返回左子树的 查找 结果；

(4) data大于 树根结点的数据域，说明data对应的结点不在根结点，也不在左子树上，则递归返回右子树的 查找 结果；

(5) data等于 树根结点的数据域，则直接返回true

```c
TreeNode* AVLGetMax(TreeNode* T) {
    while (T && T->right)  // (1)
        T = T->right;      // (2)
    return T;              // (3)
}

TreeNode* AVLGetMin(TreeNode* T) {
    while (T && T->left)   // (1)
        T = T->left;       // (2)
    return T;              // (3)
}
```

### 平衡

```c
TreeNode* AVLBalance(TreeNode* T) {
    int bf = AVLGetBalanceFactor(T);

    if (bf > +1) {
        if (AVLGetBalanceFactor(T->left) > 0)
            T = AVLTreeLL(T);                 // (1) LL
        else
            T = AVLTreeLR(T);                 // (2) LR
    }
    if (bf < -1) {
        if (AVLGetBalanceFactor(T->right) > 0)
            T = AVLTreeRL(T);                 // (3) RL
        else
            T = AVLTreeRR(T);                 // (4) RR
    }
    AVLCalcHeight(T);                         // (5)
    return T;                                 // (6) 
}
```

### 插入

对于要插入的数据data，从根结点出发，分情况依次判断：

1）若为空树，则创建一个值为data的结点并且返回；

2）data的值 等于 树根结点的值，无须执行插入，直接返回根结点；

3）data的值 小于 树根结点的值，那么插入位置一定在 左子树，递归执行插入左子树的过程，并且返回插入结果作为新的左子树；

4）data的值 大于 树根结点的值，那么插入位置一定在 右子树，递归执行插入右子树的过程，并且返回插入结果作为新的右子树；

5）最后，对于 3） 和 4） 这两步，需要对树执行 平衡 操作。

```c
TreeNode* AVLInsert(TreeNode* T, DataType data) {
    int cmpResult;
    if (T == NULL) {
        // (1) 若为空树，则创建一个值为data的结点并且返回
        T = AVLCreateNode(data);               // (1) 
        return T;
    }
    cmpResult = CompareData(&data, &T->data);
    if (cmpResult == 0) {
        // (2) data的值 等于 树根结点的值，无须执行插入，直接返回根结点
        return T;                              // (2) 
    }
    else if (cmpResult < 0) {
        // (3) 往左子树插入
        T->left = AVLInsert(T->left, data);    // (3) 
    }
    else {
        // (4) 往右子树插入
        T->right = AVLInsert(T->right, data);  // (4) 
    }
    return AVLBalance(T);                      // (5) 
}
```

### 删除

删除结点比插入结点稍微复杂一点，而且由于删除也会导致树的不平衡，所以需要和插入结点一样，判断平衡性并且调整平衡。

为了简化问题，我把删除结点抽象成了两个过程：删除根结点 和 删除非根结点。并且进行分开讨论。

**删除值为data的结点的过程**，从根结点出发，总共四种情况依次判断：

1）空树，不存在结点，直接返回空树NULL；

2）data的值 等于 树根结点的值，则调用 删除根结点 的接口，这个过程下文会详细介绍；

3）data的值 小于 树根结点的值，则需要删除的结点一定不在右子树上，递归调用删除左子树的对应结点，并且将删除结点返回的子树作为新的左子树；

4）data的值 大于 树根结点的值，则需要删除的结点一定不在左子树上，递归调用删除右子树的对应结点，并且将删除结点返回的子树作为新的右子树；

5）最后，对于 3） 和 4） 这两步，需要对树执行 平衡 操作。

**删除它的根结点**，需要保证它还是一棵二叉平衡树，则有如下四种情况：

1）空树，无法执行删除，返回空；

2）叶子结点，释放该结点空间后，返回空；

3）只有左子树时，将根结点空间释放后，返回左子树；

4）只有右子树时，将根结点空间释放后，返回右子树；

5）当左右子树都有时，根据左右子树的平衡性分情况讨论：如果左子树更高，则从左子树选择最大值替换根结点，并且递归删除左子树对应结点；右子树更高，则从右子树选择最小值替换根结点，并且递归删除右子树对应结点；

6）最后，重新计算当前结点的树高，并且返回根结点；

```c
TreeNode* AVLRemoveRoot(TreeNode* T) {

    TreeNode* retNode;
    if (T == NULL) {
        return NULL;                    // (1) 
    }
    if (!T->left && !T->right) {        // (2) 
        free(T);
        return NULL;
    }
    else if (T->left && !T->right) {    // (3)  
        retNode = T->left;
        free(T);
        return retNode;
    }
    else if (!T->left && T->right) {    // (4) 
        retNode = T->right;
        free(T);
        return retNode;
    }
    if (AVLGetHeight(T->left) > AVLGetHeight(T->right)) {  // (5) 
        T->data = AVLGetMax(T->left)->data;
        T->left = AVLRemove(T->left, T->data);
    }else {                                                // (6) 
        T->data = AVLGetMin(T->right)->data;
        T->right = AVLRemove(T->right, T->data);
    }
    AVLCalcHeight(T);                   // (7)
    return T;
}
```

(1) 空树，无法执行删除，返回空；

(2) 叶子结点，释放该结点空间后，返回空；

(3) 只有左子树时，将根结点空间释放后，返回左子树；

(4) 只有右子树时，将根结点空间释放后，返回右子树；

(5) - (6) 当左右子树都有时，根据左右子树的平衡性分情况讨论：如果左子树更高，则从左子树选择最大值替换根结点，并且递归删除左子树对应结点；右子树更高，则从右子树选择最小值替换根结点，并且递归删除右子树对应结点；

(7) 最后，重新计算当前结点的树高，并且返回根结点；