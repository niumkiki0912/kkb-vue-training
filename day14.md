###  

##### 问题

- 谈谈对vue生命周期的理解？

##### 回答

- 每个Vue实例在创建时都会经过一系列的初始化过程，vue的生命周期钩子，就是说在达到某一阶段或条件时去触发的函数，目的就是为了完成一些动作或者事件

- vue生命周期的四个阶段

  - create阶段：vue实例被创建
    - beforeCreate: 创建前，此时data和methods中的数据都还没有初始化
    - created： 创建完毕，data中有值，未挂载
  - mount阶段：vue实例被挂载到真实DOM节点
    - beforeMount：可以发起服务端请求，去数据
    - mounted:  此时可以操作Dom
  - update阶段：当vue实例里面的data数据变化时，触发组件的重新渲染
    - beforeUpdate
    - updated
  - destroy阶段：vue实例被销毁
    - beforeDestroy：实例被销毁前，此时可以手动销毁一些方法
    - destroyed

  ​