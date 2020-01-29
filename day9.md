###  

##### 问题

- 谈谈你对vue组件之间通信的理解？

##### 回答

- 组件间有三种不同情况下组件的通信方式

  - 父子组件通信
  - 兄弟组件通信
  - 跨组件跨模块通信

- 常用的组件通信

  - props

    - 常用，通过prop向子s组件传递数据，单向数据流

  - $emit/\$on  事件总线

    - $emit触发当前实例上的事件，附加参数都会传给监听器回调
    - \$on监听当前实例上自定义事件

  - vuex

  - $attrs/\$listeners

    - $attrs 包含父作用域中不作为prop被识别（且获取）的特性。当一个组件没有声明任何prop时，这里会包含所有父作用域的绑定，并且通过`v-bind="\$attrs"`获取
    - \$listeners 包含父作用域中的 v-on事件监听器。它可以通过 `v-on="$listeners"` 传入内部组件

  - provide & inject

    - 作为高阶插件/组件库提供用例，已允许一个组件组件向其所有子孙后代注入一个依赖，不论组件层次有多深，并在其上下游关系成立的事件里始终生效

  - $parent & \$children

  - 插槽：v-slot

    - 具名插槽

    - 作用域插槽

      ​

    ​

  ​