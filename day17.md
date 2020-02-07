###  

##### 问题

- 你知道vue双向数据绑定的原理吗？

##### 回答

- vue双向数据绑定是通过 数据劫持 结合 发布订阅模式的方式来实现的。数据和视图同步，数据发生变化，视图跟着变化；视图变化，数据也随之发生改变

- 核心：Object.defineProperty()方法

  - Object.defineProperty(obj, prop, descriptor) 
  - 这个函数内有三个参数，分别为obj--要定义其上属性的对象；prop---要定义或修改的属性；descriptor -- 属性描述符。重点就是最后这个属性描述符
  - descriptor  是一个对象，主要有两种形式，数据描述符合存取描述符，这两种对象只能选择一种使用。而vue使用的get和set就是存取描述符随想的属性

- vue通过Object.defineProperty()中的get和set的操作来实现,在数据变动时发布消息给订阅者，触发相应的监听回调

  - ```javascript
     Object.defineProperty(obj, 'hello', {//定义要修改对象的属性
       get: function () {
         console.log('调用了get方法')
       },
       set: function (newVal) { 
         console.log('调用了set方法')
       }
     });
    obj.hello; // => 调用了get方法
    obj.hello = 'hi' // => 调用了set方法

    ```

    ​

  ​

  ​

  ​

  ​

  ​

  ​

  ​

  ​