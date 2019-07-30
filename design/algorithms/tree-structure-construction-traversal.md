# Tree structure \(construction, traversal\)

**Trees**: Unlike Arrays, Linked Lists, Stack and queues, which are linear data structures, trees are hierarchical data structures. 

**Tree Vocabulary**: The topmost node is called _**root**_ of the tree. The elements that are directly under an element are called its _**children**_. The element directly above something is called its _**parent**_. For example, ‘a’ is a child of ‘f’, and ‘f’ is the parent of ‘a’. Finally, elements with no children are called _**leaves**_.

Tree is a hierarchical data structure. Main uses of trees include maintaining hierarchical data, providing moderate access and insert/delete operations. Binary trees are special cases of tree where every node has at most two children.

```text
      tree
      ----
       j    <-- root
     /   \
    f      k  
  /   \      \
 a     h      z    <-- leaves
```

* One reason to use trees might be because you want to store information that naturally forms a hierarchy. For example, the file system on a computer:

```text
file system
-----------
     /    <-- root
  /      \
...       home
      /          \
   ugrad        course
    /       /      |     \
  ...      cs101  cs112  cs113  
```

* Trees \(with some ordering e.g., BST\) provide moderate access/search \(quicker than Linked List and slower than arrays\).
* Trees provide moderate insertion/deletion \(quicker than Arrays and slower than Unordered Linked Lists\).
* Like Linked Lists and unlike Arrays, Trees don’t have an upper limit on number of nodes as nodes are linked using pointers.

Main applications of trees include:

1. Manipulate hierarchical data.
2. Make information easy to search \(see tree traversal\).
3. Manipulate sorted lists of data.
4. As a workflow for compositing digital images for visual effects.
5. Router algorithms
6. Form of a multi-stage decision-making \(see business chess\).

Binary Tree: A tree whose elements have at most 2 children is called a binary tree. Since each element in a binary tree can have only 2 children, we typically name them the left and right child.

#### Properties

* The maximum number of nodes at level ‘l’ of a binary tree is 2l-1.
* Maximum number of nodes in a binary tree of height ‘h’ is 2h – 1.
* In a Binary Tree with N nodes, minimum possible height or minimum number of levels is Log2\(N+1\)
* In Binary tree where every node has 0 or 2 children, number of leaf nodes is always one more than nodes with two children.

Бинарное дерево — это иерархическая структура данных, в которой каждый узел имеет значение \(оно же является в данном случае и ключом\) и ссылки на левого и правого потомка. Узел, находящийся на самом верхнем уровне \(не являющийся чьим либо потомком\) называется корнем. Узлы, не имеющие потомков \(оба потомка которых равны NULL\) называются листьями.

![binary-tree-ex](https://softserveke.firebaseapp.com/assets/img/binary-tree-ex.b8cc8d8c.png)

Бинарное дерево поиска — это бинарное дерево, обладающее дополнительными свойствами: значение левого потомка меньше значения родителя, а значение правого потомка больше значения родителя для каждого узла дерева. То есть, данные в бинарном дереве поиска хранятся в отсортированном виде. При каждой операции вставки нового или удаления существующего узла отсортированный порядок дерева сохраняется. При поиске элемента сравнивается искомое значение с корнем. Если искомое больше корня, то поиск продолжается в правом потомке корня, если меньше, то в левом, если равно, то значение найдено и поиск прекращается.

![binary-tree-past](https://softserveke.firebaseapp.com/assets/img/binary-tree-past.391ffca2.png)

Поиск минимального значения невероятно прост — это всегда самый левый узел, то есть мы пробегаем по всем потомкам, если у потомка есть левый лист, значит бежим по его потомкам. Как только мы видим, что потомков нет — вуаля, у нас самое маленькое значение

![binary-min](https://softserveke.firebaseapp.com/assets/img/binary-min.6b780d08.png)

Тоже самое с самым большим значением — оно всегда самое правое

![binary-max](https://softserveke.firebaseapp.com/assets/img/binary-max.7d24271d.png)

Поиск элемента тоже очень прост:

1. Как обычно начинаем с корневого элемента.
2. Проверяем или даный элемент — тот который нам нужен. Если да — возвращаем
3. и нет: смотрим или он больше даного, или меньше. Идем к соответствующему листу
4. Если листов нет — элемента нет. Если есть — повторяем пункт 2.

### Traversals

Unlike linear data structures \(Array, Linked List, Queues, Stacks, etc\) which have only one logical way to traverse them, trees can be traversed in different ways. Following are the generally used ways for traversing trees.

![tree-example](data:image/gif;base64,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)

Depth First Traversals:

* \(a\) Inorder \(Left, Root, Right\) : 4 2 5 1 3
* \(b\) Preorder \(Root, Left, Right\) : 1 2 4 5 3
* \(c\) Postorder \(Left, Right, Root\) : 4 5 2 3 1

Breadth First or Level Order Traversal : 1 2 3 4 5

**Inorder Traversal \(Practice\):**

```text
Algorithm Inorder(tree)
   1. Traverse the left subtree, i.e., call Inorder(left-subtree)
   2. Visit the root.
   3. Traverse the right subtree, i.e., call Inorder(right-subtree)
```

In case of binary search trees \(BST\), Inorder traversal gives nodes in non-decreasing order. To get nodes of BST in non-increasing order, a variation of Inorder traversal where Inorder traversal s reversed can be used.

**Example**: Inorder traversal for the above-given figure is 4 2 5 1 3.

**Preorder Traversal \(Practice\):**

```text
Algorithm Preorder(tree)
   1. Visit the root.
   2. Traverse the left subtree, i.e., call Preorder(left-subtree)
   3. Traverse the right subtree, i.e., call Preorder(right-subtree)
```

Preorder traversal is used to create a copy of the tree. Preorder traversal is also used to get prefix expression on of an expression tree. **Example**: Preorder traversal for the above given figure is 1 2 4 5 3.

**Postorder Traversal \(Practice\):**

```text
Algorithm Postorder(tree)
   1. Traverse the left subtree, i.e., call Postorder(left-subtree)
   2. Traverse the right subtree, i.e., call Postorder(right-subtree)
   3. Visit the root.
```

Postorder traversal is used to delete the tree. Please see the question for deletion of tree for details. Postorder traversal is also useful to get the postfix expression of an expression tree.

**Example**: Postorder traversal for the above given figure is 4 5 2 3 1.

