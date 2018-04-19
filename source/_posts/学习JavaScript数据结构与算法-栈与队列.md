---
title: 学习JavaScript数据结构与算法-栈与队列
date: 2018-03-11 23:29:58
tags:
- 算法
---
主要使用ES5来实现栈与队列，都是用对象构造器。
## 栈
    ```JavaScript
        function Stack(){
            let items = [] //用数组存储
            this.push = function(element){
                items.push(element)
            }

            this.pop = function(element){
                return items.pop()
            }

            this.peek = function(){
                return items[items.length-1]
            }
            
            this.isEmpty = function(){
                return items.length === 0
            }

            this.size = function(){
                return items.length
            }

            this.clear = function(){
                while(items[items.length-1]){
                    items.pop()
                }  
            }

            this.print = functon(){
                console.log(items.toString())
            }
        }
    ```

## 队列

    ```JavaScript
        function Queue(){
            let items = []

            this.enqueue = function(element){
                items.push(element)
            }

            this.dequeue = function(){
                return items.shift()
            }

            this.front = function(){
                return items[0]
            }

            this.isEmpty = function(){
                return items.length === 0
            }

            this.clear = function(){
                items = []
            }

            this.size = function(){
                return items.length
            }

            this.print = function(){
                console.log(items.toString())
            }
        }
    ```

## 用栈解决一些实际问题

### 进制转换

```JavaScript
    function divideBy2(decNumber){//将十进制数转为二进制数
        let remStack = new Stack(),rem,binaryString=''

        while(decNumber > 0){
            rem = Math.floor(decNumber%2)
            remStack.push(rem)
            decNumber = Math.floor(decNumber/2)
        }

        while(!remStack.isEmpty()){
            binaryString += remStack.pop().toString()
        }

        return binaryString
    }

    function baseConverter(decNumber,base){//
        let remStack = new Stack(),rem,baseString = '',digits = '012345678ABCDEF'

        while(decNumber > 0){
            rem = Math.floor(decNumber % base)
            remStack.push(rem)
            decNumber = Math.floor(decNumber / base)
        }

        while(!remStack.isEmpty()){
            baseString += digits += digits[remStack.pop()]
        }
        
        return baseString
    }
```

## 用队列解决一些实际问题

### 优先队列
```JavaScript
    function PriorityQueue(){
        let items = []

        function QueueElement(element,priority){
            this.element = element
            this.priority = priority
        }

        this.enqueue = function(element,priority){
            let queueElement = new QueueElement(element,priority)

            let added = false
            for(let i = 0; i < items.legth; i++){
                if(queueElement.priority < items[i].priority){
                    items.splice(i,0,queueElement)
                    added = true
                    break
                }
            }
            if(!added){
                items.push(queueElement)
            }
        }

        this.dequeue = function(){
            return items.shift()
        }

        this.front = function(){
            return items[0]
        }

        this.isEmpty = function(){
            return items.length === 0
        }

        this.size = function(){
            return items.length
        }

        this.print = function(){
            items.forEach((obj,key)=>{
                console.log(`${obj[key].element}-${obj[key].priority}`)
            })
        }
    }
```