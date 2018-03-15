---
title: 学习JavaScript数据结构与算法-集合
date: 2018-03-13 02:16:32
tags:
- 算法
---
## 集合

```JavaScript
    function Set(){
        let items = {}

        this.add = function(){
            if(!this.has(value)){
                items[value] = value
                return true
            }
            return false
        }

        this.delete = function(value){
            if(this.has(value)){
                delete items[value]
                return true
            }
            return false
        }

        this.has = function(value){
            return items.hasOwnProperty(value)
        }

        this.clear = function(){//清空集合
            items = {}
        }

        this.size = function(){//返回集合的长度
            return Object.keys(items).length
        }

        this.values = function(){//返回集合中的元素，以数组格式返回
            let values = []
            let keys = Object.keys(items)
            for(let i = 0; i < keys.length; i++){
                values.push(items[keys[i]])
            }
            return values
        }

        this.getItems = function(){//取得当前集合
            return items;
        };

        this.union = function(otherSet){//求并集
            let unionSet = new Set()
            let values = this.values()
            for(let i = 0; i < values.length; i++){
                unionSet.add(values[i])
            }
            values = otherSet.values()
            for(let i = 0; i < values.length; i++){
                unionSet.add(values[i])
            }
            return unionSet
        }

        this.intersection = function(ohterSet){//求交集
            let intersectionSet = new Set()
            let values = this.values()
            for(let i = 0; i < values.length; i++){
                if(otherSet.has(values[i])){
                    intersectionSet.add(values[i])
                }
            }
            return intersectionSet
        }

        this.difference = function(otherSet){//求差集
            let differenceSet = new Set(); //{1}

            let values = this.values();
            for (let i=0; i<values.length; i++){ //{2}
                if (!otherSet.has(values[i])){    //{3}
                    differenceSet.add(values[i]); //{4}
                }
            }
            return differenceSet;
        };

        this.isSubSetOf = function(otherSet){//判断是否是另一个集合的子集
            if (this.size() > otherSet.size()){
                return false;
            } else{
                let values = this.values()
                for(let i = 0; i<values.length; i++){
                    if(!otherSet.has(values[i])){//另一个集合没有此集合中的值，即false
                        return false
                    }
                }
                return true
            }
        }

    }
```
