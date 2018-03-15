---
title: 学习JavaScript数据结构与算法-树
date: 2018-03-14 00:55:38
tags:
- 算法
---

## 以二叉查找树（BST）为例

二叉搜索树是二叉树的一种，但是它只允许你在左侧节点存储比父节点小的值，在右侧节点存储比父节点大于或等于的值。
这种性质可推导出：一颗二叉搜索树的最小值在最深层最左一个节点，最大值在最右一个节点

```JavaScript
    function BinarySearTree(){//会用到大量的递归
        let Node = function(key){
            this.key = key
            this.left = null
            this.right = null
        }
        let root = null
        this.insert = function(key){//插入节点
            let newNode = new Node(key)
            if(root === null){
                root = newNode
            }else{
                insertNode(root,newNode)
            }
        }
        let insertNode = function(node,newNode){
            if(newNode.key < node.key){
                if(node.left === null){
                    node.left = newNode
                }else{
                    insertNode(node.left,node)
                }
            }else{
                if(newNode.key > noew.key){
                    if(node.right === null){
                        node.right = newNode
                    }else{
                        insertNode(node.right,node)
                    }
                }
            }
        }

        this.getRoot = function(){
            return root
        }

        this.search = function(key){//搜索特定值
            return searchNode(root,key)
        }
        let searchNode = function(node,key){
            if(node === null){
                return false
            }
            if(key < node.key){
                return searchNode(node.left,key)
            }else if(key > node.key){
                return searchNode(node.right,key)
            }else{
                return true
            }
        }

        this.inOrderTraverse = function(callback){//中序遍历
            inOrderTraverseNode(root,callback)
        }
        let inOrderTraverseNode = function(node,callback){
            if(node !== null){
                inOrderTraverseNode(node.left,callback)
                callback(node.key)
                inOrderTraverseNode(node.right,callback)
            }
        }

        this.preOrderTraverse = function(callback){//先序遍历
            preOrderTraverseNode(root, callback)
        }
        var preOrderTraverseNode = function (node, callback) {
            if (node !== null) {
                callback(node.key)
                preOrderTraverseNode(node.left, callback)
                preOrderTraverseNode(node.right, callback)
            }
        }

        this.postOrderTraverse = function(callback){//后序遍历
            postOrderTraverseNode(root, callback)
        }
        var postOrderTraverseNode = function (node, callback) {
            if (node !== null) {
                postOrderTraverseNode(node.left, callback)
                postOrderTraverseNode(node.right, callback)
                callback(node.key)
            }
        }

        this.min = function(){return minNode(root)}
        let minNode = function(node){
            if(node !== null){
                while(node && node.left!==null){
                    node = node.left
                }
                return node.key
            }
            return null
        }

        this.max = function(){return minNode(root)}
        let maxNode = function(node){
            if(node !== null){
                while(node && node.right!==null){
                    node = node.right
                }
                return node.key
            }
            return null
        }
        
        this.remove = function(key){
            root = removeNode(root,key)
        }
        let findMinNode = function(node){
            while(node && node.left!==null){
                node = node.left
            }
            return node
        }

        var removeNode = function(node, element){

            if (node === null){
                return null;
            }

            if (element < node.key){
                node.left = removeNode(node.left, element);
                return node;

            } else if (element > node.key){
                node.right = removeNode(node.right, element);
                return node;

            } else { //element is equal to node.item

                //handle 3 special conditions
                //1 - a leaf node
                //2 - a node with only 1 child
                //3 - a node with 2 children

                //case 1
                if (node.left === null && node.right === null){
                    node = null;
                    return node;
                }

                //case 2
                if (node.left === null){
                    node = node.right;
                    return node;

                } else if (node.right === null){
                    node = node.left;
                    return node;
                }

                //case 3
                var aux = findMinNode(node.right);
                node.key = aux.key;
                node.right = removeNode(node.right, aux.key);
                return node;
            }
        }
    }
```
