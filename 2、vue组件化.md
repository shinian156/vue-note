### 父传子

### props

```vue
//child
props: {
  msg: String;
}

// parent
<HelloWorld msg="Welcome to Your Vue.js App" />;
```

### refs

```vue
// parent
<HelloWorld ref="hw" />

this.$refs.hw.xx
```


### 子传父

``` vue
// child
this.$emit('add', good)

// parent
<div @add="cartAdd($event)"></div>
```

### .sync 传参绑定

.sync 其实也是事件传参的语法糖，父组件 以这样的形式@update:msg="changeEmit" 子组件 this.$emit('update:msg',this.msg)进行触发 而sync是可以进行简写的

```vue 
// 父组件
<template>
    <div class="hello">
        {{msg}}
        <son @update:msg="changeEmit"></son>
        //这下面是上面的语法糖，可以简写成这样
        <son :msg.sync="msg"></son>
    </div>
</template>
<script>
    import son from './son.vue'
    export default {
        components:{
            son
        },
        data(){
            return{
                msg:"我是父亲"
            }
        },
        methods:{
            changeEmit(value){
                this.msg = value
            }
        }
    }
</script>
// 子组件
<template>
     <div>{{msg}}</div>
</template>
<script>
    export default {
        data(){
             return{
                  msg:"我是儿子emit"
             }
        },
         mounted() {
              this.$emit('update:msg',this.msg)
         }
    }
</script>

```

### 兄弟组件：通过共同祖辈组件

通过共同的祖辈组件搭桥，$parent或$root。

```javascript
// brother1
this.$parent.$on("foo", handle);
// brother2
this.$parent.$emit("foo");
```

<!-- ### EventBus

EventBus 又称为事件总线。在Vue中可以使用 EventBus 来作为沟通桥梁的概念， 就像是所有组件共用相同的事件中心，可以向该中心注册发送事件或接收事件， 所以组件都可以上下平行地通知其他组件，但也就是太方便所以若使用不慎， 就会造成难以维护的灾难，因此才需要更完善的Vuex作为状态管理中心，将通知的概念上升到共享状态层次。

平常我们采用更多的是父传子，子传父，当遇到兄弟之间的组件通信的时候 就可以使用EventBus
如下例 Vue.prototype.$EventBus = new Vue() 这句话的意思是 因为Vue的原型上有$on $emit 方法 继承自vue原型上的方法，实现一个发布订阅模式
```vue
// main.js
//这句话的意思是 因为Vue的原型上有$on $emit 方法 继承自vue原型上的方法，实现一个发布订阅模式
Vue.prototype.$EventBus = new Vue()
// 父组件-----------------
<template>
    <div class="hello">
        {{msg}}
        <son></son>
        <son1></son1>
    </div>
</template>
<script>
    import son from './son.vue'
    import son1 from './son1.vue'
    export default {
        components:{
            son,
            son1
        },
        data(){
            return{
                msg:"我是父亲"
            }
        },

    }
</script>

// 子组件son------------------------
<template>
     <div>
          <span>{{sonValue}}</span>
     </div>
</template>
<script>
    export default {
        data(){
          return{
               sonValue:"我是son1"
          }
        },
         mounted() {
             this.$EventBus.$on('son1',(val)=>{
                  this.sonValue = val
             })
         }
    }
</script>

// 子组件son1----------------
<template>
     <div>
          <span>{{sonValue}}</span>
          <button @click="btn">在son1里面改变son的值</button>
     </div>
</template>
<script>
    export default {
        data(){
          return{
               sonValue:"我是son2"
          }
        },
         methods:{
             btn(){
                  this.$EventBus.$emit('son1','在son1里面改变son的值')
             }
         }
    }
</script>
``` -->

### 祖先和后代之间

provide/inject：能够实现祖先给后代传值

```javascript
// ancestor
provide() {    
    return {foo: 'foo'}
}

// descendant
inject: ['foo']
```

### dispatch：后代给祖先传值

``` javascript
//定义一个dispatch方法，指定要派发事件名称和数据
function dispatch(eventName, data) {
  let parent = this.$parent;
  // 只要还存在父元素就继续往上查找
  while (parent) {
    // 父元素用$emit触发
    parent.$emit(eventName, data);
    // 递归查找父元素
    parent = parent.$parent;
  }
}

// 使用，HelloWorld.vue
<h1 @click="dispatch('hello', 'hello,world')">{{ msg }}</h1>

// App.vue
this.$on('hello', this.sayHello)
```

### 任意两个组件之间：事件总线 或 vuex

事件总线：创建一个 Bus 类负责事件派发、监听和回调管理

```javascript
// Bus：事件派发、监听和回调管理
class Bus {
  constructor() {
    // {
    //   eventName1:[fn1,fn2],
    //   eventName2:[fn3,fn4],
    // }
    this.callbacks = {};
  }
  $on(name, fn) {
    this.callbacks[name] = this.callbacks[name] || [];
    this.callbacks[name].push(fn);
  }
  $emit(name, args) {
    if (this.callbacks[name]) {
      this.callbacks[name].forEach(cb => cb(args));
    }
  }
}

// main.js
Vue.prototype.$bus = new Bus()

// child1 
this.$bus.$on('foo', handle) 
// child2 
this.$bus.$emit('foo')
```

vuex：创建唯一的全局数据管理者 store，通过它管理数据并通知组件状态变更

### 双向数据绑定v-modle

一个组件上的 v-model 默认会利用名为 value 的 prop 和名为 input 的事件，但是像单选框、复选框等类型的输入控件可能会将 value attribute 用于不同的目的。model 选项可以用来避免这样的冲突：

``` javascript
Vue.component('base-checkbox', {
  model: {
    prop: 'checked',
    event: 'change'
  },
  props: {
    checked: Boolean
  },
  template: `
    <input
      type="checkbox"
      v-bind:checked="checked"
      v-on:change="$emit('change', $event.target.checked)"
    >
  `
})
```

组件中使用v-modle

### 插槽 solt


$attr    

利用 v-bind = "$attrs"     展开多个属性
