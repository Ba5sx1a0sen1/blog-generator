---
title: 学习JavaScript数据结构与算法-字典和散列表
date: 2018-03-13 17:59:19
tags:
- 算法
---
## 字典

字典与集合不同，集合中存储的是`[值，值]`,而我们在字典中存储的是`[键，值]对`，所以我们不能用数组来存储，而要用一个哈希（即JS中的对象）来存储

```JavaScript
    function Dictionary(){
        let items = {}
        this.set = function(key,value){
            items[key] = value//添加获更新
        }
        this.delete = function(key){
            if(this.has(key)){
                delete items[key]
                return true
            }
            return false
        }
        this.has = function(key){
            return key in items
        }
        this.get = function(key){
            return this.has(key)?items[key]:undefined
        }
        this.clear = function(){
            items = {}
        }
        this.size = function(){
            return Object.keys(items).length
        }
        this.keys = function(){
            return Object.keys(items)
        }
        this.values = function(){
            let values = []
            for(key in items){
                if(this.has(key)){//过滤原型继承而来的属性
                    value.push(items[key])                    
                }
            }
            return values
        }
        this.getItems = function(){
            return items
        }
    }
```

## 散列表
```JavaScript
    function HashTable(){
        let table = []
        this.put = function(key,value){
            var position = loseloseHashCode(key)
            console.log(`${position}-${key}`)
            table[position] = value
        }
        this.remove = function(key){
             table[loseloseHashCode(key)] = undefined
        }
        this.get  = function(key){
            return table[loseloseHashCode(key)]
        }

        function loseloseHashCode(key){//散列算法
            var hash = 0
            for(var i = 0; i < key.length; i++){
                hash += key.charCodeAt(i)
            }
            return hash 
            //|| return hash % 37
        }
    }
```