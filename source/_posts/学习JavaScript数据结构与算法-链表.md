---
title: 学习JavaScript数据结构与算法-链表
date: 2018-03-13 01:48:02
tags:
- 链表
---
## 单向链表（ES5实现）

```JavaScript
    function LinkedList(){

        let Node = function(){
            this.element = element
            this.next = null
        }
        
        let length = 0
        let head = null

        this.append = function(element){
            let node = new Node(element)
            let current

            if(head===null){ //列表中的第一个节点
                head = node
            }else{
                current = head
                //循环列表，直到找到最后一项
                while(current.next){
                    current.next
                }
                //找到最后一项，将其next赋值为node，并建立连接
                current.next = node
            }

            length++
        }

        this.insert = function(positon,element){
            //检查是否越界
            if(position >= 0 && positon<=length){

                let node = new Node(element),
                    current = head,
                    previous,
                    index = 0

                if(popsiton === 0){//将节点添加到头部

                    node.next = current//head
                    head = node

                }else{
                    
                    while(current.next){

                        previous = current
                        current = current.next

                    }
                    node.next = current
                    previous.next = node
                }

                length++

                return true
            }else{
                return false
            }
        }

        this.removeAt = function(positon){
            if(position >=0 && positon < length){
                let current = head,
                    previous,
                    index = 0

                if(position === 0){
                    head = current.next
                }else{
                    while(current.next){
                        previous = current
                        current = current.next
                    }
                    previous.next = current.next
                }
                length--
                return current.element
            }else{
                return null
            }
        }

        this.remove = function(element){
            let index = this.indexOf(element)
            return this.removeAt(index)
        }

        this.indexOf = function(element){
            let current = head,
                index = 0
            while(current){
                if(element === current.element){
                    return index
                }
                index++
                current = current.next
            }
            return -1
        }

        this.isEmpty = function(){
            return length===0
        }

        this.getHead = function(){
            return head
        }

        this.toString = function(){
            let current = head,
                string = ''
            while(current){
                string += current.element + (current.next?',':'')
                current = current.next
            }
            return string
        }

         this.print = function(){
            console.log(this.toString());
        };
    }
```