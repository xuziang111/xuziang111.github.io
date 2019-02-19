---
title: vue中的slot（插槽）
date: 2019-02-12 09:31:34
tags:
    - vue
---
#未命名插槽
slot未命名时，每个<slot>标签内都会生成父组件中提供的内容。
父组件app.vue
```
<template>
 <div id='app'>
        <slottest>
            <h1>Here might be a page title</h1>
                  
            <p>A paragraph for the main content.</p>
            <p>And another one.</p>
                  
            <p>Here's some contact info</p>
        </slottest>
    </div>
</template>
<script>
import slottest from './components/slottest'
export default {
  data(){
    return {
      
    }
  },
  components:{
    slottest
  }
}
</script>
```
子组件slottest.vue
```
<template>
  <div>
    <slot></slot>
<slot></slot>
  </div> 
</template> 
 
<script>
export default { 
  data(){
    return {
      
    }
  }
}
</script>

<style>

</style>
```
渲染HTML如下
![image.png](1.png)
如果子*组件中*没有包含任何一个 <slot> 元素，则任何传入它的内容都会被抛弃。

#命名插槽
父组件app.vue
```
<template>
    <div id='app'>
            <button-counter></button-counter>
        <slottest>
            <h1 slot="header">Here might be a page title</h1>
                  
            <p>A paragraph for the main content.</p>
            <p>And another one.</p>
                  
            <p slot="footer">Here's some contact info</p>
        </slottest>
    </div>
</template>
<script>
import slottest from './components/slottest'
export default {
  data(){
    return {
      
    }
  },
  components:{
    slottest
  }
}
</script>
```
子组件slottest.vue
```
<template>
  <div>
    <header>
    <slot name="header"></slot>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
  </div> 
</template> 
 
<script>
export default { 
  data(){
    return {
      
    }
  }
}
</script>

<style>

</style>
```
渲染完后html结构
![image.png](2.png)
#默认内容
```
<button type="submit">
  <slot>Submit</slot>
</button>
```
如果父组件为这个插槽提供了内容，则默认的内容会被替换掉。
#作用域插槽 | 带数据的插槽
作用域插槽要求，在slot上面绑定数据。
```
<slot name="up" :data="data"></slot>
 export default {
    data: function(){
      return {
        data: ['zhangsan','lisi','wanwu','zhaoliu','tianqi','xiaoba']
      }
    },
}
```
父组件
```
<template>
  <div class="father">
    <h3>这里是父组件</h3>
    <!--第一次使用：用flex展示数据-->
    <child>
      <template slot-scope="user">
        <div class="tmpl">
          <span v-for="item in user.data">{{item}}</span>
        </div>
      </template>

    </child>

    <!--第二次使用：用列表展示数据-->
    <child>
      <template slot-scope="user">
        <ul>
          <li v-for="item in user.data">{{item}}</li>
        </ul>
      </template>

    </child>

    <!--第三次使用：直接显示数据-->
    <child>
      <template slot-scope="user">
       {{user.data}}
      </template>

    </child>

    <!--第四次使用：不使用其提供的数据, 作用域插槽退变成匿名插槽-->
    <child>
      我就是模板
    </child>
  </div>
</template>
```
子组件
```
<template>
  <div class="child">

    <h3>这里是子组件</h3>
    // 作用域插槽
    <slot  :data="data"></slot>
  </div>
</template>

 export default {
    data: function(){
      return {
        data: ['zhangsan','lisi','wanwu','zhaoliu','tianqi','xiaoba']
      }
    }
}
```
![image.png](3.png)

