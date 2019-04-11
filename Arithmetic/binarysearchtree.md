# 二叉树的js实现
## 相关术语
- 节点：树中每个元素成为节点
- 根节点：整颗树顶点，它没有父节点
- 子节点：节点的后代
- 叶子节点：没有子节点的元素成为叶子节点
- 二叉树：是一个有限元素的集合，该集合或者为空、或者由一个成为根的元素及两个不想交的、被分别成为左右子树的二叉树组成
- 二叉查找树：BST(binarysearchtree),它只允许在左节点存储比父节点小的值、右节点存储比父节点更大的值

## 代码实现
```
class BinarySearchTree{
  constructor(){
    this.root = null;
  }
  insert(key){
    var newNode = new Node(key);
    if(this.root === null){
      var root = newNode;
    }else{
      this.insertNode(this.root, newNode)
    }
  }
  insertNode(node, newNode){
    if(newNode.key <= node.key){
      if(node.left === null){
        node.left = newNode;
      }else{
        this.insertNode(node.left, newNode);
      }
    }else{
      if(node.right === null){
        node.right = newNode;
      }else{
        this.insertNode(node.right, newNode)
      }
    }
  }
}

class Node{
  constructor(key){
    this.key = key;
    this.left = null;
    this.right = null;
  }
}
```
