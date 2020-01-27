###  

##### 问题

- 谈谈你对MVC、MVP和MVVM的理解？

##### 回答

- MVC模式

  - 是模型-视图-控制器(Mode-View-Controller)的缩写，是一种设计模式，它强制性的把应用程序的输入、处理和输出分开。所谓的MVC就是，我们把代码按照视图、数据模型和控制器的方式进行分离，视图控制网页界面，数据模型控制数据，控制器就是联系数据和模板之间如何工作的逻辑代码
  - 可以分为
    - 视图：用户看到并与之交互的界面。视图向用户显示相关的数据，并接受用户的输入，视图层不接受任何业务逻辑的处理
    - 模型：数据保存
    - 控制器：业务逻辑
  - MVC的一般流程是：View界面触发事件，传送指令到Controller --> Controller完成业务逻辑后，要求Model改变状态 --> Model将新的数据发送到View, 用户得到反馈

- MVP模式

  - MVP是MVC的分化。MVC中，随着需求变得庞大，需求的变化也变得频繁，controller就会变得很庞大，越来越难以维护。此时出现了MVP模式，也就是Model-View-Presenter
  - Presenter：与Controller一样，接受View的命令，对Model进行操作，不同的是，Presenter会反作用于View, Model的变更通知首先被Presenter获得，然后Presenter再去更新View，一个Presenter只对应一个View。
  - 它对MVC的改进思想为：切断View和Model的联系，让View和Presenter交互，减少在需求变化中需要维护的对象的数量

- MVVM模式

  - 是Model-View-ViewModel的缩写
  - ViewModel：大致就是MVP中的Presenter和Controller了，而View和ViewModel之间没有了mvp的界面接口，而是直接交互，这种模式的关键技术就是数据绑定，View的变化会直接影响ViewModel，ViewModel的变化或者内容也会直接体现在View上。数据绑定可以认为是Observer模式或者是Publish/Subscribe模式，原理都是为了用一种统一的集中方式实现频繁需要被实现的数据更新问题。
  - 比起MVP，MVVM不仅简化了业务和界面的依赖关系，还优化了数据频繁更新的解决方案

  ​

  ​

  ​

  ​

