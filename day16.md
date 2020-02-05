###  

##### 问题

- 你知道nextTick的原理吗？

##### 回答

- 使用vue中，我们经常使用nextTick,来监听当前dom节点更新完成了，（微任务），然后执行回调，那vue是怎么做到的呢？

  - 定义执行了nextTick的callbacks, 一旦最近的dom节点更新了，则会统一清除所有的callbacks，执行flushCallbacks

    ```javascript
    const callbacks = []
    let pending = false
     
    function flushCallbacks () {
      pending = false
      const copies = callbacks.slice(0)
      callbacks.length = 0
      for (let i = 0; i < copies.length; i++) {
        copies[i]()
      }
    ```

  - 判断怎么是否可以真的使用微任务。

    - 1.首先如果有Promise方法，且该方法是native code，则使用promise来做垫子。因为原生promise是属于微任务范畴，在当前宏观任务执行完成的时候，会去首先执行微任务Promise

      ```javascript

      if (typeof Promise !== 'undefined' && isNative(Promise)) {
        const p = Promise.resolve()
        timerFunc = () => {
          p.then(flushCallbacks)
          if (isIOS) setTimeout(noop)
        }
        isUsingMicroTask = true
      }
      ```

    - 如果当前不存在原生Promise，如果有原生MutationObserver, 则创建一个MutationObserver，创建一个文本节点。然后监听该文本节点。

      因为MutationObserver会监听dom的变化，多次的触发更新dom,只会在dom操作都处理完成之后才回调。

      所以模拟创建一个timeFunc 每次执行，一次，就等MutationObserver的回调来清除nextTick的callback

    ```javascript
    else if (!isIE && typeof MutationObserver !== 'undefined' && (
      isNative(MutationObserver) ||
      // PhantomJS and iOS 7.x
      MutationObserver.toString() === '[object MutationObserverConstructor]'
    )) {
      let counter = 1
      const observer = new MutationObserver(flushCallbacks)
      const textNode = document.createTextNode(String(counter))
      observer.observe(textNode, {
        characterData: true
      })
      timerFunc = () => {
        counter = (counter + 1) % 2
        textNode.data = String(counter)
      }
      isUsingMicroTask = true
    }
    ```

  - 执行nextTick，首先先存储cb，然后如果不是在正在等待flush的情况下，则执行timeFunc，触发下一次更新回调。

    ```javascript

    export function nextTick (cb?: Function, ctx?: Object) {
      let _resolve
      callbacks.push(() => {
        if (cb) {
          try {
            cb.call(ctx)
          } catch (e) {
            handleError(e, ctx, 'nextTick')
          }
        } else if (_resolve) {
          _resolve(ctx)
        }
      })
      if (!pending) {
        pending = true
        timerFunc()
      }
      // $flow-disable-line
      if (!cb && typeof Promise !== 'undefined') {
        return new Promise(resolve => {
          _resolve = resolve
        })
      }
    ```

    ​

  ​	

  ​

  ​

  ​

  ​