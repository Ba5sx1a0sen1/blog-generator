---
title: Vue中组件通信
date: 2018-07-14 21:09:25
tags:
 - Vue
 - JavaScript
---

Vue中的组件通信方式大致分为父子组件通信, 由父子组件通信衍生的爷孙组件通信, 还有兄弟间组件通信, 如果组件层级更复杂, 推荐还是使用官方的Vuex进行状态管理

## 父子组件通信
#### 父组件向子组件传递数据

  在子组件中定义props, 父组件通过v-bind将属性传入给子组件, 子组件通过props获取数据, 若想修改子组件的数据, 可在父组件上定义methods修改传入props的数据(传给子组件的数据我们托管在父组件上)
	
		```HTML 
		  <div id="app">
		    <father></father>
		  </div>
		```
		
		```JavaScript
		let vm = new Vue({
		  el:'#app',
		})
		
		Vue.component('father',{
		  data(){
		    return{
		      str:'i am father',
		      sonStr:'i am son'
		    }
		  },
		  template:`
		    <div>
		      {{str}}
		      <son :sonStr='sonStr'></son>
		    </div>
		  `
		})
		
		Vue.component('son',{
		  props:['sonStr'],
		  data(){
		    return{
		      str:this.sonStr
		    }
		  },
		  template:`
		  <div>
		    {{str}}
		  </div>
		  `
		})
		```
		
		显示结果:
		![爸到子](/images/fatherandson.png)

#### 子组件向父组件通信
   
   这种通讯方式也不难实现, 我们要遵循Vue官方的文档所说的给pros的单向数据流, 所以我们要向父组件通信, 需要用到事件发布($emit)与订阅($on), 在子组件上定义发布事件, 在父组件中template中监听事件, 这样便可实现子组件向父组件通信传递数据
   
   ```JavaScript
       Vue.component('father',{
		  data(){
		    return{
		      str:'i am father',
		      sonStr:'i am son'
		    }
		  },
		  template:`
		    <div>
		      {{str}}
		      <son @changeFatherStr="str='我被儿子改啦'" :sonStr='sonStr'></son>
		    </div>
		  `
		})
		
		Vue.component('son',{
		  props:['sonStr'],
		  data(){
		    return{
		      str:this.sonStr
		    }
		  },
		  template:`
		  <div>
		    {{str}}
		    <button @click="$emit('changeFatherStr')">我要改爸爸的字符串</button>
		  </div>
		  `
		})
		
		let vm = new Vue({
		  el:'#app',
		})
   ```
   
   点击更改爸爸字符创按钮, 结果为
   ![子到爸](/images/sonchangefather.png)
  
  
## 爷孙组件通信

假如我们想让孙子组件去改爷爷组件的数据, 我们类似父子组件通信的方法, 先告知孙子的爸爸要改爷爷组件, 爸爸在告知孙子的爷爷要修改哪里, 逐级向上传递

```JavaScript
Vue.component('father',{
  data(){
    return{
      str:'i am father',
      sonStr:'i am son'
    }
  },
  template:`
    <div>
      {{str}}
      <son @changeFatherStr="str='我被儿子改啦'" :sonStr='sonStr'
@eventFromGrandsunPassSon="str='我被孙子改啦'"
></son>
    </div>
  `
})

Vue.component('son',{
  props:['sonStr'],
  data(){
    return{
      str:this.sonStr
    }
  },
  template:`
  <div>
    {{str}}
    <button @click="$emit('changeFatherStr')">我要改爸爸的字符串</button>
    <grandson
      @eventFromGrandsun='$emit("eventFromGrandsunPassSon")'
    ></grandson>
  </div>
  `
})

Vue.component('grandson',{
  template:`
    <div>
      i am grandson
      <button @click='$emit("eventFromGrandsun")'>我要更改爷爷的字符串</button>
    </div>
  `
})

let vm = new Vue({
  el:'#app',
})
```

点击更改爷爷字符串结果为
![孙到爷](/images/grandsonchangefather.png)

## 兄弟组件间通信

兄弟组件的通信, 意思可以理解为同个层级的组件间的通信, 在Vue中, 我们可以通过创建一个让所有组件访问到的一个Vue实例, 这个实例我们成为eventBus(事件总线)或eventHub(时间中心), 用于给同级组件架起桥梁方便通信, 在一个组件中通过这个实例的$emit方法中发起事件, 在另外一个组件中通过这个实例的$on方法订阅事件, 便可方便进行兄弟组件通信

```HTML
  <div id="app">
    <father></father>
    <mother></mother>
  </div>
```

```JavaScript
let eventHub = new Vue()

Vue.component('father',{
  data(){
    return{
      str:'i am father',
      sonStr:'i am son'
    }
  },
  template:`
    <div>
      {{str}}
      <son @changeFatherStr="str='我被儿子改啦'" :sonStr='sonStr'
@eventFromGrandsunPassSon="str='我被孙子改啦'"
></son>
    </div>
  `,
  created(){
    eventHub.$on('callFather',()=>{
      this.str = '我被孩子他妈叫啦'
      //这里的this因为使用了箭头函数, 所以指向的是father组件的实例
      //如果使用es5的匿名函数, 那么this就是指向eventHub
    })
  }
})

Vue.component('mother',{
  data(){
    return{
      str:'i am mother',
    }
  },
  template:`
   <div>
     {{str}}
     <button @click='callFather'>我要叫孩子他爸</button>
   </div>
  `,
  methods:{
    callFather(){
      eventHub.$emit('callFather')
    }
  }
})
```

可以看到我们确实定义了一个事件中心, 用于father与mother这样的同级组件进行通信, 在mother组件中, 通过methods去发布事件, 在father组件的创建阶段中, 我们去订阅事件, 点击我要叫孩子他爸按钮结果为
![孙到爷](/images/mothercallfather.png)

## 总结
以上总结了常见的Vue组件通信的方式, 但是使用场景只是在我们场景不会太过复杂的情况下才比较有效, 如果组件层级太过深, 或者多个兄弟组件间需要相互通信, 像以上这样的爷孙组件与兄弟组件通信方式写出来的代码将会出现非常多的$emit与$on的模板代码, 这个时候我们就要使用官方的Vuex工具进行更好的管理状态, 才能避免我们写出低效且维护性低的代码