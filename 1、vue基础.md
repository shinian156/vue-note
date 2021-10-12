### 绑定class
你可以在对象中传入更多属性来动态切换多个 class。此外，v-bind:class 指令也可以与普通的 class 属性共存。
```javascript
// 对象语法
<div v-bind:class="{ active: isActive }"></div>

data: {
    isActive: true,
    hasError: false
}


// 数组语法
<div v-bind:class="[activeClass, errorClass]"></div>

data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}
```
### 绑定style
v-bind:style 的对象语法十分直观——看着非常像 CSS，但其实是一个 JavaScript 对象。CSS 属性名可以用驼峰式 (camelCase) 或短横线分隔 (kebab-case，记得用引号括起来) 来命名。
```javascript
// 对象语法
<div v-bind:style="styleObject"></div>

data: {
  styleObject: {
    color: 'red',
    fontSize: '13px'
  }
}

// 数组语法
<div v-bind:style="[baseStyles, overridingStyles]"></div>
```

### watch 监听

```javascript
watch: {
    data: {
        immediate: true,   //该回调将会在侦听开始之后被立即调用
        deep: true,        //该回调会在任何被侦听的对象的 property 改变时被调用，不论其被嵌套多深
        handler(newValue, oldValue) {

        }
    }
},
```

### 过渡动画
Vue 在插入、更新或者移除 DOM 时，提供多种不同方式的应用过渡效果。包括以下工具：

* 在 CSS 过渡和动画中自动应用 class
* 可以配合使用第三方 CSS 动画库，如 Animate.css
* 在过渡钩子函数中使用 JavaScript 直接操作 DOM
* 可以配合使用第三方 JavaScript 动画库，如 Velocity.js

### 混入

混入 (mixin) 提供了一种非常灵活的方式，来分发 Vue 组件中的可复用功能。一个混入对象可以包含任意组件选项。当组件使用混入对象时，所有混入对象的选项将被“混合”进入该组件本身的选项。(当多个组件中使用到相同的功能时，使用混入非常方便)


``` javascript
// 定义一个混入对象
export default {
	data(){
        type: 1
	},
	methods: {
        hello: function () {
            console.log('hello from mixin!')
        }
    }
}


// 组件中使用

import mixin from 'mixin.js'
mixins: [mixin],

mounted: function(){
    this.hello()                  //'hello from mixin!'
    console.log(this.type)        //1
}

```


### 自定义指令
